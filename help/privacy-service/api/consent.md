---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: API-eindpunt voor toestemming
description: Leer hoe u verzoeken om toestemming van klanten voor Experience Cloud-toepassingen beheert met de Privacy Service-API.
role: Developer
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Constante eindpunt

Bepaalde voorschriften vereisen uitdrukkelijke toestemming van de klant voordat de persoonsgegevens kunnen worden verzameld. Met het `/consent` -eindpunt in de [!DNL Privacy Service] API kunt u verzoeken om toestemming van klanten verwerken en deze integreren in uw privacyworkflow.

Alvorens deze gids te gebruiken, gelieve te verwijzen naar [&#x200B; begonnen &#x200B;](./getting-started.md) gids voor informatie over de vereiste authentificatiekopballen die in de voorbeeld API hieronder vraag worden voorgesteld.

## Een verzoek om toestemming van een klant verwerken

Verzoeken om toestemming worden verwerkt door een POST aan te vragen bij het `/consent` eindpunt.

**API formaat**

```http
POST /consent
```

**Verzoek**

Met de volgende aanvraag wordt een nieuwe toestemmingstaak gemaakt voor de gebruikers-id&#39;s die in de array `entities` worden opgegeven.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "optOutOfSale": true,
        "entities": [
          {
            "nameSpace": "email",
            "values": [
              "dsmith@acme.com",
              "ajones@acme.com"
            ]
          },
          {
            "nameSpace": "ECID",
            "values": [
              "443636576799758681021090721276"
            ]
          }
        ]
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `optOutOfSale` | Wanneer deze waarde is ingesteld op true, geven de gebruikers die onder `entities` worden aangeboden, aan dat ze de verkoop of het delen van hun persoonlijke gegevens willen weigeren. |
| `entities` | Een array met objecten die aangeven op welke gebruikers de aanvraag voor toestemming van toepassing is. Elk object bevat een `namespace` en een array van `values` die overeenkomen met afzonderlijke gebruikers met die naamruimte. |
| `nameSpace` | Elk voorwerp in de `entities` serie moet één van [&#x200B; standaard identiteitsnamespaces &#x200B;](./appendix.md#standard-namespaces) bevatten die door Privacy Service API wordt erkend. |
| `values` | Een array van waarden voor elke gebruiker, die overeenkomt met de opgegeven `nameSpace` . |

{style="table-layout:auto"}

>[!NOTE]
>
>Voor meer informatie over hoe te om te bepalen welke waarden van de klantenidentiteit om naar [!DNL Privacy Service] te verzenden, zie de gids over [&#x200B; het verstrekken van identiteitsgegevens &#x200B;](../identity-data.md).

**Reactie**

Een geslaagde reactie retourneert HTTP-status 202 (geaccepteerd) zonder payload om aan te geven dat de aanvraag is geaccepteerd door [!DNL Privacy Service] en wordt verwerkt.
