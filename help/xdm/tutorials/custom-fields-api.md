---
title: XDM-velden definiëren in de API voor schemaregister
description: Leer hoe u verschillende velden definieert bij het maken van XDM-bronnen (Custom Experience Data Model) in de Schema Registry API.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 6277725cd69bc94325d3584177742df1a7fd4f95
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 0%

---

# XDM-velden definiëren in de API voor het schemaregister

Alle velden van het Experience Data Model (XDM) worden gedefinieerd met de standaard [JSON Schema](https://json-schema.org/) beperkingen die van toepassing zijn op hun veldtype, met extra beperkingen voor veldnamen die door Adobe Experience Platform worden afgedwongen. Met de API voor het schemaregister kunt u aangepaste velden in uw schema&#39;s definiëren met behulp van indelingen en optionele beperkingen. De XDM gebiedstypes worden blootgesteld door het gebied-vlakke attribuut, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` is een door het systeem gegenereerde waarde en daarom hoeft u deze eigenschap niet aan de JSON voor uw veld toe te voegen wanneer u de API gebruikt (behalve wanneer [aangepaste kaarttypen maken](#custom-maps)). De beste manier is om JSON-schematypen te gebruiken (zoals `string` en `integer`) met de toepasselijke minimum/maximum-beperkingen zoals gedefinieerd in de onderstaande tabel.

In deze handleiding wordt de juiste opmaak beschreven voor het definiëren van verschillende veldtypen, inclusief die met optionele eigenschappen. Meer informatie over optionele eigenschappen en typespecifieke trefwoorden is beschikbaar via de [JSON-schemadocumentatie](https://json-schema.org/understanding-json-schema/reference/type.html).

Zoek eerst het gewenste veldtype en gebruik de voorbeeldcode om uw API-aanvraag voor [een veldgroep maken](../api/field-groups.md#create) of [een gegevenstype maken](../api/data-types.md#create).

## [!UICONTROL String] {#string}

[!UICONTROL String] velden worden aangegeven door `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

U kunt desgewenst beperken welke soorten waarden voor de tekenreeks kunnen worden ingevoerd via de volgende aanvullende eigenschappen:

* `pattern`: Een regex-patroon dat moet worden beperkt.
* `minLength`: Een minimumlengte voor de tekenreeks.
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

[!UICONTROL URI] velden worden aangegeven door `type: string` met een `format` eigenschap ingesteld op `uri`. Er worden geen andere eigenschappen geaccepteerd.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL Enum] {#enum}

[!UICONTROL Enum] velden moeten `type: string`, met de in een `enum` array:

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

U kunt klant-onder ogen ziet etiketten voor elke waarde naar keuze verstrekken onder a `meta:enum` eigenschap, waarbij elk label met een overeenkomstige waarde onder `enum`.

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
>De `meta:enum` waarde is **niet** een opsomming declareren of gegevensvalidatie zelfstandig uitvoeren. In de meeste gevallen worden tekenreeksen onder `meta:enum` ook `enum` om ervoor te zorgen dat gegevens worden beperkt. Er zijn echter gevallen waarin `meta:enum` wordt verstrekt zonder overeenkomstige `enum` array. Zie de zelfstudie aan [voorgestelde waarden definiëren](../tutorials/suggested-values.md) voor meer informatie .

U kunt desgewenst een `default` eigenschap om de standaardwaarde aan te geven `enum` waarde die het veld zal gebruiken als er geen waarde is opgegeven.

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
>Indien niet `default` waarde wordt opgegeven en het opsommingsveld wordt ingesteld op `required`, wordt een record zonder geaccepteerde waarde voor dit veld niet gevalideerd bij invoer.

## [!UICONTROL Number] {#number}

Getalvelden worden aangegeven door `type: number` en hebben geen andere vereiste eigenschappen.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` typen worden gebruikt voor elk numeriek type, gehele getallen of getallen met drijvende komma, terwijl [`integer` typen](#integer) worden specifiek voor integrale getallen gebruikt. Zie de [JSON-schemadocumentatie over numerieke typen](https://json-schema.org/understanding-json-schema/reference/numeric.html) voor meer informatie over de gebruiksgevallen voor elk type.

## [!UICONTROL Integer] {#integer}

[!UICONTROL Integer] velden worden aangegeven door `type: integer` en hebben geen andere vereiste velden.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>while `integer` de types verwijzen specifiek naar integrale aantallen; [`number` typen](#number) worden gebruikt voor numerieke typen, gehele getallen of getallen met drijvende komma. Zie de [JSON-schemadocumentatie over numerieke typen](https://json-schema.org/understanding-json-schema/reference/numeric.html) voor meer informatie over de gebruiksgevallen voor elk type.

U kunt optioneel het bereik van het gehele getal beperken door `minimum` en `maximum` eigenschappen aan de definitie. Verscheidene andere numerieke types die door de Bouwer UI van het Schema worden gesteund zijn enkel `integer` typen met specifieke `minimum` en `maximum` beperkingen, zoals [[!UICONTROL Long]](#long), [[!UICONTROL Short]](#short), en [[!UICONTROL Byte]](#byte).

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

Het equivalent van een [!UICONTROL Long] het gebied door de Bouwer van het Schema UI wordt gecreeerd is een [`integer` tekstveld](#integer) met specifieke `minimum` en `maximum` waarden (`-9007199254740992` en `9007199254740992`, respectievelijk).

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

Het equivalent van een [!UICONTROL Short] het gebied door de Bouwer van het Schema UI wordt gecreeerd is een [`integer` tekstveld](#integer) met specifieke `minimum` en `maximum` waarden (`-32768` en `32768`, respectievelijk).

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32768
}
```

## [!UICONTROL Byte] {#byte}

Het equivalent van een [!UICONTROL Byte] het gebied door de Bouwer van het Schema UI wordt gecreeerd is een [`integer` tekstveld](#integer) met specifieke `minimum` en `maximum` waarden (`-128` en `128`, respectievelijk).

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 128
}
```

## [!UICONTROL Boolean] {#boolean}

[!UICONTROL Boolean] velden worden aangegeven door `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

U kunt desgewenst een `default` De waarde die het veld zal gebruiken wanneer tijdens de invoer geen expliciete waarde wordt opgegeven.

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
>Indien niet `default` waarde wordt opgegeven en het Booleaanse veld wordt ingesteld op `required`, wordt een record zonder geaccepteerde waarde voor dit veld niet gevalideerd bij invoer.

## [!UICONTROL Date] {#date}

[!UICONTROL Date] velden worden aangegeven door `type: string` en `format: date`. U kunt desgewenst ook een array van `examples` aan hefboomwerking in gevallen waar u een koord van de steekproefdatum voor gebruikers wilt tonen die de gegevens manueel ingaan.

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

[!UICONTROL DateTime] velden worden aangegeven door `type: string` en `format: date-time`. U kunt desgewenst ook een array van `examples` aan hefboomwerking in gevallen waar u een steekproefdatetime koord voor gebruikers wilt tonen die de gegevens manueel ingaan.

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

[!UICONTROL Array] velden worden aangegeven door `type: array` en `items` object dat het schema definieert van de items die de array accepteert.

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

U kunt de arrayitems ook definiëren op basis van een bestaand gegevenstype door te verwijzen naar het `$id` van het gegevenstype via een `$ref` eigenschap. Het volgende is een array van [!UICONTROL Payment Item] objecten:

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

[!UICONTROL Object] velden worden aangegeven door `type: object` en `properties` object dat subeigenschappen voor het schemaveld definieert.

Elk subveld dat wordt gedefinieerd onder `properties` kan worden gedefinieerd met elke primitieve waarde `type` of door naar een bestaand gegevenstype te verwijzen via een `$ref` eigenschap die naar de `$id` van het betrokken gegevenstype:

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

U kunt ook het gehele object definiëren door naar een gegevenstype te verwijzen, op voorwaarde dat het gegevenstype in kwestie zelf is gedefinieerd als `type: object`:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL Map] {#map}

Een kaartveld is in wezen een [`object`-type, veld](#object) met een onbeperkte set toetsen. Kaarten hebben, net als objecten, een `type` waarde van `object`, maar `meta:xdmType` is expliciet ingesteld op `map`.

Een kaart **mogen** om het even welke eigenschappen bepalen. IT **moet** één `additionalProperties` schema om het type van waarden te beschrijven binnen de kaart (elke kaart kan slechts één enkel gegevenstype bevatten). De `type` waarde moet ofwel `string` of `integer`.

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

Om &quot;map-als&quot;gegevens efficiënt in XDM te steunen, kunnen de voorwerpen met a worden geannoteerd `meta:xdmType` instellen op `map` om duidelijk te maken dat een voorwerp zou moeten worden beheerd alsof de belangrijkste reeks onbeperkt was. Gegevens die in kaartvelden worden ingevoerd, moeten tekenreekssleutels gebruiken en alleen tekenreeks- of geheel-getalwaarden (zoals bepaald door `additionalProperties.type`).

XDM stelt de volgende beperkingen op het gebruik van deze opslagwenk:

* Type kaart MOET van het type zijn `object`.
* Voor typen toewijzingen MOET GEEN eigenschap zijn gedefinieerd (met andere woorden, ze definiëren &quot;lege&quot; objecten).
* Kaarttypen MOETEN een `additionalProperties.type` veld dat de waarden beschrijft die binnen de kaart kunnen worden geplaatst, of `string` of `integer`.

Zorg ervoor dat u kaart-type gebieden wanneer absoluut noodzakelijk slechts gebruikt, aangezien zij de volgende prestatiesnadelen dragen:

* Responstijd van [Adobe Experience Platform Query Service](../../query-service/home.md) degradeert van drie seconden tot tien seconden voor 100 miljoen verslagen.
* Kaarten moeten minder dan 16 sleutels hebben of anders risico op verdere afbraak.

De gebruikersinterface van het Platform heeft ook beperkingen in hoe het de sleutels van kaart-type gebieden kan halen. Terwijl objecttekstvelden kunnen worden uitgebreid, worden kaarten als één veld weergegeven.

## Volgende stappen

In deze handleiding wordt beschreven hoe u verschillende veldtypen in de API definieert. Zie de handleiding voor meer informatie over de opmaak van XDM-veldtypen [Beperkingen voor XDM-veldtypen](../schema/field-constraints.md).
