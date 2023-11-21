---
title: Assistent voor Adobe Experience Platform
description: Leer hoe u met Assistant door Experience Platform- en Real-time Customer Data Platform-concepten kunt navigeren en deze kunt begrijpen, en hoe u informatie over uw objecten kunt gebruiken.
badge: Alfa
hide: true
hidefromtoc: true
exl-id: 8be1c222-3ccd-4a41-978e-33ac9b730f8c
source-git-commit: afc61a5809b1dfb59b87731d835cf8a1668f79df
workflow-type: tm+mt
source-wordcount: '2175'
ht-degree: 0%

---

# Assistent voor Adobe Experience Platform

>[!NOTE]
>
>Assistent voor Adobe Experience Platform is momenteel in Alpha. De functie en documentatie kunnen worden gewijzigd.

De assistent voor Adobe Experience Platform is een UI-functie waarmee u door de concepten Experience Platform en Real-time Customer Data Platform en gebruiksinformatie over uw objecten kunt navigeren en deze kunt begrijpen.

U kunt de Medewerker vragen voor informatie zoals:

* Richtlijnen voor het uitvoeren van taken die verband houden met gegevens en publiek.
* Statussen en metriek van de bestaande gegevensobjecten in uw organisatie.
* Gebruik voorbeelden en nuances van het geval om uw gegevensvoorwerpen, met inbegrip van attributen, datasets, bestemmingen, schema&#39;s, segmenten, en bronnen beter te begrijpen.

Dit document bevat informatie over de manier waarop u Assistant kunt gebruiken om vragen te stellen en antwoorden te ontvangen over concepten van Experience Platforms en Real-Time CDP.

>[!BEGINSHADEBOX]

**Hoe werkt Assistent?**

De medewerker antwoordt aan uw voorgelegde vragen door een gegevensbestand te vragen en dan gegevens van het gegevensbestand in een leesbaar antwoord te vertalen.

Deze interne vertegenwoordiging van onderliggende gegevens is ook genoemd geworden KennisGrafiek - een uitvoerig Web van concepten, gegevens, en meta-gegevens voor een bepaald antwoord.

De Kennisgrafiek bestaat uit subgrafieken waarnaar wordt verwezen wanneer query&#39;s worden verzonden:

* Gebruikersgegevens van de klant.
* Gebruikersgegevens van de klant in verschillende meta-winkels.
* Documentatie Experience League.

Er zijn twee klassen vragen om te overwegen alvorens Medewerker te vragen:

* **Conceptvragen**: Concept-vragen gaan over Adobe-concepten met betrekking tot gegevens of publiek. Voorbeelden van vragen over concepten zijn:
   * Wat is het verschil tussen partij en het stromen segmentatie?
   * Zijn er industriële gegevensmodellen en hoe gebruik ik deze?
   * Wanneer wordt Real-Time CDP het beste voorgeschreven?
* **Gebruiksvragen**: De vragen van het gebruik zijn over de gegevensvoorwerpen binnen uw organisatie. Enkele voorbeelden van gebruiksvragen zijn:
   * Hoeveel datasets heb ik?
   * Hoeveel schemakenmerken zijn nooit gebruikt?
   * Welke segmenten zijn geactiveerd?

>[!ENDSHADEBOX]

## De Medewerker van de toegang voor Experience Platform in UI

U kunt tot Medewerker van de kopbalnavigatie in de UI van het Experience Platform toegang hebben.

Selecteer de **[!UICONTROL Assistant icon]** van de koptekst naar het deelvenster Assistent starten.

![De homepage van UI van het Experience Platform met het Hulp geselecteerde pictogram.](./images/ai-assistant/ai-assistant.png)

<!-- +++Use immersive mode

To use [!DNL Immersive mode] select the focus icon in the header navigation of the Assistant.

![select-immersive](./images/ai-assistant/select-immersive.png)

A dedicated pop-up interface for Assistant appears at the center of your screen.

![immersive-mode](./images/ai-assistant/immersive-mode.png)

+++

From here, you can input your question in the text box and query Assistant for concepts regarding data or audiences. You can also ask questions about your data objects to better understand how you can use them for your respective use case.  -->

### Voorbeeld: gebruik de assistent om het maken van het schema te versnellen

>[!NOTE]
>
>In de volgende voorbeeldworkflow wordt het proces voor het maken van het ExperienceEvent-schema gebruikt om te laten zien hoe u Assistant kunt gebruiken wanneer u de gebruikersinterface van het Experience Platform gebruikt.

