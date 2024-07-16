---
title: Vergelijkbare records ophalen met functies van hogere volgorde
description: Leer hoe te om gelijkaardige of verwante verslagen van één of meerdere datasets te identificeren en terug te winnen die op gelijkenis metrisch en gelijkenis drempel worden gebaseerd. Deze workflow kan betekenisvolle relaties of overlappingen tussen verschillende gegevenssets benadrukken.
exl-id: 4810326a-a613-4e6a-9593-123a14927214
source-git-commit: 27eab04e409099450453a2a218659e576b8f6ab4
workflow-type: tm+mt
source-wordcount: '4031'
ht-degree: 2%

---

# Verdien gelijkbare verslagen met hogere orde functies

Gebruik Data Distiller-functies in hogere volgorde om een aantal veelvoorkomende gebruiksgevallen op te lossen. Om gelijkaardige of verwante verslagen van één of meerdere datasets te identificeren en terug te winnen, gebruik de filter, transformatie, en verminder functies zoals die in deze gids worden beschreven. Leren hoe de hoog-ordefuncties kunnen worden gebruikt om complexe gegevenstypes te verwerken, zie de documentatie over hoe te [ serie en kaartgegevenstypes beheren ](../sql/higher-order-functions.md).

Gebruik deze handleiding om producten van verschillende datasets te identificeren die een significante gelijkenis in hun kenmerken of eigenschappen hebben. Deze methodologie biedt oplossingen voor onder andere gegevensdeduplicatie, koppeling van records, aanbevelingssystemen, het opvragen van informatie en tekstanalyse.

In het document wordt beschreven hoe u een samenvoeging op basis van overeenkomsten implementeert. Vervolgens worden de functies in de hogere volgorde van Data Distiller gebruikt om de gelijkenis tussen gegevenssets te berekenen en deze op basis van geselecteerde kenmerken te filteren. SQL de codefragmenten en de verklaringen worden verstrekt voor elke stap van het proces. De workflow implementeert overeenkomsten op basis van gelijkenis met de Jaccard-maateenheid en tokenisering met behulp van Data Distiller-functies in hogere volgorde. Deze methodes worden dan gebruikt om gelijkaardige of verwante verslagen van één of meerdere datasets te identificeren en terug te winnen die op gelijkenis metrisch worden gebaseerd. De zeer belangrijke secties van het proces omvatten: [ kenization die hoog-orde functies ](#data-transformation) gebruikt, [ dwars-toetreedt van unieke elementen ](#cross-join-unique-elements), de [ Jaccard gelijkenisberekening ](#compute-the-jaccard-similarity-measure), en het [ op drempel-gebaseerde filtreren ](#similarity-threshold-filter).

## Vereisten

Voordat u doorgaat met dit document, moet u vertrouwd zijn met de volgende concepten:

- A **gelijkenis sluit zich aan** is een verrichting die paren verslagen van één of meerdere lijsten identificeert en terugwint die op een maatregel van gelijkenis tussen de verslagen worden gebaseerd. De belangrijkste vereisten voor een gelijkenis verbinden zijn als volgt:
   - **metrische Gelijksoortigheid van 0}**: Een gelijkenis sluit zich aan bij baseert zich op vooraf bepaalde metrische gelijkenis of een maatregel. Dit zijn onder andere: de gelijkenis van het werkgebied, de cosingelijkenis, de bewerkingsafstand, enzovoort. De metrische waarde is afhankelijk van de aard van de gegevens en het gebruiksgeval. Deze metrische waarde kwantificeert hoe gelijkaardig of ongelijkaardig twee verslagen zijn.
   - **Drempel**: Een gelijkenisdrempel wordt gebruikt om te bepalen wanneer de twee verslagen als gelijkaardig genoeg worden beschouwd om in te sluiten bij resultaat. Records met een overeenkomstenscore die hoger is dan de drempel worden beschouwd als overeenkomsten.
- De **gelijkenis van het Jaccard** index, of de gelijkenis van het Jaccard meting, is een statistiek die wordt gebruikt om de gelijkenis en de diversiteit van steekproefreeksen te meten. Dit wordt gedefinieerd als de grootte van de doorsnede gedeeld door de grootte van de samenvoeging van de steekproefreeksen. De overeenkomende JACARD-meting loopt van 0 tot en met 1. Een Jaccard-gelijkenis van nul geeft aan dat de sets niet gelijk zijn en een Jaccard-gelijkenis van één geeft aan dat de sets identiek zijn.
  ![ A venn- diagram om de gelijkenismeting van het Jacard te illustreren.](../images/use-cases/jaccard-similarity.png)
- **hoog-ordefuncties** in Gegevens Distiller zijn dynamische, gealigneerde hulpmiddelen die gegevens direct binnen SQL verklaringen verwerken en omzetten. Deze veelzijdige functies elimineren de behoefte aan veelvoudige stappen in gegevensmanipulatie, vooral wanneer [ het behandelen van complexe types zoals series en kaarten ](../sql/higher-order-functions.md). Door vraagefficiency te verbeteren en transformaties te vereenvoudigen, dragen de hogere ordefuncties aan flexibelere analyses en betere besluitvorming in diverse bedrijfsscenario&#39;s bij.

## Aan de slag

