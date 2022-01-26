---
keywords: Experience Platform;home;populaire onderwerpen;streaming;cloudopslagaansluiting;cloudopslag
solution: Experience Platform
title: Een streaminggegevensstroom maken voor een bron voor cloudopslag in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Een dataflow is een geplande taak die gegevens van een bron aan een dataset van de Platform terugwint en opneemt. Deze zelfstudie bevat stappen voor het configureren van een nieuwe gegevensstroom met behulp van de basisaansluiting voor cloudopslag.
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
source-git-commit: 38f64f2ba0b40a20528aac6efff0e2fd6bc12ed2
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# Een streaminggegevensstroom maken voor een bron voor cloudopslag in de gebruikersinterface

Een dataflow is een geplande taak die gegevens van een bron aan een dataset van Adobe Experience Platform terugwint en opneemt. Deze zelfstudie bevat stappen voor het maken van een streaminggegevensstroom voor een bron voor cloudopslag in de gebruikersinterface.

Voordat u deze zelfstudie kunt proberen, moet u eerst een geldige en geverifieerde verbinding tot stand brengen tussen uw account voor cloudopslag en uw Platform. Als u nog geen geverifieerde verbinding hebt, raadpleegt u een van de volgende zelfstudies voor informatie over het verifiëren van uw streaming cloudopslagaccounts:

- [[!DNL Amazon Kinesis]](../../../ui/create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../../../ui/create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../../../ui/create/cloud-storage/google-pubsub.md)

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [Gegevensstromen](../../../../../dataflows/home.md): Dataflows zijn een voorstelling van gegevenstaken die gegevens over het Platform verplaatsen. Dataflows worden geconfigureerd op verschillende services, van bronnen tot [!DNL Identity Service], naar [!DNL Profile]en [!DNL Destinations].
- [Gegevensprep](../../../../../data-prep/home.md): Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model). De Prep van gegevens verschijnt als &quot;Kaart&quot;stap in de processen van de Ingestie van Gegevens, met inbegrip van CSV Ingestiewerkschema.
- [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## Gegevens toevoegen

Nadat u uw account voor streaming cloud storage hebt gemaakt, kunt u **[!UICONTROL Select data]** wordt weergegeven, zodat u een interface hebt waarmee u kunt selecteren welke gegevensstroom u naar het Platform wilt brengen.

- Het linkergedeelte van de interface is een browser waarmee u de beschikbare gegevensstromen binnen uw account kunt bekijken.
- In het rechtergedeelte van de interface kunt u maximaal 100 rijen gegevens uit een JSON-bestand voorvertonen.

![interface](../../../../images/tutorials/dataflow/cloud-storage/streaming/interface.png)

Selecteer de gegevensstroom die u wilt gebruiken, en selecteer dan **[!UICONTROL Choose file]** om een voorbeeldschema te uploaden.

>[!TIP]
>
>Als uw gegevens compatibel zijn met XDM, kunt u het uploaden van een voorbeeldschema overslaan en **[!UICONTROL Next]** om verder te gaan.

![select-stream](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-stream.png)

Zodra uw schema uploadt, werkt de voorproefinterface bij om een voorproef van het schema te tonen u uploadde. Met de voorvertoningsinterface kunt u de inhoud en structuur van een bestand controleren. U kunt ook de opdracht [!UICONTROL Search field] nut om tot specifieke punten van binnen uw schema toegang te hebben.

Als u klaar bent, selecteert u **[!UICONTROL Next]**.

![schemavoorvertoning](../../../../images/tutorials/dataflow/cloud-storage/streaming/schema-preview.png)

## Toewijzing

De **[!UICONTROL Mapping]** stap verschijnt, verstrekkend een interface om de brongegevens aan een dataset van het Platform in kaart te brengen.

Kies een dataset voor binnenkomende gegevens waarin moeten worden opgenomen. U kunt of een bestaande dataset gebruiken of nieuwe creëren.

### Nieuwe gegevensset

Om gegevens in een nieuwe dataset in te voeren, selecteer **[!UICONTROL New dataset]** en voert een naam en een beschrijving voor de gegevensset in de opgegeven velden in. Als u een schema wilt toevoegen, kunt u een bestaande schemanaam invoeren in het dialoogvenster **[!UICONTROL Select schema]** in. U kunt ook **[!UICONTROL Schema advanced search]** naar een geschikt schema zoeken.

![new-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-dataset.png)

De [!UICONTROL Select schema] wordt weergegeven, zodat u een lijst met beschikbare schema&#39;s kunt kiezen. Selecteer een schema in de lijst om het rechterspoor bij te werken om details te tonen specifiek voor het schema u selecteerde, met inbegrip van informatie over of het schema wordt toegelaten voor [!DNL Profile].

Als u het schema hebt geïdentificeerd en geselecteerd dat u wilt gebruiken, selecteert u **[!UICONTROL Done]**.

![selectieschema](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-schema.png)

De [!UICONTROL Target dataset] de pagina werkt met uw geselecteerd schema dat als deel van de dataset wordt getoond bij. Tijdens deze stap, kunt u uw dataset voor toelaten [!DNL Profile] en een holistische weergave te maken van de kenmerken en gedragingen van een entiteit. Gegevens van alle ingeschakelde gegevenssets worden opgenomen in [!DNL Profile] en wijzigingen worden toegepast wanneer u de gegevensstroom opslaat.

Schakelen tussen **[!UICONTROL Profile dataset]** knoop om uw doeldataset voor toe te laten [!DNL Profile].

![nieuw profiel](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-profile.png)

### Bestaande gegevensset

Om gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Existing dataset]** selecteert u vervolgens het pictogram voor de gegevensset.

