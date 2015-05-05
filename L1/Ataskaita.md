# PlantUML kodo prižiūrimumo charakteristikų tyrimas
## Tikslas
Susipažinti su pagrindinėmis programų išeities teksto charakteristikomis (metrikomis). Suprasti metrikų svarbą programų priežiūros kontekste. Atlikti paveldėtinės sistemos charakteristikų tyrimą.

##Teorinė dalis
 - __Programos prižiūrimumas__ -- programų sistemos arba jos komponento modifikavimo lengvumas siekaint ištaisyti klaidas, pagerinti charakteristikas arba pritaikyti prie pasikeitusios aplinkos. Programos prižiūrimumas yra tiesiogiai proporcingas jos sudėtingumui.
 - __Sistemos sudėtingumas__ -- tai sistemos charakteristika, kuri yra tiesiogiai proporcinga sistemos supratimui, kurio reikia norint atlikti sistemos pakeitimus.
 - __Programų metrika__ -- tai programos arba jos dalies tam tikros savybės (charakteristikos) kiekybinė (išmatuojama) išraiška.

###Pagrindinės metrikų grupės
####1. Dydžio metrikos
Sistemos klasių, klasių metodų, funkcijų, modulių, kintamųjų ar kt. skaičius; programos dydis kodo eilutėmis (LOC), komentarų kiekis (COM);

Programos modulio (klasės, komponento) sudėtingumas yra žemas, jei jo dydis yra mažesnis nei 100 LOC. Komentarų kiekis apskaičiuojamas kaip komentarų eilučių santykis su kodo eilutėmis (procentais)

####2. Objektinės sudėtingumo metrikos
Dažniausiai naudojamos *Chidamber* ir *Kemerer* pasiūlytos metrikos:
 - __Metodų skaičius klasėje__ (*weighted methods per class*, WMC). Kuo WMC didesnis, tuo klasėje gali būti daugiau klaidų, tuo daugiau reikia pastangų klasės sukūrimui ir priežiūrai. Klasės su aukšta WMC reikšme turi būti išskaidytos į kelias mažesnes klases. Rekomenduojama, kad WMC neviršytų 20, o sistemoje būtų ne daugiau kaip 10% klasių, kurių WMC reikšmė yra didesnė nei 24.
 - __Jungumas tarp klasių__ (*coupling between object class*, CBO). Kuo didesnis jungumas, tuo sudetingesnė klasės priežiūra. Jei CBO > 14, tai klasę reikia labai gerai ištestuoti.
 - __Klasės atsakas__ (*response for a class*, RFC) - lygus klasės metodų ir klasės iškviečiamų kitų klasių metodų sumai. Didesnė RFC reikšmė rodo aukštesnį sudėtingumą ir blogesnį suprantamumą. Kritinė RFC reikšmė yra lygi 50.
 - __Vaikų skaičius__ (*number of children*, NOC) - bazinę klasę paveldinčių klasių skaičius (paveldėjimo hierarchijos plotis). Aukšta NOC reikšmė rodo mažesnę klaidų tikimybę, tačiau aukštos NOC ir WMC reikšmės rodo didelį bazinės klasės sudėtingumą. TOkiu atveju bazinę klasę reikia restruktūrizuoti.
 - __Paveldėjimo medžio gylis__ (*depth of inheritance tree*, DIT) - ilgiausio kelio iki šakninės klasės ilgis. Aukštesnė DIT reikšmė reiškia sudėtingesnę sistemą, kurioje gali būti daugiau klaidų. Rekomenduojama, kad DIT reikšmė būtų <= 5
 - __Metodų rišlumo stoka__ (*lack of cohesion of methods*, LCOM1). Rekomenduojama, kad LCOM1 < 5.
 - __Projekto sudėtingumas__ (*design complexity*, DES). Išvestinė metrika, kuri yra skaičiuojama pagal formulę
 $$DES = 0.2 * WMC + 0.3 * RFC + 0.3 * CBO + 0.2 * DIT$$
 Kritinė DES reikšmė yra 25.

####3. *Halstead*'o sudėtingumo metrikos
Skaičiuojant *Halstead*'o sudėtingumą vertinamas programos skirtingų operatorių skaičius $n_1$, skirtingų operandų skaičius $n_2$, visų operatorių skaičius $N_1$ ir visų operandų skaičius $N_2$.
Apibrėžiamos tokios metrikos:
 - __Žodynas__ (*Vocabulary*):
$$n = n_1 + n_2$$
 - __Ilgis__ (*Length*):
$$N = N_1 + N_2$$
 - __Apimtis__ (*Volume*):
$$V = N \log_2{n}$$
 - __Sunkumas__ (*Difficulty*):
$$D = (\frac{n_1}{2}) * (\frac{N_2}{n_2})$$
Kritinė reikšmė -- 38
 - __Pastangos__ (*Effort*):
$$E = D * V$$
 - __Potenciali apimtis__ (*Potential Volume*):
$$V^\* = (2 + N_2^\*) \log_2 (2 + n_2^\*)$$

kur $N_2^\*$ yra būtinų įėjimo ir išėjimo parametrų skaičius, o $n_2^\*$ yra mažiausias galimas skirtingų operandų skaičius.
 - __Programos lygis__ (*Program level*):
$$L = \frac{V^\*}{V}$$
Jei reikšmė maža, programa realizuota pernelyg sudėtingai.
 - __Galimų klaidų skaičius__ (*Delivered Errors*):
$$B = \frac{(E^\frac{2}{3})}{3000}$$
 - __Klaidų lygis__ (*Defect rate*):
