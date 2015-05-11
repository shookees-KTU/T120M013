# PlantUML kodo prižiūrimumo charakteristikų tyrimas

[TOC]

## Tikslas 
Susipažinti su pagrindinėmis programų išeities teksto charakteristikomis (metrikomis). Suprasti metrikų svarbą programų priežiūros kontekste. Atlikti paveldėtinės sistemos charakteristikų tyrimą.
## Teorinė dalis
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

### Pagrindinės metrikų grupės
#### 1. Dydžio metrikos
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

Globalūs (bendrieji) rezultatai yra pateikiami [1 priede](#globalus-rezultatai). Pagal rezultatus nustatomos ir įvertinamos (yra mažiau, daugiau ar apytiksliai tiek, kiek apibrėžiama tos metrikos riba) anksčiau minėtos metrikos.
Reikšmės suapvalintos iki 2 sk. po kablelio.
## 1. Dydžio metrikos

|Metrika      |Vertė|
|-------------|-----|
|Abstrakčių klasių kiekis|29|
|Vidutinis metodų abstrakčioje klasėje kiekis|12.52|
|Modulių kiekis|1718|
|Viso išeities teksto eilučių|78673|
|Viso vykdomo išeities teksto eilučių|97092|

Klasių sudėtingumas pagal LOC kiekį jose (žemas < 100; vidutinis 100 - 200; didelis 200+):

|Kiekis|% nuo visų|Sudėtingumas|
|------|----------|------------|
|1425  |88.18%    | Žemas      |
|136   |8.42%     | Vidutinis  |
|55    |3.40%     | Didelis    |
|Viso  |
|1616  |          |            |

## 2. Objektinės sudėtingumo metrikos
Globalios vidutinės reikšmės:


|Metrika|Trumpinys|Vertė|Vertinimas|
|-|-|-|-|
|Vidutinis metodų skaičius klasėje|WMC|$6.31$|geras $<20$|
|Klasės turinčios daugiau nei 24 metodus|WMC|$44$|geras $2.09%$|
|Paveldėjimo medžio gylis|DIT|$0.78$|geras|
|Klasės, kurių paveldėjimo gylis $>5$|DIT|$8$|prastas|
|Vaikų skaičius|NOC|$0.31$|prastas|
|Klasės su $>=10$ vaikų|NOC|$19$|geras|
|Jungumas tarp klasių|CBO|$7.18$|geras $<14$|
|Klasės, kur jungumas $>14$|CBO|$333$|labai prastas|
|Klasės atsakas|RFC|$20.23$|geras $<50$|
|Klasės, kurių atsakas $>=50$|RFC|$151$|labai prastas|
|Metodų rišlumo stoka|LCOM1|$25.82$|labai prastas $>5$|
|Metodai, kurių rišlumo stoka $>5$|LCOM1|$707$|labai prastas $>5$|
|Projekto sudėtingumas|DES|$9.64$|geras|

# Išvados

# Literatūra

# Priedai
## Analizo
###Globalūs rezultatai*
* - realiai metrikos pavadinimai yra atskirti "_" simboliu, tačiau taip formatuojant lentelę būna per didelis plotis, todėl "_" pakeitus tarpais lentelė sutelpa ir viskas pateikiama A4 lape.

Metrikos:

|Metrika|Pavadinimas|Paaiškinimas|
|-------|-----------|------------|
|$Kurt$ |Statistinis ekscesas|Skirstinio dažnių aibės viršūnės aštrumo laipsnis lyginant su normaliuoju skirstiniu|
|$\mu$  |Vidurkis|Vidutinė reikšmė|
|$Moda$|Moda|Dažniausia reikšmė|
|$Q_ž$|Žemutinis kvantilis|Žemutinis tikimybės dažnis|
|$Q_{max}$|Maksimalus kvantilis|Didžiausias tikimybės dažnis|
|$Q_{med}$|Kvantilio mediana|Vidurinis tikimybės dažnis|
|$Q_{min}$|Minimalus kvantilis|Mažiausias tikimybės dažnis|
|$Q_{95}$|95% kvantilis| 95% tikimybės dažnis|
|$Q_u$|Viršutinis kvantilis|Viršutins tikimybės dažnis|
|$A$    |Asimetrijos koeficientas|Duomenų aibės charakteristika skirstinios grafinės funkcijos asimetriškumui|
|$\sigma$|Standartinis nuokrypis|Atsitiktinio dydžio reikšmių slaida apie vidurkį|
|$\Sigma$|Suma|Visa suma|
|$\sigma^2$|Variacija|labiausiai tikėtinas eilinio matavimo vertės nukrypimas nuo vidurkio|


|Metrika|$Kurt$|$\mu$|$Moda$|$Q_ž$|$Q_{max}$|$Q_{med}$|$Q_{min}$|$Q_{95}$|$Q_u$|$A$|$\sigma$|$\Sigma$|$\sigma^2$|
|-------|--------|----|----|--------------|------------|---------------|------------|-----------|--------------|--------|------------------|---|--------|
|acc|228.54|5.01|0|0|525|0|0|21|2|13.08|23.17|8609|537.18|
|accm|140.62|1.61|1|1|31.25|1.25|0|3.5|2|8.20|1.36|2769.61|1.87|
|amloc|53.21|7.61|1|3.5|120.25|6|0|19.25|9.70|5.12|7.75|13090.29|60.11|
|an|0|0|0|0|0|0|0|0|0|0|0|0|0|
|anpm|6.94|1.19|1|0.6|6|1|0|3|1.5|2.15|1.00|2049.31|1.01|
|asom|0|0|0|0|0|0|0|0|0|0|0|0|0|
|auv|0|0|0|0|0|0|0|0|0|0|0|0|0|
|bd|0|0|0|0|0|0|0|0|0|0|0|0|0|
|bf|0|0|0|0|0|0|0|0|0|0|0|0|0|
|cbo|-1.30|336.78|34|177.5|611|337|1|604|521|-0.10|183.63|578602|33721.27|
|da|0|0|0|0|0|0|0|0|0|0|0|0|0|
|dbz|0|0|0|0|0|0|0|0|0|0|0|0|0|
|df|0|0|0|0|0|0|0|0|0|0|0|0|0|
|dit|1.03|1.14|0|0|6|1|0|4|2|1.14|1.20|1961|1.45|
|dnp|0|0|0|0|0|0|0|0|0|0|0|0|0|
|dupv|0|0|0|0|0|0|0|0|0|0|0|0|0|
|fgbo|0|0|0|0|0|0|0|0|0|0|0|0|0|
|lcom4|117.35|1.92|1|1|46|1|0|5|2|8.48|2.38|3301|5.66|
|loc|28.90|45.79|0|10|807|25|0|156|53|4.45|68.71|78673|4721.91|
|mlk|0|0|0|0|0|0|0|0|0|0|0|0|0|
|mmloc|52.84|17.16|1|5|389|11|0|55|22|5.09|22.60|29484|511.18|
|noa|103.64|2.25|0|0|72|1|0|8|3|7.69|4.04|3867|16.34|
|noc|122.97|0.54|0|0|49|0|0|3|0|9.24|2.51|940|6.31|
|nom|22.56|5.64|2|2|70|4|0|16|7|3.87|6.56|9702|43.15|
|npa|264.98|0.15|0|0|32|0|0|1|0|15.05|1.38|268|1.90|
|npm|28.92|4.21|1|1|64|3|0|13|5|4.35|5.43|7233|29.48|
|obaa|0|0|0|0|0|0|0|0|0|0|0|0|0|
|osf|0|0|0|0|0|0|0|0|0|0|0|0|0|
|pitfc|0|0|0|0|0|0|0|0|0|0|0|0|0|
|rfc|26.38|20.28|0|5|299|12|0|69|25|4.18|28.20|34849|795.79|
|rogu|0|0|0|0|0|0|0|0|0|0|0|0|0|
|rsva|0|0|0|0|0|0|0|0|0|0|0|0|0|
|saigv|0|0|0|0|0|0|0|0|0|0|0|0|0|
|sc|103.93|630.87|0|210|17655|424|0|1960|682|7.50|891.72|1083840|795177.37|
|ua|0|0|0|0|0|0|0|0|0|0|0|0|0|
|uaf|0|0|0|0|0|0|0|0|0|0|0|0|0|
|uav|0|0|0|0|0|0|0|0|0|0|0|0|0|

|Metrika|Vertė|
|-------|-----|
|total_abstract_classes|29|
|total_cof|0.00|
|total_eloc|97092|
|total_loc|78673|
|total_methods_per_abstract_class|12.51|
|total_modules|1718|
|total_modules_with_defined_attributes|1105|
|total_modules_with_defined_methods|1616|
|total_nom|9702|
|change_cost|0.01|


## CKJM


[^1]: Išeities tekstas naudotas 2015-05-04

[^2]: Versijos atrinktos pagal *subversion* repozitorijos įrašus, žr. [Priedai/history log.txt](Priedai/history log.txt)

[^3]: http://sourceforge.net/projects/plantuml/files/ Paskutinį kartą peržiūrėta 2015-05-04

[^4]: Programos svetainė http://www.analizo.org

[^5]: Programos svetain4 http://www.spinellis.gr/sw/ckjm