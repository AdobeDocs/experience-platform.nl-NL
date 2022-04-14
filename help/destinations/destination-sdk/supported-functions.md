---
description: De Destination SDK van het Experience Platform gebruikt de malplaatjes van de Kiezelaar, toestaand u om de gegevens die van Experience Platform worden uitgevoerd in het formaat om te zetten dat door uw bestemming wordt vereist.
title: Ondersteunde transformatiefuncties in Destination SDK
source-git-commit: 840404741da06ba1593b227c7d6ba459b5f43110
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---

# Ondersteunde transformatiefuncties in Destination SDK

## Overzicht {#overview}

Experience Platform-Destination SDK gebruikt [[!DNL Pebble] sjablonen](https://pebbletemplates.io/), zodat u de uit Experience Platform geëxporteerde gegevens kunt omzetten in de indeling die voor uw bestemming vereist is.

Het Experience Platform [!DNL Pebble] de implementatie is gewijzigd, in vergelijking met de versie van de box buiten de [!DNL Pebble]. Naast de functies die buiten de box worden geleverd door [!DNL Pebble], heeft Adobe enkele extra functies gemaakt die u kunt gebruiken met Destination SDK.

## Waar wordt het gebruikt? {#where-to-use}

Gebruik de ondersteunde functies die verderop op op deze pagina staan wanneer [een sjabloon voor berichttransformatie maken](./create-template.md) voor de gegevens die uit Experience Platform naar uw bestemming worden geëxporteerd. De sjabloon voor berichttransformatie wordt gebruikt in het dialoogvenster [doelserverconfiguratie](./server-and-template-configuration.md) voor streamingdoelen.

## Vereisten {#prerequisites}

Als u de concepten en functies in deze referentiepagina wilt begrijpen, leest u de [berichtindeling](/help/destinations/destination-sdk/message-format.md) document eerst. U moet de [structuur van een profiel](/help/destinations/destination-sdk/message-format.md#profile-structure) in Experience Platform voordat u kunt gebruiken [!DNL Pebble] sjablonen voor transformatie en de geëxporteerde gegevens.

Lees de sjabloonvoorbeelden in de sectie voordat u doorgaat naar de functies die hieronder worden beschreven [Een sjabloontaal gebruiken voor de transformaties voor identiteit, kenmerken en segmentlidmaatschap](/help/destinations/destination-sdk/message-format.md#using-templating). De voorbeelden in dat verband beginnen zeer eenvoudig en nemen toe in complexiteit.

## Ondersteund [!DNL Pebble] functies {#supported-functions}

Van de [!DNL Pebble] tagsectie, alleen Destination SDK ondersteunt:
* [filter](https://pebbletemplates.io/wiki/tag/filter/)
* [for](https://pebbletemplates.io/wiki/tag/for/)
* [indien](https://pebbletemplates.io/wiki/tag/if/)
* [set](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>Gebruiken `for` is anders wanneer u doorloopt *array* of *map* elementen in een sjabloon. Wanneer u een array doorloopt, kunt u het element rechtstreeks ophalen. Wanneer u door een kaart herhaalt, krijgt u elke kaartingang, die een zeer belangrijk-waardepaar heeft.
>
> * Denk bij een voorbeeld van een arrayelement aan de identiteiten in een [identityMap](./message-format.md#identities) naamruimte, waar u elementen zoals `identityMap.gaid`, `identityMap.email`, of een soortgelijke situatie.
> * Denk aan een voorbeeld van een structuurelement over [segmentLidmaatschap](./message-format.md#segment-membership).


Van de [!DNL Pebble] filtersectie, Destination SDK ondersteunt alle functies. In het onderstaande voorbeeld wordt getoond hoe de `date` functie kan binnen Destination SDK worden gebruikt.

Van de [!DNL Pebble] functies, sectie, Adobe doet *niet* de [bereik](https://pebbletemplates.io/wiki/function/range/) functie.

## Voorbeeld van hoe het `date` function wordt gebruikt {#date-function}

Uitlijnen hoe [!DNL Pebble] functies worden gebruikt in Destination SDK, zie hieronder hoe de datumfunctie ([link in Pebble documentatie](https://pebbletemplates.io/wiki/filter/date/)) wordt gebruikt om de indeling van een tijdstempel te transformeren.

### Gebruiksscenario

U wilt het dialoogvenster `lastQualificationTime` tijdstempel van de standaard [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) waarde die Experience Platform naar een andere waarde uitvoert die door uw bestemming wordt voorkeur.

### Voorbeeld

#### Invoer

```json
{
"lastQualificationTime": "2022-02-08T18:34:24.000+0000"
}
```

#### Indeling

```java
{{ lastQualificationTime | date(existingFormat="yyyy-MM-dd'T'HH:mm:sss.SSSX", format="yyyy-MM-dd'T'HH:mm:ssX") }}
```

#### Uitvoer

```json
{
"lastQualificationTime": "2022-02-21T18:34:24Z"
}
```

## Door Adobe toegevoegde functies {#functions-added-by-adobe}

Naast de functies die buiten de box worden geleverd door [!DNL Pebble], zie onder de extra functies die door Adobe worden gecreeerd die u voor uw gegevensuitvoer kunt gebruiken.

### `addedSegments` en `removedSegments` functies {#addedsegments-removedsegments-functions}

#### Gebruiksscenario

Deze functies kunnen worden gebruikt om een lijst met segmenten te verkrijgen die aan een profiel zijn toegevoegd of uit een profiel zijn verwijderd.

#### Voorbeeld

##### Invoer

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Indeling

```java
added: {% for s in addedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}; removed: {% for s in removedSegments(segmentMembership.ups) %}<{{s.key}}>{% endfor %}
```

##### Uitvoer

```json
added: <111111><333333>; removed: <222222>
```

<!--

### Added and removed segments filters {#added-and-removed-segmnts-filters}

#### Use case {#use-case}

These filters are similar to `addedSegments` and `removedSegments`, described above. The only difference is that they are implemented as filters as opposed to functions.

#### Example {#example}

##### Input {#input}

```json
{
  "identityMap": {
    "myIdNamespace": [
      {
        "id": "external_id1"
      },
      {
        "id": "external_id2"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "111111": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "222222": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      },
      "333333": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      }
    }
  }
}
```

##### Format {#format}

```java
added: {% for s in input.profile.segmentMembership.ups | added %}<{{s.key}}>{% endfor %};|removed: {% for s in input.profile.segmentMembership.ups | removed %}<{{s.key}}>{% endfor %};
```

##### Output {#output}

```json
added: <111111><333333>;|removed: <222222>;
```

-->

## Volgende stappen {#next-steps}

U weet nu welke [!DNL Pebble] functies worden ondersteund in Destination SDK en hoe u deze kunt gebruiken om de indeling van de geëxporteerde gegevens aan uw wensen aan te passen. Hierna volgt een overzicht van de volgende pagina&#39;s:

* [Een sjabloon voor berichttransformatie maken en testen](/help/destinations/destination-sdk/create-template.md)
* [API-bewerkingen voor sjablonen renderen](/help/destinations/destination-sdk/render-template-api.md)