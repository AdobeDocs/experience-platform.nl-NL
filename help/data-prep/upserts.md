---
keywords: Experience Platform;home;populaire onderwerpen;voorvoegsel van gegevens;Prep;streaming;upsert;streaming upsert
title: Gedeeltelijke rijupdates naar realtime klantprofiel verzenden met Data Prep
description: Leer hoe u updates van gedeeltelijke rijen naar Real-Time klantprofiel verzendt met Data Prep.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 0%

---

# gedeeltelijke rijupdates verzenden naar [!DNL Real-Time Customer Profile] met [!DNL Data Prep]

>[!IMPORTANT]
>
>* De berichten van de Update van de Entiteit van het Model van de Gegevens van de Ervaring (XDM) (met verrichtingen JSON PATCH) voor de updates van het Profiel via de inlaat DCS zijn verouderd. Volg de stappen in deze handleiding als alternatief.
>
>* U kunt de bron van HTTP ook gebruiken API aan [&#x200B; binnengaan ruwe gegevens in de inlaat DCS &#x200B;](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection) en de noodzakelijke gegevenstoewijzingen specificeren om uw gegevens in XDM-Volgzame berichten voor de updates van het Profiel om te zetten.
>
>* Wanneer u arrays gebruikt in streaming upserts, moet u expliciet `upsert_array_append` of `upsert_array_replace` gebruiken om een duidelijke intentie van de bewerking te definiëren. Er kunnen fouten optreden als deze functies ontbreken.

Gebruik streaming upserts in [!DNL Data Prep] om gedeeltelijke rij-updates naar [!DNL Real-Time Customer Profile] -gegevens te verzenden en tegelijkertijd nieuwe identiteitskoppelingen te maken en tot stand te brengen met één API-aanvraag.

Door upserts te streamen, kunt u het formaat van uw gegevens behouden terwijl het omzetten van die gegevens in [!DNL Real-Time Customer Profile] PATCH verzoeken tijdens opname. Met [!DNL Data Prep] kunt u op basis van de ingevoerde gegevens één API-lading verzenden en de gegevens omzetten naar zowel [!DNL Real-Time Customer Profile] PATCH- als [!DNL Identity Service] CREATE-aanvragen.

[!DNL Data Prep] gebruikt headerparameters om onderscheid te maken tussen invoegen en invoegen. Alle rijen die upserts gebruiken, moeten een kopbal hebben. U kunt updates met of zonder identiteitsbeschrijvingen gebruiken. Als u updates met identiteiten gebruikt, moet u de configuratiestappen volgen die in de sectie op [&#x200B; worden geschetst vormend de identiteitsdataset &#x200B;](#configure-the-identity-dataset). Als u updates zonder identiteiten gebruikt, dan te hoeven u niet om identiteitsconfiguraties in uw verzoek te verstrekken. Lees de sectie over [&#x200B; het stromen upserts zonder identiteiten &#x200B;](#payload-without-identity-configuration) voor meer informatie.

>[!NOTE]
>
>Aan hefboomwerking upsert functionaliteit, wordt het geadviseerd dat u XDM-compatibele configuraties tijdens gegevensopname uitzet en de inkomende nuttige lading opnieuw in kaart brengt gebruikend [&#x200B; Prep Mapper van Gegevens &#x200B;](./ui/mapping.md).

Dit document bevat informatie over het streamen van upserts in [!DNL Data Prep] .

## Aan de slag

Voor dit overzicht is een goed begrip van de volgende Adobe Experience Platform-componenten vereist:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] stelt gegevensengineers in staat gegevens toe te wijzen, te transformeren en te valideren van en naar het XDM-model (Experience Data Model).
* [[!DNL Identity Service]](../identity-service/home.md): verbeter een beter beeld van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
* [&#x200B; Real-Time Profiel van de Klant &#x200B;](../profile/home.md): Verstrekt een verenigd, klantenprofiel in real time gebaseerd op samengevoegde gegevens van veelvoudige bronnen.
* [&#x200B; Bronnen &#x200B;](../sources/home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.

## Streaming upserts gebruiken in [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>De volgende bronnen ondersteunen het gebruik van streaming upserts:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Streaming zorgt voor een workflow op hoog niveau

Streaming upserts in [!DNL Data Prep] werken als volgt:

* U moet eerst een dataset voor [!DNL Profile] consumptie creëren en toelaten. Zie de gids op [&#x200B; toelatend een dataset voor  [!DNL Profile]](../catalog/datasets/enable-for-profile.md) voor meer informatie.
* Als de nieuwe identiteiten moeten worden verbonden, dan moet u een extra dataset **met het zelfde schema** ook tot stand brengen zoals uw [!DNL Profile] dataset.
* Zodra uw dataset(s) worden voorbereid, moet u een dataflow creëren om uw inkomende verzoek aan de [!DNL Profile] dataset in kaart te brengen;
* Vervolgens moet u de binnenkomende aanvraag bijwerken om de benodigde koppen op te nemen. Deze kopteksten definiëren:
   * De gegevensbewerking die moet worden uitgevoerd met [!DNL Profile] : `create` , `merge` en `delete` .
   * De optionele identiteitsbewerking die moet worden uitgevoerd met [!DNL Identity Service]: `create` .

### De identiteitsgegevensset configureren {#configure-the-identity-dataset}

Als nieuwe identiteiten moeten worden verbonden, dan moet u een extra dataset in de inkomende lading creëren en overgaan. Wanneer het creëren van een identiteitsdataset, moet u ervoor zorgen dat aan de volgende vereisten wordt voldaan:

* De identiteitsdataset moet zijn bijbehorend schema als [!DNL Profile] dataset hebben. Een afwijking van schema&#39;s kan tot inconsistent systeemgedrag leiden.
* U moet er echter voor zorgen dat de identiteitsgegevensset anders is dan de gegevensset [!DNL Profile] . Als de datasets het zelfde zijn, dan zullen de gegevens in plaats van bijgewerkt worden beschreven.
* Terwijl de aanvankelijke dataset voor [!DNL Profile] moet worden toegelaten, zou de identiteitsdataset **niet** voor [!DNL Profile] moeten worden toegelaten. Anders worden gegevens ook overschreven in plaats van bijgewerkt. Nochtans, zou de identiteitsdataset **&#x200B;**&#x200B;voor [!DNL Identity Service] moeten worden toegelaten.

#### Vereiste gebieden in de schema&#39;s verbonden aan de identiteitsdataset {#identity-dataset-required-fileds}

Als uw schema vereiste gebieden bevat, moet de bevestiging van de dataset worden onderdrukt om [!DNL Identity Service] toe te laten om slechts de identiteiten te ontvangen. U kunt de validatie onderdrukken door de waarde `disabled` toe te passen op de parameter `acp_validationContext` . Zie het onderstaande voorbeeld:

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags": {
        "acp_validationContext": [
            "disabled"
        ],
        "unifiedProfile": [
            "enabled:false"
        ],
        "unifiedIdentity": [
            "enabled:true"
        ]
    }
}'
```

>[!TIP]
>
>U te hoeven om geen extra configuratie te doen als het schema verbonden aan de identiteitsdataset geen vereiste gebieden heeft.

## Binnenkomende laadstructuur

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
| `flowId` | Een unieke id om een gegevensstroom te identificeren. Deze gegevensstroom-id moet overeenkomen met de bronverbinding die is gemaakt met [!DNL Amazon Kinesis] , [!DNL Azure Event Hubs] of [!DNL HTTP API] . Deze gegevensstroom zou ook een [!DNL Profile]-Toegelaten dataset als doeldataset moeten hebben. **Nota**: identiteitskaart van [!DNL Profile] - toegelaten doeldataset wordt ook gebruikt als uw `datasetId` parameter. |
| `imsOrgId` | De id die overeenkomt met uw organisatie. |
| `datasetId` | De id van de [!DNL Profile] -ingeschakelde doeldataset van uw gegevensstroom. **Nota**: Dit is zelfde identiteitskaart zoals [!DNL Profile] - toegelaten identiteitskaart van de doeldataset die in uw dataflow wordt gevonden. |
| `operations` | Deze parameter schetst de acties die [!DNL Data Prep] zal nemen gebaseerd op het inkomende verzoek. |
| `operations.data` | Definieert de handelingen die moeten worden uitgevoerd in [!DNL Real-Time Customer Profile] . |
| `operations.identity` | Definieert de bewerkingen die op de gegevens zijn toegestaan door [!DNL Identity Service] . |
| `operations.identityDatasetId` | (Optioneel) De id van het identiteitsgegevensbestand dat alleen vereist is als nieuwe identiteiten moeten worden gekoppeld. |

#### Ondersteunde bewerkingen

De volgende bewerkingen worden ondersteund door [!DNL Real-Time Customer Profile] :

| Bewerkingen | Beschrijving |
| --- | --- | 
| `create` | De standaardbewerking. Hierdoor wordt een methode gemaakt voor het maken van een XDM-entiteit voor [!DNL Real-Time Customer Profile] . |
| `merge` | Hiermee wordt een methode voor het bijwerken van XDM-entiteiten voor [!DNL Real-Time Customer Profile] gegenereerd. |
| `delete` | Hierdoor wordt een methode voor het verwijderen van XDM-entiteiten voor [!DNL Real-Time Customer Profile] gegenereerd en worden de gegevens permanent uit [!DNL Profile store] verwijderd. |

De volgende bewerkingen worden ondersteund door [!DNL Identity Service] :

| Bewerkingen | Beschrijvingen |
| --- | --- |
| `create` | De enige toegestane bewerking voor deze parameter. Als `create` wordt doorgegeven als een waarde voor `operations.identity` , genereert [!DNL Data Prep] een XDM-entiteit die een aanvraag voor [!DNL Identity Service] maakt. Als de identiteit al bestaat, wordt de identiteit genegeerd. **Nota:** als `operations.identity` aan `create` wordt geplaatst, dan moet `identityDatasetId` ook worden gespecificeerd. De XDM-entiteit maakt een bericht dat intern wordt gegenereerd door de component [!DNL Data Prep] , wordt voor deze id van de gegevensset gegenereerd. |

### Payload zonder identiteitsconfiguratie {#payload-without-identity-configuration}

Als nieuwe identiteiten niet hoeven te worden gekoppeld, kunt u de parameters `identity` en `identityDatasetId` weglaten in de bewerkingen. Als u dit doet, worden alleen gegevens verzonden naar [!DNL Real-Time Customer Profile] en wordt de [!DNL Identity Service] overgeslagen. Zie de lading hieronder voor een voorbeeld:

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

Voor XDM-updates moet het schema zijn ingeschakeld voor [!DNL Profile] en een primaire identiteit bevatten. U kunt de primaire identiteit van een XDM-schema op twee manieren specificeren:

* Wijs een statisch gebied als primaire identiteit in het schema XDM aan;
* Wijs één van de identiteitsgebieden als primaire identiteit door de het gebiedsgroep van de identiteitskaart in het XDM schema aan.

### Een statisch veld aanwijzen als primair identiteitsveld in het XDM-schema

In het onderstaande voorbeeld worden `state` , `homePhone.number` en andere kenmerken met hun respectievelijke opgegeven waarden ingevoegd in de [!DNL Profile] met de primaire identiteit `sampleEmail@gmail.com` . Vervolgens wordt een updatebericht voor een XDM-entiteit gegenereerd door de streamingcomponent [!DNL Data Prep] . [!DNL Real-Time Customer Profile] bevestigt vervolgens dat het XDM-updatebericht het profielrecord moet uploaden.

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

In dit voorbeeld bevat de header het kenmerk `operations` met de eigenschappen `identity` en `identityDatasetId` . Hierdoor kunnen gegevens worden samengevoegd met [!DNL Real-Time Customer Profile] en kunnen ook identiteiten worden doorgegeven aan [!DNL Identity Service] .

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

In het volgende voorbeeld wordt een lijst met bekende beperkingen beschreven die in acht moeten worden genomen bij het streamen van upserts met [!DNL Data Prep] :

* De streaming upserts methode zou slechts moeten worden gebruikt wanneer het verzenden van gedeeltelijke rijupdates naar [!DNL Real-Time Customer Profile]. De gedeeltelijke rijupdates worden **niet** verbruikt door gegevens meer.
* De streaming upserts-methode ondersteunt het bijwerken, vervangen en verwijderen van identiteiten niet. Er worden nieuwe identiteiten gemaakt als deze niet bestaan. Daarom moet de bewerking `identity` altijd zijn ingesteld op maken. Als er al een identiteit bestaat, is de bewerking een no-op.
* De het stromen upserts methode steunt momenteel niet [&#x200B; Adobe Experience Platform Web SDK &#x200B;](/help/web-sdk/home.md) en [&#x200B; Adobe Experience Platform Mobile SDK &#x200B;](https://developer.adobe.com/client-sdks/documentation/).

## Volgende stappen

Door dit document te lezen, moet u nu begrijpen hoe u upserts in [!DNL Data Prep] kunt streamen om gedeeltelijke rijupdates naar uw [!DNL Real-Time Customer Profile] -gegevens te verzenden, terwijl u tegelijkertijd identiteiten maakt en koppelt met één API-aanvraag. Voor meer informatie over andere [!DNL Data Prep] eigenschappen, te lezen gelieve het [[!DNL Data Prep]  overzicht &#x200B;](./home.md). Leer hoe te om kaartreeksen binnen [!DNL Data Prep] API te gebruiken, gelieve de [[!DNL Data Prep]  ontwikkelaarsgids &#x200B;](./api/overview.md) te lezen.
