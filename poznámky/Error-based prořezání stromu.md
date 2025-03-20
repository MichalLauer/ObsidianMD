---
téma: ML
tags:
  - most
aliases:
  - Error-based prunning
---
Metoda, která dokáže pročistit strom a zabránit tak přeučení. Skládá se ze dvou částí, které probíhají na **plně vytvořením modelu ze zdola nahoru**. Jelikož metoda používá statistické výpočty, čištění **je prováděno na trénovacích datech a není potřeba používat testovací data**.
# Čištění
V každém uzlu je vypočtena chybovost $E$.
$$
E = {\text{\# špatných klasifikací}\over\text{\# počet klasifikací}}
$$
V případě listového uzlu se jedná o jednoduché porovnání finálních predikcí. Pokud se jedná o rozhodovací uzel, predikce je vyhodnocena pomoc váženého součtu chyb jednotlivých podstromů. Následně je vypočtena pesimistická horní hranice odhadu, která je použita pro vyhodnocení kvality uzlu. Tyto hranice jsou vypočteny dvě - pro daný uzel a pro případ, kdy je uzel nahrazen listovým uzlem. Pokud je pesimistický odhad chybovosti listového uzlu menší nebo roven odhadu rozhodovacího uzlu, je rozhodovací uzel nahrazen listovým uzlem. Pesimističnost lze vyjádřit parametrem **Confidence factor**, který určuje kvantil normovaného normální rozdělení. Čím menší hodnota, tím více se nahrazují rozhodovací uzly listy.

> [!example] Myšlenka
> Algoritmus se ptá: ,,Když nahradím tohle rozhodovací pravidlo listovým uzlem, zlepší se výkonost modelu?" Pokud ano, celý strom se zjednoduší a zároveň zlepší.
# Zdvihání
Algoritmus také zkouší nahradit rozhodovací uzly pomocí hlubších podstromů a tím se strom zjednoduší a ponechá si hlubší strukturu. Řekněme, že existuje tento rozhodovací strom:

```
                 Outlook
                /   |   \
               /    |    \
          Sunny  Overcast  Rain
           /        |       \
          /         |        \
      Humidity   PlayTennis=Yes  Wind
      /     \                   /   \
     /       \                 /     \
   High      Low           Strong   Weak
    |         |              |       |
PlayTennis=No PlayTennis=Yes PlayTennis=No PlayTennis=Yes
```

Nejprve je vyhodnocena chybovost pro celý strom na úrovni proměnné `Outlook`. Dále je vyhodnocena chybovost na úrovni `Humidity`. V případě, že je chybovost celého stromu větší než podstromu na úrovni `Humidity`, je strom nahrazen pouze rozhodováním na úrovni `Humidity`. Strom by tedy vypadal takto:

```
                 Humidity
                /        \
               /          \
             High         Low
              |            |
        PlayTennis=No   PlayTennis=Yes
```

Nahrazení není vždy celého stromu, ale lze nahradit pouze jednotlivé podstromy pomocí jejich podstromů.
- - -
