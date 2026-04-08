---
title: Aangepast publiek opnieuw bewerken
description: Reddit Adds verbindt merken met mensen die actief hun passies en problemen in echt - tijd onderzoeken. Door intensief, door de gemeenschap gedreven gesprekken met flexibele advertentievormen en robuuste doelwitten te combineren, helpen Reddit Ads adverteerders betrokken doelgroepen bereiken, prestatiesresultaten drijven, en rechtstreeks van de gemeenschappen leren die cultuur online vormgeven. Deze handleiding is bedoeld voor adverteerders en medieteams die Adobe Experience Platform gebruiken om een publiek naar Reddit Ads te sturen. Hierin wordt beschreven wat u nodig hebt om uw accounts aan te sluiten, identiteiten toe te wijzen en het publiek te activeren.
last-substantial-update: 2026-03-31T00:00:00Z
exl-id: bcce02bd-d508-47a0-8f5c-bf162db1859d
badgeBeta: label="Beta" type="Informative"
source-git-commit: 28bbad7ccbec0b669082658b912d0b52e0374667
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 1%

---

# [!DNL Reddit Custom Audience]-verbinding {#reddit-custom-audience-connection}

## Overzicht {#overview}

[!DNL Reddit Ads] verbindt merken met mensen die actief hun passies en problemen in real time onderzoeken. Door intensief, door de gemeenschap aangestuurde gesprekken met flexibele advertentievormen en robuuste doelwitten te combineren, bereiken [!DNL Reddit Ads] Help-adverteerders betrokken doelgroepen, stimuleren ze prestatieresultaten en leren ze rechtstreeks van de gemeenschappen die online cultuur vormgeven.

Deze handleiding is bedoeld voor adverteerders en medieteams die [!DNL Adobe Experience Platform] gebruiken om soorten publiek naar [!DNL Reddit Ads] te sturen. Hierin wordt beschreven wat u nodig hebt om uw accounts aan te sluiten, identiteiten toe te wijzen en het publiek te activeren.

>[!IMPORTANT]
>
>Deze doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van [!DNL Reddit] . Voor vragen of updateverzoeken kunt u rechtstreeks contact opnemen via <adsapi-partner-support@reddit.com> .

## Gebruiksscenario&#39;s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Reddit Custom Audience] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die [!DNL Adobe Experience Platform] klanten kunnen oplossen door deze bestemming te gebruiken.

### Bestaande klanten met gepersonaliseerde aanbiedingen opnieuw samenbrengen {#use-case-1}

Een online retailer wil bestaande klanten bereiken via sociale platforms en hun persoonlijke aanbiedingen laten zien op basis van hun eerdere bestellingen. De online retailer kan e-mailadressen en apparaat-id&#39;s (IDFA en GAID) van zijn eigen CRM tot [!DNL Adobe Experience Platform] opnemen, een publiek opbouwen op basis van zijn eigen offlinegegevens en deze soorten publiek naar [!DNL Reddit Ads] sturen, waarbij de advertentie-uitgaven worden geoptimaliseerd.

## Vereisten {#prerequisites}

Alvorens deze bestemming te vormen, zorg ervoor u aan de volgende eerste vereisten voldoet:

