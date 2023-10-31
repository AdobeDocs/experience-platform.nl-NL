---
title: Streaming bron optimaliseren
description: Leer hoe u een bronverbinding en gegevensstroom kunt maken om streaminggegevens van uw Shopify-instantie in te voeren in Adobe Experience Platform
badge: Beta
last-substantial-update: 2023-04-26T00:00:00Z
exl-id: ae991913-68b5-4bbb-b8a5-e566d67a4c1a
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 0%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>De [!DNL Shopify Streaming] De bron is in bèta. Lees de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Adobe Experience Platform biedt ondersteuning voor het opnemen van gegevens uit streaming toepassingen. Ondersteuning voor streaming providers omvat [!DNL Shopify].

## Vereisten {#prerequisites}

In de volgende sectie worden de vereiste stappen beschreven die moeten worden uitgevoerd voordat u de opdracht [!DNL Shopify Streaming] bron.

U moet een geldige [!DNL Shopify] partnerrekening om met te verbinden [!DNL Shopify] API&#39;s. Als u nog geen partneraccount hebt, kunt u zich registreren via de [[!DNL Shopify] partnerdashboard](https://www.shopify.com/partners).

### Uw toepassing maken

Met een geldige [!DNL Shopify] partneraccount, kunt u nu doorgaan en uw app maken via het partnerdashboard. Voor uitgebreide stappen over het maken van uw app in [!DNL Shopify], lees de [[!DNL Shopify] gids over aan de slag gaan](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

Wanneer uw app is gemaakt, haalt u uw **client-id** en **clientgeheim** van de **clientgegevens** tabblad van het [!DNL Shopify] het dashboard van partners. De cliënt ID en het cliëntgeheim zullen in de volgende stappen worden gebruikt om uw vergunningscode en toegangstoken terug te winnen.

### De verificatiecode ophalen

Haal vervolgens de verificatiecode op door de domeingegevens in te voeren `myshopify.com` URL in uw browser, samen met vraagkoorden die uw API sleutel, werkingsgebied, en redirect URI bepalen.

De notatie voor deze URL is als volgt:

**API-indeling**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| Parameter | Beschrijving |
| --- | --- |
| `shop` | Uw subdomein `myshopify.com` URL. |
| `api_key` | Uw [!DNL Shopify] client-id. U kunt uw client-id ophalen vanuit de **clientgegevens** tabblad van het [!DNL Shopify] het dashboard van partners. |
| `scopes` | Het type toegang dat u wilt definiëren. U kunt bereik bijvoorbeeld instellen als `scope=write_orders,read_customers` om toestemmingen toe te staan om orden te wijzigen en klanten te lezen. |
| `redirect_uri` | De URL voor het script dat het toegangstoken genereert. |

**Verzoek**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**Antwoord**

Een succesvolle reactie keert uw omleidings URL, met inbegrip van de vergunningscode terug die wordt vereist om uw toegangstoken te produceren.

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### Uw toegangstoken ophalen

Nu u uw cliënt identiteitskaart, cliëntgeheim, en vergunningscode hebt, kunt u uw toegangstoken terugwinnen. Om uw toegangstoken terug te winnen, doe een verzoek van de POST aan uw domein `myshopify.com` URL terwijl het toevoegen van deze URL met [!DNL Shopify's] API-eindpunt: `/admin/oauth/access_token`.

**API-indeling**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**Verzoek**

Het volgende verzoek produceert een toegangstoken voor uw [!DNL Shopify] -instantie.

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

**Antwoord**

Een succesvolle reactie keert uw toegangstoken en toestemmingswerkingsgebied terug.

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## Webhaak voor streaming maken [!DNL Shopify] data {#webhook}

Met webhaken kunnen toepassingen gesynchroniseerd blijven met uw [!DNL Shopify] gegevens of voer een actie uit nadat een bepaalde gebeurtenis in een winkel voorkomt. Voor streaming [!DNL Shopify] gegevens aan Experience Platform, kunnen de webhooks worden gebruikt om het eindpunt van http en de onderwerpen voor abonnement te bepalen.

**Verzoek**

Met de volgende aanvraag wordt een webhaak gemaakt voor uw [!DNL Shopify Streaming] gegevens.

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
| `webhook.topic` | Het onderwerp van uw webshabonnement. Lees voor meer informatie de [[!DNL Shopify] WebHaak-gebeurtenishandleiding](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | De indeling van de gegevens. |

**Antwoord**

Een succesvolle reactie retourneert informatie over uw webhaak, inclusief de bijbehorende `id`, het adres en andere metagegevens.

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

Hieronder volgt een lijst met bekende beperkingen die u kunt tegenkomen bij het gebruik van webhaken met de [!DNL Shopify Streaming] bron.

* Het is niet gewaarborgd dat u de orde van levering van verschillende onderwerpen voor het zelfde middel kunt schikken. Het is bijvoorbeeld mogelijk dat een `products/update` webhaak wordt geleverd vóór een `products/create` webhaak.
* U kunt uw webhaak instellen om webhaakgebeurtenissen minstens één keer aan een eindpunt te leveren. Dit betekent dat een eindpunt dezelfde gebeurtenis meer dan één keer kan ontvangen. U kunt scannen op dubbele webhaakgebeurtenissen door de `X-Shopify-Webhook-Id` naar vorige gebeurtenissen.
* [!DNL Shopify] behandelt HTTP 2xx statusreacties als succesvolle berichten. Eventuele andere reacties op de statuscode worden beschouwd als mislukkingen. [!DNL Shopify] biedt een mechanisme voor het opnieuw proberen van mislukte websitemeldingen. Als er **geen reactie na het wachten van vijf seconden**, [!DNL Shopify] probeert de verbinding opnieuw **19 keer** in de loop van de volgende **48 uur**. Als er nog steeds geen reacties zijn tegen het einde van de periode van opnieuw proberen, [!DNL Shopify] Hiermee verwijdert u de webhaak.

## Volgende stappen

De volgende zelfstudies bieden stappen voor het tot stand brengen van een verbinding met uw [!DNL Shopify Streaming] bron naar Experience Platform met behulp van de API en de UI:

* [Een Shopify Streaming-bronverbinding en -gegevensstroom maken met de Flow Service API](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [Een Shopify-bronverbinding en -gegevensstroom maken in de gebruikersinterface](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
