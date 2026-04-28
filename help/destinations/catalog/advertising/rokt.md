---
title: Rokt
description: Leer hoe u het Adobe Experience Platform-publiek koppelt aan Rokt om de campagneprestaties te verbeteren door slimmer te kiezen, onderdrukken en personaliseren.
source-git-commit: a281a7c961b8576105913feb7a7f8258c975e875
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---


# [!DNL Rokt] verbinding {#rokt-destination}

## Overzicht {#overview}

[[!DNL Rokt] &#x200B;](https://www.rokt.com) ontgrendelt waarde in e-commerce gebruikend AI-gedreven real-time besluitvorming om elke Transactie Moment™ relevanter te maken. Het biedt persoonlijke ervaringen en verbindt adverteerders met klanten met hoge bedoelingen. Verbind [!DNL Adobe Experience Platform] publiek met [!DNL Rokt] om campagneprestaties door slimmer richten, onderdrukking, en verpersoonlijking te verbeteren. Bereik de juiste klanten op het juiste moment en verlaag de verspilde uitgaven.

>[!IMPORTANT]
>
>De doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van [!DNL Rokt] . Neem voor vragen of verzoeken om updates contact op met uw [!DNL Rokt] accountmanager of neem contact op met `support@rokt.com` .

## Gebruiksscenario&#39;s {#use-cases}

De volgende gebruiksgevallen laten zien hoe [!DNL Experience Platform] -klanten het [!DNL Rokt] -doel kunnen gebruiken.

### Hoofdletters/kleine letters gebruiken 1: Opnieuw rangschikken {#use-case-1}

Neem klanten met een hoge intentie opnieuw op die uw site of app hebben bezocht maar deze niet hebben geconverteerd. Bouw een publiek in [!DNL Experience Platform] met inbegrip van gebruikers die door specifieke productcategorieën doorbladeren of een controlestroom verlieten. Duw dan dat publiek aan [!DNL Rokt] om gepersonaliseerde aanbiedingen op het punt van aankoop op partnerplaatsen te dienen. [!DNL Rokt] werkt binnen het transactiemiddel, direct nadat een klant een aankoop elders heeft voltooid. Wanneer de aankoopintentie het hoogst is, wordt een publiek bereikt dat met een lager rendement is benaderd. Dit leidt tot hogere conversiesnelheden dan bij traditionele heroriëntatie van het beeldscherm.

### Hoofdlettergebruik 2: Onderdrukkingslijsten {#use-case-2}

Voorkom verspilde uitgaven en irrelevante ervaringen door het publiek te onderdrukken dat bepaalde [!DNL Rokt] -aanbiedingen niet moet ontvangen. Veelvoorkomende gevallen van suppressie zijn onder andere het uitsluiten van recente converters, loyaliteitsleden bij een actieve promotie of gebruikers die ervoor hebben gekozen niet langer op de markt te komen. Sluit bijvoorbeeld klanten uit die de afgelopen 30 dagen hebben aangeschaft. Synchroniseer deze onderdrukkingssoorten van [!DNL Experience Platform] naar [!DNL Rokt] in real-time. Hierdoor blijven campagnes gericht op nieuwe of opnieuw aanspreekbare gebruikers. Dit verbetert ROI en beschermt de klantenervaring.

## Vereisten {#prerequisites}

Voordat u de [!DNL Rokt] bestemming instelt in [!DNL Adobe Experience Platform] , moet u de volgende referenties aanvragen bij uw **[!DNL Rokt]accountmanager** :

* **API Sleutel**: gebruik dit als **[!UICONTROL Username]** wanneer [&#x200B; het voor authentiek verklaren van de bestemmingsverbinding &#x200B;](#authenticate).
* **API Geheim**: gebruik dit als **[!UICONTROL Password]** wanneer [&#x200B; het voor authentiek verklaren van de bestemmingsverbinding &#x200B;](#authenticate).

Uw accountmanager van [!DNL Rokt] zal deze gegevens op het [!DNL Rokt] -platform beschikbaar stellen voordat u het programma instelt. Neem contact op met uw accountmanager als u deze nog niet hebt ontvangen.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Rokt] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| email | E-mailadres voor normale tekst | Aanbevolen. Wordt gebruikt voor profielovereenkomst in [!DNL Rokt] . |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Zowel platte tekst als gehashte e-mailadressen van SHA256 worden ondersteund. Wanneer het bronveld hashingkenmerken bevat, selecteert u de optie **[!UICONTROL Apply transformation]** om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| telefoon | Telefoonnummer normale tekst | Wordt gebruikt voor profielovereenkomst in [!DNL Rokt] . |
| phone_sha256 | Telefoonnummers die zijn hashed met het SHA256-algoritme | Zowel gewone tekst als SHA256 gehashte telefoonaantallen worden gesteund. Wanneer het bronveld hashingkenmerken bevat, selecteert u de optie **[!UICONTROL Apply transformation]** om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| GAID | [!DNL Google] Advertising-id | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | [!DNL Apple] ID voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |
| aepProfileId | [!DNL Adobe Experience Platform] Profiel-id | Wijst identiteitskaart van het Profiel (`xdm:_id`) als reserve herkenningsteken toe. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Soorten publiek dat wordt gegenereerd via de [!DNL Experience Platform] [[!DNL Segmentation Service]](/help/segmentation/home.md) . |
| Alle andere doelgroepen | Ja | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [&#x200B; diverse publieksoorsprong &#x200B;](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [&#x200B; ingevoerde &#x200B;](/help/segmentation/ui/audience-portal.md#import-audience) in [!DNL Experience Platform] van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere [!DNL Experience Platform] -toepassingen, zoals [!DNL Adobe Journey Optimizer] , </li><li> en meer. </li></ul> |

{style="table-layout:auto"}

Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
|--------------------|-----------|-------------|-----------|
| [&#x200B; het publiek van Mensen &#x200B;](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantprofielen. Gebruik deze schema&#39;s om specifieke groepen mensen te kiezen voor marketingcampagnes. | Frequente kopers, winkeliers |
| [&#x200B; publiek van de Rekening &#x200B;](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [&#x200B; Het publiek van het Vooruitzicht &#x200B;](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [&#x200B; de uitvoer van de Dataset &#x200B;](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het [!DNL Adobe Experience Platform] Data Lake. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (e-mail, telefoon, mobiele advertentie-id of andere) die in de [!DNL Rokt] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in [!DNL Experience Platform] wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar [!DNL Rokt]. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](/help/destinations/ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

* **[!UICONTROL Username]** : Uw API-sleutel, verstrekt door uw [!DNL Rokt] accountmanager.
* **[!UICONTROL Password]** : Uw API-geheim, opgegeven door uw [!DNL Rokt] -accountmanager.

  ![&#x200B; het [!DNL Rokt] scherm van de bestemmingsconfiguratie in [!DNL Experience Platform], met rekeningsdetails, authentificatievelden, en bestemmingsdetails die worden gevuld.](/help/destinations/assets/catalog/advertising/rokt/aep-configure-destination.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]** : Een naam waarmee u deze bestemming in de toekomst zult erkennen (bijvoorbeeld, &quot; [!DNL Rokt] - het Opnieuw richten van Publiek&quot;).
* **[!UICONTROL Description]** : Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](/help/destinations/ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

Het doel [!DNL Rokt] ondersteunt het toewijzen van naamruimten van [!DNL Experience Platform] naar [!DNL Rokt] identiteitsvelden. U moet ten minste één identiteit toewijzen om een publiek te activeren. De aanbevolen toewijzingen worden weergegeven in de onderstaande tabel.

| Source-veld | Doelveld | Overwegingen |
|---|---|---|
| `IdentityMap: Email` | `Identity: email` | Aanbevolen |
| `IdentityMap: Email_LC_SHA256` | `Identity: emailSha256` | Aanbevolen |
| `IdentityMap: Phone` | `Identity: phone` | Optioneel |
| `IdentityMap: Phone_SHA256` | `Identity: phoneSha256` | Optioneel |
| `IdentityMap: GAID` | `Identity: gaid` | Optioneel |
| `IdentityMap: IDFA` | `Identity: idfa` | Optioneel |
| `xdm: _id` | `Identity: aepProfileId` | Optioneel |

{style="table-layout:auto"}

Hier volgt een voorbeeld van een volledige toewijzing:

![&#x200B; de afbeeldingsstap van het [!DNL Rokt] werkschema van de bestemmingsactivering in [!DNL Experience Platform], met bron en gevormde gebieden van de doelidentiteit.](/help/destinations/assets/catalog/advertising/rokt/aep-identity-mapping.png)

>[!NOTE]
>
>Ten minste één identiteitstoewijzing op basis van e-mail (`email` of `emailSha256` ) wordt ten zeerste aanbevolen om de overeenkomende snelheden in [!DNL Rokt] te maximaliseren.

### Programma voor publiek configureren {#audience-schedule}

Nadat u de toewijzingsstap hebt voltooid, configureert u een publieksprogramma voor elk geselecteerd publiek. Geef een **[!UICONTROL Start date]** op voor het tijdstip waarop het publiek moet beginnen met synchroniseren en een **[!UICONTROL Mapping ID]** (een label dat wordt gebruikt om dit publiek binnen [!DNL Rokt] te identificeren). U kunt de publieksnaam van [!DNL Experience Platform] gebruiken of een beschrijvende tekenreeks waarmee u en uw [!DNL Rokt] -accountmanager het publiek kunnen identificeren.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Experience Platform] gegevensbeheer afdwingt, lees het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

* [[!DNL Rokt] documentatie voor ontwikkelaars](https://docs.rokt.com)
* [Overzicht Adobe Experience Platform-bestemmingen](/help/destinations/home.md)
