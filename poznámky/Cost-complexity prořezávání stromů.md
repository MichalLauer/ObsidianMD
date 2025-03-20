---
téma: ML
tags:
  - most
aliases:
---
Algoritmus, který souží pro ořezání [[Rozhodovací strom]] a může pomáhat zabránit přeučení.
# Postup
Algoritmus prořezává jednotlivé podstromy, na kterých následně testuje predikce.
## Vytvoření plného stromu
Nejprve je vytvořen celý komplexní strom, který je potenciálně přeučený.
## Vytvoření podstromů
U plného stromu se u každého rozhodovacího uzlu vypočte efektivní cost-complexity parametr $\alpha_t$. Následně se vytvoří podstrom pro každou možnou hodnotu $\alpha_t$. Podstrom, který má nejlepší predikční schopnost, je následně vybrán a jeho $\alpha_t$ je optimální hodnota hyperparametru.
### Ztrátová funkce
Při práci s celým stromem se optimalizuje pouze metrika $R(T)$ (např. [[Giniho míra nečistoty]]). Pro optimalizaci je použita upravená minimalizační funkce
$$
\min R(T) + \alpha |T|
$$
- $\alpha$ - cost (cena) každého jednotlivého listu
- $|T|$ - počet listů
### Řezání stromů
Rozhodovací pravidlo, podle kterého se bude rozhodovat mezi rozhodovacím a listovým uzlem. Ptám se, jestli je komplexita daného podstromu větší než zlepšení, které to přináší. Pokud ano, tak měníme rozhodovací uzel na listový.
$$
(|T_t| - 1)\alpha > R(t) - R(T_t)
$$
- $(|T_t| - 1)\alpha$ - *penalizace*, že rozhodovací uzel ponechám
	- $|T_t|$ - počet listů v daném podstromu
	- $-1$ je kvůli tomu, že se jeden rozhodovací uzel promění na listový.
	- Oproti listovému uzlu mám $|T_t| - 1$ listů navíc.
- $R(t) - R(T_t)$ - *odměna*, že rozhodovací uzel ponechám
	- $R(t)$ - hodnota ztrátové funkce daného uzlu
		- Tohle je chybovost, která bude při nahrazení listovým uzlem
	- $R(T_t)$ - hodnota ztrátové funkce pro celý podstrom
		- Tohle je chybovost, která bude v případě, že ponechám rozhodovací strom
	- Rozdíl je zlepšení v případě, že ponechám rozhodovací uzel.
	- $< 0$ - automaticky přeměním na list, jelikož jeho chyba je menší než celého podstromu
Pokud rovnice platí, znamená to, že **zlepšení, které přináší podstrom je větší, než jeho penalizace**. Rovnici lze upravit do 
$$
\alpha > \frac{R(t) - R(T_t)}{(|T_t| - 1)}
$$
Pravá část je stejná pro celý strom bez ohledu na to, jaká je hodnota parametru $\alpha$. Všechny vytvoření stromy budou tedy pouze jednotlivými podstromy. Obecně lze tedy mluvit o **efektivní cost-complexity** $\alpha_t$
$$
\alpha_t = \frac{R(t) - R(T_t)}{(|T_t| - 1)}.
$$
Každý parametr tedy odpovídá právě jednomu podstromu.
### Optimalizace
Na plném stromu je pro každý uzel vypočten efektivní parametr $\alpha_t$. Každý možný podstrom s jeho parametrem $\alpha_t$ je validován na nových datech. Model, který má nejlepší predikční schopnosti je následně zvolen.
### Hyperparameter tuning
Často je tunování neefektivní, protože zkouší nějaké předem definované hodnoty $\alpha$. Nastane tedy situace, kdy optimalizujeme hodnoty $\alpha_1, \alpha_2$, který vrátí stejný rozhodovací strom, protože
$$
\alpha_{t_1} < \alpha_1 < \alpha_2 < \alpha_{t_2}.
$$
Obě hodnoty vedou tedy k rozhodovacímu podstromu, který má $\alpha_t = \alpha_{t_2}$.

- - -
