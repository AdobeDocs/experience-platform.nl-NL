---
title: Een nieuwe doelverbinding maken
type: Tutorial
description: Leer hoe u verbinding maakt met een doel in Adobe Experience Platform, waarschuwingen inschakelt en marketingacties instelt voor de verbonden bestemming.
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 59ff77ff9f4a6fe147b5d8231fd3caa2550ae20e
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 0%

---

# Een nieuwe doelverbinding maken

>[!IMPORTANT]
> 
>* Om met een bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om met een bestemming te verbinden die dataset uitvoert steunt, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage and Activate Dataset Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

## Overzicht {#overview}

Voordat u publieksgegevens naar een bestemming kunt verzenden, moet u een verbinding naar het doelplatform instellen. In dit artikel wordt uitgelegd hoe u een nieuwe doelverbinding instelt, waarop u vervolgens een publiek kunt activeren of gegevenssets kunt exporteren met de gebruikersinterface van Adobe Experience Platform.

## Het gewenste doel in de catalogus zoeken {#setup}

1. Ga naar **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteer de tab **[!UICONTROL Catalog]** .

   ![ Schermafbeelding van Experience Platform UI, die de pagina van de bestemmingscatalogus toont.](../assets/ui/connect-destinations/catalog.png)

2. De kaarten van de bestemming in de catalogus zouden verschillende actiecontroles kunnen hebben, afhankelijk van of u een bestaande verbinding aan de bestemming hebt en of de bestemmingen het activeren van publiek, het uitvoeren van datasets, of allebei steunen. U zou om het even welke volgende controles voor bestemmingskaarten kunnen zien:

   * **[!UICONTROL Set up]**. Een verbinding moet eerst opstelling aan deze bestemming zijn alvorens u publiek kunt activeren of datasets uitvoeren.
   * **[!UICONTROL Activate]**. Er is al een verbinding ingesteld met dit doel. Deze bestemming steunt publieksactivering en de uitvoer van datasets.
   * **[!UICONTROL Activate audiences]**. Er is al een verbinding ingesteld met dit doel. Deze bestemming ondersteunt alleen activering van het publiek.

   Voor meer informatie over het verschil tussen deze controles, kunt u ook naar de [ sectie van de Catalogus ](../ui/destinations-workspace.md#catalog) van de documentatie van de bestemmingswerkruimte verwijzen.

   Selecteer **[!UICONTROL Set up]**, **[!UICONTROL Activate]** of **[!UICONTROL Activate audiences]** , afhankelijk van de besturingselementen die beschikbaar zijn.

   ![ Schermafbeelding van Experience Platform UI, die de pagina van de bestemmingscatalogus met de benadrukte controle van de Opstelling toont.](../assets/ui/connect-destinations/set-up.png)

   ![ Schermafbeelding van Experience Platform UI, die de pagina van de bestemmingscatalogus met Activate benadrukt publiek toont.](../assets/ui/connect-destinations/activate-segments.png)

3. Als u **[!UICONTROL Set up]** selecteerde, skip aan de volgende stap, [&#128279;](#authenticate) aan de bestemming voor authentiek verklaren.

   Als u **[!UICONTROL Activate]**, **[!UICONTROL Activate audiences]** of **[!UICONTROL Export datasets]** hebt geselecteerd, wordt nu een lijst met bestaande doelverbindingen weergegeven.

   Selecteer **[!UICONTROL Configure new destination]** om een nieuwe verbinding met het doel tot stand te brengen.

   ![ Schermafbeelding van Experience Platform UI, die een lijst van beschikbare bestemmingen en vormt nieuwe benadrukte bestemmingscontrole toont.](../assets/ui/connect-destinations/configure-new-destination.png)

## Verifiëren voor bestemming {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_account_name"
>title="Accountnaam"
>abstract="Voer een naam in waarmee u dit doelaccount in de toekomst gemakkelijk kunt herkennen. Dit is vooral handig als u meerdere verbindingen met hetzelfde doeltype hebt."

De eerste stap in het verbinden met een bestemming moet aan het bestemmingsplatform voor authentiek verklaren.

Afhankelijk van het doel waarmee u verbinding maakt, kunt u naar de pagina van de bestemmingspartner worden gebracht voor verificatie, of u wordt gevraagd om verificatiegegevens rechtstreeks in te voeren in de Experience Platform-workflow. Hieronder ziet u een voorbeeld van de vereiste invoer voor verificatie bij een [!DNL Amazon S3] -doel. Gedetailleerde instructies over de vereiste invoer worden gegeven op elke pagina met doeldocumentatie (zie bijvoorbeeld de verificatiesectie voor [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) en voor [[!DNL Facebook]](/help/destinations/catalog/social/facebook.md#authenticate) ).

**[!DNL Amazon S3]vereiste en optionele verificatieparameters**

![ Beeld dat de vereiste en facultatieve inputparameters toont wanneer het voor authentiek verklaren aan een bestemming van Amazon S3.](../assets/ui/connect-destinations/authenticate-amazon-s3-example.png)

## Verbindingsparameters instellen {#set-up-connection-parameters}

Als u al verificatie hebt ingesteld op de bestemming, kunt u doorgaan met het bestaande account of kunt u een nieuw account instellen.

Afhankelijk van het doel waarmee u verbinding maakt, wordt u mogelijk gevraagd verschillende typen verbindingsparameters in te voeren. Wanneer u bijvoorbeeld verbinding maakt met een [!DNL Amazon S3] -doel, wordt u gevraagd gegevens te verstrekken over de naam van de [!DNL Amazon S3] emmertje en het mappad waar bestanden worden gedeponeerd. Hieronder ziet u twee voorbeelden van vereiste invoer voor een [!DNL Amazon S3] -doel en een [!DNL Trade Desk] -doel. Gedetailleerde instructies over de vereiste invoer worden gegeven op elke pagina van de doeldocumentatie.

>[!IMPORTANT]
>
>De onderstaande afbeeldingen worden alleen ter illustratie gebruikt. De details van de bestemmingsverbinding variëren tussen bestemmingen. Voor gedetailleerde informatie over de verbindingsdetails voor uw bestemming, lees **verbind met de bestemmings** sectie in elke [ bestemmingscatalogus ](../catalog/overview.md) pagina (bijvoorbeeld, [[!DNL Google Customer Match]](../catalog/advertising/google-customer-match.md#connect), [[!DNL Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md#connect), of [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)).

**[!DNL Amazon S3]vereiste en optionele invoerparameters**

![ Beeld die de vereiste en facultatieve inputparameters tonen wanneer het verbinden met een bestemming van Amazon S3.](../assets/ui/connect-destinations/connect-destination-amazons3-example.png)

**[!DNL The Trade Desk]vereiste en optionele invoerparameters**

![ Beeld dat de vereiste en facultatieve inputparameters toont wanneer het verbinden met een bestemming van het Bureau van de Handel.](../assets/ui/connect-destinations/connect-destination-trade-desk-example.png)

### Opties voor bestandsindeling instellen voor geëxporteerde bestanden {#file-formatting-and-compression-options}

Voor op bestanden gebaseerde doelen kunt u verschillende instellingen configureren die betrekking hebben op de indeling en comprimeren van de geëxporteerde bestanden. Voor meer informatie over alle beschikbare het formatteren en compressieopties, lees [ dossier het formatteren opties voor op dossier-gebaseerde bestemmingsleerprogramma ](/help/destinations/ui/batch-destinations-file-formatting-options.md).

![ Beeld dat de dossiertype selectie en diverse opties voor Csv- dossiers toont.](/help/destinations/assets/ui/connect-destinations/file-formatting-options.png)

### De bestemmingsverbinding van de opstelling voor publieksactivering, rekeningsactivering, perspectiefactivering of datasetuitvoer {#segment-activation-or-dataset-exports}

Sommige op dossier-gebaseerde bestemmingen steunen publieksactivering aan bekende klanten, rekeningsklanten, of vooruitzichten, evenals datasetuitvoer. Voor die bestemmingen, kunt u kiezen of om een verbinding tot stand te brengen die u [ toelaat om publiek ](/help/destinations/ui/activate-batch-profile-destinations.md), [ rekeningen ](/help/destinations/ui/activate-account-audiences.md), [ vooruitzichten ](/help/destinations/ui/activate-prospect-audiences.md), of [ de uitvoerdatasets ](/help/destinations/ui/export-datasets.md) te activeren.

>[!WARNING]
>
>Wanneer u gegevenssets exporteert, ziet u dat het exporteren naar JSON-bestanden alleen in de gecomprimeerde modus wordt ondersteund. Exporteren naar [!DNL Parquet] -bestanden worden ondersteund in een gecomprimeerde en niet-gecomprimeerde modus.

![ Beeld dat de controle van de gegevenstypeselectie toont die gebruikers toestaat om tussen de activering van het publiek en de uitvoer van de dataset te selecteren.](/help/destinations/assets/ui/connect-destinations/data-type-selection.png)

### Doelwaarschuwingen inschakelen {#enable-alerts}

1. (Optioneel) Selecteer de waarschuwingen voor de doelgegevensstroom waarop u zich wilt abonneren. U kunt zich op alarm abonneren wanneer het creëren van een gegevensstroom om waakzame berichten betreffende de status, het succes, of het mislukken van uw looppas te ontvangen. De beschikbare waarschuwingen verschillen afhankelijk van het doeltype (bestandsgebaseerd of streaming) waarmee u verbinding maakt. Lees [ Abonneren aan in-context bestemmingsalarm ](alerts.md) voor gedetailleerde informatie over bestemmingdataflow alarm.

   ![ Vorm nieuwe bestemmingsdialoog met de in-context benadrukte opties van het bestemmingsalarm.](../assets/ui/connect-destinations/subscribe-to-alerts.png)

2. Selecteer **[!UICONTROL Next]**.

   ![ Vorm nieuwe bestemmingsdialoog met de Volgende benadrukte controle, toestaand de gebruiker om aan de volgende stap in het werkschema te werk te gaan.](../assets/ui/connect-destinations/next.png)

## marketingacties selecteren {#select-marketing-actions}

1. Selecteer de marketingacties die van toepassing zijn op de gegevens die u naar de bestemming wilt exporteren. Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Voor meer informatie over marketing acties, zie de [ pagina van het het beleidsoverzicht van het gegevensgebruik ](../../data-governance/policies/overview.md).

   ![ Vorm nieuwe bestemmingsdialoog met de beschikbare benadrukte marketing acties. De beschikbare controles om Connect aan bestemmingswerkschema te voltooien worden ook benadrukt.](../assets/ui/connect-destinations/governance.png)

2. Selecteer **[!UICONTROL Save & Exit]** om de bestemmingsconfiguratie te bewaren, of **[!UICONTROL Next]** te selecteren om aan de stroom van de publieksgegevens [ activering ](activation-overview.md) te werk te gaan.

## Volgende stappen {#next-steps}

Door dit document te lezen, hebt u geleerd hoe u de gebruikersinterface van Experience Platform kunt gebruiken om een verbinding met een doel tot stand te brengen. Ter herinnering, variëren de beschikbare en vereiste verbindingsparameters van bestemming tot bestemming. U zou de pagina van de bestemmingsdocumentatie in de [ bestemmingscatalogus ](/help/destinations/catalog/overview.md) voor specifieke informatie over de vereiste input en beschikbare opties per bestemmingstype ook moeten raadplegen.

Daarna, kunt u aan [ het activeren publiek ](/help/destinations/ui/activation-overview.md) of [ het uitvoeren datasets ](/help/destinations/ui/export-datasets.md) aan uw bestemming te werk gaan.