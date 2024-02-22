---
keywords: Google klant match;Google klant match;Google Customer Match
title: Google Customer Match-verbinding
description: Met Google Customer Match kunt u uw online- en offline gegevens gebruiken om klanten te bereiken en opnieuw contact op te nemen met andere Google, zoals Zoeken, Winkelen, Gmail en YouTube.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: d5a22d4692226c865f6489c821366b4ce8bc2887
workflow-type: tm+mt
source-wordcount: '1934'
ht-degree: 0%

---

# [!DNL Google Customer Match] verbinding

>[!IMPORTANT]
>
> Google brengt wijzigingen in de [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [Klantenovereenkomst](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)en de [Display &amp; Video 360-API](https://developers.google.com/display-video/api/guides/getting-started/overview) ter ondersteuning van de in het kader van de [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) in de Europese Unie[Beleid voor EU-gebruikerstoestemming](https://www.google.com/about/company/user-consent-policy/)). Verwacht wordt dat de handhaving van deze wijzigingen in de toestemmingsvereisten met ingang van 6 maart 2024 in werking zal treden.
><br/><br/>
>Om zich aan het EU-beleid inzake instemming van gebruikers te houden en door te gaan met het opstellen van publiekslijsten voor gebruikers in de Europese Economische Ruimte (EER), moeten adverteerders en partners ervoor zorgen dat zij toestemming van de eindgebruiker geven bij het uploaden van publieksgegevens. Als Google-partner beschikt Adobe over de benodigde instrumenten om te voldoen aan deze toestemmingsvereisten in het kader van de DMA in de Europese Unie.
><br/><br/>
>Klanten die een privacyschild voor Adobe hebben aangeschaft en een [toestemmingsbeleid](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) om profielen zonder toestemming uit te filteren, hoeft u geen actie te ondernemen.
><br/><br/>
>Klanten die geen privacyschild voor Adobe hebben aangeschaft, moeten de [segmentdefinitie](../../../segmentation/home.md#segment-definitions) mogelijkheden binnen [Segment Builder](../../../segmentation/ui/segment-builder.md) om profielen zonder toestemming uit te filteren, zodat de bestaande Real-Time CDP Google-bestemmingen zonder onderbreking kunnen worden gebruikt.

[[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) Hiermee kunt u uw online- en offlinegegevens gebruiken om uw klanten te bereiken en opnieuw contact op te nemen met andere Google-eigendommen, zoals: [!DNL Search], [!DNL Shopping], [!DNL Gmail], en [!DNL YouTube].

![Google Customer Match-bestemming in de gebruikersinterface van Adobe Experience Platform.](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer gebruiken [!DNL Google Customer Match] doel, hier zijn voorbeelden van gebruiksgevallen die Adobe Experience Platform-klanten met deze functie kunnen oplossen.

### Hoofdletters gebruiken #1

Een atletisch merkteken wil bestaande klanten bereiken via [!DNL Google Search] en [!DNL Google Shopping] om aanbiedingen en objecten aan te passen op basis van eerdere aankopen en browsergeschiedenis. Het merk apparel kan e-mailadressen van hun eigen CRM aan Experience Platform opnemen, en publiek van hun eigen off-line gegevens bouwen. Vervolgens kunnen ze deze doelgroepen naar sturen [!DNL Google Customer Match] te gebruiken voor [!DNL Search] en [!DNL Shopping], optimalisering van hun reclame-uitgaven.

### Hoofdletters gebruiken #2

Een vooraanstaande technologiebedrijf lanceerde een nieuwe telefoon. Om dit nieuwe telefoonmodel te bevorderen, kijken zij om bewustzijn van de nieuwe eigenschappen en de functionaliteit van de telefoon aan klanten te drijven die vorige modellen van hun telefoons bezitten.

Om de versie te promoten, uploaden zij e-mailadressen van hun gegevensbestand van CRM in Experience Platform, gebruikend de e-mailadressen als herkenningstekens. Het publiek wordt gecreeerd gebaseerd op klanten die oudere telefoonmodellen bezitten. Vervolgens wordt het publiek verzonden naar [!DNL Google Customer Match], zodat kan het bedrijf huidige klanten, klanten richten die oudere telefoonmodellen bezitten en gelijkaardige klanten op [!DNL YouTube].

## Gegevensbeheer voor [!DNL Google Customer Match] bestemmingen {#data-governance}

Sommige bestemmingen in Experience Platform hebben bepaalde regels en verplichtingen voor gegevens die worden verzonden naar of ontvangen van het bestemmingsplatform. U bent verantwoordelijk voor het begrijpen van de beperkingen en verplichtingen van uw gegevens en hoe u die gegevens gebruikt in Adobe Experience Platform en het doelplatform. Adobe Experience Platform biedt tools voor gegevensbeheer om u te helpen bij het beheren van een aantal van deze gegevensgebruiksverplichtingen. [Meer informatie](../../../data-governance/labels/overview.md) over instrumenten en beleid voor gegevensbeheer.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Google Customer Match] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | Google-advertentie-id | Selecteer deze doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer deze doelidentiteit wanneer uw bronidentiteit een IDFA-naamruimte is. |
| phone_sha256_e.164 | Telefoonnummers in E164-indeling, gehasht met het SHA256-algoritme | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-telefoonnummers. Volg de instructies in de [Vereisten voor id-afstemming](#id-matching-requirements-id-matching-requirements) en gebruik de juiste naamruimten voor respectievelijk platte tekst en gehashte telefoonnummers. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Volg de instructies in de [Vereisten voor id-afstemming](#id-matching-requirements-id-matching-requirements) gebruiken en de juiste naamruimten gebruiken voor normale tekst en gehashte e-mailadressen. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| user_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |

{style="table-layout:auto"}

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
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer en andere) die worden gebruikt in het dialoogvenster [!DNL Google Customer Match] bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## [!DNL Google Customer Match] accountvereisten {#google-account-prerequisites}

Voordat u een [!DNL Google Customer Match] bestemming in Experience Platform, zorg ervoor u leest en aan het beleid van Google hanteert voor het gebruiken [!DNL Customer Match], die in de [Google-ondersteuningsdocumentatie](https://support.google.com/google-ads/answer/6299717).

Controleer vervolgens of uw [!DNL Google] account is geconfigureerd voor een [!DNL Standard] of hoger machtigingsniveau. Zie de [Google Ads-documentatie](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) voor meer informatie.

### Lijst van gewenste personen {#allowlist}

Voordat u het dialoogvenster [!DNL Google Customer Match] doel in Experience Platform, zorg ervoor dat uw [!DNL Google Ads] voldoet aan de [[!DNL Google Customer Match] beleid](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Klanten met compatibele accounts worden automatisch gevoegd op lijst van gewenste personen door Google.

## Vereisten voor id-afstemming {#id-matching-requirements}

[!DNL Google] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Daarom wordt het publiek geactiveerd tot [!DNL Google Customer Match] kan worden uitgeschakeld *hashed* id&#39;s, zoals e-mailadressen of telefoonnummers.

Afhankelijk van het type id&#39;s dat u in Adobe Experience Platform invoert, moet u aan de desbetreffende vereisten voldoen.

### Vereisten voor hashing voor telefoonnummers {#phone-number-hashing-requirements}

Er zijn twee methoden om telefoonnummers te activeren in [!DNL Google Customer Match]:

* **Raw-telefoonnummers worden geïnstalleerd**: u kunt onbewerkte telefoonnummers invoeren in het dialoogvenster [!DNL E.164] indelen in [!DNL Platform]en deze worden automatisch gehasht bij activering. Als u deze optie kiest, moet u altijd uw onbewerkte telefoonnummers invoeren in het dialoogvenster `Phone_E.164` naamruimte.
* **Hashing-telefoonnummers invoegen**: u kunt uw telefoonaantallen vóór inname vooraf hashen in [!DNL Platform]. Als u deze optie kiest, zorg ervoor om uw gehakte telefoonaantallen altijd in te nemen in `PHONE_SHA256_E.164` naamruimte.

>[!NOTE]
>
>Telefoonnummers die in de `Phone` naamruimte kan niet worden geactiveerd in [!DNL Google Customer Match].

### E-mailhashingvereisten {#hashing-requirements}

U kunt e-mailadressen hashen alvorens hen in Adobe Experience Platform op te nemen, of e-mailadressen gebruiken duidelijk in Experience Platform, en hebben [!DNL Platform] hash deze na activering.

Raadpleeg de volgende secties in de documentatie bij Google voor meer informatie over de hashingvereisten voor Google en andere activeringsbeperkingen:

* [[!DNL Customer Match] met e-mailadres, adres of gebruikersnaam](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] overwegingen](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] met telefoonnummer](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] met mobiele apparaat-id&#39;s](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


Als u meer wilt weten over het invoeren van e-mailadressen in Experience Platform, raadpleegt u de [overzicht van batch-opname](../../../ingestion/batch-ingestion/overview.md) en de [overzicht van het opnemen van streaming](../../../ingestion/streaming-ingestion/overview.md).

Als u ervoor kiest om de e-mailadressen zelf te hashen, moet u voldoen aan de Google-vereisten die in de bovenstaande koppelingen worden beschreven.

### Aangepaste naamruimten gebruiken {#custom-namespaces}

Voordat u de `User_ID` naamruimte om gegevens naar Google te verzenden, moet u uw eigen id&#39;s synchroniseren met [!DNL gTag]. Zie de [Officiële Google-documentatie](https://support.google.com/google-ads/answer/9199250) voor nadere informatie.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Video-overzicht {#video-overview}

Bekijk de onderstaande video voor een uitleg van de voordelen en hoe u gegevens activeert naar Google Customer Match.

>[!VIDEO](https://video.tv.adobe.com/v/38180/)

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: geef een naam op voor deze doelverbinding
* **[!UICONTROL Description]**: geef een beschrijving op voor deze doelverbinding
* **[!UICONTROL Account ID]**: uw [Customer ID Google Adds](https://support.google.com/google-ads/answer/1704344?hl=en). De indeling van de id is xxx-xxxx. Als u het [!DNL Google Ads Manager Account (My Client Center)], gebruik uw account-id voor Manager niet. Gebruik de [Customer ID Google Adds](https://support.google.com/google-ads/answer/1704344?hl=en) in plaats daarvan.

>[!IMPORTANT]
>
> * De **[!UICONTROL Combine with PII]** marketingactie is standaard geselecteerd voor de [!DNL Google Customer Match] doel en kan niet worden verwijderd.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten* aan bestemmingen, hebt u nodig **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](../../ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

In de **[!UICONTROL Segment schedule]** stap, moet u de [!UICONTROL App ID] wanneer verzenden [!DNL IDFA] of [!DNL GAID] publiek naar [!DNL Google Customer Match].

![Het veld Google Customer Match App ID wordt gemarkeerd in de stap voor segmentplanning van de activeringsworkflow.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Voor meer informatie over het zoeken naar de [!DNL App ID], verwijst u naar de [Officiële Google-documentatie](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) of vraag uw Google-vertegenwoordiger.

### Voorbeeld van toewijzing: publieksgegevens activeren in [!DNL Google Customer Match] {#example-gcm}

Dit is een voorbeeld van correcte identiteitstoewijzing wanneer het activeren van publieksgegevens in [!DNL Google Customer Match].

Bronvelden selecteren:

* Selecteer de `Email` naamruimte als bronidentiteit als de e-mailadressen die u gebruikt geen hashed zijn.
* Selecteer de `Email_LC_SHA256` naamruimte als bronidentiteit als u de e-mailadressen van de klant hebt gewijzigd bij het invoeren van gegevens in [!DNL Platform]volgens [!DNL Google Customer Match] [e-mailhashingvereisten](#hashing-requirements).
* Selecteer de `PHONE_E.164` naamruimte als bronidentiteit als uw gegevens uit niet-gehashte telefoonnummers bestaan. [!DNL Platform] hash de telefoonnummers waaraan moet worden voldaan [!DNL Google Customer Match] eisen.
* Selecteer de `Phone_SHA256_E.164` naamruimte als bronidentiteit als u telefoonnummers hebt gehasht bij gegevensinvoer in [!DNL Platform]volgens [!DNL Facebook] [hashingvereisten voor telefoonnummers](#phone-number-hashing-requirements).
* Selecteer de `IDFA` naamruimte als bronidentiteit als uw gegevens bestaan uit [!DNL Apple] apparaat-id&#39;s.
* Selecteer de `GAID` naamruimte als bronidentiteit als uw gegevens bestaan uit [!DNL Android] apparaat-id&#39;s.
* Selecteer de `Custom` naamruimte als bronidentiteit als uw gegevens uit andere typen id&#39;s bestaan.

Doelvelden selecteren:

* Selecteer de `Email_LC_SHA256` naamruimte als doelidentiteit wanneer de bronnaamruimten `Email` of `Email_LC_SHA256`.
* Selecteer de `Phone_SHA256_E.164` naamruimte als doelidentiteit wanneer de bronnaamruimten `PHONE_E.164` of `Phone_SHA256_E.164`.
* Selecteer de `IDFA` of `GAID` naamruimten als doelidentiteit wanneer uw bronnaamruimten `IDFA` of `GAID`.
* Selecteer de `User_ID` naamruimte als doelidentiteit wanneer uw bronnaamruimte een aangepaste naamruimte is.

![Identiteitstoewijzing tussen bron- en doelvelden die wordt weergegeven in de stap Toewijzing van de activeringsworkflow.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Gegevens uit naamruimten zonder hashing worden automatisch gehasht door [!DNL Platform] na activering.

Kenmerkbrongegevens worden niet automatisch gehasht. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen.

![Transformatiebeheer toepassen dat is gemarkeerd in de stap Toewijzing van de activeringsworkflow.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Controleren of publieksactivering is gelukt {#verify-activation}

Nadat u de activeringsstroom hebt voltooid, schakelt u over naar uw **[!UICONTROL Google Ads]** account. Het geactiveerde publiek wordt in uw Google-account weergegeven als klantenlijsten. Afhankelijk van de grootte van uw publiek, bevolken sommige soorten publiek alleen als er meer dan 100 actieve gebruikers zijn om te dienen.

Wanneer u een publiek toewijst aan beide [!DNL IDFA] en [!DNL GAID] mobiele id&#39;s, [!DNL Google Customer Match] maakt een apart publiek voor elke id-toewijzing. Uw [!DNL Google Ads] account toont twee verschillende segmenten, één voor de [!DNL IDFA]en een voor de [!DNL GAID] toewijzing.

## Problemen oplossen {#troubleshooting}

### 400 Onjuist aanvraagfoutbericht {#bad-request}

Wanneer het vormen van deze bestemming, kunt u de volgende fout ontvangen:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Deze fout treedt op wanneer de klantenrekeningen niet aan [voorwaarden](#google-account-prerequisites). Neem contact op met Google om dit probleem op te lossen en zorg ervoor dat uw account op de lijst van toegestane partijen staat en geconfigureerd is voor een [!DNL Standard] of hoger machtigingsniveau. Zie de [Google Ads-documentatie](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) voor meer informatie.