De gegevens Distiller SKU wordt vereist om de hoger-ordefuncties op uw gegevens van Adobe Experience Platform uit te voeren. Als u geen gegevens Distiller SKU hebt, contacteer uw vertegenwoordiger van de klantendienst van de Adobe voor meer informatie.

## Gelijksoortigheid vaststellen {#establish-similarity}

Voor dit gebruik is een maat vereist voor de gelijkenis tussen teksttekenreeksen die later kan worden gebruikt om een drempelwaarde voor filteren vast te stellen. In dit voorbeeld vertegenwoordigen de producten in Set A en Set B de woorden in twee documenten.

De JACARD-gelijkenismaatregel kan worden toegepast op een groot aantal gegevenstypen, zoals tekstgegevens, categoriale gegevens en binaire gegevens. Het is ook geschikt voor verwerking in real time of batch, omdat het rekenkundig efficiënt kan zijn om voor grote datasets te berekenen.

Productset A en Set B bevatten de testgegevens voor deze workflow.

- Productset A: `{iPhone, iPad, iWatch, iPad Mini}`
- Productset B: `{iPhone, iPad, Macbook Pro}`

Om de gelijkenis van Jaccard tussen productreeksen A en B te berekenen, vind eerst de **doorsnede** (gemeenschappelijke elementen) van de productreeksen. In dit geval, `{iPhone, iPad}`. Daarna, vind de **unie** (alle unieke elementen) van beide productreeksen. In dit voorbeeld, `{iPhone, iPad, iWatch, iPad Mini, Macbook Pro}`.

Gebruik ten slotte de vergelijkingsformule Jaccard: `J(A,B) = A∪B / A∩B` om de gelijkenis te berekenen.

J = Jaccard-afstand
A = set 1
B = set 2

De Jaccard-gelijkenis tussen productsets A en B is 0,4. Dit wijst op een matige mate van gelijkenis tussen de woorden die in de twee documenten worden gebruikt. Deze overeenkomst tussen de twee sets definieert de kolommen in de samenvoeging. Deze kolommen vertegenwoordigen stukken informatie, of kenmerken verbonden aan de gegevens, die in een lijst worden opgeslagen en voor het uitvoeren van de gelijkenisberekeningen worden gebruikt.

### Paarsgewijze JACARD-berekening met tekenreeksgelijkenis {#pairwise-similarity}

Als u de overeenkomsten tussen tekenreeksen nauwkeuriger wilt vergelijken, moet de paarsgewijze gelijkenis worden berekend. Met paradoxale gelijkenis worden uiterst dimensionale objecten gesplitst in kleinere dimensionale objecten voor vergelijking en analyse. Hiertoe wordt een tekenreeks opgedeeld in kleinere delen of eenheden (tokens). Het kunnen individuele letters, groepen letters (zoals lettergrepen) of hele woorden zijn. De gelijkenis wordt berekend voor elk paar tekenen tussen elk element in Reeks A met elk element in Reeks B. Deze koppeling vormt de basis voor analytische en computervergelijkingen, relaties en inzichten die op basis van de gegevens moeten worden gemaakt.

Voor de paarsgewijze berekening van de gelijkenis gebruikt dit voorbeeld bi-grammen van het karakter (twee karaktertekenen) om een gelijkenis tussen de tekstkoorden van de producten in Reeks A en Reeks B te vergelijken. Een twee-gram is een opeenvolgende opeenvolging van twee punten of elementen in een bepaalde opeenvolging of tekst. Je kan dit veralgemenen tot n-grammen.

In dit voorbeeld wordt ervan uitgegaan dat de zaak er niet toe doet en dat er geen rekening moet worden gehouden met spaties. Volgens deze criteria hebben set A en set B de volgende twee grammen:

Productset A twee gram:

- iPhone (5): &quot;ip&quot;, &quot;ph&quot;, &quot;ho&quot;, &quot;on&quot;, &quot;ne&quot;
- iPad (3): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;
- iWatch (5): &quot;iw&quot;, &quot;wa&quot;, &quot;at&quot;, &quot;tc&quot;, &quot;ch&quot;
- iPad Mini (7): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;, &quot;dm&quot;, &quot;mi&quot;, &quot;in&quot;, &quot;ni&quot;

Productset B bi-grammen:

- iPhone (5): &quot;ip&quot;, &quot;ph&quot;, &quot;ho&quot;, &quot;on&quot;, &quot;ne&quot;
- iPad (3): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;
- Macbook Pro (9): &quot;Ma&quot;, &quot;ac&quot;, &quot;cb&quot;, &quot;bo&quot;, &quot;oo&quot;, &quot;ok&quot;, &quot;kp&quot;, &quot;pr&quot;, &quot;ro&quot;

Vervolgens berekent u de gelijkheidscoëfficiënt voor elk paar:

