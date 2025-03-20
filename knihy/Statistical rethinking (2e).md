---
téma: ML
cssclasses:
  - numbering
---

# The Golem of Prague
## Statistical golems
Klasická statistika je primárně o tom vybrat si ten správný test (*test je metafora pro golema*), který jen dělá to, co mu je nařízeno. Test nezajímají splněné předpoklady nebo validita dat, prostě je to jen nějaký "algoritmus". Často se takhle učí statistika, což je špatně. Studentům je naservírováno hodně metod, mezi kterými se učí rozhodovat. Neučí se tedy podstatu statistiky a její vlastnosti, ale jen výběr "správného kladiva pro hřebík". Po čase může být všechno ale jen hřebík a je těžké rozeznat, kdy použít ten správný nástroj.
Dokud se provádí *základní výzkum*, ničemu to nevadí. Problém je, kdy se někdo chce přesunout ze základů statistiky do pokročilejších dat, kde málokdy stačí pouhé základní metody a je potřeba robustnějších alternativ.
## Statistical rethinking

> Ian Hackings - Representing and Intervening (1983)
> Karl Popper - The Myth of Framework (1996)

S odkazem na [[Karl Popper]] se klasická statistika posouvá tvořením zfalšovatelných hypotéz. Jen pokud budeme falšovat (*falsifikovat*) hypotézy, dokážeme se ve vědě posunout dále. Tohle ale není pravda ze dvou důvodů:
1) Hypotézy a modely mají vztah n:n a nějaké testy mohou něco zamítnout a něco ne.
2) Můžeme mít různé výsledky pro různá data.

> [!question] Replikovatelnost
> To ano, ale od toho je přeci důležitá replikovatelnost. Věda není založená na jednom testu, ale na replikovatelných, nezávislých a ověřených výsledcích, které dávají smysl jak z hlediska statistiky, tak teoretických.

Je také velký rozdíl mezi [[NHST]] and myšlením [[Karl Popper]]. Zatímco Karl se snaží falsifikovat hypotézy, které chce zkoumat, NHST se snaží falsifikovat opak.

**Otázka:** Má tento lék léčivé účinky?
**Hypotéza:** Léčba je efektivní.
**Karl Popper**: Udělám test a budu se snažit **zamítnout to, že je léčba efektivní.**
**NHST**: Udělám test a budu se snažit **zamítnout to, že léčba není efektivní.**

Jak jé známo, tak *Všechny modely jsou špatně, některé jsou ale užitečné.* Pokud je tedy model nepřesný, nedává smysl zamítnout hypotézy, které z toho nepřesného modelu vychází.

> [!important] Exponenciální rozdělení
> Příroda má ráda rozdělení z exponenciální rodiny, která má maximální entropii ?

Pokud bude nulová hypotéza něco, co chceme dokázat, tak je jedno, kolik máme dat; žádný objem dat hypotézu nedokáže potvrdit. Naopak stačí jedno pozorování, které hypotézu dokáže vyvrátit (viz. *černá labuť*). Ve vědecké praxi to je ještě horší, jelikož se teorie střetává např. s chybou v měření nebo špatným pozorováním. To dále vytváří problém, kdy nesprávné/nepřesné pozorování může falešně zamítnout nulovou hypotézu.
Kvůli těmto problémům je falsifikace vždycky způsobena koncensem a ne nějakou logickou podmínkou.
## Tools for golem engineering
### Bayesian analysis
Tvoření modelů je užitečnější, než používání přetvořených golemů nebo snaha o falsifikaci. Pokud vytvoříme model, který popisuje nějaký systém, dá nám to lepší obrázek o celkovém fungování a více informací než jen významné/nevýznamné. Také je důležité modelům rozumět, protože až (ne když) se začne něco rozbíjet, je důležité to napravit - a pokud není jasné, jak model funguje, je to obtížné.
Bayesovská statistika je jedním z nástrojů, jak tvořit modely. Lze popsat tak, že se podívám na data a budu uvažovat, jak moc jsou pravděpodobná a jak odpovídají mému očekávání. Oproti tomu stojí frekventistická statistika, která tvoří odhady pomocí dostatečně velkých vzorků a opakování. Z těchto opakování lze vytvořit odhady, které mají [[Výběrové rozdělení]]. Jednotlivá pozorování tedy nemají rozdělení, ale výsledné odhady ano. Bayesovská statistika pracuje s tím, že náhoda je vlastností dat a ne reálného světa.
Existují často případy, kdy bayesovská a frekventistická statistika dávají stejné výsledky. Výhody bayesovské statistiky jsou v tom, že nestojí na předpokladu velkého počtu identických opakování, které v realitě málokdy dávají smysl. Další výhodou bayesovské statistiky je její intuitivní vysvětlování a interpretace. Často se stává, že lidé interpretuji frekventistické výsledky bayesovským stylem. Je to problém jak pro statistiky, tak pro nestatistiky.

