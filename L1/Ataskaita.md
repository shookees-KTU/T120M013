# PlantUML kodo prižiūrimumo charakteristikų tyrimas

[TOC]

##Tikslas
Susipažinti su pagrindinėmis programų išeities teksto charakteristikomis (metrikomis). Suprasti metrikų svarbą programų priežiūros kontekste. Atlikti paveldėtinės sistemos charakteristikų tyrimą.
##Teorinė dalis
 - __Programos prižiūrimumas__ -- programų sistemos arba jos komponento modifikavimo lengvumas siekaint ištaisyti klaidas, pagerinti charakteristikas arba pritaikyti prie pasikeitusios aplinkos. Programos prižiūrimumas yra tiesiogiai proporcingas jos sudėtingumui.
 - __Sistemos sudėtingumas__ -- tai sistemos charakteristika, kuri yra tiesiogiai proporcinga sistemos supratimui, kurio reikia norint atlikti sistemos pakeitimus.
 - __Programų metrika__ -- tai programos arba jos dalies tam tikros savybės (charakteristikos) kiekybinė (išmatuojama) išraiška.
 - __Programų evoliucija__ -- terminas naudojamas programavimo inžinerijoje apibrėžti procesui, kuris apima pakartotinį išleisto programos atnaujinimą dėl įvairių priežasčių. 
 - __Evoliucijos dėsningumai__ -- programų evoliucijos dėsniai yra dėsniai, kuriuos sudarė *Lehman* ir *Belady*. Šie dėsniai galioja trims programų kategorijoms:
    - S-tipo programa -- realizuota tiksliai pagal apibrėžtas specifikacijas;
    - P-tipo programa -- realizuota pagal vykdymo teisingumą/korektiškumą, kurį apsprendžia pats vartotojas;
    - E-tipo programa -- realizuota realaus pasaulio problemoms. Priklauso nuo veikimo aplinkos, kuriai keičiantis tenka ir E-tipo programai keistis.

Dėsniai apibrėžia priežastis, kurios motyvuoja naujos programinės įrangos kūrimą, ir priežastis, kurios lėtina programinės įrangos tobulėjimo progresą:
   1. Nuolatinių pokyčių -- programa duotoje aplinkoje būtinai privalo keistis arba ji taps vis mažiau naudinga;
   2. Augančio sudėtingumo -- kai tobulinama programa keičiasi, jos struktūra tampa vis sudėtingesnė. Tokios sistemos išsaugojimui ir supaprastinimui reikės papildomų resursų;
   3. Didelės programos evoliucijos -- programos tobulinimas yra savireguliuojantis procesas: sistemos atributai apytikriai yra invariantiški kiekvienai versijai;
   4. Organizacinio stabilumo -- programos plėtros greitis per jos gyvavimo ciklą yra apytikriai pastovus ir nepriklauso nuo skiriamų resursų;
   5. Žinojimo (apie pakeitimus) išsaugojimo -- inkrementinis sistemos keitimas kiekvienoje versijoje yra apytikriai pastovus per visą sistemos gyvavimo ciklą;
   6. Funkcinių galimybių nuolatinio augimo -- funkcinis turinys privalo pastoviai didėti tam, kad išlaikytų vartotojų pasitenkinimą visu sistemos gyvavimu metu;
   7. Kokybės mažėjimo -- sistemos kokybė kris nebent bus kruopščiai prižiūrėta ir pritaikyta aplinkos pokyčiams;
   8. Evoliucinių procesų grįžtamojo ryšio -- PĮ evoliucija neįmanoma be grįžtamojo ryšio. Evoliuciniai procesai yra daugiaagenčiai, daugiasluoksniai, daugiacikliai su grįžtamuoju ryšiu.

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


| MI reikšmė | Programos įvertinimas |
|------------|-----------------------|
| $>85$      |    Geras prižiūrimumas|
| $65-85$    |Vidutinis prižiūrimumas|
| $0-65$     |   Blogas prižiūrimumas|
| $<0$       |Labai blogas programos kodas (nestruktūrizuotas, nekomentuotas)|


Programų keitimas atliekamas atsižvelgiant į programų sudėtingumo tyrimo rezultatus: laikoma, kad reikia atkreipti dėmesį į blogiausius 5% programos modulius (klases).
Jeigu sistemoje yra daugiau nei 5% modulių, kurie viršija ribinę prižiūrimumo vertę, tuomet visa sistema reikalauja priežiūros.
Jeigu sistema vertinama pagal kelias metrikas, tuomet reikia atkreipti dėmesį į tuos modulius, kurie 5% taisyklę tenkina bent pagal 2 metrikas.

