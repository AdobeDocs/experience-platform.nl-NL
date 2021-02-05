---
keywords: Experience Platform;thuis;Intelligente services;populaire onderwerpen;intelligente service;Intelligente service
solution: Experience Platform, Intelligent Services
title: Gegevens voorbereiden voor gebruik in intelligente services
topic: Intelligent Services
description: 'Om de Intelligente Diensten inzichten van uw marketing gebeurtenisgegevens te ontdekken, moeten de gegevens semantisch worden verrijkt en in een standaardstructuur worden gehandhaafd. Intelligente services hefboomwerkervaringsgegevensmodel (XDM) om dit te bereiken. Specifiek, moeten alle datasets die in de Intelligente Diensten worden gebruikt] met het schema van XDM van Consumer ExperienceEvent (CEE) in overeenstemming zijn. '
translation-type: tm+mt
source-git-commit: eb163949f91b0d1e9cc23180bb372b6f94fc951f
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 0%

---


# Gegevens voorbereiden voor gebruik in [!DNL Intelligent Services]

Als u [!DNL Intelligent Services] inzichten wilt laten detecteren uit de gegevens van uw marketinggebeurtenissen, moeten de gegevens semantisch worden verrijkt en onderhouden in een standaardstructuur. [!DNL Intelligent Services] hefboomwerking  [!DNL Experience Data Model] (XDM) regelingen om dit te bereiken. Specifiek, moeten alle datasets die in [!DNL Intelligent Services] worden gebruikt met het schema van XDM van Consumer ExperienceEvent (CEE) in overeenstemming zijn.

Dit document verstrekt algemene begeleiding bij het in kaart brengen van uw marketing gebeurtenisgegevens van veelvoudige kanalen aan dit schema, schetsend informatie over belangrijke gebieden binnen het schema om u te helpen bepalen hoe te om uw gegevens aan zijn structuur effectief in kaart te brengen.

## Overzicht van workflow

Het voorbereidingsproces is afhankelijk van het feit of uw gegevens in Adobe Experience Platform of extern worden opgeslagen. Deze sectie vat de noodzakelijke stappen samen u, gegeven één van beide scenario&#39;s moet nemen.

### Externe gegevensvoorbereiding

Voer de onderstaande stappen uit als uw gegevens buiten [!DNL Experience Platform] zijn opgeslagen:

1. Neem contact op met de Adobe Consulting Services om toegangsreferenties aan te vragen voor een specifieke Azure Blob Storage-container.
1. Upload uw gegevens naar de Blob-container met uw toegangsgegevens.
1. Als u werkt met Adobe Consulting Services, worden uw gegevens toegewezen aan het [Consumer ExperienceEvent-schema](#cee-schema) en opgenomen in [!DNL Intelligent Services].

### [!DNL Experience Platform] gegevensvoorbereiding

Voer de onderstaande stappen uit als uw gegevens al zijn opgeslagen in [!DNL Platform]:

1. Controleer de structuur van het [Consumer ExperienceEvent-schema](#cee-schema) en bepaal of uw gegevens kunnen worden toegewezen aan de bijbehorende velden.
1. Neem contact op met de Consulting Services voor Adobe om uw gegevens toe te wijzen aan het schema en deze in te voeren in [!DNL Intelligent Services], of [volg de stappen in deze handleiding](#mapping) als u de gegevens zelf wilt toewijzen.

## Het CEE schema {#cee-schema} begrijpen

Het schema Consumer ExperienceEvent beschrijft het gedrag van een individu aangezien het betrekking heeft op digitale marketing gebeurtenissen (web of mobiel) evenals online of off-line handelsactiviteit. Het gebruik van dit schema wordt vereist voor [!DNL Intelligent Services] wegens zijn semantisch duidelijk-bepaalde gebieden (kolommen), vermijdend om het even welke onbekende namen die anders de gegevens minder duidelijk zouden maken.

Het CEE-schema legt, net als alle XDM ExperienceEvent-schema&#39;s, de op tijdreeksen gebaseerde status van het systeem vast wanneer een gebeurtenis (of set gebeurtenissen) plaatsvond, inclusief het tijdstip en de identiteit van het betreffende onderwerp. De gebeurtenissen van de ervaring zijn feitenverslagen van wat voorkwam, en zo zijn zij onveranderlijk en vertegenwoordigen wat gebeurde zonder samenvoeging of interpretatie.

[!DNL Intelligent Services] Gebruik verscheidene zeer belangrijke gebieden binnen dit schema om inzichten van uw marketing gebeurtenisgegevens te produceren, die allen op het wortelniveau kunnen worden gevonden en worden uitgebreid om hun vereiste subfields te tonen.

![](./images/data-preparation/schema-expansion.gif)

Net als alle XDM-schema&#39;s is de CEE-mix uitbreidbaar. Met andere woorden, extra velden kunnen worden toegevoegd aan de CEE-mix en verschillende variaties kunnen indien nodig worden opgenomen in meerdere schema&#39;s.

Een volledig voorbeeld van de mix vindt u in de [openbare XDM-opslagruimte](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). Bovendien kunt u het volgende [JSON dossier](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) voor een voorbeeld bekijken en kopiëren van hoe de gegevens kunnen worden gestructureerd om aan het CEE schema te voldoen. Verwijs naar beide voorbeelden aangezien u over de belangrijkste gebieden leert die in de sectie worden geschetst hieronder, om te bepalen hoe u uw eigen gegevens aan het schema kunt in kaart brengen.

## Hoofdvelden

Er zijn verscheidene zeer belangrijke gebieden binnen de CEE mengeling die zou moeten worden gebruikt om [!DNL Intelligent Services] nuttige inzichten te produceren. In deze sectie worden het gebruiksgeval en de verwachte gegevens voor deze velden beschreven en vindt u koppelingen naar de documentatie bij naslagwerken voor meer voorbeelden.

### Verplichte velden

Hoewel het gebruik van alle belangrijke gebieden sterk wordt geadviseerd, zijn er twee gebieden die **vereist** zijn om [!DNL Intelligent Services] te werken:

* [Een primair identiteitsveld](#identity)
* [xdm:tijdstempel](#timestamp)
* [xdm:channel](#channel)  (alleen verplicht voor Attribution AI)

#### Primaire identiteit {#identity}

Een van de velden in uw schema moet zijn ingesteld als primair identiteitsveld. Hiermee kan [!DNL Intelligent Services] elke instantie van tijdreeksgegevens koppelen aan een individuele persoon.

U moet bepalen welk veld het beste kan worden gebruikt als primaire identiteit op basis van de bron en de aard van uw gegevens. Een identiteitsveld moet een naamruimte **identity** bevatten die het type identiteitsgegevens aangeeft dat het veld als waarde verwacht. Voorbeelden van geldige naamruimtewaarden zijn:

* &quot;email&quot;
* &quot;phone&quot;
* &quot;mcid&quot; (voor Adobe Audience Manager-id&#39;s)
* &quot;aid&quot; (voor Adobe Analytics-id&#39;s)

Als u onzeker bent welk gebied u als primaire identiteit zou moeten gebruiken, contacteer de Consulting Diensten van de Adobe om de beste oplossing te bepalen.

#### xdm:tijdstempel {#timestamp}

Dit veld vertegenwoordigt de datum waarop de gebeurtenis heeft plaatsgevonden. Deze waarde moet worden opgegeven als een tekenreeks, volgens de ISO 8601-standaard.

#### xdm:channel {#channel}

>[!NOTE]
>
>Dit veld is alleen verplicht bij gebruik van Attribution AI.

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

Voor volledige informatie betreffende elk van de vereiste subvelden voor `xdm:channel`, gelieve te verwijzen naar [het schema van het ervaringskanaal](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) specificatie. Voor sommige voorbeeldafbeeldingen, zie [lijst hieronder](#example-channels).

##### Voorbeeldkanaaltoewijzingen {#example-channels}

In de volgende tabel staan enkele voorbeelden van marketingkanalen die zijn toegewezen aan het schema `xdm:channel`:

| Kanaal | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Betaalde zoekopdracht | https:/<span>/ns.adobe.com/xdm/channel-types/search | betaald | klikken |
| Sociaal - Marketing | https:/<span>/ns.adobe.com/xdm/channel-types/social | verdiend | klikken |
| Weergave | https:/<span>/ns.adobe.com/xdm/channel-types/display | betaald | klikken |
| Email | https:/<span>/ns.adobe.com/xdm/channel-types/email | betaald | klikken |
| Interne referentie | https:/<span>/ns.adobe.com/xdm/channel-types/direct | eigendom | klikken |
| WeergaveThrough weergeven | https:/<span>/ns.adobe.com/xdm/channel-types/display | betaald | indrukken |
| Omleiding QR-code | https:/<span>/ns.adobe.com/xdm/channel-types/direct | eigendom | klikken |
| Mobile | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | eigendom | klikken |

### Aanbevolen velden

De overige belangrijke velden worden in deze sectie beschreven. Hoewel deze gebieden niet noodzakelijk voor [!DNL Intelligent Services] aan het werk worden vereist, wordt het sterk geadviseerd dat u zo veel van hen zo veel mogelijk gebruikt om rijkere inzichten te bereiken.

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

Voor volledige informatie betreffende elk van de vereiste subvelden voor `xdm:productListItems`, gelieve te verwijzen naar [commercedetails schema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) specificatie.

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

Voor volledige informatie betreffende elk van de vereiste subvelden voor `xdm:commerce`, gelieve te verwijzen naar [commercedetails schema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) specificatie.

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

Voor volledige informatie over elk van de vereiste subvelden voor `xdm:productListItems`, gelieve te verwijzen naar [ExperienceEvent Webdetailschema](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) specificatie.

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

Voor volledige informatie over elk van de vereiste subvelden voor `xdm:productListItems` raadpleegt u de [marketingspecificatie](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md).

## Gegevens toewijzen en invoeren {#mapping}

Zodra u hebt bepaald of uw gegevens van marketinggebeurtenissen aan het CEE schema kunnen worden in kaart gebracht, is de volgende stap te bepalen welke gegevens u in [!DNL Intelligent Services] moet brengen. Alle historische gegevens die in [!DNL Intelligent Services] worden gebruikt moeten binnen het minimumtijdvenster van vier maanden van gegevens vallen, plus het aantal dagen voorgenomen als raadplegingsperiode.

Nadat het beslissen van de waaier van gegevens u wilt verzenden, contacteer de Raadplegende Diensten van de Adobe om uw gegevens aan het schema in kaart te brengen en het in de dienst in te voeren.

Als u een [!DNL Adobe Experience Platform] abonnement hebt en de gegevens zelf wilt toewijzen en invoeren, volgt u de stappen die in de onderstaande sectie worden beschreven.

### Adobe Experience Platform gebruiken

>[!NOTE]
>
>Voor de onderstaande stappen is een abonnement op Experience Platform vereist. Als u geen toegang tot Platform hebt, sla vooruit aan [volgende stappen](#next-steps) sectie over.

In deze sectie wordt de workflow beschreven voor het toewijzen en invoeren van gegevens in Experience Platform voor gebruik in [!DNL Intelligent Services], inclusief koppelingen naar zelfstudies voor gedetailleerde stappen.

#### Een CEE-schema en gegevensset maken

Wanneer u klaar bent om uw gegevens voor opname voor te bereiden, is de eerste stap een nieuw schema te creëren XDM dat de CEE mengeling gebruikt. De volgende zelfstudies lopen door het proces om een nieuw schema in UI of API tot stand te brengen:

* [Een schema maken in de gebruikersinterface](../xdm/tutorials/create-schema-ui.md)
* [Een schema maken in de API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>De bovenstaande zelfstudies volgen een algemene workflow voor het maken van een schema. Wanneer u een klasse voor het schema kiest, moet u de **XDM ExperienceEvent-klasse** gebruiken. Nadat u deze klasse hebt gekozen, kunt u de CEE-mix aan het schema toevoegen.

Nadat u de CEE-mix aan het schema hebt toegevoegd, kunt u desgewenst andere combinaties toevoegen voor extra velden in uw gegevens.

Zodra u het schema hebt gecreeerd en bewaard, kunt u een nieuwe dataset tot stand brengen die op dat schema wordt gebaseerd. De volgende zelfstudies lopen door het proces om een nieuwe dataset in UI of API tot stand te brengen:

* [Creeer een dataset in UI](../catalog/datasets/user-guide.md#create)  (volg het werkschema voor het gebruiken van een bestaand schema)
* [Een gegevensset maken in de API](../catalog/datasets/create.md)

Nadat de dataset wordt gecreeerd, kunt u het in het Platform UI binnen **[!UICONTROL Datasets]** werkruimte vinden.

![](images/data-preparation/dataset-location.png)

#### Identiteitsvelden toevoegen aan de gegevensset

Als u gegevens van [!DNL Adobe Audience Manager], [!DNL Adobe Analytics], of een andere externe bron inbrengt, dan hebt u de optie om een schemagebied als identiteitsgebied te plaatsen. Als u een schemaveld als een identiteitsveld wilt instellen, bekijkt u de sectie over het instellen van identiteitsvelden in de [UI-zelfstudie](../xdm/tutorials/create-schema-ui.md#identity-field) of [API-zelfstudie](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) voor het maken van een schema.

Als u gegevens uit een lokaal CSV-bestand opneemt, kunt u verdergaan met de volgende sectie op [mapping en het opnemen van gegevens](#ingest).

#### Gegevens toewijzen en invoeren {#ingest}

Na het creëren van een CEE schema en dataset, kunt u beginnen uw gegevenslijsten aan het schema in kaart te brengen en die gegevens in Platform in te voeren. Zie de zelfstudie over [het toewijzen van een CSV-bestand aan een XDM-schema](../ingestion/tutorials/map-a-csv-file.md) voor stappen over hoe u dit kunt uitvoeren in de gebruikersinterface. U kunt het volgende [voorbeeld JSON dossier](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) gebruiken om het innameproces te testen alvorens uw eigen gegevens te gebruiken.

Zodra een dataset is bevolkt, kan de zelfde dataset worden gebruikt om extra gegevensdossiers in te voeren.

Als uw gegevens worden opgeslagen in een ondersteunde toepassing van derden, kunt u er ook voor kiezen om een [bronconnector](../sources/home.md) te maken om uw gegevens van marketinggebeurtenissen in real-time in [!DNL Platform] in te voeren.

## Volgende stappen {#next-steps}

Dit document bevat algemene richtlijnen voor het voorbereiden van gegevens voor gebruik in [!DNL Intelligent Services]. Neem contact op met de Adobe Consulting Support als u extra advies nodig hebt op basis van uw gebruikscase.

Als u eenmaal een gegevensset met uw klantervaringsgegevens hebt gevuld, kunt u [!DNL Intelligent Services] gebruiken om inzichten te genereren. Raadpleeg de volgende documenten om aan de slag te gaan:

* [Overzicht van Attribution AI](./attribution-ai/overview.md)
* [AI-overzicht van klant](./customer-ai/overview.md)
