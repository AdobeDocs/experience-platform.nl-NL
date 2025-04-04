---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een bestaand publiekssjabloon door Adobe Experience Platform Destination SDK te schrappen.
title: Een publiekssjabloon verwijderen
exl-id: 6eb07e3c-3269-4368-9b11-04bd993cc4ab
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Een publiekssjabloon verwijderen

>[!IMPORTANT]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Deze pagina illustreert de API-aanvraag en lading die u kunt gebruiken om een publiekssjabloon te verwijderen met behulp van het API-eindpunt `/authoring/audience-templates` .

Voor een gedetailleerde beschrijving van de mogelijkheden die u door dit eindpunt kunt vormen, zie [ beheer van publieksmeta-gegevens ](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor publiekssjablonen {#get-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Een publiekssjabloon verwijderen {#delete}

U kunt een [ bestaand ](create-audience-template.md) publiekssjabloon schrappen door a `DELETE` verzoek aan het `/authoring/audience-templates` eindpunt met `{INSTANCE_ID}` van het publiekssjabloon te maken dat u wilt schrappen.

Om een bestaand publiekssjabloon en zijn overeenkomstige `{INSTANCE_ID}` te verkrijgen, zie het artikel over [ het terugwinnen van een publiekssjabloon ](retrieve-audience-template.md).

**API formaat**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{INSTANCE_ID}` | De `ID` van de publiekssjabloon die u wilt verwijderen. |

+++verzoek

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Response

Een geslaagde reactie retourneert HTTP-status 200 samen met een lege HTTP-respons.

+++

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [ API statuscodes ](../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u een publiekssjabloon kunt verwijderen met behulp van het API-eindpunt van `/authoring/audience-templates` . Lees [ hoe te om Destination SDK te gebruiken om uw bestemming ](../guides/configure-destination-instructions.md) te vormen om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
