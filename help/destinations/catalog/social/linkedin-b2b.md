---
title: (Bedrijven) LinkedIn connection
description: Gebruik dit doel om uw accountdoelgroepen te activeren voor gebruiksscenario's van Account-Based Marketing (ABM). Activeer profielen voor uw campagnes LinkedIn voor publiek gericht, verpersoonlijking, en onderdrukking, die op gehakte e-mails worden gebaseerd.
exl-id: 68d2cca3-952b-49d0-8ea2-e776a233b752
source-git-commit: 044306709747c32c4ce265d03d3908bbae169edc
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 2%

---

# (Bedrijven) LinkedIn Identieke verbinding van publiek {#companies-linkedin}

>[!AVAILABILITY]
>
>De functionaliteit om rekeningspubliek aan (Bedrijven) te activeren LinkedIn bestemming is beschikbaar voor bedrijven die [&#x200B; zaken-aan-Zaken &#x200B;](/help/rtcdp/overview.md#rtcdp-b2b) en [&#x200B; zaken-aan-persoon &#x200B;](/help/rtcdp/overview.md#rtcdp-b2p) uitgaven van Real-Time Customer Data Platform kopen.

Gebruik deze bestemming om uw [&#x200B; rekeningspubliek &#x200B;](/help/segmentation/types/account-audiences.md) voor Account-Based Marketing (ABM) gebruiksgevallen te activeren. Adverteer relevante personen en rollen in uw doelaccounts via de **[!UICONTROL (Companies) LinkedIn]** business-to-business bestemming. Bezoek de documentatie LinkedIn aan [&#x200B; leren meer over rekening richtend &#x200B;](https://business.linkedin.com/marketing-solutions/cx/21/10/ad-targeting/account-targeting) op het platform LinkedIn.

>[!TIP]
>
>Voor individueel-niveau (of zaken-aan-consument) gebruiksgevallen, adviseert Adobe dat u [&#x200B; LinkedIn Gelijke 1&rbrace; bestemming van het Publiek gebruikt.](/help/destinations/catalog/social/linkedin.md)

![&#x200B; LinkedIn rekeningsbestemming die in Experience Platform UI wordt getoond.](/help/destinations/assets/catalog/social/linkedin-b2b/linkedin-b2b-destination.png)

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Aangepaste uploads | X | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van Csv- dossiers. |

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

### Voorwaarden voor LinkedIn-accounts {#LinkedIn-account-prerequisites}

Voordat u het doel van [!UICONTROL (Companies) LinkedIn Matched Audience] kunt gebruiken, moet u ervoor zorgen dat uw [!DNL LinkedIn Campaign Manager] -account het machtigingsniveau [!DNL Creative Manager] of hoger heeft.

Leren hoe te om uw [!DNL LinkedIn Campaign Manager] gebruikerstoestemmingen uit te geven, zie [&#x200B; toevoegen, uitgeven, en verwijderen de Toestemmingen van de Gebruiker op de Rekeningen van Advertising &#x200B;](https://www.linkedin.com/help/lms/answer/5753) in de documentatie LinkedIn.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

1. Zoek het doel [!DNL (Companies) LinkedIn Matched Audiences] in de doelcatalogus en selecteer **[!UICONTROL Set Up]** .
2. Selecteer **[!UICONTROL Connect to destination]**.
   ![&#x200B; verifieer aan LinkedIn &#x200B;](/help/destinations/assets/catalog/social/linkedin-b2b/authenticate-linkedin-destination.png)
3. Ga uw geloofsbrieven LinkedIn in en selecteer **Login**.

Nadat u het aanmeldingsproces met LinkedIn hebt voltooid, kunt u doorgaan naar de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL LinkedIn Campaign Manager Account ID] . U kunt deze id vinden in uw [!DNL LinkedIn Campaign Manager] -account.

U kunt nu het accountpubliek activeren naar LinkedIn.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om rekeningspubliek aan bestemmingen te activeren.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om rekeningspubliek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer rekeningspubliek &#x200B;](/help/destinations/ui/activate-account-audiences.md) voor instructies bij het activeren van rekeningspubliek aan deze bestemming.

## Vereiste toewijzingsparen in de toewijzingsstap bij het activeren van accountpubliek naar de **[!UICONTROL (Companies) LinkedIn Matched Audiences]** -bestemming {#required-mappings}

Houd er bij het activeren van het accountpubliek naar het **[!UICONTROL (Companies) LinkedIn Matched Audiences]** -doel rekening mee dat de volgende twee toewijzingsparen verplicht zijn om gegevens te exporteren:

![&#x200B; LinkedIn afbeelding vereiste gebieden.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Source-veld | Doelveld |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (selecteer dit veld in de **[!UICONTROL Select Identity namespace]** -weergave wanneer u de **[!UICONTROL Target Field]** selecteert). <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om rekeningspubliek aan bestemmingen te activeren.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om rekeningspubliek aan bestemmingen te activeren."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

## Geëxporteerde gegevens {#exported-data}

Een succesvolle activering betekent dat een [!DNL LinkedIn] douanepubliek programmatically in [[!DNL LinkedIn Campaign Manager] &#x200B;](https://www.linkedin.com/campaignmanager/login) wordt gecreeerd. Het lidmaatschap van het publiek wordt aangepast omdat gebruikers gekwalificeerd zijn voor of gediskwalificeerd zijn voor het actieve publiek.
