---
keywords: Google klant match;Google klant match;Google Customer Match
title: Google Customer Match-verbinding
description: Met Google Customer Match kunt u uw online- en offline gegevens gebruiken om klanten te bereiken en opnieuw contact op te nemen met andere door Google bediende en bediende eigendommen, zoals Zoeken, Winkelen en Gmail.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: ce205622260f4252d1a7db7c5011366fb2ed4d3c
workflow-type: tm+mt
source-wordcount: '2372'
ht-degree: 1%

---

# [!DNL Google Customer Match] verbinding

>[!IMPORTANT]
>
> Google geeft veranderingen in de [ Adds API van Google ](https://developers.google.com/google-ads/api/docs/start), [ Overeenkomst van de Klant ](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) vrij, en [ Vertoning &amp; Video 360 API ](https://developers.google.com/display-video/api/guides/getting-started/overview) om de naleving en toestemmings-gerelateerde vereisten te steunen die onder de [ Wet van de Markten ](https://digital-markets-act.ec.europa.eu/index_nl) (DMA) worden bepaald in de Europese Unie ([ EU het Beleid van de Toestemming van de Gebruiker ](https://www.google.com/about/company/user-consent-policy/)). De handhaving van deze wijzigingen in de toestemmingsvereisten is vanaf 6 maart 2024 van kracht.
><br/>
>Om zich aan het EU-beleid inzake instemming van gebruikers te houden en door te gaan met het opstellen van publiekslijsten voor gebruikers in de Europese Economische Ruimte (EER), moeten adverteerders en partners ervoor zorgen dat zij toestemming van de eindgebruiker geven bij het uploaden van publieksgegevens. Als Google-partner beschikt Adobe over de benodigde tools om te voldoen aan deze toestemmingsvereisten in het kader van de DMA in de Europese Unie.
><br/>
>De klanten die de Privacy &amp; het Schild van de Veiligheid van Adobe hebben gekocht en het beleid van de a [ toestemming ](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) gevormd om niet-goedgekeurde profielen uit te filteren hoeven geen actie te ondernemen.
><br/>
>De klanten die geen de Privacy &amp; het Schild van de Veiligheid van Adobe hebben gekocht moeten de ](../../../segmentation/home.md#segment-definitions) mogelijkheden van de segmentdefinitie [ binnen [ de Bouwer van het Segment ](../../../segmentation/ui/segment-builder.md) aan filter uit niet-goedgekeurde profielen gebruiken, om de bestaande bestemmingen van Real-Time CDP Google zonder onderbreking te blijven gebruiken.

[[!DNL Google Customer Match] ](https://support.google.com/google-ads/answer/6379332?hl=en) laat u uw online en off-line gegevens gebruiken om met uw klanten over Google bezeten en in werking gestelde eigenschappen, zoals: [!DNL Search], [!DNL Shopping], en [!DNL Gmail] te bereiken en opnieuw in dienst te nemen.

>[!TIP]
>
>Om klanten op [!DNL YouTube] inventaris te bereiken, gebruik de [ Gelijke van de Klant van Google + bestemming DV360 ](/help/destinations/catalog/advertising/google-customer-match-dv360.md), die de Partner API van het Publiek van Google gebruikt.

![ de Klant van Google de bestemming van de Gelijke in Adobe Experience Platform UI.](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer om de [!DNL Google Customer Match] bestemming te gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze eigenschap kunnen oplossen.

### Hoofdletters gebruiken #1

Een atletisch merkje wil bestaande klanten bereiken via [!DNL Google Search] en [!DNL Google Shopping] om aanbiedingen en objecten aan te passen op basis van hun eerdere aankopen en browsergeschiedenis. Het merk apparel kan e-mailadressen van hun eigen CRM aan Experience Platform opnemen, en publiek van hun eigen off-line gegevens bouwen. Vervolgens kunnen ze deze soorten publiek naar [!DNL Google Customer Match] sturen voor gebruik in [!DNL Search] en [!DNL Shopping] , zodat hun advertentie-uitgaven worden geoptimaliseerd.

### Hoofdletters gebruiken #2

>[!TIP]
>
>Om dit gebruiksgeval op [!DNL YouTube] inventaris uit te voeren, gebruik de nieuwe [ Gelijke van de Klant van Google + bestemming DV360 ](/help/destinations/catalog/advertising/google-customer-match-dv360.md), die de Partner API van het Publiek van Google gebruikt.

Een vooraanstaande technologiebedrijf lanceerde een nieuwe telefoon. Om dit nieuwe telefoonmodel te bevorderen, kijken zij om bewustzijn van de nieuwe eigenschappen en de functionaliteit van de telefoon aan klanten te drijven die vorige modellen van hun telefoons bezitten.

Om de release te promoten, uploaden ze e-mailadressen vanuit hun CRM-database naar Experience Platform, waarbij ze de e-mailadressen als id&#39;s gebruiken. Het publiek wordt gecreeerd gebaseerd op klanten die oudere telefoonmodellen bezitten. Vervolgens wordt het publiek verzonden naar [!DNL Google Customer Match] , zodat het bedrijf zich kan richten op huidige klanten, klanten die eigenaar zijn van oudere telefoonmodellen en vergelijkbare klanten op [!DNL YouTube] .

## Gegevensbeheer voor [!DNL Google Customer Match] doelen {#data-governance}

Sommige bestemmingen in Experience Platform hebben bepaalde regels en verplichtingen voor gegevens die naar het bestemmingsplatform worden verzonden of van het bestemmingsplatform worden ontvangen. U bent verantwoordelijk voor het begrijpen van de beperkingen en verplichtingen van uw gegevens en hoe u die gegevens gebruikt in Adobe Experience Platform en het doelplatform. Adobe Experience Platform biedt tools voor gegevensbeheer om u te helpen bij het beheren van een aantal van deze gegevensgebruiksverplichtingen. [ leer meer ](../../../data-governance/labels/overview.md) over de hulpmiddelen en het beleid van het gegevensbeheer.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Google Customer Match] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| `GAID` | GOOGLE ADVERTISING ID | Selecteer deze doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| `IDFA` | Apple-id voor adverteerders | Selecteer deze doelidentiteit wanneer uw bronidentiteit een IDFA-naamruimte is. |
| `phone_sha256_e.164` | Telefoonnummers in E164-indeling, gehasht met het SHA256-algoritme | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-telefoonnummers. Volg de instructies in de [ passende vereisten van identiteitskaart ](#id-matching-requirements-id-matching-requirements) sectie en gebruik aangewezen namespaces voor gewone teksten en gehakt telefoonaantallen, respectievelijk. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| `email_lc_sha256` | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Volg de instructies in de [ passende vereisten van identiteitskaart ](#id-matching-requirements-id-matching-requirements) sectie en gebruik aangewezen namespaces voor gewone teksten en gehakt e-mailadressen, respectievelijk. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| `user_id` | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |
| `address_info_first_name` | Voornaam gebruiker | Deze doelidentiteit moet samen met `address_info_last_name`, `address_info_country_code` en `address_info_postal_code` worden gebruikt wanneer u adresgegevens naar uw bestemming wilt verzenden. <br><br> om Google te verzekeren past het adres aan, moet u alle vier adresgebieden (`address_info_first_name` in kaart brengen, `address_info_last_name`, `address_info_country_code`, en `address_info_postal_code`) en ervoor zorgen dat geen van deze gebieden gegevens in de uitgevoerde profielen missen. <br> Als een veld niet is toegewezen of ontbrekende gegevens bevat, komt Google niet overeen met het adres. |
| `address_info_last_name` | Achternaam van de gebruiker | Deze doelidentiteit moet samen met `address_info_first_name`, `address_info_country_code` en `address_info_postal_code` worden gebruikt wanneer u adresgegevens naar uw bestemming wilt verzenden. <br><br> om Google te verzekeren past het adres aan, moet u alle vier adresgebieden (`address_info_first_name` in kaart brengen, `address_info_last_name`, `address_info_country_code`, en `address_info_postal_code`) en ervoor zorgen dat geen van deze gebieden gegevens in de uitgevoerde profielen missen. <br> Als een veld niet is toegewezen of ontbrekende gegevens bevat, komt Google niet overeen met het adres. |
| `address_info_country_code` | Landcode gebruikersadres | Deze doelidentiteit moet samen met `address_info_first_name`, `address_info_last_name` en `address_info_postal_code` worden gebruikt wanneer u adresgegevens naar uw bestemming wilt verzenden. <br><br> om Google te verzekeren past het adres aan, moet u alle vier adresgebieden (`address_info_first_name` in kaart brengen, `address_info_last_name`, `address_info_country_code`, en `address_info_postal_code`) en ervoor zorgen dat geen van deze gebieden gegevens in de uitgevoerde profielen missen. <br> Als een veld niet is toegewezen of ontbrekende gegevens bevat, komt Google niet overeen met het adres. <br><br> Toegelaten formaat: Kleine letters, 2-brief landcodes in [ ISO 3166-1 alpha-2 ](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) formaat. |
| `address_info_postal_code` | Postcode van gebruikersadres | Deze doelidentiteit moet samen met `address_info_first_name`, `address_info_last_name` en `address_info_country_code` worden gebruikt wanneer u adresgegevens naar uw bestemming wilt verzenden. <br><br> om Google te verzekeren past het adres aan, moet u alle vier adresgebieden (`address_info_first_name` in kaart brengen, `address_info_last_name`, `address_info_country_code`, en `address_info_postal_code`) en ervoor zorgen dat geen van deze gebieden gegevens in de uitgevoerde profielen missen. <br> Als een veld niet is toegewezen of ontbrekende gegevens bevat, komt Google niet overeen met het adres. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer en andere) die in de [!DNL Google Customer Match] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## [!DNL Google Customer Match] -accountvoorwaarden {#google-account-prerequisites}

Alvorens vestiging een [!DNL Google Customer Match] bestemming in Experience Platform, zorg ervoor u leest en aan het beleid van Google hanteert voor het gebruiken van [!DNL Customer Match], die in de [ de steundocumentatie van Google ](https://support.google.com/google-ads/answer/6299717) wordt geschetst.

Controleer vervolgens of uw [!DNL Google] -account is geconfigureerd voor een machtigingsniveau van [!DNL Standard] of hoger. Zie de [ documentatie van Ads van Google ](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) voor details.

### Lijst van gewenste personen {#allowlist}

Alvorens de [!DNL Google Customer Match] bestemming in Experience Platform te creëren, zorg ervoor dat uw [!DNL Google Ads] rekening met het [[!DNL Google Customer Match]  beleid ](https://support.google.com/google-ads/answer/6299717/customer-match-policy) voldoet.

Klanten met compatibele accounts worden automatisch gevoegd op lijst van gewenste personen door Google.

## Vereisten voor id-afstemming {#id-matching-requirements}

[!DNL Google] vereist dat er geen PII&#39;s (Personal Identified Information) worden verzonden. Daarom kan het publiek dat aan [!DNL Google Customer Match] wordt geactiveerd van *gehakt* herkenningstekens, zoals e-mailadressen of telefoonaantallen worden afgevinkt.

Afhankelijk van het type id&#39;s dat u in Adobe Experience Platform invoert, moet u aan de desbetreffende vereisten voldoen.

### Vereisten voor hashing voor telefoonnummers {#phone-number-hashing-requirements}

Er zijn twee methoden om telefoonnummers te activeren in [!DNL Google Customer Match] :

* **Ingesting ruwe telefoonaantallen**: u kunt ruwe telefoonaantallen in het [!DNL E.164] formaat in [!DNL Experience Platform] opnemen, en zij worden automatisch gehakt op activering. Als u deze optie kiest, moet u uw onbewerkte telefoonnummers altijd in de naamruimte `Phone_E.164` invoeren.
* **het Ingeesten hashed telefoonaantallen**: u kunt uw telefoonaantallen vóór opname in [!DNL Experience Platform] pre-hash. Als u deze optie kiest, moet u uw hashed-telefoonnummers altijd invoeren in de naamruimte `PHONE_SHA256_E.164` .

>[!NOTE]
>
>Telefoonnummers die in de naamruimte `Phone` worden ingevoerd, kunnen niet worden geactiveerd in [!DNL Google Customer Match] .

### E-mailhashingvereisten {#hashing-requirements}

U kunt e-mailadressen hashen alvorens hen in Adobe Experience Platform op te nemen, of e-mailadressen gebruiken duidelijk in Experience Platform, en [!DNL Experience Platform] hen hebben geknoeid op activering.

Raadpleeg de volgende secties in de documentatie bij Google voor meer informatie over de hashingvereisten voor Google en andere activeringsbeperkingen:

* [[!DNL Customer Match]  met e-mailadres, adres, of gebruiker - identiteitskaart ](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match]  overwegingen ](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match]  met telefoonaantal ](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match]  met mobiele apparaat IDs ](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


Om over het opnemen van e-mailadressen in Experience Platform te leren, zie het [ overzicht van de partijopname ](../../../ingestion/batch-ingestion/overview.md) en [ het stromen ingestitieoverzicht ](../../../ingestion/streaming-ingestion/overview.md).

Als u ervoor kiest om de e-mailadressen zelf te hashen, moet u voldoen aan de Google-vereisten die in de bovenstaande koppelingen worden beschreven.

### Hashingvereisten voor adresvelden {#address-field-hashing}

Wanneer het in kaart brengen van adres-verwante gebieden aan [!DNL Google Customer Match], hakt Experience Platform **** automatisch de `address_info_first_name` en `address_info_last_name` waarden alvorens hen naar Google te verzenden. Deze automatische hashing is vereist om te voldoen aan de beveiligings- en privacyvereisten van Google.

Verstrek **** niet pre-gehakt waarden voor `address_info_first_name` of `address_info_last_name`. Als u al gehashte waarden opgeeft, mislukt het overeenkomende proces.

### Aangepaste naamruimten gebruiken {#custom-namespaces}

Voordat u de naamruimte `User_ID` kunt gebruiken om gegevens naar Google te verzenden, moet u uw eigen id&#39;s eerst synchroniseren met [!DNL gTag] . Verwijs naar de [ officiële documentatie van Google ](https://support.google.com/google-ads/answer/9199250) voor gedetailleerde informatie.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Experience Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Experience Platform] automatically hash the data on activation.
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
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [ vestiging ](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: geef een naam op voor deze doelverbinding
* **[!UICONTROL Description]**: geef een beschrijving voor deze doelverbinding
* **[!UICONTROL Account ID]**: uw [ Google voegt klantenidentiteitskaart ](https://support.google.com/google-ads/answer/1704344?hl=en) toe. De indeling van de id is xxx-xxxx. Als u [!DNL Google Ads Manager Account (My Client Center)] gebruikt, gebruik dan niet uw account-id voor Manager. Gebruik in plaats hiervan [ Google Adds klant ID ](https://support.google.com/google-ads/answer/1704344?hl=en).

>[!IMPORTANT]
>
> * De marketingactie **[!UICONTROL Combine with PII]** wordt standaard geselecteerd voor het doel van [!DNL Google Customer Match] en kan niet worden verwijderd.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* naar bestemmingen uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [ publieksgegevens aan het stromen publiek de uitvoerbestemmingen ](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

In de stap **[!UICONTROL Segment schedule]** moet u [!UICONTROL App ID] opgeven wanneer u [!DNL IDFA] of [!DNL GAID] soorten publiek naar [!DNL Google Customer Match] verzendt.

![ de Klant van Google het gebied van App ID van de Klant die in de het programmastap van het Segment van het activeringswerkschema wordt benadrukt.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Voor details op hoe te om [!DNL App ID] te vinden, verwijs naar de [ officiële documentatie van Google ](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) of vraag uw vertegenwoordiger van Google.

### Voorbeeld van toewijzing: publieksgegevens activeren in [!DNL Google Customer Match] {#example-gcm}

Dit is een voorbeeld van correcte identiteitstoewijzing wanneer het activeren van publieksgegevens in [!DNL Google Customer Match].

Bronvelden selecteren:

* Selecteer de naamruimte `Email` als bronidentiteit als de e-mailadressen die u gebruikt geen hashing zijn.
* Selecteer `Email_LC_SHA256` namespace als bronidentiteit als u klant e-mailadressen op gegevensinvoer in [!DNL Experience Platform], volgens [!DNL Google Customer Match] [ e-mailhashing vereisten ](#hashing-requirements) hashing.
* Selecteer de naamruimte `PHONE_E.164` als bronidentiteit als uw gegevens uit niet-gehashte telefoonnummers bestaan. [!DNL Experience Platform] hasht de telefoonnummers om te voldoen aan [!DNL Google Customer Match] -vereisten.
* Selecteer `Phone_SHA256_E.164` namespace als bronidentiteit als u telefoonaantallen op gegevensinvoer in [!DNL Experience Platform] hashing, volgens [!DNL Facebook] [ de hashing vereisten van het telefoonaantal ](#phone-number-hashing-requirements).
* Selecteer de naamruimte `IDFA` als bronidentiteit als uw gegevens uit [!DNL Apple] apparaat-id&#39;s bestaan.
* Selecteer de naamruimte `GAID` als bronidentiteit als uw gegevens uit [!DNL Android] apparaat-id&#39;s bestaan.
* Selecteer de naamruimte `Custom` als bronidentiteit als uw gegevens uit andere id&#39;s bestaan.

Doelvelden selecteren:

* Selecteer de naamruimte `Email_LC_SHA256` als doelidentiteit wanneer de bronnaamruimten `Email` of `Email_LC_SHA256` zijn.
* Selecteer de naamruimte `Phone_SHA256_E.164` als doelidentiteit wanneer de bronnaamruimten `PHONE_E.164` of `Phone_SHA256_E.164` zijn.
* Selecteer `IDFA` of `GAID` naamruimten als doelidentiteit wanneer uw bronnaamruimten `IDFA` of `GAID` zijn.
* Selecteer de naamruimte `User_ID` als doelidentiteit wanneer de bronnaamruimte een aangepaste naamruimte is.

![ Identiteitskaart die tussen bron en doelgebieden in de stap van de Afbeelding van het activeringswerkschema wordt getoond.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Gegevens uit naamruimten zonder hashing worden automatisch gehasht door [!DNL Experience Platform] bij activering.

Kenmerkbrongegevens worden niet automatisch gehasht. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] .

![ pas transformatiecontrole toe die in de stap van de Afbeelding van het activeringswerkschema wordt benadrukt.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Doel van monitor {#monitor-destination}

Na het verbinden met de bestemming en het vestigen van een bestemmingsdataflow, kunt u de [ controlefunctionaliteit ](/help/dataflows/ui/monitor-destinations.md) in Real-Time CDP gebruiken om uitgebreide informatie over de profielverslagen te krijgen die aan uw bestemming in elke dataflow in werking worden gesteld.

>[!IMPORTANT]
>
>Wanneer u de vier aan het adres gerelateerde doelidentiteiten (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` en `address_info_postal_code`) toewijst, worden ze geteld als afzonderlijke identiteiten voor elk profiel in de controlepagina voor gegevensstroom.

## Controleren of publieksactivering is gelukt {#verify-activation}

Schakel over naar uw **[!UICONTROL Google Ads]** -account nadat u de activeringsstroom hebt voltooid. Het geactiveerde publiek wordt in uw Google-account weergegeven als klantenlijsten. Afhankelijk van de grootte van uw publiek, bevolken sommige soorten publiek alleen als er meer dan 100 actieve gebruikers zijn om te dienen.

Wanneer u een publiek toewijst aan zowel [!DNL IDFA] als [!DNL GAID] mobiele id&#39;s, maakt [!DNL Google Customer Match] een apart publiek voor elke id-toewijzing. Uw [!DNL Google Ads] -account geeft twee verschillende segmenten weer, een voor de [!DNL IDFA] -account en een voor de [!DNL GAID] -toewijzing.

## Problemen oplossen {#troubleshooting}

### 400 Onjuist aanvraagfoutbericht {#bad-request}

Wanneer het vormen van deze bestemming, kunt u de volgende fout ontvangen:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Deze fout komt voor wanneer de klantenrekeningen niet aan de [ eerste vereisten ](#google-account-prerequisites) voldoen. Neem contact op met Google om dit probleem op te lossen en zorg ervoor dat uw account op de lijst met toegestane items staat en geconfigureerd is voor een machtigingsniveau van [!DNL Standard] of hoger. Zie de [ documentatie van Ads van Google ](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) voor details.