|                   | iPhone (Set B) | iPad (Set B) | Macbook Pro (Set B) |
|-------------------|----------------------------------------------|---------------------------------------------|-------------------------------------------|
| iPhone (Set A) | (Intersectie: 5, Unie: 5) = 5 / 5 = 1 | (Doorsnede: 1, Unie: 7) =1 / 7 Wacht 0,14 | (Intersectie: 0, Unie: 14) = 0 / 14 = 0 |
| iPad (Set A) | (Doorsnede: 1, Unie: 7) = 1 / 7×0,14 | (Intersectie: 3, Unie: 3) = 3 / 3 = 1 | (Intersectie: 0, Unie: 12) = 0 / 12 = 0 |
| iWatch (Set A) | (Intersectie: 0, Unie: 8) = 0 / 8 = 0 | (Intersectie: 0, Unie: 8) = 0 / 8 = 0 | (Intersectie: 0, Unie: 8) = 0 / 8 =0 |
| iPad Mini (Set A) | (Doorsnede: 1, Unie: 11) = 1 / 11 til 0,09 | (Doorsnede: 3, Unie: 7) = 3 / 7×0,43 | (Intersectie: 0, Unie: 16) = 0 / 16 = 0 |

{style="table-layout:auto"}

## Maak de testgegevens met SQL {#create-test-data}

Als u handmatig een testtabel voor de productsets wilt maken, gebruikt u de SQL-instructie CREATE TABLE.

```SQL {line-numbers="true"}
CREATE TABLE featurevector1 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'iWatch'
     UNION ALL
    SELECT 'iPad Mini'
);
SELECT * FROM featurevector1;
```

De volgende beschrijvingen bevatten een uitsplitsing van het SQL-codeblok hierboven:

- Regel 1: `CREATE TEMP TABLE featurevector1 AS`: deze instructie maakt een tijdelijke tabel met de naam `featurevector1` . Tijdelijke tabellen zijn doorgaans alleen toegankelijk binnen de huidige sessie en worden automatisch aan het einde van de sessie verwijderd.
- Regel 1 en 2: `SELECT * FROM (...)`: Dit gedeelte van de code is een subquery die wordt gebruikt om de gegevens te genereren die in de `featurevector1` -tabel worden ingevoegd.
Binnen de subquery worden meerdere `SELECT` -instructies gecombineerd met de opdracht `UNION ALL` . Elke instructie `SELECT` genereert één rij gegevens met de opgegeven waarden voor de kolom `ProductName` .
- Regel 3: `SELECT 'iPad' AS ProductName` : hiermee wordt een rij gegenereerd met de waarde `iPad` in de kolom `ProductName` .
- Regel 5: `SELECT 'iPhone'` : hiermee wordt een rij gegenereerd met de waarde `iPhone` in de kolom `ProductName` .

De SQL-instructie maakt een tabel zoals hieronder wordt weergegeven:

|   | `ProductName` |
|---|---------------|
| 1 | iPad |
| 2 | iPhone |
| 3 | iWatch |
| 4 | iPad Mini |

{style="table-layout:auto"}

Gebruik de volgende SQL-instructie om de tweede eigenschapvector te maken:

```SQL
CREATE TABLE featurevector2 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'Macbook Pro'
);
SELECT * FROM featurevector2;
```

## Gegevenstransformaties {#data-transformation}

In dit voorbeeld moeten verschillende handelingen worden uitgevoerd om de sets nauwkeurig te vergelijken. In de eerste plaats worden alle witruimten verwijderd uit de eigenschapvectoren, omdat ervan wordt uitgegaan dat ze niet bijdragen aan de gelijkenismaatregel. Vervolgens worden eventuele duplicaten die aanwezig zijn in de functievector verwijderd terwijl ze computerverwerking verspillen. Vervolgens worden tokens van twee tekens (twee gram) uit de eigenschapvectoren geëxtraheerd. In dit voorbeeld wordt ervan uitgegaan dat ze elkaar overlappen.

>[!NOTE]
>
>Ter illustratie worden de verwerkte kolommen toegevoegd naast de eigenschapvector voor elk van de stappen.

De volgende secties illustreren de vereiste gegevenstransformaties zoals deduplicatie, verwijdering van witruimte en omzetting in kleine letters voordat het proces van tokenisatie wordt gestart.

### Deduplicatie {#deduplication}

Gebruik vervolgens de component `DISTINCT` om duplicaten te verwijderen. Er zijn geen duplicaten in dit voorbeeld, maar het is een belangrijke stap om de nauwkeurigheid van om het even welke vergelijking te verbeteren. De benodigde SQL wordt hieronder weergegeven:

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct FROM featurevector1
SELECT DISTINCT(ProductName) AS featurevector2_distinct FROM featurevector2
```

### Witruimte verwijderen {#whitespace-removal}

In de volgende SQL-instructie worden de witruimten verwijderd uit de eigenschapvectoren. Het `replace(ProductName, ' ', '') AS featurevector1_nospaces` -gedeelte van de query neemt de `ProductName` -kolom van de `featurevector1` -tabel en gebruikt de `replace()` -functie. De functie `REPLACE` vervangt alle instanties van een spatie (&#39; &#39;) door een lege tekenreeks (&#39;&#39;). Hierdoor worden alle spaties verwijderd van de `ProductName` -waarden. Het resultaat krijgt de aliasing `featurevector1_nospaces` .

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, replace(ProductName, ' ', '') AS featurevector1_nospaces FROM featurevector1
```

De resultaten zijn weergegeven in onderstaande tabel:

|   | featurevector1_different | featurevector1_nospaces |
|---|---|---|
| 1 | iPad Mini | iPadMini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

