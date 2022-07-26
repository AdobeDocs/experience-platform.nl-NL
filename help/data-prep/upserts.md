---
keywords: Experience Platform;home;populaire onderwerpen;voorvoegsel van gegevens;Prep;streaming;upsert;streaming upsert
title: Gedeeltelijke rijupdates naar profielservice verzenden met Data Prep
description: Dit document bevat informatie over het verzenden van gedeeltelijke rijupdates naar de profielservice met behulp van Data Prep.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: cc3ecbd8544839246d54f72b894ad27e850c0c90
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# Gedeeltelijke rijupdates verzenden naar [!DNL Profile Service] gebruiken [!DNL Data Prep]

Streaming updates in [!DNL Data Prep] staat u toe om gedeeltelijke rijupdates te verzenden naar [!DNL Profile Service] gegevens te maken en nieuwe identiteitskoppelingen te maken met één API-aanvraag.

Door upserts te streamen, kunt u het formaat van uw gegevens behouden terwijl het omzetten van die gegevens in [!DNL Profile Service] PATCH vraagt tijdens inname. Gebaseerd op de input u verstrekt, [!DNL Data Prep] kunt u één API-lading verzenden en de gegevens omzetten naar beide [!DNL Profile Service] PATCH en [!DNL Identity Service] CREEER verzoeken.

Dit document bevat informatie over hoe upserts kunnen worden gestreamd in [!DNL Data Prep].

## Aan de slag