> [!warning] Verze pravděpodobností
> Kromě toho, že existuje frekventistická a bayesovská definice pravděpodobnosti, existují i různé verze bayesovské pravděpodobnosti samotné. Objevují se jména jako **[[Bruno de Finetti]]**, **[[Richard Cox]]** nebo **[[Leonard Savage]]**. Nejpoužívanější interpretace je *logická*, nebo také **[[Laplace-Jeffreys-Cox-Jaynes]]** interpretace.
### Model comparison, prediction
Porovnávat modely lze pomocí hodně metod, nejpoužívanější je nejspíše krosvalidace a informační kritéria. Pomáhají zejména
- při tvoření očekávání o tom, jak bude model predikovat,
- o tom, jak je model přeučený a jak dobře generalizuje, a
- při určování vlivných pozorování.
### Multilevel models
> Jedná se o [[Hierarchické modely]]. Je to to samé jako [[Model náhodných efektů]], [[Mixed modely]].

Jsou postavené na principu, že parametry samotné zastupují nějaký model. Tyhle modely mohou mít další parametry, a tak to jde dál. Jsou schopné bránit přeučení, jelikož provádějí [[Partial pooling]]. Podle autora by mělo být **hierarchické modelování a hierarchická regrese základní způsob, jak regresi provádět**.

> [!quote] Budoucnost modelů
> Stejně jako se časem stávala trendem vícerozměrná lineární regrese, poté obecný lineární model, následně simultánní rovnice, časem se stane standardem víceúrovňové modelování.

## Casual models
Důležitá myšlenka je, že modely, které jsou kauzálně špatně, mohou mít lepší predikce, než modely kauzálně korektní. Je to z toho důvodu, že přidání *confounding* proměnných dokáže často zlepšit samotnou predikci (protože jsou spolu proměnné asociované), ale pro kauzalitu je přidání takové proměnné problémové. S tím se pojí [[Grafický kauzální model]] nebo [[Přímý acyklický graf]]. Kauzalita však stále vychází z teorie a vědeckého poznání a ne z modelu samotného. **Data nejsou vše, co je pro kauzalitu potřeba.** To lze vykládat několika způsoby
- **Kauzalita nelze dokázat.** Je to to samé jako bavit se o tom, co se stane, až člověk umře.
- Kauzalita lze studovat **pouze v experimentálních** podmínkách. To ale velmi omezuje případy, kde by kauzalita šla zkoumat (zkoumání nemocí, evoluce, biologických procesů...)
- **Kauzální salát** - jednoduše budeme kombinovat hromady proměnných a zkoumat, jestli vznikla nebo nevznikla kauzalita na základě teorie.
# Small worlds and Large worlds
V malém světě žijí modely, které chceme používat pro predikci nebo inferenci. Tyhle modely jsou pak vloženy do velkého světa, kde je ale hodně věcí a informací, se kterými modely v malém světě nepočítají. Proto je důležitý peer-review, úprava modelů a zkoumání reálného světa.
Bayesovská analýza je důležitá, ale ne vždy se vyplatí brát úplně všechny informace do kontextu. V případě, že mi zapojení komplexních informací a vztahů zlepši model o nepatrnou část, může být vhodné takové informace vynechat.
## The garden of forking data
Nastavení neinformativních apriorních rozdělení není vždy dobré, protože v reálném světě máme prakticky vždy nějaké informace. Bayesovská statistika je vlastně jenom o počítání způsobů, kolika mohla pozorovaná data nastat (likelihood) krát apriorní důvěra pro danou možnost.
## Building a model
Tvoření modelů je na základě tří kroků:
- "Příběh", podle kterého data vznikla. Na základě něho je vytvořen model.
	- Tady ale pozor, více modelů může odpovídat jednomu "příběhu" a tak validní model neznamená správný příběh.
