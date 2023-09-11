---
title: AI Assistant voor Adobe Experience Platform
description: Leer hoe u de AI Assistant gebruikt om door Experience Platform- en Real-time Customer Data Platform-concepten te navigeren en deze te begrijpen, en om informatie over uw objecten te gebruiken.
badge: Alfa
hide: true
hidefromtoc: true
source-git-commit: 55d2518cdded50bcc8d6f7cc36f29581c5e64dab
workflow-type: tm+mt
source-wordcount: '2362'
ht-degree: 0%

---

# AI Assistant voor Adobe Experience Platform

>[!NOTE]
>
>De AI-assistent voor Adobe Experience Platform bevindt zich momenteel in Alpha. De functie en documentatie kunnen worden gewijzigd.

De AI-assistent voor Adobe Experience Platform is een interface-functie waarmee u door de concepten Experience Platform en Real-time Customer Data Platform en gebruiksinformatie over uw objecten kunt navigeren en deze kunt begrijpen.

U kunt de AI-assistent vragen naar informatie zoals:

* Richtlijnen voor het uitvoeren van taken die verband houden met gegevens en publiek.
* Statussen en metriek van de bestaande gegevensobjecten in uw organisatie.
* Gebruik voorbeelden en nuances van het geval om uw gegevensvoorwerpen, met inbegrip van attributen, datasets, bestemmingen, schema&#39;s, segmenten, en bronnen beter te begrijpen.

Dit document bevat informatie over de manier waarop u de AI Assistant kunt gebruiken om vragen te stellen en antwoorden te ontvangen over concepten van Experience Platforms en Real-Time CDP.

>[!BEGINSHADEBOX]

**Hoe werkt de AI Assistant?**

De AI Medewerker antwoordt op uw voorgelegde vragen door een gegevensbestand te vragen en dan gegevens van het gegevensbestand in een leesbaar antwoord te vertalen.

Deze interne vertegenwoordiging van onderliggende gegevens is ook genoemd geworden KennisGrafiek - een uitvoerig Web van concepten, gegevens, en meta-gegevens voor een bepaald antwoord.

De Kennisgrafiek bestaat uit subgrafieken waarnaar wordt verwezen wanneer query&#39;s worden verzonden:

* Gebruikersgegevens van de klant.
* Gebruikersgegevens van de klant in verschillende meta-winkels.
* Documentatie Experience League.

Er zijn twee klassen vragen om te overwegen alvorens de Medewerker AI te vragen:

* **Conceptvragen**: Concept-vragen gaan over Adobe-concepten met betrekking tot gegevens of publiek. Voorbeelden van vragen over concepten zijn:
   * Wat is het verschil tussen partij en het stromen segmentatie?
   * Zijn er industriële gegevensmodellen en hoe gebruik ik deze?
   * Wanneer wordt Real-Time CDP het beste voorgeschreven?
* **Gebruiksvragen**: De vragen van het gebruik zijn over de gegevensvoorwerpen binnen uw organisatie. Enkele voorbeelden van gebruiksvragen zijn:
   * Hoeveel datasets heb ik?
   * Hoeveel schemakenmerken zijn nooit gebruikt?
   * Welke segmenten zijn geactiveerd?

>[!ENDSHADEBOX]

## De AI-assistent voor Experience Platform openen in de gebruikersinterface

U kunt tot de Medewerker van AI van de kopbalnavigatie in de UI van het Experience Platform toegang hebben.

Selecteer de **[!UICONTROL AI Assistant icon]** in de koptekst om het deelvenster AI Assistant te starten.

![De homepage van UI van het Experience Platform met het AI Hulp geselecteerde pictogram.](./images/ai-assistant/ai-assistant.png)

Van hier, kunt u uw vraag in het tekstvakje invoeren en AI Medewerker voor concepten betreffende gegevens of publiek vragen. U kunt ook vragen stellen over uw gegevensobjecten om beter te begrijpen hoe u deze kunt gebruiken voor uw respectievelijke gebruiksscenario.

### Voorbeeld: gebruik de AI-assistent om het maken van het schema te versnellen

>[!NOTE]
>
>In de volgende voorbeeldworkflow wordt het proces voor het maken van het ExperienceEvent-schema gebruikt om te laten zien hoe u de AI Assistant kunt gebruiken wanneer u de gebruikersinterface van het Experience Platform gebruikt.

