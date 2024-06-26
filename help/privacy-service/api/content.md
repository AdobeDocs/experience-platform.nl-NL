---
title: API-eindpunt voor inhoud
description: Leer hoe u uw toegangsgegevens kunt ophalen met de Privacy Service-API.
role: Developer
badgePrivateBeta: label="Private Bèta" type="Informative"
exl-id: b3b7ea0f-957d-4e51-bf92-121e9ae795f5
source-git-commit: e3a453ad166fe244b82bd1f90e669579fcf09d17
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Inhoudseindpunt

>[!IMPORTANT]
>
>De `/content` het eindpunt is momenteel in bèta en uw organisatie heeft tot nog toe geen toegang tot het. De functionaliteit en documentatie kunnen worden gewijzigd.

Gebruik de `/content` eindpunt om veilig terug te winnen *toegangsinformatie* (de informatie die een privacyonderwerp terecht kan aanvragen om toegang) voor uw klanten. De download-URL in het antwoord op een `/jobs/{JOB_ID}` Het verzoek van GET verwijst naar een de diensteindpunt van Adobe. U kunt dan een verzoek tot GET indienen aan `/jobs/:JOB_ID/content` om uw klantgegevens in JSON-indeling te retourneren. Deze toegangsmethode voert veelvoudige lagen van authentificatie en toegangsbeheer uit om veiligheid te verbeteren.

Voordat u deze handleiding kunt gebruiken, raadpleegt u de [gids Aan de slag](./getting-started.md) voor informatie over de vereiste authentificatiekoppen die in de voorbeeld API vraag hieronder worden voorgesteld.

>[!TIP]
>
>Als u momenteel niet baanidentiteitskaart voor de toegangsinformatie kent u vereist, doe een vraag aan `/jobs` eindpunt en gebruik extra vraagparameters om de resultaten te filtreren. Een volledige lijst van de beschikbare vraagparameters kan in worden gevonden [eindgebruikershandleiding voor privacytaken](./privacy-jobs.md).

## Taakgegevens over privacy ophalen

Als u informatie wilt ophalen over een specifieke taak, zoals de huidige verwerkingsstatus, neemt u de taak van `jobId` op het pad van een verzoek van de GET aan de `/jobs` eindpunt.

**API-indeling**

```http
GET /jobs/{JOB_ID}
```

**Verzoek**

Met het volgende verzoek worden de gegevens opgehaald van de taak waarvan `jobId` wordt opgegeven in het aanvraagpad.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de opgegeven taak.

>[!NOTE]
>
>De banen van de privacy moeten hebben `complete` status die de `downloadUrl`.

```json
{
    "jobId":"dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5",
    "requestId":"17129380910360540RX-753",
    "userKey":"1234",
    "action":"access",
    "status":"complete",
    "submittedBy":"jsnow@adobe.com",
    "createdDate":"04/12/2024 04:08 PM GMT",
    "lastModifiedDate":"04/12/2024 04:08 PM GMT",
    "userIds":[{
        "namespace":"ECID",
        "value":"1234",
        "type":"standard",
        "namespaceId":4,
        "isDeletedClientSide":false
        }],
    "productResponses":[{
        "product":"Identity",
        "retryCount":0,
        "processedDate":"04/12/2024 04:08 PM GMT",
        "productStatusResponse":{"status":"submitted"
        }}],
    "downloadUrl":"https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5/content",
    "regulation":"gdpr"
}
```