Voor dit overzicht is een goed begrip van de volgende Adobe Experience Platform-componenten vereist:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).
* [[!DNL Identity Service]](../identity-service/home.md): Verbeter een beter beeld van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
* [Klantprofiel in realtime](../profile/home.md): Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Bronnen](../sources/home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.

## Streaming updates gebruiken in [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>De volgende bronnen ondersteunen het gebruik van streaming upserts:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Streaming zorgt voor een workflow op hoog niveau

Streaming updates in [!DNL Data Prep] werkt als volgt:

* U moet eerst een dataset creëren en toelaten voor [!DNL Profile] verbruik. Zie de handleiding op [het toelaten van een dataset voor [!DNL Profile]](../catalog/datasets/enable-for-profile.md) voor meer informatie;
* Als nieuwe identiteiten moeten worden verbonden, dan moet u ook een extra dataset creëren **met hetzelfde schema** als uw [!DNL Profile] gegevensset;
* Zodra uw dataset(s) worden voorbereid, moet u een dataflow creëren om uw inkomende verzoek aan in kaart te brengen [!DNL Profile] gegevensset;
* Vervolgens moet u de binnenkomende aanvraag bijwerken om de benodigde koppen op te nemen. Deze kopteksten definiëren:
   * De gegevensbewerking die moet worden uitgevoerd met [!DNL Profile]: `create`, `merge`, en `delete`;
   * De optionele identiteitsbewerking die moet worden uitgevoerd met [!DNL Identity Service]: `create`.

### De identiteitsgegevensset configureren

Als nieuwe identiteiten moeten worden verbonden, dan moet u een extra dataset in de inkomende lading creëren en overgaan. Wanneer het creëren van een identiteitsdataset, moet u ervoor zorgen dat aan de volgende vereisten wordt voldaan:

* De identiteitsdataset moet zijn bijbehorend schema als hebben [!DNL Profile] dataset. Een afwijking van de schema&#39;s kan leiden tot inconsequent systeemgedrag;
* Nochtans, moet u ervoor zorgen dat de identiteitsdataset van verschillend is [!DNL Profile] dataset. Als de datasets het zelfde zijn, dan zullen de gegevens in plaats van bijgewerkt worden beschreven;
* Terwijl de aanvankelijke dataset moet worden toegelaten voor [!DNL Profile], de identiteitsgegevens **mogen** worden ingeschakeld voor [!DNL Profile]. Anders worden gegevens ook overschreven in plaats van bijgewerkt.

#### Vereiste gebieden in de schema&#39;s verbonden aan de identiteitsdataset {#identity-dataset-required-fileds}

Als uw schema vereiste gebieden bevat, moet de bevestiging van de dataset worden onderdrukt om toe te laten [!DNL Identity Service] alleen de identiteiten te ontvangen. U kunt validatie onderdrukken door het toepassen van de `disabled` aan de `acp_validationContext` parameter. Zie het onderstaande voorbeeld:

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags":{
        "acp_validationContext": ["disabled"]
        }
}'
```

>[!TIP]
>
>U te hoeven om geen extra configuratie te doen als het schema verbonden aan de identiteitsdataset geen vereiste gebieden heeft.

## Binnenkomende payload-structuur

In het volgende voorbeeld ziet u een voorbeeld van een inkomende ladingsstructuur die nieuwe identiteitskoppelingen tot stand brengt.

### Payload met identiteitsconfiguratie

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create" (default)/"merge"/"delete",
        "identity": "create",
        "identityDatasetId": "621fc19ab33d941949af16d9"
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

| Parameter | Beschrijving |
| --- | --- |
| `flowId` | Een unieke id om een gegevensstroom te identificeren. Deze gegevensstroom-id moet overeenkomen met de bronverbinding die is gemaakt met [!DNL Amazon Kinesis], [!DNL Azure Event Hubs], of [!DNL HTTP API]. Deze gegevensstroom moet ook een [!DNL Profile]- toegelaten dataset als doel dataset. **Opmerking**: De id van de [!DNL Profile]-enabled doeldataset wordt ook gebruikt als uw `datasetId` parameter. |
| `imsOrgId` | De id die overeenkomt met uw organisatie. |
| `datasetId` | De id van de [!DNL Profile]- toegelaten doeldataset van uw dataflow. **Opmerking**: Dit is dezelfde id als de [!DNL Profile]- toegelaten identiteitskaart van de doeldataset die in uw gegevensstroom wordt gevonden. |
| `operations` | Deze parameter beschrijft de acties die [!DNL Data Prep] wordt gebaseerd op de binnenkomende aanvraag. |
| `operations.data` | Definieert de handelingen die moeten worden uitgevoerd in [!DNL Profile Service]. |
| `operations.identity` | Definieert de bewerkingen die op de gegevens zijn toegestaan door [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Optioneel) De id van het identiteitsgegevensbestand dat alleen vereist is als nieuwe identiteiten moeten worden gekoppeld. |

#### Ondersteunde bewerkingen

De volgende bewerkingen worden ondersteund door [!DNL Profile Service]:

| Bewerkingen | Beschrijving |
| --- | --- | 
| `create` | De standaardbewerking. Dit produceert een entiteit XDM creeert methode voor [!DNL Profile Service]. |
| `merge` | Hiermee wordt een updatemethode voor XDM-entiteiten gegenereerd [!DNL Profile Service]. |
| `delete` | Dit produceert een XDM entiteit schrappingsmethode voor [!DNL Profile Service] en verwijdert de gegevens permanent uit de [!DNL Profile Store]. |

De volgende bewerkingen worden ondersteund door [!DNL Identity Service]:

| Bewerkingen | Beschrijvingen |
| --- | --- |
| `create` | De enige toegestane bewerking voor deze parameter. Indien `create` wordt doorgegeven als waarde voor `operations.identity`vervolgens [!DNL Data Prep] genereert een XDM-entiteit die een aanvraag maakt voor [!DNL Identity Service]. Als de identiteit al bestaat, wordt de identiteit genegeerd. **Opmerking:** Indien `operations.identity` is ingesteld op `create`en de `identityDatasetId` moet ook worden gespecificeerd. De XDM-entiteit maakt een bericht dat intern wordt gegenereerd door [!DNL Data Prep] wordt voor deze id van de gegevensset gegenereerd. |

### Payload zonder identiteitsconfiguratie

Als nieuwe identiteiten niet hoeven te worden gekoppeld, kunt u de eigenschap `identity` en `identityDatasetId` parameters in de bewerkingen. Hiermee verzendt u gegevens alleen naar [!DNL Profile Service] en slaat de [!DNL Identity Service]. Zie de lading hieronder voor een voorbeeld:

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create"/"merge"/"delete",
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

## Primaire identiteiten dynamisch doorgeven

Voor XDM-updates moet het schema zijn ingeschakeld voor [!DNL Profile] en bevatten een primaire identiteit. U kunt de primaire identiteit van een XDM-schema op twee manieren specificeren:

* Wijs een statisch gebied als primaire identiteit in het schema XDM aan;
* Wijs één van de identiteitsgebieden als primaire identiteit door de het gebiedsgroep van de identiteitskaart in het XDM schema aan.

### Een statisch veld aanwijzen als primair identiteitsveld in het XDM-schema

In het onderstaande voorbeeld: `state`, `homePhone.number` en andere eigenschappen worden met de respectieve gegeven waarden in de [!DNL Profile] met de primaire identiteit van `sampleEmail@gmail.com`. Vervolgens wordt een updatebericht voor een XDM-entiteit gegenereerd door streaming [!DNL Data Prep] component. [!DNL Profile Service] bevestigt dan dat XDM updatebericht om het profielverslag op te nemen.

>[!NOTE]
>
>In dit voorbeeld worden identiteiten niet aan elkaar gekoppeld, omdat er geen bewerkingen voor identiteit zijn gedefinieerd.

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {
         "data": "create"
     }
    },
    {
        "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
}'
```

