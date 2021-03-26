---
keywords: Experience Platform;home;populaire onderwerpen;schema;schema;Schema;mixin;Mixin;Mixins;gegevenstype;gegevenstype;gegevenstypen;Gegevenstypen;Gegevenstype;schemaontwerp;datatype;gegevenstype;Gegevenstype;schema's;Schema's;Schema-ontwerp;kaart;Kaart;
solution: Experience Platform
title: Beperkingen voor XDM-veldtypen
topic: ' - overzicht'
description: Een verwijzing voor gebiedstype beperkingen in het Model van Gegevens van de Ervaring (XDM), met inbegrip van de andere rangschikkingsformaten zij aan en kunnen worden in kaart gebracht hoe te om uw eigen gebiedstypes in API te bepalen.
translation-type: tm+mt
source-git-commit: bb5880340ca4c01d0b25c7cb16fd422d3182a89e
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 1%

---


# Beperkingen voor XDM-veldtypen

In schema&#39;s van het Model van Gegevens van de Ervaring (XDM), beperkt het type van een gebied welk soort gegevens het gebied kan bevatten. Dit document biedt een overzicht van elk kernveldtype, inclusief de andere serialisatie-indelingen waaraan ze kunnen worden toegewezen en hoe u uw eigen veldtypen in de API kunt definiëren om verschillende beperkingen af te dwingen.

## Aan de slag

Alvorens deze gids te gebruiken, te herzien gelieve de [grondbeginselen van schemacompositie](./composition.md) voor een inleiding aan schema XDM, klassen, en mengen.

Als u van plan bent om uw eigen gebiedstypes in API te bepalen, adviseert men sterk dat u met [de ontwikkelaarsgids van de Registratie van het Schema](../api/getting-started.md) begint om te leren hoe te om mengen en gegevenstypes tot stand te brengen om uw douanevelden in te omvatten. Als u het Experience Platform UI gebruikt om uw schema&#39;s tot stand te brengen, zie de gids op [het bepalen van gebieden in UI](../ui/fields/overview.md) leren hoe invoert beperkingen op gebieden die u binnen douanemengsels en gegevenstypes bepaalt.

## Basisstructuur en voorbeelden

XDM wordt gebouwd bovenop het Schema van JSON, en daarom erven de gebieden XDM een gelijkaardige syntaxis wanneer het bepalen van hun type. Begrijpen hoe de verschillende gebiedstypes in het Schema JSON worden vertegenwoordigd kan helpen op de basisbeperkingen van elk type wijzen.

>[!NOTE]
>
>Zie de [handleiding voor API-basisbeginselen](../../landing/api-fundamentals.md#json-schema) voor meer informatie over JSON-schema en andere onderliggende technologieën in Platform-API&#39;s.

In de volgende tabel wordt beschreven hoe elk XDM-type wordt vertegenwoordigd in JSON-schema, samen met een voorbeeldwaarde die overeenkomt met het type:

<table>
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
{
  "type": "integer",
  "maximum": 9007199254740991,
  "minimum": -9007199254740991
}</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL-geheel getal]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "maximum": 2147483648,
  "minimum": -2147483648
}</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "maximum": 32768,
  "minimum": -32768
}</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL-byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "integer",
  "maximum": 128
  "minimum": -128
}</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Date]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "string",
  "formaat": "date"
}</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type": "string",
  "formaat": "date-time"
}</pre>
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

**Alle tekenreeksen met datumnotatie moeten voldoen aan de ISO 8601-standaard ([RFC 3339, sectie 5.6](https://tools.ietf.org/html/rfc3339#section-5.6)).*

## XDM-typen toewijzen aan andere indelingen

In de onderstaande secties wordt beschreven hoe elk XDM-type wordt toegewezen aan andere algemene serialisatie-indelingen:

* [Parquet, Spark SQL en Java](#parquet)
* [Scala, .NET en CosmosDB](#scala)
* [MongoDB, Aerospike en Protobuf 2](#mongo)

>[!IMPORTANT]
>
>Onder de standaard XDM types die in de lijsten hieronder worden vermeld, is het [!UICONTROL Map] type ook inbegrepen. Kaarten worden gebruikt in standaardschema&#39;s wanneer de gegevens als sleutels worden vertegenwoordigd die aan bepaalde waarden in kaart brengen, of waar de sleutels redelijkerwijs niet in een statisch schema kunnen worden omvat en als gegevenswaarden moeten worden behandeld.
>
>De kaart-type gebieden zijn gereserveerd voor industrie en verkopersschemagebruik en daarom kunnen niet in douanemiddelen worden gebruikt die u bepaalt. De opname van het kaarttype in de onderstaande tabellen is alleen bedoeld om u te helpen bepalen hoe u uw bestaande gegevens kunt toewijzen aan XDM als deze momenteel zijn opgeslagen in een van de hieronder vermelde indelingen.

### Parquet, Spark SQL en Java {#parquet}

| XDM-type | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL String] | Type: `BYTE_ARRAY`<br>Annotatie: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Double] | Type: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Long] | Type: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Integer] | Type: `INT32`<br>Annotatie: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Short] | Type: `INT32`<br>Annotatie: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | Type: `INT32`<br>Annotatie: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Date] | Type: `INT32`<br>Annotatie: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Type: `INT64`<br>Annotatie: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Boolean] | Type: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Map] | `MAP`-annotated group<br><br>(`<key-type>` must be  `STRING`) | `MapType`<br><br>(`keyType` moet zijn  `StringType`) | `java.util.Map` |

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

