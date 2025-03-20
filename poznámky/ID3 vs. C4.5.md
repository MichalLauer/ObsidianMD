---
téma: ML
tags:
  - most
aliases:
---
[[Učící algoritmus C4.5]] je nástupcem algoritmu [[Učící algoritmus ID3]], který přináší několik základních vylepšení a snad ve všech ohledech je vhodnější.
# Porovnání
## Proměnné
Zatímco ID3 umí pracovat pouze s kategoriálními proměnnými, C4.5 dokáže pracovat i s čísly, kde tvoří binární uzly.
## Funkce
C4.5 používá lepší matematické funkce, které nezvýhodňují velmi zastoupené třídy. Díky tomu strom netrpí tolik přeučením.
## Chybějící hodnoty
V případě algoritmu C4.5 není nutné předzpracovávat chybějící hodnoty, jelikož algoritmus je zvládne sám zpracovat a zohlednit při tvoření stromu.
## Prunning
Algoritmus ID3 nepoužívá žádnou formu prunningu, kvůli čemuž je strom velmi náchylný k přeučení. c4.5 používá jak pre-prunning, tak post-prunning.


- - -
