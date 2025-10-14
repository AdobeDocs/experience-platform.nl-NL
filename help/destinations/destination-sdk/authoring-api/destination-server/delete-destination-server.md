---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een bestaande configuratie van de bestemmingsserver door Adobe Experience Platform Destination SDK te schrappen.
title: Een doelserverconfiguratie verwijderen
exl-id: 2322a2ce-220e-4590-a553-b15152412752
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Een doelserverconfiguratie verwijderen

Deze pagina illustreert de API-aanvraag en lading die u kunt gebruiken om een bestaande configuratie van de doelserver te verwijderen met behulp van het API-eindpunt `/authoring/destination-servers` .

Lees de volgende artikelen voor een gedetailleerde beschrijving van de mogelijkheden die u via dit eindpunt kunt verwijderen:

* [Serverspecificaties voor doelen die met Destination SDK zijn gemaakt](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Sjabloonspecificaties voor bestemmingen die zijn gemaakt met Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Berichtindeling](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuratie bestandsindeling](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor doelserver {#get-started}

Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](../../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Een doelserverconfiguratie verwijderen {#delete}

U kunt een [&#x200B; bestaande &#x200B;](create-destination-server.md) configuratie van de bestemmingsserver schrappen door a `DELETE` verzoek aan het `/authoring/destination-servers` eindpunt met `{INSTANCE_ID}` van de configuratie van de bestemmingsserver te maken die u wilt schrappen.

>[!TIP]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Om een bestaande configuratie van de bestemmingsserver en zijn overeenkomstige `{INSTANCE_ID}` te verkrijgen, zie het artikel over [&#x200B; het terugwinnen van een configuratie van de bestemmingsserver &#x200B;](retrieve-destination-server.md).

**API formaat**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{INSTANCE_ID}` | De `ID` van de configuratie van de bestemmingsserver u wilt schrappen. |

+++verzoek

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++Response

Een geslaagde reactie retourneert HTTP-status 200 samen met een lege HTTP-respons.

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [&#x200B; API statuscodes &#x200B;](../../../../landing/troubleshooting.md#api-status-codes) en [&#x200B; de fouten van de verzoekkopbal &#x200B;](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u een bestaande doelserver kunt verwijderen via het API-eindpunt van Destination SDK `/authoring/destination-servers` .

Raadpleeg de volgende artikelen voor meer informatie over wat u met dit eindpunt kunt doen:

* [Een doelserverconfiguratie maken](create-destination-server.md)
* [De configuratie van een doelserver ophalen](retrieve-destination-server.md)
* [Een doelserverconfiguratie bijwerken](update-destination-server.md)
