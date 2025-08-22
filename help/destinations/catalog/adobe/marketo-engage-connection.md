---
title: Marketo Engage-verbinding
description: Marketo Engage is de enige CXM-oplossing (end-to-end Customer Experience Management) voor marketing, reclame, analyse en handel. Hiermee kunt u activiteiten automatiseren en beheren van CRM-beheer en de betrokkenheid van klanten tot marketing en inkomstentoewijzing op basis van account.
source-git-commit: 88864353d4872d62258914d6490b90331692fa96
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 0%

---


# Marketo Engage-verbinding

## Overzicht {#overview}

[!DNL Marketo Engage] is de enige CXM-oplossing (end-to-end Customer Experience Management) voor marketing, reclame, analyse en handel. Hiermee kunt u activiteiten automatiseren en beheren van CRM-beheer en de betrokkenheid van klanten tot marketing en inkomstentoewijzing op basis van account.

Gebruik deze bestemming voor synchronisatie in real time van publieksgegevens en profielattributen tussen Adobe Experience Platform en Marketo Engage.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Marketo Engage] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Gebruiksscenario&#39;s voor publiekssynchronisatie {#audience-sync-use-cases}

**herhaal bekende slechts lood**

Het marketingteam wil een win-back campagne voeren voor leiders die zich niet meer dan 90 dagen hebben ingezet, maar al bestaan in Marketo.

Ze kunnen het publiek naar Marketo Engage activeren en het synchronisatietype **[!UICONTROL Audience Only]** gebruiken.

### Gebruiksgevallen voor publiek- en profielsynchronisatie {#audience-profile-sync-use-cases}

**herhaal bekende lood en werk lood bij**

Het marketingteam wil een campagne starten voor een nieuwe betrokkenheid voor bestaande Marketo-contactpersonen die belangstelling hebben getoond op basis van websitebezoeken. Ze willen ook de leidende informatie (zoals voorkeuren, demografische informatie) bijwerken, maar geen nieuwe mensen in Marketo maken.

Ze kunnen het publiek naar Marketo Engage activeren en het synchronisatietype **[!UICONTROL Audience and Profile]** in combinatie met de handeling **[!UICONTROL Update existing persons only]** gebruiken om ervoor te zorgen dat alleen het publiek wordt bereikt dat al in Marketo bestaat.

**herhaal en breid bereik met volledige profielsynchronisatie** uit

Het marketingteam wil een publiek met belangstelling voor een product activeren voor een nieuwe campagne. Hoewel veel van de profielen al bestaan in Marketo, zijn sommige nieuw en komen ze alleen voor in Real-Time CDP. Voor de bestaande mensen willen ze ervoor zorgen dat ze die mensen in Marketo bijwerken, maar ze willen ook nieuwe profielen maken.

Ze kunnen hun publiek in Marketo Engage activeren en het **[!UICONTROL Audience and Profile]** sync-type in combinatie met de **[!UICONTROL Update existing and create new persons]** -actie gebruiken om ervoor te zorgen dat ze zich richten op bestaande leads uit Marketo en nieuwe maken voor het nieuwe publiek dat wordt geëxporteerd uit Real-Time CDP.

## Vereisten {#prerequisites}

