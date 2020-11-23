---
keywords: Experience Platform;home;popular topics;schema;Schema;mixin;Mixin;Mixins;mixins;data type;data types;Data types;Data type;schema design;datatype;Datatype;data type;Data type;schemas;Schemas;Schema design;map;Map;
solution: Experience Platform
title: Beperkingen voor XDM-veldtypen
topic: overview
description: Een verwijzing voor XDM gebiedstype beperkingen, met inbegrip van de andere rangschikkingsformaten zij aan kunnen worden in kaart gebracht en hoe te om uw eigen gebiedstypes in API te bepalen.
translation-type: tm+mt
source-git-commit: e92294b9dcea37ae2a4a398c9d3397dcf5aa9b9e
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 2%

---


# Beperkingen voor XDM-veldtypen

De XDM gebiedstypes u voor uw schema&#39;s selecteert beperken welke soorten gegevens die gebieden kunnen bevatten. Dit document biedt een overzicht van elk kernveldtype, inclusief de andere serialisatie-indelingen waaraan ze kunnen worden toegewezen, en hoe u uw eigen veldtypen in de API kunt definiëren om verschillende beperkingen af te dwingen.

## Aan de slag

Alvorens deze gids te gebruiken, te herzien gelieve de [grondbeginselen van schemacompositie](./composition.md) voor een inleiding aan schema XDM, klassen, en mixins.

Als u op het bepalen van uw eigen gebiedstypes van plan bent, adviseert men sterk dat u met de de ontwikkelaarsgids [van de Registratie van het](../api/getting-started.md) Schema begint om te leren hoe te om mengen en gegevenstypes tot stand te brengen om uw douanegebieden in te omvatten.

## XDM-typen toewijzen aan andere indelingen

In de onderstaande tabel wordt de toewijzing tussen elk XDM-type (`meta:xdmType`) en andere serialisatie-indelingen beschreven.