Overweeg een gebruiksgeval waarin u een **Apparaathandel in gebeurtenisschema**. Tijdens het aanmaakproces van het ExperienceEvent-schema komt u tegen `eventType` veld. U kunt nu de workflow verlaten en de documentatie in het dialoogvenster [grondbeginselen van een schemacompositie](../xdm/schema/composition.md)U kunt Assistant ook gebruiken om directe antwoorden op uw vragen op te halen.

Om te beginnen voert u uw vraag in het tekstvak in. In het onderstaande voorbeeld wordt Assistent de vraag gesteld: &quot;**Wat is het eventType-veld in een ExperienceEvent-schema?**&quot;

![De assistent voor Experience Platform met de volgende vraag voorbereid voor het vragen: &quot;Wat is het eventType-veld in een ExperienceEvent-schema?](./images/ai-assistant/question.png)

De medewerker vraagt dan zijn kennisbasis en berekent een antwoord. Na enkele ogenblikken retourneert de assistent een antwoord en verwante suggesties die u kunt gebruiken als follow-upaanwijzingen.

Een bepaald antwoord biedt hyperlinks naar entiteiten waarnaar wordt verwezen. Selecteer in het onderstaande voorbeeld de optie **[!UICONTROL Schemas]** om een lijst van de referenced schema&#39;s te bekijken, of **[!UICONTROL Segments]** om een lijst van de referenced segmenten te bekijken.

![Assistent voor Experience Platform met een antwoord op de vorige query.](./images/ai-assistant/answer.png)

De Medewerker verstrekt u een manier om uw antwoord te bevestigen door zijn bron te bekijken. De verbindingen aan de documentatie worden verstrekt voor concept vragen, terwijl de vragen van het gegevensgebruik met een SQL vraag kunnen worden geverifieerd die aantoont hoe het antwoord werd gegevens verwerkt.

![Opties die de assistent na het retourneren van een antwoord biedt.](./images/ai-assistant/options.png)

#### Vervolgvraag

+++Selecteer om een voorbeeld van een vervolgvraag te bekijken

U kunt meer over een bepaald onderwerp leren door een vervolgvraag te stellen. In het volgende voorbeeld, wordt de Medewerker gevraagd hoe eventType in segmentatie kan worden gebruikt.

![Een vervolgvraag en antwoord die op de Medewerker voor Experience Platform worden getoond.](./images/ai-assistant/follow-up-question.png)

+++

#### Vraag over gegevensgebruik

+++Selecteer om een voorbeeld van een vraag over gegevensgebruik te bekijken

U kunt ook vragen stellen aan de assistent over uw gegevensgebruik. Wanneer u informatie invraagt over het gebruik van gegevens, moet u zich in een actieve zandbak bevinden opdat de Medewerker uw vraag beantwoordt.

Voor reacties die informatie over gegevensgebruik bevatten, biedt Assistant koppelingen naar entiteiten in kwestie. Daarnaast geeft Assistant uitleg over de manier waarop het antwoord is berekend.

![Een vraag over gegevensgebruik, die vraagt hoeveel segmenten een gebruiker heeft.](./images/ai-assistant/data-usage-question.png)

+++

#### Meervoudig draaien

+++Selecteren om een voorbeeld van meerdere keren te bekijken

U kunt de multi-boommogelijkheden van Medewerker gebruiken om een natuurlijker gesprek tijdens uw ervaring te hebben. De assistent kan vervolgvragen beantwoorden aangezien de context van een vroegere interactie kan worden afgeleid.

In het onderstaande voorbeeld wordt de assistent gevraagd om een lijst met de bestaande segmenten in de organisatie te maken als follow-up van een eerdere query over het totale aantal segmenten.

![](./images/ai-assistant/multi-turn-one.png)

Vervolgens ontvangt Assistant een ander vervolgverzoek. Deze keer, antwoordt de Medewerker door de bestaande segmenten te vermelden die door hun respectieve grootte worden bevolen.

![](./images/ai-assistant/multi-turn-two.png)

+++

#### Automatisch aanvullen gebruiken

+++Selecteren om een voorbeeld van automatisch aanvullen weer te geven

Met de functie Automatisch aanvullen kunt u een lijst met gegevensobjecten ontvangen die in uw sandbox staan. De aanbevelingen van Autocomplete zijn beschikbaar voor de volgende domeinen: segmenten, schema&#39;s, datasets, bronnen, en bestemmingen.

