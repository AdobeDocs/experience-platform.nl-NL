---
title: Overzicht van AI Assistant
description: Leer meer over AI Assistant, de nuances en gebruiksgevallen en hoe u deze kunt gebruiken om uw workflow met Adobe Experience Platform en Real-time Customer Data Platform te versnellen.
hide: true
hidefromtoc: true
source-git-commit: fe87a487079f5154f238b2d425cdd249a4724762
workflow-type: tm+mt
source-wordcount: '2294'
ht-degree: 0%

---

# AI Assistant in Adobe Experience Platform

Lees dit document voor meer informatie over AI Assistant in Adobe Experience Platform.

AI Assistant in Adobe Experience Platform is een conversatie-ervaring die u kunt gebruiken om uw workflows in Adobe-toepassingen te versnellen. U kunt AI Medewerker gebruiken om productkennis beter te begrijpen, problemen problemen op te lossen, of door informatie te zoeken en operationele inzichten te vinden. AI Assistant biedt ondersteuning voor Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer en Customer Journey Analytics.

>[!IMPORTANT]
>
>* U moet akkoord gaan met [een gebruikersovereenkomst](https://adobe.sharepoint.com/:w:/s/ExCUserExperience/EVzJv1jFBiZGnaFEufsfIqwBC_9ehv3KaXTkEMTGpQFRpg?e=qzwOo8) voordat u AI Assistant kunt gebruiken. De gebruikersovereenkomst bevat ook de openbare bètaovereenkomst. Dit is zodat u extra eigenschappen van AI Medewerker kunt gebruiken aangezien zij in een bètacapaciteit uitrollen.

![De AI Assistant-interface waarbij de eerste gebruikerservaring wordt geactiveerd.](./images/blank.png)

## AI-assistent begrijpen {#understanding-ai-assistant}

De Medewerker van AI antwoordt op uw voorgelegde vragen door een gegevensbestand te vragen en dan gegevens van het gegevensbestand in een leesbaar antwoord te vertalen.

Deze interne representatie van onderliggende gegevens wordt ook wel de **[!DNL Knowledge Graph]** - een uitgebreid web van concepten, gegevens en metagegevens voor een bepaald antwoord.

De [!DNL Knowledge Graph] bestaat uit subgrafieken waarnaar wordt verwezen wanneer query&#39;s worden ingediend:

* Operationele inzichten van de klant.
* Operationele inzichten van de klant in verschillende meta-winkels.
* Documentatie Experience League.

Er zijn twee klassen vragen om te overwegen alvorens AI Medewerker te vragen:

### Productkennis {#product-knowledge}

De kennis van het product verwijst naar concepten en onderwerpen die in de documentatie van het Experience League worden gebaseerd. Vragen over productkennis kunnen nader worden omschreven in de volgende subgroepen:

| Productkennis | Voorbeelden |
| --- | --- |
| Aanbevolen lessen | <ul><li>Wat is het verschil tussen een identiteit en een primaire of buitenlandse sleutel?</li><li>Hoe wordt profielrijkheid berekend?</li></ul> |
| Openbare detectie | <ul><li>Hoe kan ik deze dataset uitvoeren?</li><li>Zijn er regelingen voor klanten in de gezondheidszorg?</li></ul> |
| Problemen oplossen | <ul><li>Waarom kan ik geen schema aanzetten dat door Adobe voor profiel wordt bezeten?</li><li>Waarom kan ik een segment niet verwijderen?</li></ul> |

{style="table-layout:auto"}

### Operationele inzichten {#operational-insights}

>[!IMPORTANT]
>
>De antwoorden van de operationele inzichten zijn in bèta. Iedereen die toegang heeft tot de **Operationele inzichten weergeven** toestemming zal toegang hebben tot antwoorden op operationele inzichten .

De operationele inzichten verwijzen naar antwoorden AI Medewerker produceert over uw voorwerpen van meta- gegevens (attributen, publiek, dataflows, datasets, bestemmingen, reizen, schema&#39;s, en bronnen), met inbegrip van tellingen, raadplegingen, en lijneffect. Er worden geen gegevens in de sandbox weergegeven.

* Hoeveel datasets heb ik?
* Hoeveel schemakenmerken zijn nooit gebruikt?
* Welk publiek is geactiveerd?

U kunt AI Assistant-vragen stellen over uw operationele inzichten in de volgende domeinen:

* Attributen
* Soorten publiek
* Gegevensstromen
* Gegevenssets
* Doelen _(Vragen over accounts en sommige vragen over gegevensstroom kunnen op dit moment niet worden beantwoord.)_
* Journeys
* Schemas _(Op dit moment kunnen vragen met betrekking tot veldgroepen niet worden beantwoord.)_
* Bronnen _(Op dit moment kunnen vragen over de rekeningen niet worden beantwoord.)_

Voor vragen over operationele inzichten weerspiegelen de antwoorden mogelijk niet de huidige status van de gebruikersinterface. De gegevens die deze vragen ondersteunen, worden om de 24 uur bijgewerkt. Zo worden wijzigingen die gebruikers overdag aanbrengen in Real-Time CDP gesynchroniseerd met de gegevensopslag &#39;s nachts, waarna ze &#39;s ochtends beschikbaar komen voor vragen van gebruikers. U moet zich aanmelden bij een sandbox voor informatie over specifieke gegevens die betrekking hebben op objecten.

## Toegang tot functies {#feature-access}

Voor de toegang tot AI Assistant gelden de volgende parameters:

* **Toegang krijgen tot de toepassing:** U hebt toegang tot AI Assistant in Adobe Experience Platform, Adobe Real-Time CDP, Adobe Journey Optimizer en [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).
* **Contractuele toegang:** Uw bedrijf moet akkoord gaan met bepaalde [!DNL GenAI]-related legal terms voordat uw organisatie AI Assistant kan gebruiken. Neem contact op met de beheerder van uw organisatie of met uw accountteam voor Adoben als u geen toegang kunt krijgen tot AI Assistant.
* **Rechten:** Gebruik de [Gebruikersinterface voor machtigingen](../access-control/abac/ui/permissions.md) toegang tot AI Assistant in uw organisatie verlenen of intrekken. Als u de AI-assistent wilt gebruiken, moet een bepaalde gebruiker tot een rol behoren die is ingericht met de **AI-assistent inschakelen** en **Operationele inzichten weergeven** machtigingen.
   * Als beheerder kunt u de opdracht **AI-assistent inschakelen** aan een bepaalde rol en voeg een gebruiker aan die rol toe, om hen toe te staan om tot AI Medewerker in uw organisatie toegang te hebben.
   * Als beheerder kunt u de opdracht **Operationele inzichten weergeven** aan een bepaalde rol en voeg een gebruiker aan die rol toe, om hen toe te staan om de operationele mogelijkheden van Inzichten van AI Medewerker te gebruiken. Operationele inzichten bevinden zich momenteel in bèta.

![De pagina met bevoegdheden UI met de Enable AI Assistant en View Operational Insights onder een bepaalde rol.](./images/permissions.png)

## Voorbeeldvragen {#example-questions}

In deze sectie worden voorbeeldvragen beschreven waarnaar u tijdens uw workflows kunt verwijzen. De vragen zijn gegroepeerd in drie secties: operationele inzichten, doelstellingen, en voorwerpen.

### Voorbeeldvragen gegroepeerd op operationele inzichten {#operational-insights-questions}

+++Selecteer deze optie om voorbeelden weer te geven van vragen over het operationele inzicht en de bijbehorende gebruiksgevallen:

| Type vraag | Hoofdletters gebruiken | Voorbeelden |
| --- | --- | --- | 
| Gegevensverbinding | Gebruik van een of meerdere objecten bijhouden over andere Experience Platforms | <ul><li>Welke datasets gebruiken het schema &quot;ACME&quot;?</li><li>Hoeveel datasets zijn opgenomen gebruikend het zelfde schema?</li><li>Welke datasets zijn gebruikt in geactiveerd publiek?</li><li>Maak een lijst van de schema&#39;s die attributen hebben die in geactiveerd publiek worden gebruikt.</li><li>Toon me het publiek dat aan &quot;Doel ACME&quot;wordt geactiveerd en meer dan 1000 profielen heeft.</li><li>Toon me de attributen die in de geactiveerde doelgroepen worden gebruikt die na jan 2023 zijn gewijzigd.</li><li>Wat worden de datasets via &quot;ACME Amazon S3&quot;bron opgenomen?</li><li>Welke gegevensstromen worden geassocieerd met &quot;ACME Loyalty Dataflow&quot;?</li><li>Geef een overzicht van de schema&#39;s die betrekking hebben op geactiveerd publiek en die in het afgelopen jaar zijn gemaakt.</li></ul> |
| Distributie en aggregaties | Op samenvattingen gebaseerde vragen over het gebruik van Experience Platforms-objecten | <ul><li>Wat is het percentage van het actieve publiek?</li><li>Hoeveel velden worden in segmentatie gebruikt?</li><li>Welk publiek wordt geactiveerd aan het meeste aantal bestemmingen?</li><li>Duplicaat publiek weergeven.</li><li>Toon me het publiek dat aan &quot;Doel ACME&quot;wordt geactiveerd en rangschikt hen door profielgrootte.</li><li>Wat is het percentage van het publiek dat niet is geactiveerd, maar meer dan 100 profielen heeft. Laat me hun namen zien.</li><li>Maak een lijst van de 3 bronschakelaars die gegevens in mijn datasets opnemen.</li><li>Geef me de bovenste 5 kenmerken weer die bij actiepunten worden gebruikt, afhankelijk van het aantal dat ze voorkomen.</li></ul> |
| Object opzoeken | Haal een Experience Platform-object of de eigenschappen ervan op of open het object. | <ul><li>Welke datasets hebben geen schema verbonden aan hen</li><li>De kenmerken weergeven die worden gebruikt voor &quot;ACME Audience&quot;?</li><li>Geef me de lijst van schema&#39;s die profiel toegelaten zijn maar niet sinds hun verwezenlijking zijn gewijzigd.</li><li>Welk publiek is de afgelopen week gewijzigd?</li><li>Geef mij een overzicht van de doelgroepen die dezelfde segmentdefinities hebben en de datum waarop ze zijn gemaakt.</li><li>Welke datasets toegelaten profiel zijn en ook omvatten hoeveel publiek van elke dataset is gecreeerd.</li><li>Welke bronrekeningen worden geassocieerd met dataset XYZ?</li><li>Toon me de segmentdefinitie en wijzigingsdatum van &quot;ACME Publiek&quot;.</li></ul> |
| Objectvergelijking | Dubbele doelgroepen identificeren. | <ul><li>Vermeld op basis van hun segmentdefinitie de soorten publiek die duplicaten zijn.</li><li>Welke dubbele soorten publiek worden geactiveerd aan &quot;ACME Doelen&quot;.</li></ul> |

{style="table-layout:auto"}

+++

### Voorbeeldvragen gegroepeerd op doelstellingen {#objectives-questions}

+++Selecteren om een lijst weer te geven met doelstellingen die u kunt bereiken met AI Assistant

| Doelstelling | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Leerconcepten en doorlopende workflows | <ul><li>Als beginnende gebruiker, kunt u AI Medewerker gebruiken om de concepten van Real-Time CDP en van Adobe Journey Optimizer te leren en aan boord aan producten en eigenschappen te zijn die u niet vertrouwd met bent.</li><li>Als ervaren gebruiker, kunt u AI Medewerker gebruiken om een randgeval op te lossen dat uw werkschema kan blokkeren. | <ul><li>Hoe kan ik een dashboard instellen in Journey Analytics?</li><li>Vertel me wat gebruiksgevallen voor Real-Time CDP.</li></ul> |
| Problemen oplossen | Met AI Assistant leert u hoe u fouten in de basisbeginselen die u in uw workflow tegenkomt, kunt opsporen. | <ul><li>Wat is deze fout? {ERROR_MESSAGE} bedoel?</li><li>Waarom kan ik het publiek met de naam &quot;Luma: Email Audience&quot; niet verwijderen?</li></ul> |
| Zandbakhygiëne | Met AI Assistant kunt u eventuele duplicaten of ongebruikte objecten identificeren, zodat u de sandbox op efficiënte wijze kunt onderhouden. | <ul><li>Kan je me een publiek laten zien dat vergelijkbaar is?</li><li>Zijn er regelingen die geen bijbehorende dataset hebben?</li></ul> |
| Waardeanalyse | Met AI Assistant kunt u de meest gebruikte gegevensobjecten identificeren en prestatie-indicatoren beoordelen of de meest waardevolle gegevensobjecten vinden. | <ul><li>Hoeveel profielen bevinden zich in de segmentdefinitie &quot;Luma: Email Audience&quot;?</li><li>Wanneer werd het publiek geactiveerd aan de bestemming van het publiek van het Experience Cloud?</li></ul> |
| Zoeken | De Medewerker van AI van het gebruik om gesteunde voorwerpen van het Experience Platform zoals publiek, datasets, bestemmingen, schema&#39;s, en bronnen te vinden. | <ul><li>Maak een lijst van de soorten publiek die &quot;Luma&quot;in de naam bevatten die in het laatste kwartaal werden gecreeerd.</li><li>Welke kenmerken bevinden zich in het XDM-schema &quot;Luma: Custom Actions&quot;?</li></ul> |
| Effectanalyse | Met AI Assistant kunt u gegevensobjecten identificeren die in bepaalde workflows zijn gebruikt, zodat u het effect van wijzigingen kunt beoordelen. | <ul><li>Welk publiek gebruikt `homeAddress.city` in het schema &quot;Luma: PersonProfiles&quot;?</li><li>Welke datasets zijn `consents.marketing.push.val` profielkenmerk opgeslagen in?</li></ul> |

{style="table-layout:auto"}

+++

### Voorbeeldvragen gegroepeerd op objecten {#objects-questions}

+++Selecteer om een lijst met voorbeeldvragen weer te geven die u met AI Assistant kunt helpen:

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

+++

## Uw vragen formuleren {#phrasing-your-questions}

U moet uw vragen duidelijk en in de context tot AI Assistant richten om zo accuraat mogelijk te kunnen antwoorden. Raadpleeg de volgende tips voor het stellen van een duidelijke vraag met betrekking tot de context:

* Geef uw taak en/of vraag beknopt weer.
* Vermijd dubbelzinnige taal of te complexe syntaxis om het begrip te vergemakkelijken.
* Een relevante context bieden met betrekking tot uw taak en/of vraag als context kan AI Assistant helpen meer relevante reacties te genereren.

Lees de onderstaande tabellen voor meer informatie over aanbevolen procedures bij het stellen van vragen aan AI Assistant.

+++Selecteer om voorbeelden weer te geven van aanbevolen procedures voor het formuleren van uw vragen

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

+++

## Volgende stappen

Nu u een algemeen begrip van AI Medewerker hebt, kunt u nu te werk gaan en AI Medewerker tijdens uw werkschema&#39;s gebruiken. Raadpleeg de volgende documentatie voor meer informatie:

* [Handleiding voor AI Assistant-gebruikersinterface](./ui-guide.md)
* [Privacy, beveiliging en bestuur in AI Assistant](./privacy.md)
* [Veelgestelde vragen](./faq.md)