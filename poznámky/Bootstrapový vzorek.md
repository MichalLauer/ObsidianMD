---
téma: Statistika, ML
tags:
  - definice
aliases:
---
Proces, při kterém je vytvořen z dat o velikosti $n$ nový vzorek o velikosti $n$ tak, že se z původních dat vybírají záznamy s vracením.
# Využití dat
Každý řádek má $1/n \space \%$ pravděpodobnost, že bude vybrán. Pravděpodobnost, že nebude ani jednou vybrán, je
$$
\left(1 - {1 \over n} \right)^n.
$$
S rostoucím $n$ lze zjistit, že
$$
\lim_{n\to\infty} \left(1 - {1 \over n} \right)^n = e^{-1} \approx 0,3679.
$$
Pravděpodobnost, že vzorek nebude vybrán, je zhruba 36,8 %. **Při bootstrapovém vzorkování je tedy vybráno zhruba 63 % dat.**

- - -
