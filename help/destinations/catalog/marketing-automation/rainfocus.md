---
title: Deelnemerprofielen opnieuw instellen
description: Leer hoe u de doelconnector voor RainFocus-profielen van deelnemers gebruikt om de publieksprofielen te synchroniseren met het RainFocus Global-deelnemerprofiel.
last-substantial-update: 2024-12-17T00:00:00Z
exl-id: 27c3848c-411a-4305-a5d5-00b145b95287
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# Deelnemerprofielen opnieuw instellen {#rainfocus-destination}

## Overzicht {#overview}

Gebruik de bestemming [!DNL RainFocus Attendee Profiles] om klantprofielen te streamen van [!DNL Adobe Experience Platform] naar het [!DNL RainFocus] -platform om deelnemerprofielen te maken en bij te werken.

>[!IMPORTANT]
>
>De doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van [!DNL RainFocus] . Voor om het even welke onderzoeken of updateverzoeken, contacteer hen direct bij `clientcare@rainfocus.com` of bezoek het Centrum van de Hulp RainFocus [ ](https://help.rainfocus.com/hc/en-us).

## Gebruiksscenario&#39;s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de bestemming RainFocus zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die [!DNL Adobe Experience Platform] klanten kunnen oplossen door deze bestemming te gebruiken.

### Hoofdletters gebruiken #1 {#use-case-1}

Een groot technologiebedrijf voor bedrijven staat open voor registratie voor de komende wereldwijde expo en wil klantprofielen naar [!DNL RainFocus] duwen om het registratieproces te stroomlijnen.

### Hoofdletters gebruiken #2 {#use-case-2}

Een merk voor financiële diensten moet een reeks roadshows ontvangen die zich richten op nieuwe en bestaande klanten. Zij hebben een reeks publiekssegmenten met doelklanten in [!DNL Adobe Experience Platform]. Met de [!DNL RainFocus] bestemmingsconnector kunnen ze die profielen eenvoudig naar [!DNL RainFocus] verzenden voor activering.

## Vereisten {#prerequisites}

Voordat u het doel van [!DNL RainFocus] kunt gebruiken, moet u aan de volgende voorwaarden voldoen:

* Maak een [!DNL RainFocus] API-profiel met OAuth (Global).
   * Het **eindpunt van de Opslag van 0} Aanwezigen {moet worden toegelaten.**
   * A **identiteitskaart van de Cliënt** en **Geheime cliënt** zal moeten worden geproduceerd.

U moet ook een herkenningsteken van de gebeurteniscode RainFocus **hebben**, waarin u profielen zou willen die naar worden verzonden.

## Ondersteunde identiteiten {#supported-identities}

[!DNL RainFocus] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Zowel platte tekst als gehashte e-mailadressen van SHA256 worden ondersteund door [!DNL Adobe Experience Platform]. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [ ](../../../segmentation/home.md). |
| Alle andere doelgroepen | Nee | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [ diverse publieksoorsprong ](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere Experience Platform-toepassingen, zoals [!DNL Adobe Journey Optimizer] , </li><li> en meer. </li></ul> |

{style="table-layout:auto"}



Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
|--------------------|-----------|-------------|-----------|
| [ het publiek van Mensen ](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantenprofielen, die u toestaan om specifieke groepen mensen voor marketing campagnes te richten. | Frequente kopers, winkeliers |
| [ publiek van de Rekening ](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [ Het publiek van het Vooruitzicht ](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [ de uitvoer van de Dataset ](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het [!DNL Adobe Experience Platform] Data Lake. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}


## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment, samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm van de uitgezochte profielkenmerken van het [ werkschema van de bestemmingsactivering ](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

![ verstrekken authentificatiedetails voor de Schakelaar van de Bestemming RainFocus ](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-authentication.png)

* **[!UICONTROL Client ID]**: vul de [!DNL Client ID] in die wordt geleverd door RainFocus API Profile.
* **[!UICONTROL Client secret]**: vul de [!DNL Client Secret] in die wordt geleverd door RainFocus API Profile.
* **[!UICONTROL Environment]**: geef op met welke RainFocus-omgeving u verbinding maakt, bijvoorbeeld `dev` , `prod` .
* **[!UICONTROL Org ID]**: geef de unieke `orgid` voor uw instantie van RainFocus op.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![ verstrekt verbindingsdetails voor de Schakelaar van de Bestemming RainFocus ](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-configure-destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Event ID]**: De code-id van de [!DNL RainFocus] -gebeurtenis waarnaar u profielen wilt verzenden.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Lees [ actief publiek aan het stromen bestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

De volgende naamruimte(s) voor de doelidentiteit moeten worden toegewezen, afhankelijk van het gebruiksgeval:

* **E-mail** moet als doelgebied worden in kaart gebracht gebruikend **gebied van het Doel > Uitgezochte identiteitskaart namespace > e-mail**

![ hoe te profiel en identiteitsgebieden in kaart brengen ](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-mapping.png)

U wordt aangeraden extra profielvelden toe te wijzen, zodat het deelnemersprofiel in [!DNL RainFocus] volledig wordt ingevuld. De volgende doelvelden zijn beschikbaar via [!DNL RainFocus] :

| Doelveld | Beschrijving |
|------------|-------------|
| `address1` | De eerste regel van het adres |
| `address2` | De tweede regel van het adres van de straat (indien van toepassing) |
| `city` | De plaatsnaam |
| `companyname` | De naam van de onderneming |
| `countryid` | Een ISO 3166-1 alfa-2 landcode-id voor het land |
| `email` | Het e-mailadres |
| `firstname` | De voornaam van de persoon |
| `lastname` | Achternaam van de persoon |
| `jobtitle` | De functie van de persoon |
| `phone` | Het telefoonnummer |
| `state` | De FIPS-staats-alfacode voor de staat of provincie |
| `zip` | De postcode of postcode |

{style="table-layout:auto"}

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Nadat een set profielen naar [!DNL RainFocus] is verzonden, gebruikt u de aanmelding voor het API-profiel [!DNL RainFocus] om te controleren of de profielen zijn verwerkt.

![ Logboeken van de Mening in het API Profiel in RainFocus ](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-profile.png)

![ bevestigt dat de profielen met succes zijn opgenomen ](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-logging.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

* [ RainFocus Streaming Source Connector ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/analytics/rainfocus)
