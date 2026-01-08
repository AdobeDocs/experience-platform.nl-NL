---
keywords: mobiel; bruin; berichten;
title: Braze verbinding
description: Braze is een uitgebreid platform voor klantbetrokkenheid dat relevante en gedenkwaardige ervaringen tussen klanten en de merken die ze leuk vinden, mogelijk maakt.
last-substantial-update: 2024-08-20T00:00:00Z
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: cc97efec5fba090378ceaf73441d0b4bd7fbf51f
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 0%

---

# [!DNL Braze]-verbinding

## Overzicht {#overview}

Met het doel [!DNL Braze] kunt u profielgegevens naar [!DNL Braze] verzenden.

[!DNL Braze] is een uitgebreid platform voor klantenservice dat relevante en gedenkwaardige ervaringen tussen klanten en de merken die ze leuk vinden, mogelijk maakt.

Als u profielgegevens naar [!DNL Braze] wilt verzenden, moet u eerst verbinding maken met het doel.

## Doelspecificaties {#specifics}

Let op de volgende details die specifiek zijn voor het doel van [!DNL Braze] :

* [!DNL Adobe Experience Platform] publiek wordt geëxporteerd naar [!DNL Braze] under het `AdobeExperiencePlatformSegments` kenmerk.

>[!NOTE]
>
>Vergeet niet dat het verzenden van extra aangepaste kenmerken naar [!DNL Braze] kan leiden tot een toename van het [!DNL Braze] -verbruik van gegevenspunten. Neem contact op met uw [!DNL Braze] -accountmanager voordat u aanvullende aangepaste kenmerken verzendt.

## Gebruiksscenario’s {#use-cases}

Als markeerteken wil ik gebruikers in een mobiele betrokkenheidsbestemming aanwijzen, met een publiek dat is ingebouwd in [!DNL Adobe Experience Platform] . Daarnaast wil ik hen persoonlijke ervaringen bieden op basis van kenmerken uit hun [!DNL Adobe Experience Platform] -profielen, zodra het publiek en de profielen worden bijgewerkt in [!DNL Adobe Experience Platform] .

## Ondersteunde identiteiten {#supported-identities}

[!DNL Braze] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| external_id | Aangepaste [!DNL Braze] id die het toewijzen van elke identiteit ondersteunt. | U kunt om het even welke [ identiteit ](../../../identity-service/features/namespaces.md) naar de [!DNL Braze] bestemming verzenden, zolang u het aan [!DNL Braze] in kaart brengt [`external_id` ](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

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
|---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam) en/of identiteiten volgens uw veldtoewijzing.[!DNL Adobe Experience Platform] publiek wordt geëxporteerd naar [!DNL Braze] under het `AdobeExperiencePlatformSegments` kenmerk. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

