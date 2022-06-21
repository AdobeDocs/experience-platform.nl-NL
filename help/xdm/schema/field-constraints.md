---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;veldgroep;Veldgroep;Veldgroepen;veldgroepen;gegevenstype;gegevenstypen;Gegevenstypen;Gegevenstype;schemaontwerp;datatype;Datatype;Gegevenstype;Schema's;Schema's;Schema-ontwerp;Kaart;Kaart;
solution: Experience Platform
title: Beperkingen voor XDM-veldtypen
topic-legacy: overview
description: Een verwijzing voor gebiedstype beperkingen in het Model van Gegevens van de Ervaring (XDM), met inbegrip van de andere rangschikkingsformaten zij aan en kunnen worden in kaart gebracht hoe te om uw eigen gebiedstypes in API te bepalen.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 2a58236031834bbe298576e2fcab54b04ec16ac3
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# Beperkingen voor XDM-veldtypen

In schema&#39;s van het Model van Gegevens van de Ervaring (XDM), beperkt het type van een gebied welk soort gegevens het gebied kan bevatten. Dit document biedt een overzicht van elk kernveldtype, inclusief de andere serialisatie-indelingen waaraan ze kunnen worden toegewezen en hoe u uw eigen veldtypen in de API kunt definiëren om verschillende beperkingen af te dwingen.

## Aan de slag

Lees voordat u deze handleiding gebruikt de [grondbeginselen van de schemacompositie](./composition.md) voor een inleiding aan schema&#39;s XDM, klassen, en groepen van het schemagebied.

Als u van plan bent om uw eigen veldtypen in de API te definiëren, wordt u ten zeerste aangeraden om te beginnen met de [Handleiding voor ontwikkelaars van het schema Register](../api/getting-started.md) voor meer informatie over het maken van veldgroepen en gegevenstypen waarin u aangepaste velden kunt opnemen. Als u de interface van het Experience Platform gebruikt om uw schema&#39;s tot stand te brengen, zie de gids op [velden definiëren in de gebruikersinterface](../ui/fields/overview.md) leren hoe u beperkingen implementeert op velden die u definieert binnen aangepaste veldgroepen en gegevenstypen.

## Basisstructuur en voorbeelden {#basic-types}

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

Met de API voor het schemaregister kunt u aangepaste velden definiëren met behulp van indelingen en optionele beperkingen. Zie de handleiding op [aangepaste velden definiëren in de API voor het schemaregister](../tutorials/custom-fields-api.md) voor meer informatie .
