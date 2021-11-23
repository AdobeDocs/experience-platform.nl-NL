---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;veldgroep;Veldgroep;Veldgroepen;veldgroepen;gegevenstype;gegevenstypen;Gegevenstypen;Gegevenstype;schemaontwerp;datatype;Datatype;Gegevenstype;Schema's;Schema's;Schema-ontwerp;Kaart;Kaart;
solution: Experience Platform
title: Beperkingen voor XDM-veldtypen
topic-legacy: overview
description: Een verwijzing voor gebiedstype beperkingen in het Model van Gegevens van de Ervaring (XDM), met inbegrip van de andere rangschikkingsformaten zij aan en kunnen worden in kaart gebracht hoe te om uw eigen gebiedstypes in API te bepalen.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 684237122e7384f6c611e1c602c30af2518aba58
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 1%

---

# Beperkingen voor XDM-veldtypen

In schema&#39;s van het Model van Gegevens van de Ervaring (XDM), beperkt het type van een gebied welk soort gegevens het gebied kan bevatten. Dit document biedt een overzicht van elk kernveldtype, inclusief de andere serialisatie-indelingen waaraan ze kunnen worden toegewezen en hoe u uw eigen veldtypen in de API kunt definiëren om verschillende beperkingen af te dwingen.

## Aan de slag

Lees voordat u deze handleiding gebruikt de [grondbeginselen van de schemacompositie](./composition.md) voor een inleiding aan schema&#39;s XDM, klassen, en groepen van het schemagebied.

Als u van plan bent om uw eigen veldtypen in de API te definiëren, wordt u ten zeerste aangeraden om te beginnen met de [Handleiding voor ontwikkelaars van het schema Register](../api/getting-started.md) voor meer informatie over het maken van veldgroepen en gegevenstypen waarin u aangepaste velden kunt opnemen. Als u de interface van het Experience Platform gebruikt om uw schema&#39;s tot stand te brengen, zie de gids op [velden definiëren in de gebruikersinterface](../ui/fields/overview.md) leren hoe u beperkingen implementeert op velden die u definieert binnen aangepaste veldgroepen en gegevenstypen.

## Basisstructuur en voorbeelden

XDM wordt gebouwd bovenop het Schema van JSON, en daarom erven de gebieden XDM een gelijkaardige syntaxis wanneer het bepalen van hun type. Begrijpen hoe de verschillende gebiedstypes in het Schema JSON worden vertegenwoordigd kan helpen op de basisbeperkingen van elk type wijzen.

>[!NOTE]
>
>Zie de [Handleiding voor API-basisbeginselen](../../landing/api-fundamentals.md#json-schema) voor meer informatie over JSON Schema en andere onderliggende technologieën in Platform APIs.

In de volgende tabel wordt beschreven hoe elk XDM-type wordt vertegenwoordigd in JSON-schema, samen met een voorbeeldwaarde die overeenkomt met het type:

<table style="table-layout:auto">
  <thead>
    <tr>
      <th>XDM-type</th>
      <th>JSON Schema</th>
      <th>Voorbeeld</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[!UICONTROL String]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Double]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "number"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 9007199254740991, "minimum": -9007199254740991 }</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 2147483648, "minimum": -2147483648 }</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 32768, "minimum": -32768 }</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "integer", "maximum": 128, "minimum": -128 }</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Date]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "string", "format": "date" }</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type": "string", "format": "date-time" }</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Boolean]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**Alle tekenreeksen met datumnotatie moeten voldoen aan de ISO 8601-standaard ([RFC 3339, punt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## XDM-typen toewijzen aan andere indelingen

In de onderstaande secties wordt beschreven hoe elk XDM-type wordt toegewezen aan andere algemene serialisatie-indelingen:

