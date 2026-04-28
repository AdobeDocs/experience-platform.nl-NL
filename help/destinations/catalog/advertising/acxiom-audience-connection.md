---
title: Acxiom Audience Connection
description: Gebruik de  [!DNL Acxiom Audience Connection]  bestemming om publiek met  [!DNL Acxiom]'s [!DNL Real ID]  technologie te verbeteren en hen over ad platforms te activeren.
source-git-commit: 71e655be2bdae3c89bd1652e2f83ab7bcc8c18fa
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 2%

---


# [!DNL Acxiom Audience Connection] doel

Gebruik de [!DNL Acxiom Audience Connection] bestemming om publiek met [!DNL Acxiom] [&#x200B; Echte ID™ &#x200B;](https://www.acxiom.com/real-id/real-id/) technologie te verbeteren. Vervolgens activeert u deze soorten publiek op verschillende platformen, zoals [!DNL Altice] , [!DNL Ampersand] , [!DNL Comcast] en meer.

>[!NOTE]
>
>Deze doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van [!DNL Acxiom] . Voor om het even welke onderzoeken of updateverzoeken, contact [!DNL Acxiom] direct in [&#x200B; acxiom-adobe-help@acxiom.com &#x200B;](mailto:acxiom-adobe-help@acxiom.com).

Voer de volgende stappen uit om een [!DNL Acxiom Audience Connection] doelconnector te maken met behulp van de gebruikersinterface van [!DNL Adobe Experience Platform] . Gebruik deze schakelaar om publiek aan geselecteerde bestemmingen te bouwen en te verspreiden.

## Gebruiksscenario&#39;s {#use-cases}

De volgende gebruiksgevallen laten zien hoe u het doel van [!DNL Acxiom Audience Connection] gebruikt.

### Soorten publiek verzenden vanuit [!DNL Experience Platform] naar uw [!DNL Acxiom] -account {#send-audiences}

Gebruik deze doelconnector om soorten publiek van [!DNL Experience Platform] naar uw [!DNL Acxiom] -account te verzenden voor aanschaf via meerdere kanalen.

Zo is de afdeling Marketing Operations van een wereldwijd merk voor financiële diensten geïnteresseerd in de aanschaf van klanten via meerdere reclameplatforms via verschillende kanalen. Ze kunnen de doelconnector van [!DNL Acxiom Audience Connection] gebruiken om een publiek van [!DNL Experience Platform] naar [!DNL Acxiom] te sturen, het publiek te verbeteren met de technologie van [!DNL Acxiom] s [!DNL Real ID] en het publiek te activeren op meerdere platforms, zoals [!DNL Altice] , [!DNL Ampersand] , [!DNL Comcast] en meer.

## Vereisten {#prerequisites}

Voordat u het doel van [!DNL Acxiom Audience Connection] configureert, moet u aan de volgende voorwaarden voldoen.

* **Bevestig termijnen van gebruik:** lees en onderteken [!DNL Acxiom] de Overeenkomst van het Gebruik van de Voorwaarden. U ontvangt de koppeling naar de overeenkomst zodra de uitgevoerde verkooporder is voltooid. Totdat u de overeenkomst ondertekent, wordt de [!DNL Acxiom Audience Connection] -doelkaart niet weergegeven in de [!DNL Experience Platform] -doelcatalogus. Nadat u de overeenkomst hebt geaccepteerd en ondertekend, voltooit [!DNL Adobe] de installatie en wordt de [!DNL Acxiom Audience Connection] -doelkaart zichtbaar.
* **weet uw [!DNL Adobe] organisatie identiteitskaart:** Uw [!DNL Adobe] organisatie identiteitskaart is nodig om uw Overeenkomst van het Gebruik te voltooien. Zie *Organisaties van 0&rbrace; &lbrace;in Experience Cloud* onderwerp voor details op hoe te [&#x200B; uw organisatie identiteitskaart &#x200B;](https://experienceleague.adobe.com/nl/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255) bekijken.[!DNL Adobe]

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
| --------- | ---------- | ---------- |
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de [!DNL Experience Platform] [&#x200B; Dienst van de Segmentatie &#x200B;](/help/segmentation/home.md). |
| Alle andere doelgroepen | Ja | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [&#x200B; diverse publieksoorsprong &#x200B;](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li>de douane uploadt publiek [&#x200B; ingevoerde &#x200B;](/help/segmentation/ui/audience-portal.md#import-audience) in [!DNL Experience Platform] van Csv- dossiers,</li><li>gelijksoortige doelgroepen,</li><li>federaal publiek,</li><li>publiek dat wordt gegenereerd in andere [!DNL Experience Platform] -toepassingen, zoals [!DNL Adobe Journey Optimizer] ,</li><li>en meer.</li></ul> |

{style="table-layout:auto"}

### Ondersteunde doelgroepen per gegevenstype {#supported-audiences-data-type}

In de volgende tabel wordt beschreven welke soorten publieksgegevens u naar dit doel kunt exporteren.

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
| -------------------- | ----------- | ------------- | ----------- |
| [&#x200B; het publiek van Mensen &#x200B;](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantprofielen. Gebruik deze om specifieke groepen mensen te kiezen voor marketingcampagnes. | Frequente kopers, winkeliers |
| [&#x200B; publiek van de Rekening &#x200B;](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [&#x200B; Het publiek van het Vooruitzicht &#x200B;](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [&#x200B; de uitvoer van de Dataset &#x200B;](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het [!DNL Adobe Experience Platform] Data Lake. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

In de volgende tabel staan het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
| ---- | ---- | ----- |
| Exporttype | **[!UICONTROL Audience export]** | Exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de [!DNL Acxiom Audience Connection] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Lees meer over [&#x200B; partij op dossier-gebaseerde bestemmingen &#x200B;](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Ondersteunde doelen {#supported-destinations}

Activeer het publiek naar de volgende platformen via de bestemming [!DNL Acxiom Audience Connection] .

* [!DNL Altice]
* [[!DNL Amazon]](#amazon)
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL Facebook]](#facebook)
* [[!DNL LG Ads]](#lg-ads)
* [[!DNL Pinterest]](#pinterest)
* [!DNL Spectrum]
* [!DNL Viant]
* [[!DNL Vizio]](#vizio)

## Verbinden met de bestemming {#connect}

[!DNL Experience Platform] handelt verificatie automatisch af voor uw [!DNL Acxiom Audience Connection] -doel.

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

## Doelspecifieke instellingen {#destination-settings}

Voor sommige [!DNL Acxiom Audience Connection] -doelen is aanvullende informatie vereist. De volgende secties verstrekken gedetailleerde begeleiding op hoe te om deze opties te vormen.

### [!DNL Amazon] {#amazon}

Om details voor de bestemming te vormen, voltooi de volgende gebieden.

* **[!UICONTROL Publisher Account ID]** : Voer de uitgevers-account-id in die aan dit doel is gekoppeld.

  ![&#x200B; Schermafbeelding van het [!DNL Amazon] paneel van bestemmingsdetails die het gebied van identiteitskaart van de Rekening van de Uitgever tonen.](../../assets/catalog/advertising/acxiom-audience-distribution/amazon_destination_details.png){zoomable="yes"}

### [!DNL Facebook] {#facebook}

Om details voor de bestemming te vormen, voltooi de volgende gebieden.

* **[!UICONTROL Destination Account ID]** : Voer de id van de doelaccount voor deze bestemming in.

  ![&#x200B; Schermafbeelding van het [!DNL Facebook] paneel dat van bestemmingsdetails het gebied van identiteitskaart van de Rekening van de Bestemming toont.](../../assets/catalog/advertising/acxiom-audience-distribution/facebook_destination_details.png){zoomable="yes"}

### [!DNL LG Ads] {#lg-ads}

Om details voor de bestemming te vormen, voltooi de volgende gebieden.

* **[!UICONTROL Segment Category]** : De doelcategorie of -verticaal waar uw segment in valt. Voorbeeld: financiële diensten, auto&#39;s of gezondheid.

  ![&#x200B; Schermafbeelding van het [!DNL LG Ads] paneel dat van bestemmingsdetails het gebied van de Categorie van het Segment toont.](../../assets/catalog/advertising/acxiom-audience-distribution/lg_ads_destination_details.png){zoomable="yes"}

### [!DNL Pinterest] {#pinterest}

Om details voor de bestemming te vormen, voltooi de volgende gebieden.

* **[!UICONTROL Destination Account ID]** : Voer de id van de doelaccount voor deze bestemming in.

  ![&#x200B; Schermafbeelding van het [!DNL Pinterest] paneel dat van bestemmingsdetails het gebied van identiteitskaart van de Rekening van de Bestemming toont.](../../assets/catalog/advertising/acxiom-audience-distribution/pinterest_destination_details.png){zoomable="yes"}

### [!DNL Vizio] {#vizio}

Om details voor de bestemming te vormen, voltooi de volgende gebieden.

* **[!UICONTROL Advertiser Name]** : Voer de naam van de adverteerder voor dit doel in.

  ![&#x200B; Schermafbeelding van het [!DNL Vizio] paneel dat van bestemmingsdetails het Advertiser gebied van de Naam toont.](../../assets/catalog/advertising/acxiom-audience-distribution/vizio_destination_details.png){zoomable="yes"}

## Soorten publiek naar dit doel activeren {#activate}

Lees [&#x200B; activeer publieksgegevens aan de uitvoerbestemmingen van het partijprofiel &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png){width="100" zoomable="yes"}

>[!NOTE]
>
>Het doel [!DNL Acxiom Audience Connection] ondersteunt alleen het exporteren van volledige bestanden.

### Kenmerken en identiteiten toewijzen {#map}

Als u publieksgegevens correct wilt ontvangen, wijst u de bronvelden van [!DNL Experience Platform] toe aan de juiste doelvelden van [!DNL Acxiom Audience Connection] .

De volgende doelvelden worden automatisch vooraf ingevuld in de volgorde die [!DNL Acxiom] vereist. U moet een bronveld toewijzen aan elk doelveld om de activeringsstroom te voltooien.

>[!IMPORTANT]
>
>Alle doelvelden moeten worden toegewezen in de gebruikersinterface. Alleen voor **[!UICONTROL Last Name]** , **[!UICONTROL Address Line 1]** , **[!UICONTROL City]** , **[!UICONTROL State]** en **[!UICONTROL Zip Code]** zijn echter werkelijke gegevens in uw profielschema nodig. Wijs om het even welk beschikbaar brongebied aan de resterende doelgebieden toe om aan het vereiste UI te voldoen.

| Veldnaam | Beschrijving | Vereist door de gebruikersinterface | Vereiste gegevens voor verwerking | Veldvolgorde | Max. lengte |
| -------------------- | ------------ | ------------------ | ---------------------------- | ----------- | ---------- |
| Voornaam | Voornaam van individu | Ja | Nee | 1 | 255 |
| Midden | Tweede voornaam of initiaal van de persoon | Ja | Nee | 2 | 50 |
| Achternaam | Achternaam van de persoon | Ja | **ja** | 3 | 255 |
| Algemeen achtervoegsel | Achtervoegsel van de persoon | Ja | Nee | 4 | 10 |
| Adresregel 1 | Adres 1 veld primaire woonplaats | Ja | **ja** | 5 | 255 |
| Adresregel 2 | Adres 2 veld primaire woonplaats | Ja | Nee | 6 | 255 |
| Plaats | Plaats van primaire woonplaats | Ja | **ja** | 7 | 255 |
| Staat | Afkorting van de primaire verblijfplaats | Ja | **ja** | 8 | 2 |
| Postcode | Volledige postcode van primaire verblijfplaats | Ja | **ja** | 9 | 10 |
| E-mail | Primaire e-mail. Standaard wordt dit veld gebruikt als een deduplicatietoets om de records uniek te maken. | Ja | Nee | 10 | 255 |
| Telefoon | Telefoonnummer van individu (netnummer + nummer). Standaard wordt dit veld gebruikt als een deduplicatietoets om de records uniek te maken. | Ja | Nee | 11 | 10 |

{style="table-layout:auto"}

Voer in de kolom **[!UICONTROL Source Field]** de naam in van elk bronkenmerk dat u wilt toewijzen aan het corresponderende doelveld. Of selecteer **[!UICONTROL Select source field]** om door beschikbare bronvelden te bladeren.

![&#x200B; het scherm dat van de afbeelding bron en doelgebiedkolommen toont met [!DNL Acxiom] vereiste gebieden die voor de [!DNL Acxiom Audience Connection] bestemming worden voorbevolkt.](../../assets/catalog/advertising/acxiom-audience-distribution/mapping_screen.png){zoomable="yes"}

Selecteer **[!UICONTROL Next]** nadat u alle velden hebt toegewezen.

Om een niet-standaardschema te gebruiken, zie de [&#x200B; gids UI van de Dienst van de Vraag &#x200B;](/help/query-service/ui/overview.md) om uw gebiedsnamen aan het [!DNL Adobe] standaardschema in kaart te brengen.

### Uw bestemming bekijken {#review}

Nadat u alle stappen hebt uitgevoerd, controleert u de status van de doelverbinding en de publieksgegevens voordat u deze activeert. Het geselecteerde publiek verschijnt in een lijst. Elk publiek is een aparte aanroep van de [!DNL Acxiom Audience Connection] API.

Als u tevreden bent met het resultaat, selecteert u **[!UICONTROL Finish]** om uw doel te activeren.

![&#x200B; herzie uw publieksscherm die de status van de bestemmingsverbinding en geselecteerde publiek tonen.](../../assets/catalog/advertising/acxiom-audience-distribution/review_audience.png){zoomable="yes"}

## Problemen oplossen {#troubleshooting}

Als uw doelvertegenwoordiger uw publiek niet kan vinden, neemt u contact op met uw [!DNL Adobe] -vertegenwoordiger voor hulp.

Geef de volgende informatie op aan uw [!DNL Adobe] vertegenwoordiger:

* Naam publiek
* Doelnaam
* Activeringsdatum publiek
* Geëxporteerde bestandsnaam

## Volgende stappen {#next-steps}

U hebt een publiek geactiveerd voor het geselecteerde doelplatform. Neem vervolgens contact op met de vertegenwoordiger van het doelplatform om uw campagne in te stellen.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).