Overweeg een gebruiksgeval waarin u een **Apparaathandel in gebeurtenisschema**. Tijdens het aanmaakproces van het ExperienceEvent-schema komt u tegen `eventType` veld. U kunt nu de workflow verlaten en de documentatie in het dialoogvenster [grondbeginselen van een schemacompositie](../xdm/schema/composition.md)U kunt ook de AI Assistant gebruiken om directe antwoorden op uw vragen op te halen.

Om te beginnen voert u uw vraag in het tekstvak in. In het onderstaande voorbeeld wordt aan de AI Assistant de volgende vraag gesteld: &quot;**Wat is het eventType-veld in een Experience Event-schema?**&quot;

![De AI-assistent voor Experience Platform met de volgende vraag voorbereid voor query: &quot;Wat is het veld eventType in een ExperienceEvent-schema?](./images/ai-assistant/question.png)

De AI Medewerker zoekt dan zijn kennisbasis en berekent een antwoord. Na enkele ogenblikken retourneert de AI-assistent een antwoord en verwante suggesties die u kunt gebruiken als follow-upaanwijzingen.

![De AI Medewerker voor Experience Platform met een antwoord op de vorige vraag.](./images/ai-assistant/answer.png)

U kunt meer over een bepaald onderwerp leren door een vervolgvraag te stellen. In het volgende voorbeeld wordt aan de AI-assistent gevraagd hoe het eventType in segmentatie kan worden gebruikt.

![Een vervolgvraag en antwoord die worden weergegeven in de AI Assistant voor Experience Platform.](./images/ai-assistant/follow-up-answer.png)

U kunt ook vragen stellen aan de AI Assistant over uw gegevensgebruik. Wanneer u informatie invraagt over gegevensgebruik, moet u in een actieve zandbak zijn opdat de AI Medewerker uw vraag beantwoordt.

![Een vraag over gegevensgebruik, die vraagt hoeveel segmenten een gebruiker heeft.](./images/ai-assistant/data-usage-question.png)

Met elk antwoord biedt de AI-assistent u een manier om uw antwoord te valideren door de bron ervan te bekijken. De verbindingen aan de documentatie worden verstrekt voor concept vragen, terwijl de vragen van het gegevensgebruik met een SQL vraag kunnen worden geverifieerd die aantoont hoe het antwoord werd gegevens verwerkt.

>[!BEGINSHADEBOX]

**Je feedback is aangevraagd**

Tijdens dit alfakanaal wordt u gevraagd feedback te geven over de reacties die u ontvangt van de AI Assistant. Alle reacties en ingediende feedback worden gecontroleerd om de AI Assistant-ervaring te blijven verbeteren.

Als u feedback wilt geven, selecteert u duimen omhoog of duimen omlaag na ontvangst van een reactie van de AI Assistant en voert u uw feedback in het tekstvak in. Selecteer vervolgens **[!UICONTROL Submit feedback]** om te verzenden.

>[!ENDSHADEBOX]

>[!BEGINTABS]

>[!TAB Show source]

Selecteren **[!UICONTROL Show source]** voor een lijst met koppelingen naar de documentatie waarnaar de AI-assistent verwijst om zijn reactie te berekenen.

![De koppelingen naar de bron in de AI-assistent.](./images/ai-assistant/show-sources.png)

>[!TAB Stompelen omhoog]

Selecteer het pictogram van duim op om feedback te geven over wat goed met uw ervaring met de AI Assistant is gegaan.

![Het positieve feedbackvenster.](./images/ai-assistant/positive-feedback.png)

>[!TAB Miniatuur omlaag]

Selecteer het pictogram met de miniaturen omlaag om feedback te geven over de verbeteringen die u kunt aanbrengen op basis van uw ervaring met de AI Assistant. Tijdens deze stap kunt u ook specifieke opmerkingen maken over uw ervaring. De feedback in de opmerkingen wordt dagelijks bekeken.

![Het negatieve feedbackvenster.](./images/ai-assistant/negative-feedback.png)

>[!TAB Markering]

Selecteer het vlagpictogram om verdere rapporten over uw ervaring te verstrekken gebruikend de Medewerker AI.

