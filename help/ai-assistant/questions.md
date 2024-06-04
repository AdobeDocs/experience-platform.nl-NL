---
title: Vraag voor AI-assistent
description: Lees dit document om voorbeeldvragen te leren die u kunt gebruiken wanneer het vragen van AI Medewerker.
source-git-commit: a1092e21940c5e4ba9b598bc51ba1243b57a0051
workflow-type: tm+mt
source-wordcount: '1224'
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

| Object | Beschrijving |
| --- | --- |
| Publiek - Operationele inzichten | <ul><li>Welk publiek gebruikt ander publiek?</li><li>Wat is de verdeling van het aantal profielen over het publiek?</li><li>Toon me het publiek dat het laatst werd gewijzigd eerder {RELATIVE_DATE}.</li><li>Welk publiek heeft 0 profielen?</li><li>Is {USE_AUTOCOMPLETE_TO_FILL_AUDIENCE_NAME} bij andere doelgroepen worden gebruikt?</li></ul> |
| Attributen - Operationele inzichten | <ul><li>Welk publiek heeft XDM-kenmerk {ATTRIBUTE_PATH} in hun segmentdefinitie?</li><li>Hoeveel XDM schemakenmerken worden niet gebruikt in om het even welk publiek?</li><li>Welke schema&#39;s hebben XDM attribuut {ATTRIBUTE_PATH} in hen?</li><li>Welke attributen XDM worden geactiveerd?</li><li>Welke XDM-kenmerken worden gebruikt bij het publiek met meer dan 10 profielen</li></ul> |
| Gegevensstromen - Operationele inzichten | <ul><li>Welke gegevensstromen bijdragen tot {DATASET_NAME} gegevensset?</li><li>Welke brongegevens worden niet gebruikt of hebben geen gegevens die binnen komen?</li><li> |
| Datasets - Operationele inzichten | <ul><li>Hoeveel datasets zijn opgenomen gebruikend het zelfde schema?</li><li>Welke bronschakelaar wordt geassocieerd met {DATASET_NAME} dataset></li><li>Welke datasets worden gebruikt in elk publiek?</li><li>Welke schema&#39;s worden niet gebruikt in om het even welke datasets?</li><li>Hoeveel datasets heb ik?</li></ul> |
| Doelen - Operationele inzichten | <ul><li>Welke bestemmingen zijn in een actieve staat?</li><li>Welke bestemmingsrekeningen hebben 0 publiek geactiveerd?</li><li> |
| Transparantie - Operationele inzichten | <ul><li>Hoeveel reizen heb ik?</li><li>Welke reizen zijn er gemaakt {RELATIVE_DATE} (bijvoorbeeld vorige week) of {RELATIVE_DATE} (bijvoorbeeld voor/na/op een bepaalde datum)?</li><li>Toon me de lijst van reizen die binnen werden gewijzigd {RELATIVE_DATE} (bijvoorbeeld vorige week) of {RELATIVE_DATE} (bijvoorbeeld voor/na/op een bepaalde datum)?</li><li>Geef een lijst van de reizen die ik heb.</li><li>Geef een overzicht van de soorten publiek die worden gebruikt voor rechtstreekse reizen.</li></ul> |
| Schema&#39;s - Operationele inzichten | <ul><li>Welke gebieden van het schema hebben tot het meest publiek bijgedragen?</li><li>Hoeveel schema&#39;s worden profiel toegelaten?</li><li>Alle schema&#39;s weergeven die in de laatste week zijn gewijzigd.</li><li>Welke schema&#39;s worden niet gebruikt in om het even welke datasets?</li><li>Alle schema&#39;s weergeven die in de laatste week zijn gemaakt.</li></ul> |
| Bronnen - Operationele inzichten | <ul><li>Welke bronnen zijn actief?</li><li>Welke bronschakelaar met dataset wordt geassocieerd {DATASET_NAME}?</li><li>Welke bronschakelaar heeft het hoogste aantal bijbehorende rekeningen?</li><li>Toon me de gegevensstromen en hun bijbehorende bronschakelaars.</li></ul> |
| Puntleren - Productkennis (Real-Time CDP en Journey Optimizer) | <ul><li>Waarmee kan AI Assistant helpen?</li><li>Wat zijn gewone kijkers?</li><li>Hoe zijn Gebruikersgroepen verwant aan Rollen?</li><li>Wanneer moet ik een gegevenstype versus een veldgroep gebruiken?</li><li>Wat is het verschil tussen een identiteit en een primaire of buitenlandse sleutel?</li><li>Hoe wordt profielrijkheid berekend?</li></ul> |
| Problemen oplossen - Productkennis (Real-Time CDP en Journey Optimizer) | <ul><li>Waarmee kan AI Assistant helpen?</li><li>Kan ik een profiel-toegelaten schema schrappen nadat de gegevens worden opgenomen?</li><li>Waarom kan ik geen publiek verwijderen?</li><li>Hoe lang duurt het voordat het publiek wordt geëvalueerd en de resultaten beschikbaar zijn voor doelgericht onderzoek?</li></ul> |

{style="table-layout:auto"}

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
