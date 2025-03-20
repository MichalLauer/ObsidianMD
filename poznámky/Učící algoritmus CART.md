---
téma: ML
tags:
  - most
aliases:
---
*CART (Classification and Regression Trees)* je algoritmus, který vytváří binární [[Rozhodovací strom]]. Dokáže provádět jak klasifikaci, tak regresi. 
# Proměnné
Algoritmus dokáže zpracovat jak číselné, tak kategoriální proměnné. V obou případech vytváří rozhodovací pravidla, která vytváří dvě další možné větve (nebo listový uzel).
## Číselné proměnné
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
## Kategorické proměnné
U kategoriálních proměnných algoritmus zkouší každou možnou podmnožinu kategorií (kromě prázdné a plné množiny). Může se vytvořit např. uzel
$$
X \in \{\text{modrá, zelená}\}
$$
Moderní algoritmy dokáží heuristicky podmnožiny filtrovat a tak v praxi není zkoušená každá jednotlivá možnost.
# Ztrátová funkce
V případě klasifikace algoritmus minimalizuje [[Giniho míra nečistoty]], v případě regrese se jedná o [[Střední kvadratická chyba]].
# Chybějící data
Algoritmus funguje jinak podle toho, zda se na chybějící proměnnou dokáže při tréninku připravit nebo ne.
## Data chybí pří tréninku
Pokud se algoritmus rozhodne rozdělit data podle nějaké proměnné, ve které chybí data, je nutné vytvořit tzn. náhradní (*surrogate*) uzel. Algoritmus nejprve vezme kompletní data a najde optimální bod, podle kterého se rozhodovat. V případě, že proměnná v uzlu obsahuje chybějící data, jsou vytvořené náhradní uzly, které nejlépe kopírují původní rozdělení. Tvoření náhradních uzlů je provedeno pouze na kompletních datech. Po vytvoření náhradních uzlů jsou uzly ohodnoceny podle toho, jak často posílají záznamy stejnou cestou jako původní rozdělení. Pokud náhradní uzel pošle doleva 40 stejných záznamů, doprava 50 stejných záznamů a celkově má k dispozici 100 záznamů, jeho hodnocení je $(40 + 50) / 100 = 0,9$. Těchto náhradních uzlů je vytvoření více
Pokud při inferenci narazí strom na chybějící hodnotu, rozhodne se podle uzlu, který má
- největší možnou spolehlivost, a
- existuje pro něj hodnota.
Pokud je tedy náhradní uzel Věk (1) a Kraj (2), v případě známého věku je použit uzel (1). Pokud ale věk chybím je použit náhradní uzel (2). Pokud chybí všechny záznamy pro náhradní uzly, algoritmus pokračuje cestou, do které při tréninku šlo nejvíce záznamů - použíje tedy nejvíce pravděpodobnou cestu.
## Data jsou při tréninku kompletní
Pokud má proměnná v trénovací části kompletní data, nejsou pro ni vytvořené náhradní uzly. Chybějící hodnoty při inferenci tedy nemají stanoveno, podle kterých náhradních uzlů se mají dále rozdělit. V takovém případě je záznam poslán tím směrem, kam při tréninku šlo nejvíce záznamů. Je tedy znovu použita nejvíce pravděpodobná cesta.
### Robustnost
Pokud jsou data čistá a hrozí, že při inferenci nějaké záznamy budou chybět, lze náhodně chybějící záznamy smazat. Pokud se to bude dělat robustně (třeba bootstrapem), může dojít k lepší generalizaci a tím pádem lepší predikci na nových, chybějících datech.
## Implementační rozdíly
Implementace algoritmu se v praxi může lišit a pravidla mohou být tvořena trošku jinak.
# Ořezávání
Algoritmus používá jak parametry pro [[Předběžné ořezávání]], tak [[Cost-complexity prořezávání stromů]].
- - -
