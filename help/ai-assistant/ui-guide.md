---
title: AI Assistant in Adobe Experience Platform
description: Leer hoe u met AI Assistant door Experience Platform- en Real-time Customer Data Platform-concepten kunt navigeren en deze kunt begrijpen, en hoe u informatie over uw objecten kunt gebruiken.
exl-id: 3fed2b1d-75fc-47ce-98d1-a811eb8a1d8e
source-git-commit: 94245fe25828025b60ea57ddebede2b3ccf890eb
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 0%

---

# UI-gids voor AI-assistent

Lees deze handleiding voor meer informatie over het gebruik van AI Assistant in de gebruikersinterface van Adobe Experience Platform.

De volgende video is bedoeld als ondersteuning voor uw begrip van AI Assistant.

>[!VIDEO](https://video.tv.adobe.com/v/3429845?learn=on)

## De Hulp van AI van de toegang in de UI van het Experience Platform

Als u AI Assistant wilt starten, selecteert u de **[!UICONTROL AI Assistant icon]** in de bovenste koptekst van de gebruikersinterface van het Experience Platform.

![ de homepage van het Experience Platform, met het AI Hulp geselecteerde pictogram en de AI Hulp open interface.](./images/ai-assistant-full-icon.png)

De interface AI Assistant wordt weergegeven en bevat direct informatie die u nodig hebt om aan de slag te gaan. U kunt de opties onder [!UICONTROL Ideas to get started] gebruiken om vragen en opdrachten te beantwoorden, zoals:

* [!UICONTROL Which of my audiences are activated?]
* [!UICONTROL What is a schema?]
* [!UICONTROL Tell me some common use cases for Real-Time CDP]

## Handleiding voor AI Assistant-gebruikersinterface

>[!NOTE]
>
>De volgende workflow is een voorbeeld waarin het proces voor het maken van een ervaringsgebeurtenisschema wordt gebruikt om te laten zien hoe u AI Assistant kunt gebruiken wanneer u de gebruikersinterface van het Experience Platform gebruikt.

Overweeg een gebruiksgeval waarin u de Handel van het a **Apparaat in het Schema van de Gebeurtenis** creeert. Tijdens het maken van het gebeurtenisschema komt u tegen het veld `eventType` . &quot;Op dit punt, hebt u de optie om of uw werkschema weg te gaan en naar de [ grondbeginselen van een schemacompositie ](../xdm/schema/composition.md) documentatie te verwijzen, of u kunt AI Medewerker gebruiken om antwoorden aan uw vragen terug te winnen en extra middelen door de documentatiekoppelingen te vinden die door AI Medewerker worden geadviseerd.&quot;

Om te beginnen voert u uw vraag in het tekstvak in. In het voorbeeld hieronder, wordt AI Medewerker verstrekt de vraag: &quot;**wat het eventType gebied in een schema ExperienceEvent is?**&quot;

![ AI Medewerker voor Experience Platform met de volgende vraag die voor het vragen wordt voorbereid: &quot;Wat is het eventType gebied in een schema ExperienceEvent?](./images/question.png)

AI Assistant zoekt vervolgens naar zijn kennisbasis en berekent een antwoord. AI Assistant retourneert na enkele ogenblikken een antwoord en verwante suggesties die u kunt gebruiken als follow-upaanwijzingen.

![ AI Medewerker voor Experience Platform met een antwoord op de vorige vraag.](./images/answer.png)

Nadat u een reactie hebt ontvangen van AI Assistant, kunt u een aantal opties selecteren om te bepalen hoe u wilt doorgaan.

### AI Assistant-functies {#features}

In deze sectie worden de verschillende functies van AI Assistant beschreven die u kunt gebruiken tijdens uw workflows op het Experience Platform.

### Operationele gegevensobjecten weergeven {#view-operational-data-objects}

Afhankelijk van uw query biedt AI Assistant aanvullende informatie over de gegevens in uw sandbox. Selecteer **[!UICONTROL In your sandbox]als u wilt zien hoe de reactie op uw query op uw specifieke sandbox wordt toegepast.**

Wanneer u gegevens met betrekking tot uw sandbox weergeeft, kan AI Assistant directe koppelingen bevatten naar specifieke UI-pagina&#39;s waarop de gevraagde gegevens worden weergegeven.

+++Selecteren om voorbeeld weer te geven

In dit voorbeeld retourneert AI Assistant aanvullende informatie over de bestaande XDM-schema&#39;s in uw sandbox, inclusief het totale aantal en de vijf meest gebruikte velden.

![ &quot;in uw zandbak&quot;dropdown venster open, tonend extra informatie over uw schema&#39;s.](./images/in-your-sandbox.png)

+++

### citaten weergeven {#view-citations}

U kunt antwoorden verifiëren die door AI Assistant aan u zijn geretourneerd door citaten te bekijken die beschikbaar zijn bij elk antwoord op de productkennis.

++ + selecteren om een voorbeeld te bekijken van hoe te om bronnen te tonen

Selecteer **[!UICONTROL Show sources]** als u citaties wilt weergeven en de reactie van AI Assistant wilt valideren.

![ de AI Hulp reactie met &quot;toont geselecteerde bronnen&quot;.](./images/show-sources.png)

AI Assistant werkt de interface bij en biedt koppelingen naar documentatie die de eerste reactie bevestigen. Wanneer citaties zijn ingeschakeld, werkt AI Assistant het antwoord bij en worden voetnoten opgenomen om de specifieke delen van het antwoord aan te geven die naar de opgegeven documentatie verwijzen.

![ drop-down menu van A van de citaties die AI Medewerker voor conceptenvragen verstrekt.](./images/citations.png)

U kunt ook de suggesties die AI Assistant onder **[!UICONTROL Related suggestions]** biedt, gebruiken om verder te zoeken naar onderwerpen die betrekking hebben op uw oorspronkelijke vraag.

![ een lijst van suggesties die door AI Medewerker worden verstrekt.](./images/related-suggestions.png)

+++

### Operationele inzichten {#operational-insights}

AI Assistant moet zich in een actieve sandbox bevinden om voldoende te kunnen reageren op een vraag over uw operationele inzichten.

+++Selecteer om een voorbeeld van een vraag over operationele inzichten te bekijken

In het voorbeeld hieronder, wordt AI Medewerker gevraagd de volgende vraag: **&quot;toon me dataflows die gebruikend de bron van Amazon S3 werden gecreeerd&quot;**.

![ een vraag over operationele inzichten.](./images/op-insights-question.png)

AI Assistant reageert vervolgens met een tabel waarin uw gegevens en de bijbehorende id&#39;s worden vermeld. Als u de hele tabel met gegevens wilt weergeven, selecteert u het pictogram voor uitvouwen rechtsboven.

![ een operationeel inzicht antwoord ](./images/op-insights-answer.png)

Er wordt een uitgebreide weergave van de tabel weergegeven, zodat u een uitgebreidere lijst met gegevensstromen krijgt op basis van de parameters van de query.

![ een mening van de uitgebreide lijst.](./images/table.png)

Als deze wordt gevraagd om een vraag over operationele inzichten, geeft AI Assistant een uitleg van de manier waarop het antwoord is berekend. In het onderstaande voorbeeld geeft AI Assistant een overzicht van de stappen die zijn uitgevoerd om de gegevensstromen te identificeren die zijn gemaakt met de bron [!DNL Amazon S3] .

![ AI Medewerker die een verklaring op verstrekt hoe het zijn antwoord gegevens verwerkt.](./images/answer-explained.png)

U kunt ook filters en wijzigingen in uw vragen opgeven en u kunt de AI Assistant de opdracht geven zijn bevindingen te genereren op basis van de filters die u opneemt. Bijvoorbeeld, kunt u AI Medewerker vragen om u een trend van de telling van segmentdefinities in de orde van hun gecreeerde datum te tonen, segmentdefinities met nul totale profielen te verwijderen, en maandnamen in plaats van gehelen te gebruiken wanneer het tonen van de gegevens.

**Nota:** De operationele inzichten antwoorden zijn momenteel in bèta. Selecteer het knopinfo-pictogram in de gebruikersinterface van de AI-assistent om de Beta-kennisgeving weer te geven en voor een koppeling naar de documentatie.

![ AI Hulp geselecteerd tooltip pictogram.](./images/op-insights-beta-note.png)

+++

### Reacties met operationele inzichten controleren {#verify-responses}

U kunt elke reactie met betrekking tot operationele vragen van inzichten verifiëren gebruikend een SQL vraag die AI Medewerker verstrekt.

+++Selecteren om een voorbeeld weer te geven van het controleren van reacties op operationele inzichten

Nadat u een antwoord voor een vraag over operationele inzichten hebt ontvangen, selecteert u **[!UICONTROL Show sources]** en selecteert u vervolgens **[!UICONTROL View source query]** .

![ vraag van de meningsbron ](./images/view-source-query.png)

Wanneer gevraagd met een operationele inzichten vraag, verstrekt AI Assistant een SQL vraag die u kunt gebruiken om het proces te verifiëren dat het nam om zijn antwoord te berekenen. Deze bronvraag is slechts voor verificatiedoeleinden en wordt niet gesteund op de Dienst van de Vraag.

![ voorbeeld van bronvraag ](./images/source-query.png)

+++

### Automatisch aanvullen gebruiken {#use-auto-complete}

Met de functie Automatisch aanvullen kunt u een lijst met gegevensobjecten ontvangen die in uw sandbox staan. De aanbevelingen van Autocomplete zijn beschikbaar voor de volgende domeinen: publiek, schema&#39;s, datasets, bronnen, en bestemmingen.

+++Select om een voorbeeld van automatisch aanvullen te bekijken

U kunt autocomplete gebruiken door het plusteken (**`+`**) in uw vraag te omvatten. U kunt ook het plusteken (**`+`**) onder aan het tekstinvoervak selecteren. Er wordt een venster weergegeven met een lijst met aanbevolen gegevensobjecten uit uw sandbox.

![ Voorbeeld van auto-volledig ](./images/autocomplete.png)

+++

### Meerdere keren gebruiken {#use-multi-turn}

U kunt de multi-boommogelijkheden van AI Medewerker gebruiken om een natuurlijker gesprek tijdens uw ervaring te hebben. AI Assistant kan vervolgvragen beantwoorden. die context kan worden afgeleid uit een eerdere interactie.

+++Selecteren om een voorbeeld van meerdere keren te bekijken

In het onderstaande voorbeeld wordt AI Assistant eerst gevraagd naar het totale aantal gegevensstromen en wordt vervolgens gevraagd de 10 meest recente gegevensstromen weer te geven.

![ Voorbeeld van multi-draai ](./images/multiturn.png)

+++

### Een nieuw gesprek starten

U kunt onderwerpen met AI Medewerker veranderen door opnieuw in te stellen en een nieuw gesprek te beginnen.

+++Select om een voorbeeld te bekijken van het terugstellen van uw gesprek

Om terug te stellen, selecteer de ellipsen (**`...`**) op de interface AI van de Medewerker en selecteer dan **[!UICONTROL Start new conversation]**. Dit informeert AI Medewerker dat u op veranderende onderwerpen van plan bent en kan bijzonder nuttig zijn wanneer het oplossen van problemenvragen die of ontbreken of van verwijzingen voorzien onjuiste informatie.

![ de ellipsen selecteerden en de begin nieuwe geselecteerde gespreksoptie.](./images/reset.png)

+++

### Detectie gebruiken {#use-discoverability}

U kunt de ontdekkingsfunctie van AI Assistant gebruiken om een lijst weer te geven met algemene onderwerpen, gegroepeerd in entiteiten, die door AI Assistant worden ondersteund.

+++Selecteren om voorbeelden van ontdekkingsmogelijkheden weer te geven

Selecteer het pictogram met de gloeilamp in de bovenste koptekst van de AI Assistant-interface om de ontdekkingsmogelijkheden weer te geven.

![ De AI Hulp ontdekkingseigenschap.](./images/lightbulb.png)

Selecteer vervolgens een categorie en selecteer vervolgens een vraag in de opgegeven lijst. U kunt deze functie gebruiken om een beter idee te krijgen van de typen vragen die AI Assistant kan beantwoorden. U kunt de reeds bestaande herinneringen met specifieke details ook bijwerken die tot uw zandbak gebruikend vrije tekst of [ autocomplete ](#use-auto-complete) behoren.

![ de Hulp AI herinneringen in ontdekkingsbaarheid.](./images/prompt.png)

+++

## Feedback geven {#feedback}

U kunt feedback over uw ervaringen met AI Assistant opgeven met de opties die bij het antwoord worden geleverd.

Als u feedback wilt opgeven, selecteert u duimen omhoog, duimen omlaag of een markering nadat u een reactie van de AI-assistent hebt ontvangen. Vervolgens voert u uw feedback in het opgegeven tekstvak in.

![ terugkoppelt optie in AI Medewerker.](./images/provide-feedback.png)

+++Selecteren om meer voorbeelden weer te geven

>[!BEGINTABS]

>[!TAB  duimen omhoog ]

Selecteer het pictogram van duim op om feedback te geven over wat goed met uw ervaring met de AI Assistant is gegaan.

![ positieve terugkoppelt venster.](./images/thumbs-up.png)

>[!TAB  duimen neer ]

Selecteer het pictogram met de miniaturen omlaag om feedback te geven over de verbeteringen die u kunt aanbrengen op basis van uw ervaring met de AI Assistant. Tijdens deze stap kunt u ook specifieke opmerkingen maken over uw ervaring. De feedback in de opmerkingen wordt dagelijks bekeken.

![ negatief terugkoppelt venster.](./images/thumbs-down.png)

>[!TAB  Vlag ]

Selecteer het vlagpictogram om verdere rapporten over uw ervaring te verstrekken gebruikend de Medewerker AI.

![ het venster van de rapportresultaten.](./images/flag.png)

>[!ENDTABS]

+++