De SQL-instructie en de resultaten ervan op de tweede functievector zijn hieronder te zien:

+++Selecteren om uit te breiden

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, replace(ProductName, ' ', '') AS featurevector2_nospaces FROM featurevector2
```

De resultaten zijn als volgt:

|   | featurevector2_different | featurevector2_nospaces |
|---|---|---|
| 1 | iPad | iPad |
| 2 | Macbook Pro | MacbookPro |
| 3 | iPhone | iPhone |

{style="table-layout:auto"}

+++

### Omzetten in kleine letters {#lowercase-conversion}

Vervolgens is de SQL verbeterd en zijn de productnamen omgezet in kleine letters en worden de spaties verwijderd. De onderste functie (`lower(...)`) wordt toegepast op het resultaat van de functie `replace()` . Met de onderste functie worden alle tekens in de gewijzigde `ProductName` -waarden omgezet in kleine letters. Dit zorgt ervoor dat de waarden in kleine letters zijn, ongeacht het originele geval.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform FROM featurevector1;
```

Het resultaat van deze verklaring is:

|   | featurevector1_different | featurevector1_transform |
|---|---|---|
| 1 | iPad Mini | ipadmini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

De SQL-instructie en de resultaten ervan op de tweede functievector zijn hieronder te zien:

+++Selecteren om uit te breiden

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, lower(replace(ProductName, ' ', '')) AS featurevector2_transform FROM featurevector2
```

De resultaten zijn als volgt:

|   | featurevector2_different | featurevector2_transform |
|---|---|---|
| 1 | iPad | ipad |
| 2 | Macbook Pro | macbookpro |
| 3 | iPhone | iphone |

{style="table-layout:auto"}

+++

### Tokens extraheren met SQL {#tokenization}

De volgende stap is tokenization, of text splitting. Vergelijking is het proces waarbij tekst in afzonderlijke termen wordt opgedeeld. Doorgaans gaat het om het splitsen van zinnen in woorden. In dit voorbeeld worden tekenreeksen opgesplitst in twee grammen (en in hogere volgorde n-grammen) door tokens te extraheren met SQL-functies zoals `regexp_extract_all` . Voor een effectieve kenisering moeten overlappende bigrammen worden gegenereerd.

Het gebruik van `regexp_extract_all` is verder verbeterd voor de SQL-versie. `regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0) AS tokens:` In dit gedeelte van de query worden de gewijzigde `ProductName` -waarden verwerkt die in de vorige stap zijn gemaakt. De functie `regexp_extract_all()` wordt gebruikt om alle niet-overlappende subtekenreeksen van een tot twee tekens te extraheren uit de gewijzigde waarden en de waarden in kleine letters `ProductName` . Het reguliere-expressiepatroon van `.{2}` komt overeen met subtekenreeksen van twee tekens lang. Het `regexp_extract_all(..., '.{2}', 0)` -gedeelte van de functie extraheert vervolgens alle overeenkomende subtekenreeksen uit de invoertekst.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
regexp_extract_all(lower(replace(ProductName, ' ', '')) , '.{2}', 0) AS tokens
FROM featurevector1;
```

De resultaten zijn weergegeven in onderstaande tabel:

+++Selecteren om uit te breiden

|   | featurevector1_different | featurevector1_transform | tokens |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;,&quot;ad&quot;,&quot;mi&quot;,&quot;ni&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;,&quot;ad&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;,&quot;at&quot;, &quot;ch&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;,&quot;ho&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Om de nauwkeurigheid verder te verbeteren, moet SQL worden gebruikt om overlappende tokens tot stand te brengen. In de bovenstaande tekenreeks &quot;iPad&quot; ontbreekt bijvoorbeeld het token &quot;pa&quot;. U kunt dit corrigeren door de lookahead-operator (met `substring` ) één stap te verschuiven en de twee-grammen te genereren.

Net als in de vorige stap extraheert `regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0):` tweetakenreeksen uit de gewijzigde productnaam, maar begint het tweede teken met de methode `substring` om overlappende tokens te maken. Vervolgens combineert de functie `array_union()` in regels 3-7 (`array_union(...) AS tokens`) de arrays van reeksen van twee tekens die worden verkregen door de twee reguliere expressies. Dit zorgt ervoor dat het resultaat unieke tokens van zowel niet-overlappende als overlappende reeksen bevat.

```SQL {line-numbers="true"}
SELECT DISTINCT(ProductName) AS featurevector1_distinct, 
       lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
       array_union(
           regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0),
           regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0)
       ) AS tokens
FROM featurevector1;
```

De resultaten zijn weergegeven in onderstaande tabel:

+++Selecteren om uit te breiden

|   | featurevector1_different | featurevector1_transform | tokens |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;,&quot;ad&quot;,&quot;mi&quot;,&quot;ni&quot;,&quot;pa&quot;,&quot;dm&quot;,&quot;in&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;,&quot;ad&quot;,&quot;pa&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;,&quot;at&quot;,&quot;ch&quot;,&quot;wa&quot;,&quot;tc&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;,&quot;ho&quot;,&quot;ne&quot;,&quot;ph&quot;,&quot;on&quot;} |

{style="table-layout:auto"}

+++

