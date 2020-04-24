---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Bronnen weergeven
topic: developer guide
translation-type: tm+mt
source-git-commit: 58549241f05f1bd604f33762f681c60946fa52f5

---


# Bronnen weergeven

U kunt een lijst van alle middelen van de Registratie van het Schema van een bepaald type (klassen, mixins, schema&#39;s, gegevenstypes, of beschrijvers) binnen een container bekijken door één enkele GET verzoek uit te voeren.

>[!NOTE] Bij het vermelden van bronnen, beperkt het resultaat van de Registratie van het Schema aan 300 punten. Als u bronnen buiten deze limiet wilt retourneren, moet u [pagineringsparameters](#paging)gebruiken. Men adviseert ook dat u vraagparameters gebruikt om resultaten [te](#filtering) filtreren en het aantal teruggekeerde middelen te verminderen.

**API-indeling**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONTAINER_ID}` | De container waar de middelen worden gevestigd (&quot;globaal&quot;of &quot;huurder&quot;). |
| `{RESOURCE_TYPE}` | Het type van middel om van de Bibliotheek van het Schema terug te winnen. Geldige typen zijn `classes`, `mixins`, `schemas`, `datatypes`en `descriptors`. |
| `{QUERY_PARAMS`} | Optionele queryparameters om resultaten te filteren op. Zie de sectie over [vraagparameters](#query) voor meer informatie. |

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
| application/vnd.adobe.xed-id+json | Retourneert een korte samenvatting van elke bron. Dit is de aanbevolen koptekst voor aanbiedingsbronnen. (Limiet: 300) |
| application/vnd.adobe.xed+json | Retourneert het volledige JSON-schema voor elke bron, met origineel `$ref` en `allOf` opgenomen. (Limiet: 300) |
| application/vnd.adobe.xdm-v2+json | Wanneer het gebruiken van het `/descriptors` eindpunt, moet deze Accept kopbal worden gebruikt om het pagineren mogelijkheden te gebruiken. |

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

## Query-parameters gebruiken {#query}

De Registratie van het Schema steunt het gebruik van vraagparameters aan pagina en filterresultaten wanneer het vermelden van middelen.

>[!NOTE] Wanneer het combineren van veelvoudige vraagparameters, moeten zij door ampersands (`&`) worden gescheiden.

### Paginering {#paging}

De gemeenschappelijkste vraagparameters voor het pagineren omvatten:

| Parameter | Beschrijving |
| --- | --- |
| `start` | Geef op waar de weergegeven resultaten moeten worden opgehaald. Voorbeeld: `start=2` vermeldt de resultaten van het derde geretourneerde object. |
| `limit` | Beperk het aantal geretourneerde bronnen. Voorbeeld: `limit=5` retourneert een lijst met vijf bronnen. |
| `orderby` | Resultaten sorteren op een bepaalde eigenschap. Voorbeeld: De resultaten worden op titel in oplopende volgorde (A-Z) gesorteerd. `orderby=title` Als u een `-` vóór titel (`orderby=-title`) toevoegt, worden de items op titel gesorteerd in aflopende volgorde (Z-A). |

### Filteren {#filtering}

U kunt resultaten filtreren door de `property` parameter te gebruiken, die wordt gebruikt om een specifieke exploitant op een bepaalde bezit JSON binnen de teruggewonnen middelen toe te passen. Tot de ondersteunde operatoren behoren:

| Operator | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `==` | Filtert op of de eigenschap gelijk is aan de opgegeven waarde. | `property=title==test` |
| `!=` | Filtert op of de eigenschap niet gelijk is aan de opgegeven waarde. | `property=title!=test` |
| `<` | Filtert op of de eigenschap kleiner is dan de opgegeven waarde. | `property=version<5` |
| `>` | Filtert op of de eigenschap groter is dan de opgegeven waarde. | `property=version>5` |
| `<=` | Filtert op of de eigenschap kleiner dan of gelijk is aan de opgegeven waarde. | `property=version<=5` |
| `>=` | Filtert op of de eigenschap groter dan of gelijk is aan de opgegeven waarde. | `property=version>=5` |
| `~` | Filtert op of de eigenschap overeenkomt met een opgegeven reguliere expressie. | `property=title~test$` |
| (Geen) | Wanneer alleen de naam van de eigenschap wordt opgegeven, worden alleen items geretourneerd waar de eigenschap bestaat. | `property=title` |

>[!TIP] U kunt de `property` parameter aan filtermengen door hun compatibele klasse gebruiken. Retourneert bijvoorbeeld alleen `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` mixins die compatibel zijn met de klasse Individueel profiel XDM.