* [Parquet, Spark SQL en Java](#parquet)
* [Scala, .NET en CosmosDB](#scala)
* [MongoDB, Aerospike en Protobuf 2](#mongo)

>[!IMPORTANT]
>
>Onder de standaard XDM types die in de lijsten hieronder worden vermeld, [!UICONTROL Map] type is ook opgenomen. Kaarten worden gebruikt in standaardschema&#39;s wanneer de gegevens als sleutels worden vertegenwoordigd die aan bepaalde waarden in kaart brengen, of waar de sleutels redelijkerwijs niet in een statisch schema kunnen worden omvat en als gegevenswaarden moeten worden behandeld.
>
>De kaart-type gebieden zijn gereserveerd voor industrie en verkopersschemagebruik en daarom kunnen niet in douanemiddelen worden gebruikt die u bepaalt. De opname van het kaarttype in de onderstaande tabellen is alleen bedoeld om u te helpen bepalen hoe u uw bestaande gegevens kunt toewijzen aan XDM als deze momenteel zijn opgeslagen in een van de hieronder vermelde indelingen.

### Parquet, Spark SQL en Java {#parquet}

| XDM-type | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL String] | Type: `BYTE_ARRAY`<br>Aantekening: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Double] | Type: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Long] | Type: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Integer] | Type: `INT32`<br>Aantekening: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Short] | Type: `INT32`<br>Aantekening: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | Type: `INT32`<br>Aantekening: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Date] | Type: `INT32`<br>Aantekening: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Type: `INT64`<br>Aantekening: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Boolean] | Type: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Map] | `MAP`-annotated group<br><br>(`<key-type>` moet `STRING`) | `MapType`<br><br>(`keyType` moet `StringType`) | `java.util.Map` |

{style=&quot;table-layout:auto&quot;}

### Scala, .NET en CosmosDB {#scala}

| XDM-type | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL String] | `String` | `System.String` | `String` |
| [!UICONTROL Double] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Long] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Integer] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Short] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Date] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Boolean] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Map] | `Map` | (N.v.t.) | `object` |

{style=&quot;table-layout:auto&quot;}

### MongoDB, Aerospike en Protobuf 2 {#mongo}

| XDM-type | MongoDB | Aerospike | Protocol 2 |
| --- | --- | --- | --- |
| [!UICONTROL String] | `string` | `String` | `string` |
| [!UICONTROL Double] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL Integer] | `int` | `Integer` | `int32` |
| [!UICONTROL Short] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Date] | `date` | `Integer`<br>(Unix milliseconds) | `int64`<br>(Unix milliseconds) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(Unix milliseconds) | `int64`<br>(Unix milliseconds) |
| [!UICONTROL Boolean] | `bool` | `Integer`<br>(0/1 binair) | `bool` |
| [!UICONTROL Map] | `object` | `map` | `map<key_type, value_type>` |

{style=&quot;table-layout:auto&quot;}

## XDM-veldtypen definiëren in de API {#define-fields}