* **[!UICONTROL Braze account token]**: dit is de [!DNL Braze] [!DNL API] -toets. U kunt gedetailleerde instructies op vinden hoe te om uw [!DNL API] sleutel hier te verkrijgen: [ REST API Zeer belangrijk Overzicht ](https://www.braze.com/docs/api/api_key/).

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]** : voer een naam in waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]** : voer een beschrijving in die u helpt deze bestemming in de toekomst te identificeren.
* **[!UICONTROL Endpoint Instance]**: alle [ gebied-specifieke eindpunten ](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) die door [!DNL Braze] worden gesteund zijn beschikbaar voor selectie. Vraag uw [!DNL Braze] vertegenwoordiger welke eindpuntinstantie u zou moeten gebruiken.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [ publieksgegevens aan het stromen publiek de uitvoerbestemmingen ](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

## Toewijzingsoverwegingen {#mapping-considerations}

Als u de publieksgegevens correct vanuit [!DNL Adobe Experience Platform] naar het [!DNL Braze] -doel wilt verzenden, moet u de stap voor veldtoewijzing doorlopen.

Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden [!DNL Experience Data Model] (XDM) in uw [!DNL Experience Platform] -account en de bijbehorende equivalenten van de doelbestemming.

Voer de volgende stappen uit om uw XDM-velden correct toe te wijzen aan de [!DNL Braze] -doelvelden:

Klik in de stap [!UICONTROL Mapping] op **[!UICONTROL Add new mapping]** .

![ Wrijf Bestemming toevoegen Toewijzing ](../../assets/catalog/mobile-engagement/braze/mapping.png)

Klik in de sectie [!UICONTROL Source Field] op de pijlknop naast het lege veld.

![ de Afbeelding van Source van de Bestemming van de Wrijvel ](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

In het venster [!UICONTROL Select source field] kunt u kiezen uit twee categorieën XDM-velden:

* [!UICONTROL Select attributes]: gebruik deze optie om een specifiek veld van uw XDM-schema toe te wijzen aan een [!DNL Braze] -kenmerk.

![ breid de Attributen van Source van de Bestemming in kaart ](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Select identity namespace]: Gebruik deze optie om een naamruimte [!DNL Experience Platform] identity aan een naamruimte [!DNL Braze] toe te wijzen.

![ Bodembestemming die Source Namespace ](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png) in kaart brengt

Kies het bronveld en klik op **[!UICONTROL Select]** .

Klik in de sectie [!UICONTROL Target Field] op het koppelingspictogram rechts van het veld.

![ breid het Doel Toewijzing van het Doel ](../../assets/catalog/mobile-engagement/braze/mapping-target.png) uit

In het venster [!UICONTROL Select target field] kunt u kiezen uit twee categorieën doelvelden:

* [!UICONTROL Select identity namespace]: Gebruik deze optie om [!DNL Experience Platform] naamruimten toe te wijzen aan [!DNL Braze] naamruimten.
* [!UICONTROL Select custom attributes]: Gebruik deze optie om XDM-kenmerken toe te wijzen aan aangepaste [!DNL Braze] -kenmerken die u in uw [!DNL Braze] -account hebt gedefinieerd. <br> U kunt deze optie ook gebruiken om de naam van bestaande XDM-kenmerken te wijzigen in [!DNL Braze] . Als u bijvoorbeeld een `lastName` XDM-kenmerk toewijst aan een aangepast `Last_Name` -kenmerk in [!DNL Braze] , wordt het `Last_Name` -kenmerk in [!DNL Braze] gemaakt, als dat nog niet het geval is, en wordt het `lastName` XDM-kenmerk eraan toegewezen.

![ breid de Gebieden van de Toewijzing van het Doel van de Bestemming ](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png) uit

Kies het doelveld en klik op **[!UICONTROL Select]** .

Nu wordt de veldtoewijzing weergegeven in de lijst.

![ Volledige Toewijzing van de Bestemming van het Wrijven ](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Herhaal de vorige stappen om meer toewijzingen toe te voegen.

## Voorbeeld van toewijzing {#mapping-example}

Stel dat uw XDM-profielschema en uw [!DNL Braze] -instantie de volgende kenmerken en identiteiten bevatten:

|  | XDM-profielschema | [!DNL Braze] Instantie |
|---|---|---|
| Attributen | <ul><li><code> person.name.firstName</code></li><li><code> person.name.lastName</code></li><li><code> mobilePhone.number</code></li></ul> | <ul><li><code> FirstName</code></li><li><code> LastName</code></li><li><code> PhoneNumber</code></li></ul> |
| Identiteiten | <ul><li><code> E-mail</code></li><li><code> identiteitskaart van Google (GAID)</code></li><li><code> identiteitskaart van Apple voor Advertisers (IDFA)</code></li></ul> | <ul><li><code> external_id</code></li></ul> |

De juiste toewijzing zou er als volgt uitzien:

![ breid het Voorbeeld van de Afbeelding van de Bestemming ](../../assets/catalog/mobile-engagement/braze/mapping-example.png) uit

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL Braze] -account om te controleren of gegevens naar de [!DNL Braze] -bestemming zijn geëxporteerd. [!DNL Adobe Experience Platform] publiek wordt geëxporteerd naar [!DNL Braze] under het `AdobeExperiencePlatformSegments` kenmerk.

## Problemen oplossen {#troubleshooting}

**ik ontving een onderbrekingsfout terwijl het activeren van mijn publiek aan deze bestemming. Wat moet ik doen?**

Soms kan activering van het publiek naar deze bestemming leiden tot een time-outfout. Deze fout geeft niet altijd een activeringsprobleem aan.

Als er een time-outfout optreedt, controleert u de publieksgrootte in het doelplatform. Als de publieksgrootte correct is, dan werkt de integratie zoals verwacht.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie [ Overzicht van de Governance van Gegevens ](../../../data-governance/home.md).
