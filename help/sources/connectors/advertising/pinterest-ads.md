---
keywords: Experience Platform;thuis;populaire onderwerpen;Pinterest-advertenties;
title: Overzicht van pinterest Adds-bronnen
description: Leer hoe u Pinterest Ads met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>De [!DNL Pinterest Ads] De bron is in bèta. Lees de [Overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een derde-advertentiesysteem. De steun voor reclamebureaus omvat [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) is een visuele zoekmachine om recepten, home décor, stijlinspiratie en andere ideeën op het web te vinden. Deze worden op kleine schaal weergegeven met behulp van afbeeldingen, geanimeerde GIFFEN en video&#39;s in pinboardindeling. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) staat u toe om uw zaken uit te breiden en 400 miljoen mensen te bereiken die [!DNL Pinterest].

Met [!DNL Pinterest Ads], kunt u gebruikers bereiken via gerichte advertenties om uw producten te ontdekken en te kopen. Vastzetten van [!DNL Pinterest Ads] gesponsord worden om extra blootstelling te ontvangen in relevante zoekresultaten. Gebruikers met een abonnement op [!DNL Pinterest Business] U kunt kiezen of u bestaande best presterende punten wilt promoten, een nieuw beeld of video wilt maken of zelfs een afbeelding wilt promoten die van een website is vastgezet. [!DNL Pinterest Ads] biedt verschillende advertentievormen aan om u te helpen uw specifieke campagnedoelstellingen te verwezenlijken.

## [!DNL Pinterest] API&#39;s {#pinterest-apis}

De [!DNL Pinterest Ads] bron gebruikt de [!DNL Pinterest] API&#39;s om uw [!DNL Pinterest Ads] gegevens, samen met alle prestaties en meetgegevens. De ondersteunde API-eindpunten zijn:

* [Campagneanalyses](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Analyse van advertentiegroep](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Advertentieanalyse](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Gebruik de [!DNL Pinterest Ads] bron om uw gegevens over te brengen van [!DNL Pinterest] naar Experience Platform, waar u vervolgens gegevensanalyses kunt uitvoeren. Gegevens worden geretourneerd vanaf de datum van inname gedurende een achterhaald bereik van 90 dagen. [!DNL Pinterest Ads] gebruikt dragertokens als authentificatiemechanisme om met het [!DNL Pinterest] API&#39;s.

## Vereisten {#prerequisites}

De eerste stap bij het maken van een [!DNL Pinterest Ads] De bronverbinding moet ervoor zorgen dat u een Pinterest-ontwikkelaarsaccount hebt. Als u er nog geen hebt, gaat u naar [aanmelden](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) pagina om uw account te registreren en te maken.

### Instellen [!DNL Pinterest] app en genereer toegangstoken {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Het wordt aanbevolen om de [!DNL Pinterest] APIs om uw toegangstoken te produceren omdat het produceren van uw toegangstoken in UI een beperkte toegang verleent. Via de interface hebt u alleen toegang tot het volgende bereik: `pins:read`, `boards:read` en `user_accounts:read`. Deze beperking is niet geschikt voor gebruik met de analytische eindpunten van de [!DNL Pinterest] API.

Om uw toegangstoken te produceren, lees [!DNL Pinterest] hulplijnen op [uw app instellen](https://developers.pinterest.com/docs/getting-started/set-up-app/) en [verifiëren met OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Vereiste referenties verzamelen {#gather-required-credentials}

Om verbinding te maken [!DNL Pinterest Ads] als u een Platform wilt maken, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| --- | --- |
| Toegangstoken | De [!DNL Pinterest Ads] toegangstoken voor uw gebruikersaccount. De gebruikersaccount van het token moet de eigenaar zijn van de opgegeven [!DNL Pinterest Ad] account of een van de noodzakelijke taken hebben die hun via Business Access worden toegekend: Beheerder, analist of Campagnebeheerder. Voor meer informatie over het toegangstoken, gelieve te verwijzen naar [[!DNL Pinterest] gids over het produceren van uw toegangstoken](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| ID advertentieaccount | Verwante [!DNL Pinterest Ads] Adaccount ID for your business unit. Voor informatie over het ophalen van je account-id. Ga naar [[!DNL Pinterest] gids voor het zoeken naar id&#39;s in Advertentiebeheer](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Campagne, advertentiegroep of advertentie-id | De `campaign`, `ad group`, of `ad` ID&#39;s die overeenkomen met je account-id. Navigeer naar de [!DNL Pinterest] pagina voor **Pinterest Business Hub** > **Overzicht van advertentieaccount** > **Campagnes** / **Toegevoegde groepen** / **Adds** en kopieer de vereiste id&#39;s die net onder elk van hun namen worden vermeld. |

>[!NOTE]
>
>De [!DNL Pinterest] API biedt afzonderlijke API&#39;s voor het ophalen van gegevens die aan elke id zijn gekoppeld. U hoeft dan ook alleen de bijbehorende id&#39;s door te geven voor het gewenste id-type.

## Guardrails {#guardrails}

In de volgende secties vindt u informatie over gegevenshulplijnen voor [!DNL Pinterest].

### [!DNL Pinterest] datumbereik {#pinterest-date-range}

De [!DNL Pinterest] API ondersteunt beide `start_date` en `end_date` parameter voor het ophalen van analysegegevens tussen een bepaald datumbereik.

* De `start_date` mag niet meer dan 90 dagen vóór de huidige datum liggen.
* De `end_date` mag niet meer dan 90 dagen na de `start_date`.

Wanneer het plannen van uw gegevensstroom, moet u één van de volgende frequentie en intervalmontages vormen:

| Frequentie | Interval |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Bijvoorbeeld, als de opname op 15 Maart, 2023 met een frequentie en interval wordt geplaatst die aan wordt gevormd `Day=1` of `Hour=24`en de [!DNL Pinterest] API haalt alleen gegevens op vanaf 15 december 2022, omdat de berekening 90 dagen achterhaald is.

### [!DNL Pinterest] tijdbereik {#pinterest-time-range}

De [!DNL Pinterest] API ondersteunt verschillende soorten tijdsgranulariteit voor het ophalen van gegevens:

| Tijdkorreligheid | Beschrijving |
| --- | --- |
| **TOTAAL** | De gegevensmetriek worden geaggregeerd over een opgegeven datumbereik. |
| **DAG** | De gegevens worden dagelijks uitgesplitst. |
| **UUR** | De gegevens worden per uur uitgesplitst. |
| **WEEKLY** | De gegevens worden wekelijks uitgesplitst. |
| **MAANDELIJK** | De gegevens worden maandelijks uitgesplitst. |

Voor Platform [!DNL Pinterest Ads] bron intern wordt gevormd aan `Day`, hetgeen betekent dat gegevens dagelijks worden geaggregeerd. Als u bijvoorbeeld `impressions recorded` als metrisch, aangezien granularity als a wordt gevormd `DAY`, dan krijgt u `xx` indrukken op `day 1`, `yy` indrukken op `day 2` enzovoort.

>[!IMPORTANT]
>
>Pinterest stelt een maximale snelheid van 1000 API-aanroepen per dag op voor de API om informatie te lezen van advertenties, ad-hocgroepen of advertentiecampagnes. Raadpleeg voor informatie over de tarieflimieten die van toepassing zijn op onderliggende API-aanroepen de [[!DNL Pinterest] documentatie over tarieflimieten](https://developers.pinterest.com/docs/reference/ratelimits/).

## Verbinden [!DNL Pinterest Ads] naar Platform {#connect-to-platform}

In de onderstaande documentatie vindt u informatie over het maken van een verbinding [!DNL Pinterest Ads] Platforms met behulp van API&#39;s of de gebruikersinterface:

### Verbinden [!DNL Pinterest Ads] naar Platform met API&#39;s {#connect-to-platform-using-api}

* [Een Pinterest-basisverbinding maken met de Flow Service API](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
* [Een gegevensstroom maken voor een advertentiebron met behulp van de Flow Service API](../../tutorials/api/collect/advertising.md)

### Verbinden [!DNL Pinterest Ads] naar Platform met behulp van de gebruikersinterface {#connect-to-platform-using-ui}

* [Een Pinterest-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Een gegevensstroom maken voor een verbinding met een advertentiebron in de gebruikersinterface](../../tutorials/ui/dataflow/advertising.md)
