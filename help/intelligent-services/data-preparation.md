---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: Gegevens voorbereiden voor gebruik in intelligente services
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 9905f0248fe88bac5194560318cf8eced32ba93c
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 0%

---


# Gegevens voorbereiden voor gebruik in intelligente services

Om de Intelligente Diensten inzichten van uw marketing gebeurtenisgegevens te ontdekken, moeten de gegevens semantisch worden verrijkt en in een standaardstructuur worden gehandhaafd. Intelligente services hefboomwerkervaringsgegevensmodel (XDM) om dit te bereiken. Specifiek, moeten alle datasets die in de Intelligente Diensten worden gebruikt met het schema van XDM van **Consumer ExperienceEvent (CEE)** in overeenstemming zijn.

Dit document verstrekt algemene begeleiding bij het in kaart brengen van uw marketing gebeurtenisgegevens van veelvoudige kanalen aan dit schema, schetsend informatie over belangrijke gebieden binnen het schema om u te helpen bepalen hoe te om uw gegevens aan zijn structuur effectief in kaart te brengen.

## Overzicht van workflow

Het voorbereidingsproces varieert afhankelijk van het feit of uw gegevens in het Adobe Experience Platform of extern worden opgeslagen. Deze sectie vat de noodzakelijke stappen samen u, gegeven één van beide scenario&#39;s moet nemen.

### Externe gegevensvoorbereiding

Als uw gegevens buiten [!DNL Experience Platform]zijn opgeslagen, voert u de volgende stappen uit:

