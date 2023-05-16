---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een bestaand publiekssjabloon door Adobe Experience Platform Destination SDK te schrappen.
title: Een publiekssjabloon verwijderen
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---


# Een publiekssjabloon verwijderen

>[!IMPORTANT]
>
>**API-eindpunt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Deze pagina illustreert de API-aanvraag en lading die u kunt gebruiken om een publiekssjabloon te verwijderen met de `/authoring/audience-templates` API-eindpunt.

Voor een gedetailleerde beschrijving van de mogelijkheden die u door dit eindpunt kunt vormen, zie [beheer van metagegevens van het publiek](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor publiekssjablonen {#get-started}

Controleer voordat je doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Een publiekssjabloon verwijderen {#delete}

U kunt een [bestaand](create-audience-template.md) publiekssjabloon door een `DELETE` verzoek aan de `/authoring/audience-templates` met de `{INSTANCE_ID}`van de publiekssjabloon die u wilt verwijderen.

Een bestaande publiekssjabloon en de bijbehorende sjabloon opvragen `{INSTANCE_ID}`, raadpleegt u het artikel over [ophalen van een publiekssjabloon](retrieve-audience-template.md).

**API-indeling**

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

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u een publiekssjabloon kunt verwijderen met de opdracht `/authoring/audience-templates` API-eindpunt. Lezen [hoe te om Destination SDK te gebruiken om uw bestemming te vormen](../guides/configure-destination-instructions.md) om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
