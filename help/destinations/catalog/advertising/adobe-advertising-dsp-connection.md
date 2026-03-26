---
title: Adobe Advertising DSP-verbinding
description: Leer hoe u geverifieerde en niet-geverifieerde soorten publiek van de eerste partij kunt delen met Adobe Advertising Demand-Side Platform (DSP) door meerdere typen identiteiten te gebruiken.
feature: Destinations
exl-id: 0ff80d38-993f-4609-bf2a-01a3e6cfe10b
source-git-commit: 60a8296d20a254f6c431c6986f8b2704dced3516
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 0%

---

# Adobe Advertising DSP-verbinding

## Overzicht {#overview}

Met de bestemming Adobe Advertising Demand-Side Platform (DSP) kunnen gebruikers zowel geverifieerde als niet-geverifieerde eerderechten delen met een DSP-account of specifieke adverteerder binnen een account.

Deze bestemming staat klanten toe om het eerste-partijpubliek met om het even welk of elk van deze IDs te delen:

* Verborgen e-mailadres, dat wordt omgezet in een [!DNL LiveRamp RampID] of [!DNL Unified ID 2.0] (UID2.0) voor activering in DSP

* Experience Cloud ID (ECID) en Adobe Advertising cookies van derden

* Mobiele advertentie-id&#39;s (MAID&#39;s):

   * [!DNL Google] Advertising-id&#39;s (GAID&#39;s) voor [!DNL Android] -apparaten

   * Id&#39;s voor adverteerders (IDFA&#39;s) voor [!DNL Apple iOS] -apparaten

