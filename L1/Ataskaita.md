# PlantUML kodo prižiūrimumo charakteristikų tyrimas

[TOC]

##Tikslas
Susipažinti su pagrindinėmis programų išeities teksto charakteristikomis (metrikomis). Suprasti metrikų svarbą programų priežiūros kontekste. Atlikti paveldėtinės sistemos charakteristikų tyrimą.
##Teorinė dalis
 -   Programos prižiūrimumas   -- programų sistemos arba jos komponento modifikavimo lengvumas siekaint ištaisyti klaidas, pagerinti charakteristikas arba pritaikyti prie pasikeitusios aplinkos. Programos prižiūrimumas yra tiesiogiai proporcingas jos sudėtingumui.
 -   Sistemos sudėtingumas   -- tai sistemos charakteristika, kuri yra tiesiogiai proporcinga sistemos supratimui, kurio reikia norint atlikti sistemos pakeitimus.
 -   Programų metrika   -- tai programos arba jos dalies tam tikros savybės (charakteristikos) kiekybinė (išmatuojama) išraiška.
 -   Programų evoliucija   -- terminas naudojamas programavimo inžinerijoje apibrėžti procesui, kuris apima pakartotinį išleisto programos atnaujinimą dėl įvairių priežasčių.
 -   Evoliucijos dėsningumai   -- programų evoliucijos dėsniai yra dėsniai, kuriuos sudarė *Lehman* ir *Belady*. Šie dėsniai galioja trims programų kategorijoms:
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
 -   Metodų skaičius klasėje   (*weighted methods per class*, WMC). Kuo WMC didesnis, tuo klasėje gali būti daugiau klaidų, tuo daugiau reikia pastangų klasės sukūrimui ir priežiūrai. Klasės su aukšta WMC reikšme turi būti išskaidytos į kelias mažesnes klases. Rekomenduojama, kad WMC neviršytų 20, o sistemoje būtų ne daugiau kaip 10% klasių, kurių WMC reikšmė yra didesnė nei 24.
 -   Jungumas tarp klasių   (*coupling between object class*, CBO). Kuo didesnis jungumas, tuo sudetingesnė klasės priežiūra. Jei CBO > 14, tai klasę reikia labai gerai ištestuoti.
 -   Klasės atsakas   (*response for a class*, RFC) - lygus klasės metodų ir klasės iškviečiamų kitų klasių metodų sumai. Didesnė RFC reikšmė rodo aukštesnį sudėtingumą ir blogesnį suprantamumą. Kritinė RFC reikšmė yra lygi 50.
 -   Vaikų skaičius   (*number of children*, NOC) - bazinę klasę paveldinčių klasių skaičius (paveldėjimo hierarchijos plotis). Aukšta NOC reikšmė rodo mažesnę klaidų tikimybę, tačiau aukštos NOC ir WMC reikšmės rodo didelį bazinės klasės sudėtingumą. TOkiu atveju bazinę klasę reikia restruktūrizuoti.
 -   Paveldėjimo medžio gylis   (*depth of inheritance tree*, DIT) - ilgiausio kelio iki šakninės klasės ilgis. Aukštesnė DIT reikšmė reiškia sudėtingesnę sistemą, kurioje gali būti daugiau klaidų. Rekomenduojama, kad DIT reikšmė būtų <= 5
 -   Metodų rišlumo stoka   (*lack of cohesion of methods*, LCOM1). Rekomenduojama, kad LCOM1 < 5.
 -   Projekto sudėtingumas   (*design complexity*, DES). Išvestinė metrika, kuri yra skaičiuojama pagal formulę
 $$DES = 0.2 * WMC + 0.3 * RFC + 0.3 * CBO + 0.2 * DIT$$
 Kritinė DES reikšmė yra 25.

####3. *Halstead*'o sudėtingumo metrikos
Skaičiuojant *Halstead*'o sudėtingumą vertinamas programos skirtingų operatorių skaičius $n 1$, skirtingų operandų skaičius $n 2$, visų operatorių skaičius $N 1$ ir visų operandų skaičius $N 2$.
Apibrėžiamos tokios metrikos:
 -   Žodynas   (*Vocabulary*):
$$n = n 1 + n 2$$
 -   Ilgis   (*Length*):
$$N = N 1 + N 2$$
 -   Apimtis   (*Volume*):
$$V = N \log 2{n}$$
 -   Sunkumas   (*Difficulty*):
$$D = (\frac{n 1}{2}) * (\frac{N 2}{n 2})$$
Kritinė reikšmė -- 38
 -   Pastangos   (*Effort*):
