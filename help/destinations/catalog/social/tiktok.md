---
title: TikTok-verbinding
description: Bouw een aangepast publiek op TikTok met uw gegevens voor doelgerichte advertentiecampagnes. Dit soort publiek zou kunnen bestaan uit mensen die uw website hebben bezocht of interactie hebben gehad met uw inhoud. Snel en veilig het gewenste publiek van Adobe Experience Platform naar TikTok duwen met Adobe in real-time integratie met TikTok Ads Manager.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 1%

---

# TikTok-verbinding

## Overzicht {#overview}

Bouw een aangepast publiek op TikTok met uw gegevens voor doelgerichte advertentiecampagnes. Dit soort publiek zou kunnen bestaan uit mensen die uw website hebben bezocht of interactie hebben gehad met uw inhoud. Snel en veilig het gewenste publiek van Adobe Experience Platform naar TikTok duwen met Adobe in real-time integratie met TikTok Ads Manager. Bezoek [&#x200B; TikTok bedrijfs hulpcentrum &#x200B;](https://ads.tiktok.com/help/article/audiences) voor meer informatie.

>[!IMPORTANT]
>
>Deze doelconnector en documentatiepagina worden gemaakt en onderhouden door het TikTok-team. Voor om het even welke onderzoeken of updateverzoeken, gelieve hen direct in [&#x200B; https://ads.tiktok.com/help/ &#x200B;](https://ads.tiktok.com/help/) te contacteren.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de bestemming van TikTok zou moeten gebruiken, is hier een voorbeeld gebruiksgeval voor klanten van Adobe Experience Platform.

### Gebruiksscenario {#use-case-1}

Een atletisch merk kledingartikelen wil bestaande klanten bereiken via hun sociale-mediakanalen. Het merk apparel kan e-mailadressen van zijn eigen CRM aan Adobe Experience Platform opnemen, publiek maken van zijn eigen offline gegevens en deze soorten publiek naar TikTok sturen om advertenties weer te geven in de sociale media van hun klanten.

## Vereisten {#prerequisites}

U moet [!DNL Admin] of [!DNL Operator] toegang hebben tot de TikTok Ads Manager-account waarnaar u het publiek wilt sturen. Meer instructies kunnen op het [&#x200B; Centrum van de Hulp van TikTok &#x200B;](https://ads.tiktok.com/help/article/add-users-tiktok-business-center) worden gevonden.

Voordat u gegevens naar uw TikTok Ads Manager-account kunt verzenden, moet u Adobe Experience Platform toestemming geven om toegang te krijgen tot uw advertentieaccount voor `Audience Management` . Deze toestemming kan door [&#x200B; worden verleend ingaat uw identiteitskaart van de Manager van Advertenties &#x200B;](#authenticate) in Experience Platform UI en het verlenen van de toestemming na wordt opnieuw gericht aan uw Rekening van de Manager van de Advertentie van TikTok.

## Ondersteunde identiteiten {#supported-identities}

TikTok ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. Zowel onbewerkte tekst als SHA256 gehashte GAID-waarden worden ondersteund door Adobe Experience Platform. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. Zowel onbewerkte tekst als SHA256 hashed IDFA-waarden worden ondersteund door Adobe Experience Platform. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| Telefoonnummer | Telefoonnummers die zijn hashed met het SHA256-algoritme | Onbewerkte tekst en gehashte telefoonnummers van SHA256 worden ondersteund door Adobe Experience Platform en moeten de indeling E.164 hebben. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| Email | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |
| [!DNL Federated Audience Composition] | ✓ | Het publiek werd ingevoerd in Experience Platform door [&#x200B; Federated Samenstelling van het Publiek &#x200B;](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/start/audiences). |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de TikTok-bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, wordt u omgeleid naar uw [!DNL TikTok Ads Manager] -account en geeft u Adobe toestemming om namens u het publiek te beheren.

![&#x200B; Beeld van de toestemmingsselectie van TikTok van TikTok UI voor het selecteren van toestemmingen &#x200B;](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "")

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![&#x200B; de verbindingsdetails van de Bestemming &#x200B;](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png " Beeld van Experience Platform UI, die de details van de bestemmingsverbinding tonen in te vullen ")

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL TikTok Ads Manager ID]**: Uw [!DNL TikTok Ads Manager ID] . U kunt dit vinden in uw [!DNL TikTok Ads manager] account.

![&#x200B; identiteitskaart van de Manager van Advertentie van TikTok &#x200B;](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png " Beeld van de Manager UI van Advertentie van TikTok, die toont hoe te om identiteitskaart van de Manager van Advertentie van TikTok te krijgen ")

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Identiteiten toewijzen {#map}

Hieronder ziet u een voorbeeld van correcte identiteitstoewijzing bij het exporteren van soorten publiek naar TikTok Ads Manager.

Bronvelden selecteren:

* Selecteer een herkenningsteken (bijvoorbeeld:` Email_LC_SHA256`) als bronidentiteit die uniek een profiel in Adobe Experience Platform en [!DNL TikTok Ads Manager] identificeert.

Doelvelden selecteren:

* Selecteer de naamruimte E-mail als doel-id.

![&#x200B; het afbeelding van de Identiteit &#x200B;](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png " Beeld van Experience Platform UI, afbeelding van identiteiten ")

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL TikTok Ads Manager] rekening (onder **Assets > Soorten publiek**) om te verifiëren of uw publiek van Experience Platform met succes werd uitgevoerd. Het publiek wordt gevuld met het type publiek: `Partner Audience` .

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Gelieve te verwijzen naar de [&#x200B; pagina van het Centrum van de Hulp van TikTok &#x200B;](https://ads.tiktok.com/help/article/audiences) voor extra informatie.