![Het venster met rapportresultaten.](./images/ai-assistant/report-results.png)

>[!ENDTABS]

### Aan de slag

U kunt ook de vooraf ingestelde aanwijzingen gebruiken die de AI Assistant biedt om aan de slag te gaan.

![De verstrekte herinneringen in het AI Hulp paneel.](./images/ai-assistant/ideas.png)

## Aanvullende informatie

Raadpleeg deze sectie voor meer informatie over de AI Assistant voor Experience Platform.

### Bereik

De AI-assistent kan vragen beantwoorden op basis van de documentatie en uw gegevensgebruik.

#### Documentatie

U kunt documentatievragen stellen op basis van Real-time Customer Data Platform en Soorten publiek. Momenteel geldt de documentatie-index voor Adobe Experience Platform (Real-Time CDP en Soorten publiek). De index wordt periodiek bijgewerkt.

Het documentatiemodel wordt opgeleid op Experience Platform (Real-Time CDP en Soorten publiek). Vragen die buiten Adobe Experience Platform vallen, zoals vragen over andere producten van de Adobe, zoals Adobe Target en de Creative Cloud-suite, kunnen niet worden beantwoord.

#### Gegevensgebruik

U kunt ook vragen stellen aan de AI Assistant over uw gegevensgebruik in de volgende domeinen:

* Attributen
* Gegevenssets
* Doelen (Vragen over accounts en sommige vragen over gegevensstroom kunnen op dit moment niet worden beantwoord.)
* Schema&#39;s (vragen over veldgroepen kunnen op dit moment niet worden beantwoord.)
* Segmenten
* Bronnen (Vragen over rekeningen kunnen op dit moment niet worden beantwoord.)

Voor vragen van gebruiksgegevens, kunnen de antwoorden niet op de huidige staat van UI wijzen. De gegevens die deze vragen ondersteunen, worden om de 24 uur bijgewerkt. Zo worden wijzigingen die gebruikers overdag aanbrengen in Real-Time CDP gesynchroniseerd met de gegevensopslag &#39;s nachts, waarna ze &#39;s ochtends beschikbaar komen voor vragen van gebruikers. Mogelijk moet u de vragen opmaken als: &quot;Wanneer was het segment met de titel {TITLE} gemaakt?&quot; in plaats van &quot;Wanneer was het {TITLE} segment gemaakt?&quot;

U moet zich aanmelden bij een sandbox om informatie te krijgen over specifieke gegevens die betrekking hebben op objecten, zoals schema&#39;s, datasets, kenmerken, doelen en segmenten.

### Ondersteunde vragen over gegevensgebruik

+++Selecteren om een lijst met ondersteunde vragen over gegevensgebruik weer te geven

Hieronder volgt een lijst met vragen over het momenteel ondersteunde gegevensgebruik, gegroepeerd op domein.

* De kenmerken weergeven die voor dit segment worden gebruikt?
* Hoeveel segmenten zijn er in totaal?
* Een lijst weergeven met segmenten die de laatste maand zijn gewijzigd.
* Welke segmenten zijn de afgelopen week gewijzigd?
* Wat is het aantal profielen voor {SEGMENT_NAME} segment?
* Alle gedupliceerde segmenten weergeven.
* Toon me segmenten die in afgelopen 7 dagen zijn gemaakt of bijgewerkt.
* Wat is de verdeling van het aantal profielen over segmenten?
* Hoeveel velden worden in segmentatie gebruikt?
* Wat is het totale aantal geactiveerde segmenten?
* Welke segmenten worden geactiveerd?
* Hoeveel dubbele segmenten zijn geactiveerd?
* De segmenten van de lijst die in het laatste jaar werden gecreeerd.
* Segmenten weergeven die het laatst zijn gewijzigd vóór {DATE}.
* Hoeveel unieke segmentnamen zijn gekoppeld aan de {SCHEMA_NAME} schema?
* Welke schema&#39;s het meest meestal over segmenten worden gebruikt?
* Hoeveel schema&#39;s heb ik?
* Welke gegevensset(s) gebruiken {SCHEMA_NAME} schema?
* Alle schema&#39;s weergeven die in de laatste week zijn gewijzigd.
* Hoeveel schema&#39;s worden profiel toegelaten?
* Alle schema&#39;s voor de ervaringsgebeurtenisklasse weergeven?
* Welke datasets in worden opgenomen {SCHEMA_NAME} schema?
* Hoeveel datasets zijn opgenomen gebruikend het zelfde schema?
* Hoeveel datasets heb ik?
* Welke datasets worden gebruikt in elk segment?
* Welke segmenten gebruiken {ATTRIBUTE_NAME} kenmerk?
* Welke schema&#39;s hebben {ATTRIBUTE_NAME} in de eigenschappen?
* Hoeveel XDM schemakenmerken worden niet gebruikt in om het even welke segmenten?
* Waarin gegevensset(s) {ATTRIBUTE_NAME} XDM-velden gevuld?
* Welke datasets gegevens hebben voor {ATTRIBUTE_NAME} kenmerk?
* Hoeveel segmenten worden geactiveerd voor elke bestemming?
* Welke segmenten worden geactiveerd aan het meeste aantal bestemmingen?
* Hebben om het even welke segmenten 0 profielen?
* Hoeveel gegevensstromen heb ik?

