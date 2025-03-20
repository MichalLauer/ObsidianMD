---
téma: Statistika, ML
tags:
  - koncept
  - definice
  - most
aliases:
---
# Známý rozptyl
$$
\overline{X} \sim N \left(\mu, {\sigma^2 \over n}\right)
$$
## Střední hodnota
$$
E(\overline{X}) = E\left({1 \over n} \sum_{i=1}^n x_i\right) =
{1 \over n} \sum_{i=1}^n E(x_i) = {1 \over n} n \mu = \mu
$$
## Rozptyl
$$
D(\overline{X}) = {1 \over n^2} \sum_{i=1}^n D(x_i) =
{1 \over n^2} n \sigma^2 = {\sigma^2 \over n}
$$
# Neznámý rozptyl
$$
\left( \overline{X} - \mu \right) {\sqrt n \over S} \sim T(n-1)
$$
- - -