### Wijs één van de identiteitsgebieden als primaire identiteit door de het gebiedsgroep van het identiteitskaartgebied in het XDM schema aan

In dit voorbeeld bevat de header de `operations` kenmerk met de `identity` en `identityDatasetId` eigenschappen. Hierdoor kunnen gegevens worden samengevoegd met [!DNL Profile Service] en ook voor het doorgeven van identiteit aan [!DNL Identity Service].

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {          
            "data": "merge",
            "identity": "create",
            "identityDatasetId": "6254a93b851ecd194b64af9e"
      }
    },
    {        
       "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
 }'
```

## Bekende beperkingen en belangrijke overwegingen

In het volgende voorbeeld wordt een lijst met bekende beperkingen beschreven die in acht moeten worden genomen bij het streamen van updates met [!DNL Data Prep]:

* De streaming upserts methode zou slechts moeten worden gebruikt wanneer het verzenden van gedeeltelijke rijupdates naar [!DNL Profile Service]. Gedeeltelijke rij-updates zijn **niet** verbruikt door data Lake.
* De streaming upserts-methode ondersteunt het bijwerken, vervangen en verwijderen van identiteiten niet. Er worden nieuwe identiteiten gemaakt als deze niet bestaan. Daarom `identity` bewerking moet altijd zijn ingesteld op maken. Als er al een identiteit bestaat, is de bewerking een no-op.
* De streaming upserts-methode ondersteunt momenteel alleen primitieve attributen met één waarde (zoals gehele getallen, datums, tijdstempels en tekenreeksen) en objecten.
* De streaming upserts-methode ondersteunt momenteel niet [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=en) en [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/).

## Volgende stappen

Door dit document te lezen, moet u nu begrijpen hoe u upserts kunt streamen in [!DNL Data Prep] om gedeeltelijke rijupdates naar uw te verzenden [!DNL Profile Service] gegevens, maar ook identiteiten maken en koppelen met één API-aanvraag. Voor meer informatie over andere [!DNL Data Prep] functies, lees de [[!DNL Data Prep] overzicht](./home.md). Leer hoe u toewijzingssets kunt gebruiken in het dialoogvenster [!DNL Data Prep] API, lees de [[!DNL Data Prep] ontwikkelaarsgids](./api/overview.md).