+++

### Gesprekkervaring

Bij het opvragen van de AI Assistant moet u rekening houden met verschillende nuances ten aanzien van de beleving van gesprekken.

>[!NOTE]
>
>Deze beperkingen zijn tijdelijk en worden gedurende de gehele alpha verbeterd.

>[!BEGINTABS]

>[!TAB Kan context niet afleiden uit eerdere discussie]

De AI-assistent kan op dit moment niet verwijzen naar eerdere besprekingen als context voor een bepaalde vraag. Zie de onderstaande tabel voor voorbeelden:

| Ambigueuze vraag | Vraag wissen | Opmerking |
| --- | --- | --- |
| <ul><li>Eerste vraag: &quot;Wat is een segment?&quot;</li><li>Vervolgvraag: &quot;Zijn er verschillende soorten?&quot;</li></ul> | <ul><li>Eerste vraag: &quot;Wat is een segment?&quot;</li><li>Vervolgvraag: &quot;Zijn er verschillende soorten **segmenten**?&quot;</li></ul> | De AI-assistent kan niet concluderen wat &quot;zij&quot; betekent. |
| <ul><li>Eerste vraag: &quot;Wat is een segment?&quot;</li><li>Vervolgvraag: &quot;Kan je meer toelichten?&quot;</li></ul> | <ul><li>Eerste vraag: &quot;Wat is een segment?&quot;</li><li>Vervolgvraag: &quot;Uitleggen wat een segment diepgaand is&quot;</li></ul> | De AI Assistant kan op intelligente wijze niet verwijzen naar documentatie die is gebaseerd op &quot;meer&quot;. |
| <ul><li>Eerste vraag: &quot;Wat is een segment?&quot;</li><li>Vervolgvraag: &quot;Kan je me een voorbeeld geven?&quot;</li></ul> | <ul><li>Eerste vraag: &quot;Wat is een segment?&quot;</li><li>Vervolgvraag: &quot;Kan je me een voorbeeld geven van een segment?&quot;</li></ul> | De AI-assistent kan niet bepalen van wat u een voorbeeld wilt. |
| <ul><li>Eerste vraag: &quot;Wat is een batchsegment?&quot;</li><li>Vervolgvraag: &quot;Hoe vergelijk het met een streaming segment?&quot;</li></ul> | <ul><li>Eerste vraag: &quot;Wat is een batchsegment?&quot;</li><li>Vervolgvraag: &quot;Kan u een streaming segment vergelijken met een batch-segment?&quot;</li></ul> | De AI-assistent kan niet concluderen waarnaar &quot;het&quot; verwijst en kan het streamingsegment dus niet vergelijken. |
| <ul><li>Eerste vraag: &quot;Hoeveel segmenten heb ik?&quot;</li><li>Vervolgvraag: &quot;Hoeveel van hen gebruiken Facebook als bestemming?&quot;</li></ul> | <ul><li>Eerste vraag: &quot;Hoeveel segmenten heb ik?&quot;</li><li>Vervolgvraag: &quot;Hoeveel segmenten die ik heb gebruiken Facebook als bestemming?&quot;</li></ul> | De AI-assistent kan niet concluderen waar &quot;zij&quot; naar verwijzen. |

{style="table-layout:auto"}