Het gebruik van `substring` als oplossing voor het probleem heeft echter beperkingen. Als u tokens van de tekst zou maken die op tri-grammen (drie karakters) worden gebaseerd, zou het gebruik van twee `substrings` aan lookahead tweemaal vereisen om de vereiste verschuivingen te krijgen. Als u 10-gram wilt maken, hebt u negen `substring` -expressies nodig. Hierdoor zou de code bloat worden en onhoudbaar worden. Het gebruik van eenvoudige reguliere expressies is ongeschikt. Er is een nieuwe aanpak nodig.

### De lengte van de productnaam wijzigen {#length-adjustment}

De SQl kan met de opeenvolging en lengtefuncties worden verbeterd. In het volgende voorbeeld genereert `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3)` een reeks getallen van één tot de lengte van de gewijzigde productnaam min drie. Als de gewijzigde productnaam bijvoorbeeld &quot;ipadmini&quot; is met een tekenlengte van acht, worden getallen van één tot vijf (acht-drie) gegenereerd.

De onderstaande instructie extraheert unieke productnamen en verdeelt elke naam in reeksen tekens (tokens) met een lengte van vier tekens, exclusief spaties, en geeft deze als twee kolommen weer. Eén kolom toont de unieke productnamen en de andere kolom toont de gegenereerde tokens.

```SQL
SELECT
   DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 4)
  ) AS tokens
FROM
  featurevector1;
```

De resultaten zijn weergegeven in onderstaande tabel:

+++Selecteren om uit te breiden

|   | featurevector1_different | tokens |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipad&quot;,&quot;padm&quot;,&quot;admi&quot;,&quot;dmin&quot;,&quot;mini&quot;} |
| 2 | iPad | {&quot;ipad&quot;} |
| 3 | iWatch | {&quot;iwat&quot;,&quot;watc&quot;,&quot;atch&quot;} |
| 4 | iPhone | {&quot;ipho&quot;,&quot;phon&quot;,&quot;hone&quot;} |

{style="table-layout:auto"}

+++

### Instellen van tokenlengte {#ensure-set-token-length}

Er kunnen aanvullende voorwaarden aan de instructie worden toegevoegd om ervoor te zorgen dat de gegenereerde reeksen een specifieke lengte hebben. De volgende SQL-instructie breidt de logica voor het genereren van tokens uit door de functie `transform` complexer te maken. De instructie gebruikt de `filter` functie binnen `transform` om ervoor te zorgen dat de gegenereerde reeksen zes tekens lang zijn. Het behandelt de gevallen waar dat niet mogelijk is door ONGELDIGE waarden aan die posities toe te wijzen.

```SQL
SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 5),
      i -> i + 5 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 6)) = 6
               THEN substring(lower(replace(ProductName, ' ', '')), i, 6)
               ELSE NULL
          END
  ) AS tokens
FROM
  featurevector1;
```

De resultaten zijn weergegeven in onderstaande tabel:

+++Selecteren om uit te breiden

|   | featurevector1_different | tokens |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipadmi&quot;,&quot;padmin&quot;,&quot;admini&quot;} |
| 2 | iPad | {null} |
| 3 | iWatch | {&quot;iwatch&quot;} |
| 4 | iPhone | {&quot;iphone&quot;} |

{style="table-layout:auto"}

+++

## Oplossingen ontdekken met Data Distiller-functies voor hogere volgorde {#higher-order-function-solutions}

Hogere-ordefuncties zijn krachtige constructies waarmee u &#39;programmeren&#39; kunt implementeren, zoals syntaxis in Data Distiller. Ze kunnen worden gebruikt om een functie te herhalen over meerdere waarden in een array.

In de context van Data Distiller zijn functies met een hogere volgorde ideaal voor het maken van n-grammen en het herhalen van reeksen tekens.

De functie `reduce` , met name wanneer deze wordt gebruikt binnen reeksen die door `transform` worden gegenereerd, biedt een manier om cumulatieve waarden of aggregaten af te leiden, die van cruciaal belang kunnen zijn in verschillende analyse- en planningsprocessen.

In de onderstaande SQl-instructie aggregeert de functie `reduce()` bijvoorbeeld elementen in een array met behulp van een aangepaste aggregator. Het simuleert a voor lijn aan **creeert de cumulatieve sommen van alle gehelen** van één tot vijf. `1, 1+2, 1+2+3, 1+2+3+4, 1+2+3+4` .

```SQL {line-numbers="true"}
SELECT transform(
    sequence(1, 5), 
    x -> reduce(
        sequence(1, x),  
        0,  -- Initial accumulator value
        (acc, y) -> acc + y  -- Higher-order function to add numbers
    )
) AS sum_result;
```

Hieronder volgt een analyse van de SQL-instructie:

- Regel 1: `transform` past de functie `x -> reduce` toe op elk element dat in de reeks wordt gegenereerd.
- Regel 2: `sequence(1, 5)` genereert een reeks getallen van 1 tot en met 5.
- Regel 3: `x -> reduce(sequence(1, x), 0, (acc, y) -> acc + y)` voert een verminderingsverrichting voor elk element x in de opeenvolging (van 1 tot 5) uit.
   - De functie `reduce` gebruikt een initiële accumulatorwaarde van 0, een opeenvolging van één aan de huidige waarde van `x`, en een hoger-ordefunctie `(acc, y) -> acc + y` om de aantallen toe te voegen.
   - De functie met een hogere volgorde `acc + y` accumuleert de som door de huidige waarde `y` toe te voegen aan de accu `acc` .
