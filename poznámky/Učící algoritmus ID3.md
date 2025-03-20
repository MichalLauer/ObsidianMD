---
aliases: 
tags:
  - most
---
Algoritmus, který tvoří [[Rozhodovací strom]]. Název znamená *Iterative Dichotomizer 3*, což jednoduše popisuje to, jak vlastně celý funguje.
# Hlavní vlastnosti
## Použité proměnné
Algoritmus dokáže pracovat pouze s kategoriálními proměnnými. Pokud je nutné, aby zpracoval i číselné proměnné, je nutné data předzpracovat. Typicky stačí jednoduchá kategorizace.
# Funkce
Algoritmus na každém uzlu používá [[Vážená informační entropie]] pro
- aktuální uzel,
- všechny možné další uzly.
Nové uzly, které mají oproti tomu aktuálnímu největší [[Informační zisk]] jsou použity pro další větvení.
# Větvení
Když se vybere proměnná, podle které se bude dále větvit, tak je vytvořen nový uzel pro každou jednotlivou možnou kategorii. Strom se větví, doku není splněná zastavující podmínka nebo dokud není každý uzel listový.
# Přeučení
Stromy ID3 mají tendenci se přeučit. Jelikož má [[Informační zisk]] tendenci preferovat proměnné s hodně kategoriemi, může dojít k naučení velmi složitých pravidel na trénovacích datech. Zároveň je algoritmus *greedy*, což může tvořit zbytečně komplexní stromy.
- - -
