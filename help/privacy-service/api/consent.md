---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Constante eindpunt
topic: developer guide
description: Leer hoe u verzoeken om toestemming van klanten voor Experience Cloud-toepassingen beheert met de Privacy Service-API.
translation-type: tm+mt
source-git-commit: 238a9200e4b43d41335bed0efab079780b252717
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Constante eindpunt

Bepaalde voorschriften vereisen uitdrukkelijke toestemming van de klant voordat de persoonsgegevens kunnen worden verzameld. Met het `/consent`-eindpunt in de [!DNL Privacy Service]-API kunt u verzoeken om toestemming van klanten verwerken en deze integreren in uw privacyworkflow.

Voordat u deze handleiding gebruikt, raadpleegt u de sectie [Aan de slag](./getting-started.md) voor informatie over de vereiste verificatieheaders in de voorbeeld-API-aanroep hieronder.

## Een verzoek om toestemming van een klant verwerken

De toestemmingsverzoeken worden verwerkt door een verzoek van de POST aan het `/consent` eindpunt te doen.

**API-indeling**

```http
POST /consent
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe toestemmingstaak voor gebruiker - IDs die in `entities` serie wordt verstrekt.

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
| `optOutOfSale` | Wanneer ingesteld op true, geeft dit aan dat de gebruikers die worden geleverd onder `entities`, de verkoop of het delen van hun persoonlijke gegevens willen weigeren. |
| `entities` | Een array met objecten die aangeven op welke gebruikers de aanvraag voor toestemming van toepassing is. Elk object bevat een `namespace` en een array van `values` om afzonderlijke gebruikers met die naamruimte te laten overeenkomen. |
| `nameSpace` | Elk object in de `entities`-array moet een van de [standaard naamruimten](./appendix.md#standard-namespaces) bevatten die door de Privacy Service-API worden herkend. |
| `values` | Een array van waarden voor elke gebruiker, die overeenkomt met de opgegeven `nameSpace`. |

>[!NOTE]
>
>Zie de handleiding over [het verschaffen van identiteitsgegevens](../identity-data.md) voor meer informatie over hoe u kunt bepalen welke waarden voor de identiteit van klanten u naar [!DNL Privacy Service] wilt verzenden.

**Antwoord**

Een succesvolle reactie keert HTTP status 202 (Toegelaten) zonder nuttige lading terug, erop wijzend dat het verzoek door [!DNL Privacy Service] werd goedgekeurd en aan verwerking ondergaat.