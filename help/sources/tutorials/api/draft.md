---
keywords: Experience Platform;thuis;populaire onderwerpen;de stroomdienst;
title: Conceptgegevensstromen met behulp van de Flow Service API
description: Leer hoe u uw gegevensstromen in een ontwerpstaat plaatst gebruikend de Dienst API van de Stroom.
badge: label="New Feature" type="Positive"
source-git-commit: d093e34ae4b353d1ed6db922b6da66cf23f25c48
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# Conceptgegevensstromen met behulp van de Flow Service API

Sla uw gegevensstromen op als concepten wanneer u de Flow Service API gebruikt door de `mode=draft` de vraagparameter tijdens de vraag van de stroomverwezenlijking. Concepten kunnen later met nieuwe informatie worden bijgewerkt en vervolgens worden gepubliceerd zodra ze gereed zijn. In deze zelfstudie worden de stappen beschreven waarmee u uw gegevens in een conceptstatus instelt met behulp van de Flow Service API.

## Aan de slag

Voor deze zelfstudie hebt u een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Vereisten

Deze zelfstudie vereist dat u al de benodigde middelen hebt gegenereerd om een gegevensstroom te maken. Dit omvat het volgende:

* Een geverifieerde basisverbinding
* Een bronverbinding
* Een doel-XDM-schema
* Een doelgegevensset
* Een doelverbinding
* Een toewijzing

Als u deze waarden nog niet hebt, selecteert u een bron uit [de catalogus in het overzicht van de bronnen](../../home.md). Volg vervolgens de instructies van die bron om de benodigde elementen te genereren voor het samenstellen van een gegevensstroom.

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../landing/api-guide.md).

## Een gegevensstroom instellen op een concept-status

In de volgende secties wordt een overzicht gegeven van het proces om een gegevensstroom in te stellen als concept, de gegevensstroom bij te werken, de gegevensstroom te publiceren en uiteindelijk de gegevensstroom te verwijderen.

### Concepten van gegevensstroom

Als u een gegevensstroom wilt instellen als concept, vraagt u een POST naar de `/flows` eindpunt terwijl het toevoegen van `mode=draft` als een queryparameter. Op deze manier kunt u een gegevensstroom maken en deze opslaan als concept.

**API-indeling**

```http
POST /flows?mode=draft
```

| Parameter | Beschrijving |
| --- | --- |
| `mode` | Een door de gebruiker opgegeven queryparameter die de status van de gegevensstroom bepaalt. Als u een gegevensstroom wilt instellen als concept, stelt u `mode` tot `draft`. |

**Verzoek**

Met het volgende verzoek wordt een concept-gegevensstroom gemaakt.

```shell
  'https://platform-int.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "HTTP source dataflow for ACME data",
    "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
    ],
    "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
    ],
    "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
    }
  }'
```

**Antwoord**

Als de reactie succesvol was, worden de `id` en de overeenkomstige `etag` van uw gegevensstroom.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Een gegevensstroom bijwerken

Als u uw concept wilt bijwerken, vraagt u de PATCH aan `/flows` eindpunt terwijl het verstrekken van identiteitskaart van dataflow die u wilt bijwerken. Tijdens deze stap moet u ook een `If-Match` header parameter, die overeenkomt met de `etag` van de gegevensstroom die u wilt bijwerken.

**API-indeling**

```http
PATCH /flows/{FLOW_ID}
```

**Verzoek**

Met de volgende verzoeken voegt u toewijzingstransformaties toe aan de opgestelde gegevensstroom.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "69057131-0000-0200-0000-640f48320000"' \
  -d '[
        {
          "op": "add",
          "path": "/transformations",
          "value": [
              {
                  "name": "Mapping",
                  "params": {
                      "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
                      "mappingVersion": 0
                  }
              }
          ]
      }
  ]'
```

**Antwoord**

Een geslaagde reactie retourneert uw flow-id en `etag`. Om de wijziging te verifiëren, kunt u een verzoek van de GET indienen aan `/flows` eindpunt terwijl het verstrekken van uw stroom ID.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Een gegevensstroom publiceren

Wanneer uw concept klaar is om te worden gepubliceerd, kunt u de POST `/flows` eindpunt terwijl het verstrekken van identiteitskaart van het ontwerp dataflow die u wilt publiceren, evenals een actieverrichting voor het publiceren.

**API-indeling**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parameter | Beschrijving |
| --- | --- |
| `op` | Een handelingsverrichting die de staat van de gevraagde dataflow bijwerkt. Als u een conceptgegevensstroom wilt publiceren, stelt u `op` tot `publish`. |

**Verzoek**

Met het volgende verzoek wordt uw conceptgegevensstroom gepubliceerd.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een geslaagde reactie retourneert de id en de bijbehorende `etag` van uw gegevensstroom.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Een gegevensstroom verwijderen

Als u de gegevensstroom wilt verwijderen, vraagt u de DELETE aan `/flows` eindpunt terwijl het verstrekken van identiteitskaart van dataflow die u wilt schrappen. Voor gedetailleerde stappen over hoe te om een gegevensstroom te schrappen gebruikend de Dienst API van de Stroom, lees de gids op [verwijderen, een gegevensstroom in de API](./delete-dataflows.md).