- Regel 8: `AS sum_result` wijzigt de naam van de resulterende kolom in sum_result.

Samenvattend, neemt deze hoger-ordefunctie twee parameters (`acc` en `y`) en bepaalt de uit te voeren verrichting, die in dit geval `y` aan de accumulator `acc` toevoegt. Deze functie van hogere orde wordt uitgevoerd voor elk element in de opeenvolging tijdens het verminderingsproces.

De output van deze verklaring is één enkele kolom (`sum_result`) die de cumulatieve bedragen van aantallen van één tot vijf bevat.

### De waarde van functies met een hogere volgorde {#value-of-higher-order-functions}

Deze sectie analyseert een afgeslankte versie van een tri-gram SQL verklaring om de waarde van hoger-ordefuncties in Gegevens Distiller beter te begrijpen om n-grammen efficiënter tot stand te brengen.

De onderstaande instructie werkt op de kolom `ProductName` in de tabel `featurevector1` . Hiermee wordt een set subtekenreeksen van drie tekens gemaakt die zijn afgeleid van de gewijzigde productnamen in de tabel, waarbij posities worden gebruikt die zijn verkregen uit de gegenereerde reeks.

```SQL {line-numbers="true"}
SELECT
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 3)
  ) 
FROM
  featurevector1
```

Hieronder volgt een analyse van de SQL-instructie:

- Regel 2: `transform` past een hoger-ordefunctie op elk geheel in de opeenvolging toe.
- Regel 3: `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2)` produceert een opeenvolging van gehelen van `1` aan de lengte van de gewijzigde productnaam minus twee.
   - `length(lower(replace(ProductName, ' ', '')))` berekent de lengte van de `ProductName` nadat deze in kleine letters is gemaakt en spaties zijn verwijderd.
   - `- 2` trekt twee van de lengte af om ervoor te zorgen dat de opeenvolging geldige beginnende posities voor 3 karaktersubstrings produceert. Als u 2 aftrekt, beschikt u na elke startpositie over voldoende tekens om een subtekenreeks van 3 tekens te extraheren. De substring functie hier werkt als een lookahead operator.
- Regel 4: `i -> substring(lower(replace(ProductName, ' ', '')), i, 3)` is een hoger-ordefunctie die op elk geheel `i` in de geproduceerde opeenvolging werkt.
   - De functie `substring(...)` extraheert een subtekenreeks van 3 tekens uit de kolom `ProductName` .
   - Voordat de subtekenreeks wordt geëxtraheerd, zet `lower(replace(ProductName, ' ', ''))` de `ProductName` om in kleine letters en worden spaties verwijderd om de consistentie te garanderen.

De uitvoer bestaat uit een lijst subtekenreeksen van drie tekens lang, die worden geëxtraheerd uit de gewijzigde productnamen, op basis van de posities die in de reeks zijn opgegeven.

## De resultaten filteren {#filter-results}