Voer een plusteken in als u Automatisch aanvullen wilt gebruiken (**`+`**) als onderdeel van uw vraag. U kunt ook het plusteken (**`+`**) in het tekstinvoervak. Vervolgens wordt een venster weergegeven met een lijst met aanbevolen gegevensobjecten die in uw sandbox aanwezig zijn.

![](./images/ai-assistant/autocomplete-options.png)

Selecteer vervolgens het gegevensobject waarop u een query wilt uitvoeren om uw vraag te voltooien en verzend uw vraag.

![](./images/ai-assistant/autocomplete-question.png)

+++

## Bereik

De assistent kan vragen beantwoorden over de concepten Real-Time CDP en Experience Platform, maar ook over het specifieke gegevensgebruik voor je gebruikersaccount. De medewerker kan context ook afleiden die op de UI-pagina wordt gebaseerd die u binnen bent. Het kan identificeren:

* De gebruikersaccount die u gebruikt.
* De organisatie waartoe u behoort.
* De pagina die u op het scherm bekijkt.
* De bron (inclusief type en id) die u op uw scherm bekijkt.
* Aangezien u bezig bent met een bepaald Experience Platform of Real-Time CDP-workflow, kan Assistant uw intentie afleiden.

### Documentatie

Momenteel geldt de documentatie-index voor Adobe Experience Platform (Real-Time CDP en Soorten publiek). De index wordt periodiek bijgewerkt.

Het documentatiemodel wordt opgeleid op Experience Platform (Real-Time CDP en Soorten publiek). Vragen die buiten Adobe Experience Platform vallen, zoals vragen over andere producten van de Adobe, zoals Adobe Target en de Creative Cloud-suite, kunnen niet worden beantwoord.

### Gegevensgebruik

U kunt Assistent-vragen stellen over uw gegevensgebruik in de volgende domeinen:

* Attributen
* Gegevenssets
* Doelen _(Vragen over accounts en sommige vragen over gegevensstroom kunnen op dit moment niet worden beantwoord.)_
* Schemas _(Op dit moment kunnen vragen met betrekking tot veldgroepen niet worden beantwoord.)_
* Segmenten
* Bronnen _(Op dit moment kunnen vragen over de rekeningen niet worden beantwoord.)_

Voor vragen van gebruiksgegevens, kunnen de antwoorden niet op de huidige staat van UI wijzen. De gegevens die deze vragen ondersteunen, worden om de 24 uur bijgewerkt. Zo worden wijzigingen die gebruikers overdag aanbrengen in Real-Time CDP gesynchroniseerd met de gegevensopslag &#39;s nachts, waarna ze &#39;s ochtends beschikbaar komen voor vragen van gebruikers. Mogelijk moet u de vragen opmaken als: &quot;Wanneer was het segment met de titel {TITLE} gemaakt?&quot; in plaats van &quot;Wanneer was het {TITLE} segment gemaakt?&quot;

U moet zich aanmelden bij een sandbox om informatie te krijgen over specifieke gegevens die betrekking hebben op objecten, zoals schema&#39;s, datasets, kenmerken, doelen en segmenten.

### Voorbeeldvragen over gegevensgebruik

+++Selecteren om een lijst met voorbeelden van vragen over gegevensgebruik weer te geven

