---
title: API-eindpunt voor publiek maken
description: Leer hoe u de metagegevens voor een extern publiek maakt met de API.
hide: true
hidefromtoc: true
exl-id: e841a5f6-f406-4e1d-9e8a-acb861ba6587
source-git-commit: ea7fd13675a95941be7267f1cf75056b224efcd3
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---

# Het eindpunt voor het publiek maken

Het POST `/audiences` eindpunt kan worden gebruikt creeert de meta-gegevens voor een extern publiek, dat het publiek in de Portaal van de Publiek zichtbaar laat zijn. U zou dit eindpunt moeten gebruiken als de publieksinname in de afzonderlijke dienst, zoals partijingestie zal worden beheerd.

## Aan de slag

>[!IMPORTANT]
>
>De eindpunten in deze handleiding worden voorafgegaan door `/core/ais` , in tegenstelling tot `/core/ups` .

om Experience Platform APIs te gebruiken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) hebben voltooid. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in Experience Platform API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie bij het werken met zandbakken in [!DNL Experience Platform], zie de [ documentatie van het zandbakenoverzicht ](../../sandboxes/home.md).

**API formaat**

>[!IMPORTANT]
>
>U **moet** de `createAudienceMetaOnly=true` vraagparameter als deel van het verzoek omvatten.

```http
POST /audiences?createAudienceMetaOnly=true
```

**Verzoek**

>[!IMPORTANT]
>
>U **moet** de `Accept: application/vnd.adobe.external.audiences+json; version=2` kopbal als deel van het API verzoek omvatten.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/audiences?createAudienceMetaOnly=true \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'\
 -H 'Accept: application/vnd.adobe.external.audiences+json; version=2'
 -d '{
    "name": "Sample audience name",
    "description": "A sample description for the audience.",
    "audienceId": "4a815904-f2f9-4237-82fb-55605bcc2ad7",
    "namespace": "agora",
    "originName": "Agora_Collaboration"
 }'
```

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| `name` | String | De naam voor het publiek. |
| `description` | String | Een optionele beschrijving voor het publiek. |
| `audienceId` | String | Een extern gegenereerde id voor het publiek. |
| `namespace` | String | De naamruimte voor het publiek. |
| `originName` | String | De naam van de oorsprong van het publiek. |

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met informatie over het pas gecreëerde publiek terug.

```json
{
    "id": "6bb1ee15-8f64-49fd-bce3-d5c2f22f1f14",
    "name": "Sample audience name",
    "audienceId": "4a815904-f2f9-4237-82fb-55605bcc2ad7"
}
```

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| `id` | String | Het systeem produceerde identiteitskaart voor het publiek. |
| `name` | String | De naam van het publiek dat u hebt gemaakt. |
| `audienceId` | String | De extern opgegeven id van het publiek dat u hebt gemaakt. |