De gebruiker die opstelling de bestemming moet [ hebben uitgeeft Persoon ](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions#access-database) toestemming in hun instantie en verdeling van Marketo.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Marketo Engage] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| `DedupeField` | Het veld dat wordt gebruikt voor het identificeren en afstemmen van bestaande leads in Marketo. | Tijdens de [ toewijzingsstap ](#mapping), kaart om het even welk brongebied (zoals `Email` of andere douanedetectie) dat u als deduplicatiegebied aan deze doelidentiteit wilt gebruiken. Voor de beste resultaten kiest u een veld dat consistent beschikbaar en uniek is in al uw klantprofielen. `ECID` wordt niet ondersteund als een deduplicatieveld. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren. De twee lijsten hieronder wijzen op welk publiek deze schakelaar steunt, door _kijkoorsprong_ en _profieltypes inbegrepen in het publiek_:

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [ ](../../../segmentation/home.md). |
| Alle andere doelgroepen | ✓ | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [ diverse publieksoorsprong ](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere Experience Platform-apps, zoals Adobe Journey Optimizer; </li><li> en meer. </li></ul> <br> |

{style="table-layout:auto"}

Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario’s |
|--------------------|-----------|-------------|-----------|
| [ het publiek van Mensen ](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantenprofielen, die u toestaan om specifieke groepen mensen voor marketing campagnes te richten. | Frequente kopers, winkeliers |
| [ publiek van de Rekening ](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [ Het publiek van het Vooruitzicht ](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [ de uitvoer van de Dataset ](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het Data Lake van Adobe Experience Platform. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (e-mail, ECID) die in de [!DNL Marketo Engage] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Overeenkomend gedrag voor lead {#lead-matching}

Als u begrijpt hoe Marketo lead matching werkt, kunt u de juiste configuratie voor uw gebruikscase kiezen. Het overeenkomende gedrag is afhankelijk van de geselecteerde instellingen **[!UICONTROL Sync Type]** en **[!UICONTROL Person Action]** .

Marketo gebruikt de **[!UICONTROL Marketo deduplication field]** die u selecteert om Experience Platform-profielen aan te passen aan bestaande Marketo-leads. Het overeenkomende proces zoekt in alle partities in uw Marketo-instantie naar bestaande leads. Raadpleeg de onderstaande tabel voor meer informatie over het maken en bijwerken van leads in uw Marketo-exemplaar, afhankelijk van de geselecteerde configuratie.

| Type synchronisatie | Persoonsactie | Gelijkend gedrag |
|-----------|---------------|-------------------|
| **[!UICONTROL Profile only]** | **[!UICONTROL Update existing and create new persons]** | <ul><li>Bestaande leads bijwerken met nieuwe profielgegevens</li><li>Hiermee maakt u nieuwe leads in de geselecteerde partitie voor profielen zonder overeenkomst</li></ul> |
| **[!UICONTROL Profile only]** | **[!UICONTROL Update existing persons only]** | <ul><li>Bestaande leads bijwerken met nieuwe profielgegevens</li><li>Geen nieuwe leads gemaakt voor niet-overeenkomende profielen</li></ul> |
| **[!UICONTROL Audience only]** | N.v.t. | <ul><li>Bestaande leads toevoegen aan publiekslijsten</li><li>Geen nieuwe leads gemaakt voor niet-overeenkomende profielen</li></ul> |
| **[!UICONTROL Audience and profile]** | **[!UICONTROL Update existing and create new persons]** | <ul><li>Bestaande leads bijwerken met nieuwe profielgegevens</li><li>Bestaande leads toevoegen aan publiekslijsten</li><li>Hiermee maakt u nieuwe leads in de geselecteerde partitie voor profielen zonder overeenkomst</li><li>Nieuwe leads toevoegen aan publiekslijsten</li></ul> |
| **[!UICONTROL Audience and profile]** | **[!UICONTROL Update existing persons only]** | <ul><li>Bestaande leads bijwerken met nieuwe profielgegevens</li><li>Bestaande leads toevoegen aan publiekslijsten</li><li>Geen nieuwe leads gemaakt voor niet-overeenkomende profielen</li></ul> |

{style="table-layout:auto"}

### Belangrijke overwegingen

* **de selectie van het het gebiedsselectie van de Deduplicatie**: Kies een gebied dat constant beschikbaar en uniek over uw klantenprofielen (bijvoorbeeld: e-mailadres, klantenidentiteitskaart) is
* **Verwerking van de Verdeling**: Wanneer het creëren van nieuwe lood, worden zij geplaatst in uw geselecteerde verdeling (of **[!UICONTROL Default]** verdeling als u geen verdeling selecteerde)
* **Dubbele behandeling**: Als de veelvoudige lood van Marketo het zelfde profiel aanpast, slechts zal de onlangs bijgewerkte lood worden bijgewerkt
* **dwars-verdeling aanpassing**: De systeemonderzoeken over alle verdelingen om bestaande lood te vinden, ongeacht welke verdeling u voor nieuwe lood hebt geselecteerd

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>* Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig.
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Selecteer **[!UICONTROL Connect to destination]** als u wilt verifiëren bij het doel.

![ Schermschot die tonen hoe te om aan de bestemming ](../../assets/catalog/adobe/marketo-engage-connection/connect-destination.png) voor authentiek te verklaren

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![ het schermschot van de Steekproef die hoe te om details voor uw bestemming te vullen ](../../assets/catalog/adobe/marketo-engage-connection/destination-details.png) tonen

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Munchkin ID]**: selecteer [!DNL Marketo Munchkin ID] die u voor dit doel wilt gebruiken.
* **[!UICONTROL Workspace ID]**: selecteer de Marketo-werkruimte-id.
* **[!UICONTROL Sync type]**: Selecteer het synchronisatietype dat u voor dit doel wilt gebruiken:
   * **[!UICONTROL Audience and profile]**: selecteer deze optie als u zowel publieksleden wilt toevoegen aan Marketo-lijsten als hun profielgegevens up-to-date wilt houden.
   * **[!UICONTROL Profile only]**: selecteer deze optie als u de Marketo-lead-profielen up-to-date wilt houden met de meest recente informatie van Experience Platform.
   * **[!UICONTROL Audience only]**: selecteer deze optie als u leden van het publiek wilt toevoegen aan Marketo-lijsten zonder hun profielgegevens bij te werken.
* **[!UICONTROL Partition]**: *de selectie van de Verdeling is beschikbaar slechts wanneer het kiezen **[!UICONTROL Profile only]**of **[!UICONTROL Audience and profile]**synchronisatietypen*. Selecteer een Marketo-partitie-id die is gekoppeld aan uw gekozen werkruimte. Op deze manier kunt u opgeven welke hoofdpartitie in Marketo de geëxporteerde gegevens ontvangt. Als u geen specifieke partitie kiest, worden uw gegevens naar de **[!UICONTROL Default]** -partitie in Marketo verzonden.
* **[!UICONTROL Marketo deduplication field]**: selecteer het Marketo-deduplicatieveld dat u wilt gebruiken bij het bijwerken van bestaande Marketo-leads. Deze kiezer toont de velden die u hebt gemarkeerd als deduplicatievelden in Marketo. Als u een specifiek gebied van Marketo als deduplicatieveld wilt tonen, moet u het gebied als a [ doorzoekbaar gebied ](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/lead-database) in Marketo merken.

  >[!NOTE]
  >
  >Marketo `Lead ID` en Experience Cloud IDs (`ECID`) worden niet gesteund voor deduplicatie.

* **[!UICONTROL Person Action]**: selecteer de Marketo-handeling die u wilt uitvoeren bij het exporteren van gegevens.
   * **[!UICONTROL Update existing and create new persons]**: selecteer deze optie om bestaande Marketo-leads bij te werken en nieuwe leads te maken voor publieksleden die zich nog niet in Marketo bevinden. Nieuwe leads worden gemaakt in de geselecteerde partitie. Als u geen partitie hebt geselecteerd, worden nieuwe leads gemaakt in de **[!UICONTROL Default]** -partitie.
   * **[!UICONTROL Update existing persons only]**: selecteer deze optie als u alleen bestaande Marketo-leads wilt bijwerken zonder nieuwe te maken. Als meerdere leads overeenkomen met hetzelfde profiel, wordt alleen de meest recente bijgewerkte Marketo lead bijgewerkt met uw Experience Platform-gegevens.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, lees de gids over [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Vereiste toewijzingen {#required-mappings}

Wijs tijdens de toewijzingsstap elk bronveld (zoals `email` of andere aangepaste id&#39;s) dat u als deduplicatieveld wilt gebruiken, toe aan de `DedupeField` -doelidentiteit. Voor de beste resultaten kiest u een veld dat consistent beschikbaar en uniek is in al uw klantprofielen.

Marketo kan alleen leads maken als u ook de volgende vereiste doelkenmerken toewijst:

* `firstName`: De voornaam van de lead
* `lastName`: De achternaam van de lead
* `email`: Het e-mailadres van de lead

Als u `email` als deduplicatieveld gebruikt, moet u ook de kenmerken `firstName` en `lastName` toewijzen, zoals in de onderstaande afbeelding wordt getoond.

![ Schermafbeelding die vereiste afbeelding tonen wanneer het gebruiken van E-mail als deduplicatieveld ](../../assets/catalog/adobe/marketo-engage-connection/required-mapping-email-dedupe.png)

Als u een ander deduplicatieveld gebruikt, moet u de drie vereiste kenmerken (`firstName`, `lastName`, `email`) handmatig toewijzen, zoals in de onderstaande afbeelding wordt getoond.

![ Schermafbeelding die vereiste afbeelding tonen wanneer het gebruiken van E-mail niet als deduplicatieveld ](../../assets/catalog/adobe/marketo-engage-connection/required-mapping-email.png)

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Nadat u een publiek naar Marketo Engage hebt geëxporteerd, meldt u zich aan bij uw Marketo-account om te controleren of het publiek naar behoren is geactiveerd. Controleer de relevante hoofdpartities en werkruimten in Marketo om te bevestigen dat de publieksgegevens correct worden weergegeven en dat de beoogde acties (zoals het bijwerken of maken van personen) zijn uitgevoerd.

Als u de verwachte gegevens niet ziet, controleert u de toewijzing- en exportinstellingen in Adobe Experience Platform en probeert u het exporteren opnieuw.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).