>[!TAB Kan context niet afleiden van een pagina]

Wanneer u de AI-assistent vraagt naar een bepaald element van de gebruikersinterface van het Experience Platform waarop u zich bevindt, moet u het specifieke element in uw vraag duidelijk definiëren.

| Ambigueuze vraag | Vraag wissen | Opmerking |
| --- | --- | --- |
| Wat doet dit? | &quot;Wat doet {PAGE_NAME} doen? | De AI-assistent kan niet concluderen waar &quot;this&quot; naar verwijst. U moet het specifieke pagina-element opgeven waar u om vraagt. |
| &quot;Waarom zal het niet redden?&quot; | &quot;Waarom kan ik geen nieuwe sandbox opslaan met de naam {NAME}?&quot; | De AI-assistent kan niet concluderen waarnaar &quot;het&quot; verwijst en kan niet weten dat u problemen hebt met een entiteit. |

{style="table-layout:auto"}

Bovendien kan de AI-assistent alleen vragen met betrekking tot foutberichten beantwoorden, aangezien de fout in het Experience League is gedocumenteerd.

>[!TAB dubbelzinnigheid]

U moet uw vragen duidelijk formuleren en deze in een product, toepassing of domein opnemen, aangezien de AI Assistant momenteel geen vragen kan doorgeven.

| Ambigueuze vraag | Vraag wissen | Opmerking |
| --- | --- | --- |
| &quot;Hoe maak ik een filter? | Hoe maak ik een filter in de Taal van de Vraag van het Profiel? | U moet de eigenschap specificeren waarvoor u filtert omdat een verscheidenheid van de eigenschappen van het Experience Platform het filtreren steunt. |
| &quot;Hoe begin ik? | Hoe begin ik met het gebruik van bestemmingen? | U moet duidelijkheid over uw doelstellingen en gebruiksgeval verstrekken omdat de te brede concepten in generische of onnodig specifieke antwoorden kunnen resulteren. |

{style="table-layout:auto"}

>[!ENDTABS]

### Beperkte kleine praatjes

U kunt kleine gesprekken voeren met de AI Assistant, maar deze mogelijkheid is momenteel beperkt.

### Capaciteitsvragen

De AI-assistent kan een onjuiste indruk geven van wat hij kan doen. De volgende typen vragen kunnen onjuist worden beantwoord:

| Voorbeeldvraag | Opmerking |
| --- | --- |
| &quot;Kunt u vragen beantwoorden op {ENTITY}?&quot; | Zolang de AI-assistent in zijn index een enkele pagina kan vinden die naar een bepaalde entiteit verwijst, zal hij ja antwoorden. |
| &quot;Weet je **x** taal?&quot; | De AI Assistant ondersteunt momenteel alleen Engels, maar kan &quot;ja&quot; antwoorden omdat het onderliggende model het ondersteunt. |
| &quot;Kan je...?&quot; | De AI-assistent kan ja antwoorden, ook al is dat niet het geval. |

### Tips

#### De vragen kunnen met de verkeerde informatiebron worden beantwoord

Soms kan een vraag over uw gebruiksgegevens resulteren in een antwoord op basis van de documentatie. Dit komt omdat de AI-assistent uw vraag verkeerd kan doorsturen naar de verkeerde informatiebron. U kunt dit voorkomen door:

* Herhaal uw vraag om meer SQL-achtige taal te gebruiken
* Expliciet het roepen van de informatiebron aan gebruik.

Lees de onderstaande tabel voor voorbeelden:

| Onjuiste vraag | Goede vraag | Notities |
| --- | --- | --- |
| Wat is mijn grootste segment? | Wat is mijn grootste segment? Gegevens gebruiken. | Vertel de AI Assistant expliciet dat het antwoord moet zijn gebaseerd op gegevens. |
| Wat is mijn grootste segment? | Maak een lijst van mijn grootste segment. | Er zijn gevallen waarin een &quot;wat...&quot;-vraag kan worden verward met een documentatiegebaseerde vraag. Het gebruik van een opdracht als &quot;list&quot; is een sterkere indicator die u een vraag stelt met gegevens in context. |
| Hoeveel datasets heb ik? | Tel mijn datasets. | De oorspronkelijke vraag werkt voor segmenten, maar werkt mogelijk niet met gegevenssets. |


