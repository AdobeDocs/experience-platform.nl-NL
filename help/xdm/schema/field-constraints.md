---
keywords: Experience Platform;home;populaire onderwerpen;schema;schema;Schema;mixin;Mixin;Mixins;gegevenstype;gegevenstype;gegevenstypen;Gegevenstypen;Gegevenstype;schemaontwerp;datatype;gegevenstype;Gegevenstype;schema's;Schema's;Schema-ontwerp;map;Kaart;
solution: Experience Platform
title: Beperkingen voor XDM-veldtypen
topic: overview
description: Een verwijzing voor XDM gebiedstype beperkingen, met inbegrip van de andere rangschikkingsformaten zij aan kunnen worden in kaart gebracht en hoe te om uw eigen gebiedstypes in API te bepalen.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 2%

---


# Beperkingen voor XDM-veldtypen

De XDM gebiedstypes u voor uw schema&#39;s selecteert beperken welke soorten gegevens die gebieden kunnen bevatten. Dit document biedt een overzicht van elk kernveldtype, inclusief de andere serialisatie-indelingen waaraan ze kunnen worden toegewezen, en hoe u uw eigen veldtypen in de API kunt definiëren om verschillende beperkingen af te dwingen.

## Aan de slag

Alvorens deze gids te gebruiken, te herzien gelieve de [grondbeginselen van schemacompositie](./composition.md) voor een inleiding aan schema XDM, klassen, en mengen.

Als u op het bepalen van uw eigen gebiedstypes van plan bent, adviseert men sterk dat u met [de ontwikkelaarsgids van de Registratie van het Schema](../api/getting-started.md) begint om te leren hoe te om mengen en gegevenstypes tot stand te brengen om uw douanevelden in te omvatten.

## XDM-typen toewijzen aan andere indelingen

De lijst hieronder beschrijft de afbeelding tussen elk type XDM (`meta:xdmType`) en andere rangschikkingsformaten.

