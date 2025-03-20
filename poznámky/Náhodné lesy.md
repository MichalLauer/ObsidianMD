---
téma: ML
tags:
  - most
aliases:
  - Random forest
---
Metoda, který kombinuje [[Rozhodovací strom]] a [[Bagging přístup]] pro vytvoření robustního estimátoru.
# Volba prediktorů
Hlavním rozdílem oproti Baggingu je, že každý rozhodovací strom pracuje s jinými prediktory. Díky tomu se snižuje závislost mezi jednotlivými stromy a zvyšuje se pokles rozptylu. Často se volí počet prediktorů jako $\sqrt{p}$, ale jedná se o hyperparametr, který je možné nastavit.
# Velká korelace prediktorů
V případě, že jsou jednotlivé prediktory velmi závislé, bude pokles u Bagging metod nevýrazný. I přes různé datové vzorky budou data a modely tak závislá, že se přístup nemusí vyplatit. Lze to vyřešit přísným výběrem náhodných prediktorů pro každý model, díky čemuž lze závislost do určitě míry zmenšit.
- - -
