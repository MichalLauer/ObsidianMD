---
aliases:
  - ML
tags:
  - koncept
---
Algoritmus, který tvoří pravidla, podle kterých se učí. Lze použít jak pro klasifikaci, tak regresi Na základě vybrané proměnné tvoří pravidla, podle kterých se postupuje níž. Výběr rozhodovacího pravidla záleží na daném algoritmu.
## Obecný popis větvení
Na začátku se musí pomocí nějaké heuristiky vybrat proměnná a hodnota, podle které se bude strom dále větvit. To, jak se jednotlivé pravidla tvoří, se liší podle algoritmů. Na možných nových podmnožinách se maximalizuje informační funkce a je vyhodnoceno, jak je rozdělení kvalitní. V případě klasifikace je cílem co nejlépe rozdělit predikované hodnoty, v případě regrese pak dosáhnout co nejmenší hodnoty optimalizační funkce. Pokud není, hledá se dál. Pokud ano, proces se rekurzivně opakuje na každé podmnožině dat. Růst stromu roste, dokud jsou data nebo není splněno nějaké zastavující kritérium.
## Větve
Při větvení může vzniknout buď rozhodovací uzel *(split nodes)* nebo listový uzel *(leaf node)*. V případě, že se jedná o rozhodovací uzel, algoritmus se nenachází na konci stromu a je nutné se dále rozhodovat. Listové uzly reprezentují konečné uzly, na základě kterých se tvoří rozhodnutí.
# Metody použití
Zmíněné metody byly vyvinuté s nějakým účelem a s nějakou definicí, ale v praxi se implementace může lišit podle jazyka nebo balíčku.
## Klasifikace
- [[Učící algoritmus ID3]]
- [[Učící algoritmus C4.5]]
## Regrese i klasifikace
- [[Učící algoritmus CART]]
- - -