![bestaande gegevensset](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-dataset.png)

De **[!UICONTROL Select dataset]** wordt weergegeven, op basis waarvan u een lijst met beschikbare gegevenssets kunt kiezen. Selecteer een dataset van de lijst om de juiste spoorstaaf bij te werken om details te tonen specifiek voor de dataset u selecteerde, met inbegrip van informatie over of de dataset kan worden toegelaten voor [!DNL Profile].

Nadat u de gegevensset hebt geïdentificeerd en geselecteerd die u wilt gebruiken, selecteert u **[!UICONTROL Done]**.

![select-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-dataset.png)

Nadat u de gegevensset hebt geselecteerd, selecteert u de [!DNL Profile] schakelen om uw gegevensset in te schakelen voor [!DNL Profile].

![bestaand profiel](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-profile.png)

### Standaardvelden toewijzen

Als uw dataset en schema worden gevestigd, **[!UICONTROL Map standard fields]** wordt weergegeven, zodat u handmatig toewijzingsvelden voor uw gegevens kunt configureren.

>[!TIP]
>
>Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen.

Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie [UI-hulplijn voor gegevensvoorinstelling](../../../../../data-prep/ui/mapping.md).

Selecteer **[!UICONTROL Next]**.

![toewijzing](../../../../images/tutorials/dataflow/cloud-storage/streaming/mapping.png)

## Gegevens

De **[!UICONTROL Dataflow detail]** wordt weergegeven, zodat u een naam kunt geven en een korte beschrijving kunt geven van uw nieuwe gegevensstroom.

Geef waarden op voor de gegevensstroom en selecteer **[!UICONTROL Next]**.

![dataFlow-detail](../../../../images/tutorials/dataflow/cloud-storage/streaming/dataflow-detail.png)

### Controleren

De **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

- **[!UICONTROL Connection]**: Hiermee geeft u de naam van uw account, het type bron en andere informatie weer die specifiek is voor de streamingbron voor cloudopslag die u gebruikt.
- **[!UICONTROL Assign dataset and map fields]**: Toont de doeldataset en het schema u voor uw gegevensstroom gebruikt.

Nadat u de gegevensstroom hebt gecontroleerd, selecteert u **[!UICONTROL Finish]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

![revisie](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Uw gegevensstroom controleren en verwijderen

Nadat u de gegevens voor de streaming cloud storage hebt gemaakt, kunt u de gegevens controleren die er doorheen worden ingevoerd. Raadpleeg de zelfstudie voor meer informatie over het controleren en verwijderen van streaming dataflows [streaming gegevens controleren](../../monitor-streaming.md).

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een gegevensstroom gemaakt om gegevens van een bron voor cloudopslag te streamen. Inkomende gegevens kunnen nu worden gebruikt door downstreamdiensten voor Platforms, zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

- [[!DNL Real-time Customer Profile] - overzicht](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] - overzicht](../../../../../data-science-workspace/home.md)