---
title: Verizon MediaYahoo DataX-verbinding
description: DataX is een geaggregeerde Verizon Media/Yahoo-infrastructuur die verschillende componenten host die Verizon Media/Yahoo in staat stellen gegevens met zijn externe partners op een veilige, geautomatiseerde en schaalbare manier uit te wisselen.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 1%

---

# [!DNL Verizon Media/Yahoo DataX]-verbinding

## Overzicht {#overview}

[!DNL DataX] is een geaggregeerde [!DNL Verizon Media/Yahoo] -infrastructuur die fungeert als host voor verschillende componenten, die [!DNL Verizon Media/Yahoo] in staat stellen gegevens op een veilige, geautomatiseerde en schaalbare manier uit te wisselen met externe partners.

>[!IMPORTANT]
>
>Deze doelconnector en documentatiepagina worden gemaakt en onderhouden door het [!DNL Verizon Media/Yahoo] -team van [!DNL DataX] . Voor om het even welke onderzoeken of updateverzoeken, contacteer hen direct in [ dataoperations@yahooinc.com](mailto:dataoperations@yahooinc.com)

## Vereisten {#prerequisites}

**identiteitskaart MDM**

Dit is een unieke id in [!DNL Yahoo DataX] en het is een verplicht veld voor het instellen van gegevensexport naar dit doel. Neem contact op met uw accountmanager van [!DNL Yahoo DataX] als u deze id niet kent.

**meta-gegevens van de Taxonomie**

De bron Taxonomy definieert een extensie via de structuur Metagegevens basis [!DNL DataX]

```json
{

  >>(Base DataX Metadata)<<

        "extensions": { "action":
        {string}, "incrementalData":
        {
                "taxonomyId": {string}
                },
                "links": [{
                "rel": "https://datax.yahooapis.com/rels/fullTaxonomy", "title": "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

Lees meer over [ Metagegevens van de Taxonomie ](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) in de [!DNL DataX] ontwikkelaarsdocumentatie.

## Snelheidslimieten en guardrails {#rate-limits-guardrails}

>[!IMPORTANT]
>
>Als u meer dan 100 soorten publiek activeert naar [!DNL Verizon Media/Yahoo DataX] , krijgt u mogelijk een foutmelding met betrekking tot de snelheid van het doel. Wanneer u het publiek activeert op deze bestemming, probeert u minder dan 100 soorten publiek te activeren in één activeringsgegevensstroom. Als u meer segmenten moet activeren, maakt u een nieuw doel op hetzelfde account.

[!DNL DataX] is tarief-beperkt per de quotagrenzen voor taxonomie en publieksposten die in de [ documentatie DataX ](https://developer.verizonmedia.com/datax/guide/rate-limits/) worden geschetst.


| Foutcode | Foutbericht | Beschrijving |
|---------|----------|---------|
| 429 Te veel verzoeken | Snelheidslimiet overschreden per uur **(Limiet: 100)** | Aantal toegestane verzoeken in een uur per leverancier. |

{style="table-layout:auto"}

## Ondersteunde identiteiten {#supported-identities}

[!DNL Verizon Media] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Zowel platte tekst als gehashte e-mailadressen van SHA256 worden ondersteund door [!DNL Adobe Experience Platform]. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| GAID | GOOGLE ADVERTISING ID | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

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
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (E-mail, GAID, IDFA) die worden gebruikt in de bestemming Verizon Media. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Gebruiksscenario’s {#use-cases}

[!DNL DataX] API&#39;s zijn beschikbaar voor adverteerders die een specifieke doelgroep willen activeren die e-mailadressen heeft uitgeschakeld in [!DNL Verizon Media] (VMG), zodat ze snel een nieuw publiek kunnen maken en de gewenste doelgroep kunnen duwen met de vrijwel realtime API van VMG.

## Verbinden met doel {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

![ Yahoo DataX bestemmingskaart in Experience Platform UI ](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [ vestiging ](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL MDM ID]**: dit is een unieke id in [!DNL Yahoo DataX] en het is een verplicht veld voor het instellen van gegevens die naar dit doel worden geëxporteerd. Neem contact op met uw accountmanager van [!DNL Yahoo DataX] als u deze id niet kent.  Met MDM IDs, kunnen de gegevens voor gebruik slechts met een bepaalde reeks exclusieve gebruikers (zoals eerste partijgegevens voor adverteerders) worden beperkt.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer profielen en publiek aan een bestemming ](../../ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan bestemmingen.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [ overzicht van het Beleid van Gegevens ](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Aanvullende bronnen {#additional-resources}

Voor meer informatie, lees de [!DNL Yahoo/Verizon Media] [ documentatie over  [!DNL DataX] ](https://developer.verizonmedia.com/datax/guide/).