- Aktualizace modelu podle nasbíraných dat.
	- Je jedno, jestli do modelu budu posílat data po jednom nebo všechny naráz.
- Evaluace kvality modelu.
	- Výsledné posteriorní rozdělení je podmíněno i modelem, ze kterého je vytvořeno. Výsledky mohou být velmi jisté, ale zároveň být kompletně špatně, protože je špatný model
	- Nemá cenu zkoumat, jestli model je úplně přesný nebo ne; nikdy úplně přesný nebude.
Bayesovské odhady jsou platné pro jakoukoliv velikost vzorku a na rozdíl od frekventistických metod se nespoléhají na asymptotické vlastnosti.
## Components of the model
Bayesovská a klasická statistika je velmi propojená likelihoodem, který v obou světech znamená něco jiného. Existuje odrůda subjektivního bayesovského přístupu, která používá velmi subjektivní apriorní rozdělení. Ve vědě však není častá. Statistika je vlastně celá subjektivní a není jedno správné řešení pro libovolný problém. I přes snahu být objektivní autoři analýz vnáší určitou míru subjektivity do analýzy. 
Apriorní rozdělení se stává jedním z předpokladem modelů a je nutné s ním pracovat, upravovat ho a starat se o něj.
Jedním aspektem kritiky bayesovské statistiky je jednoduché lhaní pomocí apriorních očekávání, která lze upravit tak, aby vyšel libovolný výsledek. Takové lži jsou ale hned odhaleny a nebude mít žádný efekt (protože apriorní informace musí být uvedeny i s modelem). Pro zavádějící výsledky autoři často sáhnou po odlehlých hodnotých nebo různých úpravách dat.
## Making the model go
Součástí modelu je i to, pomocí jakého optimalizační nástroje byla analýza hotová. Na jiných metodách můžeme docházet k jiným závěrům.

> [!question] MCMC
> To nedává moc smysl, protože MC algoritmy zaručují, že asymptoticky jsou rozdělení identická ???

# Sampling the imaginary

> [!success] Příklad
> Super příklad na Bayese a upíry

Tyhle příklady ale nereprezentují bayesovskou statistiku, ale bayesovský vzorec. Dokonce ten příklad je celý "frekventistický", protože se počítá s relativní četností na nějakém vzorku. Takové příklady lze ale přepsat do bayesovského světa. Často je lepší vzorce vyjádřit [[Frekventistický formát Bayesova vzorce|absolutně]]. 
Parametry modelů jsou sice vyjádřené pomocí rozdělení, ale ta rozdělení nereprezentují nějaký skutečný náhodný proces, ale míru přesvědčení. To je důležitý rozdíl.
Náhoda je vlastností dat a ne reálného světa, protože reálný svět je deterministický. Náhodu způsobuje nedostatek dat.

> [!important] Bayesův vzorec při testování hypotéz
> V případě, že se aplikuje Bayesův vzorec na frekventistickou statistiku, pravděpodobnost pravdivé hypotézy za předpokladu významného testu je velmi malá.

## Sampling from a grid-approximate posterior
## Sampling to summarize
Obecně jsou při inferenci tři typy odhadů
- Bodový odhad
- Intervalový odhad
	- [[Percentilový interval]]
- Hustotní odhad
	- [[Interval nejvyšší hustoty]]
