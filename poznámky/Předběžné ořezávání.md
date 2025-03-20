---
téma: Statistika, ML
tags:
  - most
aliases:
  - Pre-prunning
---
Metody, které používá [[Rozhodovací strom]] pro lepší generalizaci na trénovacích datech. Jejich úkolem je předem nastavit parametry růstu stromu tak, aby v případě málo znalostí nebo velké nejistoty zastavil růst a "nepřeučil" se. Jedná se např. o parametry:

| Hyperparametr       | Popis                                                                         | Účel                  |
| ------------------- | ----------------------------------------------------------------------------- | --------------------- |
| `max_depth`         | Maximální hloubka stromu.                                                     | Zastavující kritérium |
| `min_samples_split` | Minimální počet vzorků, který je potřeba pro vytvoření **rozhodovacího** uzlu | Regularizace          |
| `min_samples_leaf`  | Minimální počet vzorků, který je potřeba pro vytvoření **listového** uzlu     | Regularizace          |
| `max_leaf_nodes`    | Maximální počet listových uzlů                                                | Regularizace          |

Ty se však mohou lišit podle použitého algoritmu nebo implementace.
- - -
