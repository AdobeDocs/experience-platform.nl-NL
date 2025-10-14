---
keywords: Experience Platform;home;populaire onderwerpen;bronnen;connectors;bronconnectors;campagne;beheerde services voor campagne
title: Een Adobe Campaign Managed Cloud Services-bronverbinding maken met de gebruikersinterface van Experience Platform
description: Leer hoe u Adobe Experience Platform via de gebruikersinterface van Experience Platform verbindt met Adobe Campaign Managed Cloud Services.
exl-id: 067ed558-b239-4845-8c85-3bf9b1d4caed
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 0%

---

# Een Adobe Campaign Managed Cloud Services-bronverbinding maken met de gebruikersinterface van Experience Platform

Deze zelfstudie bevat stappen om een bronverbinding te maken waarmee uw Adobe Campaign Managed Cloud Services-gegevens naar Adobe Experience Platform worden overgebracht.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [&#x200B; Sandboxes &#x200B;](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## Adobe Campaign Managed Cloud Services verbinden met Experience Platform

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt de zoekbalk ook gebruiken om de weergegeven bronnen te beperken.

Selecteer onder de categorie **[!UICONTROL Adobe applications]** de optie **[!UICONTROL Adobe Campaign Managed Cloud Services]** en selecteer vervolgens **[!UICONTROL Add data]** .

![&#x200B; de broncatalogus die de kaart van Adobe Campaign Managed Cloud Services toont.](../../../../images/tutorials/create/campaign/catalog.png)

### Gegevens selecteren {#select-data}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="Adobe Campaign-milieu-instantie"
>abstract="De naam van de Adobe Campaign-omgeving die u wilt gebruiken."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="Targettoewijzing"
>abstract="De afbeeldingen van het doel zijn technische voorwerpen die door Campagne worden gebruikt om berichten te leveren, en bevatten alle technische montages die worden vereist om leveringen (adressen, telefoonaantallen, opt-in indicatoren, extra herkenningstekens..) te verzenden."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="Schemanaam"
>abstract="De naam van de entiteit die is gedefinieerd in de Adobe Campaign-database."
>text="Learn more in documentation"

De stap [!UICONTROL Select data] wordt weergegeven en verschaft u een interface voor het configureren van [!UICONTROL Adobe Campaign instance] , [!UICONTROL Target mapping] en [!UICONTROL Schema name] .

| Eigenschap | Beschrijving |
| --- | --- |
| Adobe Campaign-exemplaar | De naam van de Adobe Campaign-omgevingsinstantie die u gebruikt. |
| Targettoewijzing | De technische voorwerpen die door Campaign worden gebruikt om berichten te leveren, en bevatten alle technische montages die worden vereist om leveringen te verzenden. |
| Schemanaam | De naam van de schemaentiteit die u aan Experience Platform brengt. De opties omvatten het Logboek van de Levering en het Volgen Logboek. |

![&#x200B; een interface waar u uw instantie van Adobe Campaign, doelafbeelding, en schemanaam kunt vormen.](../../../../images/tutorials/create/campaign/select-data.png)

Zodra u waarden voor uw instantie van de Campagne, doelafbeelding, en schemanaam hebt verstrekt, werkt het scherm bij om een voorproef van uw schema evenals een steekproefdataset te tonen. Selecteer **[!UICONTROL Next]** als u klaar bent.

![&#x200B; een voorproef van uw schemahiërarchie evenals een steekproef van uw dataset &#x200B;](../../../../images/tutorials/create/campaign/preview.png)

### Een bestaande gegevensset gebruiken

De [!UICONTROL Dataflow detail] pagina staat u toe om te selecteren of u een bestaande dataset wilt gebruiken of een nieuwe dataset voor uw gegevensstroom vormen.

Selecteer **[!UICONTROL Existing dataset]** als u een bestaande gegevensset wilt gebruiken. U kunt of een bestaande dataset terugwinnen gebruikend de [!UICONTROL Advanced search] optie of door door de lijst van bestaande datasets in het dropdown menu te scrollen.

Selecteer een gegevensset en geef een naam op voor de gegevensstroom en een optionele beschrijving.

![&#x200B; een interface die de bestaande datasetoptie toont.](../../../../images/tutorials/create/campaign/existing-dataset.png)

### Een nieuwe gegevensset gebruiken

Als u een nieuwe gegevensset wilt gebruiken, selecteert u **[!UICONTROL New dataset]** en geeft u vervolgens een naam voor de uitvoergegevensset en een optionele beschrijving op. Selecteer vervolgens het schema dat u wilt toewijzen met de optie [!UICONTROL Advanced search] of door door de lijst met bestaande schema&#39;s in het vervolgkeuzemenu te bladeren. Selecteer **[!UICONTROL Next]** als u klaar bent.

![&#x200B; een interface die de nieuwe datasetoptie toont.](../../../../images/tutorials/create/campaign/new-dataset.png)

### Waarschuwingen inschakelen

U kunt waarschuwingen inschakelen om meldingen te ontvangen over de status van uw gegevensstroom. Selecteer een waarschuwing in de lijst om u te abonneren en meldingen te ontvangen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bronalarm gebruikend UI &#x200B;](../../alerts.md).

Wanneer u klaar bent met het opgeven van details voor de gegevensstroom, selecteert u **[!UICONTROL Next]** .

![&#x200B; een selectie van verschillende waakzame types die u voor uw dataflow kunt toelaten.](../../../../images/tutorials/create/campaign/alerts.png)

### Gegevensvelden toewijzen aan een XDM-schema

De stap [!UICONTROL Mapping] verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Experience Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie de [&#x200B; gids UI van de Prep van Gegevens &#x200B;](../../../../../data-prep/ui/mapping.md).

>[!IMPORTANT]
>
>Wanneer u uw bronvelden toewijst aan doel-XDM-velden, moet u ervoor zorgen dat u het toegewezen primaire identiteitsveld toewijst aan het juiste doel-XDM-veld.
>
>Voor elk publiek kunt u maximaal 20 velden toevoegen om toe te wijzen aan Adobe Campaign. U kunt deze limiet wijzigen door de waarde van de optie `NmsCdp_Aep_Sources_Max_Columns` bij te werken in de map Beheer > Platform > Opties van Campagneverkenner.

Selecteer **[!UICONTROL Next]** wanneer de brongegevens correct zijn toegewezen.

![&#x200B; de toewijzingsboom van A met vier brongegevensgebieden die aan hun overeenkomstige XDM schemagebieden in kaart worden gebracht.](../../../../images/tutorials/create/campaign/mapping.png)

### Controleer uw gegevensstroom

De stap **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt bekijken voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: geeft het brontype, het relevante pad van het gekozen bronbestand en de hoeveelheid kolommen in dat bronbestand weer.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt aan.

Nadat u de gegevensstroom hebt gereviseerd, selecteert u **[!UICONTROL Finish]** en laat u enige tijd over om de gegevensstroom te maken.

![&#x200B; een overzichtspagina die verbinding en datasetinformatie toont.](../../../../images/tutorials/create/campaign/review.png)

### Uw gegevenssetactiviteit controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over ingebedde tarieven en succesvolle en ontbroken partijen te zien.

Selecteer **[!UICONTROL Dataflows]** in de broncatalogus om uw gegevenssetactiviteit weer te geven.

![&#x200B; de pagina van de broncatalogus met de gegevens geselecteerde kopbal.](../../../../images/tutorials/create/campaign/dataflows.png)

Selecteer vervolgens de doeldataset in de lijst met gegevensstromen die worden weergegeven.

![&#x200B; een lijst van bestaande gegevensstromen met de geselecteerde het doeldataset van de Logboeken van de Levering van Adobe Campaign.](../../../../images/tutorials/create/campaign/target-dataset.png)

De pagina met gegevenssetactiviteiten wordt weergegeven. Van hier, kunt u informatie over de prestaties van uw gegevensstroom zien, met inbegrip van tarief van opname, succesvolle partijen, en ontbroken partijen.

Deze pagina voorziet u ook van een interface om de meta-gegevensbeschrijving van uw gegevensstroom bij te werken, gedeeltelijke opname en foutendiagnostiek toe te laten, evenals nieuwe gegevens toe te voegen aan uw dataset.

![&#x200B; een interface met grafieken die het innametarief van een geselecteerde dataset vertegenwoordigen.](../../../../images/tutorials/create/campaign/dataset-activity.png)


>[!IMPORTANT]
>
>U kunt geen back-up maken van oude gebeurtenislogboeken met de Adobe Campaign Managed Cloud Services-bron. Als backfill vereist is, gebruikt u een aangepaste workflow of een aangepaste implementatie om gegevens te exporteren naar Amazon S3 of Azure Blob, of van Amazon S3 of Azure Blob naar een Adobe Experience Platform-gegevensset.


## Volgende stappen

Aan de hand van deze zelfstudie hebt u een gegevensstroom gemaakt waarmee u uw AMPAGE v8-leveringslogs en logbestandsgegevens voor bijhouden naar Experience Platform kunt overbrengen. Binnenkomende gegevens kunnen nu worden gebruikt door downstream Experience Platform-services, zoals [!DNL Real-Time Customer Profile] en [!DNL Data Science Workspace] . Raadpleeg de volgende documenten voor meer informatie:

* [[!DNL Real-Time Customer Profile]-overzicht](../../../../../profile/home.md)
* [[!DNL Data Science Workspace]-overzicht](../../../../../data-science-workspace/home.md)
