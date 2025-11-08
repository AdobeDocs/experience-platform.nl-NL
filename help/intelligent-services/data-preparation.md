---
keywords: Experience Platform;home;Intelligente services;populaire onderwerpen;intelligente service;Intelligente service
solution: Experience Platform
title: Gegevens voorbereiden voor gebruik in intelligente services
description: Om de Intelligente Diensten inzichten van uw marketing gebeurtenisgegevens te ontdekken, moeten de gegevens semantisch worden verrijkt en in een standaardstructuur worden gehandhaafd. De intelligente diensten gebruiken de schema's van de Gegevens van de Ervaring (XDM) om dit te bereiken.
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: 73dea391f8fcb1d2d491c814b453afb4e538459d
workflow-type: tm+mt
source-wordcount: '2938'
ht-degree: 0%

---

# Gegevens voorbereiden voor gebruik in [!DNL Intelligent Services]

Als u in [!DNL Intelligent Services] inzichten wilt detecteren uit de gegevens van uw marketinggebeurtenissen, moeten de gegevens semantisch worden verrijkt en onderhouden in een standaardstructuur. [!DNL Intelligent Services] hefboomwerking [!DNL Experience Data Model] (XDM) schema&#39;s om dit te bereiken. Specifiek, moeten alle datasets die in [!DNL Intelligent Services] worden gebruikt met het schema van XDM van Consumer ExperienceEvent (CEE) in overeenstemming zijn of de schakelaar van Adobe Analytics gebruiken. Daarnaast ondersteunt de AI van de Klant de Adobe Audience Manager-aansluiting.

