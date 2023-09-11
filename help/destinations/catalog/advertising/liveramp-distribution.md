---
title: LiveRamp - Distribution-verbinding
description: Leer hoe u de LiveRamp - Distribution-connector kunt gebruiken om soorten publiek die eerder in LiveRamp zijn opgenomen, te activeren voor andere advertentiebestemmingen.
hide: true
hidefromtoc: true
source-git-commit: c04c7ff4f1ab45d944f4ab516d7842df536fae40
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 5%

---


# [!DNL LiveRamp - Distribution] verbinding {#liveramp-onboarding}

De [!DNL LiveRamp - Distribution] Met deze verbinding kunt u het publiek activeren van Experience Platform tot hoogwaardige uitgevers op mobiele media, het web, displays en verbonden tv-media.

>[!IMPORTANT]
>
>Deze doelconnector en documentatiepagina worden gemaakt en onderhouden door LiveRamp. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen met LiveRamp [hier](mailto:example@email.com).

## Ondersteunde doelen {#supported-destinations}

[!DNL LiveRamp - Distribution] ondersteunt momenteel activering van het publiek voor de volgende platforms:

* [!DNL 4C Insights]
* [!DNL Acast]
* [!DNL Amobee]
* [!DNL Ampersand.tv]
* [!DNL Captify]
* [!DNL Cardlytics]
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [!DNL iHeartMedia]
* [!DNL Index Exchange]
* [!DNL Magnite CTV Platform]
* [!DNL Magnite DV+ (Rubicon Project)]
* [!DNL One Fox]
* [!DNL Pandora]
* [!DNL Reddit]
* [[!DNL Roku]](#roku)
* [!DNL Spotify]
* [!DNL Taboola]
* [!DNL TargetSpot]
* [!DNL Teads]
* [!DNL WB Discovery]

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL LiveRamp - Distribution] doel, hier is een geval van steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

Het marketingteam van een detailhandelaar in sportkleding gebruikte de [LiveRamp - Onboarding](liveramp-onboarding.md) verbinding om het publiek van Experience Platform naar zijn LiveRamp-account te sturen.

Via de [!DNL LiveRamp - Distribution] verbinding kunnen zij nu de activering van het onbewaakte publiek aan de bestemmingen teweegbrengen die bij de bovenkant van deze pagina worden vermeld, zodat zij gebruikers op mobiele, open Web, sociale, en [!DNL CTV] platforms.

## Boordpubliek naar LiveRamp {#onboarding}

Voordat u het publiek activeert via de [!DNL LiveRamp - Distribution] verbinding gebruiken [LiveRamp - Onboarding](liveramp-onboarding.md) verbinding om uw publiek van het Experience Platform naar LiveRamp uit te voeren.

