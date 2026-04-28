---
title: Acxiom Real ID&trade Poortverbinding
description: Gebruik de  [!DNL Acxiom Real ID&trade; Audience Connection]  bestemming om publiek over platforms zoals  [!DNL Altice] te verbeteren en te activeren,  [!DNL Ampersand], en  [!DNL Comcast].
source-git-commit: 3aefb36bbf525a5eebe3a9330e25587501167a64
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 0%

---


# [!DNL Acxiom Real ID™ Audience Connection] doel

Gebruik de [!DNL Acxiom Real ID Audience Connection] bestemming om publiek met [!DNL Acxiom] [&#x200B; Echte ID™ &#x200B;](https://www.acxiom.com/real-id/real-id/) technologie te verbeteren. Vervolgens activeert u deze soorten publiek op verschillende platformen, zoals [!DNL Altice] , [!DNL Ampersand] , [!DNL Comcast] en meer.

>[!NOTE]
>
>Deze doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van [!DNL Acxiom] . Voor om het even welke onderzoeken of updateverzoeken, contact [!DNL Acxiom] direct in [&#x200B; acxiom-adobe-help@acxiom.com &#x200B;](mailto:acxiom-adobe-help@acxiom.com).

Voer de volgende stappen uit om een [!DNL Acxiom Real ID Audience Connection] doelconnector te maken met behulp van de gebruikersinterface van [!DNL Adobe Experience Platform] . Gebruik deze schakelaar om publiek aan geselecteerde bestemmingen te bouwen en te verspreiden.

## Gebruiksscenario&#39;s {#use-cases}

Gebruik dit doel als u [!DNL Real ID] van [!DNL Acxiom] als id in [!DNL Real-Time CDP] hebt geladen. De volgende gebruiksgevallen laten zien hoe u het doel van [!DNL Acxiom Real ID Audience Connection] kunt gebruiken.

### Soorten publiek verzenden vanuit [!DNL Experience Platform] naar uw [!DNL Acxiom] -account {#send-audiences}

Gebruik deze doelconnector om soorten publiek van [!DNL Experience Platform] naar uw [!DNL Acxiom] -account te verzenden voor aanschaf via meerdere kanalen.

Zo is de afdeling Marketing Operations van een wereldwijd merk voor financiële diensten geïnteresseerd in de aanschaf van klanten via meerdere reclameplatforms via verschillende kanalen. Ze kunnen de doelconnector van [!DNL Acxiom Real ID Audience Connection] gebruiken om een publiek van [!DNL Experience Platform] naar [!DNL Acxiom] te sturen, het publiek te verbeteren met de technologie van [!DNL Acxiom] s [!DNL Real ID] en het publiek te activeren op meerdere platforms, zoals [!DNL Altice] , [!DNL Ampersand] , [!DNL Comcast] en meer.

## Vereisten {#prerequisites}

Voordat u het doel van [!DNL Acxiom Real ID Audience Connection] configureert, moet u aan de volgende voorwaarden voldoen.

* **Bevestig termijnen van gebruik:** lees en onderteken [!DNL Acxiom] de Overeenkomst van het Gebruik van de Voorwaarden. U ontvangt de koppeling naar de overeenkomst zodra de uitgevoerde verkooporder is voltooid. Totdat u de overeenkomst ondertekent, wordt de [!DNL Acxiom Real ID Audience Connection] -doelkaart niet weergegeven in de [!DNL Experience Platform] -doelcatalogus. Nadat u de overeenkomst hebt geaccepteerd en ondertekend, voltooit [!DNL Adobe] de installatie en wordt de [!DNL Acxiom Real ID Audience Connection] -doelkaart zichtbaar.
* **weet uw [!DNL Adobe] organisatie identiteitskaart:** Uw [!DNL Adobe] organisatie identiteitskaart is nodig om uw Overeenkomst van het Gebruik te voltooien. Zie *Organisaties van 0&rbrace; &lbrace;in Experience Cloud* onderwerp voor details op hoe te [&#x200B; uw organisatie identiteitskaart &#x200B;](https://experienceleague.adobe.com/nl/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255) bekijken.[!DNL Adobe]
* **verkrijg een vergunning voor [!DNL Acxiom] [!DNL Real ID] product:** nadat u een vergunning verkrijgt, maak [!DNL Acxiom] [!DNL Real ID] beschikbaar binnen [!DNL Real-Time CDP]. Zie [&#x200B; Verbetering van Gegevens van Acxiom &#x200B;](/help/destinations/catalog/data-partner/acxiom-data-enhancement.md) voor details.

## Ondersteunde identiteiten {#supported-identities}

De [!DNL Real ID] Audience Connection-bestemming van [!DNL Acxiom] ondersteunt de volgende identiteitsbewerkingen. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
| --------------- | ----------- | -------------- |
| [!DNL Real ID] | [!DNL Real ID] | Wijs een bronveld toe aan deze doelidentiteit. Het bronveld kan een [!DNL Acxiom] [!DNL Real ID] of een aangepaste id zijn. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
| --------------- | --------- | ----------- |
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de [!DNL Experience Platform] [&#x200B; Dienst van de Segmentatie &#x200B;](/help/segmentation/home.md). |
| Alle andere doelgroepen | Ja | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [&#x200B; diverse publieksoorsprong &#x200B;](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li>de douane uploadt publiek [&#x200B; ingevoerde &#x200B;](/help/segmentation/ui/audience-portal.md#import-audience) in [!DNL Experience Platform] van Csv- dossiers,</li><li>gelijksoortige doelgroepen,</li><li>federaal publiek,</li><li>publiek dat wordt gegenereerd in andere [!DNL Experience Platform] -toepassingen, zoals [!DNL Adobe Journey Optimizer] ,</li><li>en meer.</li></ul> |

{style="table-layout:auto"}

### Ondersteunde doelgroepen per gegevenstype {#supported-audiences-data-type}

In de volgende tabel wordt beschreven welke soorten publieksgegevens u naar dit doel kunt exporteren.

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
| -------------------- | --------- | ----------- | --------- |
| [&#x200B; het publiek van Mensen &#x200B;](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantprofielen. Gebruik deze om specifieke groepen mensen te kiezen voor marketingcampagnes. | Frequente kopers, winkeliers |
| [&#x200B; publiek van de Rekening &#x200B;](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [&#x200B; Het publiek van het Vooruitzicht &#x200B;](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [&#x200B; de uitvoer van de Dataset &#x200B;](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het [!DNL Adobe Experience Platform] Data Lake. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

In de volgende tabel staan het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
| ---- | ---- | ----- |
| Exporttype | **[!UICONTROL Audience export]** | Exporteert alle leden van een publiek met de id&#39;s die in het doel [!DNL Acxiom Real ID Audience Connection] worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Lees meer over [&#x200B; partij op dossier-gebaseerde bestemmingen &#x200B;](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Ondersteunde doelen {#supported-destinations}

Activeer het publiek naar de volgende platformen via de bestemming [!DNL Acxiom Real ID Audience Connection] .

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

[!DNL Experience Platform] handelt verificatie automatisch af voor uw [!DNL Acxiom Real ID Audience Connection] -doel.

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

## Doelspecifieke instellingen {#destination-settings}

Voor sommige [!DNL Acxiom Real ID Audience Connection] -doelen is aanvullende informatie vereist. De volgende secties verstrekken gedetailleerde begeleiding op hoe te om deze opties te vormen.

### [!DNL Amazon] {#amazon}

Om details voor de bestemming te vormen, voltooi de volgende gebieden.

* **[!UICONTROL Publisher Account ID]** : Voer de uitgevers-account-id in die aan dit doel is gekoppeld.

  ![&#x200B; Schermafbeelding van het [!DNL Amazon] paneel van bestemmingsdetails die het gebied van identiteitskaart van de Rekening van de Uitgever tonen.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_amazon_destination_details.png){zoomable="yes"}

### [!DNL Facebook] {#facebook}

Om details voor de bestemming te vormen, voltooi de volgende gebieden.

* **[!UICONTROL Destination Account ID]** : Voer de id van de doelaccount voor deze bestemming in.

  ![&#x200B; Schermafbeelding van het [!DNL Facebook] paneel dat van bestemmingsdetails het gebied van identiteitskaart van de Rekening van de Bestemming toont.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_facebook_destination_details.png){zoomable="yes"}

### [!DNL LG Ads] {#lg-ads}

Om details voor de bestemming te vormen, voltooi de volgende gebieden.

* **[!UICONTROL Segment Category]** : De doelcategorie of -verticaal waar uw segment in valt. Voorbeeld: financiële diensten, auto&#39;s of gezondheid.

  ![&#x200B; Schermafbeelding van het [!DNL LG Ads] paneel dat van bestemmingsdetails het gebied van de Categorie van het Segment toont.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_lg_ads_destination_details.png){zoomable="yes"}

### [!DNL Pinterest] {#pinterest}

Om details voor de bestemming te vormen, voltooi de volgende gebieden.

* **[!UICONTROL Destination Account ID]** : Voer de id van de doelaccount voor deze bestemming in.

  ![&#x200B; Schermafbeelding van het [!DNL Pinterest] paneel dat van bestemmingsdetails het gebied van identiteitskaart van de Rekening van de Bestemming toont.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_pinterest_destination_details.png){zoomable="yes"}

### [!DNL Vizio] {#vizio}

Om details voor de bestemming te vormen, voltooi de volgende gebieden.

* **[!UICONTROL Advertiser Name]** : Voer de naam van de adverteerder voor dit doel in.

  ![&#x200B; Schermafbeelding van het [!DNL Vizio] paneel dat van bestemmingsdetails het Advertiser gebied van de Naam toont.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_vizio_destination_details.png){zoomable="yes"}

## Soorten publiek naar dit doel activeren {#activate}

Lees [&#x200B; activeer publieksgegevens aan de uitvoerbestemmingen van het partijprofiel &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png){width="100" zoomable="yes"}

>[!NOTE]
>
>Het doel [!DNL Acxiom Real ID Audience Connection] ondersteunt alleen het exporteren van volledige bestanden.

### Kenmerken en identiteiten toewijzen {#map}

Wijs het bronveld van [!DNL Experience Platform] toe aan het juiste doelveld [!DNL Acxiom Real ID Audience Connection] zodat het doel van [!DNL Acxiom Real ID Audience Connection] de publieksgegevens correct kan ontvangen.

Het doelveld **[!UICONTROL Real ID]** wordt automatisch vooraf ingevuld in de toewijzingsstap. Wijs het bronveld toe: Een aangepaste id-naamruimte of een werkelijke [!DNL Acxiom] [!DNL Real ID] die is opgeslagen in uw profielschema.

| Veldnaam | Beschrijving | Vereist |
| ---------- | ----------- | -------- |
| [!DNL Real ID] | Een [!DNL Real ID] is een unieke alfanumerieke id van 36 bytes uit de grafiek met de resolutie van uw identiteit van [!DNL Acxiom] . Het is een id die een persoon, huishouden of adres vertegenwoordigt. | Ja |

{style="table-layout:auto"}

Voer in de kolom **[!UICONTROL Source Field]** de naam in van het bronkenmerk dat u wilt toewijzen aan het doelveld van **[!UICONTROL Real ID]** . Of selecteer **[!UICONTROL Select source field]** om door beschikbare bronvelden te bladeren. Selecteer vervolgens **[!UICONTROL Next]** .

![&#x200B; Schermafbeelding van het kaartscherm die de [!UICONTROL Source Field] kolom en het [!UICONTROL Select source field] paneel tonen.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_mapping_screen.png){zoomable="yes"}

Als u niet het standaardschema van [!DNL Adobe] gebruikt, zie de [&#x200B; gids UI van de Dienst van de Vraag &#x200B;](/help/query-service/ui/overview.md) om het [!DNL Adobe] standaardschema met uw gebiedsnamen te bevolken.

### Uw bestemming bekijken {#review}

Nadat u alle stappen hebt uitgevoerd, controleert u de status van de doelverbinding en de publieksgegevens voordat u deze activeert. Het geselecteerde publiek verschijnt in een lijst. Elk publiek is een aparte aanroep van de [!DNL Acxiom Real ID Audience Connection] API.

Wanneer de resultaten er goed uitzien, selecteert u **[!UICONTROL Finish]** om de bestemming te activeren.

![&#x200B; Schermafbeelding van het scherm van het Overzicht die de status van de bestemmingsverbinding en de geselecteerde soorten publiek tonen vóór activering.](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_review_audience.png){zoomable="yes"}

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