| XDM Type<br>(meta:xdmType) | JSON<br>(JSON-schema) | Parquet<br>(type/annotatie) | [!DNL Spark] SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aerospike | Protocol 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | tekst:tekenreeks | BYTE_ARRAY/UTF8 | StringType | java.lang.String | Tekenreeks | System.String | Tekenreeks | string | Tekenreeks | string |
| getal | tekst:nummer | DUBBEL | DoubleType | java.lang.Double | Dubbel | System.Double | Getal | double | Dubbel | double |
| lang | type:integer<br>maximum:2^53+1<br>minimum:-2^53+1 | INT64 | LongType | java.lang.Long | Lang | System.Int64 | Getal | lang | Geheel | int64 |
| int | type:integer<br>maximum:2^31<br>minimum:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Getal | int | Geheel | int32 |
| kort | type:integer<br>maximum:2^15<br>minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Kort | System.Int16 | Getal | int | Geheel | int32 |
| byte | type:integer<br>maximum:2^7<br>minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Byte | System.SByte | Getal | int | Geheel | int32 |
| boolean | type:boolean | BOOLEAN | BooleanType | java.lang.Boolean | Boolean | System.Boolean | Boolean | bool | Geheel | Geheel | bool |
| date | type:string<br>format:date<br>(RFC 3339, sectie 5.6) | INT32/DATE | DateType | java.util.Date | java.util.Date | System.DateTime | Tekenreeks | date | Integer<br>(unix millis) | int64<br>(unix millis) |
| date-time | type:string<br>format:date-time<br>(RFC 3339, sectie 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | Tekenreeks | timestamp | Integer<br>(unix millis) | int64<br>(unix millis) |
| map | object | Gemannoteerde MAP groep<br><br>&lt;<span>key_type</span>> MOET STRING<br><br>&lt;<span>value_type</span>> type kaartwaarden zijn | MapType<br><br>&quot;keyType&quot; MOET StringType<br><br>&quot;valueType&quot; is het type kaartwaarden. | java.util.Map | Kaart | — | object | object | map | map&lt;<span>key_type, value_type</span>> |

## XDM-veldtypen definiëren in de API {#define-fields}

XDM schema&#39;s worden bepaald gebruikend [JSON Schema](https://json-schema.org/) normen en basisgebiedstypes, met extra beperkingen voor gebiedsnamen die door [!DNL Experience Platform] worden afgedwongen. Met de [Schemaregistratie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) kunt u aanvullende veldtypen definiëren door het gebruik van indelingen en optionele beperkingen. XDM gebiedtypes worden blootgesteld door het gebied-vlakke attribuut, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` is een door het systeem gegenereerde waarde en daarom hoeft u deze eigenschap niet aan de JSON toe te voegen voor uw veld. De beste manier is om JSON-schematypen (zoals een tekenreeks en een geheel getal) te gebruiken met de juiste min/max-beperkingen zoals gedefinieerd in de onderstaande tabel.

In de volgende tabel wordt de juiste opmaak beschreven voor het definiëren van scalaire veldtypen en meer specifieke veldtypen met behulp van optionele eigenschappen. Meer informatie over optionele eigenschappen en typespecifieke trefwoorden is beschikbaar via de [JSON-schemadocumentatie](https://json-schema.org/understanding-json-schema/reference/type.html).

Om te beginnen, vind het gewenste gebiedstype en gebruik de steekproefcode wordt verstrekt om uw API verzoek voor [het creëren van een mixin](../api/mixins.md#create) of [het creëren van een gegevenstype](../api/data-types.md#create) te bouwen.

<table>
  <tr>
    <th>Gewenst type<br/>(meta:xdmType)</th>
    <th>JSON<br/>(JSON-schema)</th>
    <th>Codevoorbeeld</th>
  </tr>
  <tr>
    <td>string</td>
    <td>type: string<br/><br/><strong>Optionele eigenschappen:</strong><br/>
      <ul>
        <li>patroon</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
            "type": "string",
            "patroon": "^[A-Z]{2}$",
            "maxLength": 2
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>type: string<br/>format: uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "formaat": "uri"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType: tekenreeks)</td>
    <td>type: string<br/><br/><strong>Optionele eigenschap:</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>Geef labels voor klantgerichte opties op met "meta:enum":
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
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>getal</td>
    <td>type: getal<br/>minimum: ±2,23×10^308<br/>maximaal: ±1,80×10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "number"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>lang</td>
    <td>type: integer<br/>maximum:2^53+1<br>minimum:-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimum": -9007199254740992,
          "maximum": 9007199254740992
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>type: integer<br/>maximum:2^31<br>minimum:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimum": -2147483648,
          "maximum": 2147483648
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>kort</td>
    <td>type: integer<br/>maximum:2^15<br>minimum:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimum": -32768,
          "maximum": 32768
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>byte</td>
    <td>type: integer<br/>maximum:2^7<br>minimum:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "integer",
          "minimum": -128,
          "maximum": 128
          }
      </pre>
    </td>
  </tr>
  <tr>
    <td>boolean</td>
    <td><br/>type: boolean<br/>{true, false}<br/><br/><strong>Optionele eigenschap:</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "boolean",
          "default": false
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>date</td>
    <td>type: string<br/>format: date</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "formaat": "date",
          "voorbeelden": ["2004-10-23"]
        }
      </pre>
      Datum zoals gedefinieerd in <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 339, sectie 5.6</a>, waarbij "full-date" = date-fullyear "-" date-month "-" date-mday (YYYY-MM-DD)
    </td>
  </tr>
  <tr>
    <td>date-time</td>
    <td>type: string<br/>format: date-time</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "string",
          "formaat": "date-time",
          "voorbeelden": ["2004-10-23T12:00:00-06:00"]
        }
      </pre>
      Datum-tijd zoals bepaald door <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 339, sectie 5.6</a>, waar "date-time" = full-date "T" full-time:<br/>(YYYY-MM-DD'T'HH:MM:SS.SSSSX)
    </td>
  </tr>
  <tr>
    <td>array</td>
    <td>type: array</td>
    <td>items.type kan worden gedefinieerd met elk scalair type:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "array",
          "objecten": {
            "type": "string"
          }
        }
      </pre>
      Array van objecten die door een ander schema worden gedefinieerd:<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "array",
          "objecten": {
            "$ref": "id"
          }
        }
      </pre>
      Hierbij is 'id' de {id} van het referentieschema.
    </td>
  </tr>
  <tr>
    <td>object</td>
    <td>type: object</td>
    <td>eigenschappen.{field}.type kan worden gedefinieerd met elk scalair type:
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
        }
      </pre>
      Veld van type "object" dat wordt gedefinieerd door een referentieschema:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "$ref": "id"
        }
      </pre>
      Hierbij is 'id' de {id} van het referentieschema.
    </td>
  </tr>
  <tr>
    <td>map</td>
    <td>type: object<br/><br/><strong>Opmerking:</strong><br/>Het gebruik van het gegevenstype 'map' is gereserveerd voor het gebruik van het schema in de branche en de leverancier en is niet beschikbaar voor gebruik in door huurders gedefinieerde velden. Het wordt gebruikt in standaardschema's wanneer het gegeven als sleutels wordt vertegenwoordigd die aan één of andere waarde in kaart brengen, of waar de sleutels redelijkerwijs niet in een statisch schema kunnen worden omvat en als gegevenswaarden moeten worden behandeld.</td>
    <td>A 'map' MAG GEEN eigenschappen definiëren. Het MOET één "[!UICONTROL additionalProperties]"-schema definiëren om het type waarden in de 'map' te beschrijven. Een 'map' in XDM kan slechts één gegevenstype bevatten. Waarden kunnen elke geldige XDM-schemadefinitie zijn, inclusief een array of een object, of als verwijzing naar een ander schema (via $ref).<br/><br/>Veld toewijzen met waarden van het type 'string':
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "additionalProperties":{
            "type": "string"
          }
        }
      </pre>
    Veld toewijzen met waarden die een array van tekenreeksen zijn:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "additionalProperties":{
            "type": "array",
            "objecten": {
              "type": "string"
            }
          }
        }
      </pre>
    Het gebied van de kaart dat verwijzingen een ander schema:
      <pre class="JSON language-JSON hljs">
        "sampleField": {
          "type": "object",
          "additionalProperties":{
            "$ref": "id"
          }
        }
      </pre>
      Hierbij is 'id' de {id} van het referentieschema.
    </td>
  </tr>
</table>