## PlantUML tekstinė UML diagramų modeliavimo programa
Ši priemonė yra atviro kodo įrankis, skirtas kurti UML (*Unified Modeling Language* - Vieninga modeliavimo kalba) diagramas jas aprašant paprasta ir intuityvia kalba. Ši kalba yra DSL (*Domain-specific language* - specializuotoji kalba) tipo kalba. Šią programinę įrangą 2009 metais sukūrė ir šiuo metu prižiūri *Arnaud Roques*. Šios sistemos išeities tekstas yra talpinamas *[Sourceforge](http://sourceforge.net/projects/plantuml)* projektų talpinimo repoztorijoje ir yra parašytas Java programavimo kalba.
Šiuo metu naujausia versija yra 8024 [^1] ir iki tol yra išleidęs 126[^2] versijas. PlantUML pagal projekto svetainę yra pasiekiama ne vien per *Sourceforge* tinklapį, tačiau ir per kelis kitus distributorius, kurie sukūrė integracinius paketus platformoms. Pagal *Sourceforge* statistiką[^3] šio projekto failai yra parsiųsti 2653 kartus.
Išeities tekstas taip pat naudoja trečios šalies programinę įrangą, tačiau jų išeities tekstas nebus tiriamas.

## Analizo - programos išeities kodo tiriamoji programinė įranga
Ši programa yra nemokamas, išplečiamas išeities teksto analizės ir vizualizacijos įrankis[^4].
Pagal github kodo panaudos statistiką, didelę dalį užima HTML tipo failai, kurie yra naudojami vizualizacijos šablonų kūrimui. Pagrindinė programinė kalba - Perl.
Ši programinė įranga pateikia šias metrikas:


| Globalios metrikos | Aprašymas | Modulio metrikos | Aprašymas |
|--------------------|-----------|------------------|-----------|
| change_cost            |Keitimo kaina| acc              |Įcentrinių jungčių klasei|
| total_abstract_classes |Viso abstrakčių klasių| accm |Vidutinis CC metodui|
| total_cof |Viso jungumo faktorių| amloc |Vidutinis LOC metodui|
| total_eloc |Viso ELOC| an |Argumentų su 'nonnull' atributu perduoda 'null'|
| total_loc |Viso LOC| anpm |Vidutinis parametrų kiekis metodui|
| total_methods_per_abstract_class |Metodų kiekis abstrakčioje klasėje| asom |Alokacijos 'typeof' neatitikimas|
| total_modules |Viso modulių| auv |Priskirta vertė yra šiukšlė arba neapibrėžta (undefined)| 
| total_modules_with_defined_attributes |Viso modulių su bent vienu atributu| bd |Blogas dealokatorius| 
| total_modules_with_defined_methods |Viso modulių su bent vienu metodu| bf |Blogas atminties atlaisvinimas (free)| 
| total_nom |Viso metodų| cbo |Jungumas tarp objektų|


| Modulios metrikos | Aprašymas | Modulios metrikos | Aprašymas |
|-------------------|-----------|-------------------|-----------|
| da |Nepasiekiamas priskyrimas| npa |Viešų atributų kiekis|
| dbz |Dalyba iš nulio| npm |Viešų metodų kiekis|
| df |Pasikartojantis to paties objekto atminties atlaisvinimas (double free)| obaa |Masyvo skaitymas už rėžių|
| dit |Paveldimumo medžio gylis| osf |Offset free|
| dnp |Derefencijavimas null pointeriui| pitfc |Potencialiai nesaugus laikinas failas su 'mktemp' komanda|
| dupv |Derefencijavimas null reikšmei| rfc |Atsakas klasei|
| fgbo |Potencialus buferio perpildymas su 'gets' komanda| rogu |Operacijos rezultatas šiukšlė arba undefined|
| lcom4 |Trūksta sąryšio metodų| rsva |Steko kintamojo adreso grąžinimas|
| loc |LOC| saigv | Steko adresas išsaugotas globaliame kintamajame|
| mlk |Atminties nutekėjimas| sc |Struktūrinis sudėtingumas|
| mmloc |Didžiausias metodo LOC| ua |Undefined alokacija su 0 baitų (CERT MEM04-C; CWE-131) |
| noa |Atributų kiekis| uaf |Naudojimas po atlaisvinimo|
| noc |Vaikų kiekis| uav |Neaprašyto argumento reikšmė|
| nom |Metodų kiekis|  |  |


## CKJM - *Chidamber* ir *Kemerer* Java metrikos
Ši programa apskaičiuojama *Chidamber* ir *Kemerer* objektines metrikas tirdami sukompiliuotus Java projektus[^5]. Apskaičiuojamos 6 metrikos kiekvienai klasei:

 1. WMC -- *Weighted Methods per Class*, metodų svoris klasei;
 2. DIT -- *Depth of Inheritance Tree*, paveldėjimo medžio gylis;
 3. NOC -- *Number of children*, vaikų kiekis;
 4. CBO -- *Coupling Between Object classes*, Jungumas tarp objektų klasių;
 5. RFC -- *Response For a Class*, atsakas klasei;
 6. LCOM -- *Lack of cohesion in methods*, sąryšio trūkumas metoduose.

Taip pat kiekvienai klasei papildomai apskaičiuojama (Ne pagal *Chidamber ir *Kemerer* objektines metrikas):

 * Ca -- *Afferent couplings* Įcentrinis jungumas;
 * NPM -- *Number of Public Methods* Viešų metodų kiekis.

# Rezultatai

# Išvados

# Literatūra

# Priedai
## Analizo

## CKJM


[^1]: Išeities tekstas naudotas 2015-05-04 

[^2]: Versijos atrinktos pagal *subversion* repozitorijos įrašus, žr. [Priedai/history_log.txt](Priedai/history_log.txt)

[^3]: http://sourceforge.net/projects/plantuml/files/ Paskutinį kartą peržiūrėta 2015-05-04

[^4]: Programos svetainė http://www.analizo.org

[^5]: Programos svetain4 http://www.spinellis.gr/sw/ckjm