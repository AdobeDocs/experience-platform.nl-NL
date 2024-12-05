---
title: (Bedrijven) LinkedIn-verbinding
description: Gebruik dit doel om uw accountdoelgroepen te activeren voor gebruiksscenario's van Account-Based Marketing (ABM). Activeer profielen voor uw LinkedIn-campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P Edition" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
source-git-commit: e45c50a6447be4a60145eea6956d30d51166e675
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 2%

---

# (Bedrijven) LinkedIn-verbinding voor iedereen {#companies-linkedin}

>[!AVAILABILITY]
>
>De functionaliteit om rekeningspubliek aan de (Bedrijven) bestemming van LinkedIn te activeren is beschikbaar voor bedrijven die [ zaken-aan-Zaken ](/help/rtcdp/overview.md#rtcdp-b2b) en [ zaken-aan-Persoon ](/help/rtcdp/overview.md#rtcdp-b2p) uitgaven van Real-time Customer Data Platform kopen.

Gebruik deze bestemming om uw [ rekeningspubliek ](/help/segmentation/ui/account-audiences.md) voor Account-Based Marketing (ABM) gebruiksgevallen te activeren. Adverteer relevante personen en rollen in uw doelaccounts via de **[!UICONTROL (Companies) LinkedIn]** business-to-business bestemming. Bezoek de documentatie van LinkedIn aan [ meer over rekening het richten ](https://business.linkedin.com/marketing-solutions/cx/21/10/ad-targeting/account-targeting) op het platform van LinkedIn leren.

>[!TIP]
>
>Voor individueel-niveau (of zaken-aan-consument) gebruiksgevallen, adviseert de Adobe dat u de [ LinkedIn Gelijke bestemming van het publiek ](/help/destinations/catalog/social/linkedin.md) gebruikt.

![ de rekeningsbestemming van LinkedIn die in het Experience Platform UI wordt getoond.](/help/destinations/assets/catalog/social/linkedin-b2b/linkedin-b2b-destination.png)

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van het Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | X | Het publiek [ ingevoerde ](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-and-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|--------------|-----------|---------------------------|
| Exporttype | Publiek exporteren | Alle publieksleden zullen met zeer belangrijke herkenningstekens zoals naam, telefoonaantal, en meer worden uitgevoerd. |
| Frequentie | Streaming | &quot;Altijd aan&quot; API-gebaseerde verbindingen. Updates worden direct na het wijzigen van het profiel verzonden. |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

Zorg ervoor dat u aan de onderstaande voorwaarden voldoet om accountpubliek naar LinkedIn te exporteren:

### Voorwaarden voor linkedIn-accounts {#LinkedIn-account-prerequisites}

Voordat u het doel van [!UICONTROL (Companies) LinkedIn Matched Audience] kunt gebruiken, moet u ervoor zorgen dat uw [!DNL LinkedIn Campaign Manager] -account het machtigingsniveau [!DNL Creative Manager] of hoger heeft.

Leren hoe te om uw [!DNL LinkedIn Campaign Manager] gebruikerstoestemmingen uit te geven, zie [ toevoegen, uitgeven, en verwijderen de Toestemmingen van de Gebruiker op de Rekeningen van Advertising ](https://www.linkedin.com/help/lms/answer/5753) in de documentatie van LinkedIn.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

1. Zoek het doel [!DNL (Companies) LinkedIn Matched Audiences] in de doelcatalogus en selecteer **[!UICONTROL Set Up]** .
2. Selecteer **[!UICONTROL Connect to destination]**.
   ![ verifieer aan LinkedIn ](/help/destinations/assets/catalog/social/linkedin-b2b/authenticate-linkedin-destination.png)
3. Ga uw geloofsbrieven van LinkedIn in en selecteer **Login**.

Nadat u het aanmeldingsproces met LinkedIn hebt voltooid, kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL LinkedIn Campaign Manager Account ID] . U kunt deze id vinden in uw [!DNL LinkedIn Campaign Manager] -account.

U kunt nu accountsoorten activeren voor LinkedIn.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om rekeningspubliek aan bestemmingen te activeren.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om rekeningspubliek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer rekeningspubliek ](/help/destinations/ui/activate-account-audiences.md) voor instructies bij het activeren van rekeningspubliek aan deze bestemming.

## Vereiste toewijzingsparen in de toewijzingsstap bij het activeren van accountpubliek naar de **[!UICONTROL (Companies) LinkedIn Matched Audiences]** -bestemming {#required-mappings}

Houd er bij het activeren van het accountpubliek naar het **[!UICONTROL (Companies) LinkedIn Matched Audiences]** -doel rekening mee dat de volgende twee toewijzingsparen verplicht zijn om gegevens te exporteren:

![ de afbeelding van LinkedIn vereiste gebieden.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Source-veld | Doelveld |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (selecteer dit veld in de **[!UICONTROL Select Identity namespace]** -weergave wanneer u de **[!UICONTROL Target Field]** selecteert). <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om rekeningspubliek aan bestemmingen te activeren.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om rekeningspubliek aan bestemmingen te activeren."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

## Geëxporteerde gegevens {#exported-data}

Een succesvolle activering betekent dat een [!DNL LinkedIn] douanepubliek programmatically in [[!DNL LinkedIn Campaign Manager] ](https://www.linkedin.com/campaignmanager/login) wordt gecreeerd. Het lidmaatschap van het publiek wordt aangepast omdat gebruikers gekwalificeerd zijn voor of gediskwalificeerd zijn voor het actieve publiek.