Nadat u uw publiek hebt aangemeld bij LiveRamp, kunt u de activeringsworkflow voortzetten vanuit het dialoogvenster [verbinden met de bestemming](#connect) stap.

## Verbinden met de bestemming {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_identifier_settings"
>title="Id-instellingen"
>abstract="Selecteer de id&#39;s die door uw doel worden ondersteund. Zie de documentatie voor de volledige lijst van gesteunde herkenningstekens voor elke bestemming."

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor LiveRamp {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

![Platform UI-afbeelding die het doelverbindingsscherm.l weergeeft](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-new-connection.png)

* **[!UICONTROL Token URL]**: De URL van uw token LiveRamp.
* **[!UICONTROL LiveRamp Organization ID]**: De organisatie-id van uw LiveRamp-account.
* **[!UICONTROL Username]**: Uw gebruikersnaam van uw LiveRamp-account.
* **[!UICONTROL Password]**: Uw wachtwoord voor uw LiveRamp-account.

### Doeldetails configureren {#destination-details}

Nadat u verbinding hebt gemaakt met uw LiveRamp-account, voert u de vereiste informatie in om verbinding te maken met het doel waarop u het publiek wilt activeren.

![Platform UI-afbeelding die het scherm met doeldetails weergeeft.l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-destination-details.png)

* **[!UICONTROL Name]**: Vul de voorkeursnaam in voor uw doelverbinding.
* **[!UICONTROL Description]**: Voer een beschrijving in voor uw doel. Gebruik een beschrijving die u zal helpen het doel van deze bestemming gemakkelijk identificeren.
* **[!UICONTROL Destination]**: Gebruik het keuzemenu om het doel te selecteren waarnaar u het publiek wilt activeren. De bestemming u hier selecteert beïnvloedt direct wat u in [doelspecifieke instellingen](#destination-settings) scherm.
* **[!UICONTROL Integration]**: Selecteer de integratieaccount die u voor uw doel wilt gebruiken.
* **[!UICONTROL Identifier]**: Selecteer de id&#39;s die door uw doel worden ondersteund. Momenteel hebben alle bestemmingen hun gesteunde herkenningstekens die in het drop-down menu worden voorgevuld.

## Doelspecifieke instellingen {#destination-settings}

Elk van de bestemmingen [ondersteund](#supported-destinations) door [!DNL LiveRamp - Onboarding] vereist dat u specifieke configuratieopties invult.

Zie de secties hieronder voor gedetailleerde begeleiding op hoe te om elke bestemming te vormen.

### [!DNL 4C Insights] {#insights}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_4cinsights_profile_id"
>title="4C-merkprofiel-id"
>abstract="Voer de numerieke id in die aan uw 4C-merkprofiel is gekoppeld. Als u deze id niet hebt, neemt u contact op met uw 4C-vertegenwoordiger voor clientservices."

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

### [!DNL Acast] {#acast}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_acast_client"
>title="Naam client"
>abstract="Uw naam van de adverteerderaccount, zoals u wilt dat deze aan de doelpartner wordt getoond. Gebruik uw bedrijfsnaam. Gebruik geen spaties of speciale tekens."

### [!DNL Amobee] {#amobee}

### [!DNL Ampersand.tv] {#ampersand-tv}

### [!DNL Captify] {#captify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_captify_client"
>title="Naam client"
>abstract="Uw naam van de adverteerderaccount, zoals u wilt dat deze aan de doelpartner wordt getoond. Gebruik uw bedrijfsnaam. Gebruik geen spaties of speciale tekens."

### [!DNL Cardlytics] {#cardlytics}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_cardlytics_client"
>title="Naam client"
>abstract="Uw naam van de adverteerderaccount, zoals u wilt dat deze aan de doelpartner wordt getoond. Gebruik uw bedrijfsnaam. Gebruik geen spaties of speciale tekens."

### [!DNL Disney (Hulu/ESPN/ABC)] {#disney}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_agreement"
>title="Terreurovereenkomst voor gegevensbestemming van adverteerders"
>abstract="Type in `I AGREE` om de bevestiging en instemming met de gegevensvoorwaarden van Disney-adverteerders te bevestigen."
>additional-url="https://www.disneyadvertising.com/ADVERTISER-DATA-DESTINATION-TERMS/" text="De overeenkomst lezen"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_client"
>title="Naam client"
>abstract="Uw naam van de adverteerderaccount, zoals u wilt dat deze aan de doelpartner wordt getoond. Gebruik uw bedrijfsnaam. Gebruik geen spaties of speciale tekens."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_email"
>title="Uw e-mailadres"
>abstract="Voer een e-mailadres in dat aan een persoon is gekoppeld. Dit e-mailadres fungeert als handtekening op de overeenkomst met de gegevensvoorwaarden van de adverteerder. Dit e-mailadres wordt ook gebruikt om indien nodig contact met u op te nemen."

Vul de onderstaande velden in om details voor de bestemming te configureren.

![De beeld van UI van het platform die de gebieden van klantengegevens voor de bestemming van de Ontkenning toont.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-disney-fields.png)

* **[!UICONTROL Advertiser data destination terms agreement]**: Type in `I AGREE` om de bevestiging en instemming met de gegevensvoorwaarden van Disney-adverteerders te bevestigen.
* **[!UICONTROL Client name]**: Ga uw bedrijfsnaam in aangezien u het aan de bestemmingspartner wilt worden getoond.
* **[!UICONTROL Email address]**: Voer een e-mailadres in dat aan een persoon is gekoppeld. Dit e-mailadres fungeert als handtekening op de overeenkomst met de gegevensvoorwaarden van de adverteerder.

### [!DNL iHeartMedia] {#iheartmedia}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_iheartmedia_client"
>title="Naam client"
>abstract="Uw naam van de adverteerderaccount, zoals u wilt dat deze aan de doelpartner wordt getoond. Gebruik uw bedrijfsnaam. Gebruik geen spaties of speciale tekens."

### [!DNL Index Exchange] {#index-exchange}

### [!DNL Magnite CTV Platform] {#magnite}

### [!DNL Magnite DV+ (Rubicon Project)] {#magnite-dv}

### [!DNL One Fox] {#fox}

### [!DNL Pandora] {#pandora}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_data_provider_name"
>title="Naam gegevensaanbieder"
>abstract="De naam van uw bedrijf zoals u het aan Pandora wilt tonen. De naam kan maximaal 40 kleine letters en alfanumerieke tekens bevatten (bijvoorbeeld My_Company)."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_rep_email"
>title="E-mailadres van accountvertegenwoordiger"
>abstract="Het e-mailadres van uw vertegenwoordiger van uw Pandora-account. Dit adres wordt gebruikt om taxonomie updates te verzenden. Als u meerdere adressen wilt invoeren, scheidt u deze met komma&#39;s."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_email"
>title="E-mailadres"
>abstract="Dit adres wordt gebruikt om taxonomie updates te verzenden. Als u meerdere adressen wilt invoeren, scheidt u deze met komma&#39;s."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_account_name"
>title="Accountnaam"
>abstract="De naam van uw Pandora-account. Neem contact op met uw vertegenwoordiger van uw Pandora-account als u niet zeker weet wat uw accountnaam is. Gebruik geen spaties of speciale tekens."

### [!DNL Reddit] {#reddit}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_id"
>title="Advertentie-id bewerken"
>abstract="Je advertentie-id voor Reddit. Moet beginnen met &quot;t2_&quot; of &quot;a2_&quot;. Neem contact op met uw vertegenwoordiger van Reddit als u uw adverteerder-id niet kent."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_name"
>title="Naam van adverteerder wijzigen"
>abstract="De naam van uw reddit-adverteerder. Gebruik geen spaties of speciale tekens."

### Roku {#roku}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_email"
>title="E-mailadres van Roku-account"
>abstract="Voer het e-mailadres in dat aan uw Roku-account is gekoppeld."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_representative_email"
>title="E-mailadres van vertegenwoordiger van Roku-account"
>abstract="Voer het e-mailadres in van uw vertegenwoordiger van uw Roku-account. Dit adres wordt gebruikt om taxonomie updates te verzenden. Als u meerdere adressen wilt invoeren, scheidt u deze met komma&#39;s."

Vul de onderstaande velden in om details voor de bestemming te configureren.

![Platform UI-afbeelding die de ondersteunde id&#39;s voor de Roku-bestemming weergeeft.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-roku-fields.png)

* **[!UICONTROL Roku account email address]**: Voer het e-mailadres in dat aan uw Roku-account is gekoppeld.
* **[!UICONTROL Roku account representative email address]**: Voer het e-mailadres in van uw vertegenwoordiger van uw Roku-account. Als u meerdere adressen wilt invoeren, scheidt u deze met komma&#39;s.

### [!DNL Spotify] {#spotify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_client"
>title="Naam client"
>abstract="Uw naam van de adverteerderaccount, zoals u wilt dat deze aan de doelpartner wordt getoond. Gebruik uw bedrijfsnaam. Gebruik geen spaties of speciale tekens."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_account_token"
>title="Account-token"
>abstract="Een alfanumerieke id die Spotify meedeelt waar de gegevens moeten worden poort en u bent geverifieerd dat u deze workflow wilt gebruiken. Neem contact op met uw accountmanager voor Spotify om deze token te verkrijgen."

### [!DNL Taboola] {#taboola}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_taboola_rep_email"
>title="E-mailadres van accountmanager"
>abstract="Het e-mailadres van uw accountmanager van Taboola."

### [!DNL TargetSpot] {#targetspot}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_targetspot_client"
>title="Naam client"
>abstract="Uw naam van de adverteerderaccount, zoals u wilt dat deze aan de doelpartner wordt getoond. Gebruik uw bedrijfsnaam. Gebruik geen spaties of speciale tekens."

### [!DNL Teads] {#teads}

### [!DNL WB Discovery] {#wb-discovery}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_wb_client"
>title="Naam client"
>abstract="Uw naam van de adverteerderaccount, zoals u wilt dat deze aan de doelpartner wordt getoond. Gebruik uw bedrijfsnaam. Gebruik geen spaties of speciale tekens."

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Lees voor meer informatie over waarschuwingen de handleiding op [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

De [!DNL LiveRamp - Distribution] De verbinding activeert publiek dat reeds aan uw rekening LiveRamp door [LiveRamp - Onboarding](liveramp-onboarding.md) verbinding.

Als u uw publiek wilt activeren, moet u in deze stap de optie **zelfde publiek** die u eerder hebt aangemeld bij LiveRamp.

>[!IMPORTANT]
>
>Wanneer een publiek wordt geselecteerd dat nog niet eerder aan LiveRamp is toegewezen, wordt het instappen van het nieuwe publiek niet geactiveerd.

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Als u de activering van uw publiek wilt controleren en controleren, meldt u zich aan bij uw LiveRamp-account en controleert u de activeringsgegevens.

Als u vragen hebt over de activering van het publiek, neemt u contact op met uw accountvertegenwoordiger van LiveRamp.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Voor meer details over hoe te om uw te vormen [!DNL LiveRamp - Onboarding] opslaan, zie de [officiële documentatie](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
