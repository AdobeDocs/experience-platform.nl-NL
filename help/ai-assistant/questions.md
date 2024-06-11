---
title: Vraag voor AI-assistent
description: Lees dit document om voorbeeldvragen te leren die u kunt gebruiken wanneer het vragen van AI Medewerker.
exl-id: d16d1262-cc2d-45c9-94c4-b86132183442
source-git-commit: 26e27e7a62731fe43ef203741121b22226078b28
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# Vraag voor AI-assistent

Lees dit document voor een set voorbeeldvragen die u kunt gebruiken bij het opvragen van AI Assistant.

U kunt dit document ook gebruiken om tips te leren over [uw vragen formuleren](#phrasing-your-questions) voor optimale reacties van AI Assistant.

## Op doelstellingen gebaseerde vragen {#objectives-questions}

De volgende voorbeeldvragen worden gegroepeerd op doelstellingen die u kunt verwezenlijken wanneer het gebruiken van AI Medewerker:

| Doelstelling | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Leerconcepten en doorlopende workflows | <ul><li>Als beginnende gebruiker, kunt u AI Medewerker gebruiken om de concepten van Real-Time CDP en van Adobe Journey Optimizer te leren en aan boord aan producten en eigenschappen te zijn die u niet vertrouwd met bent.</li><li>Als ervaren gebruiker, kunt u AI Medewerker gebruiken om een randgeval op te lossen dat uw werkschema kan blokkeren. | <ul><li>Hoe kan ik een dashboard instellen in Journey Analytics?</li><li>Vertel me wat gebruiksgevallen voor Real-Time CDP.</li></ul> |
| Problemen oplossen | Met AI Assistant leert u hoe u fouten in de basisbeginselen die u in uw workflow tegenkomt, kunt opsporen. | <ul><li>Wat is deze fout? {ERROR_MESSAGE} bedoel?</li><li>Waarom kan ik het publiek met de naam &quot;Luma: Email Audience&quot; niet verwijderen?</li></ul> |
| Zandbakhygiëne | Met AI Assistant kunt u eventuele duplicaten of ongebruikte objecten identificeren, zodat u de sandbox op efficiënte wijze kunt onderhouden. | <ul><li>Kan je me een publiek laten zien dat vergelijkbaar is?</li><li>Zijn er regelingen die geen bijbehorende dataset hebben?</li></ul> |
| Waardeanalyse | Met AI Assistant kunt u de meest gebruikte gegevensobjecten identificeren en prestatie-indicatoren beoordelen of de meest waardevolle gegevensobjecten vinden. | <ul><li>Hoeveel profielen bevinden zich in de segmentdefinitie &quot;Luma: Email Audience&quot;?</li><li>Wanneer werd het publiek geactiveerd aan de bestemming van het publiek van het Experience Cloud?</li></ul> |
| Zoeken | De Medewerker van AI van het gebruik om gesteunde voorwerpen van het Experience Platform zoals publiek, datasets, bestemmingen, schema&#39;s, en bronnen te vinden. | <ul><li>Maak een lijst van de soorten publiek die &quot;Luma&quot;in de naam bevatten die in het laatste kwartaal werden gecreeerd.</li><li>Welke kenmerken bevinden zich in het XDM-schema &quot;Luma: Custom Actions&quot;?</li></ul> |
| Effectanalyse | Met AI Assistant kunt u gegevensobjecten identificeren die in bepaalde workflows zijn gebruikt, zodat u het effect van wijzigingen kunt beoordelen. | <ul><li>Welk publiek gebruikt `homeAddress.city` in het schema &quot;Luma: PersonProfiles&quot;?</li><li>Welke datasets zijn `consents.marketing.push.val` profielkenmerk opgeslagen in?</li></ul> |

{style="table-layout:auto"}

## Operationele inzichten per entiteit en productkennisvragen{#objects-questions}

De volgende vragen worden gegroepeerd op gegevensobjecten en worden als een van beide geclassificeerd [operationele inzichten](./home.md#operational-insights) of [productkennis](./home.md#product-knowledge).

* **Publiek - Operationele inzichten**
   * Welk publiek gebruikt ander publiek?
   * Wat is de verdeling van het aantal profielen over het publiek?
   * Toon me publiek dat het laatst werd gewijzigd eerder {RELATIVE_DATE}.
   * Welk publiek heeft 0 profielen?
   * Is {USE_AUTO_COMPLETE_TO_FILL_AUDIENCE_NAME} bij andere doelgroepen worden gebruikt?
* **Attributen - Operationele inzichten**
   * Welk publiek heeft xdm-kenmerk {ATTRIBUTE_PATH} in hun segmentdefinitie?
   * Hoeveel XDM schemakenmerken worden niet gebruikt in om het even welk publiek?
   * Welke schema&#39;s hebben xdm-kenmerk {ATTRIBUTE_PATH} in hen?
   * Welke attributen XDM worden geactiveerd?
   * Welke attributen XDM worden gebruikt in publiek met meer dan 10 profielen?
* **Gegevensstromen - Operationele inzichten**
   * Welke gegevensstromen bijdragen tot {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} gegevensset?
   * Welke brongegevens worden niet gebruikt of hebben geen gegevens die binnen komen?
   * Maak een lijst van de brongegevensstromen die ik heb.
   * Welke dataflows worden gevormd voor elke bronschakelaar?
* **Datasets - Operationele inzichten**
   * Hoeveel datasets zijn opgenomen gebruikend het zelfde schema?
   * Welke bronschakelaar wordt geassocieerd met {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} gegevensset?
   * Welke datasets worden gebruikt in elk publiek?
   * Welke schema&#39;s worden niet gebruikt in om het even welke datasets?
   * Hoeveel datasets heb ik?
* **Doelen - Operationele inzichten**
   * Welke bestemmingen zijn in een actieve staat?
   * Welke bestemmingsrekeningen hebben 0 publiek geactiveerd?
   * Hoeveel publiek wordt geactiveerd voor elke bestemming?
   * Welke bestemmingen hebben het hoogste aantal geactiveerde doelgroepen?
* **Transparantie - Operationele inzichten**
   * Hoeveel reizen heb ik?
   * Welke reizen zijn er gemaakt {RELATIVE_DATE} (bijvoorbeeld de laatste week) of {RELATIVE_DATE} (bijvoorbeeld voor/na/op een bepaalde datum)?
   * Toon me de lijst van reizen die binnen werden gewijzigd {RELATIVE_DATE} (bijvoorbeeld de laatste week) of {RELATIVE_DATE} (bijvoorbeeld voor/na/op een bepaalde datum)?
   * Maak een lijst van de levende reizen die ik heb.
   * Geef een overzicht van de soorten publiek die worden gebruikt voor rechtstreekse reizen.
* **Bronnen - Operationele inzichten**
   * Welke bronnen zijn actief?
   * Welke bronschakelaar met dataset wordt geassocieerd {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}.
   * Welke bronschakelaar heeft het hoogste aantal bijbehorende rekeningen?
   * Toon me de gegevensstromen en hun bijbehorende bronschakelaars.
* **Puntleren - Productkennis (Real-Time CDP en Journey Optimizer)**
   * Wat zijn gewone kijkers?
   * Hoe zijn Gebruikersgroepen verwant aan Rollen?
   * Wanneer moet ik een gegevenstype versus een veldgroep gebruiken?
   * Wat is het verschil tussen een identiteit en een primaire of buitenlandse sleutel?
   * Hoe wordt de rijkerheid van het Profiel berekend?
* **Problemen oplossen - Productkennis (Real-Time CDP en Journey Optimizer)**
   * Waarmee kan AI Assistant helpen?
   * Kan ik een profiel schrappen toegelaten schema nadat de gegevens worden opgenomen?
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
| <ul><li>Wees specifiek voor het object of de informatie die u wilt ophalen of analyseren.</li><li>Plaats uw gegevensobjectnamen tussen aanhalingstekens. Als u slechts een deel van de objecten naam kent, kunt u dat ook specificeren in de vraag.</li><li>Gebruiken [object automatisch aanvullen](./ui-guide.md#use-auto-complete) om AI Assistant te helpen de context van uw query beter te begrijpen.</li></ul> | <ul><li>Welke datasets gebruiken het &quot;Luma - Loyalty&quot;schema?</li><li>Toon me de geactiveerde segmenten die &quot;Luma&quot;in hun naam hebben. Rang ze op het aantal profielen.</li></ul> |
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

## Volgende stappen

Door dit document te lezen, hebt u nu inzicht in hoe u uw vragen kunt optimaliseren voor AI Assistant. Lees voor meer informatie over het gebruik van de functie tijdens uw workflows de [Handleiding voor AI Assistant-gebruikersinterface](ui-guide.md).