* Een [!DNL Reddit Ads] -account die aangepaste soorten publiek en lijsten van klanten mag gebruiken.
* Machtiging voor verbinding. Dit moet een gebruiker zijn die zich kan aanmelden bij [!DNL Reddit] en toegang voor [!DNL Experience Platform] kan goedkeuren om het publiek namens de advertentieaccount te beheren.
* Uw [!DNL Reddit] id van de Advertentierekening: het herkenningsteken voor de advertentierekening waar het publiek wordt gecreeerd. U kunt uw identiteitskaart van de advertentierekening in [ Rekeningen ](https://ads.reddit.com/accounts) vinden. Bijvoorbeeld: `a2_1b2c34d` .

## Ondersteunde identiteiten {#supported-identities}

[!DNL Reddit Custom Audience] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
| --- | --- | --- |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Zowel platte tekst als gehashte e-mailadressen van SHA256 worden ondersteund door [!DNL Adobe Experience Platform]. Wanneer het bronveld niet-gehashte kenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in, zodat [!DNL Platform] de gegevens bij activering automatisch hasht. |
| magistraat | Google Advertising ID or Apple ID for Advertisers, both hashed with the SHA256 algorithm | Kaart of GAID of IDFA op **maid**. Wanneer het bronveld niet-gehashte kenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in, zodat [!DNL Platform] de gegevens bij activering automatisch hasht. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
| --- | --- | --- |
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de [!DNL Experience Platform] [ Dienst van de Segmentatie ](../../../segmentation/home.md). |
| Alle andere doelgroepen | Ja | Deze categorie omvat alle publieksoorsprong buiten publiek dat door de Dienst van de Segmentatie wordt geproduceerd. Lees over de [ diverse publieksoorsprong ](/help/segmentation/ui/audience-portal.md#customize). |

{style="table-layout:auto"}

Ondersteund publiek op gegevenstype:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
| --- | --- | --- | --- |
| [ het publiek van Mensen ](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantenprofielen, die u toestaan om specifieke groepen mensen voor marketing campagnes te richten. | Frequente kopers, winkeliers |
| [ publiek van de Rekening ](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [ Het publiek van het Vooruitzicht ](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [ de uitvoer van de Dataset ](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het [!DNL Adobe Experience Platform] Data Lake. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
| --- | --- | --- |
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de [!DNL Reddit Custom Audience] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]** .

![ het Reddit het bestemmingsauthentificatiescherm van het publiek van de Douane die gebieden tonen die worden vereist om te verbinden.](../../assets/catalog/advertising/redditcustomaudience/configure_new_destination_fields.png)

U wordt omgeleid om u aan te melden met [!DNL Reddit]. Nadat u de aangevraagde machtigingen hebt gecontroleerd, selecteert u **[!UICONTROL Allow]** , zodat [!DNL Experience Platform] een publiek kan maken en het lidmaatschap namens uw advertentieaccount kan bijwerken.

![ reddit het toestemmingsscherm van OAuth.](../../assets/catalog/advertising/redditcustomaudience/reddit_oauth.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![ het Reddit de bestemmingsdetailscherm van het Audience van de Douane.](../../assets/catalog/advertising/redditcustomaudience/reddit_account_details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel herkent.
* **[!UICONTROL Description]**: Een beschrijving waarmee u dit doel kunt identificeren.
* **[!UICONTROL Ad Account ID]**: Uw [!DNL Reddit] id van het Advertentieaccount.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

De volgende naamruimten voor de doelidentiteit moeten worden toegewezen, afhankelijk van het gebruiksgeval:

| Source-veld | Doelveld | Notities |
| --- | --- | --- |
| E-mail (normale tekst of hashed) | email_lc_sha256 | Het bronveld kan worden gehasht of losgekoppeld. [!DNL Reddit] accepteert alleen gehashte waarden. Schakel **[!UICONTROL Apply transformation]** in zodat [!DNL Experience Platform] de e-mail hasht voordat deze wordt verzonden. |
| MAID (normale tekst of hashed) | magistraat | Het bronveld kan worden gehasht of losgekoppeld. [!DNL Reddit] accepteert alleen gehashte waarden. Schakel **[!UICONTROL Apply transformation]** in zodat [!DNL Experience Platform] de waarde hasht voordat deze wordt verzonden. |

U moet ten minste een van de identiteiten toewijzen.

![ het scherm van de identiteitstoewijzing die bron en doelgebieden tonen voor Reddit de Audience van de Douane worden gevormd.](../../assets/catalog/advertising/redditcustomaudience/mapping.png)

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Nadat u het publiek hebt geactiveerd, kunt u deze weergeven in uw account van [!DNL Reddit] Advertentiebeheer.

Soorten publiek die nieuw zijn gemaakt in [!DNL Reddit] , worden in behandeling weergegeven. Nadat de gegevensstroom is uitgevoerd en de profielen zijn geëxporteerd, stemt [!DNL Reddit] overeen met de profielen ten opzichte van [!DNL Reddit] -gebruikers. Nadat de gegevens zijn verwerkt, verandert de status van het publiek in **[!UICONTROL Valid]** . De grootte van het publiek moet [ 1.000 gebruikers of meer ](https://ads-api.reddit.com/docs/v3/manage-customer-lists) bereiken om als geldig te worden beschouwd. Soorten publiek dat niet de vereiste grootte heeft, worden weergegeven als **[!UICONTROL Invalid]** .

![ de Reddit Manager van Advertenties die een uitgevoerd publiek en zijn status tonen.](../../assets/catalog/advertising/redditcustomaudience/see_audience_in_reddit.png)

Hieronder ziet u een voorbeeld van de lading die naar [!DNL Reddit] wordt verzonden:

```json
{
  "data": {
    "action_type": "ADD",
    "column_order": [
      "EMAIL_SHA256",
      "MAID_SHA256"
    ],
    "user_data": [
      [
        "d7ef2e7b2a3663c25284a3d6d13b1ca727fc8c659474b81afe0cec997a4737d2",
        "510870d7b3e47a28a2b2f3aef27a4c81aab0b2eefda27dea50bc4c991d9e5435"
      ]
    ]
  }
}
```

Zie [ API documentatie ](https://ads-api.reddit.com/docs/v3/operations/Update%20Custom%20Audience%20Users) voor extra details opnieuw uitgeven.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Zie [ API documentatie ](https://ads-api.reddit.com/docs/v3/operations/Update%20Custom%20Audience%20Users) voor details over hoe de functies van het douanepuntpunt van het publiek opnieuw uitgeven.
