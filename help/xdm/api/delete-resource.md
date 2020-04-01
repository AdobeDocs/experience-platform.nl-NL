---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een bron verwijderen
topic: developer guide
translation-type: tm+mt
source-git-commit: d9ab2b1226b051be43f8fc0dd222bc075caed6f0

---


# Een bron verwijderen

Het kan soms noodzakelijk zijn om (DELETE) een middel uit de Registratie van het Schema te verwijderen. Slechts kunnen de middelen die u in de huurderscontainer creeert worden geschrapt. Dit wordt gedaan door een verzoek van de SCHRAPPING uit te voeren gebruikend de bron `$id` u wenst om te schrappen.

**API-indeling**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beschrijving |
| --- | --- |
| `{RESOURCE_TYPE}` | Het type resource dat uit de Schemabibliotheek moet worden verwijderd. Geldige typen zijn `datatypes`, `mixins`, `schemas`en `classes`. |
| `{RESOURCE_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van de bron. |

**Verzoek**

Voor verzoeken VERWIJDEREN zijn geen headers voor accepteren vereist.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fmixins%2F4fbd5368aa67f0e74d5838f67694c867 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de schrapping bevestigen door een raadpleging (GET) verzoek aan het middel te proberen. U zult een Accept- kopbal in het verzoek moeten omvatten, maar zou een status 404 van HTTP (niet Gevonden) moeten ontvangen omdat het middel uit de Registratie van het Schema is verwijderd.