1. Neem contact op met de Adobe Consulting Services om toegangsreferenties aan te vragen voor een specifieke Azure Blob Storage-container.
1. Upload uw gegevens naar de Blob-container met uw toegangsgegevens.
1. Als u werkt met Adobe Consulting Services, worden uw gegevens toegewezen aan het [Consumer ExperienceEvent-schema](#cee-schema) en opgenomen in Intelligent Services.

### [!DNL Experience Platform] gegevensvoorbereiding

Voer de onderstaande stappen uit als uw gegevens al zijn opgeslagen in [!DNL Platform]:

1. Controleer de structuur van het schema [](#cee-schema) Consumer ExperienceEvent en bepaal of uw gegevens kunnen worden toegewezen aan de velden.
1. Neem contact op met de Adobe Consulting Services om u te helpen uw gegevens toe te wijzen aan het schema en deze in te voeren in Intelligente services. U kunt ook de stappen in deze handleiding [](#mapping) volgen als u de gegevens zelf wilt toewijzen.

## Het CEE-schema {#cee-schema}

Het schema Consumer ExperienceEvent beschrijft het gedrag van een individu aangezien het betrekking heeft op digitale marketing gebeurtenissen (web of mobiel) evenals online of off-line handelsactiviteit. Het gebruik van dit schema wordt vereist voor de Intelligente Diensten wegens zijn semantisch duidelijk bepaalde gebieden (kolommen), vermijdend om het even welke onbekende namen die anders de gegevens minder duidelijk zouden maken.

Het CEE-schema legt, net als alle XDM ExperienceEvent-schema&#39;s, de op tijdreeksen gebaseerde status van het systeem vast wanneer een gebeurtenis (of set gebeurtenissen) plaatsvond, inclusief het tijdstip en de identiteit van het betreffende onderwerp. De gebeurtenissen van de ervaring zijn feitenverslagen van wat voorkwam, en zo zijn zij onveranderlijk en vertegenwoordigen wat gebeurde zonder samenvoeging of interpretatie.

De intelligente Diensten gebruiken verscheidene zeer belangrijke gebieden binnen dit schema om inzichten van uw marketing gebeurtenisgegevens te produceren, die allen op het wortelniveau kunnen worden gevonden en worden uitgebreid om hun vereiste subfields te tonen.

![](./images/data-preparation/schema-expansion.gif)

Net als alle XDM-schema&#39;s is de CEE-mix uitbreidbaar. Met andere woorden, extra velden kunnen worden toegevoegd aan de CEE-mix en verschillende variaties kunnen indien nodig worden opgenomen in meerdere schema&#39;s.

Een volledig voorbeeld van de mix vindt u in de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)en moet worden gebruikt als referentie voor de belangrijkste velden die in de sectie hieronder worden beschreven.

## Hoofdvelden

Er zijn verscheidene zeer belangrijke gebieden binnen de CEE mengeling die zou moeten worden gebruikt om de Intelligente Diensten nuttige inzichten te produceren. In deze sectie worden het gebruiksgeval en de verwachte gegevens voor deze velden beschreven en vindt u koppelingen naar de documentatie bij naslagwerken voor meer voorbeelden.

### Verplichte velden

Hoewel het gebruik van alle belangrijke gebieden sterk wordt aanbevolen, zijn er twee gebieden die **vereist** zijn om de Intelligente Diensten te laten werken:

* [Een primair identiteitsveld](#identity)
* [xdm:tijdstempel](#timestamp)
* [xdm:channel](#channel) (alleen verplicht voor AI-kenmerk)

#### Primaire identiteit {#identity}

Één van de gebieden in uw schema moet als primair identiteitsgebied worden geplaatst, dat de Intelligente Diensten toestaat om elke instantie van tijd-reeksgegevens aan een individuele persoon te verbinden.

U moet bepalen welk veld het beste kan worden gebruikt als primaire identiteit op basis van de bron en de aard van uw gegevens. Een identiteitsveld moet een naamruimte **voor de** identiteit bevatten die het type identiteitsgegevens aangeeft dat het veld als waarde verwacht. Voorbeelden van geldige naamruimtewaarden zijn:

* &quot;email&quot;
* &quot;phone&quot;
* &quot;mcid&quot; (voor Adobe Audience Manager-id&#39;s)
* &quot;aid&quot; (voor Adobe Analytics-id&#39;s)

Als u niet zeker weet welk veld u als primaire identiteit moet gebruiken, neemt u contact op met Adobe Consulting Services om de beste oplossing te bepalen.

#### xdm:tijdstempel {#timestamp}

Dit veld vertegenwoordigt de datum waarop de gebeurtenis heeft plaatsgevonden. Deze waarde moet worden opgegeven als een tekenreeks, volgens de ISO 8601-standaard.

#### xdm:kanaal {#channel}

>[!NOTE] Dit veld is alleen verplicht bij gebruik van Attribution AI.

Dit gebied vertegenwoordigt het marketing kanaal met betrekking tot ExperienceEvent. Het veld bevat informatie over het kanaaltype, het mediatype en het locatietype.

![](./images/data-preparation/channel.png)

**Voorbeeldschema**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Voor volledige informatie over elk van de vereiste subvelden voor `xdm:channel`, gelieve te verwijzen naar het schema [van het](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) ervaringskanaal. Zie de [tabel hieronder](#example-channels)voor een aantal voorbeeldtoewijzingen.

##### Voorbeeldkanaaltoewijzingen {#example-channels}

In de volgende tabel staan enkele voorbeelden van marketingkanalen die zijn toegewezen aan het `xdm:channel` schema:

| Kanaal | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Betaalde zoekopdracht | https:/<span>/ns.adobe.com/xdm/channel-types/search | betaald | klikken |
| Sociaal - Marketing | https:/<span>/ns.adobe.com/xdm/channel-types/social | verdiend | klikken |
| Weergave | https:/<span>/ns.adobe.com/xdm/channel-types/display | betaald | klikken |
| E-mail | https:/<span>/ns.adobe.com/xdm/channel-types/email | betaald | klikken |
| Interne referentie | https:/<span>/ns.adobe.com/xdm/channel-types/direct | eigendom | klikken |
| WeergaveThrough weergeven | https:/<span>/ns.adobe.com/xdm/channel-types/display | betaald | indrukken |
| Omleiding QR-code | https:/<span>/ns.adobe.com/xdm/channel-types/direct | eigendom | klikken |
| Mobile | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | eigendom | klikken |

### Aanbevolen velden

De overige belangrijke velden worden in deze sectie beschreven. Hoewel deze gebieden niet noodzakelijk voor de Intelligente Diensten aan het werk worden vereist, wordt het sterk geadviseerd dat u zo veel van hen zo veel mogelijk gebruikt om rijkere inzichten te bereiken.

#### xdm:productListItems

Dit veld is een array van items die producten vertegenwoordigen die door een klant zijn geselecteerd, waaronder de SKU, naam, prijs en hoeveelheid van het product.

![](./images/data-preparation/productListItems.png)

**Voorbeeldschema**

```json
[
  {
    "xdm:SKU": "1002352692",
    "xdm:name": "24-Watt 8-Light Chrome Integrated LED Bath Light",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 159.45
  },
  {
    "xdm:SKU": "3398033623",
    "xdm:name": "16ft RGB LED Strips",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 79.99
  }
]
```

Voor volledige informatie over elk van de vereiste subvelden voor `xdm:productListItems`, gelieve te verwijzen naar het schema [van](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) handelsdetails.

#### xdm:handel

Dit veld bevat handelspecifieke informatie over de ExperienceEvent, waaronder het inkoopordernummer en betalingsgegevens.

![](./images/data-preparation/commerce.png)

**Voorbeeldschema**

```json
{
    "xdm:order": {
      "xdm:purchaseID": "a8g784hjq1mnp3",
      "xdm:purchaseOrderNumber": "123456",
      "xdm:payments": [
        {
          "xdm:transactionID": "transactid-a111",
          "xdm:paymentAmount": 59,
          "xdm:paymentType": "credit_card",
          "xdm:currencyCode": "USD"
        },
        {
          "xdm:transactionId": "transactid-a222",
          "xdm:paymentAmount": 100,
          "xdm:paymentType": "gift_card",
          "xdm:currencyCode": "USD"
        }
      ],
      "xdm:currencyCode": "USD",
      "xdm:priceTotal": 159
    },
    "xdm:purchases": {
      "xdm:value": 1
    }
  }
```

Voor volledige informatie over elk van de vereiste subvelden voor `xdm:commerce`, gelieve te verwijzen naar het schema [van](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) handelsdetails.

#### xdm:web

In dit veld worden de webdetails weergegeven die betrekking hebben op de ExperienceEvent, zoals de interactie, paginagegevens en de referentie.

![](./images/data-preparation/web.png)

**Voorbeeldschema**

```json
{
  "xdm:webPageDetails": {
    "xdm:siteSection": "Shopping Cart",
    "xdm:server": "example.com",
    "xdm:name": "Purchase Confirmation",
    "xdm:URL": "https://www.example.com/orderConf",
    "xdm:errorPage": false,
    "xdm:homePage": false,
    "xdm:pageViews": {
      "xdm:value": 1
    }
  },
  "xdm:webReferrer": {
    "xdm:URL": "https://www.example.com/checkout",
    "xdm:referrerType": "internal"
  }
}
```

Voor volledige informatie over elk van de vereiste subvelden voor `xdm:productListItems`, raadpleegt u de specificatie van het schema [voor](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) ExperienceEvent-webdetails.

#### xdm:marketing

Dit veld bevat informatie over marketingactiviteiten die actief zijn met het aanraakpunt.

![](./images/data-preparation/marketing.png)

**Voorbeeldschema**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Voor volledige informatie over elk van de vereiste subvelden voor `xdm:productListItems`, gelieve te verwijzen naar de specificatie van het [marketingdossier](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) .

## Gegevens toewijzen en opnemen (#mapping)

Zodra u hebt bepaald of uw gegevens van de marketinggebeurtenissen aan het CEE schema kunnen worden in kaart gebracht, is de volgende stap te bepalen welke gegevens u in de Intelligente Diensten moet brengen. Alle historische gegevens die in de Intelligente Diensten worden gebruikt moeten binnen het minimumtijdvenster van vier maanden van gegevens vallen, plus het aantal dagen voorgenomen als raadplegingsperiode.

Nadat u het gegevensbereik hebt bepaald dat u wilt verzenden, neemt u contact op met de Adobe Consulting Services om uw gegevens toe te wijzen aan het schema en deze in te voeren in de service.

Als u een [!DNL Adobe Experience Platform] abonnement hebt en de gegevens zelf wilt toewijzen en invoeren, volgt u de stappen die in de onderstaande sectie worden beschreven.

### Adobe Experience Platform gebruiken

>[!NOTE] Voor de onderstaande stappen is een abonnement op Experience Platform vereist. Als u geen toegang tot Platform hebt, gaat u verder met de sectie [Volgende stappen](#next-steps) .

Deze sectie schetst de werkschema voor het in kaart brengen van en het opnemen van gegevens in Experience Platform voor gebruik in de Intelligente Diensten, met inbegrip van verbindingen aan leerprogramma&#39;s voor gedetailleerde stappen.

#### Een CEE-schema en gegevensset maken

Wanneer u klaar bent om uw gegevens voor opname voor te bereiden, is de eerste stap een nieuw schema te creëren XDM dat de CEE mengeling gebruikt. De volgende zelfstudies lopen door het proces om een nieuw schema in UI of API tot stand te brengen:

* [Een schema maken in de gebruikersinterface](../xdm/tutorials/create-schema-ui.md)
* [Een schema maken in de API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] De bovenstaande zelfstudies volgen een algemene workflow voor het maken van een schema. Wanneer u een klasse voor het schema kiest, moet u de **klasse** XDM ExperienceEvent gebruiken. Nadat u deze klasse hebt gekozen, kunt u de CEE-mix aan het schema toevoegen.

Nadat u de CEE-mix aan het schema hebt toegevoegd, kunt u desgewenst andere combinaties toevoegen voor extra velden in uw gegevens.

Zodra u het schema hebt gecreeerd en bewaard, kunt u een nieuwe dataset tot stand brengen die op dat schema wordt gebaseerd. De volgende zelfstudies lopen door het proces om een nieuwe dataset in UI of API tot stand te brengen:

* [Creeer een dataset in UI](../catalog/datasets/user-guide.md#create) (volg het werkschema voor het gebruiken van een bestaand schema)
* [Een gegevensset maken in de API](../catalog/datasets/create.md)

Nadat de dataset wordt gecreeerd, kunt u het in het Platform UI binnen de *[!UICONTROL werkruimte van Datasets]* vinden.

![](images/data-preparation/dataset-location.png)

#### Een primaire naamruimte-tag toevoegen aan de gegevensset

>[!NOTE] De toekomstige versies van Intelligente Diensten zullen de Dienst [van de Identiteit van het](../identity-service/home.md) Adobe Experience Platform in hun mogelijkheden van de klantenidentificatie integreren. De hieronder beschreven stappen kunnen dan ook worden gewijzigd.

Als u gegevens uit [!DNL Adobe Audience Manager], [!DNL Adobe Analytics]of een andere externe bron inbrengt, dan moet u een `primaryIdentityNameSpace` markering aan de dataset toevoegen. Dit kan worden gedaan door een PATCH- verzoek aan de Dienst API van de Catalogus te doen.

Als u gegevens uit een lokaal CSV-bestand opneemt, kunt u verdergaan met de volgende sectie over het [toewijzen en invoeren van gegevens](#ingest).

Voordat u de voorbeeld-API-aanroep hieronder volgt, raadpleegt u de sectie [Aan de](../catalog/api/getting-started.md) slag in de handleiding voor ontwikkelaars van catalogi voor belangrijke informatie over vereiste koppen.

**API-indeling**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De id van de gegevensset die u eerder hebt gemaakt. |

**Verzoek**

Afhankelijk van de bron waaruit u gegevens opgeeft, moet u de juiste waarden opgeven `primaryIdentityNamespace` en de juiste `sourceConnectorId` waarden opgeven in de payload van de aanvraag.

In het volgende verzoek worden de juiste tagwaarden voor Audience Manager toegevoegd:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "tags": {
          "primaryIdentityNameSpace": ["mcid"],
          "sourceConnectorId": ["audiencemanager"],
        }
      }'
```

In het volgende verzoek worden de juiste tagwaarden voor Analytics toegevoegd:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "tags": {
          "primaryIdentityNameSpace": ["aaid"],
          "sourceConnectorId": ["analytics"],
        }
      }'
```

>[!NOTE] Zie het overzicht [van naamruimte voor](../identity-service/namespaces.md)identiteiten voor meer informatie over het werken met naamruimten in het Platform.

**Antwoord**

Een succesvolle reactie keert een serie terug die identiteitskaart van de bijgewerkte dataset bevat. Deze id moet overeenkomen met de id die in de PATCH-aanvraag is verzonden.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

#### Gegevens toewijzen en opnemen {#ingest}

Na het creëren van een CEE schema en dataset, kunt u beginnen uw gegevenslijsten aan het schema in kaart te brengen en die gegevens in Platform in te voeren. Zie de zelfstudie over het [toewijzen van een CSV-bestand aan een XDM-schema](../ingestion/tutorials/map-a-csv-file.md) voor stappen over het uitvoeren van dit bestand in de gebruikersinterface. Zodra een dataset is bevolkt, kan de zelfde dataset worden gebruikt om extra gegevensdossiers in te voeren.

Als uw gegevens in een gesteunde derdetoepassing worden opgeslagen, kunt u ook verkiezen om een [bronschakelaar](../sources/home.md) tot stand te brengen om uw gegevens van marketinggebeurtenissen in Platform in real time in te voeren.

## Volgende stappen {#next-steps}

Dit document bevat algemene richtlijnen voor het voorbereiden van gegevens voor gebruik in Intelligente services. Neem contact op met de Technische Ondersteuning van Adobe als u extra advies nodig hebt op basis van uw gebruikscase.

Zodra u met succes een dataset met uw gegevens van de klantenervaring hebt bevolkt, kunt u de Intelligente Diensten gebruiken om inzichten te produceren. Raadpleeg de volgende documenten om aan de slag te gaan:

* [Overzicht AI-kenmerken](./attribution-ai/overview.md)
* [AI-overzicht van klant](./customer-ai/overview.md)