$$DR = \frac{B}{KLOC}$$

Programos patikimumas vertinamas atsižvelgiant į programos taikymo sritį:

| Taikymo sritis                          | Toleruojamas klaidų lygis $DR$ |
|-----------------------------------------|--------------------------------|
| Pramonės programinė įranga (valdikliai) | $<5$                           |
| Bankinės sistemos                       | $<6$                           |
| Duomenų apdorojimas (duombazės)         | $<8$                           |
| Programavimo įrankiai                   | $<8$                           |
| Karinės sistemos                        | $<1$                           |
| Kosminės Sistemos                       | $<0.4$                         |
| Mokslinės Sistemos                      | $<2$                           |
| Ryšių Sistemos                          | $<6$                           |
| Interneto programinė įranga             | $<11$                          |

####4. *McCabe* ciklomatinis sudėtingumas (*Cyclomatic Complexity*, CC)
Nepriklausomų kelių programos kodo grafe skaičius.
Ciklomatinio sudėtingumo reikšmės vertinimas:

| CC reikšmė | Programos įvertinimas             |
|------------|-----------------------------------|
| $1-10$     | Paprasta, klaidų tikimybė maža    |
| $11-20$    | Vidutinio sudėtingumo             |
| $21-50$    | Sudėtinga, klaidų tikimybė didelė |
| $>50%      | Netestuojama                      |

Ciklomatinio sudėtingumo variantas yra __esminis sudėtingumas__ (*Essential complexity*, $ev(G)$) - tai ciklomatinis sudėtingumas skaičiuojamas programoje pakeitus visus struktūrizuotus sakinius paprastu sakiniu. Jei $ev(G) > 4$, tai prižiūrimumas yra blogas

####5. Prižiūrimumo indekas (*Maintainability index*, MI)
Programų sistemos priežiūriai reikalingų pastangų matas.
Prižiūrimumo indeksas gali būti skaičiuojamas tiek visai sistemai (tuomet imamos vidutinės parametrų reikšmės), tiek atskiriems jos moduliams. Galimi keli šio indekso reikšmių skaičiavimo variantai:
$$MI_1 = 171 - 3.42 * \ln(HE) - 0.23 * CC - 16.2 * \ln(LOC)$$
$$MI_2 = 171 - 3.42 * \ln(HE) - 0.23 * CC - 16.2 * \ln(LOC) + 0.99 * CM$$
$$MI_3 = 171 - 3.42 * \ln(HE) - 0.23 * CC - 16.2 * \ln(LOC) + 50 * \sin{\sqrt{2.46 * CM}}$$
$$MI_4 = 171 - 5.2 * \ln(HV) - 0.23 * CC - 16.2 * \ln(LOC)$$
kur $HE$ - *Halstead Effort*; $HV$ - *Halstead Volume*; $CC$ - *Cyclomatic Complexity*; $LOC$ - *Lines of code*; $CM$ - *Comment measurement*(%) 

Prižiūrimumo indekso reikšmės vertinimas:

**TODO: suformatuoti gražiai lentelę (išeities tekste)

| MI reikšmė | Programos įvertinimas
|-|-|
|$>85$|Geras prižiūrimumas|
|$65-85$|Vidutinis prižiūrimumas|
|$0-65$|Blogas prižiūrimumas|
|$<0$|Labai blogas programos kodas (nestruktūrizuotas, nekomentuotas)|

Programų keitimas atliekamas atsižvelgiant į programų sudėtingumo tyrimo rezultatus: laikoma, kad reikia atkreipti dėmesį į blogiausius 5% programos modulius (klases).
Jeigu sistemoje yra daugiau nei 5% modulių, kurie viršija ribinę prižiūrimumo vertę, tuomet visa sistema reikalauja priežiūros.
Jeigu sistema vertinama pagal kelias metrikas, tuomet reikia atkreipti dėmesį į tuos modulius, kurie 5% taisyklę tenkina bent pagal 2 metrikas.

## PlantUML tekstinė UML diagramų modeliavimo programa
Ši priemonė yra atviro kodo įrankis, skirtas kurti UML (*Unified Modeling Language* - Vieninga modeliavimo kalba) diagramas jas aprašant paprasta ir intuityvia kalba. Ši kalba yra DSL (*Domain-specific language* - specializuotoji kalba) tipo kalba. Šią programinę įrangą 2009 metais sukūrė ir šiuo metu prižiūri *Arnaud Roques*. Šios sistemos išeities tekstas yra talpinamas *[Sourceforge](http://sourceforge.net/projects/plantuml)* projektų talpinimo repoztorijoje ir yra parašytas Java programavimo kalba.
Šiuo metu naujausia versija yra 8024 [^1] ir iki tol yra išleidęs 126[^2] versijas. PlantUML pagal projekto svetainę yra pasiekiama ne vien per *Sourceforge* tinklapį, tačiau ir per kelis kitus distributorius, kurie sukūrė integracinius paketus platformoms. Pagal *Sourceforge* statistiką[^3] šio projekto failai yra parsiųsti 2653 kartus.
Išeities tekstas taip pat naudoja trečios šalies programinę įrangą, tačiau jų išeities tekstas nebus tiriamas.

## Analizo - programos išeities kodo tiriamoji programinė įranga


[^1]: Išeities tekstas naudotas 2015-05-04 
[^2]: Versijos atrinktos pagal *subversion* repozitorijos įrašus, žr. [Priedai/history_log.txt](Priedai/history_log.txt)
[^3]: http://sourceforge.net/projects/plantuml/files/ Paskutinį kartą peržiūrėta 2015-05-04