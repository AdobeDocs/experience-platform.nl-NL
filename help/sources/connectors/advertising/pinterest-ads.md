---
keywords: Experience Platform;thuis;populaire onderwerpen;Pinterest-advertenties;
title: Pinterest Ads Source - Overzicht
description: Leer hoe u Pinterest Ads met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>De bron [!DNL Pinterest Ads] is in bèta. Lees het [ Bronoverzicht ](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een derde-advertentiesysteem. Tot de ondersteuning voor advertentieproviders behoren [!DNL Pinterest Ads] .

[[!DNL Pinterest] ](https://www.pinterest.com) is een visuele ontdekkingsmotor voor het vinden van recepten, huisdécor, stijlinspiratie, en andere ideeën over het Web. Deze worden op kleine schaal weergegeven met behulp van afbeeldingen, geanimeerde GIFFEN en video&#39;s in pinboardindeling. [[!DNL Pinterest Ads] ](https://ads.pinterest.com/) staat u toe om uw zaken uit te breiden en 400 miljoen mensen te bereiken gebruikend [!DNL Pinterest].

Met [!DNL Pinterest Ads] kunt u gebruikers bereiken via gerichte advertenties om uw producten te ontdekken en te kopen. Spelden van [!DNL Pinterest Ads] worden gesponsord om extra blootstelling in relevante onderzoeksresultaten te ontvangen. Gebruikers met een abonnement op [!DNL Pinterest Business] kunnen bestaande best presterende punten promoten, een nieuw beeld of video maken of zelfs een afbeelding promoten die van een website is vastgezet. [!DNL Pinterest Ads] biedt verschillende advertentievormen aan om u te helpen uw specifieke campagnedoelstellingen te verwezenlijken.

## [!DNL Pinterest] API&#39;s {#pinterest-apis}

De [!DNL Pinterest Ads] -bron gebruikt de [!DNL Pinterest] API&#39;s om uw [!DNL Pinterest Ads] -gegevens op te halen, samen met alle prestaties en meetgegevens. De ondersteunde API-eindpunten zijn:

* [ Analytics van de Campagne ](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [ analyseert de Groep van de Advertentie ](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [ Adds analyseert ](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Gebruik de [!DNL Pinterest Ads] -bron om uw gegevens van [!DNL Pinterest] naar het Experience Platform te brengen, waar u vervolgens gegevensanalyses kunt uitvoeren. Gegevens worden geretourneerd vanaf de datum van inname gedurende een achterhaald bereik van 90 dagen. [!DNL Pinterest Ads] gebruikt tokens aan toonder als verificatiemechanisme om te communiceren met de API&#39;s van [!DNL Pinterest] .

## Vereisten {#prerequisites}

De eerste stap bij het maken van een [!DNL Pinterest Ads] -bronverbinding is ervoor te zorgen dat u een Pinterest-ontwikkelaarsaccount hebt. Als u niet reeds hebt, bezoek de [ login ](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) pagina om uw rekening te registreren en te creëren.

### Toepassing instellen [!DNL Pinterest] en toegangstoken genereren {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Het wordt aanbevolen de API&#39;s van [!DNL Pinterest] te gebruiken om uw toegangstoken te genereren, omdat het genereren van uw toegangstoken in de gebruikersinterface een beperkte toegang biedt. Via de interface hebt u alleen toegang tot het volgende bereik: `pins:read`, `boards:read` en `user_accounts:read` . Deze beperking is niet geschikt voor gebruik met de eindpunten van analysemogelijkheden van de API [!DNL Pinterest] .

Om uw toegangstoken te produceren, lees de [!DNL Pinterest] gidsen op [ vestiging uw app ](https://developers.pinterest.com/docs/getting-started/set-up-app/) en [ voor authentiek gebruikend OAuth 2.0 ](https://developers.pinterest.com/docs/getting-started/authentication/).

### Vereiste referenties verzamelen {#gather-required-credentials}

Als u [!DNL Pinterest Ads] wilt verbinden met Platform, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| --- | --- |
| Toegangstoken | Het toegangstoken [!DNL Pinterest Ads] voor uw gebruikersaccount. De gebruikersaccount van het token moet de eigenaar zijn van de opgegeven [!DNL Pinterest Ad] -account of een van de benodigde rollen hebben die aan hen zijn toegekend via Business Access: Admin, Analyst of Campagne Manager. Voor meer informatie over het toegangstoken, gelieve te verwijzen naar de [[!DNL Pinterest]  gids bij het produceren van uw toegangstoken ](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| ID advertentieaccount | De bijbehorende [!DNL Pinterest Ads] id van de advertentie voor uw bedrijfseenheid. Voor informatie over het ophalen van je account-id. Bezoek de [[!DNL Pinterest]  gids bij het vinden IDs in de Manager van Advertenties ](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Campagne, advertentiegroep of advertentie-id | De `campaign` -, `ad group` - of `ad` -id&#39;s die overeenkomen met de id van uw advertentieaccount. Om vereiste IDs te verkrijgen, navigeer aan de [!DNL Pinterest] pagina voor **Van Bedrijfs Pinterest Hub** > **Advertentieoverzicht van de Rekening** > **Campagnes** / **Advertentiegroepen** / **Advertenties** en kopieer de vereiste identiteitskaart wordt vermeld enkel onder elk van hun namen. |

>[!NOTE]
>
>De API van [!DNL Pinterest] biedt afzonderlijke API&#39;s voor het ophalen van de gegevens die aan elke id zijn gekoppeld. U hoeft dan ook alleen de bijbehorende id&#39;s door te geven voor het gewenste id-type.

## Guardrails {#guardrails}

In de volgende secties vindt u informatie over gegevenshulplijnen voor [!DNL Pinterest] .

### [!DNL Pinterest] datumbereik {#pinterest-date-range}

De API van [!DNL Pinterest] ondersteunt zowel een parameter `start_date` als een parameter `end_date` om analysegegevens tussen een bepaald datumbereik op te halen.

* De `start_date` mag niet langer zijn dan 90 dagen vóór de huidige datum.
* De `end_date` mag niet langer zijn dan 90 dagen na de `start_date` .

Wanneer het plannen van uw gegevensstroom, moet u één van de volgende frequentie en intervalmontages vormen:

| Frequentie | Interval |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Als inname bijvoorbeeld is ingesteld op 15 maart 2023 met een frequentie- en intervalinstelling geconfigureerd op `Day=1` of `Hour=24` , haalt de [!DNL Pinterest] -API alleen gegevens op vanaf 15 december 2022, omdat de berekening 90 dagen achterhaald is.

### [!DNL Pinterest] tijdbereik {#pinterest-time-range}

De API van [!DNL Pinterest] ondersteunt verschillende soorten tijdsgranulariteit voor het ophalen van gegevens:

| Tijdkorreligheid | Beschrijving |
| --- | --- |
| **TOTAL** | De gegevensmetriek worden geaggregeerd over een opgegeven datumbereik. |
| **DAG** | De gegevens worden dagelijks uitgesplitst. |
| **UUR** | De gegevens worden per uur uitgesplitst. |
| **WEEKLY** | De gegevens worden wekelijks uitgesplitst. |
| **MAANDELIJKS** | De gegevens worden maandelijks uitgesplitst. |

Voor Platform is de [!DNL Pinterest Ads] -bron intern geconfigureerd voor `Day` . Dit houdt in dat gegevens dagelijks worden geaggregeerd. Als u bijvoorbeeld `impressions recorded` als metrische waarde gebruikt en de granulariteit als `DAY` hebt geconfigureerd, krijgt u `xx` -afbeeldingen op `day 1` , `yy` -afbeeldingen op `day 2` enzovoort.

>[!IMPORTANT]
>
>Pinterest stelt een maximale snelheid van 1000 API-aanroepen per dag op voor de API om informatie te lezen van advertenties, ad-hocgroepen of advertentiecampagnes. Voor informatie over tariefgrenzen van toepassing op onderliggende API vraag, verwijs naar de [[!DNL Pinterest]  documentatie over tariefgrenzen ](https://developers.pinterest.com/docs/reference/ratelimits/).

## Verbinden [!DNL Pinterest Ads] met platform {#connect-to-platform}

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Pinterest Ads] en Platform via API&#39;s of de gebruikersinterface:

### Verbinding maken [!DNL Pinterest Ads] met platform met behulp van API&#39;s {#connect-to-platform-using-api}

* [Een Pinterest-basisverbinding maken met de Flow Service API](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
* [Een dataflow maken voor een advertentiebron met behulp van de Flow Service API](../../tutorials/api/collect/advertising.md)

### Verbinding maken [!DNL Pinterest Ads] met platform via de gebruikersinterface {#connect-to-platform-using-ui}

* [Een Pinterest-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Een gegevensstroom maken voor een verbinding met een advertentiebron in de gebruikersinterface](../../tutorials/ui/dataflow/advertising.md)
