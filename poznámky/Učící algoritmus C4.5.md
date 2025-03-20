---
téma: ML
tags:
  - most
aliases:
---
Algoritmus, který tvoří [[Rozhodovací strom]].

> [!important] Pravděpodobnostní váhy
> Velmi důležitým konceptem je to, že algoritmus pracuje u každého pozorování (řádku) s váhami a ne s jeho relativní četností. Díky tomu se může v případě chybějících hodnot pracovat s částmi řádků.

# Proměnné
Algoritmus pracuje jak s kategoriálními, tak číselnými hodnotami. Nové možné uzly porovnává pomocí [[Poměr informačního zisku]]. Díky tomu nepreferuje třídy s velkým množstvím dat.
## Kategoriální
V případě kategorií je po vybrání konkrétní proměnné vytvořen nový uzel pro každou jednotlivou kategorii. Každý uzel je buď listový (konečný), nebo se v něm tvoří další podstrom.
## Číselné
Pokud je proměnná číselná, algoritmus hledá optimální hodnotu, podle které data rozdělí na dva podstromy.
$$
X \leq \text{hodnota}; \space X > \text{hodnota}
$$
Pro vytvoření takového pravidla je nutné vyzkoušet každý možný bod, kterých může být teoreticky $n - 1$. Algoritmus na to jde ale chytře a nejprve si data seřadí podle $x$. Rozdělující hodnoty pak jsou hodnoty, ve kterých se mění sledovaná kategorie. Např. v seřazených datech:

| $x$ | kategorie |
| :-: | :-------: |
|  1  |     A     |
|  3  |     A     |
|  4  |     A     |
|  5  |     B     |
|  8  |     B     |
|  9  |     A     |
budou otestovány body $4.5$ a $8.5$. Podle toho, jaký bod nejlépe rozdělí data, bude vytvořen uzel.
# Chybějící hodnoty
Model z chybějících hodnot tvoří váhy, které jsou použity při inferenci.
## Trénování
Pokud jsou v proměnné chybějící záznamy, data jsou rozdělena na chybějící a nechybějící.
$$
\begin{align}
C &= \text{kompletní data} \\
M &= \text{chybějící data}
\end{align}
$$
Na datech v množině $C$ se tvoří rozhodovací strom. Výsledný [[Poměr informačního zisku]] je vynásoben poměrem vah jednotlivých množin.
$$
IGR(S, A)_{new} = IGR(S, A)_{old} \space\times\space {\sum_{p \in C} p \over \sum_{p \in S} p} 
$$
To penalizuje proměnné, ve kterých chybí mnoho záznamů a pro jejich použití je tedy nutné, aby přinášeli opravdu velké množství informací.
Druhým krokem je chybějící hodnoty "rozložit" do nově vytvořených uzlů pomocí vah. V případě, že v proměnné nejsou žádné chybějící hodnoty, se data "rozešlou" do dalších uzlů podle toho, jakou hodnotu mají. V případě chybějících hodnot to ale nelze, protože není jasné, kam hodnotu zařadit. Řádky, které mají chybějící hodnotu se proto zváží podle počtu záznamů v jednotlivých kategorií. **Řádky s chybějící hodnotou jdou tedy do každého podstromu, ale vždy s jinou váhou!** To umožňuje stromu pracovat s nejistotou a přenášet ji do dalšího rozhodování. Když se v dalších uzlech rozhoduje s chybějící hodnotou, váhy jsou znovu pronásobeny.

Řekněme, že ze 100 řádků známé hodnoty u 80 z nich
- Kategorie A: 20 záznamů ($20 / 80 = 0,25 \space \%$)
- Kategorie B: 30 záznamů ($30 / 80 = 0,375 \space \%$)
- Kategorie C: 30 záznamů ($30/80 = 0,375 \space \%$)
Ve zbylých 20ti případech hodnotu neznáme, a proto je všech 20 řádků posláno do každého jednotlivého uzlu s různou váhou.
 - do kategorie A s váhou $20 \times 0,25= 5$
 - do kategorie A s váhou $20 \times 0,375=7,5$
 - do kategorie A s váhou $20 \times 0,375=7,5$
Např. do uzlu s kategorií A půjde $20+20=40$ řádků, ale součet jejich vah bude $20 + 5 = 25$.

> [!example] Vysvětlení
> Myšlenka je taková, že rozdělení chybějících hodnot je pravděpodobnostní. Implicitně vlastně říkáme:
> > Pokud ve známých datech je 25 % dat v kategorii A, znamená to, že chybějící řádek má 25% pravděpodobnost toho, že bude zařazen do kategorie A.

V dalších uzlech může nastat, že hodnoty budou znovu chybět. V takovém případě je rozdělení stále pravděpodobností, akorát se pracuje už s upravenými váhami. Pokud bychom měli novou podkategorii, kde z 40ti řádků (kategorie A) s celkovou váhou 25 jich známe 30, pak
- Kategorie A / Podkategorie E: 15 záznamů a u deseti chybí kategorie ($(5 + 10*0,25)/16,5  = 0,4545 \space \%$)
- Kategorie A / Podkategorie F: 15 záznamů a u osmi chybí kategorie ($(7 + 8*0,25)/16,5=0,5454 \space \%$)
zbylých 10 záznamů s váhou ($8 + 2*0,25 = 8,5$) záznamů musí být rozděleno. Do obou nových uzlů půjde všech 10 řádků s váhou:
- Do Kategorie A / Podkategorie E s váhou $8,5 \times 0,4545 = 3,86$
	- Celkový váha uzlu: $5 + 10 \times 0,25 + 10 \times 3,86$
- Do Kategorie A / Podkategorie F s váhou $8,5 \times 0,5454 = 4.63$
	- Celkový váha uzlu: $7 + 8 \times 0,25 + 10 \times 4,63$
## Inference
Pokud je nutné provést inferenci na datech, kde nechybí žádné údaje, je predikce provedena klasickým způsobem. V případě, že v nějakém uzlu nechybí žádné údaje, je postup stejný jako v ostatních algoritmech. Pokud se narazí na údaj, který je v uzlu potřebný a daná proměnná chybí, je vytvořeno $k$ predikci pro jednotlivé kategorie. Každá predikce je pak zvážená relativní četností dané kategorie. Z příkladu víše, pokud
- Kategorie A predikuje: Kočka = 0,25; Pes = 0,50; Delfín = 0,25
- Kategorie B predikuje: Kočka = 0,40; Pes = 0,10; Delfín = 0,50
- Kategorie C predikuje: Kočka = 0,05; Pes = 0,05; Delfín = 0,90
Poté
 - $P(\text{kočka}) = 0,25 \times 0,25 + 0,40 \times 0,375 + 0,05 \times 0,375 =0,23$
 - $P(\text{pes}) = 0,50 \times 0,25 + 0,10 \times 0,375 + 0,05 \times 0,375 = 0,18$
 - $P(\text{delfín}) = 0,25 \times 0,25 + 0,50 \times 0,375 + 0,90 \times 0,375 = 0,59$
Finální predikce by tedy byla kategorie *delfín*. Pokud by tento uzel byl součástí nějakého většího stromu, vypočtené pravděpodobnosti by se rekurzivně posunuly víš.
# Pruning
Po vytvoření stromu algoritmus používá [[Error-based prořezání stromu|Error-based prunning]] a [[Předběžné ořezávání]].

- - -
AI, vlastní výpočty