| XDM Type<br>(meta:xdmType) | JSON<br>(JSON-schema) | Parquet<br>(type/aantekening) | [!DNL Spark] SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aerospike | Protocol 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | tekst:tekenreeks | BYTE_ARRAY/UTF8 | StringType | java.lang.String | Tekenreeks | System.String | Tekenreeks | string | Tekenreeks | string |
| getal | tekst:nummer | DUBBEL | DoubleType | java.lang.Double | Dubbel | System.Double | Getal | double | Dubbel | double |
| lang | type:<br>integerMaximum:2^53+1<br>minimum:-2^53+1 | INT64 | LongType | java.lang.Long | Lang | System.Int64 | Getal | lang | Geheel | int64 |
| int | type:<br>integerMaximum:2^31<br>minimum:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Getal | int | Geheel | int32 |
| kort | type:<br>integerMaximum:2^15<br>minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Kort | System.Int16 | Getal | int | Geheel | int32 |
| byte | type:<br>integerMaximum:2^7<br>minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Byte | System.SByte | Getal | int | Geheel | int32 |
| boolean | type:boolean | BOOLEAN | BooleanType | java.lang.Boolean | Boolean | System.Boolean | Boolean | bool | Geheel | Geheel | bool |
| date | type:<br>stringformat:date<br>(RFC 3339, sectie 5.6) | INT32/DATE | DateType | java.util.Date | java.util.Date | System.DateTime | Tekenreeks | date | Geheel getal<br>(unix millis) | int64<br>(unix millis) |
| date-time | type:<br>stringnotatie:date-time<br>(RFC 3339, sectie 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | Tekenreeks | timestamp | Geheel getal<br>(unix millis) | int64<br>(unix millis) |
| map | object | MAP geannoteerde groep<br><br>&lt;<span>key_type</span>> MOET STRING<br><br>&lt;<span>value_type</span>> type kaartwaarden zijn | MapType<br><br>&quot;keyType&quot; MOET StringType<br><br>&quot;valueType&quot; zijn type toewijzingswaarden. | java.util.Map | Kaart | --- | object | object | map | map&lt;<span>key_type, value_type</span>> |

## XDM-veldtypen definiëren in de API {#define-fields}

De schema&#39;s XDM worden bepaald gebruikend de normen van het Schema [JSON en basisgebiedstypes, met extra beperkingen voor gebiedsnamen die door worden afgedwongen](https://json-schema.org/) [!DNL Experience Platform]. Met de API [voor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) schemaregistratie kunt u aanvullende veldtypen definiëren door indelingen en optionele beperkingen te gebruiken. De XDM gebiedstypes worden blootgesteld door het gebied-vlakke attribuut, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` is een door het systeem gegenereerde waarde en daarom hoeft u deze eigenschap niet aan de JSON toe te voegen voor uw veld. De beste manier is om JSON-schematypen (zoals een tekenreeks en een geheel getal) te gebruiken met de juiste min/max-beperkingen zoals gedefinieerd in de onderstaande tabel.

In de volgende tabel wordt de juiste opmaak beschreven voor het definiëren van scalaire veldtypen en meer specifieke veldtypen met behulp van optionele eigenschappen. Meer informatie over optionele eigenschappen en type-specifieke trefwoorden is beschikbaar via de documentatie [van het](https://json-schema.org/understanding-json-schema/reference/type.html)JSON-schema.

Zoek eerst het gewenste veldtype en gebruik de voorbeeldcode om uw API-aanvraag samen te stellen voor het [maken van een mix](../api/mixins.md#create) of het [maken van een gegevenstype](../api/data-types.md#create).

<table>
  <tr>
    <th>Gewenst type<br/>(meta:xdmType)</th>
    <th>JSON<br/>(JSON-schema)</th>
    <th>Codevoorbeeld</th>
  </tr>
  <tr>
    <td>string</td>
    <td>type:<br/><br/><strong>stringOptional eigenschappen:</strong><br/>
      <ul>
        <li>patroon</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "pattern": "^[A-Z]{2}$", "maxLength": 2}
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>type:<br/>tekenreeksindeling: uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "uri" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType: tekenreeks)</td>
    <td>type:<br/><br/><strong>stringOptional, eigenschap:</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>Geef labels voor klantgerichte opties op met "meta:enum":
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "enum": [ "value1", "value2", "value3" ], "meta:enum": { "value1": "Waarde 1", "waarde2": "Waarde 2", "waarde3": "Value 3" }, "default": "value1" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>getal</td>
    <td>type: minimum<br/>aantal: ±2,23×10^308<br/>maximaal: ±1,80×10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "number" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>lang</td>
    <td>type:<br/>integerMaximum:2^53+1<br>minimum:-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "minimum": -9007199254740992, "maximum": 9007199254740992 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>type:<br/>integerMaximum:2^31<br>minimum:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "minimum": -2147483648, "maximum": 2147483648 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>kort</td>
    <td>type:<br/>integerMaximum:2^15<br>minimum:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "minimum": -32768, "maximum": 32768 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>byte</td>
    <td>type:<br/>integerMaximum:2^7<br>minimum:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "integer", "minimum": -128, "maximum": } 128
      </pre>
    </td>
  </tr>
  <tr>
    <td>boolean</td>
    <td><br/>type: boolean<br/>{true, false}<br/><br/><strong>Optional property:</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "boolean", "default": false }
      </pre>
    </td>
  </tr>
  <tr>
    <td>date</td>
    <td>type:<br/>tekenreeksindeling: date</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "date", "examples": ["2004-10-23"] }
      </pre>
      Datum zoals gedefinieerd in <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339, punt 5.6</a>, waarbij "full-date" = date-fullyear "-" date-month "-" date-mday (YYYY-MM-DD)
    </td>
  </tr>
  <tr>
    <td>date-time</td>
    <td>type:<br/>tekenreeksindeling: date-time</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "string", "format": "date-time", "examples": ["2004-10-23T12:00:00-06:00"] }
      </pre>
      Datum-tijd zoals bepaald door <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 339, punt 5.6</a>, waar "date-time" = full-date "T" full-time:<br/>(YYYY-MM-DD'T'HH:MM:SS.SSX)
    </td>
  </tr>
  <tr>
    <td>array</td>
    <td>type: array</td>
    <td>items.type kan worden gedefinieerd met elk scalair type:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "array", "items": { "type": "string" } }
      </pre>
      Array van objecten die door een ander schema worden gedefinieerd:<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "array", "items": { "$ref": "id" }
      </pre>
      Hierbij is 'id' de {id} van het referentieschema.
    </td>
  </tr>
  <tr>
    <td>object</td>
    <td>type: object</td>
    <td>eigenschappen.{field}.type kan worden gedefinieerd met elk scalair type:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "eigenschappen": {1} "field1": { "type": "string" }, "field2": { "type": "number" } } }
      </pre>
      Veld van type "object" dat wordt gedefinieerd door een referentieschema:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "$ref": "id" }
      </pre>
      Hierbij is 'id' de {id} van het referentieschema.
    </td>
  </tr>
  <tr>
    <td>map</td>
    <td>type:<br/><br/><strong>objectNote:</strong><br/>Het gebruik van het gegevenstype 'map' is gereserveerd voor gebruik in de industrie en het schema van leveranciers en is niet beschikbaar voor gebruik in door huurders gedefinieerde velden. Het wordt gebruikt in standaardschema's wanneer het gegeven als sleutels wordt vertegenwoordigd die aan één of andere waarde in kaart brengen, of waar de sleutels redelijkerwijs niet in een statisch schema kunnen worden omvat en als gegevenswaarden moeten worden behandeld.</td>
    <td>A 'map' MAG GEEN eigenschappen definiëren. Het MOET één "[!UICONTROL additionalProperties]"-schema definiëren om het type waarden in de 'map' te beschrijven. Een 'map' in XDM kan slechts één gegevenstype bevatten. Waarden kunnen elke geldige XDM-schemadefinitie zijn, inclusief een array of een object, of als verwijzing naar een ander schema (via $ref).<br/><br/>Veld toewijzen met waarden van het type 'string':
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "additionalProperties":{ "type": "string" } }
      </pre>
    Veld toewijzen met waarden die een array van tekenreeksen zijn:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "additionalProperties":{ "type": "array", "items": { "type": "string" } } }
      </pre>
    Het gebied van de kaart dat verwijzingen een ander schema:
      <pre class="JSON language-JSON hljs">
        "sampleField": { "type": "object", "additionalProperties":{ "$ref": "id" }
      </pre>
      Hierbij is 'id' de {id} van het referentieschema.
    </td>
  </tr>
</table>
