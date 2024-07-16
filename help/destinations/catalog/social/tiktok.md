---
title: TikTok-verbinding
description: Bouw een aangepast publiek op TikTok met uw gegevens voor doelgerichte advertentiecampagnes. Dit soort publiek zou kunnen bestaan uit mensen die uw website hebben bezocht of interactie hebben gehad met uw inhoud. Snel en veilig het gewenste publiek van Adobe Experience Platform naar TikTok duwen met behulp van de realtime integratie van Adobe met TikTok Ads Manager.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 1%

---

# TikTok-verbinding

## Overzicht {#overview}

Bouw een aangepast publiek op TikTok met uw gegevens voor doelgerichte advertentiecampagnes. Dit soort publiek zou kunnen bestaan uit mensen die uw website hebben bezocht of interactie hebben gehad met uw inhoud. Snel en veilig het gewenste publiek van Adobe Experience Platform naar TikTok duwen met behulp van de realtime integratie van Adobe met TikTok Ads Manager. Bezoek [ TikTok bedrijfs hulpcentrum ](https://ads.tiktok.com/help/article/audiences) voor meer informatie.

>[!IMPORTANT]
>
>Deze doelconnector en documentatiepagina worden gemaakt en onderhouden door het TikTok-team. Voor om het even welke onderzoeken of updateverzoeken, gelieve hen direct in [ https://ads.tiktok.com/help/ ](https://ads.tiktok.com/help/) te contacteren.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de bestemming van TikTok zou moeten gebruiken, is hier een voorbeeld gebruiksgeval voor klanten van Adobe Experience Platform.

### Gebruiksscenario {#use-case-1}

Een atletisch merk kledingartikelen wil bestaande klanten bereiken via hun sociale-mediakanalen. Het merk apparel kan e-mailadressen van zijn eigen CRM aan Adobe Experience Platform opnemen, publiek maken van zijn eigen offline gegevens en deze soorten publiek naar TikTok sturen om advertenties weer te geven in de sociale media van hun klanten.

## Vereisten {#prerequisites}

U moet [!DNL Admin] of [!DNL Operator] toegang hebben tot de TikTok Ads Manager-account waarnaar u het publiek wilt sturen. Meer instructies kunnen op het [ Centrum van de Hulp van TikTok ](https://ads.tiktok.com/help/article/add-users-tiktok-business-center) worden gevonden.

Voordat u gegevens naar uw TikTok Ads Manager-account kunt verzenden, moet u Adobe Experience Platform toestemming geven om toegang te krijgen tot uw advertentieaccount voor `Audience Management` . Deze toestemming kan door [ worden verleend ingaat uw identiteitskaart van de Manager van Advertenties ](#authenticate) in het Experience Platform UI en het verlenen van de toestemming na wordt opnieuw gericht aan uw Rekening van de Manager van de Advertentie van TikTok.

## Ondersteunde identiteiten {#supported-identities}

TikTok ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |
| Telefoonnummer | Telefoonnummers die zijn hashed met het SHA256-algoritme | Onbewerkte tekst en gehashte telefoonnummers van SHA256 worden ondersteund door Adobe Experience Platform en moeten de indeling E.164 hebben. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Platform] . |
| Email | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Platform] . |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de TikTok-bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren naar de bestemming, wordt u omgeleid naar uw [!DNL TikTok Ads Manager] -account en wordt u gemachtigd om het publiek namens u te beheren.

](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png " Beeld van de toestemmingsselectie van TikTok van TikTok UI voor het selecteren van toestemmingen ")![

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![ de verbindingsdetails van de Bestemming ](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png " Beeld van het Platform UI, die de details van de bestemmingsverbinding tonen in te vullen ")

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL TikTok Ads Manager ID]**: Uw [!DNL TikTok Ads Manager ID] . U kunt dit vinden in uw [!DNL TikTok Ads manager] account.

![ identiteitskaart van de Manager van Advertentie van TikTok ](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png " Beeld van de Manager UI van Advertentie van TikTok, die toont hoe te om identiteitskaart van de Manager van Advertentie van TikTok te krijgen ")

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Identiteiten toewijzen {#map}

Hieronder ziet u een voorbeeld van correcte identiteitstoewijzing bij het exporteren van soorten publiek naar TikTok Ads Manager.

Bronvelden selecteren:

* Selecteer een herkenningsteken (bijvoorbeeld:` Email_LC_SHA256`) als bronidentiteit die uniek een profiel in Adobe Experience Platform en [!DNL TikTok Ads Manager] identificeert.

Doelvelden selecteren:

* Selecteer de naamruimte E-mail als doel-id.

](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png " Beeld van de afbeelding van de Identiteit van het Platform UI, afbeelding van identiteiten ")![

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL TikTok Ads Manager] rekening (onder **Assets > Soorten publiek**) om te verifiëren of uw publiek van het Experience Platform met succes werd uitgevoerd. Het publiek wordt gevuld met het type publiek: `Partner Audience` .

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Gelieve te verwijzen naar de [ pagina van het Centrum van de Hulp van TikTok ](https://ads.tiktok.com/help/article/audiences) voor extra informatie.