De `filter` functie, met verdere [ gegevenstransformaties ](#data-transformation), staat voor een meer verfijnde en nauwkeurige extractie van relevante informatie van tekstgegevens toe. Hierdoor kunt u inzichten afleiden, de gegevenskwaliteit verbeteren en betere besluitvormingsprocessen vergemakkelijken.

De functie `filter` in de volgende SQL-instructie dient om de volgorde van posities binnen de tekenreeks waaruit subtekenreeksen worden geëxtraheerd, te verfijnen en te beperken met behulp van de daaropvolgende transformatiefunctie.

```SQL
SELECT
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 6),
      i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 7)) = 7
               THEN substring(lower(replace(ProductName, ' ', '')), i, 7)
               ELSE NULL
          END
  )
FROM
  featurevector1;
```

De functie `filter` genereert een reeks geldige startposities binnen de gewijzigde `ProductName` en extraheert subtekenreeksen van een specifieke lengte. Alleen beginposities die het extraheren van een subtekenreeks van zeven tekens mogelijk maken, zijn toegestaan.

De voorwaarde `i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))` zorgt ervoor dat de startpositie `i` plus `6` (de lengte van de gewenste subtekenreeks van zeven tekens min één) de lengte van de gewijzigde `ProductName` niet overschrijdt.

De instructie `CASE` wordt gebruikt om subtekenreeksen op basis van hun lengte voorwaardelijk op te nemen of uit te sluiten. Alleen subtekenreeksen van zeven tekens worden opgenomen; andere worden vervangen door NULL. Deze subtekenreeksen worden vervolgens door de functie `transform` gebruikt om een reeks subtekenreeksen te maken van de kolom `ProductName` in de tabel `featurevector1` .

>[!TIP]
>
>U kunt de [ bepaalde van parameters voorzien malplaatjes ](../ui/parameterized-queries.md) eigenschap gebruiken om logica binnen uw vragen opnieuw te gebruiken en te onttrekken. Wanneer u bijvoorbeeld hulpprogrammafuncties voor algemene doeleinden maakt (zoals de hierboven weergegeven functie voor het tokeniseren van tekenreeksen), kunt u met Data Distiller geparameteriiseerde sjablonen gebruiken waarbij het aantal tekens een parameter zou zijn.

## De cross-join van unieke elementen berekenen met twee functievectoren {#cross-join-unique-elements}

Het opsporen van verschillen of discrepanties tussen de twee datasets op basis van een specifieke transformatie van de gegevens is een gemeenschappelijk proces om de gegevensnauwkeurigheid te behouden, de gegevenskwaliteit te verbeteren en consistentie tussen de gegevensreeksen te waarborgen.

Deze SQL-instructie hieronder extraheert de unieke productnamen die aanwezig zijn in `featurevector2` maar niet in `featurevector1` nadat de transformaties zijn toegepast.

```SQL
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector2
EXCEPT
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector1;
```

>[!TIP]
>
>Naast `EXCEPT` kunt u ook `UNION` en `INTERSECT` gebruiken, afhankelijk van het gebruik. U kunt ook experimenteren met `ALL` - of `DISTINCT` -componenten om het verschil te zien tussen het opnemen van alle waarden en het retourneren van alleen de unieke waarden voor de opgegeven kolommen.

De resultaten zijn weergegeven in onderstaande tabel:

+++Selecteren om uit te breiden

|   | lower(ProductName, &#39;, &#39;&#39;)) |
|---|---------------------------------------|
| 1 | macbookpro |

{style="table-layout:auto"}

+++

Vervolgens voert u een cross-join uit om elementen van de twee eigenschapvectoren te combineren en paren elementen te maken die kunnen worden vergeleken. De eerste stap in dit proces is het maken van een verdeelde vector.

Een gescheiden vector is een gestructureerde weergave van tekstgegevens waarbij elk woord, elke woordgroep of elke betekeniseenheid (token) wordt omgezet in een numerieke indeling. Met deze conversie kunnen algoritmen voor de verwerking van natuurlijke talen tekstinformatie begrijpen en analyseren.

Met de onderstaande SQl maakt u een verdeelde vector.

```SQL
CREATE TABLE featurevector1tokenized AS SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
  (SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector1);
SELECT * FROM featurevector1tokenized;
```

>[!NOTE]
>
>Als u [!DNL DbVisualizer] gebruikt, vernieuwt u, nadat u een tabel hebt gemaakt of verwijderd, de databaseverbinding zodat de metagegevenscache van de tabel wordt vernieuwd. Data Distiller biedt geen updates van metagegevens.

De resultaten zijn weergegeven in onderstaande tabel:

+++Selecteren om uit te breiden

|   | featurevector1_different | tokens |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} |
| 2 | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 3 | iwatch | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} |
| 4 | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Herhaal vervolgens het proces voor `featurevector2` :

```SQL
CREATE TABLE featurevector2tokenized AS 
SELECT
  DISTINCT(ProductName) AS featurevector2_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
(SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector2
);
SELECT * FROM featurevector2tokenized;
```

De resultaten zijn weergegeven in onderstaande tabel:

+++Selecteren om uit te breiden

|   | featurevector2_different | tokens |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 2 | macbookpro | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 3 | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Als beide samengevoegde vectoren zijn voltooid, kunt u nu de kruissamenvoeging maken. Dit is te zien in de onderstaande SQL:

```SQL {line-numbers="true"}
SELECT
    A.featurevector1_distinct AS SetA_ProductNames,
    B.featurevector2_distinct AS SetB_ProductNames,
    A.tokens AS SetA_tokens1,
    B.tokens AS SetB_tokens2
FROM
    featurevector1tokenized A
CROSS JOIN
    featurevector2tokenized B;
```

Hier volgt een overzicht van de SQl die is gebruikt om de cross join te maken:

- Regel 2: `A.featurevector1_distinct AS SetA_ProductNames` selecteert de `featurevector1_distinct` kolom in de tabel `A` en wijst er een alias aan toe `SetA_ProductNames` . Deze sectie van SQL resulteert in een lijst van verschillende productnamen van de eerste dataset.
- Regel 4: `A.tokens AS SetA_tokens1` selecteert de `tokens` kolom in de tabel of subquery `A` en wijst er een alias aan toe `SetA_tokens1` . Deze sectie van SQL resulteert in een lijst van verdeelde waarden verbonden aan de productnamen van de eerste dataset.
- Regel 8: De `CROSS JOIN` verrichting combineert alle mogelijke combinaties rijen van de twee datasets. Met andere woorden, paren het elk productnaam en zijn bijbehorende tokens van de eerste lijst (`A`) met elke productnaam en zijn bijbehorende tokens van de tweede lijst (`B`). Dit resulteert in een Cartesisch product van de twee datasets, waar elke rij in de output een combinatie van een productnaam en zijn bijbehorende tokens van beide datasets vertegenwoordigt.

De resultaten zijn weergegeven in onderstaande tabel:

+++Selecteren om uit te breiden

| * | SetA_ProductNames | SetB_ProductName | _tokens 1 instellen | _Tokens 2 instellen |
|---|---------------------|-------------------|---|---|
| 1 | ipadmini | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 3 | ipadmini | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 4 | ipad | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 5 | ipad | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 6 | ipad | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 7 | iwatch | ipad | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 8 | iwatch | macbookpro | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 9 | iwatch | iphone | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 10 | iphone | ipad | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 11 | iphone | macbookpro | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 12 | iphone | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