Alle XDM-velden worden gedefinieerd met de standaard [JSON Schema](https://json-schema.org/) beperkingen die van toepassing zijn op hun veldtype, met extra beperkingen voor veldnamen die worden afgedwongen door [!DNL Experience Platform]. Met de API voor het schemaregister kunt u aanvullende veldtypen definiëren via het gebruik van indelingen en optionele beperkingen. De XDM gebiedstypes worden blootgesteld door het gebied-vlakke attribuut, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` is een door het systeem gegenereerde waarde en daarom hoeft u deze eigenschap niet aan de JSON voor uw veld toe te voegen wanneer u de API gebruikt. De beste manier is om JSON-schematypen te gebruiken (zoals `string` en `integer`) met de toepasselijke minimum/maximum-beperkingen zoals gedefinieerd in de onderstaande tabel.

In de volgende tabel ziet u de juiste opmaak voor het definiëren van verschillende veldtypen, inclusief die met optionele eigenschappen. Meer informatie over optionele eigenschappen en typespecifieke trefwoorden is beschikbaar via de [JSON-schemadocumentatie](https://json-schema.org/understanding-json-schema/reference/type.html).

Zoek eerst het gewenste veldtype en gebruik de voorbeeldcode om uw API-aanvraag voor [een veldgroep maken](../api/field-groups.md#create) of [een gegevenstype maken](../api/data-types.md#create).

<table style="table-layout:auto">
  <tr>
    <th>XDM-type</th>
    <th>Optionele eigenschappen</th>
    <th>Voorbeeld</th>
  </tr>
  <tr>
    <td>[!UICONTROL String]</td>
    <td>
      <ul>
        <li><code>pattern</code></li>
        <li><code>minLength</code></li>
        <li><code>maxLength</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "pattern": "^[A-Z]{2}$", "maxLength": 2}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "uri" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Enum]</td>
    <td>
      <ul>
        <li><code>default</code></li>
        <li><code>meta:enum</code></li>
      </ul>
    </td>
    <td>Beperkte opsommingswaarden worden opgegeven onder de <code>enum</code> array, terwijl optionele klantgerichte labels voor elke waarde onder <code>meta:enum</code>:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "enum": [ "value1", "value2", "value3" ], "meta:enum": { "value1": "Waarde 1", "waarde2": "Waarde 2", "waarde3": "Value 3" }, "default": "value1" }</pre>
    <br>De <code>meta:enum</code> waarde is <strong>niet</strong> een opsomming declareren of gegevensvalidatie zelfstandig uitvoeren. In de meeste gevallen worden tekenreeksen onder <code>meta:enum</code> ook <code>enum</code> om ervoor te zorgen dat gegevens worden beperkt. Er zijn echter gevallen waarin <code>meta:enum</code> wordt verstrekt zonder overeenkomstige <code>enum</code> array. Zie de zelfstudie aan <a href="../tutorials/extend-soft-enum.md">uitbreiden, zachte nummers</a> voor meer informatie .
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Number]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "number" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -9007199254740992, "maximum": 9007199254740992 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Integer]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -2147483648, "maximum": 2147483648 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Short]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -32768, "maximum": 32768 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Byte]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -128, "maximum": } 128</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Boolean]</td>
    <td>
      <ul>
        <li><code>default</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "boolean", "default": false }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Date]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "date", "examples": ["2004-10-23"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "date-time", "examples": ["2004-10-23T12:00:00-06:00"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Array]</td>
    <td></td>
    <td>Een array van elementaire scalaire typen (bijvoorbeeld tekenreeksen):
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "array", "items": { "type": "string" } }</pre>
      Een array met objecten die door een ander schema worden gedefinieerd:<br/>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "array", "items": { "$ref": "https://ns.adobe.com/xdm/data/paymentitem" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Object]</td>
    <td></td>
    <td>De <code>type</code> kenmerk van elk subveld dat wordt gedefinieerd onder <code>properties</code> kan worden gedefinieerd met elk scalair type:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "properties": {
    "field1": {
      "type": "string"
    },
    "field2": {
      "type": "number"
    }
  }
}</pre>
      Objecttype velden kunnen worden gedefinieerd door te verwijzen naar de <code>$id</code> van een gegevenstype:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>Een kaart <strong>mogen</strong> om het even welke eigenschappen bepalen. IT <strong>moet</strong> één <code>additionalProperties</code> schema om het type van waarden te beschrijven binnen de kaart (elke kaart kan slechts één enkel gegevenstype bevatten). Waarden kunnen elke geldige XDM zijn <code>type</code> kenmerk, of een verwijzing naar een ander schema met behulp van een <code>$ref</code> kenmerk.<br/><br/>Een toewijzingsveld met tekenreekswaarden:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "additionalProperties":{ "type": "string" } }</pre>
    Een toewijzingsveld met arrays van tekenreeksen voor waarden:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "additionalProperties":{ "type": "array", "items": { "type": "string" } } }</pre>
    Een kaartveld dat naar een ander gegevenstype verwijst:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "additionalProperties":{ "$ref": "https://ns.adobe.com/xdm/data/paymentitem" }</pre>
    </td>
  </tr>
</table>
