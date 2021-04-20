---
keywords: Experience Platform;home;populaire onderwerpen;streamingverbinding;maak streamingverbinding;ui-handleiding;zelfstudie;maak een streamingverbinding;streaming opname;opname;
solution: Experience Platform
title: Een streamingverbinding maken met de gebruikersinterface
topic: zelfstudie
type: Tutorial
description: Deze UI-handleiding helpt u bij het maken van een streamingverbinding met Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
translation-type: tm+mt
source-git-commit: 3b71f1399a770e097cf75827e626d6d4e289ab77
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---


# Een streamingverbinding maken met de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een streamingbronverbinding met de werkruimte [!UICONTROL Sources].

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## Een streamingverbinding maken

Selecteer **[!UICONTROL Sources]** in de gebruikersinterface van het Platform in de linkernavigatie om de werkruimte [!UICONTROL Sources] te openen. In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL Streaming]** onder de categorie **[!UICONTROL HTTP API]** en selecteer **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/http/catalog.png)

De pagina **[!UICONTROL Connect HTTP API account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de HTTP API-account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![bestaande rekening](../../../../images/tutorials/create/http/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]**. Geef in het invoerformulier dat wordt weergegeven een accountnaam en een optionele beschrijving op. U zult ook de optie krijgen om de volgende configuratieeigenschappen te verstrekken:

- **[!UICONTROL Authentication]:** This property determines whether or not the streaming connection requires authentication. Verificatie zorgt ervoor dat gegevens worden verzameld van vertrouwde bronnen. Als u met Persoonlijk Identificeerbare Informatie (PII) werkt, zou dit bezit moeten worden aangezet. Deze eigenschap is standaard uitgeschakeld.
- **[!UICONTROL XDM compatible]:** Deze eigenschap geeft aan of deze streamingverbinding gebeurtenissen verzendt die compatibel zijn met XDM-schema&#39;s. Deze eigenschap is standaard uitgeschakeld.

Wanneer gebeëindigd, selecteer **[!UICONTROL Connect to source]** en selecteer dan **[!UICONTROL Next]** om te werk te gaan.

![nieuwe rekening](../../../../images/tutorials/create/http/new.png)

## Gegevens selecteren

Nadat u de HTTP API-verbinding hebt gemaakt, wordt de stap **[!UICONTROL Select data]** weergegeven, waarmee u een interface krijgt voor het uploaden en voorvertonen van uw gegevens.

Selecteer **[!UICONTROL Upload files]** om uw gegevens te uploaden. U kunt uw gegevens ook naar de sectie [!UICONTROL Drag and drop files] van de interface slepen.

![add-data](../../../../images/tutorials/create/http/add-data.png)

Als uw gegevens zijn geüpload, kunt u de rechterkant van de interface gebruiken om een voorvertoning van de bestandshiërarchie weer te geven. Selecteer **[!UICONTROL Next]** om door te gaan.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## Gegevensvelden toewijzen aan een XDM-schema

De stap [!UICONTROL Mapping] verschijnt, die een interface verstrekken om de brongegevens aan een dataset van het Platform in kaart te brengen.

De dossiers van het Parket moeten XDM volgzaam zijn en vereisen u niet om de afbeelding manueel te vormen, terwijl de Csv- dossiers u vereisen om de afbeelding uitdrukkelijk te vormen, maar u toe te staan om te kiezen welke brongegevensgebieden aan kaart te brengen. Voor JSON-bestanden die als XDM-klacht zijn gemarkeerd, is geen handmatige configuratie vereist. Nochtans, als het niet duidelijk als volgzaam XDM is, zal het u vereisen om de afbeelding uitdrukkelijk te vormen.

Kies een dataset voor binnenkomende gegevens waarin moeten worden opgenomen. U kunt of een bestaande dataset gebruiken of nieuwe creëren.

### Een nieuwe gegevensset maken

Selecteer **[!UICONTROL New dataset]** om een nieuwe dataset te maken. Voor de vorm die verschijnt, verstrek de naam, een facultatieve beschrijving, evenals het doelschema voor de dataset. Als u een [!DNL Profile]-Toegelaten schema selecteert, kunt u kiezen als de dataset ook [!DNL Profile]-toegelaten zou moeten zijn.

![new-dataset](../../../../images/tutorials/create/http/new-dataset.png)

### Een bestaande gegevensset gebruiken

Als u een bestaande gegevensset wilt gebruiken, selecteert u **[!UICONTROL Existing dataset]**. Selecteer in het formulier dat wordt weergegeven de gegevensset die u wilt gebruiken. Zodra u een dataset selecteert, kunt u kiezen als de dataset [!DNL Profile]-toegelaten zou moeten zijn.

![bestaande gegevensset](../../../../images/tutorials/create/http/existing-dataset.png)

### Standaardvelden toewijzen

Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Raadpleeg de zelfstudie over het toewijzen van CSV-gegevens aan XDM-schemavelden](../../../../../ingestion/tutorials/map-a-csv-file.md) voor meer informatie over gegevenstoewijzing en mapperfuncties.[

Als u een nieuw bronveld wilt toevoegen, selecteert u **[!UICONTROL Add new mapping]**.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Er wordt een nieuw bronveld en een nieuwe koppeling naar een doelveld weergegeven. Als u een nieuw bronveld wilt toevoegen, selecteert u het pijlpictogram naast de invoerbalk [!UICONTROL Select source field].

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

In het deelvenster [!UICONTROL Select attributes] kunt u de bestandshiërarchie verkennen en een specifiek bronveld selecteren om toe te wijzen aan een doel-XDM-veld. Als u het bronveld hebt geselecteerd dat u wilt toewijzen, selecteert u **[!UICONTROL Select]** om door te gaan.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

Als er een bronveld is geselecteerd, kunt u nu het juiste doel-XDM-veld identificeren waarnaar u de hyperlink wilt koppelen. Selecteer het schemapictogram onder de sectie van het doelgebied.

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

Het [!UICONTROL Map source field to target field] venster verschijnt, die u van een interface voorzien om het schema van uw doeldataset te onderzoeken. Selecteer het doelveld dat overeenkomt met het bronveld en selecteer **[!UICONTROL Select]** om door te gaan.

![map-naar-target-field](../../../../images/tutorials/create/http/map-to-target-field.png)

Als alle bronvelden zijn toegewezen aan de juiste XDM-doelvelden, selecteert u **[!UICONTROL Next]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## Gegevens

De stap **[!UICONTROL Dataflow detail]** wordt weergegeven. Op deze pagina kunt u details voor de gemaakte gegevensstroom verstrekken door een naam en een facultatieve beschrijving te geven.

Nadat u de details voor de gegevensstroom hebt opgegeven, selecteert u **[!UICONTROL Next]**.

![dataFlow-detail](../../../../images/tutorials/create/http/dataflow-detail.png)

## Controleren

De stap **[!UICONTROL Review]** wordt weergegeven, zodat u de details van de gegevensstroom kunt bekijken voordat deze wordt gemaakt. De details zijn groep binnen de volgende categorieën:

- **[!UICONTROL Connection]**: Hier worden de naam van de account, het bronplatform en de bronnaam weergegeven.
- **[!UICONTROL Assign dataset and map fields]**: Toont de doeldataset en het schema dat de dataset aansluit.

Nadat de details correct zijn bevestigd, uitgezocht **[!UICONTROL Finish]**.

![revisie](../../../../images/tutorials/create/http/review.png)

## URL voor streamingeindpunt ophalen

Als de verbinding is gemaakt, wordt de pagina met brondetails weergegeven. Deze pagina bevat details van de zojuist gemaakte verbinding, waaronder eerder uitgevoerde dataflows, ID en URL van het streamingeindpunt.

![eindpunt](../../../../images/tutorials/create/http/endpoint.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een het stromen verbinding van HTTP gecreeerd, toelatend u om het het stromen eindpunt te gebruiken om tot een verscheidenheid van [!DNL Data Ingestion] APIs toegang te hebben. Voor instructies voor het maken van een streamingverbinding in de API leest u de [zelfstudie voor het maken van een streamingverbinding](../../../api/create/streaming/http.md).

Lees de zelfstudie over [streamingtijdreeksgegevens](../../../../../ingestion/tutorials/streaming-time-series-data.md) of de zelfstudie over [streamingrecordgegevens](../../../../../ingestion/tutorials/streaming-record-data.md) voor meer informatie over het streamen van gegevens naar Platform.