## De vergelijkbare Jaccard-maatregel berekenen {#compute-the-jaccard-similarity-measure}

Vervolgens berekent u de vergelijkingscoëfficiënt Jaccard om een gelijkenisanalyse tussen de twee sets productnamen uit te voeren door de aangepaste representaties te vergelijken. De uitvoer van het SQL-script hieronder biedt de volgende mogelijkheden: productnamen van beide sets, hun verdeelde representaties, tellingen van algemene en totale unieke tokens en de berekende Jaccard-vergelijkingscoëfficiënt voor elk paar datasets.


```SQL {line-numbers="true"}
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) /    size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    );
```

Hieronder volgt een overzicht van de SQL die wordt gebruikt om de Jaccard-coëfficiënt voor gelijkenis te berekenen:

- Regel 6: `size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count` berekent het aantal tokens dat zowel voor `SetA_tokens1` als `SetB_tokens2` wordt gebruikt. Deze berekening wordt bereikt door de grootte van de doorsnede van de twee series van tokens te berekenen.
- Regel 7: `size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count` berekent het totale aantal unieke tokens voor zowel `SetA_tokens1` als `SetB_tokens2` . Deze regel berekent de grootte van de samenvoeging van de twee arrays tokens.
- Lijn 8-10: `ROUND(CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity` berekent de gelijkenis van het Jacard tussen de tokenreeksen. Deze regels verdelen de grootte van de tokendoorsnede door de grootte van de tokenvereniging en ronden het resultaat in twee decimale posities. Het resultaat is een waarde tussen nul en één, waarbij een volledige gelijkenis aangeeft.

De resultaten zijn weergegeven in onderstaande tabel:

+++Selecteren om uit te breiden

| * | SetA_ProductNames | SetB_ProductName | _tokens 1 instellen | _Tokens 2 instellen | token_intersect_count | token_intersect_count | Jaccard-gelijkenis |
|---|---------------------|-------------------|---------------------------------------|-------------------------------------------------|----|----|----|
| 1 | ipadmini | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 3 | 7 | 0,43 |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 16 | 0,0 |
| 3 | ipadmini | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 1 | 11 | 0,09 |
| 4 | ipad | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 3 | 3 | 1,0 |
| 5 | ipad | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 12 | 0,0 |
| 6 | ipad | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 1 | 7 | 0,14 |
| 7 | iwatch | ipad | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 0 | 8 | 0,0 |
| 8 | iwatch | macbookpro | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 14 | 0,0 |
| 9 | iwatch | iphone | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 0 | 10 | 0,0 |
| 10 | iphone | ipad | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 1 | 7 | 0,14 |
| 11 | iphone | macbookpro | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 14 | 0,0 |
| 12 | iphone | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 5 | 5 | 1,0 |

{style="table-layout:auto"}

+++

## Filterresultaten op basis van Jaccard-simulatiedrempel {#similarity-threshold-filter}

Ten slotte filtert u de resultaten op basis van een vooraf gedefinieerde drempel om alleen die paren te selecteren die aan de criteria voor gelijkenis voldoen. De SQL-instructie hieronder filtert de producten met een Jaccard-equivalentiecoëfficiënt van ten minste 0,4. Hierdoor worden de resultaten tot paren beperkt die een aanzienlijke mate van gelijkenis vertonen.

```SQL
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames
FROM 
(SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)),
        2
    ) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    )
)
WHERE jaccard_similarity>=0.4
```

De resultaten van deze vraag geven de kolommen voor gelijkenis zich bij, zoals hieronder wordt gezien:

+++Selecteren om uit te breiden

|   | SetA_ProductNames | SetA_ProductNames |
|---|--------------------------|------------------------|
| 1 | ipadmini | ipad |
| 2 | ipad | ipad |
| 3 | iphone | iphone |

{style="table-layout:auto"}

+++:

### Volgende stappen {#next-steps}

Door dit document te lezen, kunt u deze logica nu gebruiken om betekenisvolle relaties of overlappingen tussen verschillende gegevenssets te benadrukken. De capaciteit om producten van verschillende datasets te identificeren die een significante gelijkenis in hun eigenschappen of eigenschappen hebben heeft talrijke real-world toepassingen. Deze logica kan worden gebruikt voor scenario&#39;s zoals:

- Productovereenkomst: vergelijkbare producten groeperen of aanbevelen aan klanten.
- Gegevensreiniging: verbeteren van de gegevenskwaliteit.
- Marktmand-analyse: inzicht verschaffen in het gedrag van klanten, voorkeuren en potentiële mogelijkheden voor cross-selling.

Als u dit nog niet hebt gedaan, wordt u geadviseerd om het [ AI/ML overzicht van de eigenschappijpleiding ](../data-distiller/ml-feature-pipelines/overview.md) te lezen. Met dit overzicht leert u hoe Data Distiller en het leren van uw voorkeurscomputer aangepaste gegevensmodellen kunnen maken die uw gebruiksscenario&#39;s voor marketingdoeleinden ondersteunen met behulp van Experience Platforms.