## XDM-veldtypen definiëren in de API {#define-fields}

Alle XDM gebieden worden bepaald gebruikend standaard [JSON Schema](https://json-schema.org/) beperkingen die op hun gebiedstype van toepassing zijn, met extra beperkingen voor gebiedsnamen die door [!DNL Experience Platform] worden afgedwongen. Met de API voor het schemaregister kunt u aanvullende veldtypen definiëren via het gebruik van indelingen en optionele beperkingen. XDM gebiedtypes worden blootgesteld door het gebied-vlakke attribuut, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` is een door het systeem gegenereerde waarde en daarom hoeft u deze eigenschap niet aan de JSON voor uw veld toe te voegen wanneer u de API gebruikt. De beste manier is om JSON-schematypen (zoals `string` en `integer`) te gebruiken met de juiste min/max-beperkingen zoals gedefinieerd in de onderstaande tabel.

In de volgende tabel ziet u de juiste opmaak voor het definiëren van verschillende veldtypen, inclusief die met optionele eigenschappen. Meer informatie over optionele eigenschappen en typespecifieke trefwoorden is beschikbaar via de [JSON-schemadocumentatie](https://json-schema.org/understanding-json-schema/reference/type.html).

Om te beginnen, vind het gewenste gebiedstype en gebruik de steekproefcode wordt verstrekt om uw API verzoek voor [het creëren van een mixin](../api/mixins.md#create) of [het creëren van een gegevenstype](../api/data-types.md#create) te bouwen.

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
"sampleField": {
    "type": "string",
    "patroon": "^[A-Z]{2}$",
    "maxLength": 2
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "formaat": "uri"
}</pre>
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
    <td>Beperkte opsommingswaarden worden verschaft onder de <code>enum</code>-array, terwijl optionele klantgerichte labels voor elke waarde kunnen worden opgegeven onder <code>meta:enum</code>:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Waarde 1",
      "value2": "Waarde 2",
      "value3": "Waarde 3"
  },
  "default": "value1"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL-nummer]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "number"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL-geheel getal]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "minimum": -2147483648,
  "maximum": 2147483648
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL short]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "minimum": -32768,
  "maximum": 32768
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL-byte]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "integer",
  "minimum": -128,
  "maximum": 128
  }</pre>
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
"sampleField": {
  "type": "boolean",
  "default": false
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL-datum]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "formaat": "date",
  "voorbeelden": ["2004-10-23"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "string",
  "formaat": "date-time",
  "voorbeelden": ["2004-10-23T12:00:00-06:00"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL-array]</td>
    <td></td>
    <td>Een array van elementaire scalaire typen (bijvoorbeeld tekenreeksen):
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "array",
  "objecten": {
    "type": "string"
  }
}</pre>
      Een array van objecten die door een ander schema worden gedefinieerd:<br/>
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "array",
  "objecten": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!Object UICONTROL]</td>
    <td></td>
    <td>Het <code>type</code>-kenmerk van elk subveld dat onder <code>properties</code> wordt gedefinieerd, kan met elk scalair type worden gedefinieerd:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "eigenschappen": {
    "field1": {
      "type": "string"
    },
    "field2": {
      "type": "number"
    }
  }
}</pre>
      Objecttype velden kunnen worden gedefinieerd door te verwijzen naar <code>$id</code> van een gegevenstype:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>Een kaart <strong>mag geen eigenschappen definiëren. </strong> Het <strong>must</strong> bepaalt één enkel <code>additionalProperties</code> schema om het type van waarden te beschrijven bevat binnen de kaart (elke kaart kan slechts één enkel gegevenstype bevatten). Waarden kunnen elk geldig XDM <code>type</code>-kenmerk zijn of een verwijzing naar een ander schema met een <code>$ref</code>-kenmerk.<br/><br/>Een toewijzingsveld met tekenreekswaarden:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "additionalProperties":{
    "type": "string"
  }
}</pre>
    Een toewijzingsveld met arrays van tekenreeksen voor waarden:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "additionalProperties":{
    "type": "array",
    "objecten": {
      "type": "string"
    }
  }
}</pre>
    Een kaartveld dat naar een ander gegevenstype verwijst:
      <pre class="JSON language-JSON hljs">
"sampleField": {
  "type": "object",
  "additionalProperties":{
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
</table>
