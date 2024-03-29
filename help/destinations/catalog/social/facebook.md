---
keywords: facebook-verbinding;facebook-verbinding;facebook-bestemmingen;facebook;instagram;messenger;facebook-boodschapper
title: Facebook-verbinding
description: Activeer profielen voor uw Facebook-campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 1%

---

# [!DNL Facebook] verbinding

## Overzicht {#overview}

Profielen activeren voor uw [!DNL Facebook] campagnes voor doelgroepen, personalisatie en onderdrukking op basis van gehakte e-mails.

U kunt deze bestemming voor publiek gebruiken die zich over richt [!DNL Facebook's] apps die worden ondersteund door [!DNL Custom Audiences], inclusief [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], en [!DNL Messenger]. De selectie van de app waarin u de campagne wilt voeren, wordt aangegeven op het plaatsingsniveau in [!DNL Facebook Ads Manager].

![Facebook-bestemming in de gebruikersinterface van Adobe Experience Platform.](../../assets/catalog/social/facebook/catalog.png)

## Gebruiksscenario’s

Om u te helpen beter begrijpen hoe en wanneer gebruiken [!DNL Facebook] doel, hier zijn twee voorbeelden van gebruiksgevallen die Adobe Experience Platform-klanten kunnen oplossen door deze functie te gebruiken.

### Hoofdletters gebruiken #1

Een online detailhandelaar wil bestaande klanten door sociale platforms bereiken en hen gepersonaliseerde aanbiedingen tonen die op hun vorige orden worden gebaseerd. De online detailhandelaar kan e-mailadressen van hun eigen CRM aan Adobe Experience Platform opnemen, publiek van hun eigen off-line gegevens bouwen, en deze publiek naar het verzenden [!DNL Facebook] sociaal platform, optimalisering van hun reclame-uitgaven.

### Hoofdletters gebruiken #2

Een luchtvaartmaatschappij heeft verschillende klantniveaus (Bronze, Silver en Gold) en wil elk niveau via sociale platforms voorzien van persoonlijke aanbiedingen. Niet alle klanten gebruiken echter de mobiele app van de luchtvaartmaatschappij en sommige van hen hebben zich niet aangemeld bij de website van het bedrijf. De enige id&#39;s die het bedrijf over deze klanten heeft, zijn id&#39;s voor lidmaatschap en e-mailadressen.

Om hen over sociale media te richten, kunnen zij de klantengegevens van hun CRM aan boord nemen in Adobe Experience Platform, gebruikend de e-mailadressen als herkenningstekens.

Vervolgens kunnen ze hun offline gegevens gebruiken, inclusief de bijbehorende id&#39;s van het lidmaatschap en klantniveaus, om nieuwe doelgroepen te maken die ze via de [!DNL Facebook] bestemming.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Facebook Custom Audiences] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | Google-advertentie-id | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |
| phone_sha256 | Telefoonnummers die zijn hashed met het SHA256-algoritme | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-telefoonnummers. Volg de instructies in de [Vereisten voor id-afstemming](#id-matching-requirements-id-matching-requirements) en gebruik de juiste naamruimten voor respectievelijk platte tekst en gehashte telefoonnummers. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Volg de instructies in de [Vereisten voor id-afstemming](#id-matching-requirements-id-matching-requirements) gebruiken en de juiste naamruimten gebruiken voor normale tekst en gehashte e-mailadressen. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| extern_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de Facebook-bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voorwaarden voor facebook-accounts {#facebook-account-prerequisites}

Voordat u uw publiek naar kunt sturen [!DNL Facebook]voldoet aan de volgende vereisten:

* Uw [!DNL Facebook] gebruikersaccount moet volledige toegang hebben tot [!DNL Facebook Business Account] die eigenaar is van de advertentierekening die u gebruikt.
* Uw [!DNL Facebook] gebruikersaccount moet de **[!DNL Manage campaigns]** Toestemming ingeschakeld voor de advertentie-account die u wilt gebruiken.
* De **Adobe Experience Cloud** bedrijfsaccount moet worden toegevoegd als advertentiepartner in uw [!DNL Facebook Ad Account]. Gebruik `business ID=206617933627973`. Zie [Partners toevoegen aan uw Business Manager](https://www.facebook.com/business/help/1717412048538897) in de documentatie van Facebook voor meer informatie.
  >[!IMPORTANT]
  >
  > Wanneer u de machtigingen voor Adobe Experience Cloud configureert, moet u de optie **Campagnes beheren** toestemming. De toestemming wordt vereist voor [!DNL Adobe Experience Platform] integratie.
* Lees en onderteken de [!DNL Facebook Custom Audiences] Servicevoorwaarden. Ga hiertoe naar `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, waarbij `accountID` is uw [!DNL Facebook Ad Account ID].
  >[!IMPORTANT]
  >
  >Bij het ondertekenen van de [!DNL Facebook Custom Audiences] Servicevoorwaarden, gebruik dezelfde gebruikersaccount als voor verificatie in de Facebook API.

## Vereisten voor id-afstemming {#id-matching-requirements}

[!DNL Facebook] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Daarom wordt het publiek geactiveerd tot [!DNL Facebook] kan worden uitgeschakeld *hashed* id&#39;s, zoals e-mailadressen of telefoonnummers.

Afhankelijk van het type id&#39;s dat u in Adobe Experience Platform invoert, moet u aan de desbetreffende vereisten voldoen.

## Vereisten voor hashing voor telefoonnummers {#phone-number-hashing-requirements}

Er zijn twee methoden om telefoonnummers te activeren in [!DNL Facebook]:

* **Raw-telefoonnummers worden geïnstalleerd**: u kunt onbewerkte telefoonnummers invoeren in het dialoogvenster [!DNL E.164] indelen in [!DNL Platform]. Deze werden automatisch gehasht bij activering. Als u deze optie kiest, moet u altijd uw onbewerkte telefoonnummers invoeren in het dialoogvenster `Phone_E.164` naamruimte.
* **Hashing-telefoonnummers invoegen**: u kunt uw telefoonaantallen vóór inname vooraf hashen in [!DNL Platform]. Als u deze optie kiest, zorg ervoor om uw gehakte telefoonaantallen altijd in te nemen in `Phone_SHA256` naamruimte.

>[!NOTE]
>
>Telefoonnummers die in de `Phone` naamruimte kan niet worden geactiveerd in [!DNL Facebook].

## E-mailhashingvereisten {#email-hashing-requirements}

U kunt e-mailadressen hashen alvorens hen in Adobe Experience Platform op te nemen, of e-mailadressen gebruiken duidelijk in Experience Platform, en hebben [!DNL Platform] hash deze na activering.

Als u meer wilt weten over het invoeren van e-mailadressen in Experience Platform, raadpleegt u de [overzicht van batch-opname](/help/ingestion/batch-ingestion/overview.md) en de [overzicht van het opnemen van streaming](/help/ingestion/streaming-ingestion/overview.md).

Als u ervoor kiest om de e-mailadressen zelf te hashen, moet u aan de volgende vereisten voldoen:

* Alle spaties aan het begin en aan het einde van de e-mailtekenreeks bijsnijden; voorbeeld: `johndoe@example.com`, niet `<space>johndoe@example.com<space>`;
* Wanneer u de e-mailtekenreeksen hasht, moet u ervoor zorgen dat de kleine-lettertekenreeks wordt gehaseerd.
   * Voorbeeld: `example@email.com`, niet `EXAMPLE@EMAIL.COM`;
* Zorg ervoor dat de hashtekenreeks alleen in kleine letters wordt weergegeven
   * Voorbeeld: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, niet `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Zilp de tekenreeks niet.

>[!NOTE]
>
>Gegevens uit naamruimten zonder hashing worden automatisch gehasht door [!DNL Platform] na activering.
> Kenmerkbrongegevens worden niet automatisch gehasht. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen.
> De **[!UICONTROL Apply transformation]** Deze optie wordt alleen weergegeven wanneer u kenmerken selecteert als bronvelden. Deze wordt niet weergegeven wanneer u naamruimten kiest.

![Transformatiebeheer toepassen dat is gemarkeerd in de toewijzingsstap.](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Aangepaste naamruimten gebruiken {#custom-namespaces}

Voordat u de `Extern_ID` naamruimte waarnaar gegevens moeten worden verzonden [!DNL Facebook]moet u uw eigen id&#39;s synchroniseren met [!DNL Facebook Pixel]. Zie de [Officiële facebook-documentatie](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) voor nadere informatie.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

In de onderstaande video ziet u ook de stappen voor het configureren van een [!DNL Facebook] doel en activeer het publiek.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>De gebruikersinterface van het Experience Platform wordt vaak bijgewerkt en kan sinds de opname van deze video zijn veranderd. Voor de meest recente informatie raadpleegt u de [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verifiëren voor bestemming {#authenticate}

1. Zoek het Facebook-doel in de doelcatalogus en selecteer **[!UICONTROL Set Up]**.
2. Selecteer **[!UICONTROL Connect to destination]**.
   ![Verifieer aan de stap van Facebook die in het activeringswerkschema wordt getoond.](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. Voer uw Facebook-gebruikersgegevens in en selecteer **Aanmelden**.

### Doelgegevens invullen {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="Account-id"
>abstract="Je Facebook-account-id. Je kunt deze id vinden in je Facebook Ads Manager account. Geef bij het invoeren van deze id altijd een voorvoegsel op `act_`."

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL Facebook Ad Account ID]. U kunt deze id vinden in uw [!DNL Facebook Ads Manager] account. Geef bij het invoeren van deze id altijd een voorvoegsel op `act_`.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="Oorsprong van het publiek"
>abstract="Kies hoe de klantgegevens in het publiek oorspronkelijk zijn verzameld. De gegevens worden in Facebook weergegeven wanneer een gebruiker voor het segment is ingesteld"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customers"
>title="Oorsprong van het publiek"
>abstract="Adverteerders verzamelden gegevens rechtstreeks bij klanten."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_partners"
>title="Oorsprong van het publiek"
>abstract="Adverteerders verzamelden gegevens rechtstreeks bij hun partners."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customersandpartners"
>title="Oorsprong van het publiek"
>abstract="Adverteerders verzamelden gegevens rechtstreeks bij hun klanten en partners."

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](../../ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

In de **[!UICONTROL Segment schedule]** stap, moet u de [!UICONTROL Origin of audience] bij het verzenden van publiek naar [!DNL Facebook Custom Audiences].

![Oorsprong van de vervolgkeuzelijst Publiek weergegeven in de activeringsstap van Facebook.](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Voorbeeld van toewijzing: publieksgegevens activeren in [!DNL Facebook Custom Audience] {#example-facebook}

Hieronder ziet u een voorbeeld van correcte identiteitstoewijzing bij het activeren van publieksgegevens in [!DNL Facebook Custom Audience].

Bronvelden selecteren:

* Selecteer de `Email` naamruimte als bronidentiteit als de e-mailadressen die u gebruikt geen hashed zijn.
* Selecteer de `Email_LC_SHA256` naamruimte als bronidentiteit als u de e-mailadressen van de klant hebt gewijzigd bij het invoeren van gegevens in [!DNL Platform]volgens [!DNL Facebook] [e-mailhashingvereisten](#email-hashing-requirements).
* Selecteer de `PHONE_E.164` naamruimte als bronidentiteit als uw gegevens uit niet-gehashte telefoonnummers bestaan. [!DNL Platform] hash de telefoonnummers waaraan moet worden voldaan [!DNL Facebook] eisen.
* Selecteer de `Phone_SHA256` naamruimte als bronidentiteit als u telefoonnummers hebt gehasht bij gegevensinvoer in [!DNL Platform]volgens [!DNL Facebook] [hashingvereisten voor telefoonnummers](#phone-number-hashing-requirements).
* Selecteer de `IDFA` naamruimte als bronidentiteit als uw gegevens bestaan uit [!DNL Apple] apparaat-id&#39;s.
* Selecteer de `GAID` naamruimte als bronidentiteit als uw gegevens bestaan uit [!DNL Android] apparaat-id&#39;s.
* Selecteer de `Custom` naamruimte als bronidentiteit als uw gegevens uit andere typen id&#39;s bestaan.

Doelvelden selecteren:

* Selecteer de `Email_LC_SHA256` naamruimte als doelidentiteit wanneer de bronnaamruimten `Email` of `Email_LC_SHA256`.
* Selecteer de `Phone_SHA256` naamruimte als doelidentiteit wanneer de bronnaamruimten `PHONE_E.164` of `Phone_SHA256`.
* Selecteer de `IDFA` of `GAID` naamruimten als doelidentiteit wanneer uw bronnaamruimten `IDFA` of `GAID`.
* Selecteer de `Extern_ID` naamruimte als doelidentiteit wanneer uw bronnaamruimte een aangepaste naamruimte is.

>[!IMPORTANT]
>
>Gegevens uit naamruimten zonder hashing worden automatisch gehasht door [!DNL Platform] na activering.
> 
>Kenmerkbrongegevens worden niet automatisch gehasht. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen.

![Transformatiebeheer toepassen dat is gemarkeerd in de toewijzingsstap.](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Facebook], een geslaagde activering betekent dat een [!DNL Facebook] aangepaste doelgroep wordt programmatisch gemaakt in [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Het lidmaatschap van het publiek wordt toegevoegd en verwijderd omdat gebruikers gekwalificeerd zijn voor of gediskwalificeerd zijn voor het actieve publiek.

>[!TIP]
>
>De integratie tussen Adobe Experience Platform en [!DNL Facebook] biedt ondersteuning voor historische publieksbackfills. Alle historische publiekskwalificaties worden verzonden naar [!DNL Facebook] wanneer u het publiek naar het doel activeert.

## Problemen oplossen {#troubleshooting}

### 400 Onjuist aanvraagfoutbericht {#bad-request}

Wanneer het vormen van deze bestemming, kunt u de volgende fout ontvangen:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Deze fout treedt op wanneer klanten nieuwe accounts gebruiken en [!DNL Facebook] machtigingen zijn nog niet actief.

Als u de `400 Bad Request` foutbericht na het volgen van de stappen in [Voorwaarden voor facebook-accounts](#facebook-account-prerequisites), kunt u enkele dagen [!DNL Facebook] bevoegdheden om in werking te treden.
