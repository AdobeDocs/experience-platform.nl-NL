---
keywords: gekoppeld in verbinding;gekoppeld in verbinding;gekoppeld in doelen;gekoppeld in;
title: Koppeling in verbinding met passend publiek
description: Activeer profielen voor uw campagnes LinkedIn voor publiek gericht, verpersoonlijking, en onderdrukking, die op gehakte e-mails worden gebaseerd.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 1%

---

# [!DNL LinkedIn Matched Audiences]-verbinding

## Overzicht {#overview}

Activeer profielen voor uw [!DNL LinkedIn] -campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails en mobiele id&#39;s.

![&#x200B; LinkedIn bestemming in Adobe Experience Platform UI &#x200B;](../../assets/catalog/social/linkedin/catalog.png)

## Gebruiksscenario’s

Om u beter te helpen begrijpen hoe en wanneer om de [!DNL LinkedIn Matched Audiences] bestemming te gebruiken, is hier een gebruiksgeval dat de klanten van Adobe Experience Platform door deze eigenschap kunnen oplossen.

Een softwarebedrijf organiseert een conferentie en wil met deelnemers in contact blijven, en hen gepersonaliseerde aanbiedingen tonen die op hun status van de conferentieaanwezigheid worden gebaseerd. Het bedrijf kan e-mailadressen of mobiele apparaat-id&#39;s van eigen [!DNL CRM] invoeren in Adobe Experience Platform. Vervolgens kunnen ze publiek maken op basis van hun eigen offline gegevens en deze soorten publiek naar het [!DNL LinkedIn] sociale platform sturen, zodat hun advertentie-uitgaven geoptimaliseerd worden.

## Ondersteunde identiteiten {#supported-identities}

[!DNL LinkedIn Matched Audiences] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

>[!IMPORTANT]
>
>Vanaf september 2025 kunt u [!DNL IDFA] niet meer toewijzen als doelidentiteit, aangezien [!DNL IDFA] niet meer wordt ondersteund door het doel van [!DNL LinkedIn Matched Audiences] . Zie de [!DNL LinkedIn Matched Audiences] integratie [&#x200B; documentatie &#x200B;](https://learn.microsoft.com/en-us/linkedin/marketing/matched-audiences/create-and-manage-segment-users?view=li-lms-2025-07&tabs=http#idtypes) voor meer details. Deze wijziging is het gevolg van LinkedIn&#39;s vereisten en is niet gerelateerd aan Experience Platform-upgrades van de bestemmingsservice.


| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Selecteer deze doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Volg de instructies in de [&#x200B; passende vereisten van identiteitskaart &#x200B;](#id-matching-requirements-id-matching-requirements) sectie en gebruik aangewezen namespaces voor gewone teksten en gehakte e-mails, respectievelijk. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer en andere) die in de [!DNL LinkedIn Matched Audiences] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voorwaarden voor LinkedIn-accounts {#LinkedIn-account-prerequisites}

Voordat u het doel van [!UICONTROL LinkedIn Matched Audience] kunt gebruiken, moet u ervoor zorgen dat uw [!DNL LinkedIn Campaign Manager] -account het machtigingsniveau [!DNL Creative Manager] of hoger heeft.

Leren hoe te om uw [!DNL LinkedIn Campaign Manager] gebruikerstoestemmingen uit te geven, zie [&#x200B; toevoegen, uitgeven, en verwijderen de Toestemmingen van de Gebruiker op de Rekeningen van Advertising &#x200B;](https://www.linkedin.com/help/lms/answer/5753) in de documentatie LinkedIn.

## Vereisten voor id-afstemming {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] vereist dat er geen PII&#39;s (Personal Identified Information) worden verzonden. Daarom kan het publiek dat aan [!DNL LinkedIn Matched Audiences] wordt geactiveerd van *gehakt* herkenningstekens, zoals e-mailadressen of mobiele apparaat IDs worden afgevinkt.

Afhankelijk van het type id&#39;s dat u in Adobe Experience Platform invoert, moet u aan de desbetreffende vereisten voldoen.

## E-mailhashingvereisten {#email-hashing-requirements}

U kunt e-mailadressen hashen alvorens hen in Adobe Experience Platform op te nemen, of e-mailadressen gebruiken duidelijk in Experience Platform, en [!DNL Experience Platform] hen hebben geknoeid op activering.

Om over het opnemen van e-mailadressen in Experience Platform te leren, zie het [&#x200B; overzicht van de partijopname &#x200B;](/help/ingestion/batch-ingestion/overview.md) en [&#x200B; het stromen ingestitieoverzicht &#x200B;](/help/ingestion/streaming-ingestion/overview.md).

Als u ervoor kiest om de e-mailadressen zelf te hashen, moet u aan de volgende vereisten voldoen:

* Snijd alle spaties aan het begin en aan het einde van de e-mailtekenreeks bij. Bijvoorbeeld: `johndoe@example.com` , niet `<space>johndoe@example.com<space>` ;
* Wanneer u de e-mailtekenreeksen hasht, moet u ervoor zorgen dat de kleine-lettertekenreeks wordt gehaseerd.
   * Voorbeeld: `example@email.com` , not `EXAMPLE@EMAIL.COM` ;
* Zorg ervoor dat de hashtekenreeks alleen in kleine letters wordt weergegeven
   * Voorbeeld: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149` , not `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149` ;
* Zilp de tekenreeks niet.

>[!NOTE]
>
>Gegevens uit naamruimten zonder hashing worden automatisch gehasht door [!DNL Experience Platform] bij activering.
> Kenmerkbrongegevens worden niet automatisch gehasht.
> 
> Tijdens de [&#x200B; stap van de Toewijzing van de Identiteit &#x200B;](../../ui/activate-segment-streaming-destinations.md#mapping), wanneer uw brongebied unhashed attributen bevat, controleer de **[!UICONTROL Apply transformation]** optie, om [!DNL Experience Platform] automatisch de gegevens bij activering te hebben.
> 
> De optie **[!UICONTROL Apply transformation]** wordt alleen weergegeven wanneer u kenmerken als bronvelden selecteert. Deze wordt niet weergegeven wanneer u naamruimten kiest.

![&#x200B; de afbeeldingstransformatie van de Identiteit &#x200B;](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

In de onderstaande video ziet u ook de stappen voor het configureren van een [!DNL LinkedIn Matched Audiences] -bestemming en het activeren van het publiek.

>[!VIDEO](https://video.tv.adobe.com/v/3475119/?quality=12&learn=on&captions=dut)

>[!NOTE]
>
>De Experience Platform-gebruikersinterface wordt vaak bijgewerkt en kan zijn gewijzigd sinds de opname van deze video. Voor de meest bijgewerkte informatie, verwijs naar het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md).

### Verifiëren voor bestemming {#authenticate}

1. Zoek het doel [!DNL LinkedIn Matched Audiences] in de doelcatalogus en selecteer **[!UICONTROL Set Up]** .
2. Selecteer **[!UICONTROL Connect to destination]**.
   ![&#x200B; verifieer aan LinkedIn &#x200B;](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Ga uw geloofsbrieven LinkedIn in en selecteer **Login**.

### Verificatiegegevens vernieuwen {#refresh-authentication-credentials}

LinkedIn tokens verlopen elke 60 dagen. U kunt de vervaldatums van uw tokens controleren in de kolom **[!UICONTROL Account expiration date]** op de tabbladen **[[!UICONTROL Accounts]](../../ui/destinations-workspace.md#accounts)** of **[[!UICONTROL Browse]](../../ui/destinations-workspace.md#browse)** .

Zodra het teken is verlopen, de gegevensuitvoer naar de bestemming houdt op werkend. Om deze situatie te verhinderen, verifieer opnieuw door de volgende stappen uit te voeren:

1. Ga naar **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]**
2. (Optioneel) Gebruik de beschikbare filters op de pagina om alleen LinkedIn-accounts weer te geven.
   ![&#x200B; Filter om slechts rekeningen te tonen LinkedIn &#x200B;](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-filters.png)
3. Selecteer de account die u wilt vernieuwen, selecteer de ellips en selecteer **[!UICONTROL Edit details]** .
   ![&#x200B; uitgezocht geef detailcontrole &#x200B;](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-edit-details.png) uit
4. Selecteer **[!UICONTROL Reconnect OAuth]** in het modale venster en verifieer het opnieuw met uw LinkedIn-referenties.
   ![&#x200B; Modal venster met Opnieuw verbinden optie OAuth &#x200B;](/help/destinations/assets/catalog/social/linkedin/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>Uw verificatiereferenties worden vernieuwd en de vervaltijd wordt ingesteld op 60 dagen.

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="Account-id"
>abstract="Uw LinkedIn-account-id van Campagnebeheer. U kunt deze id vinden in uw LinkedIn Campaign Manager-account."

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL LinkedIn Campaign Manager Account ID] . U kunt deze id vinden in uw [!DNL LinkedIn Campaign Manager] -account.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [&#x200B; publieksgegevens aan het stromen publiek de uitvoerbestemmingen &#x200B;](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

## Geëxporteerde gegevens {#exported-data}

Een succesvolle activering betekent dat een [!DNL LinkedIn] douanepubliek programmatically in [[!DNL LinkedIn Campaign Manager] &#x200B;](https://www.linkedin.com/campaignmanager/login) wordt gecreeerd. Het lidmaatschap van het publiek wordt aangepast omdat gebruikers gekwalificeerd zijn voor of gediskwalificeerd zijn voor het actieve publiek.

>[!TIP]
>
>De integratie tussen Adobe Experience Platform en [!DNL LinkedIn Matched Audiences] ondersteunt historische publieksbackfills. Alle historische publiekskwalificaties worden naar [!DNL LinkedIn] verzonden wanneer u het publiek activeert naar het doel.