Dit document verstrekt algemene begeleiding bij het in kaart brengen van uw gegevens van marketinggebeurtenissen van veelvoudige kanalen aan het CEE schema, schetsend informatie over belangrijke gebieden binnen het schema om u te helpen bepalen hoe te om uw gegevens aan zijn structuur effectief in kaart te brengen. Als u bij het gebruiken van de gegevens van Adobe Analytics van plan bent, te bekijken gelieve de sectie voor [&#x200B; de gegevensvoorbereiding van Adobe Analytics &#x200B;](#analytics-data). Als u bij het gebruiken van de gegevens van Adobe Audience Manager (Klant AI slechts) van plan bent, te bekijken gelieve de sectie voor [&#x200B; de gegevensvoorbereiding van de Manager van de Volgorde van Adobe &#x200B;](#AAM-data).

## Gegevensvereisten

[!DNL Intelligent Services] vereist verschillende hoeveelheden historische gegevens, afhankelijk van het doel dat u maakt. Ongeacht, moeten de gegevens u voor **allen** [!DNL Intelligent Services] voorbereidingen treft zowel positieve als negatieve klantenreizen/gebeurtenissen omvatten. Het hebben van zowel negatieve als positieve gebeurtenissen verbetert modelprecisie en nauwkeurigheid.

Als u bijvoorbeeld de AI van de Klant gebruikt om de neiging te voorspellen om een product te kopen, heeft het model voor AI van de Klant zowel voorbeelden van succesvolle aankoopwegen als voorbeelden van mislukte wegen nodig. Dit komt omdat de AI van de Klant tijdens modeltraining probeert te begrijpen welke gebeurtenissen en reizen tot een aankoop leiden. Dit omvat ook de acties die zijn ondernomen door klanten die geen goederen hebben gekocht, zoals een persoon die zijn reis heeft gestopt bij het toevoegen van een artikel aan de wagen. Deze klanten kunnen echter op vergelijkbare wijze te werk gaan. Klantenservice kan echter inzichten verschaffen en de belangrijkste verschillen en factoren die tot een hogere prioriteitsscore leiden, opruimen. Op dezelfde manier vereist Attribution AI zowel soorten gebeurtenissen als reizen om metriek zoals touchpoint doeltreffendheid, hoogste omzettingswegen, en onderverdelingen door touchpoint positie te tonen.

Voor meer voorbeelden en informatie over historische gegevensvereisten, bezoek de [&#x200B; AI van de Klant &#x200B;](./customer-ai/data-requirements.md#data-requirements) of [&#x200B; sectie van de Eigenschappen AI &#x200B;](./attribution-ai/input-output.md#data-requirements) historische gegevensvereisten in de input/outputdocumentatie.

### Richtlijnen voor het koppelen van gegevens

U wordt aangeraden de gebeurtenissen van een gebruiker zo veel mogelijk aan te sluiten op een gemeenschappelijke id. U hebt bijvoorbeeld gebruikersgegevens met &quot;id1&quot; voor 10 gebeurtenissen. Later heeft dezelfde gebruiker de cookie-id verwijderd en wordt deze als &quot;id2&quot; opgenomen bij de volgende 20 gebeurtenissen. Als u weet dat id1 en id2 aan de zelfde gebruiker beantwoorden, is de beste praktijk om alle 30 gebeurtenissen met gemeenschappelijke identiteitskaart te hechten.

Als dit niet mogelijk is, moet u elke set gebeurtenissen als een andere gebruiker behandelen wanneer u uw modelinvoergegevens maakt. Dit zorgt voor de beste resultaten tijdens modeltraining en scoring.

## Overzicht van workflow

Het voorbereidingsproces is afhankelijk van het feit of uw gegevens in Adobe Experience Platform of extern worden opgeslagen. Deze sectie vat de noodzakelijke stappen samen u, gegeven één van beide scenario&#39;s moet nemen.

### Externe gegevensvoorbereiding

Als uw gegevens buiten Experience Platform worden opgeslagen, moet u uw gegevens aan de vereiste en relevante gebieden in het schema van a [&#x200B; Consumer ExperienceEvent in kaart brengen &#x200B;](#cee-schema). Dit schema kan worden aangevuld met aangepaste veldgroepen om uw klantgegevens beter vast te leggen. Zodra in kaart gebracht, kunt u een dataset tot stand brengen gebruikend uw schema van Consumer ExperienceEvent en [&#x200B; neemt uw gegevens aan Experience Platform &#x200B;](../ingestion/home.md) in. De CEE dataset kan dan worden geselecteerd wanneer het vormen van [!DNL Intelligent Service].

Afhankelijk van de [!DNL Intelligent Service] die u wilt gebruiken, zijn mogelijk verschillende velden vereist. Houd er rekening mee dat u het beste gegevens aan een veld kunt toevoegen als u over de beschikbare gegevens beschikt. Om meer over de vereiste gebieden te leren, bezoek de [&#x200B; AI van de Attributie &#x200B;](./attribution-ai/input-output.md) of [&#x200B; de gids van de Klant AI &#x200B;](./customer-ai/data-requirements.md) gegevensvereisten.

### Adobe Analytics-gegevensvoorbereiding {#analytics-data}

AI en Attribution AI bieden native ondersteuning voor Adobe Analytics-gegevens. Om de gegevens van Adobe Analytics te gebruiken, volg de stappen die in de documentatie worden geschetst aan opstelling een [&#x200B; bron van Analytics schakelaar &#x200B;](../sources/tutorials/ui/create/adobe-applications/analytics.md).

Zodra de bronschakelaar uw gegevens in Experience Platform stroomt, kunt u Adobe Analytics als gegevensbron selecteren die door een dataset tijdens uw instantieconfiguratie wordt gevolgd. Alle vereiste groepen van schemagebieden en individuele gebieden worden automatisch gecreeerd tijdens de verbindingsopstelling. U te hoeven niet om (Extraheren, Transformeren, Lading) de datasets in het formaat te ETL.

Als u de gegevens die door de Adobe Analytics-bronconnector naar Adobe Experience Platform worden geleid, vergelijkt met Adobe Analytics-gegevens, kunnen er verschillen optreden. De Analytics Source-connector kan rijen neerzetten tijdens de transformatie naar een XDM-schema (Experience Data Model). Er kunnen meerdere redenen zijn waarom de hele rij ongeschikt is voor transformatie, zoals ontbrekende tijdstempels, ontbrekende ID&#39;s, ongeldige id&#39;s of id&#39;s van grote personen, ongeldige analytische waarden en meer.

Voor meer informatie en voorbeelden, bezoek de documentatie voor [&#x200B; het vergelijken van gegevens van Adobe Analytics en van Customer Journey Analytics &#x200B;](https://www.adobe.com/go/compare-aa-data-to-cja-data). Dit artikel is ontworpen om u te helpen voor die verschillen diagnostiseren en op te lossen zodat u en uw team Adobe Experience Platform-gegevens voor Intelligente services kunnen gebruiken zonder dat dit wordt belemmerd door zorgen over gegevensintegriteit.

In de Diensten van de Vraag van Adobe Experience Platform, stel de volgende Totale Verslagen tussen begin en eind timestamp door channel.typeAtSource vraag in werking om de telling door marketing kanalen te vinden.

```SELECT channel.typeAtSource as typeAtSource,
       Count(_id) AS Records 
FROM  df_hotel
WHERE timestamp>=from_utc_timestamp('2021-05-15','UTC')
        AND timestamp<from_utc_timestamp('2022-01-10','UTC')
        AND timestamp IS NOT NULL
        AND enduserids._experience.aaid.id IS NOT NULL
GROUP BY channel.typeAtSource
```

>[!IMPORTANT]
>
>De Adobe Analytics-aansluiting heeft maximaal vier weken nodig om back-ups van gegevens te maken. Als u onlangs opstelling een verbinding zou moeten verifiëren u dat de dataset de minimumlengte van gegevens heeft die voor Klant of AI van de Attributie wordt vereist. Gelieve te herzien de historische gegevenssecties in [&#x200B; AI van de Klant &#x200B;](./customer-ai/data-requirements.md#data-requirements) of [&#x200B; AI van de Attributie &#x200B;](./attribution-ai/input-output.md#data-requirements), en verifieer u genoeg gegevens voor uw vooruitgangsdoel hebt.

### Adobe Audience Manager-gegevensvoorbereiding (alleen voor AI van klant) {#AAM-data}

Adobe Audience Manager-gegevens worden native door de klant ondersteund. Om de gegevens van Audience Manager te gebruiken, volg de stappen die in de documentatie worden geschetst aan opstelling een [&#x200B; bron van Audience Manager schakelaar &#x200B;](../sources/tutorials/ui/create/adobe-applications/audience-manager.md).

Zodra de bronaansluiting uw gegevens naar Experience Platform stroomt, kunt u Adobe Audience Manager selecteren als gegevensbron, gevolgd door een gegevensset tijdens uw AI-configuratie van de klant. Alle groepen van schemagebieden en individuele gebieden worden automatisch gecreeerd tijdens de verbindingsopstelling. U te hoeven niet om (Extraheren, Transformeren, Lading) de datasets in het formaat te ETL.

>[!IMPORTANT]
>
>Als u onlangs opstelling een schakelaar zou moeten verifiëren u dat de dataset de minimumlengte van vereiste gegevens heeft. Gelieve te herzien de historische gegevenssectie in de [&#x200B; input/outputdocumentatie &#x200B;](./customer-ai/data-requirements.md) voor Klant AI, en verifieer u genoeg gegevens voor uw vooruitgangsdoel hebt.

### [!DNL Experience Platform] gegevensvoorbereiding

Voer de onderstaande stappen uit als uw gegevens al zijn opgeslagen in [!DNL Experience Platform] en niet via de Adobe Analytics- of Adobe Audience Manager-bronconnectors (alleen Customer AI) worden gestreamd. Het wordt nog geadviseerd u het CEE schema begrijpt.

1. Herzie de structuur van het [&#x200B; schema van ExperienceEvent van de Consumenten &#x200B;](#cee-schema) en bepaal of uw gegevens aan zijn gebieden kunnen worden in kaart gebracht.
2. De Diensten van Adobe Consulting van het contact helpen uw gegevens aan het schema in kaart brengen en het opnemen in [!DNL Intelligent Services], of [&#x200B; volgen de stappen in deze gids &#x200B;](#mapping) als u de gegevens wilt in kaart brengen zelf.

## Het CEE-schema {#cee-schema}

Het schema Consumer ExperienceEvent beschrijft het gedrag van een individu aangezien het betrekking heeft op digitale marketing gebeurtenissen (web of mobiel) evenals online of off-line handelsactiviteit. Het gebruik van dit schema is vereist voor [!DNL Intelligent Services] vanwege de semantisch duidelijk gedefinieerde velden (kolommen). Hierbij worden onbekende namen vermeden die de gegevens anders minder duidelijk zouden maken.

Het CEE-schema legt, net als alle XDM ExperienceEvent-schema&#39;s, de op tijdreeksen gebaseerde status van het systeem vast wanneer een gebeurtenis (of set gebeurtenissen) plaatsvond, inclusief het tijdstip en de identiteit van het betreffende onderwerp. De gebeurtenissen van de ervaring zijn feitenverslagen van wat voorkwam, en zo zijn zij onveranderlijk en vertegenwoordigen wat gebeurde zonder samenvoeging of interpretatie.

[!DNL Intelligent Services] gebruikt verscheidene zeer belangrijke gebieden binnen dit schema om inzichten van uw gegevens van marketinggebeurtenissen te produceren, die allen op het wortelniveau kunnen worden gevonden en worden uitgebreid om hun vereiste subfields te tonen.

![&#x200B; Demo van schemauitbreiding in Adobe Experience Platform UI, die navigatie en subfield details tonen.](./images/data-preparation/schema-expansion.gif)

Net als alle XDM-schema&#39;s is de veldgroep van het CEE-schema uitbreidbaar. Met andere woorden, er kunnen extra velden worden toegevoegd aan de CEE-veldgroep en indien nodig kunnen verschillende variaties in meerdere schema&#39;s worden opgenomen.

Een volledig voorbeeld van de gebiedsgroep kan in de [&#x200B; openbare bewaarplaats worden gevonden XDM &#x200B;](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). Bovendien kunt u het volgende [&#x200B; JSON- dossier &#x200B;](https://github.com/AdobeDocs/experience-platform.nl-NL/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) voor een voorbeeld van bekijken en kopiëren hoe de gegevens kunnen worden gestructureerd om aan het CEE schema te voldoen. Verwijs naar beide voorbeelden aangezien u over de belangrijkste gebieden leert die in de sectie worden geschetst hieronder, om te bepalen hoe u uw eigen gegevens aan het schema kunt in kaart brengen.

## Hoofdvelden

Er zijn verschillende sleutelvelden in de CEE-veldgroep die moeten worden gebruikt om [!DNL Intelligent Services] nuttige inzichten te laten genereren. In deze sectie worden het gebruiksgeval en de verwachte gegevens voor deze velden beschreven en vindt u koppelingen naar de documentatie bij naslagwerken voor meer voorbeelden.

### Verplichte velden

Terwijl het gebruik van alle zeer belangrijke gebieden sterk wordt geadviseerd, zijn er twee gebieden die **&#x200B;**&#x200B;worden vereist opdat [!DNL Intelligent Services] werken:

* [Een primair identiteitsveld](#identity)
* [xdm:tijdstempel](#timestamp)
* [&#x200B; xdm:kanaal &#x200B;](#channel) (verplicht slechts voor AI van de Attributie)

#### Primaire identiteit {#identity}

Een van de velden in uw schema moet zijn ingesteld als primair identiteitsveld. Dit betekent dat [!DNL Intelligent Services] elke instantie van tijdreeksgegevens kan koppelen aan een individuele persoon.

U moet bepalen welk veld het beste kan worden gebruikt als primaire identiteit op basis van de bron en de aard van uw gegevens. Een identiteitsgebied moet een **identiteit namespace** omvatten die op het type van identiteitsgegevens wijst het gebied als waarde verwacht. Enkele geldige naamruimtewaarden zijn:

>[!NOTE]
>
>De Experience Cloud-id (ECID) wordt ook wel MCID genoemd en wordt nog steeds gebruikt in naamruimten.

* &quot;email&quot;
* &quot;phone&quot;
* &quot;mcid&quot; (voor Adobe Audience Manager-id&#39;s)
* &quot;aid&quot; (voor Adobe Analytics-id&#39;s)

Als u niet zeker bent welk gebied u als primaire identiteit zou moeten gebruiken, contacteer de Diensten van Adobe Consulting om de beste oplossing te bepalen. Als er geen primaire identiteit is ingesteld, gebruikt de toepassing Intelligente service het volgende standaardgedrag:

| Standaard | Attributie-AI | Customer AI |
| --- | --- | --- |
| Identiteitskolom | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| Naamruimte | STEUN | ECID |

Als u een primaire identiteit wilt instellen, navigeert u naar het schema op het tabblad **[!UICONTROL Schemas]** en selecteert u de hyperlink voor de schemanaam om het schema **[!DNL Schema Editor]** te openen.

![&#x200B; Navigatie aan het schema in Adobe Experience Platform UI.](./images/data-preparation/navigate_schema.png)

Navigeer vervolgens naar het veld dat u als primaire identiteit wilt gebruiken en selecteer het. Het menu **[!UICONTROL Field properties]** wordt geopend voor dat veld.

![&#x200B; het proces om het gewenste gebied in Adobe Experience Platform UI te selecteren.](./images/data-preparation/find_field.png)

Blader in het menu **[!UICONTROL Field properties]** omlaag totdat u het selectievakje **[!UICONTROL Identity]** hebt gevonden. Nadat u het selectievakje hebt ingeschakeld, wordt de optie voor het instellen van de geselecteerde identiteit weergegeven als de **[!UICONTROL Primary identity]** . Selecteer dit vak ook.

![&#x200B; Checkbox om primaire identiteit in Adobe Experience Platform UI te plaatsen.](./images/data-preparation/set_primary_identity.png)

Vervolgens moet u een **[!UICONTROL Identity namespace]** opgeven uit de lijst met vooraf gedefinieerde naamruimten in het vervolgkeuzemenu. In dit voorbeeld wordt de ECID-naamruimte geselecteerd omdat een Adobe Audience Manager-id `mcid.id` wordt gebruikt. Selecteer **[!UICONTROL Apply]** om de updates te bevestigen en selecteer vervolgens **[!UICONTROL Save]** in de rechterbovenhoek om de wijzigingen in het schema op te slaan.

![&#x200B; Vervolgkeuzemenu dat de selectie van ECID namespace in Adobe Experience Platform UI toont.](./images/data-preparation/select_namespace.png)

#### xdm:tijdstempel {#timestamp}

Dit veld vertegenwoordigt de datum waarop de gebeurtenis heeft plaatsgevonden. Deze waarde moet worden opgegeven als een tekenreeks, volgens de ISO 8601-standaard.

#### xdm:kanaal {#channel}

>[!NOTE]
>
>Dit veld is alleen verplicht bij gebruik van Attribution AI.

Dit gebied vertegenwoordigt het marketing kanaal met betrekking tot ExperienceEvent. Het veld bevat informatie over het kanaaltype, het mediatype en het locatietype.

![&#x200B; Diagram die de structuur van xdm tonen:kanaalgebied, met inbegrip van subfields zoals type, mediaType, en mediaAction.](./images/data-preparation/channel.png)

**schema van het Voorbeeld**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Voor volledige informatie betreffende elk van de vereiste subfields voor `xdm:channel`, gelieve te verwijzen naar het [&#x200B; schema van het ervaringskanaal &#x200B;](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) specificatie. Voor sommige voorbeeldafbeeldingen, zie de [&#x200B; lijst hieronder &#x200B;](#example-channels).

#### Voorbeeldkanaaltoewijzingen {#example-channels}

In de volgende tabel staan enkele voorbeelden van marketingkanalen die zijn toegewezen aan het schema `xdm:channel` :

| Kanaal | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Betaalde zoekopdracht | https:/<span> /ns.adobe.com/xdm/channel-types/search | betaald | klikken |
| Sociaal - Marketing | https:/<span> /ns.adobe.com/xdm/channel-types/social | verdiend | klikken |
| Weergave | https:/<span> /ns.adobe.com/xdm/channel-types/display | betaald | klikken |
| Email | https:/<span> /ns.adobe.com/xdm/channel-types/email | betaald | klikken |
| Interne referentie | https:/<span> /ns.adobe.com/xdm/channel-types/direct | eigendom | klikken |
| WeergaveThrough weergeven | https:/<span> /ns.adobe.com/xdm/channel-types/display | betaald | indrukken |
| Omleiding QR-code | https:/<span> /ns.adobe.com/xdm/channel-types/direct | eigendom | klikken |
| Mobiel | https:/<span> /ns.adobe.com/xdm/channel-types/mobile | eigendom | klikken |

### Aanbevolen velden

De overige belangrijke velden worden in deze sectie beschreven. Hoewel deze velden niet noodzakelijkerwijs vereist zijn voor [!DNL Intelligent Services] , wordt u ten zeerste aangeraden zoveel mogelijk velden te gebruiken om rijkere inzichten te verkrijgen.

#### xdm:productListItems

Dit veld is een array van items die producten vertegenwoordigen die door een klant zijn geselecteerd, waaronder de SKU, naam, prijs en hoeveelheid van het product.

![&#x200B; xdm:productListItems gebied, met inbegrip van subfields zoals SKU, naam, currencyCode, hoeveelheid, en priceTotal.](./images/data-preparation/productListItems.png)

**schema van het Voorbeeld**

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

Voor volledige informatie betreffende elk van vereiste subfields voor `xdm:productListItems`, gelieve te verwijzen naar het [&#x200B; schema van handelsdetails &#x200B;](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) specificatie.

#### xdm:handel

Dit veld bevat handelspecifieke informatie over de ExperienceEvent, waaronder het inkoopordernummer en betalingsgegevens.

![&#x200B; de structuur van xdm:handelgebied, met inbegrip van subgebieden zoals orde, aankopen, en betalingen.](./images/data-preparation/commerce.png)

**schema van het Voorbeeld**

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

Voor volledige informatie betreffende elk van vereiste subfields voor `xdm:commerce`, gelieve te verwijzen naar het [&#x200B; schema van handelsdetails &#x200B;](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) specificatie.

#### xdm:web

In dit veld worden de webdetails weergegeven die betrekking hebben op de ExperienceEvent, zoals de interactie, paginagegevens en de referentie.

![&#x200B; xdm:Webgebied, met inbegrip van subfields zoals webPageDetails en webReferrer.](./images/data-preparation/web.png)

**schema van het Voorbeeld**

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

Voor volledige informatie betreffende elk van de vereiste subfields voor `xdm:productListItems`, gelieve te verwijzen naar het [&#x200B; ExperienceEvent Web details schema &#x200B;](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) specificatie.

#### xdm:marketing

Dit veld bevat informatie over marketingactiviteiten die actief zijn met het aanraakpunt.

![&#x200B; de structuur van xdm:marketing gebied, met inbegrip van subfields zoals trackingCode, campagneGroup, en campagneName.](./images/data-preparation/marketing.png)

**schema van het Voorbeeld**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Voor volledige informatie betreffende elk van vereiste subfields voor `xdm:productListItems`, gelieve te verwijzen naar [&#x200B; marketing sechma &#x200B;](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) specificatie.

## Gegevens toewijzen en opnemen {#mapping}

Nadat u hebt bepaald of de gegevens van uw marketinggebeurtenissen kunnen worden toegewezen aan het CEE-schema, kunt u nu bepalen in welke gegevens u de gegevens wilt opnemen in [!DNL Intelligent Services] . Alle historische gegevens die in [!DNL Intelligent Services] worden gebruikt, moeten binnen het minimale tijdvenster van vier maanden aan gegevens vallen, plus het aantal dagen dat als terugzoekperiode wordt bedoeld.

Nadat u het gegevensbereik hebt bepaald dat u wilt verzenden, neemt u contact op met Adobe Consulting Services om uw gegevens toe te wijzen aan het schema en deze in te voeren in de service.

Als u een [!DNL Adobe Experience Platform] -abonnement hebt en de gegevens zelf wilt toewijzen en invoeren, volgt u de stappen in de onderstaande sectie.

### Adobe Experience Platform gebruiken

>[!NOTE]
>
>Voor de onderstaande stappen is een abonnement op Experience Platform vereist. Als u geen toegang tot Experience Platform hebt, ga vooruit aan de [&#x200B; volgende stappen &#x200B;](#next-steps) sectie over.

In deze sectie wordt de workflow beschreven voor het toewijzen en invoeren van gegevens in Experience Platform voor gebruik in [!DNL Intelligent Services] , inclusief koppelingen naar zelfstudies voor gedetailleerde stappen.

#### Een CEE-schema en gegevensset maken

Wanneer u klaar bent om uw gegevens voor opname voor te bereiden, moet de eerste stap een nieuw XDM schema tot stand brengen dat de CEE gebiedsgroep aanwendt. De volgende zelfstudies lopen door het proces om een nieuw schema in UI of API tot stand te brengen:

* [Een schema maken in de gebruikersinterface](../xdm/tutorials/create-schema-ui.md)
* [Een schema maken in de API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>De bovenstaande zelfstudies volgen een algemene workflow voor het maken van een schema. Wanneer het kiezen van een klasse voor het schema, moet u de **klasse gebruiken XDM ExperienceEvent**. Zodra deze klasse is gekozen, kunt u de CEE gebiedsgroep aan het schema dan toevoegen.

Nadat u de CEE-veldgroep aan het schema hebt toegevoegd, kunt u desgewenst andere veldgroepen toevoegen voor extra velden in uw gegevens.

Zodra u het schema hebt gecreeerd en bewaard, kunt u een nieuwe dataset tot stand brengen die op dat schema wordt gebaseerd. De volgende zelfstudies lopen door het proces om een nieuwe dataset in UI of API tot stand te brengen:

* [&#x200B; creeer een dataset in UI &#x200B;](../catalog/datasets/user-guide.md#create) (volg het werkschema voor het gebruiken van een bestaand schema)
* [Een gegevensset maken in de API](../catalog/datasets/create.md)

Nadat de dataset is gecreeerd, kunt u het in Experience Platform UI binnen de **[!UICONTROL Datasets]** werkruimte vinden.

![](images/data-preparation/dataset-location.png)

#### Identiteitsvelden toevoegen aan de gegevensset

Als u gegevens van [!DNL Adobe Audience Manager], [!DNL Adobe Analytics], of een andere externe bron inbrengt, dan hebt u de optie om een schemagebied als identiteitsgebied te plaatsen. Om een schemagebied als identiteitsgebied te plaatsen, bekijk de sectie bij het plaatsen van identiteitsgebieden binnen het [&#x200B; leerprogramma UI &#x200B;](../xdm/tutorials/create-schema-ui.md#identity-field) of [&#x200B; API leerprogramma &#x200B;](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) voor het creëren van een schema.

Als u gegevens van een lokaal Csv- dossier opneemt, kunt u vooruit aan de volgende sectie op [&#x200B; afbeelding overslaan en gegevens opnemen &#x200B;](#ingest).

#### Gegevens toewijzen en opnemen {#ingest}

Nadat u een CEE-schema en -gegevensset hebt gemaakt, kunt u uw gegevenstabellen aan het schema toewijzen en die gegevens in Experience Platform invoeren. Zie het leerprogramma op [&#x200B; in kaart brengen een Csv- dossier aan een XDM- schema &#x200B;](../ingestion/tutorials/map-csv/overview.md) voor stappen op hoe te om dit in UI uit te voeren. U kunt het volgende [&#x200B; steekproefJSON- dossier &#x200B;](https://github.com/AdobeDocs/experience-platform.nl-NL/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) gebruiken om het innameproces te testen alvorens uw eigen gegevens te gebruiken.

Zodra een dataset is bevolkt, kan de zelfde dataset worden gebruikt om extra gegevensdossiers in te voeren.

Als uw gegevens in een gesteunde derdetoepassing worden opgeslagen, kunt u ook verkiezen om a [&#x200B; bronschakelaar &#x200B;](../sources/home.md) tot stand te brengen om uw marketing gebeurtenisgegevens in [!DNL Experience Platform] in real time in te nemen.

## Volgende stappen {#next-steps}

Dit document bevat algemene richtlijnen voor het voorbereiden van gegevens voor gebruik in [!DNL Intelligent Services] . Neem contact op met Adobe Consulting Support als je aanvullende consultancy nodig hebt op basis van je gebruikscase.

Zodra u met succes een dataset met uw gegevens van de klantenervaring hebt bevolkt, kunt u [!DNL Intelligent Services] gebruiken om inzichten te produceren. Raadpleeg de volgende documenten om aan de slag te gaan:

* [Overzicht van Attribution AI](./attribution-ai/overview.md)
* [AI-klantoverzicht](./customer-ai/overview.md)
