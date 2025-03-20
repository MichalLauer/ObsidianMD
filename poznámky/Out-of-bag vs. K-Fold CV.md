---
téma: Statistika, ML
tags:
  - most
aliases:
---

Porovnání [[Out-of-bag error]] a [[K-Fold CV]] pro vyhodnocení kvality modelů.
# Konvergence
Při velkém počtu opakování by měli obě metody konvergovat ke stejným výsledkům.
# Náročnost
OOB je mnohem méně náročná metoda, protože provede
1) trénování na datech,
2) vyhodnocení na zbylých nepozorovaných datech.
K-Fold CV musí proces trénování a vyhodnocování provést $k$-krát, což trvat mnohem delší dobu.
- - -
