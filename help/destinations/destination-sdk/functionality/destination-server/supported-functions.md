---
description: De Destination SDK van het Experience Platform gebruikt de malplaatjes van de Kiezelaar, toestaand u om de gegevens die van Experience Platform worden uitgevoerd in het formaat om te zetten dat door uw bestemming wordt vereist.
title: Ondersteunde transformatiefuncties in Destination SDK
exl-id: 36f761c7-9d76-41fe-b05f-d4cad655ddd2
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# Ondersteunde transformatiefuncties in Destination SDK

De Destination SDK van het Experience Platform gebruikt [[!DNL Pebble]  malplaatjes &#x200B;](https://pebbletemplates.io/), toestaand u om de gegevens die van Experience Platform worden uitgevoerd in het formaat om te zetten dat door uw bestemming wordt vereist.

De implementatie van het Experience Platform [!DNL Pebble] heeft enkele wijzigingen ten opzichte van de versie van het tekstvak die wordt geleverd door [!DNL Pebble] . Naast de functies die [!DNL Pebble] biedt voor &#39;out-of-the-box&#39;, heeft Adobe ook enkele extra functies gemaakt die u kunt gebruiken met Destination SDK.

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Waar wordt het gebruikt? {#where-to-use}

Gebruik de gesteunde die functies verder hieronder op deze pagina worden vermeld wanneer [&#x200B; creërend een malplaatje van de berichttransformatie &#x200B;](../../testing-api/streaming-destinations/create-template.md) voor de gegevens uit Experience Platform naar uw bestemming worden uitgevoerd.

Het malplaatje van de berichttransformatie wordt gebruikt in de [&#x200B; configuratie van de bestemmingsserver &#x200B;](templating-specs.md) voor het stromen bestemmingen.

## Vereisten {#prerequisites}

Om de concepten en de functies in deze verwijzingspagina te begrijpen, lees eerst het [&#x200B; document van het berichtformaat &#x200B;](message-format.md). U moet de [&#x200B; structuur van een profiel &#x200B;](message-format.md#profile-structure) in Experience Platform begrijpen alvorens u [!DNL Pebble] malplaatjes kunt gebruiken om en de uitgevoerde gegevens te transformeren.

Alvorens u aan de hieronder gedocumenteerde functies vooruitgaat, herzie de sjabloonvoorbeelden in de sectie [&#x200B; Gebruikend een het malplaatjetaal voor de identiteit, de attributen, en de transformaties van het publiekslidmaatschap &#x200B;](message-format.md#using-templating). De voorbeelden in dat verband beginnen zeer eenvoudig en nemen toe in complexiteit.

## Ondersteunde [!DNL Pebble] functies {#supported-functions}

In de sectie [!DNL Pebble] -tags ondersteunt alleen Destination SDK:

* [&#x200B; filter &#x200B;](https://pebbletemplates.io/wiki/tag/filter/)
* [&#x200B; for &#x200B;](https://pebbletemplates.io/wiki/tag/for/)
* [&#x200B; als &#x200B;](https://pebbletemplates.io/wiki/tag/if/)
* [&#x200B; plaats &#x200B;](https://pebbletemplates.io/wiki/tag/set/)

>[!TIP]
>
>Het gebruiken `for` is verschillend wanneer het herhalen door *serie* of *kaart* elementen in een malplaatje. Wanneer u een array doorloopt, kunt u het element rechtstreeks ophalen. Wanneer u door een kaart herhaalt, krijgt u elke kaartingang, die een zeer belangrijk-waardepaar heeft.
>
> * Voor een voorbeeld van een serieelement, denk over de identiteiten in [&#x200B; identityMap &#x200B;](message-format.md#identities) namespace, waar u door elementen zoals `identityMap.gaid` kon herhalen, `identityMap.email`, of gelijkaardig.
> * Voor een voorbeeld van een kaartelement, denk over [&#x200B; segmentMembership &#x200B;](message-format.md#segment-membership).

Vanuit de filtersectie [!DNL Pebble] biedt Destination SDK ondersteuning voor alle functies. In het onderstaande voorbeeld wordt getoond hoe de functie `date` binnen Destination SDK kan worden gebruikt.

Van de [!DNL Pebble] functies sectie, steunt de Adobe ** niet de [&#x200B; waaier &#x200B;](https://pebbletemplates.io/wiki/function/range/) functie.

## Voorbeeld van het gebruik van de functie `date` {#date-function}

Om te verklaren hoe [!DNL Pebble] functies in Destination SDK worden gebruikt, zie onder hoe de datumfunctie ([&#x200B; verbinding in de documentatie van de Beerbeurt &#x200B;](https://pebbletemplates.io/wiki/filter/date/)) wordt gebruikt om het formaat van een timestamp om te zetten.

### Gebruiksscenario

U wilt `lastQualificationTime` timestamp van de standaard [&#x200B; ISO 8601 &#x200B;](https://en.wikipedia.org/wiki/ISO_8601) waarde veranderen die het Experience Platform naar een andere waarde uitvoert die door uw bestemming wordt voorkeur.

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

Naast de functies buiten de doos die door [!DNL Pebble] worden verstrekt, zie hieronder de extra functies die door Adobe worden gecreeerd die u voor uw gegevensuitvoer kunt gebruiken.

### `addedSegments` en `removedSegments` functies {#addedsegments-removedsegments-functions}

#### Gebruiksscenario

Deze functies kunnen worden gebruikt om een lijst met soorten publiek te verkrijgen die aan een profiel zijn toegevoegd of uit een profiel zijn verwijderd.

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

### Added and removed audiences filters {#added-and-removed-segmnts-filters}

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

U weet nu welke [!DNL Pebble] -functies worden ondersteund in Destination SDK en hoe u deze kunt gebruiken om de indeling van de geëxporteerde gegevens aan uw wensen aan te passen. Hierna volgt een overzicht van de volgende pagina&#39;s:

* [Een sjabloon voor berichttransformatie maken en testen](../../testing-api/streaming-destinations/create-template.md)
* [API-bewerkingen voor sjablonen renderen](../../testing-api/streaming-destinations/render-template-api.md)
