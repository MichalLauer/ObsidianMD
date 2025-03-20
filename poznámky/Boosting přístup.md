---
téma: ML
tags:
  - koncept
aliases:
---
Boosting je metoda, která obecně staví slabé učitele *za sebe*. Modely jsou jednoduché a všechny, kromě prvního, se učí postupně opravovat model před sebou. Finální predikce je pak součet jednotlivých modelů, tedy
$$
\hat y = \sum_{i=1}^p f_p(x).
$$
První model se učí podle $y_i$, druhý $r^1_i = y_i - \hat y$, třetí $r^2_i = y_i - \hat y - \hat r^1_i$.
# Různé verze
Existuje mnoho různých modifikací, ale myšlenka je vždy stejná - hlubší modely se snaží opravit modely před ním.
## Shrinkage parametr
Kontroluje, jak rychle se model učí. Jelikož boosting algoritmy se **dokáží přeučit**, je vhodné ho volit nižší.
$$
\hat y = \sum_{i=1}^p \lambda f_p(x).
$$
## Vážení
V některých implementací se residua váží podle toho, jak jsou závažná. Větší odchylky mají větší prioritu a je snaha opravit ty největší chyby a soustředit se na celkovou průměrnou přesnost.
# Citlivost
Model je citlivý na odlehlý pozorování, protože jedna velká chyba se propaguje do dalších modelů a ty nejsou schopné se soustředit na celkovou přesnost.

- - -