| Type vraag | Beschrijving | Voorbeelden |
| --- | --- | --- | 
| Gegevensverbinding | Gebruik van een of meerdere objecten bijhouden over andere Experience Platforms | <ul><li>Welke gegevensset(s) gebruiken {SCHEMA_NAME} schema?</li><li>Hoeveel datasets zijn opgenomen gebruikend het zelfde schema?</li><li>Welke datasets zijn gebruikt in geactiveerde segmenten?</li><li>Maak een lijst van de schema&#39;s die attributen hebben die in geactiveerde segmenten worden gebruikt.</li><li>Toon me de segmenten die worden geactiveerd om {DESTINATION_ACCOUNT_NAME} en hebben meer dan 1000 profielen.</li><li>Toon me de attributen die in de geactiveerde segmenten worden gebruikt die na jan 2023 zijn gewijzigd.</li><li>Wat zijn de datasets die via worden opgenomen {SOURCE_NAME}?</li><li>Aan welke gegevensstromen is gekoppeld {DATAFLOW_NAME}</li><li>Maak een lijst van de schema&#39;s die met geactiveerde segmenten verwant zijn en in vorig 1 jaar gecreeerd.</li></ul> |
| Distributie en aggregaties | Op samenvattingen gebaseerde vragen over het gebruik van Experience Platforms-objecten | <ul><li>Wat is het percentage van geactiveerde segmenten?</li><li>Hoeveel velden worden in segmentatie gebruikt?</li><li>Welke segmenten worden geactiveerd aan het meeste aantal bestemmingen?</li><li>Duplicaatsegmenten weergeven.</li><li>Toon me de segmenten die aan worden geactiveerd {DESTINATION_ACCOUNT_NAME} en rangschikken op profielgrootte.</li><li>Wat is het percentage van de segmenten die niet zijn geactiveerd maar meer dan 100 profielen hebben. Laat me hun namen zien.</li><li>Maak een lijst van de 3 bronschakelaars die gegevens in mijn datasets opnemen.</li><li>Geef me de bovenste 5 kenmerken weer die in geactiveerde segmenten worden gebruikt op basis van hun voorval.</li></ul> |
| Object opzoeken | Haal een Experience Platform-object of de eigenschappen ervan op of open het object. | <ul><li>Welke datasets hebben geen schema verbonden aan hen</li><li>De kenmerken weergeven die worden gebruikt voor {SEGMENT_NAME}?</li><li>Geef me de lijst van schema&#39;s die profiel toegelaten zijn maar niet sinds hun verwezenlijking zijn gewijzigd.</li><li>Welke segmenten zijn de afgelopen week gewijzigd?</li><li>Maak een lijst van de segmenten die de zelfde segmentdefinities samen met hun verwezenlijking datum hebben.</li><li>Welke datasets toegelaten profiel zijn en ook omvatten hoeveel segmenten van elke dataset zijn gecreeerd.</li><li>Welke bronrekeningen worden geassocieerd met dataset XYZ?</li><li>De segmentdefinitie en wijzigingsdatum weergeven van {SEGMENT_NAME}.</li></ul> |

+++

## Het antwoord controleren

U kunt de reactie verifiëren die de Medewerker gebruikend een aantal verschillende manieren terugkeert.

### Bijschriften voor documentatie

Met elke reactie geeft Assistant citaten waar je naar kunt verwijzen voor verificatie of meer informatie.

Selecteren **[!UICONTROL Show source]** voor een lijst van verbindingen aan documentatie die de Hulpverwijzingen om zijn reactie te berekenen. Wanneer u een koppeling naar de documentatie waarnaar wordt verwezen selecteert, wordt u doorverwezen naar de desbetreffende sectie van die bepaalde pagina, met de specifieke informatie gemarkeerd.

![De verbindingen aan de bron die in de Medewerker wordt getoond.](./images/ai-assistant/show-sources.png)

## Feedback geven

>[!BEGINSHADEBOX]

**Je feedback is aangevraagd**

Tijdens deze Alpha wordt u gevraagd feedback te geven over de reacties die u van de assistent ontvangt. Alle reacties en verzonden feedback worden gecontroleerd om de assistent-ervaring te blijven verbeteren.

Als u feedback wilt geven, selecteert u duimen omhoog of duimen omlaag na ontvangst van een reactie van de assistent en voert u vervolgens uw feedback in het tekstvak in. Selecteer vervolgens **[!UICONTROL Submit feedback]** om te verzenden.

>[!ENDSHADEBOX]

+++Feedback geven

>[!BEGINTABS]

>[!TAB Stompelen omhoog]

Selecteer het pictogram van duim omhoog om feedback te geven over wat goed met uw ervaring met de Medewerker ging.

![Het positieve feedbackvenster.](./images/ai-assistant/thumbs-up.png)

>[!TAB Miniatuur omlaag]

Selecteer de duim onderaan pictogram om feedback te geven over wat op basis van uw ervaring met de Medewerker zou kunnen worden verbeterd. Tijdens deze stap kunt u ook specifieke opmerkingen maken over uw ervaring. De feedback in de opmerkingen wordt dagelijks bekeken.

![Het negatieve feedbackvenster.](./images/ai-assistant/thumbs-down.png)

>[!TAB Markering]

Selecteer het vlagpictogram om verdere rapporten over uw ervaring te verstrekken gebruikend de Medewerker.

![Het venster met rapportresultaten.](./images/ai-assistant/flag.png)

>[!ENDTABS]

+++

## Aanvullende informatie

Raadpleeg deze sectie voor meer informatie over de assistent voor Experience Platform.

### Voorzorgsmaatregelen en beperkingen

De volgende sectie schetst huidige waarschuwingen en beperkingen om te overwegen wanneer het gebruiken van Medewerker.
<!-- 
#### Conversational experience

You must consider several nuances regarding the conversational experience when querying the Assistant.

>[!NOTE]
>
>These limitations are temporary and are being improved upon throughout the course of the alpha.