Výběr intervalu by měl být obecně jedno, protože celé posteriorní rozdělení je bayesiánský odhad - ne jen jedno číslo.
Při rozhodovaná o tom, jaký bodový odhad vybrat, je důležité stanovit funkci, podle které se vybrat. Pokud chci např. minimalizovat vzdálenost, volím medián. Nikdy ale nelze říct, že jedno číslo je obecně vždy správně.
## Sampling to simulate predictions
Díky vzorkování lze generovat data podle různých parametrů, tvořit predikce, ověřovat apriorní rozdělení nebo pozorovaná data.
U složitých modelů kontrola dat a predikcí nemusí dávat smysl, protože už tam je hodně komplexity.
Když se predikují nová data, musí se použít jak nejistota o náhodných parametrech, tak nejistota o pozorovaných datech. Kombinaci tvoří [[Posteriorní prediktivní rozdělení]].

# Geocentric Models
- Geocentrický model světa je sice špatně, ale lze pomocí něho aproximovat velmi dobře různé vztahy a blízká tělesa. I když je špatně, má tedy aplikační použití díky jeho jednoduchosti.
- Lineární regrese hraje ve statistice tu stejnou roli, jako geocentrický model. Lineární vztah je málokdy v reálném světě správný, avšak lze ho použít k velmi dobré aproximaci.
## Why normal distributions are normal
- Tady je pěkně zobrazeno normální rozdělení a CLT, kde je nejprve zobrazen vývoj zleva doprava. Tam je pěkně vidět to, jak se ten proces do začátku rozvine do normálního rozdělení.

> [!important] Centrální limitní věta - součet
> *,,Any process that adds together random values from the same distribution (with finite variance) converges to a normal"* 
```r
x <- replicate( 5000 , sum( rpois(5000, 2) ))
plot(density(x))
```


> [!important] Centrální limitní věta - součin
> *,,Products generate normal distributions on the log scale. That is because $\log(\prod f(\cdot) )$ is just $\sum \log(f(\cdot))$"*
```r
x <- replicate( 5000 , log(prod(1 + runif(30, 0, 0.5))) )
plot(density(x))
```

- V reálném světě je normální rozdělení všude, protože většina procesů je jen součet nějakých čísel. **Není to ale univerzální pravidlo.**
- Rozdělení, které popisují reálný svět, patří do skupiny [[Rodina exponenciálních rozdělení]]
## A language for describing models
## Gaussian model of height
- Apriorní rozdělení musí být založeno pouze na informacích, které neplynou z nasbíraných dat.
- Gausovské apriorní rozdělení a likelihood tvoří znovu normální rozdělení; to však neplatí u rozptylu.
- 89% interval je PRIME!!!
- Změna apriorního rozdělení pro $\mu$ ovlivní posteriorní rozdělení pro $\sigma^2$. Pokud je apriorní rozdělení moc jisté, a data tomu neodpovídají, rozptyl se musí zákonitě zvětšit.
## Linear prediction
- Ve chvíli, kde se používá lineární regrese, tak $\mu$ nemá rozdělení ($\mu\sim$), ale je to nějaká lineární transformace ostatních parametrů a dat ($\mu=$).
- Když data v regresi normalizuju ($x_j - \bar x_j$), tak se **interpretace koeficientu nemění, ani koeficient samotný se nemění. Mění se interpretace interceptu**.
- Normované normální rozdělení pro $\beta$ je v případě centrován přirozené, protože dává stejnou váhu jak na pozitivní, tak negativní asociaci. Zároveň vychází z nuly, což znamená, že žádná asociace není.
- Tabulková reprezentace (marginálních) posteriorních rozdělení je vhodná jen při málo parametrech.
- Při predikci není použita pouze ta nejvíce pravděpodobná přímka, ale i ostatní. Tím s propaguje nejistota do predikce a inference.
- Výsledky jsou vždy implicitně podmíněné na vybraném modelu.
- Pro generování intervalů kolem střední hodnoty stačí použít posteriorní rozdělení střední hodnoty.
- Pro generování intervalů kolem predikce je nutné zapojit i odhad pro $\sigma^2$.
## Curves from lines
- Určení apriorních rozdělení u polynomiálních koeficientů není jednoduché - dost k tomu pomáhá apriorní predikce.
- Standardizace je při odhadu důležitá kvůli stabilitě.
- Interpretace $\alpha$ není tak jednoduchá, protože polynomiál to ničí.
- Lineární regrese - lineární v parametrech.
# The Many Variables & The Spurious Waffles
