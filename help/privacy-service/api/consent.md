---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Toestemming
topic: developer guide
translation-type: tm+mt
source-git-commit: a3178ab54a7ab5eacd6c5f605b8bd894779f9e85
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Toestemming

Bepaalde voorschriften vereisen uitdrukkelijke toestemming van de klant voordat hun persoonsgegevens kunnen worden verzameld. Het `/consent` eindpunt in de API van de Dienst van de Privacy staat u toe om verzoeken van de klantentoestemming te verwerken en hen in uw privacywerkschema te integreren.

Voordat u deze handleiding gebruikt, raadpleegt u de sectie Aan de [slag](./getting-started.md) voor informatie over de vereiste verificatieheaders in de voorbeeld-API-aanroep hieronder.

## Een verzoek om toestemming van een klant verwerken

De toestemmingsverzoeken worden verwerkt door een POST- verzoek aan het `/consent` eindpunt te doen.

**API-indeling**

```http
POST /consent
```

**Verzoek**

Met de volgende aanvraag wordt een nieuwe goedkeuringstaak gemaakt voor de gebruikers-id&#39;s die in de `entities` array zijn opgenomen.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `optOutOfSale` | Wanneer deze waarde wordt ingesteld op true, geeft dit aan dat de gebruikers die onder `entities` wens zijn aangeboden, zich willen onthouden van de verkoop of het delen van hun persoonsgegevens. |
| `entities` | Een array met objecten die aangeven op welke gebruikers de aanvraag voor toestemming van toepassing is. Elk object bevat een array `namespace` en een array `values` die overeenkomen met afzonderlijke gebruikers met die naamruimte. |
| `nameSpace` | Elk object in de `entities` array moet een van de [standaardnaamruimten](./appendix.md#standard-namespaces) bevatten die door de API van de privacyservice worden herkend. |
| `values` | Een array van waarden voor elke gebruiker, die overeenkomt met de opgegeven waarden `nameSpace`. |

>[!NOTE] Voor meer informatie over hoe te om te bepalen welke waarden van de klantenidentiteit om naar de Dienst van de Privacy te verzenden, zie de gids over het [verstrekken van identiteitsgegevens](../identity-data.md).

**Antwoord**

Een succesvolle reactie keert HTTP status 202 (Toegelaten) zonder lading terug, erop wijzend dat het verzoek door de Dienst van de Privacy werd goedgekeurd en aan verwerking ondergaat.