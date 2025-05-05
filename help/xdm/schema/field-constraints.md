---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;veldgroep;Veldgroep;Veldgroepen;Veldgroepen;Gegevenstype;Gegevenstypen;Gegevenstype;Schema-ontwerp;Datatype;Datatype;Gegevenstype;Schema's;Schema's;Schema-ontwerp;Kaart;Kaart;
solution: Experience Platform
title: Beperkingen voor XDM-veldtypen
description: Een verwijzing voor gebiedstype beperkingen in het Model van Gegevens van de Ervaring (XDM), met inbegrip van de andere rangschikkingsformaten zij aan en kunnen worden in kaart gebracht hoe te om uw eigen gebiedstypes in API te bepalen.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Beperkingen voor XDM-veldtypen

In schema&#39;s van het Model van Gegevens van de Ervaring (XDM), beperkt het type van een gebied welk soort gegevens het gebied kan bevatten. Dit document biedt een overzicht van elk kernveldtype, inclusief de andere serialisatie-indelingen waaraan ze kunnen worden toegewezen en hoe u uw eigen veldtypen in de API kunt definiëren om verschillende beperkingen af te dwingen.

## Aan de slag

Alvorens deze gids te gebruiken, te herzien gelieve de [ grondbeginselen van schemacompositie ](./composition.md) voor een inleiding aan schema XDM, klassen, en groepen van het schemagebied.

Als u van plan bent om uw eigen gebiedstypes in API te bepalen, adviseert men sterk dat u met de [ de ontwikkelaarsgids van de Registratie van het Schema ](../api/getting-started.md) begint om te leren hoe te om gebiedsgroepen en gegevenstypes tot stand te brengen om uw douanegebieden in te omvatten. Als u Experience Platform UI gebruikt om uw schema&#39;s tot stand te brengen, zie de gids op [ bepalende gebieden in UI ](../ui/fields/overview.md) leren hoe te om beperkingen op gebieden uit te voeren die u binnen de groepen van het douanegebied en gegevenstypes bepaalt.

## Basisstructuur en voorbeelden {#basic-types}

XDM wordt gebouwd bovenop het Schema van JSON, en daarom erven de gebieden XDM een gelijkaardige syntaxis wanneer het bepalen van hun type. Begrijpen hoe de verschillende gebiedstypes in het Schema JSON worden vertegenwoordigd kan helpen op de basisbeperkingen van elk type wijzen. Namen van aangepaste velden zijn hoofdlettergevoelig en moeten verschillende namen hebben op hetzelfde niveau in het schema.

>[!NOTE]
>
>Zie de [ API grondbeginselen gids ](../../landing/api-fundamentals.md#json-schema) voor meer informatie over Schema JSON en andere onderliggende technologieën in Experience Platform APIs.

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
      <td>[!UICONTROL Number]</td>
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
&lbrace;
  "type": "integer",
  "maximum": 9007199254740991,
  "minimum": -9007199254740991
&rbrace;</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "integer",
  "maximum": 2147483648,
  "minimum": -2147483648
&rbrace;</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "integer",
  "maximum": 32768,
  "minimum": -32768
&rbrace;</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "integer",
  "maximum": 128,
  "minimum": -128
&rbrace;</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Date]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "string",
  "format": "date"
&rbrace;</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "string",
  "format": "date-time"
&rbrace;</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Boolean]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "boolean"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**Alle datum-geformatteerde koorden moeten met ISO 8601 norm ([ RFC 3339, sectie 5.6 ](https://tools.ietf.org/html/rfc3339#section-5.6) in overeenstemming zijn).*

## XDM-typen toewijzen aan andere indelingen

In de onderstaande secties wordt beschreven hoe elk XDM-type wordt toegewezen aan andere algemene serialisatie-indelingen:

* [Parquet, Spark SQL en Java](#parquet)
* [Scala, .NET en CosmosDB](#scala)
* [MongoDB, Aerospike en Protobuf 2](#mongo)

>[!NOTE]
>
>Onder de standaard XDM-typen die in de onderstaande tabellen worden vermeld, wordt ook het [!UICONTROL Map] -type opgenomen. Kaarten worden gebruikt in standaardschema&#39;s wanneer de gegevens als sleutels worden vertegenwoordigd die aan bepaalde waarden in kaart brengen, of waar de sleutels redelijkerwijs niet in een statisch schema kunnen worden omvat en als gegevenswaarden moeten worden behandeld.
>
>Vele standaardXDM componenten gebruiken kaarttypes, en u kunt ook [ gebieden van de douanekaart ](../tutorials/custom-fields-api.md#custom-maps) bepalen indien gewenst. De opname van het kaarttype in de onderstaande tabellen is bedoeld om u te helpen bepalen hoe u uw bestaande gegevens kunt toewijzen aan XDM als deze momenteel zijn opgeslagen in een van de hieronder vermelde indelingen.

### Parquet, Spark SQL en Java {#parquet}

| XDM-type | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL String] | Type: `BYTE_ARRAY`<br> annotatie: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Number] | Type: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Long] | Type: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Integer] | Type: `INT32`<br> annotatie: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Short] | Type: `INT32`<br> annotatie: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | Type: `INT32`<br> annotatie: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Date] | Type: `INT32`<br> annotatie: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | Type: `INT64`<br> annotatie: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Boolean] | Type: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Map] | `MAP` -annoated group <br><br> (`<key-type>` moet `STRING` zijn) | `MapType`<br><br> (`keyType` must be `StringType`) | `java.util.Map` |

{style="table-layout:auto"}

### Scala, .NET en CosmosDB {#scala}

| XDM-type | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL String] | `String` | `System.String` | `String` |
| [!UICONTROL Number] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Long] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Integer] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Short] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Date] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Boolean] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Map] | `Map` | (N.v.t.) | `object` |

{style="table-layout:auto"}

### MongoDB, Aerospike en Protobuf 2 {#mongo}

| XDM-type | MongoDB | Aerospike | Protocol 2 |
| --- | --- | --- | --- |
| [!UICONTROL String] | `string` | `String` | `string` |
| [!UICONTROL Number] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL Integer] | `int` | `Integer` | `int32` |
| [!UICONTROL Short] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Date] | `date` | `Integer`<br> (Unix milliseconds) | `int64`<br> (Unix milliseconds) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br> (Unix milliseconds) | `int64`<br> (Unix milliseconds) |
| [!UICONTROL Boolean] | `bool` | `Integer`<br> (0/1 binair) | `bool` |
| [!UICONTROL Map] | `object` | `map` | `map<key_type, value_type>` |

{style="table-layout:auto"}

## XDM-veldtypen definiëren in de API {#define-fields}

Met de API voor het schemaregister kunt u aangepaste velden definiëren met behulp van indelingen en optionele beperkingen. Zie de gids op [ bepalend douanegebieden in de Registratie API van het Schema ](../tutorials/custom-fields-api.md) voor meer informatie.
