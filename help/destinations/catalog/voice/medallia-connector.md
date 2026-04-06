---
title: verbinding met Medallia
description: Activeer profielen voor gerichte Media enquêtes en koppel inzameling terug om klantenbehoeften en verwachtingen beter te begrijpen.
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# verbinding met Medallia

## Overzicht {#overview}

Activeer profielen voor gerichte Media enquêtes en koppel inzameling terug om klantenbehoeften en verwachtingen beter te begrijpen.

>[!IMPORTANT]
>
>Deze bestemmingsschakelaar en documentatiepagina worden gecreeerd en door het team van Medallia gehandhaafd. Voor vragen of updateverzoeken kunt u rechtstreeks contact opnemen met de afdeling adobe-integrations@medallia.com.

## Gebruiksscenario&#39;s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de bestemming van Medallia zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die [!DNL Adobe Experience Platform] klanten door deze bestemming kunnen oplossen.

### Hoofdletters gebruiken #1 {#use-case-1}

Een B2B-merk wil zijn instapprogramma evalueren en stroomlijnen. Ze willen persoonlijke enquêtes in real-time verzenden naar klanten die net het instapproces hebben voltooid.

### Hoofdletters gebruiken #2 {#use-case-2}

Een retailer probeert beter inzicht te krijgen in de voorkeuren van klanten voor het uitvoeren van bestellingen. Ze willen een korte SMS-enquête met één vraag verzenden naar klanten die de afgelopen maand online en in-store aankopen hebben gedaan.

## Vereisten {#prerequisites}

Voor de verbinding met Medallia is de volgende informatie vereist:

* **OAuth Symbolische Eindpunt URL**
* **identiteitskaart van de Cliënt**
* **Geheim van de Cliënt**
* **URL van de Gateway van API Gateway**
* **de Naam van de Invoer API**

Werk samen met uw Media-leveringsteam om deze gegevens te verkrijgen.

## Ondersteunde identiteiten {#supported-identities}

Medallia ondersteunt de activering van de identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| email | E-mailadres | Selecteer de identiteit van het e-maildoel wanneer u enquêtes wilt verzenden naar een e-mailuitnodiging. Als een profiel is gekoppeld aan meerdere e-mailadressen, wordt de uitnodiging alleen voor de eerste e-mail geactiveerd. |
| telefoon | Telefoonnummers in E.164-indeling | Selecteer de identiteit van het telefoondoel wanneer u op SMS-Gebaseerde onderzoeken wilt verzenden. Het telefoonnummer moet de E.164-indeling hebben, die een plusteken (+), een internationale aanroepcode van het land, een lokale netcode en een telefoonnummer bevat. Bijvoorbeeld: (+)(landcode)(netnummer)(telefoonnummer). Wanneer een profiel met veelvoudige telefoonaantallen wordt geassocieerd, zal Medallia de uitnodiging aan het eerste slechts telefoonaantal teweegbrengen. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Alle andere doelgroepen | Nee | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [&#x200B; diverse publieksoorsprong &#x200B;](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere Experience Platform-toepassingen, zoals [!DNL Adobe Journey Optimizer] , </li><li> en meer. </li></ul> |

{style="table-layout:auto"}



Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
|--------------------|-----------|-------------|-----------|
| [&#x200B; het publiek van Mensen &#x200B;](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantenprofielen, die u toestaan om specifieke groepen mensen voor marketing campagnes te richten. | Frequente kopers, winkeliers |
| [&#x200B; publiek van de Rekening &#x200B;](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [&#x200B; Het publiek van het Vooruitzicht &#x200B;](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [&#x200B; de uitvoer van de Dataset &#x200B;](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het [!DNL Adobe Experience Platform] Data Lake. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}


## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle onlangs gekwalificeerde leden van een segment, samen met de gewenste schemagebieden (bijvoorbeeld: e-mailadres, telefoonaantal, achternaam), zoals gekozen in het uitgezochte scherm van profielattributen van het [&#x200B; werkschema van de bestemmingsactivering &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

* **[!UICONTROL OAuth Token Endpoint URL]**: De notatie https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL Client ID]**: Vraag het aan bij uw Media-leveringsteam.
* **[!UICONTROL Client Secret]**: Vraag het aan bij uw Media-leveringsteam.

![&#x200B; Beeld dat het authentificatiescherm voor deze bestemming toont.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL API Gateway URL]**: Vraag het aan bij uw Media-leveringsteam. De notatie https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Import API Name]**: Vraag het aan bij uw Media-leveringsteam. Naam van de Media Import API (ook wel Web Feed genoemd) die in deze verbinding moet worden gebruikt. U kunt verschillende soorten publiek activeren voor verschillende API&#39;s voor importeren om verschillende enquêteprogramma&#39;s te activeren.

![&#x200B; Beeld dat het scherm van bestemmingsdetails voor deze bestemming toont.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

De volgende naamruimte(s) voor de doelidentiteit moeten worden toegewezen, afhankelijk van het gebruiksgeval:

* Voor op e-mail-Gebaseerde onderzoeken, **e-mail** moet als doelgebied worden in kaart gebracht gebruikend **het gebied van het Doel** > **Uitgezochte identiteit namespace** > **e-mail**
* Voor op SMS-Gebaseerde onderzoeken, **telefoon** moet als doelgebied worden in kaart gebracht gebruikend **het gebied van het Doel** > **Uitgezochte identiteit namespace** > **telefoon**. Telefoonnummers moeten de E.164-indeling hebben, waaronder een plusteken (+), een internationale aanroepcode van het land, een lokale netcode en een telefoonnummer.

Het wordt sterk geadviseerd dat u ook extra attributen van de doeldouane in kaart brengt om gepersonaliseerde onderzoeken tot stand te brengen en extra informatie over de klant aan het onderzoeksverslag toe te voegen:

* De gepersonaliseerde onderzoeken richten typisch de klant door naam

   * Wijs de voornaam van de klant aan **gebied van het Doel** toe > **Uitgezochte douanekenmerken** > **naam van Attributen** > **firstname**
   * Wijs de achternaam van de klant aan **gebied van het Doel** toe > **Uitgezochte douanekenmerken** > **Naam van Attributen** > **lastname**

* Toewijzingen toevoegen voor andere aangepaste doelkenmerken naar wens

![&#x200B; Beeld dat een steekproefafbeelding voor identiteiten en attributen toont.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
>
> Het aandeel met uw Media leveringsteam de nauwkeurige **namen van Attributen** voor elk attribuut van de doeldouane u in kaart brengt gebruikend **gebied van het Doel** > **Uitgezochte douanekenmerken** > **naam van Attributen**. Mogelijk wilt u een schermafbeelding maken van de toewijzingspagina om deze rechtstreeks te delen.

## Geëxporteerde gegevens {#exported-data}

Nadat u de segmenten hebt geactiveerd naar de bestemming, stelt u het leveringsteam van Medallia op de hoogte, dat de geëxporteerde gegevens van [!DNL Adobe Experience Platform] naar Medallia zal kunnen valideren. Let op: enquêtes kunnen alleen in Medallia worden geactiveerd nadat de gegevens zijn geverifieerd; voorafgaand aan deze verificatie worden de gegevens naar Medallia geëxporteerd, maar worden geen enquêtes naar de klanten gestart.

Een steekproef JSON van de uitgevoerde gegevens wordt hieronder verstrekt, die de voorbeeldafbeelding van het scherm hierboven in de **attributen en identiteiten van de Kaart** sectie gebruikt:

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  "John" ,
        "lastname":  "Smith",
        "contactId": "jsmith120002",
    }
]
```

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).
