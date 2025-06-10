---
title: Een Google PubSub Source Connection maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform kunt verbinden met een Google PubSub-account met behulp van de Flow Service API.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 0%

---

# Een [!DNL Google PubSub] Source-verbinding maken met de Flow Service API

>[!IMPORTANT]
>
>De [!DNL Google PubSub] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.

Dit leerprogramma begeleidt u door de stappen om [!DNL Google PubSub] (verder die als &quot; [!DNL PubSub]&quot;worden bedoeld) met Experience Platform te verbinden, gebruikend [[!DNL Flow Service]  API ](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u [!DNL PubSub] met de API van [!DNL Flow Service] kunt verbinden met Experience Platform.

### Vereiste referenties verzamelen

U moet waarden opgeven voor de verbindingseigenschappen die hieronder worden beschreven om uw [!DNL PubSub] -account aan te sluiten op [!DNL Flow Service] . Voor meer informatie over authentificatie en eerste vereiste opstelling, lees het [[!DNL PubSub source]  overzicht ](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).

>[!BEGINTABS]

>[!TAB  op project-gebaseerde authentificatie ]

| Credentials | Beschrijving |
| --- | --- |
| `projectId` | De project-id die is vereist voor verificatie [!DNL PubSub] . |
| `credentials` | De referentie die is vereist voor verificatie [!DNL PubSub]. U moet ervoor zorgen dat u het volledige JSON-bestand plaatst nadat u de witruimten uit uw referenties hebt verwijderd. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en brondoelverbindingen terug. De [!DNL PubSub] -id van de verbindingsspecificatie is: `70116022-a743-464a-bbfe-e226a7f8210c` . |

>[!TAB  Onderwerp en op abonnement-Gebaseerde authentificatie ]

| Credentials | Beschrijving |
| --- | --- |
| `credentials` | De referentie die is vereist voor verificatie [!DNL PubSub]. U moet ervoor zorgen dat u het volledige JSON-bestand plaatst nadat u de witruimten uit uw referenties hebt verwijderd. |
| `topicName` | De naam van de bron die een feed met berichten vertegenwoordigt. U moet een onderwerpnaam specificeren als u toegang tot een specifieke stroom van gegevens in uw [!DNL PubSub] bron wilt verlenen. De indeling van de onderwerpnaam is: `projects/{PROJECT_ID}/topics/{TOPIC_ID}` . |
| `subscriptionName` | De naam van uw [!DNL PubSub] -abonnement. In [!DNL PubSub], staan de abonnementen u toe om berichten te ontvangen, door aan het onderwerp in te tekenen waarin de berichten zijn gepubliceerd aan. **Nota**: Één enkel [!DNL PubSub] abonnement kan slechts voor één dataflow worden gebruikt. Als u meerdere gegevensstromen wilt maken, hebt u meerdere abonnementen nodig. De indeling voor de abonnementsnaam is: `projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}` . |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en brondoelverbindingen terug. De [!DNL PubSub] -id van de verbindingsspecificatie is: `70116022-a743-464a-bbfe-e226a7f8210c` . |

>[!ENDTABS]

Voor meer informatie over deze waarden, lees dit [[!DNL PubSub]  authentificatie ](https://cloud.google.com/pubsub/docs/authentication) document. Om de dienst op rekening-gebaseerde authentificatie te gebruiken, leest deze [[!DNL PubSub]  gids bij het creëren van de dienstrekeningen ](https://cloud.google.com/docs/authentication/production#create_service_account) voor stappen op hoe te om uw geloofsbrieven te produceren.

>[!TIP]
>
>Als u de op rekening-gebaseerde authentificatie van de dienst gebruikt, zorg ervoor dat u voldoende gebruikerstoegang tot uw de dienstrekening hebt verleend en dat er geen extra witte ruimten in JSON zijn, wanneer het kopiëren en het kleven van uw geloofsbrieven.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

>[!TIP]
>
>Nadat u een [!DNL Google PubSub] basisverbinding hebt gemaakt, kunt u het verificatietype niet wijzigen. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.

De eerste stap bij het maken van een bronverbinding is het verifiëren van de [!DNL PubSub] -bron en het genereren van een basis-verbindings-id. Met een basis-verbindings-id kunt u bestanden verkennen en door de bestanden navigeren vanuit de bron en specifieke items identificeren die u wilt invoeren, zoals informatie over de gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL PubSub] -verificatiegegevens op als onderdeel van de aanvraagparameters.

Met de bron [!DNL PubSub] kunt u het type toegang opgeven dat u wilt toestaan tijdens verificatie. U kunt uw account zo instellen dat deze toegang tot een bepaald onderwerp en een bepaald abonnement van [!DNL PubSub] heeft of beperkt.

>[!NOTE]
>
>Hoofd (rollen) die aan een [!DNL PubSub] project worden toegewezen worden geërft in alle onderwerpen en abonnementen die binnen een [!DNL PubSub] project worden gecreeerd. Als u een hoofd (rol) toegang tot een specifiek onderwerp wilt hebben, dan moet dat hoofd (rol) ook aan het overeenkomstige abonnement van het onderwerp worden toegevoegd. Voor meer informatie, lees de [[!DNL PubSub]  documentatie over toegangsbeheer ](<https://cloud.google.com/pubsub/docs/access-control>).

**API formaat**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB  op project-gebaseerde authentificatie ]

Als u een basisverbinding wilt maken met verificatie op basis van een project, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de instructies `projectId` en `credentials` op in de aanvraagtekst.

+++verzoek

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Project Based Authentication",
          "params": {
              "projectId": "{PROJECT_ID}",
              "credentials": "{CREDENTIALS}"
          }
      },
      "connectionSpec": {
          "id": "70116022-a743-464a-bbfe-e226a7f8210c",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.projectId` | De project-id die is vereist voor verificatie [!DNL PubSub] . |
| `auth.params.credentials` | De referentie of sleutel die is vereist voor verificatie [!DNL PubSub]. |
| `connectionSpec.id` | De [!DNL PubSub] connection spec ID: `70116022-a743-464a-bbfe-e226a7f8210c` . |

++++

+++Response

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze basis verbindings identiteitskaart wordt vereist in de volgende stap om een bronverbinding tot stand te brengen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!TAB  Onderwerp en op abonnement-Gebaseerde authentificatie ]

Als u een basisverbinding met een onderwerp en verificatie op basis van een abonnement wilt maken, dient u een POST-aanvraag in bij het eindpunt van `/connections` en geeft u `credentials` , `topicName` en `subscriptionName` op in de aanvraagtekst.

+++verzoek

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google PubSub connection",
      "description": "Google PubSub connection",
      "auth": {
          "specName": "Topic & Subscription Based Authentication",
          "params": {
              "credentials": "{CREDENTIALS}",
              "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
              "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}"
          }
      },
      "connectionSpec": {
          "id": "70116022-a743-464a-bbfe-e226a7f8210c",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.credentials` | De referentie of sleutel die is vereist voor verificatie [!DNL PubSub]. |
| `auth.params.topicName` | De project identiteitskaart en het paar van onderwerpidentiteitskaart voor de [!DNL PubSub] bron die u toegang tot wilt verlenen. |
| `auth.params.subscriptionName` | De project-id en het paar met abonnement-id voor de [!DNL PubSub] -bron waartoe u toegang wilt verlenen. |
| `connectionSpec.id` | De [!DNL PubSub] connection spec ID: `70116022-a743-464a-bbfe-e226a7f8210c` . |

+++

+++Response

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze basis verbindings identiteitskaart wordt vereist in de volgende stap om een bronverbinding tot stand te brengen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

++++

>[!ENDTABS]


## Een bronverbinding maken {#source}

Een bronverbinding maakt en beheert de verbinding met de externe bron vanwaar gegevens worden ingevoerd. Een bronverbinding bestaat uit informatie zoals gegevensbron, gegevensformaat, en een identiteitskaart van de bronverbinding nodig om een gegevensstroom tot stand te brengen. Een bronverbindingsinstantie is specifiek voor een huurder en organisatie.

Als u een bronverbinding wilt maken, vraagt u een POST-aanvraag naar het `/sourceConnections` -eindpunt van de [!DNL Flow Service] API.

**API formaat**

```http
POST /sourceConnections
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Google PubSub source connection",
      "description": "A source connection for Google PubSub",
      "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
      "connectionSpec": {
          "id": "70116022-a743-464a-bbfe-e226a7f8210c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "topicName": "projects/{PROJECT_ID}/topics/{TOPIC_ID}",
          "subscriptionName": "projects/{PROJECT_ID}/subscriptions/{SUBSCRIPTION_ID}",
          "dataType": "raw"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de bronverbinding. Zorg ervoor dat de naam van uw bronverbinding beschrijvend is aangezien u dit kunt gebruiken om informatie over uw bronverbinding op te zoeken. |
| `description` | Een optionele waarde die u kunt opgeven voor meer informatie over uw bronverbinding. |
| `baseConnectionId` | De basis verbindings-id van de [!DNL PubSub] -bron die in de vorige stap is gegenereerd. |
| `connectionSpec.id` | The fixed connection specification ID for [!DNL PubSub]. Deze id is: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | De indeling van de [!DNL PubSub] -gegevens die u wilt invoeren. Momenteel is de enige ondersteunde gegevensindeling `json` . |
| `params.topicName` | De naam van het [!DNL PubSub] -onderwerp. In [!DNL PubSub] is een onderwerp een benoemde bron die een feed met berichten vertegenwoordigt. |
| `params.subscriptionName` | De abonnementsnaam die met een bepaald onderwerp beantwoordt. In [!DNL PubSub] kunt u met abonnementen berichten lezen van een onderwerp. Één of vele abonnementen kunnen aan één enkel onderwerp worden toegewezen. |
| `params.dataType` | Deze parameter bepaalt het type van de gegevens die worden opgenomen. Tot de ondersteunde gegevenstypen behoren: `raw` en `xdm` . |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde bronverbinding terug. Deze id is vereist in de volgende zelfstudie om een gegevensstroom te maken.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

>[!NOTE]
>
>Nadat u een streaming gegevensstroom hebt gemaakt of bijgewerkt, moet u de gegevensinvoer kort na vijf minuten pauzeren om te voorkomen dat gegevens verloren gaan of dat gegevens verloren gaan.

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL PubSub] -bronverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze bron verbindingsidentiteitskaart in het volgende leerprogramma gebruiken om [ een het stromen dataflow tot stand te brengen gebruikend  [!DNL Flow Service]  API ](../../collect/streaming.md).
