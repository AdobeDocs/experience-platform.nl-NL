---
keywords: gekoppeld in verbinding;gekoppeld in verbinding;gekoppeld in doelen;gekoppeld in;
title: Koppeling in verbinding met passend publiek
description: Activeer profielen voor uw LinkedIn-campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 74d7c48042b0d2b938705b588c185f3c3f96f1cd
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 0%

---

# [!DNL LinkedIn Matched Audiences] verbinding

## Overzicht {#overview}

Activeer profielen voor uw [!DNL LinkedIn] -campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails en mobiele id&#39;s.

![ bestemming van LinkedIn in Adobe Experience Platform UI ](../../assets/catalog/social/linkedin/catalog.png)

## Gebruiksscenario’s

Om u beter te helpen begrijpen hoe en wanneer om de [!DNL LinkedIn Matched Audiences] bestemming te gebruiken, is hier een gebruiksgeval dat de klanten van Adobe Experience Platform door deze eigenschap kunnen oplossen.

Een softwarebedrijf organiseert een conferentie en wil met deelnemers in contact blijven, en hen gepersonaliseerde aanbiedingen tonen die op hun status van de conferentieaanwezigheid worden gebaseerd. Het bedrijf kan e-mailadressen of mobiele apparaat-id&#39;s van eigen [!DNL CRM] invoeren in Adobe Experience Platform. Vervolgens kunnen ze publiek maken op basis van hun eigen offline gegevens en deze soorten publiek naar het [!DNL LinkedIn] sociale platform sturen, zodat hun advertentie-uitgaven geoptimaliseerd worden.

## Ondersteunde identiteiten {#supported-identities}

[!DNL LinkedIn Matched Audiences] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Selecteer deze doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer deze doelidentiteit wanneer uw bronidentiteit een IDFA-naamruimte is. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Volg de instructies in de [ passende vereisten van identiteitskaart ](#id-matching-requirements-id-matching-requirements) sectie en gebruik aangewezen namespaces voor gewone teksten en gehakte e-mails, respectievelijk. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Platform] . |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van het Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer en andere) die in de [!DNL LinkedIn Matched Audiences] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voorwaarden voor linkedIn-accounts {#LinkedIn-account-prerequisites}

Voordat u het doel van [!UICONTROL LinkedIn Matched Audience] kunt gebruiken, moet u ervoor zorgen dat uw [!DNL LinkedIn Campaign Manager] -account het machtigingsniveau [!DNL Creative Manager] of hoger heeft.

Leren hoe te om uw [!DNL LinkedIn Campaign Manager] gebruikerstoestemmingen uit te geven, zie [ toevoegen, uitgeven, en verwijderen de Toestemmingen van de Gebruiker op de Rekeningen van Advertising ](https://www.linkedin.com/help/lms/answer/5753) in de documentatie van LinkedIn.

## Vereisten voor id-afstemming {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] vereist dat er geen PII&#39;s (Personal Identified Information) worden verzonden. Daarom kan het publiek dat aan [!DNL LinkedIn Matched Audiences] wordt geactiveerd van *gehakt* herkenningstekens, zoals e-mailadressen of mobiele apparaat IDs worden afgevinkt.

Afhankelijk van het type id&#39;s dat u in Adobe Experience Platform invoert, moet u aan de desbetreffende vereisten voldoen.

## E-mailhashingvereisten {#email-hashing-requirements}

U kunt e-mailadressen hashen alvorens hen in Adobe Experience Platform op te nemen, of e-mailadressen gebruiken duidelijk in Experience Platform, en [!DNL Platform] hen hebben hakt bij activering.

Om over het opnemen van e-mailadressen in Experience Platform te leren, zie het [ overzicht van de partijopname ](/help/ingestion/batch-ingestion/overview.md) en [ het stromen ingestitieoverzicht ](/help/ingestion/streaming-ingestion/overview.md).

Als u ervoor kiest om de e-mailadressen zelf te hashen, moet u aan de volgende vereisten voldoen:

* Snijd alle spaties aan het begin en aan het einde van de e-mailtekenreeks bij. Bijvoorbeeld: `johndoe@example.com` , niet `<space>johndoe@example.com<space>` ;
* Wanneer u de e-mailtekenreeksen hasht, moet u ervoor zorgen dat de kleine-lettertekenreeks wordt gehaseerd.
   * Voorbeeld: `example@email.com` , not `EXAMPLE@EMAIL.COM` ;
* Zorg ervoor dat de hashtekenreeks alleen in kleine letters wordt weergegeven
   * Voorbeeld: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149` , not `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149` ;
* Zilp de tekenreeks niet.

>[!NOTE]
>
>Gegevens uit naamruimten zonder hashing worden automatisch gehasht door [!DNL Platform] bij activering.
> Kenmerkbrongegevens worden niet automatisch gehasht.
> 
> Tijdens de [ stap van de Toewijzing van de Identiteit ](../../ui/activate-segment-streaming-destinations.md#mapping), wanneer uw brongebied unhashed attributen bevat, controleer de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] automatisch de gegevens bij activering te hebben.
> 
> De optie **[!UICONTROL Apply transformation]** wordt alleen weergegeven wanneer u kenmerken als bronvelden selecteert. Deze wordt niet weergegeven wanneer u naamruimten kiest.

![ de afbeeldingstransformatie van de Identiteit ](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

In de onderstaande video ziet u ook de stappen voor het configureren van een [!DNL LinkedIn Matched Audiences] -bestemming en het activeren van het publiek.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>De gebruikersinterface van het Experience Platform wordt vaak bijgewerkt en kan sinds de opname van deze video zijn veranderd. Voor de meest bijgewerkte informatie, verwijs naar het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md).

### Verifiëren voor bestemming {#authenticate}

1. Zoek het doel [!DNL LinkedIn Matched Audiences] in de doelcatalogus en selecteer **[!UICONTROL Set Up]** .
2. Selecteer **[!UICONTROL Connect to destination]**.
   ![ verifieer aan LinkedIn ](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Ga uw geloofsbrieven van LinkedIn in en selecteer **Login**.

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="Account-id"
>abstract="Je account-id voor LinkedIn Campagne Manager. U kunt deze id vinden in uw LinkedIn Campaign Manager-account."

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL LinkedIn Campaign Manager Account ID] . U kunt deze id vinden in uw [!DNL LinkedIn Campaign Manager] -account.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [ publieksgegevens aan het stromen publiek de uitvoerbestemmingen ](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

## Geëxporteerde gegevens {#exported-data}

Een succesvolle activering betekent dat een [!DNL LinkedIn] douanepubliek programmatically in [[!DNL LinkedIn Campaign Manager] ](https://www.linkedin.com/campaignmanager/login) wordt gecreeerd. Het lidmaatschap van het publiek wordt aangepast omdat gebruikers gekwalificeerd zijn voor of gediskwalificeerd zijn voor het actieve publiek.

>[!TIP]
>
>De integratie tussen Adobe Experience Platform en [!DNL LinkedIn Matched Audiences] ondersteunt historische publieksbackfills. Alle historische publiekskwalificaties worden naar [!DNL LinkedIn] verzonden wanneer u het publiek activeert naar het doel.
