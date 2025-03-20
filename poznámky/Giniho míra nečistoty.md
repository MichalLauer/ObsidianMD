---
téma: ML
tags:
  - definice
aliases:
  - Gini impurity
---
Koeficient měří pravděpodobnost toho, že je náhodně vybraný záznam špatně klasifikován v případě, že klasifikace probíhá nezávisle podle rozdělení jednotlivých kategorií. Čím větší míra, tím větší čistota a v datech je větší náhodnost.

$$
G(D) = \sum_{i=1}^k p_i(1-p_i) = \sum_{i=1}^k p_i - \sum_{i=1}^k p_i^2 =
1 - \sum_{i=1}^k p_i^2
$$

> [!example] Myšlenka
> Počítám pravděpodobnost, že si kategorii $i$ vyberu ($p_i$) a následně ji budu špatně klasifikovat ($1 - p_i$). To dělám pro každou kategorii $i = 1, \dots, k$.
# Hranice
**Kompletní čistota** - všechna data patří do jedné kategorie; $p_1 = 1$; $p_i = 0; i = 2, \dots, k$
$$
G = 1 - (1^2 + 0^2 + \dots + 0^2) = 0
$$
**Kompletní nečistota** - data mají rovnoměrné rozdělení; $p_i = p_k; \forall i, j = 1, \dots, k$
$$
G
= 1 - \sum_{i=1}^k \left({{n \over k} \over n}\right)^2
= 1 - k {1 \over k^2}
= 1 - {1 \over k}
$$
pro dvě kategorie je hranice $1/2$ a pro tři kategorie je hranice $2/3$.
- - -