$$E = D * V$$
 -   Potenciali apimtis   (*Potential Volume*):
$$V^\* = (2 + N 2^\*) \log 2 (2 + n 2^\*)$$

kur $N 2^\*$ yra būtinų įėjimo ir išėjimo parametrų skaičius, o $n 2^\*$ yra mažiausias galimas skirtingų operandų skaičius.
 -   Programos lygis   (*Program level*):
$$L = \frac{V^\*}{V}$$
Jei reikšmė maža, programa realizuota pernelyg sudėtingai.
 -   Galimų klaidų skaičius   (*Delivered Errors*):
$$B = \frac{(E^\frac{2}{3})}{3000}$$
 -   Klaidų lygis   (*Defect rate*):
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

Ciklomatinio sudėtingumo variantas yra   esminis sudėtingumas   (*Essential complexity*, $ev(G)$) - tai ciklomatinis sudėtingumas skaičiuojamas programoje pakeitus visus struktūrizuotus sakinius paprastu sakiniu. Jei $ev(G) > 4$, tai prižiūrimumas yra blogas

####5. Prižiūrimumo indekas (*Maintainability index*, MI)
Programų sistemos priežiūriai reikalingų pastangų matas.
Prižiūrimumo indeksas gali būti skaičiuojamas tiek visai sistemai (tuomet imamos vidutinės parametrų reikšmės), tiek atskiriems jos moduliams. Galimi keli šio indekso reikšmių skaičiavimo variantai:
$$MI 1 = 171 - 3.42 * \ln(HE) - 0.23 * CC - 16.2 * \ln(LOC)$$
$$MI 2 = 171 - 3.42 * \ln(HE) - 0.23 * CC - 16.2 * \ln(LOC) + 0.99 * CM$$
$$MI 3 = 171 - 3.42 * \ln(HE) - 0.23 * CC - 16.2 * \ln(LOC) + 50 * \sin{\sqrt{2.46 * CM}}$$
$$MI 4 = 171 - 5.2 * \ln(HV) - 0.23 * CC - 16.2 * \ln(LOC)$$
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
| change cost            |Keitimo kaina| acc              |Įcentrinių jungčių klasei|
| total abstract classes |Viso abstrakčių klasių| accm |Vidutinis CC metodui|
| total cof |Viso jungumo faktorių| amloc |Vidutinis LOC metodui|
| total eloc |Viso ELOC| an |Argumentų su 'nonnull' atributu perduoda 'null'|
| total loc |Viso LOC| anpm |Vidutinis parametrų kiekis metodui|
| total methods per abstract class |Metodų kiekis abstrakčioje klasėje| asom |Alokacijos 'typeof' neatitikimas|
| total modules |Viso modulių| auv |Priskirta vertė yra šiukšlė arba neapibrėžta (undefined)|
| total modules with defined attributes |Viso modulių su bent vienu atributu| bd |Blogas dealokatorius|
| total modules with defined methods |Viso modulių su bent vienu metodu| bf |Blogas atminties atlaisvinimas (free)|
| total nom |Viso metodų| cbo |Jungumas tarp objektų|


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