| Eigenschap | Beschrijving |
|----------------------|---------------------------------------------------------------------------------------------------------------|
| `jobId` | Een unieke id voor de privacytaak. |
| `requestId` | Een unieke identificatiecode voor het specifieke verzoek dat aan de Privacy Service wordt gedaan. |
| `userKey` | `userKey` is de `key` waarde die u hebt opgegeven toen u het privacyverzoek hebt verzonden. De `key` waarde is uw kans om een id voor de betrokkene te verstrekken die voor u zinvol is. Het is doorgaans een unieke id die uw systeem heeft gemaakt voor het bijhouden van die gegevens. TIP: Je kunt alle actieve privacytaken aanbieden en je `key` voor elke baan. |
| `action` | Het gevraagde type actie. De toegestane waarden zijn `access` en `delete`. |
| `status` | De huidige status van de privacytaak. |
| `submittedBy` | Het e-mailadres van de persoon die de privacytaak heeft ingediend. |
| `createdDate` | De datum en tijd waarop de privacytaak is gemaakt. |
| `lastModifiedDate` | De datum en tijd waarop de privacytaak voor het laatst is gewijzigd. |
| `userIds` | Een array met gebruikers-id&#39;s en verwante informatie. |
| `userIds.namespace` | De naamruimte die voor de gebruikersnaam wordt gebruikt. |
| `userIds.value` | De werkelijke waarde van de gebruikersidentificatie. |
| `userIds.type` | Het type id (bijvoorbeeld `standard` of `custom`). |
| `userIds.namespaceId` | Een id voor de naamruimte die wordt gebruikt om gebruikersidentiteiten te categoriseren en te beheren. |
| `userIds.isDeletedClientSide` | Een Booleaanse waarde die aangeeft of de id aan de clientzijde is verwijderd. |
| `productResponses` | Een array met reacties van verschillende producten of services met betrekking tot de privacytaak. |
| `productResponses.product` | De naam van het product of de dienst die is gebruikt om informatie over de betrokkene te verkrijgen. |
| `productResponses.retryCount` | Het aantal keren dat de aanvraag opnieuw is geprobeerd. |
| `productResponses.processedDate` | De datum en het tijdstip waarop de reactie van het product is verwerkt. |
| `productResponses.productStatusResponse` | Een object dat de status van de reactie van het product bevat. |
| `productResponses.productStatusResponse.status` | De status van de respons van het product. |
| `downloadURL` | Deze eigenschap verstrekt een eindpunt, dat beschikbaar is om 60 dagen te roepen nadat de baan voltooit. De status van de baan moet `complete` en de `action` moet `access`. Anders is dit veld niet aanwezig. |
| `regulation` | Het regelgevingskader waaronder het privacyverzoek wordt verwerkt, zoals `gdpr`, `ccpa`, `lgpd_bra`, `pdpa_tha`, enzovoort. |

{style="table-layout:auto"}

## De informatie van de klantentoegang terugwinnen {#retrieve-access-data}

Om de &#39;toegangsinformatie&#39; te krijgen die wordt geproduceerd in antwoord op de vraag van uw betrokkene, doe een verzoek van de GET aan `/jobs/{JOB_ID}/content` eindpunt. De reactie is een ZIP-bestand (*.zip) dat een map bevat met submappen voor elk product dat gegevens over de betrokkene bevat.

>[!TIP]
>
>U hebt een specifieke taak-id nodig om deze aanvraag in te dienen. Als u de specifieke taak-id moet ophalen, vraagt u eerst een GET aan bij de `/jobs` eindpunt en gebruik extra vraagparameters om de resultaten te filtreren. Gedetailleerde informatie, waaronder de toegestane queryparameters, vindt u in het gedeelte [eindgebruikershandleiding voor privacytaken](./privacy-jobs.md).

**API-indeling**

```http
GET /jobs/{JOB_ID}/content
```

**Verzoek**

Het volgende verzoek retourneert &#39;toegangsinformatie&#39; voor de taak-id die in het verzoek wordt opgegeven.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/32d429b1-f7f4-11ee-a365-574bcf5a525d/content \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'Accept: application/json`
```

**Antwoord**

De reactie is een ZIP-bestand (*.zip). De informatie wordt doorgaans geretourneerd in JSON-indeling, maar dat kan niet worden gegarandeerd. Geëxtraheerde gegevens kunnen in elke indeling worden geretourneerd.

