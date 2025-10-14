---
title: Een HTTP API-streamingverbinding maken met de gebruikersinterface
description: Deze UI-handleiding helpt u bij het maken van een streamingverbinding met Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 0%

---


# Een [!DNL HTTP API] streamingverbinding maken met de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een streamingbronverbinding met de werkruimte van [!UICONTROL Sources] .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   - [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

## Een streamingverbinding maken

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Streaming]** de optie **[!UICONTROL HTTP API]** en selecteer vervolgens **[!UICONTROL Add data]** .

![&#x200B; catalogus &#x200B;](../../../../images/tutorials/create/http/catalog.png)

De pagina **[!UICONTROL Connect HTTP API account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u het HTTP API-account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u vervolgens **[!UICONTROL Next]** om door te gaan.

![&#x200B; bestaand-rekening &#x200B;](../../../../images/tutorials/create/http/existing.png)

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u een nieuwe account maakt. Geef in het invoerformulier dat wordt weergegeven een accountnaam en een optionele beschrijving op. U zult ook de optie krijgen om de volgende configuratieeigenschappen te verstrekken:

- **[!UICONTROL Authentication]:** This property determines whether or not the streaming connection requires authentication. Verificatie zorgt ervoor dat gegevens worden verzameld van vertrouwde bronnen. Als u met Persoonlijk Identificeerbare Informatie (PII) werkt, zou dit bezit moeten worden aangezet. Deze eigenschap is standaard uitgeschakeld.
- **[!UICONTROL XDM compatible]:** Deze eigenschap geeft aan of deze streamingverbinding gebeurtenissen verzendt die compatibel zijn met XDM-schema&#39;s. Deze eigenschap is standaard uitgeschakeld.

Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en selecteert u **[!UICONTROL Next]** om door te gaan.

![&#x200B; nieuw-rekening &#x200B;](../../../../images/tutorials/create/http/new.png)

## Gegevens selecteren

Nadat u de HTTP API-verbinding hebt gemaakt, wordt de stap **[!UICONTROL Select data]** weergegeven en krijgt u een interface voor het uploaden en voorvertonen van uw gegevens.

Selecteer **[!UICONTROL Upload files]** om uw gegevens te uploaden. U kunt uw gegevens ook naar het gedeelte [!UICONTROL Drag and drop files] van de interface slepen.

![&#x200B; toe:voegen-gegevens &#x200B;](../../../../images/tutorials/create/http/add-data.png)

Als uw gegevens zijn geüpload, kunt u de rechterkant van de interface gebruiken om een voorvertoning van de bestandshiërarchie weer te geven. Selecteer **[!UICONTROL Next]** om door te gaan.

![&#x200B; voorproef-steekproef-gegevens &#x200B;](../../../../images/tutorials/create/http/preview-sample-data.png)

## Gegevensvelden toewijzen aan een XDM-schema

De stap [!UICONTROL Mapping] wordt weergegeven en biedt een interface voor het toewijzen van de brongegevens aan een Experience Platform-gegevensset.

De [!DNL HTTP API] -bron ondersteunt inname van JSON-bestanden. JSON-bestanden vereisen geen handmatige configuratie als deze zijn gemarkeerd als XDM-klap. Als niet, dan moet u de afbeelding uitdrukkelijk vormen.

Kies een dataset voor binnenkomende gegevens waarin moeten worden opgenomen. U kunt een bestaande gegevensset gebruiken of een nieuwe gegevensset maken.

### Een nieuwe gegevensset maken

Selecteer **[!UICONTROL New dataset]** als u een nieuwe gegevensset wilt maken. Voor de vorm die verschijnt, verstrek de naam, een facultatieve beschrijving, evenals het doelschema voor de dataset. Als u een [!DNL Profile] -schema selecteert, kunt u kiezen of de dataset ook [!DNL Profile] -enabled zou moeten zijn.

![&#x200B; nieuw-dataset &#x200B;](../../../../images/tutorials/create/http/new-dataset.png)

### Een bestaande gegevensset gebruiken

Selecteer **[!UICONTROL Existing dataset]** als u een bestaande gegevensset wilt gebruiken. Selecteer in het formulier dat wordt weergegeven de gegevensset die u wilt gebruiken. Nadat u een gegevensset hebt geselecteerd, kunt u kiezen of de gegevensset [!DNL Profile] moet zijn ingeschakeld.

![&#x200B; bestaand-dataset &#x200B;](../../../../images/tutorials/create/http/existing-dataset.png)

### Standaardvelden toewijzen

Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie de [&#x200B; gids UI van de Prep van Gegevens &#x200B;](../../../../../data-prep/ui/mapping.md).

Selecteer **[!UICONTROL Add new mapping]** als u een nieuw bronveld wilt toevoegen.

![&#x200B; toe:voegen-nieuw-afbeelding &#x200B;](../../../../images/tutorials/create/http/add-new-mapping.png)

Er wordt een nieuw bronveld en een nieuwe koppeling naar een doelveld weergegeven. Als u een nieuw bronveld wilt toevoegen, selecteert u het pijlpictogram naast de invoerbalk van [!UICONTROL Select source field] .

![&#x200B; selecteren-bron-gebied &#x200B;](../../../../images/tutorials/create/http/select-source-field.png)

In het deelvenster [!UICONTROL Select attributes] kunt u de bestandshiërarchie verkennen en een specifiek bronveld selecteren om toe te wijzen aan een doel-XDM-veld. Als u het bronveld hebt geselecteerd dat u wilt toewijzen, selecteert u **[!UICONTROL Select]** om door te gaan.

![&#x200B; selecteren-attributen &#x200B;](../../../../images/tutorials/create/http/select-attributes.png)

Als er een bronveld is geselecteerd, kunt u nu het juiste doel-XDM-veld identificeren waarnaar u de hyperlink wilt koppelen. Selecteer het schemapictogram onder de sectie van het doelgebied.

![&#x200B; selecteren-doel-gebied &#x200B;](../../../../images/tutorials/create/http/select-target-field.png)

Het [!UICONTROL Map source field to target field] venster verschijnt, die u van een interface voorzien om het schema van uw doeldataset te onderzoeken. Selecteer het doelveld dat overeenkomt met het bronveld en selecteer vervolgens **[!UICONTROL Select]** om door te gaan.

![&#x200B; kaart-aan-doel-gebied &#x200B;](../../../../images/tutorials/create/http/map-to-target-field.png)

Als alle bronvelden zijn toegewezen aan de juiste XDM-doelvelden, selecteert u **[!UICONTROL Next]**

![&#x200B; gegeven-prep-volledig &#x200B;](../../../../images/tutorials/create/http/data-prep-complete.png)

## Gegevens

De stap **[!UICONTROL Dataflow detail]** wordt weergegeven. Op deze pagina kunt u details voor de gemaakte gegevensstroom verstrekken door een naam en een facultatieve beschrijving te geven.

Selecteer **[!UICONTROL Next]** nadat u details voor de gegevensstroom hebt opgegeven.

![&#x200B; dataflow-detail &#x200B;](../../../../images/tutorials/create/http/dataflow-detail.png)

## Controleren

De stap **[!UICONTROL Review]** wordt weergegeven, zodat u de details van de gegevensstroom kunt bekijken voordat deze wordt gemaakt. De details zijn groep binnen de volgende categorieën:

- **[!UICONTROL Connection]**: geeft de accountnaam, het bronplatform en de bronnaam weer.
- **[!UICONTROL Assign dataset and map fields]**: toont de doeldataset en het schema dat de dataset volgt.

Selecteer **[!UICONTROL Finish]** nadat u hebt bevestigd dat de details juist zijn.

![&#x200B; overzicht &#x200B;](../../../../images/tutorials/create/http/review.png)

## URL voor streamingeindpunt ophalen

Als de verbinding is gemaakt, wordt de pagina met brondetails weergegeven. Deze pagina bevat details van de zojuist gemaakte verbinding, waaronder eerder uitgevoerde dataflows, ID en URL van het streamingeindpunt.

![&#x200B; eindpunt &#x200B;](../../../../images/tutorials/create/http/endpoint.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een streaming HTTP-verbinding gemaakt, waarmee u het streaming eindpunt kunt gebruiken voor toegang tot diverse [!DNL Data Ingestion] API&#39;s. Voor instructies om een het stromen verbinding in API tot stand te brengen, te lezen gelieve [&#x200B; creërend een het stromen verbindingsleerprogramma &#x200B;](../../../api/create/streaming/http.md).

Leren hoe te om gegevens aan Experience Platform te stromen, te lezen gelieve of het leerprogramma op [&#x200B; het stromen tijdreeksgegevens &#x200B;](../../../../../ingestion/tutorials/streaming-time-series-data.md) of het leerprogramma op [&#x200B; het stromen verslaggegevens &#x200B;](../../../../../ingestion/tutorials/streaming-record-data.md).