Globalūs (bendrieji) rezultatai yra pateikiami [1 priede](#globalus-rezultatai). Pagal rezultatus nustatomos

# Išvados

# Literatūra

# Priedai
## Analizo
###Globalūs rezultatai*
* - realiai metrikos pavadinimai yra atskirti "_" simboliu, tačiau taip formatuojant lentelę būna per didelis plotis, todėl "_" pakeitus tarpais lentelė sutelpa ir viskas pateikiama A4 lape.

|Metrika|Vertė|Metrika|Vertė|
|-------|-----|-------|-----|
|acc kurtosis|228.547982459137|acc mean|5.01105937136205|
|acc mode|0|acc quantile lower|0|
|acc quantile max|525|acc quantile median|0|
|acc quantile min|0|acc quantile ninety five|21|
|acc quantile upper|2|acc skewness|13.0810811376735|
|acc standard deviation|23.1772033414368|acc sum|8609|
|acc variance|537.182754730311|accm kurtosis|140.626333942121|
|accm mean|1.61211507812085|accm mode|1|
|accm quantile lower|1|accm quantile max|31.25|
|accm quantile median|1.25|accm quantile min|0|
|accm quantile ninety five|3.5|accm quantile upper|2|
|accm skewness|8.20706594888645|accm standard deviation|1.36815325250871|
|accm sum|2769.61370421161|accm variance|1.87184332235016|
|amloc kurtosis|53.2135822384211|amloc mean|7.61949709834696|
|amloc mode|1|amloc quantile lower|3.5|
|amloc quantile max|120.25|amloc quantile median|6|
|amloc quantile min|0|amloc quantile ninety five|19.25|
|amloc quantile upper|9.70238095238095|amloc skewness|5.1215489416558|
|amloc standard deviation|7.75329005542143|amloc sum|13090.2960149601|
|amloc variance|60.1135066834968|an kurtosis|0|
|an mean|0|an mode|0|
|an quantile lower|0|an quantile max|0|
|an quantile median|0|an quantile min|0|
|an quantile ninety five|0|an quantile upper|0|
|an skewness|0|an standard deviation|0|
|an sum|0|an variance|0|
|anpm kurtosis|6.94871156336281|anpm mean|1.19285010990947|
|anpm mode|1|anpm quantile lower|0.6|
|anpm quantile max|6|anpm quantile median|1|
|anpm quantile min|0|anpm quantile ninety five|3|
|anpm quantile upper|1.5|anpm skewness|2.15581463068434|
|anpm standard deviation|1.00848097957434|anpm sum|2049.31648882447|
|anpm variance|1.01703388616321|asom kurtosis|0|
|asom mean|0|asom mode|0|
|asom quantile lower|0|asom quantile max|0|
|asom quantile median|0|asom quantile min|0|
|asom quantile ninety five|0|asom quantile upper|0|
|asom skewness|0|asom standard deviation|0|
|asom sum|0|asom variance|0|
|auv kurtosis|0|auv mean|0|
|auv mode|0|auv quantile lower|0|
|auv quantile max|0|auv quantile median|0|
|auv quantile min|0|auv quantile ninety five|0|
|auv quantile upper|0|auv skewness|0|
|auv standard deviation|0|auv sum|0|
|auv variance|0|bd kurtosis|0|
|bd mean|0|bd mode|0|
|bd quantile lower|0|bd quantile max|0|
|bd quantile median|0|bd quantile min|0|
|bd quantile ninety five|0|bd quantile upper|0|
|bd skewness|0|bd standard deviation|0|
|bd sum|0|bd variance|0|
|bf kurtosis|0|bf mean|0|
|bf mode|0|bf quantile lower|0|
|bf quantile max|0|bf quantile median|0|
|bf quantile min|0|bf quantile ninety five|0|
|bf quantile upper|0|bf skewness|0|
|bf standard deviation|0|bf sum|0|
|bf variance|0|cbo kurtosis|-1.30741881857161|
|cbo mean|336.78812572759|cbo mode|34|
|cbo quantile lower|177.5|cbo quantile max|611|
|cbo quantile median|337|cbo quantile min|1|
|cbo quantile ninety five|604|cbo quantile upper|521|
|cbo skewness|-0.102184558545387|cbo standard deviation|183.633521361426|
|cbo sum|578602|cbo variance|33721.2701675975|
|change cost|0.01|da kurtosis|0|
|da mean|0|da mode|0|
|da quantile lower|0|da quantile max|0|
|da quantile median|0|da quantile min|0|
|da quantile ninety five|0|da quantile upper|0|
|da skewness|0|da standard deviation|0|
|da sum|0|da variance|0|
|dbz kurtosis|0|dbz mean|0|
|dbz mode|0|dbz quantile lower|0|
|dbz quantile max|0|dbz quantile median|0|
|dbz quantile min|0|dbz quantile ninety five|0|
|dbz quantile upper|0|dbz skewness|0|
|dbz standard deviation|0|dbz sum|0|
|dbz variance|0|df kurtosis|0|
|df mean|0|df mode|0|
|df quantile lower|0|df quantile max|0|
|df quantile median|0|df quantile min|0|
|df quantile ninety five|0|df quantile upper|0|
|df skewness|0|df standard deviation|0|
|df sum|0|df variance|0|
|dit kurtosis|1.03513500873182|dit mean|1.14144353899884|
|dit mode|0|dit quantile lower|0|
|dit quantile max|6|dit quantile median|1|
|dit quantile min|0|dit quantile ninety five|4|
|dit quantile upper|2|dit skewness|1.14854868315941|
|dit standard deviation|1.20729418240917|dit sum|1961|
|dit variance|1.45755924287902|dnp kurtosis|0|
|dnp mean|0|dnp mode|0|
|dnp quantile lower|0|dnp quantile max|0|
|dnp quantile median|0|dnp quantile min|0|
|dnp quantile ninety five|0|dnp quantile upper|0|
|dnp skewness|0|dnp standard deviation|0|
|dnp sum|0|dnp variance|0|
|dupv kurtosis|0|dupv mean|0|
|dupv mode|0|dupv quantile lower|0|
|dupv quantile max|0|dupv quantile median|0|
|dupv quantile min|0|dupv quantile ninety five|0|
|dupv quantile upper|0|dupv skewness|0|
|dupv standard deviation|0|dupv sum|0|
|dupv variance|0|fgbo kurtosis|0|
|fgbo mean|0|fgbo mode|0|
|fgbo quantile lower|0|fgbo quantile max|0|
|fgbo quantile median|0|fgbo quantile min|0|
|fgbo quantile ninety five|0|fgbo quantile upper|0|
|fgbo skewness|0|fgbo standard deviation|0|
|fgbo sum|0|fgbo variance|0|
|lcom4 kurtosis|117.359947801532|lcom4 mean|1.92142025611176|
|lcom4 mode|1|lcom4 quantile lower|1|
|lcom4 quantile max|46|lcom4 quantile median|1|
|lcom4 quantile min|0|lcom4 quantile ninety five|5|
|lcom4 quantile upper|2|lcom4 skewness|8.48281078722283|
|lcom4 standard deviation|2.3808094792925|lcom4 sum|3301|
|lcom4 variance|5.66825377668904|loc kurtosis|28.9038576281626|
|loc mean|45.7933643771828|loc mode|0|
|loc quantile lower|10|loc quantile max|807|
|loc quantile median|25|loc quantile min|0|
|loc quantile ninety five|156|loc quantile upper|53|
|loc skewness|4.45804025680692|loc standard deviation|68.7162238494271|
|loc sum|78673|loc variance|4721.91942012458|
|mlk kurtosis|0|mlk mean|0|
|mlk mode|0|mlk quantile lower|0|
|mlk quantile max|0|mlk quantile median|0|
|mlk quantile min|0|mlk quantile ninety five|0|
|mlk quantile upper|0|mlk skewness|0|
|mlk standard deviation|0|mlk sum|0|
|mlk variance|0|mmloc kurtosis|52.8439436071371|
|mmloc mean|17.1618160651921|mmloc mode|1|
|mmloc quantile lower|5|mmloc quantile max|389|
|mmloc quantile median|11|mmloc quantile min|0|
|mmloc quantile ninety five|55|mmloc quantile upper|22|
|mmloc skewness|5.09134615902239|mmloc standard deviation|22.6094569862887|
|mmloc sum|29484|mmloc variance|511.187545214838|
|noa kurtosis|103.642975025057|noa mean|2.25087310826542|
|noa mode|0|noa quantile lower|0|
|noa quantile max|72|noa quantile median|1|
|noa quantile min|0|noa quantile ninety five|8|
|noa quantile upper|3|noa skewness|7.69531435827785|
|noa standard deviation|4.04336378947464|noa sum|3867|
|noa variance|16.3487907340347|noc kurtosis|122.978840945913|
|noc mean|0.547147846332945|noc mode|0|
|noc quantile lower|0|noc quantile max|49|
|noc quantile median|0|noc quantile min|0|
|noc quantile ninety five|3|noc quantile upper|0|
|noc skewness|9.24325632053896|noc standard deviation|2.51306209351755|
|noc sum|940|noc variance|6.3154810858748|
|nom kurtosis|22.5647654078428|nom mean|5.64726426076834|
|nom mode|2|nom quantile lower|2|
|nom quantile max|70|nom quantile median|4|
|nom quantile min|0|nom quantile ninety five|16|
|nom quantile upper|7|nom skewness|3.87893287064606|
|nom standard deviation|6.56929561002518|nom sum|9702|
|nom variance|43.1556448118961|npa kurtosis|264.982523296634|
|npa mean|0.155995343422584|npa mode|0|
|npa quantile lower|0|npa quantile max|32|
|npa quantile median|0|npa quantile min|0|
|npa quantile ninety five|1|npa quantile upper|0|
|npa skewness|15.0568825738445|npa standard deviation|1.38175844681206|
|npa sum|268|npa variance|1.90925640533649|
|npm kurtosis|28.9256145365752|npm mean|4.21012805587893|
|npm mode|1|npm quantile lower|1|
|npm quantile max|64|npm quantile median|3|
|npm quantile min|0|npm quantile ninety five|13|
|npm quantile upper|5|npm skewness|4.35956941928052|
|npm standard deviation|5.43008422221552|npm sum|7233|
|npm variance|29.4858146603539|obaa kurtosis|0|
|obaa mean|0|obaa mode|0|
|obaa quantile lower|0|obaa quantile max|0|
|obaa quantile median|0|obaa quantile min|0|
|obaa quantile ninety five|0|obaa quantile upper|0|
|obaa skewness|0|obaa standard deviation|0|
|obaa sum|0|obaa variance|0|
|osf kurtosis|0|osf mean|0|
|osf mode|0|osf quantile lower|0|
|osf quantile max|0|osf quantile median|0|
|osf quantile min|0|osf quantile ninety five|0|
|osf quantile upper|0|osf skewness|0|
|osf standard deviation|0|osf sum|0|
|osf variance|0|pitfc kurtosis|0|
|pitfc mean|0|pitfc mode|0|
|pitfc quantile lower|0|pitfc quantile max|0|
|pitfc quantile median|0|pitfc quantile min|0|
|pitfc quantile ninety five|0|pitfc quantile upper|0|
|pitfc skewness|0|pitfc standard deviation|0|
|pitfc sum|0|pitfc variance|0|
|rfc kurtosis|26.3816035171695|rfc mean|20.2846332945285|
|rfc mode|0|rfc quantile lower|5|
|rfc quantile max|299|rfc quantile median|12|
|rfc quantile min|0|rfc quantile ninety five|69|
|rfc quantile upper|25|rfc skewness|4.18692689369344|
|rfc standard deviation|28.2098985745823|rfc sum|34849|
|rfc variance|795.798377588221|rogu kurtosis|0|
|rogu mean|0|rogu mode|0|
|rogu quantile lower|0|rogu quantile max|0|
|rogu quantile median|0|rogu quantile min|0|
|rogu quantile ninety five|0|rogu quantile upper|0|
|rogu skewness|0|rogu standard deviation|0|
|rogu sum|0|rogu variance|0|
|rsva kurtosis|0|rsva mean|0|
|rsva mode|0|rsva quantile lower|0|
|rsva quantile max|0|rsva quantile median|0|
|rsva quantile min|0|rsva quantile ninety five|0|
|rsva quantile upper|0|rsva skewness|0|
|rsva standard deviation|0|rsva sum|0|
|rsva variance|0|saigv kurtosis|0|
|saigv mean|0|saigv mode|0|
|saigv quantile lower|0|saigv quantile max|0|
|saigv quantile median|0|saigv quantile min|0|
|saigv quantile ninety five|0|saigv quantile upper|0|
|saigv skewness|0|saigv standard deviation|0|
|saigv sum|0|saigv variance|0|
|sc kurtosis|103.938670255463|sc mean|630.873108265425|
|sc mode|0|sc quantile lower|210|
|sc quantile max|17655|sc quantile median|424|
|sc quantile min|0|sc quantile ninety five|1960|
|sc quantile upper|682|sc skewness|7.50382351104905|
|sc standard deviation|891.727184937954|sc sum|1083840|
|sc variance|795177.372357369|total abstract classes|29|
|total cof|0.00291849701302391|total eloc|97092|
|total loc|78673|total methods per abstract class|12.5172413793103|
|total modules|1718|total modules with defined attributes|1105|
|total modules with defined methods|1616|total nom|9702|
|ua kurtosis|0|ua mean|0|
|ua mode|0|ua quantile lower|0|
|ua quantile max|0|ua quantile median|0|
|ua quantile min|0|ua quantile ninety five|0|
|ua quantile upper|0|ua skewness|0|
|ua standard deviation|0|ua sum|0|
|ua variance|0|uaf kurtosis|0|
|uaf mean|0|uaf mode|0|
|uaf quantile lower|0|uaf quantile max|0|
|uaf quantile median|0|uaf quantile min|0|
|uaf quantile ninety five|0|uaf quantile upper|0|
|uaf skewness|0|uaf standard deviation|0|
|uaf sum|0|uaf variance|0|
|uav kurtosis|0|uav mean|0|
|uav mode|0|uav quantile lower|0|
|uav quantile max|0|uav quantile median|0|
|uav quantile min|0|uav quantile ninety five|0|
|uav quantile upper|0|uav skewness|0|
|uav standard deviation|0|uav sum|0|
|uav variance|0|||

## CKJM


[^1]: Išeities tekstas naudotas 2015-05-04

[^2]: Versijos atrinktos pagal *subversion* repozitorijos įrašus, žr. [Priedai/history log.txt](Priedai/history log.txt)

[^3]: http://sourceforge.net/projects/plantuml/files/ Paskutinį kartą peržiūrėta 2015-05-04

[^4]: Programos svetainė http://www.analizo.org

[^5]: Programos svetain4 http://www.spinellis.gr/sw/ckjm