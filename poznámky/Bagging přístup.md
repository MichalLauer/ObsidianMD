---
téma: ML
tags:
  - koncept
aliases:
---
Bagging (*bootstrap aggregation*) je přístup, pomocí kterého je vytvořeno několik slabých učitelů, kteří jsou použiti k predikci. 
# Slabé modely
Jednotlivé modely nejsou nijak robustní. Mohou být velmi jednoduché nebo přeučené. Důležité je, že je lze
1) rychle natrénovat, a
2) rychle použít.
# Agregace
Po vytvoření $B$ různých modelů je vytvořena predikce jednoduchou agregací pomocí průměru. Síla agregace je v tom, že s rostoucím $B$ snižuje výrazně rozptyl odhadu, zatímco velmi málo zvyšuje zkreslenost. Jedná se tedy o formu [[Bias-variance tradeoff]], kdy mám sice hodně zkreslených estimátorů, ale jejich rozptyl je mnohem menší.
## Regrese
Díky [[Rozdělení průměru]] se rozptyl odhadu s rostoucím $B$ snižuje. 
# Modely
Každý model je naučen na [[Bootstrapový vzorek]] z původních dat. Pro rychlý pokles rozptylu je důležité, aby byly jednotlivé modely nezávislé.  Metoda je vhodná pro modely, které jsou citlivé na vybraná data. 
Nejčastěji se kombinuje s [[Rozhodovací strom]], který je na různě vytvořené datové vzorky citlivý a mezi modely není až tak velká závislost. Naopak [[Lineární regrese]] je pro metodu spíše nevhodná, protože má analytické řešení a závislost zde může být významná.
# Náročnost
Při baggingu je nutné vytvořit *paralelně* několik různých modelů. K tomu lze využít paralelní počítače a díky tomu je trénování a inference relativně rychlá záležitost (alespoň než ostatní komplexní metody).
# Robustnost
Každý model se učí pravidla na různých verzích dat. Pro každý model je využito zhruba 63 % dat ([[Bootstrapový vzorek]]) a tak se modely učí na velmi různých verzích dat. Dokáží se naučit jiná pravidla, závislosti nebo vztahy a výsledky jsou tak robustní. Robustnost závisí také na tom, jak moc jsou jednotlivé modely závislé; čím menší závislost, tím menší větší citlivost na vybraná data a tím robustnější výsledky.
# Optimalizace
Díky [[Bootstrapový vzorek]] a využití pouhých zhruba 63 % lze použít [[Out-of-bag error]] pro odhad kvality estimátorů.

- - -
