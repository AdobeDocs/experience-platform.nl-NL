---
title: Streaming op Source
description: Leer hoe u een bronverbinding en gegevensstroom kunt maken om streaminggegevens van uw Shopify-instantie in te voeren in Adobe Experience Platform
badge: Beta
last-substantial-update: 2023-04-26T00:00:00Z
exl-id: ae991913-68b5-4bbb-b8a5-e566d67a4c1a
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>De bron [!DNL Shopify Streaming] is in bèta. Gelieve te lezen het [ overzicht van bronnen ](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Adobe Experience Platform biedt ondersteuning voor het opnemen van gegevens uit streaming toepassingen. Tot de ondersteuning voor streamingproviders behoren [!DNL Shopify] .

## Vereisten {#prerequisites}

In de volgende sectie worden de vereiste stappen beschreven die moeten worden uitgevoerd voordat de [!DNL Shopify Streaming] -bron wordt gebruikt.

U moet een geldige [!DNL Shopify] partneraccount hebben om verbinding te kunnen maken met de [!DNL Shopify] API&#39;s. Als u nog geen partnerrekening hebt, gelieve te registreren gebruikend het [[!DNL Shopify]  partners dashboard ](https://www.shopify.com/partners).

### Uw toepassing maken

Met een geldig [!DNL Shopify] partneraccount kunt u nu doorgaan en uw app maken via het partnerdashboard. Voor uitvoerige stappen op hoe te om uw app in [!DNL Shopify] tot stand te brengen, lees de [[!DNL Shopify]  gids op begonnen worden ](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

Zodra uw app wordt gecreeerd, wint uw **cliëntidentiteitskaart** en **cliëntgeheim** van het **cliëntgeloofsbrieven** lusje van het [!DNL Shopify] partnerdashboard terug. De cliënt ID en het cliëntgeheim zullen in de volgende stappen worden gebruikt om uw vergunningscode en toegangstoken terug te winnen.

### De verificatiecode ophalen

Vervolgens haalt u uw machtigingscode op door de `myshopify.com` URL van uw domein in te voeren in uw browser, samen met querytekenreeksen die uw API-sleutel, bereik en de omleidings-URI definiëren.

De notatie voor deze URL is als volgt:

**API formaat**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| Parameter | Beschrijving |
| --- | --- |
| `shop` | De URL van het subdomein `myshopify.com` . |
| `api_key` | Uw [!DNL Shopify] client-id. U kunt uw cliëntidentiteitskaart van de **cliëntgeloofsbrieven** lusje van het [!DNL Shopify] partnerdashboard terugwinnen. |
| `scopes` | Het type toegang dat u wilt definiëren. U kunt bereik bijvoorbeeld instellen als `scope=write_orders,read_customers` om machtigingen toe te staan om bestellingen te wijzigen en klanten te lezen. |
| `redirect_uri` | De URL voor het script dat het toegangstoken genereert. |

**Verzoek**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**Reactie**

Een succesvolle reactie keert uw omleidings URL, met inbegrip van de vergunningscode terug die wordt vereist om uw toegangstoken te produceren.

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### Uw toegangstoken ophalen

Nu u uw cliënt identiteitskaart, cliëntgeheim, en vergunningscode hebt, kunt u uw toegangstoken terugwinnen. Als u uw toegangstoken wilt ophalen, vraagt u een POST aan naar de URL van uw domein `myshopify.com` terwijl u deze URL toevoegt met het [!DNL Shopify's] API-eindpunt: `/admin/oauth/access_token` .

**API formaat**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**Verzoek**

Met de volgende aanvraag wordt een toegangstoken voor de instantie [!DNL Shopify] gegenereerd.

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/oauth/access_token' \
  -H 'developer-token: {DEVELOPER_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'Cookie: _master_udr=xxx; request_method=POST'
  -d '{
    "client_id": "l6fiviermmzpram5i1spfub99shms3j9",
    "client_secret": "dajn3caxz9s7ti624ncyv_m4f60jnwi3ii3y3k",
    "code": "k6j2palgrbljja228ou8c20fmn7w41gz"
}'
```

**Reactie**

Een succesvolle reactie keert uw toegangstoken en toestemmingswerkingsgebied terug.

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## Webhaak maken voor streaming [!DNL Shopify] -gegevens {#webhook}

Met webhaken kunnen toepassingen gesynchroniseerd blijven met uw [!DNL Shopify] -gegevens of een actie uitvoeren nadat een bepaalde gebeurtenis in een winkel heeft plaatsgevonden. Voor het stromen [!DNL Shopify] gegevens aan Experience Platform, kunnen de webhooks worden gebruikt om het eindpunt van http en de onderwerpen voor abonnement te bepalen.

**Verzoek**

Met de volgende aanvraag wordt een webhaak voor uw [!DNL Shopify Streaming] -gegevens gemaakt.

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/api/2022-07/webhooks.json' \
  -H 'X-Shopify-Access-Token: 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' \
  -H 'Content-Type: application/json' \; request_method=POST' \
  -d '{
  "webhook": {
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "format": "json"
  }
}'
```

| Parameter | Beschrijving |
| --- | --- | 
| `webhook.address` | Het eindpunt van http waar het stromen berichten worden verzonden. |
| `webhook.topic` | Het onderwerp van uw webshabonnement. Voor meer informatie, leest de [[!DNL Shopify]  gids van de webshgebeurtenis onderwerpen ](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | De indeling van de gegevens. |

**Reactie**

Een geslaagde reactie retourneert informatie over de webhaak, inclusief de bijbehorende `id` , het adres en andere metagegevens.

```json
{
  "webhook": {
    "id": 1091138715786,
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "created_at": "2022-07-20T07:15:23-04:00",
    "updated_at": "2022-07-20T07:15:23-04:00",
    "format": "json",
    "fields": [],
    "metafield_namespaces": [],
    "api_version": "2021-10",
    "private_metafield_namespaces": []
  }
}
```

### Beperkingen {#limitations}

Hieronder volgt een lijst met bekende beperkingen die u kunt tegenkomen bij het gebruik van websites met de [!DNL Shopify Streaming] -bron.

* Het is niet gewaarborgd dat u de orde van levering van verschillende onderwerpen voor het zelfde middel kunt schikken. Het is bijvoorbeeld mogelijk dat een `products/update` webhaak wordt geleverd vóór een `products/create` -webhaak.
* U kunt uw webhaak instellen om webhaakgebeurtenissen minstens één keer aan een eindpunt te leveren. Dit betekent dat een eindpunt dezelfde gebeurtenis meer dan één keer kan ontvangen. U kunt scannen op dubbele webhaakgebeurtenissen door de header van `X-Shopify-Webhook-Id` te vergelijken met vorige gebeurtenissen.
* [!DNL Shopify] behandelt de statusreacties van HTTP 2xx als geslaagde meldingen. Eventuele andere reacties op de statuscode worden beschouwd als mislukkingen. [!DNL Shopify] biedt een mechanisme voor het opnieuw proberen van mislukte websitemeldingen. Als er **geen reactie na het wachten op vijf seconden** is, [!DNL Shopify] probeert de verbinding **19 keer** over de cursus van volgende **48 uren** opnieuw. Als er nog steeds geen reacties zijn tegen het einde van de hertestperiode, verwijdert [!DNL Shopify] de webhaak.

## Volgende stappen

De volgende zelfstudies bieden stappen voor het aansluiten van de [!DNL Shopify Streaming] -bron op een Experience Platform met behulp van de API en de UI:

* [Een Shopify Streaming-bronverbinding en -gegevensstroom maken met de Flow Service API](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [Een Shopify-bronverbinding en -gegevensstroom maken in de gebruikersinterface](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
