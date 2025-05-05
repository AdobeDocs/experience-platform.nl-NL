---
title: Vraag voor AI-assistent
description: Lees dit document om voorbeeldvragen te leren die u kunt gebruiken wanneer het vragen van AI Medewerker.
exl-id: d16d1262-cc2d-45c9-94c4-b86132183442
source-git-commit: 7268895d0b1924f9d3e7cee24e549c79245ef099
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 1%

---

# Vraag voor AI-assistent

Lees dit document voor een set voorbeeldvragen die u kunt gebruiken bij het opvragen van AI Assistant.

U kunt dit document ook gebruiken om uiteinden op [ te leren hoe te om uw vragen ](#phrasing-your-questions) te formuleren om optimale reacties van AI Medewerker te krijgen.

## Op doelstellingen gebaseerde vragen {#objectives-questions}

De volgende voorbeeldvragen worden gegroepeerd op doelstellingen die u kunt verwezenlijken wanneer het gebruiken van AI Medewerker:

| Doelstelling | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Leerconcepten en doorlopende workflows | <ul><li>Als beginnende gebruiker, kunt u AI Medewerker gebruiken om de concepten van Real-Time CDP en van Adobe Journey Optimizer te leren en aan boord aan producten en eigenschappen te zijn die u niet vertrouwd met bent.</li><li>Als ervaren gebruiker, kunt u AI Medewerker gebruiken om een randgeval op te lossen dat uw werkschema kan blokkeren. | <ul><li>Hoe kan ik een dashboard instellen in Journey Analytics?</li><li>Vertel me wat gebruiksgevallen voor Real-Time CDP.</li></ul> |
| Problemen oplossen | Met AI Assistant leert u hoe u fouten in de basisbeginselen die u in uw workflow tegenkomt, kunt opsporen. | <ul><li>Wat betekent deze fout {ERROR_MESSAGE}?</li><li>Waarom kan ik het publiek met de naam &quot;Luma: Email Audience&quot; niet verwijderen?</li></ul> |
| Zandbakhygiëne | Met AI Assistant kunt u eventuele duplicaten of ongebruikte objecten identificeren, zodat u de sandbox op efficiënte wijze kunt onderhouden. | <ul><li>Kan je me een publiek laten zien dat vergelijkbaar is?</li><li>Zijn er regelingen die geen bijbehorende dataset hebben?</li></ul> |
| Waardeanalyse | Met AI Assistant kunt u de meest gebruikte gegevensobjecten identificeren en prestatie-indicatoren beoordelen of de meest waardevolle gegevensobjecten vinden. | <ul><li>Hoeveel profielen bevinden zich in de segmentdefinitie &quot;Luma: Email Audience&quot;?</li><li>Wanneer werd het publiek geactiveerd aan de bestemming van het publiek van het Experience Cloud?</li></ul> |
| Zoeken | De Medewerker van AI van het gebruik om gesteunde voorwerpen van het Experience Platform zoals publiek, datasets, bestemmingen, schema&#39;s, en bronnen te vinden. | <ul><li>Maak een lijst van de soorten publiek die &quot;Luma&quot;in de naam bevatten die in het laatste kwartaal werden gecreeerd.</li><li>Welke kenmerken bevinden zich in het XDM-schema &quot;Luma: Custom Actions&quot;?</li></ul> |
| Effectanalyse | Met AI Assistant kunt u gegevensobjecten identificeren die in bepaalde workflows zijn gebruikt, zodat u het effect van wijzigingen kunt beoordelen. | <ul><li>Welk publiek gebruikt `homeAddress.city` in het schema &quot;Luma: PersonProfiles&quot;?</li><li>In welke gegevenssets wordt het profielkenmerk `consents.marketing.push.val` opgeslagen?</li></ul> |

{style="table-layout:auto"}

## Operationele inzichten per entiteit en productkennisvragen{#objects-questions}

De volgende vragen worden gegroepeerd door gegevensvoorwerpen en als of [ operationele inzichten ](./home.md#operational-insights) of [ productkennis ](./home.md#product-knowledge) geclassificeerd.

![](./images/prompt.png)

* **Soorten publiek - Operationele inzichten**
   * Welk publiek gebruikt ander publiek?
   * Wat is de verdeling van het aantal profielen over het publiek?
   * Toon mij publiek dat voor het laatst is gewijzigd vóór {RELATIVE_DATE} .
   * Welk publiek heeft 0 profielen?
   * Wordt {USE_AUTO_COMPLETE_TO_FILL_AUDIENCE_NAME} gebruikt bij andere doelgroepen?
* **Attributen - Operationele inzichten**
   * Welk publiek heeft xdm attribuut {ATTRIBUTE_PATH} in hun segmentdefinitie?
   * Hoeveel XDM schemakenmerken worden niet gebruikt in om het even welk publiek?
   * Welke schema&#39;s hebben xdm attribuut {ATTRIBUTE_PATH} in hen?
   * Welke attributen XDM worden geactiveerd?
   * Welke attributen XDM worden gebruikt in publiek met meer dan 10 profielen?
* **Dataflows - Operationele inzichten**
   * Welke gegevensstromen dragen bij aan {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} dataset?
   * Welke brongegevens worden niet gebruikt of hebben geen gegevens die binnen komen?
   * Maak een lijst van de brongegevensstromen die ik heb.
   * Welke dataflows worden gevormd voor elke bronschakelaar?
* **Datasets - Operationele inzichten**
   * Hoeveel datasets zijn opgenomen gebruikend het zelfde schema?
   * Welke bronschakelaar wordt geassocieerd met {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} dataset?
   * Welke datasets worden gebruikt in elk publiek?
   * Welke schema&#39;s worden niet gebruikt in om het even welke datasets?
   * Hoeveel datasets heb ik?
* **Doelen - Operationele inzichten**
   * Welke bestemmingen zijn actief?
   * Welke bestemmingsrekeningen hebben 0 publiek geactiveerd?
   * Hoeveel publiek wordt geactiveerd voor elke bestemming?
   * Welke bestemmingen hebben het hoogste aantal geactiveerde doelgroepen?
* **Reizen - Operationele inzichten**
   * Hoeveel reizen heb ik?
   * Welke reizen zijn gemaakt in {RELATIVE_DATE} (bijvoorbeeld de laatste week) of {RELATIVE_DATE} (bijvoorbeeld voor/na/op een bepaalde datum)?
   * Geef me de lijst met reizen weer die zijn gewijzigd in {RELATIVE_DATE} (bijvoorbeeld de laatste week) of {RELATIVE_DATE} (bijvoorbeeld voor/na/op een bepaalde datum)?
   * Maak een lijst van de levende reizen die ik heb.
   * Geef een overzicht van de doelgroepen die worden gebruikt voor live journeys.
* **Bronnen - Operationele inzichten**
   * Welke bronnen zijn actief?
   * Welke bronschakelaar wordt geassocieerd met dataset {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}.
   * Welke bronschakelaar heeft het hoogste aantal bijbehorende rekeningen?
   * Toon me de gegevensstromen en hun bijbehorende bronschakelaars.
* **Aangewezen het leren - de kennis van het Product (Real-Time CDP en Journey Optimizer)**
   * Wat zijn lookalike doelgroepen?
   * Hoe zijn Gebruikersgroepen verwant aan Rollen?
   * Wanneer moet ik een gegevenstype versus een veldgroep gebruiken?
   * Wat is het verschil tussen een identiteit en een primaire of buitenlandse sleutel?
* **het Oplossen van problemen - de kennis van het Product (Real-Time CDP en Journey Optimizer)**
   * Waarmee kan AI Assistant helpen?
   * Kan ik een schema verwijderen dat voor een profiel is ingeschakeld nadat gegevens zijn opgenomen?
   * Waarom kan ik geen publiek verwijderen?
   * Hoe lang duurt het voordat het publiek wordt geëvalueerd en de resultaten beschikbaar zijn om doelgericht te zijn?

## Uw vragen formuleren {#phrasing-your-questions}

U moet uw vragen duidelijk en in de context tot AI Assistant richten om zo accuraat mogelijk te kunnen antwoorden. Raadpleeg de volgende tips voor het stellen van een duidelijke vraag met betrekking tot de context:

* Geef uw taak en/of vraag beknopt weer.
* Vermijd dubbelzinnige taal of te complexe syntaxis om het begrip te vergemakkelijken.
* Een relevante context bieden met betrekking tot uw taak en/of vraag als context kan AI Assistant helpen meer relevante reacties te genereren.

Lees de onderstaande tabellen voor meer informatie over aanbevolen procedures bij het stellen van vragen aan AI Assistant.

In de volgende tabellen worden de aanbevolen werkwijzen beschreven die u kunt volgen bij het gebruik van AI Assistant:

| Do | Voorbeeld |
| --- | --- |
| <ul><li>Wees specifiek voor het object of de informatie die u wilt ophalen of analyseren.</li><li>Plaats uw gegevensobjectnamen tussen aanhalingstekens. Als u slechts een deel van de objecten naam kent, kunt u dat ook specificeren in de vraag.</li><li>Het voorwerp van het gebruik [&#128279;](./ui-guide.md#use-auto-complete) auto-complete  om AI Medewerker te helpen beter de context van uw vraag begrijpen.</li></ul> | <ul><li>Welke datasets gebruiken het &quot;Luma - Loyalty&quot;schema?</li><li>Toon me de geactiveerde segmenten die &quot;Luma&quot;in hun naam hebben. Rang ze op het aantal profielen.</li></ul> |
| <ul><li>Vermijd dubbelzinnigheid en gebruik duidelijke taal</li><li>Gebruik nauwkeurige terminologie om betere duidelijkheid in uw vraag te verzekeren.</li><li>Wanneer u vragen stelt over Adobe Experience Platform, probeert u specifieke terminologie voor Experience Platform te gebruiken om de relevantie van antwoorden te verbeteren.</li></ul> | <ul><li>Hoeveel profielen heb ik in &quot;ACME Audience&quot;.</li><li>Toon me de hoogste 5 attributen XDM die in geactiveerd publiek worden gebruikt.</li></ul> |
| <ul><li>Geef context op of geef criteria op om de resultaten te filteren.</li><li>Gebruik filtercriteria in de vragen om het volume van gegevens in de reactie te beperken.</li></ul> | <ul><li>Toon me publiek dat niet geactiveerd is en meer dan zes maanden geleden is gecreëerd en nooit gewijzigd is.</li><li>Toon me publiek geactiveerd aan &quot;Doel ACME&quot;en heeft meer dan 10000 profielen.</li></ul> |

{style="table-layout:auto"}

| Niet doen | Voorbeeld |
| --- | --- |
| Gebruik een vage of dubbelzinnige taal. | <ul><li>Geef me informatie over datasets.</li><li>Hoeveel gebruikers heb ik in &quot;ACME Audience&quot;?</li><li>Segmenten tonen.</li><li>Lijstkenmerken.</li></ul> |
| Voer onvolledige verzoeken in. | &quot;Luma - Loyalty Dataset&quot; |
| Kennis aannemen zonder context. | <ul><li>Soorten publiek in de laatste zes maanden.</li><li>Bouw een vraag voor me.</li></ul> |
| U kunt te complexe query&#39;s opmaken. | Verstrek een uitvoerige analyse van gegevenslijn over alle voorwerpen en hun gebiedsdelen. |
| Criteria of parameters weglaten. | Toon me gegevenssets. |

{style="table-layout:auto"}

## Waarneming gegevensset {#dataset-observability}

De Medewerker van AI kan vragen over specifieke datasetmetriek zoals opslaggrootte en rijtelling nu beantwoorden.

* Wat zijn mijn grootste datasets door grootte?
* Wat zijn mijn grootste dataset door rijen?
* Hoeveel datasets zijn leeg?
* Welke datasets zijn leeg?

Bovendien kunt u een vergelijkbare intentie overbrengen door een aantal verschillende variaties aan te brengen op de vier bovenstaande vragen.

+++Selecteer om geaccepteerde variaties van de vragen van de datasetwaarneming te bekijken

* Wat zijn de hoogste vijf datasets door grootte?
* Welke dataset heeft het grootste aantal rijen?
* Hoeveel datasets hebben geen gegevens in hen?
* Geef de datasets weer met grootte > 10 MB?
* Maak een lijst van de datasets met rijen minder dan 10.
* Kun je me de gegevenssets laten zien die volledig leeg zijn?
* Welke dataset is grootste door opslaggrootte?
* Wat is de kleinste dataset in termen van rijtelling?
* Hoeveel van mijn datasets hebben gegevens en hoeveel leeg zijn?
* Wat is het rijaantal voor dataset genoemd {DATASET_NAME}?
* Hoe vergelijk de grootte van {DATASET_NAME} met mijn andere datasets?
* Wat is de grootte van {DATASET_NAME}?
* Hoeveel rijen heeft {DATASET_NAME}?
* Wat is de grootte en het aantal rijen van {DATASET_NAME}?
* Kunt u de grootste en kleinste datasets door opslaggrootte opsommen?

+++

U kunt uw vragen van de gegevenswaarneembaarheid met een kwalificatie ook verfijnen om uw vraag door een bepaalde tijdspanne te filtreren:

* Datasets die batches ontvangen in de afgelopen (x) dagen
* Datasets die de afgelopen (x) dagen geen batches ontvangen
* Datasets met de meest gegevens die in de afgelopen (x) dagen zijn ingevoerd
* Aantal records voor een specifieke gegevensset in de laatste (x) dagen

+++Selecteer om geaccepteerde variaties van de vragen van de datasetwaarneming te bekijken

* Hoeveel datasets ontvingen partijen in de laatste (x) dagen?
* Welke datasets hebben partijen in de afgelopen (x) dagen ontvangen?
* Kunt u een lijst maken van de datasets die gegevens in de laatste (x) dagen werden opgenomen?
* Hoeveel datasets ontvingen nieuwe partijen in de vorige (x) dagen?
* Wat zijn de datasets die met nieuwe gegevens in de laatste (x) dagen werden bijgewerkt?
* Lijst datasets die partijactiviteit binnen de laatste (x) dagen hadden.
* Hoeveel datasets ontvingen geen partijen in de laatste (x) dagen?
* Welke datasets hebben geen partijen in de afgelopen (x) dagen ontvangen?
* Kunt u gegevenssets identificeren zonder gegevensinvoer in de laatste (x) dagen?
* Hoeveel datasets ontvingen geen updates in de laatste (x) dagen?
* Welke datasets zijn de afgelopen (x) dagen inactief geweest?
* De datasets van de lijst die geen nieuwe partijen in de laatste (x) dagen kregen.
* Wanneer was de laatste tijd toen de gegevens op dataset (x) werden opgenomen?
* Wat zijn Top 10 datasets waarin de meeste gegevens in laatste (x) dagen werden opgenomen?
* Wat zijn de hoogste 10 datasets door gegevensvolume dat in de laatste (x) dagen wordt opgenomen?
* Welke 10 datasets hadden de grootste gegevensopname in de laatste (x) dagen?
* Toon de top 10 datasets met de hoogste gegevensopname in de vorige (x) dagen.
* Wat zijn de hoogste datasets door gegevens die in de laatste (x) dagen worden ontvangen?
* Maak een lijst van de hoogste 10 datasets die de meeste gegevens in de afgelopen (x) dagen opnamen.
* Hoeveel verslagen werden ontvangen in dataset (x), in de laatste (y) dagen?
* Hoeveel verslagen ontving dataset (x) in de laatste (y) dagen?
* Wat is het recordaantal dat voor dataset (x) in de afgelopen (y) dagen wordt opgenomen?
* Kan u het aantal verslagen verstrekken die aan dataset (x) in de laatste (y) dagen worden toegevoegd?
* Hoeveel gegevens werden ontvangen door dataset (x) in de laatste (y) dagen?
* Wat is het volume van verslagen die voor dataset (x) in de vorige (y) dagen worden opgenomen?

+++


## Voorbeelden van niet-ondersteunde vragen {#unsupported-questions}

Hieronder volgt een lijst met voorbeelden van vragen die momenteel niet worden ondersteund door AI Assistant.

+++Selecteren om voorbeelden weer te geven van niet-ondersteunde vragen

### Operationele inzichten

* Hoeveel profielen in deze zandbak leven in Californië? (**Nota**: voor gelijkaardige vragen, moet u een specifieke criteria verstrekken om genoeg context voor uw verzoek te geven, in dit geval, zijn de specifieke criteria &quot;levend in Californië&quot;).
* In welke segmenten bevindt dit profiel zich {PROFILE_INFO/ATTRIBUTE_VALUE}?
* Hoeveel profielen in de dataset hebben een e-mail?
* Welke dataset bestaat uit maximaal aantal profielen in deze sandbox?
* Welke dataset heeft het hoogste aantal verslagen?
* Hoeveel segmenten zijn verwijderd in {RELATIVE_DATE} ?
* Welke van mijn datasets heeft de grootste grootte?
* Geef me een profiel in {AUDIENCE_NAME}.
* Het totale aantal profielen in mijn sandbox
* Hoeveel naamruimten zijn gekoppeld aan het publiek {AUDIENCE_NAME}?
* Toon me een rapport van alle publiekssegmenten die vandaag werden geëvalueerd
* Hoeveel segmenten hebben overlappende profielen?
* Hoeveel batches worden geladen in {DATASET_NAME}
* Hoeveel actieve aanbiedingen heb ik?
* Hoeveel actieve campagnes heb ik?
* Waar komen mijn gegevensbronnen vandaan?
* Wat is de grootste dataset of gegevensbron?
* Kan ik de lijst krijgen van gebruikers die deze schema&#39;s hebben gecreeerd?

### Problemen oplossen

* Waarom wordt deze batch {BATCH_NAME/BATCH_ID} nog steeds verwerkt?
* Waarom komt niemand in aanmerking voor dit publiek {AUDIENCE_NAME} ?
* Ik kan de AI van de Klant niet zien, waarom en hoe los ik het op?
* Ik kan geen Dataset voorproef zien, waarom en hoe verbeter ik het?
* Waarom kan ik {SEGMENT/DATASET/SCHEMA_NAME} niet verwijderen?
* Heb ik toegang tot de Dienst van de Vraag?

### Taak en automatisering

* Schrijf een vraag die me één verslag van {DATASET_NAME} geeft.
* Schrijf een steekproefAPI vraag aan /schemas/{schemaId}/fields/{fieldPath}/values.
* Stel een bron/bestemming voor mij in.
* Maak een publiek voor mij met criteria {USER_SPECIFIC_CRITERIA} .

+++

## Volgende stappen

Door dit document te lezen, hebt u nu inzicht in hoe u uw vragen kunt optimaliseren voor AI Assistant. Voor informatie over hoe te om de eigenschap tijdens uw werkschema&#39;s te gebruiken, lees de [ AI Hulp UI gids ](ui-guide.md).
