---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: API-eindpunt voor toestemming
topic-legacy: developer guide
description: Leer hoe u verzoeken om toestemming van klanten voor Experience Cloud-toepassingen beheert met de Privacy Service-API.
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Constante eindpunt

Bepaalde voorschriften vereisen uitdrukkelijke toestemming van de klant voordat de persoonsgegevens kunnen worden verzameld. De `/consent` in de [!DNL Privacy Service] Met API kunt u verzoeken om toestemming van klanten verwerken en deze integreren in uw privacyworkflow.

Voordat u deze handleiding kunt gebruiken, raadpleegt u de [aan de slag](./getting-started.md) gids voor informatie over de vereiste authentificatiekopballen die in de voorbeeld API vraag hieronder worden voorgesteld.

## Een verzoek om toestemming van een klant verwerken

Aanvragen om toestemming worden verwerkt door een POST aan de `/consent` eindpunt.

**API-indeling**

```http
POST /consent
```

**Verzoek**

Met het volgende verzoek wordt een nieuwe goedkeuringstaak gemaakt voor de gebruikers-id&#39;s die worden geleverd in het dialoogvenster `entities` array.

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
| `optOutOfSale` | Indien ingesteld op true, geeft dit aan dat de gebruikers onder `entities` de wens te kennen te geven zich niet aan de verkoop of het delen van hun persoonsgegevens te houden. |
| `entities` | Een array met objecten die aangeven op welke gebruikers de aanvraag voor toestemming van toepassing is. Elk object bevat een `namespace` en een array van `values` om afzonderlijke gebruikers met die naamruimte te laten overeenkomen. |
| `nameSpace` | Elk object in het dialoogvenster `entities` array moet een van de [standaardnaamruimten](./appendix.md#standard-namespaces) wordt herkend door de Privacy Service-API. |
| `values` | Een array van waarden voor elke gebruiker, die overeenkomt met de opgegeven waarden `nameSpace`. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Voor meer informatie over hoe te bepalen welke waarden van de klantenidentiteit om te verzenden naar [!DNL Privacy Service], zie de handleiding op [identiteitsgegevens verstrekken](../identity-data.md).

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 202 (geaccepteerd) zonder payload om aan te geven dat de aanvraag is geaccepteerd door [!DNL Privacy Service] en wordt verwerkt.