Deze verbinding vervangt de [&#x200B; Verouderde verbinding van Adobe Advertising Cloud DSP van Adobe &#x200B;](adobe-advertising-cloud-dsp-connection-legacy.md), die slechts gehakt e-mailadressen steunt.

>[!IMPORTANT]
>
>Deze pagina is gemaakt door het team van Adobe Advertising [!DNL DSP] . Voor vragen of updateverzoeken kunt u rechtstreeks via `adcloud_support@adobe.com` contact opnemen met de ondersteuning van Advertising.

## Gebruiksscenario&#39;s {#use-cases}

Met deze bestemming kunnen adverteerders hun publiek in verschillende browsers bereiken met cookies en zonder cookies.

Adverteerders kunnen ervoor kiezen om segmenten te delen met geverifieerde id&#39;s van de eerste partij (zoals [!DNL RampID] en [!DNL UID2.0] ) of als niet-geverifieerde id&#39;s (zoals cookies en MAID&#39;s).

## Vereisten {#prerequisites}

* Voor [!DNL RampID activation] geldt dat [!DNL DSP] instellingen op accountniveau en op campagneniveau het delen van gebruikers met [!DNL LiveRamp RampID] mogelijk maken. Hiermee worden klantgegevens naar [!DNL RampIDs] vertaald om doelgerichte segmenten te maken. Uw Adobe-accountteam zal deze configuratie uitvoeren. [!DNL RampID] is beschikbaar via een partnerschap tussen [!DNL DSP] en [!DNL LiveRamp] en u hebt geen eigen [!DNL LiveRamp] -lidmaatschap nodig om dit te gebruiken.

* Id&#39;s publiek:

   * Voor [!DNL RampID] en [!DNL UID2.0] moeten profielen hashed-e-mailadressen bevatten.

   * Voor cookies stelt u een cookiesynchronisatieproces in met [!DNL Web SDK] gegevensstreams of de [!DNL Experience Cloud ID Service] . Zie [&#x200B; de synchronisatie van identiteitskaart van de Opstelling om koekjes &#x200B;](#cookie-sync) hieronder te delen.

   * Voor profielen met MAID&#39;s:

      * Neem voor elke GAID de waarde `GAID` op in een kolom IdentityMap.

      * Neem voor elke IDFA de waarde `IDFA` op in een kolom IdentityMap.

* De Experience Cloud-organisatie-id voor de Experience Platform-account. Je kunt je gebruikersnaam vinden op je Adobe [!DNL Real-Time Customer Data Platform] ([!DNL Real-Time CDP] )-gebruikersprofielpagina.

* A [[!DNL Real-Time CDP]  bron in DSP &#x200B;](https://experienceleague.adobe.com/nl/docs/advertising/dsp/audiences/sources/source-manage) om publiek voor campagneactivering te ontvangen. Uw Adobe-accountteam maakt de bron met uw Experience Cloud-organisatie-id.

* De bronsleutel voor de [!DNL DSP] rekening of adverteerder, die wordt geproduceerd wanneer a [[!DNL Real-Time CDP]  bron in  [!DNL DSP] &#x200B;](https://experienceleague.adobe.com/nl/docs/advertising/dsp/audiences/sources/source-manage) wordt gecreeerd. Uw accountteam van [!DNL DSP] deelt deze sleutel met u. U gebruikt deze in Experience Platform om een doelverbinding met de Advertising DSP-bestemming te maken, zoals hieronder wordt uitgelegd.

### Synchronisatie van id&#39;s instellen om cookies te delen {#cookie-sync}

ID-synchronisatie is een eerste vereiste voor het delen van cookies van derden. Stel een cookiesynchronisatieproces in met [!DNL Web SDK] gegevensstreams of de [!DNL Experience Cloud ID Service] . Voor meer context over identiteit behandeling voor derdekoekjes, zie [&#x200B; bestemmingen Advertising die zich op de integratie van derdekoekjes baseren &#x200B;](/help/destinations/how-destinations-work/identity-handling.md#third-party-cookie-destinations).

**Het synchroniseren van id&#39;s van derden inschakelen met[!DNL Web SDK]**

Als u [!DNL Experience Platform Web SDK] gebruikt, moet u synchronisatie van id&#39;s van derden voor uw gegevensstroom inschakelen door de optie [!UICONTROL Third Party ID Sync] in de geavanceerde instellingen te configureren. Voor instructies, zie [&#x200B; geavanceerde opties &#x200B;](/help/datastreams/configure.md#advanced-options) in de documentatie van gegevensstromen vormen.

**laat derde identiteitskaart toe synchroniserend met[!DNL Experience Cloud ID Service]**

Als u [!DNL Experience Platform] markeringen met [!DNL Experience Cloud ID Service] gebruikt, vorm de synchronisatie van derdeidentiteitskaart gebruikend de [&#x200B; uitbreiding van de Dienst van identiteitskaart van Experience Cloud &#x200B;](/help/tags/extensions/client/id-service/overview.md). Hierdoor is de overeenkomende Adobe Advertising-cookie voor de opgegeven ECID beschikbaar wanneer u het publiek activeert vanuit [!DNL Real-Time CDP] .

## Ondersteunde identiteiten {#supported-identities}

De Adobe Advertising DSP-bestemming ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
| --------------- | ----------- | -------------- |
| `email_lc_sha256` | E-mailadressen die met het algoritme SHA256 worden gehasht | Experience Platform ondersteunt zowel normale tekst- als SHA256-hashed-e-mailadressen. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in zodat Experience Platform de gegevens automatisch hasht bij activering. |
| `ECID` | Eerste cookie voor Experience Cloud | Vereist voor het maken van op cookies gebaseerde segmenten. |
| `adcloud` | Cookie van derden voor Adobe Advertising | Vereist voor het maken van op cookies gebaseerde segmenten. |
| `GAID` | [!DNL Android] apparaat-id | Vereist voor doelapparaten van [!DNL Android] . |
| `IDFA` | [!DNL iOS] apparaat-id | Vereist voor doelapparaten van [!DNL iOS] . |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Alle andere doelgroepen | Ja | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [&#x200B; diverse publieksoorsprong &#x200B;](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere Experience Platform-toepassingen, zoals [!DNL Adobe Journey Optimizer] , </li><li> en meer. </li></ul> |

{style="table-layout:auto"}

Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
| -------------------- | --------- | ----------- | --------- |
| [&#x200B; het publiek van Mensen &#x200B;](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantenprofielen, die u toestaan om specifieke groepen mensen voor marketing campagnes te richten. | Frequente kopers, winkeliers |
| [&#x200B; publiek van de Rekening &#x200B;](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [&#x200B; Het publiek van het Vooruitzicht &#x200B;](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [&#x200B; de uitvoer van de Dataset &#x200B;](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het [!DNL Adobe Experience Platform] Data Lake. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de volgende tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
| ---- | ---- | ----- |
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de gekozen id&#39;s. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) voor Experience Platform nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met de bestemming te verbinden, volg de instructies om [&#x200B; een bestemmingsverbinding &#x200B;](/help/destinations/ui/connect-destination.md) tot stand te brengen gebruikend het gebruikersinterface van Experience Platform. Vul in de workflow voor doelconfiguratie de velden in die in de onderstaande subsecties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u verbinding wilt maken met het doel, geeft u de volgende parameter op in de sectie [!UICONTROL Connection type] en selecteert u **[!UICONTROL Connect to destination]** :

* **[!UICONTROL Account or Advertiser Key]**: Dit [!UICONTROL Source Key] wordt geproduceerd wanneer a [[!DNL Real-Time CDP]  bron in het gebruikersinterface van DSP &#x200B;](https://experienceleague.adobe.com/nl/docs/advertising/dsp/audiences/sources/source-manage) wordt gecreeerd. Uw Adobe-accountteam deelt deze sleutel met u nadat de bron is gemaakt.

![&#x200B; Schermafbeelding van het type van Verbinding die het Sleutelgebied van de Rekening of Advertiser toont.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

![&#x200B; Schermafbeelding van de gebieden van het bestemmingsdetail die de input van de Naam en van de Beschrijving tonen.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_adcloud_dsp"
>title="Vooraf geconfigureerde toewijzingssets"
>abstract="Deze twee sets met toewijzingen zijn vooraf geconfigureerd: ECID en [!DNL adcloud] cookie. Wanneer u gegevens naar Adobe Advertising DSP activeert, moeten de profielen die voor het geactiveerde publiek zijn gekwalificeerd, ten minste een ECID-identiteit hebben die aan het profiel is gekoppeld, om naar de bestemming te kunnen worden geëxporteerd."
>additional-url="https://experienceleague.adobe.com/nl/docs/experience-platform/destinations/catalog/advertising/adobe-advertising-dsp-connection#preconfigured-mappings" text="Lees meer over de vooraf geconfigureerde toewijzingen"

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om identiteiten uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

De identiteitstoewijzingen voor deze bestemming zijn gedeeltelijk preconfigured. Controleer de vooraf geconfigureerde toewijzingen hieronder en voeg desgewenst id&#39;s toe die u wilt opnemen.

### Vooraf geconfigureerde toewijzingen {#preconfigured-mappings}

De volgende identiteitstoewijzingen zijn **vooraf gevormd en automatisch bevolkt** tijdens het werkschema van de publiekactivering:

* **`ECID`** (Experience Cloud-id)
* **`adcloud`** (Adobe Advertising cookie van derden)

![&#x200B; Schermafbeelding van de sectie van de identiteitstoewijzing die koekjesherkenningstekens, Onderbroken E-mail, IDFA, en GAID opties tonen.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/identity-mapping.png)

Deze toewijzingen worden grijs en alleen-lezen weergegeven. U hoeft niets in deze stap te configureren. U kunt optioneel de volgende toewijzingen toevoegen:

* **`email_lc_sha256`** (Onderbroken e-mail)
* **IDFA** ([!DNL Apple iOS] apparatenidentiteitskaart)
* **GAID** ([!DNL Android] apparatenidentiteitskaart)

Selecteer **[!UICONTROL Next]** om door te gaan.

>[!IMPORTANT]
>
>**ECID wordt vereist voor op koekjes-gebaseerde uitvoer om te slagen.** Profielen zonder ECID worden niet opgenomen in op cookies gebaseerde segmenten. Voor geverifieerde publiekssegmenten die [!DNL RampID] of [!DNL UID2.0] gebruiken, moeten profielen hashed-e-mailadressen bevatten.

Voor instructies, zie [&#x200B; attributen en identiteiten van de Kaart &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

## Gegevens exporteren valideren {#exported-data}

Controleer het volgende om te controleren of de publieksgegevens zijn gedeeld met Adobe Advertising:

* De gegevensstroom in uw [!DNL Real-Time CDP] -doel is voltooid.

* In DSP is het publiek beschikbaar wanneer u een publiek maakt of bewerkt vanuit **[!UICONTROL Audiences]** > **[!UICONTROL All Audiences]** of vanuit de sectie **[!UICONTROL Audience Targeting]** met plaatsingsinstellingen. Het publiek moet zichtbaar zijn op het tabblad [!UICONTROL Adobe Segments] onder de map [!UICONTROL Real-Time CDP] .

![&#x200B; Schermafbeelding van de interface van het Soorten publiek van DSP die een [!DNL Real-Time CDP] omslag met ingevoerde publiekssegmenten toont die onder het lusje van de Segmenten van Adobe worden vermeld.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).