>[!BEGINTABS]

>[!TAB Unable to infer context from prior discussion]

The Assistant currently cannot reference prior discussions as context for a given question. See the table below for examples:

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of them?"</li></ul>| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of **segments**?"</li></ul> | The Assistant cannot infer what "them" means. |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you elaborate more?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Explain what a segment is in depth"</li></ul> | The Assistant cannot intelligently reference documentation based on "more". |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of one?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of a segment?"</li></ul> | The Assistant cannot infer what you want an example of.|
| <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "How does it compare to a streaming segment?"</li></ul> | <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "Can you compare a streaming segment to a batch segment?"</li></ul> | The Assistant cannot infer what "it" is referring to and thus cannot compare the streaming segment. |
| <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of them use Facebook as a destination?"</li></ul> | <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of the segments that I have are using Facebook as a destination?"</li></ul> | The Assistant is cannot infer what "them" is referring to. |

{style="table-layout:auto"}

>[!TAB Unable to infer context from a page]

When asking the Assistant about a particular element of the Experience Platform UI page that you are on, you must clearly define the specific element within your question. 

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "What does this do?" | "What does {PAGE_NAME} do? | The Assistant cannot infer what "this" is referring to. You must provide the specific page element that you are querying about. |
| "Why won't it save?" | "Why can't I save a new sandbox called {NAME}?" | The Assistant cannot infer what "it" is referring to and cannot know that you are having issues with an entity. |

{style="table-layout:auto"}

Furthermore, the Assistant can only answer questions regarding error messages, given that the error is documented in Experience League.

>[!TAB Ambiguity]

You must phrase your questions clearly and scope them within a product, application, or domain, as the Assistant currently cannot disambiguate questions.

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "How do I create a filter? | How do I create a filter in Profile Query Language? | You must specify the feature that which you are filtering for because a variety of Experience Platform features support filtering. |
| "How do I get started? | How do I get started using destinations? | You must provide clarity on your goals and use case because overly broad concepts may result in generic or unnecessarily specific answers. |

{style="table-layout:auto"}

>[!ENDTABS] -->

#### Beperkte kleine praatjes

U kunt kleine gesprekken voeren met de assistent, maar deze mogelijkheid is momenteel beperkt.

#### Capaciteitsvragen

De assistent kan een onjuiste indruk geven van wat hij kan doen. De volgende typen vragen kunnen onjuist worden beantwoord:

| Voorbeeldvraag | Opmerking |
| --- | --- |
| &quot;Kunt u vragen beantwoorden op {ENTITY}?&quot; | Zolang de Medewerker één enkele pagina kan vinden die naar een bepaalde entiteit in zijn index verwijst, dan zal het ja antwoorden. |
| &quot;Weet je **x** taal?&quot; | De Medewerker steunt momenteel slechts Engels, maar kan &quot;ja&quot;antwoorden aangezien het onderliggende model het kan steunen. |
| &quot;Kan je...?&quot; | De assistent kan ja antwoorden, hoewel dat niet het geval is. |

### Tips

In de volgende sectie worden enkele tips en tijdelijke oplossingen beschreven die u in overweging kunt nemen bij het gebruik van de assistent.

#### De vragen kunnen met de verkeerde informatiebron worden beantwoord

Soms kan een vraag over uw gebruiksgegevens resulteren in een antwoord op basis van de documentatie. Dit komt omdat de assistent uw vraag verkeerd naar de verkeerde informatiebron kan leiden. U kunt dit voorkomen door:

* Herhaal uw vraag om meer SQL-achtige taal te gebruiken
* Expliciet het roepen van de informatiebron aan gebruik.

Lees de onderstaande tabel voor voorbeelden:

| Onjuiste vraag | Goede vraag | Notities |
| --- | --- | --- |
| Wat is mijn grootste segment? | Wat is mijn grootste segment? Gegevens gebruiken. | Vertel de Medewerker uitdrukkelijk dat u het antwoord op gegevens wilt worden gebaseerd. |
| Wat is mijn grootste segment? | Maak een lijst van mijn grootste segment. | Er zijn gevallen waarin een &quot;wat...&quot;-vraag kan worden verward met een documentatiegebaseerde vraag. Het gebruik van een opdracht als &quot;list&quot; is een sterkere indicator die u een vraag stelt met gegevens in context. |
| Hoeveel datasets heb ik? | Tel mijn datasets. | De oorspronkelijke vraag werkt voor segmenten, maar werkt mogelijk niet met gegevenssets. |
