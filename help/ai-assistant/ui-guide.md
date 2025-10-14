---
title: AI Assistant in Adobe Experience Platform
description: Leer hoe u met AI Assistant door Experience Platform- en Real-Time Customer Data Platform-concepten kunt navigeren en deze kunt begrijpen, en hoe u informatie over uw objecten kunt gebruiken.
exl-id: 3fed2b1d-75fc-47ce-98d1-a811eb8a1d8e
source-git-commit: 4fd40d66ecc2fe7604e157fcd230883c6c48d761
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 0%

---

# UI-gids voor AI-assistent

Lees deze handleiding voor meer informatie over het gebruik van AI Assistant in de gebruikersinterface van Adobe Experience Platform.

## AI-assistent openen in de gebruikersinterface van Experience Platform

Als u AI Assistant wilt starten, selecteert u de **[!UICONTROL AI Assistant icon]** in de bovenste koptekst van de gebruikersinterface van Experience Platform.

![&#x200B; de homepage van Experience Platform, met het AI Hulp geselecteerde pictogram en de AI Hulp open interface.](./images/ai-assistant-full-icon.png)

De interface AI Assistant wordt weergegeven en bevat direct informatie die u nodig hebt om aan de slag te gaan. U kunt de opties onder [!UICONTROL Ideas to get started] gebruiken om vragen en opdrachten te beantwoorden, zoals:

* [!UICONTROL Which of my audiences are activated?]
* [!UICONTROL What is a schema?]
* [!UICONTROL Tell me some common use cases for Real-Time CDP]

## Handleiding voor AI Assistant-gebruikersinterface

>[!NOTE]
>
>De volgende workflow is een voorbeeld waarin het proces voor het maken van een ervaringsgebeurtenisschema wordt gebruikt om te laten zien hoe u AI Assistant kunt gebruiken wanneer u de gebruikersinterface van Experience Platform gebruikt.

Overweeg een gebruiksgeval waarin u de Handel van het a **Apparaat in het Schema van de Gebeurtenis** creeert. Tijdens het maken van het gebeurtenisschema komt u tegen het veld `eventType` . &quot;Op dit punt, hebt u de optie om of uw werkschema weg te gaan en naar de [&#x200B; grondbeginselen van een schemacompositie &#x200B;](../xdm/schema/composition.md) documentatie te verwijzen, of u kunt AI Medewerker gebruiken om antwoorden aan uw vragen terug te winnen en extra middelen door de documentatiekoppelingen te vinden die door AI Medewerker worden geadviseerd.&quot;

Om te beginnen voert u uw vraag in het tekstvak in. In het voorbeeld hieronder, wordt AI Medewerker verstrekt de vraag: &quot;**wat het eventType gebied in een schema ExperienceEvent is?**&quot;

![&#x200B; AI Medewerker voor Experience Platform met de volgende vraag die voor het vragen wordt voorbereid: &quot;Wat is het eventType gebied in een schema ExperienceEvent?](./images/question.png)

AI Assistant zoekt vervolgens naar zijn kennisbasis en berekent een antwoord. AI Assistant retourneert na enkele ogenblikken een antwoord en verwante suggesties die u kunt gebruiken als follow-upaanwijzingen.

![&#x200B; AI Medewerker voor Experience Platform met een antwoord op de vorige vraag.](./images/answer.png)

Nadat u een reactie hebt ontvangen van AI Assistant, kunt u een aantal opties selecteren om te bepalen hoe u wilt doorgaan.

### AI Assistant-functies {#features}

In deze sectie worden de verschillende functies van AI Assistant beschreven die u kunt gebruiken tijdens uw workflows op Experience Platform.

### Operationele gegevensobjecten weergeven {#view-operational-data-objects}

Afhankelijk van uw query biedt AI Assistant aanvullende informatie over de gegevens in uw sandbox. Selecteer **[!UICONTROL In your sandbox]als u wilt zien hoe de reactie op uw query op uw specifieke sandbox wordt toegepast.**

Wanneer u gegevens met betrekking tot uw sandbox weergeeft, kan AI Assistant directe koppelingen bevatten naar specifieke UI-pagina&#39;s waarop de gevraagde gegevens worden weergegeven.

+++Selecteren om voorbeeld weer te geven

In dit voorbeeld retourneert AI Assistant aanvullende informatie over de bestaande XDM-schema&#39;s in uw sandbox, inclusief het totale aantal en de vijf meest gebruikte velden.

![&#x200B; &quot;in uw zandbak&quot;dropdown venster open, tonend extra informatie over uw schema&#39;s.](./images/in-your-sandbox.png)

+++

### citaten weergeven {#view-citations}

U kunt antwoorden verifiëren die door AI Assistant aan u zijn geretourneerd door citaten te bekijken die beschikbaar zijn bij elk antwoord op de productkennis.

+++ selecteren om een voorbeeld te bekijken van hoe te om bronnen te tonen

Selecteer **[!UICONTROL Show sources]** als u citaties wilt weergeven en de reactie van AI Assistant wilt valideren.

![&#x200B; de AI Hulp reactie met &quot;toont geselecteerde bronnen&quot;.](./images/show-sources.png)

AI Assistant werkt de interface bij en biedt koppelingen naar documentatie die de eerste reactie bevestigen. Wanneer citaties zijn ingeschakeld, werkt AI Assistant het antwoord bij en worden voetnoten opgenomen om de specifieke delen van het antwoord aan te geven die naar de opgegeven documentatie verwijzen.

![&#x200B; drop-down menu van A van de citaties die AI Medewerker voor conceptenvragen verstrekt.](./images/citations.png)

+++

### Operationele inzichten {#operational-insights}

AI Assistant moet zich in een actieve sandbox bevinden om voldoende te kunnen reageren op een vraag over uw operationele inzichten.

+++Selecteer om een voorbeeld van een vraag over operationele inzichten te bekijken

In het voorbeeld hieronder, wordt AI Medewerker gevraagd de volgende vraag: **&quot;toon me dataflows die gebruikend de bron van Amazon S3 werden gecreeerd&quot;**.

![&#x200B; een vraag over operationele inzichten.](./images/op-insights-question.png)

AI Assistant reageert vervolgens met een tabel waarin uw gegevens en de bijbehorende id&#39;s worden vermeld. Selecteer het downloadpictogram (![&#x200B; pictogram van de Download &#x200B;](/help/images/icons/download.png)) om de lijst als Csv- dossier te downloaden. Om de volledige lijst te bekijken, selecteer uitvouwen pictogram (![&#x200B; breid pictogram &#x200B;](/help/images/icons/expand.png) uit).

![&#x200B; een operationeel inzicht antwoord &#x200B;](./images/op-insights-answer.png)

Er wordt een uitgebreide weergave van de tabel weergegeven, zodat u een uitgebreidere lijst met gegevensstromen krijgt op basis van de parameters van de query.

![&#x200B; een mening van de uitgebreide lijst.](./images/table.png)

Als deze wordt gevraagd om een vraag over operationele inzichten, geeft AI Assistant een uitleg van de manier waarop het antwoord is berekend. In het onderstaande voorbeeld geeft AI Assistant een overzicht van de stappen die zijn uitgevoerd om de gegevensstromen te identificeren die zijn gemaakt met de bron [!DNL Amazon S3] .

![&#x200B; AI Medewerker die een verklaring op verstrekt hoe het zijn antwoord gegevens verwerkt.](./images/answer-explained.png)

U kunt ook filters en wijzigingen in uw vragen opgeven en u kunt de AI Assistant de opdracht geven zijn bevindingen te genereren op basis van de filters die u opneemt. Bijvoorbeeld, kunt u AI Medewerker vragen om u een trend van de telling van segmentdefinities in de orde van hun gecreeerde datum te tonen, segmentdefinities met nul totale profielen te verwijderen, en maandnamen in plaats van gehelen te gebruiken wanneer het tonen van de gegevens.

+++

### Reacties met operationele inzichten controleren {#verify-responses}

U kunt elke reactie met betrekking tot operationele vragen van inzichten verifiëren gebruikend een SQL vraag die AI Medewerker verstrekt.

+++Selecteren om een voorbeeld weer te geven van het controleren van reacties op operationele inzichten

Nadat u een antwoord voor een vraag over operationele inzichten hebt ontvangen, selecteert u **[!UICONTROL Show sources]** en selecteert u vervolgens **[!UICONTROL View source query]** .

![&#x200B; vraag van de meningsbron &#x200B;](./images/view-source-query.png)

Wanneer gevraagd met een operationele inzichten vraag, verstrekt AI Assistant een SQL vraag die u kunt gebruiken om het proces te verifiëren dat het nam om zijn antwoord te berekenen. Deze bronvraag is slechts voor verificatiedoeleinden en wordt niet gesteund op de Dienst van de Vraag.

![&#x200B; voorbeeld van bronvraag &#x200B;](./images/source-query.png)

+++

### Entiteiten automatisch aanvullen {#use-entity-auto-complete}

Met de functie Automatisch aanvullen kunt u een lijst met gegevensobjecten ontvangen die in uw sandbox staan. Er zijn aanbevelingen voor automatisch aanvullen beschikbaar voor de volgende domeinen: publiek, schema&#39;s, datasets, reizen, bronnen en bestemmingen.

+++Select om een voorbeeld van automatisch aanvullen te bekijken

U kunt autocomplete gebruiken door het plusteken (**`+`**) in uw vraag te omvatten. U kunt ook het plusteken (**`+`**) onder aan het tekstinvoervak selecteren. Er wordt een venster weergegeven met een lijst met aanbevolen gegevensobjecten uit uw sandbox.

![&#x200B; Voorbeeld van auto-volledig &#x200B;](./images/autocomplete.png)

+++

### Meerdere keren gebruiken {#use-multi-turn}

U kunt de multi-boommogelijkheden van AI Medewerker gebruiken om een natuurlijker gesprek tijdens uw ervaring te hebben. AI Assistant kan vervolgvragen beantwoorden. die context kan worden afgeleid uit een eerdere interactie.

+++Selecteren om een voorbeeld van meerdere keren te bekijken

In het onderstaande voorbeeld wordt AI Assistant eerst gevraagd naar het totale aantal gegevensstromen en wordt vervolgens gevraagd de 10 meest recente gegevensstromen weer te geven.

![&#x200B; Voorbeeld van multi-draai &#x200B;](./images/multiturn.png)

+++

### Een nieuw gesprek starten

U kunt onderwerpen met AI Medewerker veranderen door opnieuw in te stellen en een nieuw gesprek te beginnen.

+++Select om een voorbeeld te bekijken van het terugstellen van uw gesprek

Om terug te stellen, selecteer de ellipsen (**`...`**) op de interface AI van de Medewerker en selecteer dan **[!UICONTROL Start new conversation]**. Dit informeert AI Medewerker dat u op veranderende onderwerpen van plan bent en kan bijzonder nuttig zijn wanneer het oplossen van problemenvragen die of ontbreken of van verwijzingen voorzien onjuiste informatie.

![&#x200B; de ellipsen selecteerden en de begin nieuwe geselecteerde gespreksoptie.](./images/reset.png)

+++

### Detectie gebruiken {#use-discoverability}

U kunt de ontdekkingsfunctie van AI Assistant gebruiken om een lijst weer te geven met algemene onderwerpen, gegroepeerd in entiteiten, die door AI Assistant worden ondersteund.

+++Selecteren om voorbeelden van ontdekkingsmogelijkheden weer te geven

Selecteer het pictogram met de gloeilamp in de bovenste koptekst van de AI Assistant-interface om de ontdekkingsmogelijkheden weer te geven.

![&#x200B; De AI Hulp ontdekkingseigenschap.](./images/lightbulb.png)

Selecteer vervolgens een categorie en selecteer vervolgens een vraag in de opgegeven lijst. U kunt deze functie gebruiken om een beter idee te krijgen van de typen vragen die AI Assistant kan beantwoorden. U kunt de reeds bestaande herinneringen met specifieke details ook bijwerken die tot uw zandbak gebruikend vrije tekst of [&#x200B; autocomplete &#x200B;](#use-auto-complete) behoren.

![&#x200B; de Hulp AI herinneringen in ontdekkingsbaarheid.](./images/prompt.png)

+++

### Vraag automatisch aanvullen {#use-question-autocomplete}

Met de functie voor automatisch aanvullen van vragen van AI Assistant kunt u een vraag selecteren in een lijst met aanbevelingen van AI Assistant.

+++Selecteren om een voorbeeld weer te geven van een vraag die automatisch is voltooid

Als u het deelvenster met voorgestelde vragen wilt weergeven, typt u ten minste 7 (7) tekens in het invoervak. Selecteer vervolgens de vraag die voor u relevant is in het menu dat wordt weergegeven.

![&#x200B; het pop-up paneel met voorgestelde vragen van AI Medewerker.](./images/suggested_questions.png)

Mogelijk moet u tijdelijke aanduidingen bijwerken in sommige gevallen waarin een voorgestelde vraag betrekking heeft op operationele inzichten. U moet bijvoorbeeld mogelijk de specifieke naam van een gegevensset of een publiek toevoegen als de suggestie van AI Assistant plaatsaanduidingen bevat.

![&#x200B; een suggestie van AI Medewerker die placeholders omvat.](./images/placeholder.png)

Plaatsaanduidingen worden in blauw gemarkeerd. Selecteer de tijdelijke aanduiding om de waarde ervan bij te werken. Voor de beste resultaten bij numerieke plaatsaanduidingen moet u ervoor zorgen dat u cijfers in plaats van tekst gebruikt. U kunt ook de functie voor automatisch aanvullen van de entiteit gebruiken om de waarden van de plaatsaanduiding bij te werken. U kunt geen vraag verzenden die niet-ingevulde plaatsaanduidingen heeft.

**NOTA**: De suggesties worden toegelaten door gebrek. Selecteer de schakeloptie **[!UICONTROL Suggest ideas]** om de functie uit te schakelen.

![&#x200B; een suggestie van AI Medewerker met bijgewerkte placeholders.](./images/updated_placeholder.png)

+++

### Verwante suggesties gebruiken {#use-related-suggestions}

U kunt de verwante suggesties sectie van elke AI Hulp- reactie gebruiken om uw gesprek voort te zetten.

+++Selecteren om voorbeeld van verwante suggesties weer te geven

Verwante suggesties worden geretourneerd bij elke reactie van AI Assistant. Om uw gesprek voort te zetten, selecteer om het even welke suggesties in de verwante suggesties sectie.

![&#x200B; een lijst van verwante suggesties van AI Medewerker.](./images/related_suggestions.png)

Net als voor plaatsaanduidingen in kwestie die automatisch zijn voltooid, moet u plaatsaanduidingen bijwerken die zijn opgenomen in verwante suggesties voordat u de query kunt verzenden.

![&#x200B; een vraag van verwante suggesties met bijgewerkte placeholders.](./images/related_suggestions_placeholder.png)

+++

## Feedback geven {#feedback}

U kunt feedback over uw ervaringen met AI Assistant opgeven met de opties die bij het antwoord worden geleverd.

Als u feedback wilt opgeven, selecteert u duimen omhoog, duimen omlaag of een markering nadat u een reactie van de AI-assistent hebt ontvangen. Vervolgens voert u uw feedback in het opgegeven tekstvak in.

![&#x200B; terugkoppelt optie in AI Medewerker.](./images/provide-feedback.png)

+++Selecteren om meer voorbeelden weer te geven

>[!BEGINTABS]

>[!TAB  duimen omhoog ]

Selecteer het pictogram van duim op om feedback te geven over wat goed met uw ervaring met de AI Assistant is gegaan.

![&#x200B; positieve terugkoppelt venster.](./images/thumbs-up.png)

>[!TAB  duimen neer ]

Selecteer het pictogram met de miniaturen omlaag om feedback te geven over de verbeteringen die u kunt aanbrengen op basis van uw ervaring met de AI Assistant. Tijdens deze stap kunt u ook specifieke opmerkingen maken over uw ervaring. De feedback in de opmerkingen wordt dagelijks bekeken.

![&#x200B; negatief terugkoppelt venster.](./images/thumbs-down.png)

>[!TAB  Vlag ]

Selecteer het vlagpictogram om verdere rapporten over uw ervaring te verstrekken gebruikend de Medewerker AI.

![&#x200B; het venster van de rapportresultaten.](./images/flag.png)

>[!ENDTABS]

+++
