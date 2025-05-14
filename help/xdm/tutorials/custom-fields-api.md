---
title: XDM-velden definiëren in de API voor schemaregister
description: Leer hoe u verschillende velden definieert bij het maken van XDM-bronnen (Custom Experience Data Model) in de Schema Registry API.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 6c6104a6aa0a80c886f4f02486a7645eb95da781
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# XDM-velden definiëren in de API voor het schemaregister

Alle gebieden van de Gegevens van de Ervaring Model (XDM) worden bepaald gebruikend de standaard [&#128279;](https://json-schema.org/) beperkingen van het Schema JSON  die op hun gebiedstype van toepassing zijn, met extra beperkingen voor gebiedsnamen die door Adobe Experience Platform worden afgedwongen. Met de API voor het schemaregister kunt u aangepaste velden in uw schema&#39;s definiëren met behulp van indelingen en optionele beperkingen. XDM-veldtypen worden weergegeven door het kenmerk op veldniveau, `meta:xdmType` .

>[!NOTE]
>
>`meta:xdmType` is een systeem-geproduceerde waarde, en daarom wordt u vereist om dit bezit aan JSON voor uw gebied toe te voegen wanneer het gebruiken van API (behalve wanneer [ het creëren van de types van douanekaart ](#custom-maps)). De beste manier is om JSON-schematypen (zoals `string` en `integer` ) te gebruiken met de juiste min/max-beperkingen zoals gedefinieerd in de onderstaande tabel.

In deze handleiding wordt de juiste opmaak beschreven voor het definiëren van verschillende veldtypen, inclusief die met optionele eigenschappen. Meer informatie betreffende facultatieve eigenschappen en type-specifieke sleutelwoorden is beschikbaar door de [ documentatie van het Schema JSON ](https://json-schema.org/understanding-json-schema/reference/type.html).

Om te beginnen, het gewenste gebiedstype te vinden en de steekproefcode te gebruiken die wordt verstrekt om uw API verzoek voor [ te bouwen creërend een gebiedsgroep ](../api/field-groups.md#create) of [ creërend een gegevenstype ](../api/data-types.md#create).

## [!UICONTROL String] {#string}

[!UICONTROL String] -velden worden aangegeven door `type: string` .

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

U kunt desgewenst beperken welke soorten waarden voor de tekenreeks kunnen worden ingevoerd via de volgende aanvullende eigenschappen:

* `pattern`: Een regex-patroon dat moet worden beperkt.
* `minLength`: een minimumlengte voor de tekenreeks. Tekenreeksen krijgen standaard de minimale waarde `1` .
* `maxLength`: Een maximumlengte voor de tekenreeks.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field with added constraints.",
  "type": "string",
  "pattern": "^[A-Z]{2}$",
  "maxLength": 2
}
```

## [!UICONTROL URI] {#uri}

[!UICONTROL URI] -velden worden aangegeven door `type: string` met een eigenschap `format` ingesteld op `uri` . Er worden geen andere eigenschappen geaccepteerd.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL Enum] {#enum}

[!UICONTROL Enum] -velden moeten `type: string` gebruiken, waarbij de opsommingswaarden zelf onder een `enum` -array worden opgegeven:

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ]
}
```

U kunt desgewenst labels voor klanten opgeven voor elke waarde onder een eigenschap `meta:enum` , waarbij elk label onder `enum` wordt toegepast op een corresponderende waarde.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Value 1",
      "value2": "Value 2",
      "value3": "Value 3"
  }
}
```

>[!NOTE]
>
>De `meta:enum` waarde verklaart **&#x200B;**&#x200B;geen opsomming of drijft om het even welke gegevensbevestiging op zijn. In de meeste gevallen worden onder `meta:enum` verschafte tekenreeksen ook onder `enum` opgegeven om ervoor te zorgen dat er beperkingen gelden voor gegevens. Er zijn echter enkele gebruiksgevallen waarin `meta:enum` wordt geleverd zonder overeenkomende `enum` -array. Zie het leerprogramma op [ bepalend gesuggereerde waarden ](../tutorials/suggested-values.md) voor meer informatie.

U kunt desgewenst een eigenschap `default` opgeven die de standaardwaarde `enum` aangeeft die het veld gebruikt wanneer geen waarde wordt opgegeven.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels and a default value.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Value 1",
      "value2": "Value 2",
      "value3": "Value 3"
  },
  "default": "value1"
}
```

>[!IMPORTANT]
>
>Als er geen `default` -waarde is opgegeven en het opsommingsveld is ingesteld op `required` , zal een record waarin een geaccepteerde waarde voor dit veld ontbreekt, de validatie tijdens het invoeren mislukken.

## [!UICONTROL Number] {#number}

Nummervelden worden aangegeven door `type: number` en hebben geen andere vereiste eigenschappen.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` types worden gebruikt voor om het even welk numeriek type, of gehelen of drijvende puntaantallen, terwijl [`integer` types ](#integer) specifiek voor integrale aantallen worden gebruikt. Verwijs naar de [ documentatie van het Schema JSON over numerieke types ](https://json-schema.org/understanding-json-schema/reference/numeric.html) voor meer informatie over de gebruiksgevallen voor elk type.

## [!UICONTROL Integer] {#integer}

[!UICONTROL Integer] -velden worden aangegeven door `type: integer` en hebben geen andere vereiste velden.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>Hoewel `integer` types specifiek naar integrale aantallen verwijzen, [`number` types ](#number) worden gebruikt voor om het even welk numeriek type, of gehelen of drijvende puntaantallen. Verwijs naar de [ documentatie van het Schema JSON over numerieke types ](https://json-schema.org/understanding-json-schema/reference/numeric.html) voor meer informatie over de gebruiksgevallen voor elk type.

U kunt optioneel het bereik van het gehele getal beperken door eigenschappen `minimum` en `maximum` aan de definitie toe te voegen. Verschillende andere numerieke typen die door de Schema Builder-gebruikersinterface worden ondersteund, zijn `integer` -typen met specifieke `minimum` - en `maximum` -beperkingen, zoals [[!UICONTROL Long]](#long) , [[!UICONTROL Short]](#short) en [[!UICONTROL Byte]](#byte) .

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field with added constraints.",
  "type": "integer",
  "minimum": 1,
  "maximum": 100
}
```

## [!UICONTROL Long] {#long}

Het equivalent van een [!UICONTROL Long] gebied dat door de Bouwer van het Schema UI wordt gecreeerd is een [`integer` typegebied ](#integer) met specifieke `minimum` en `maximum` waarden (`-9007199254740992` en `9007199254740992`, respectievelijk).

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL Short] {#short}

Het equivalent van een [!UICONTROL Short] gebied dat door de Bouwer van het Schema UI wordt gecreeerd is een [`integer` typegebied ](#integer) met specifieke `minimum` en `maximum` waarden (`-32768` en `32767`, respectievelijk).

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32767
}
```

## [!UICONTROL Byte] {#byte}

Het equivalent van een [!UICONTROL Byte] gebied dat door de Bouwer van het Schema UI wordt gecreeerd is een [`integer` typegebied ](#integer) met specifieke `minimum` en `maximum` waarden (`-128` en `127`, respectievelijk).

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 127
}
```

## [!UICONTROL Boolean] {#boolean}

[!UICONTROL Boolean] -velden worden aangegeven door `type: boolean` .

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

U kunt desgewenst een `default` -waarde opgeven die door het veld wordt gebruikt wanneer tijdens het innemen geen expliciete waarde wordt opgegeven.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field with a default value.",
  "type": "boolean",
  "default": false
}
```

>[!IMPORTANT]
>
>Als er geen `default` -waarde is opgegeven en het Booleaanse veld is ingesteld op `required` , zal een record zonder een geaccepteerde waarde voor dit veld niet worden gevalideerd bij invoer.

## [!UICONTROL Date] {#date}

[!UICONTROL Date] -velden worden aangegeven met `type: string` en `format: date` . U kunt desgewenst ook een array van `examples` aan hefboomwerking verstrekken in gevallen waarin u een koord van de steekproefdatum voor gebruikers wilt tonen die de gegevens manueel ingaan.

```json
"sampleField": {
  "title": "Sample Date Field",
  "description": "An example date field with an example array item.",
  "type": "string",
  "format": "date",
  "examples": ["2004-10-23"]
}
```

## [!UICONTROL DateTime] {#date-time}

[!UICONTROL DateTime] -velden worden aangegeven met `type: string` en `format: date-time` . U kunt desgewenst ook een array van `examples` aan hefboomwerking verstrekken in gevallen waar u een steekproefdatetime koord voor gebruikers wilt tonen die de gegevens manueel ingaan.

```json
"sampleField": {
  "title": "Sample Datetime Field",
  "description": "An example datetime field with an example array item.",
  "type": "string",
  "format": "date-time",
  "examples": ["2004-10-23T12:00:00-06:00"]
}
```

## [!UICONTROL Array] {#array}

[!UICONTROL Array] -velden worden aangegeven door `type: array` en een `items` -object dat het schema definieert van de items die de array accepteert.

U kunt array-items definiëren met behulp van primitieve typen, zoals een array van tekenreeksen:

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a primitive type.",
  "type": "array",
  "items": {
    "type": "string"
  }
}
```

U kunt de array-items ook definiëren op basis van een bestaand gegevenstype door via een eigenschap `$ref` naar de eigenschap `$id` van het gegevenstype te verwijzen. Hieronder ziet u een array van [!UICONTROL Payment Item] -objecten:

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a data type reference.",
  "type": "array",
  "items": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}
```

## [!UICONTROL Object] {#object}

[!UICONTROL Object] -velden worden aangegeven door `type: object` en een `properties` -object dat subeigenschappen voor het schemaveld definieert.

Het subveld dat onder `properties` wordt gedefinieerd, kan worden gedefinieerd met elke primitieve waarde `type` of door te verwijzen naar een bestaand gegevenstype via een eigenschap `$ref` die verwijst naar de eigenschap `$id` van het gegevenstype in kwestie:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field.",
  "type": "object",
  "properties": {
    "field1": {
      "type": "string"
    },
    "field2": {
      "$ref": "https://ns.adobe.com/xdm/common/measure"
    }
  }
}
```

U kunt ook het gehele object definiëren door naar een gegevenstype te verwijzen, op voorwaarde dat het gegevenstype in kwestie zelf is gedefinieerd als `type: object` :

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL Map] {#map}

Een kaartgebied is hoofdzakelijk een [`object` - type gebied ](#object) met een onbeperkte reeks sleutels. Kaarten hebben net als objecten de waarde `type` `object` , maar hun `meta:xdmType` is expliciet ingesteld op `map` .

Een kaart **moet** geen eigenschappen bepalen. Het **moet** één enkel `additionalProperties` schema bepalen om het type van waarden te beschrijven binnen de kaart (elke kaart kan slechts één enkel gegevenstype bevatten). De `type` -waarde moet `string` of `integer` zijn.

Een kaartveld met tekenreekswaarden wordt bijvoorbeeld als volgt gedefinieerd:

```json
"sampleField": {
  "title": "Sample Map Field",
  "description": "An example map field.",
  "type": "object",
  "meta:xdmType": "map",
  "additionalProperties": {
    "type": "string"
  }
}
```

Zie de onderstaande sectie voor meer informatie over het maken van aangepaste kaartvelden.

### Aangepaste toewijzingstypen maken {#custom-maps}

Om &#39;map-like&#39; gegevens efficiënt te ondersteunen in XDM, kunnen objecten worden voorzien van een annotatie `meta:xdmType` ingesteld op `map` om duidelijk te maken dat een object moet worden beheerd alsof de toetsenset onbeperkt is. Gegevens die in kaartvelden worden ingevoerd, moeten tekenreekssleutels gebruiken en alleen tekenreeks- of gehele-getalwaarden (zoals bepaald door `additionalProperties.type` ).

XDM stelt de volgende beperkingen op het gebruik van deze opslagwenk:

* Kaarttypen MOETEN van het type `object` zijn.
* Voor typen toewijzingen MOET GEEN eigenschap zijn gedefinieerd (met andere woorden, ze definiëren &quot;lege&quot; objecten).
* Kaarttypen MOETEN een `additionalProperties.type` -veld bevatten dat de waarden beschrijft die binnen de kaart kunnen worden geplaatst, `string` of `integer` .

Zorg ervoor dat u kaart-type gebieden wanneer absoluut noodzakelijk slechts gebruikt, aangezien zij de volgende prestatiesnadelen dragen:

* De tijd van de reactie van [ de Dienst van de Vraag van Adobe Experience Platform ](../../query-service/home.md) degradeert van drie seconden aan tien seconden voor 100 miljoen verslagen.
* Kaarten moeten minder dan 16 sleutels hebben of anders risico op verdere afbraak.

De gebruikersinterface van Experience Platform heeft ook beperkingen in de manier waarop de sleutels van map-type gebieden kunnen halen. Terwijl objecttekstvelden kunnen worden uitgebreid, worden kaarten als één veld weergegeven.

## Volgende stappen

In deze handleiding wordt beschreven hoe u verschillende veldtypen in de API definieert. Voor meer informatie hoe de XDM gebiedstypes geformatteerd zijn, zie de gids op [ XDM gebiedstype beperkingen ](../schema/field-constraints.md).
