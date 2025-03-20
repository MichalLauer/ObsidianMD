---
téma: Statistika
tags:
  - most
aliases:
---
Pokud se aplikuje [[Bayesův vzorec]] na [[NHST]], je vidět, jak mohou být výsledky zavádějící. Mějme
- $P(sig | h_0) = 0,95$ - [[Síla testu]]
- $P(sig|\neg h_0) = 0,05)$ - [[False-positive]]
- $P(h_0) = 0,01$ - pravděpodobnost, že je hypotéza pravdivá

$$
P(h_0 | sig) =
\frac{p(sig|h_0)P(h_0)}{p(sig|h_0)p(h_0) + p(sig|\neg h_0)p(\neg h_0)} \approx
0,16
$$

> [!warning] Klam
> Pravděpodobnost, že je hypotéza pravdivá za předpokladu významného testu je pouze 0,16.

# Kritika oproti definici [[NHST]]
Základním předpokladem NHST ale je, že hypotéza platí, tedy $P(H_0) = 1$. To zkrátí výpočet na 
$$
P(h_0 | sig) =
\frac{p(sig|h_0)1}{p(sig|h_0)1 + p(sig|\neg h_0)0} = 1.
$$
Je tedy důležité zvážit, jestli předpoklad pravdivé nulové hypotézy dává smysl.
- - -
[[Statistical rethinking (2e)]], 3.0