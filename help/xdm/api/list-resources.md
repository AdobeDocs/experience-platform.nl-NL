---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Bronnen weergeven
topic: developer guide
translation-type: tm+mt
source-git-commit: 1541b027a4e572dc5e4e64de1117a269c58bafab

---


# Bronnen weergeven

U kunt een lijst van alle middelen (schema&#39;s, klassen, mixins, of gegevenstypes) binnen een container bekijken door één enkele GET verzoek uit te voeren. Om filterresultaten te helpen, steunt de Registratie van het Schema het gebruik van vraagparameters wanneer het vermelden van middelen.

De gemeenschappelijkste vraagparameters omvatten:

* `limit` - Beperk het aantal geretourneerde bronnen. Voorbeeld: `limit=5` retourneert een lijst met vijf bronnen.
* `orderby` - Resultaten sorteren op een bepaalde eigenschap. Voorbeeld: De resultaten worden op titel in oplopende volgorde (A-Z) gesorteerd. `orderby=title` Als u een `-` vóór titel (`orderby=-title`) toevoegt, worden de items op titel gesorteerd in aflopende volgorde (Z-A).
* `property` - Filterresultaten voor alle kenmerken op hoofdniveau. Retourneert bijvoorbeeld alleen `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` mixins die compatibel zijn met de klasse Individueel profiel XDM.

Wanneer het combineren van veelvoudige vraagparameters, moeten zij door ampersands (`&`) worden gescheiden.

**API-indeling**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container waar de middelen worden gevestigd (&quot;globaal&quot;of &quot;huurder&quot;). |
| `{RESOURCE_TYPE}` | Het type van middel om van de Bibliotheek van het Schema terug te winnen. Geldige typen zijn `datatypes`, `mixins`, `schemas`en `classes`. |

**Verzoek**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes&limit=2 \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De responsindeling is afhankelijk van de Accept-header die in de aanvraag wordt verzonden. De volgende koppen Accepteren zijn beschikbaar voor aanbiedingsbronnen:

| Koptekst accepteren | Beschrijving |
| ------- | ------------ |
| application/vnd.adobe.xed-id+json | Hiermee wordt een korte samenvatting van elke bron geretourneerd, doorgaans de voorkeursheader voor vermelding |
| application/vnd.adobe.xed+json | Retourneert het volledige JSON-schema voor elke bron, met origineel `$ref` en `allOf` inbegrepen |

**Antwoord**

In het bovenstaande verzoek wordt de header `application/vnd.adobe.xed-id+json` Accepteren gebruikt. Daarom bevat de reactie alleen de kenmerken `title`, `$id`, `meta:altId`en `version` kenmerken voor elke bron. Als u `full` de header Accepteren vervangt, worden alle kenmerken van elke bron geretourneerd. Selecteer de juiste Accept-header, afhankelijk van de informatie die u in uw reactie nodig hebt.

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```
