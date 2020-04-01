---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Aanhangsel voor ontwikkelaar van het schemaregister
topic: developer guide
translation-type: tm+mt
source-git-commit: f7c87cc86bfc5017ec5c712d05e39be5c14a7147

---


# Aanhangsel

Dit document bevat aanvullende informatie over het werken met de API voor het registreren van het schema.

## Compatibiliteitsmodus

Experience Data Model (XDM) is een openbaar gedocumenteerde specificatie die door Adobe wordt aangestuurd om de interoperabiliteit, expressiviteit en kracht van digitale ervaringen te verbeteren. Adobe handhaaft de broncode en de formele definities XDM in een [open bronproject op GitHub](https://github.com/adobe/xdm/). Deze definities worden geschreven in de Standaardaantekening XDM, gebruikend JSON-LD (de Nota van Objecten JavaScript voor Gekoppelde Gegevens) en Schema JSON als grammatica voor het bepalen van XDM schema&#39;s.

Als u formele XDM-definities bekijkt in de openbare opslagplaats, ziet u dat de standaard XDM verschilt van wat u ziet in het Adobe Experience Platform. Wat u in het Platform van de Ervaring ziet wordt genoemd de Wijze van de Verenigbaarheid, en het verstrekt een eenvoudige afbeelding tussen standaardXDM en de manier het binnen Platform wordt gebruikt.

### Hoe de Wijze van de Verenigbaarheid werkt

De Wijze van de verenigbaarheid staat het model XDM JSON-LD toe om met bestaande gegevensinfrastructuur te werken door waarden binnen standaardXDM te veranderen terwijl het houden van de semantiek het zelfde. Er wordt een geneste JSON-structuur gebruikt, waarbij schema&#39;s in een boomachtige indeling worden weergegeven.

Het belangrijkste verschil tussen de standaard-XDM en de compatibiliteitsmodus is de verwijdering van het voorvoegsel &quot;xdm:&quot; voor veldnamen.

Hieronder volgt een vergelijking naast elkaar van verjaardagsgerelateerde velden (met verwijderde &quot;beschrijving&quot;-kenmerken) in zowel standaard XDM- als compatibiliteitsmodus. De velden Compatibiliteitsmodus bevatten een verwijzing naar het XDM-veld en het gegevenstype ervan in de kenmerken &quot;meta:xdmField&quot; en &quot;meta:xdmType&quot;.

<table>
  <th>Standaard XDM</th>
  <th>Compatibiliteitsmodus</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        {1} "xdm:bornDate": {1} "title": "Geboortedatum", "type": "string", "format": "date", }, "xdm:bornDayAndMonth": {1} "title": "Geboortedatum", "type": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", }, "xdm:bornYear": {1} "title": "Geboortejaar", "type": "integer", "minimum": 1, "maximum": 32767 }
      </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        {"bornDate": {1} "title": "Geboortedatum", "type": "string", "format": "date", "meta:xdmField": "xdm:bornDate", "meta:xdmType": "date" }, "bornDayAndMonth": {1} "title": "Geboortedatum", "type": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", "meta:xdmField": "xdm:bornDayAndMonth", "meta:xdmType": "string" }, "bornYear": {1} "title": "Geboortejaar", "type": "integer", "minimum": 1, "maximum": 32767, "meta:xdmField": "xdm:bornYear", "meta:xdmType": "short" }
      </pre>
  </td>
  </tr>
</table>

### Waarom is de Wijze van de Verenigbaarheid noodzakelijk?

Het Adobe Experience Platform is ontworpen om met meerdere oplossingen en services te werken, elk met hun eigen technische uitdagingen en beperkingen (bijvoorbeeld hoe bepaalde technologieën speciale tekens verwerken). Om deze beperkingen te verhelpen, werd de compatibiliteitsmodus ontwikkeld.

De meeste diensten van het Platform van de Ervaring met inbegrip van Catalogus, het Meer van Gegevens, en het Gebruik van het Profiel van de Klant in real time de Wijze van de Verenigbaarheid van de Verenigbaarheid in plaats van standaardXDM. De API voor het schemaregister gebruikt ook de compatibiliteitsmodus en de voorbeelden in dit document worden allemaal weergegeven met de compatibiliteitsmodus.

Het is de moeite waard om te weten dat een afbeelding tussen standaard XDM en de manier plaatsvindt het in het Platform van de Ervaring wordt in werking gesteld, maar het zou uw gebruik van de diensten van het Platform niet moeten beïnvloeden.

Het open bronproject is beschikbaar aan u, maar wanneer het over het in wisselwerking staan met middelen door de Registratie van het Schema komt, verstrekken de API voorbeelden in dit document de beste praktijken u zou moeten kennen en volgen.

## XDM-veldtypen definiëren in de API {#field-types}

De schema&#39;s XDM worden bepaald gebruikend de normen van het Schema JSON en basisgebiedstypes, met extra beperkingen voor gebiedsnamen die door het Platform van de Ervaring worden afgedwongen. Met XDM kunt u aanvullende veldtypen definiëren met behulp van indelingen en optionele beperkingen. De XDM gebiedstypes worden blootgesteld door het gebied-vlakke attribuut, `meta:xdmType`.

>[!NOTE] `meta:xdmType` is een door het systeem gegenereerde waarde en daarom hoeft u deze eigenschap niet aan de JSON voor uw veld toe te voegen. De beste manier is om JSON-schematypen (zoals een tekenreeks en een geheel getal) te gebruiken met de juiste min/max-beperkingen zoals gedefinieerd in de onderstaande tabel.

In de volgende tabel wordt de juiste opmaak beschreven voor het definiëren van scalaire veldtypen en meer specifieke veldtypen met behulp van optionele eigenschappen. Meer informatie over optionele eigenschappen en type-specifieke trefwoorden is beschikbaar via de documentatie [van het](https://json-schema.org/understanding-json-schema/reference/type.html)JSON-schema.

Zoek eerst het gewenste veldtype en gebruik de voorbeeldcode om uw API-aanvraag samen te stellen.

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
    <td>A 'map' MAG GEEN eigenschappen definiëren. Het MOET één enkel "additionalProperties"schema bepalen om het type van waarden te beschrijven in de "kaart". Een 'map' in XDM kan slechts één gegevenstype bevatten. Waarden kunnen elke geldige XDM-schemadefinitie zijn, inclusief een array of een object, of als verwijzing naar een ander schema (via $ref).<br/><br/>Veld toewijzen met waarden van het type 'string':
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


## XDM-typen toewijzen aan andere indelingen

In de onderstaande tabel wordt de toewijzing tussen &quot;meta:xdmType&quot; en andere serialisatie-indelingen beschreven.

| XDM Type<br>(meta:xdmType) | JSON<br>(JSON-schema) | Parquet<br>(type/aantekening) | Spark SQL | Java | Scala | .NET | CosmosDB | MongoDB | Aerospike | Protocol 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | tekst:tekenreeks | BYTE_ARRAY/UTF8 | StringType | java.lang.String | String | System.String | String | string | String | string |
| getal | tekst:nummer | DUBBEL | DoubleType | java.lang.Double | Dubbel | System.Double | Getal | double | Dubbel | double |
| lang | type:<br>integerMaximum:2^53+1<br>minimum:-2^53+1 | INT64 | LongType | java.lang.long | Lang | System.Int64 | Getal | lang | Geheel | int64 |
| int | type:<br>integerMaximum:2^31<br>minimum:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | Getal | int | Geheel | int32 |
| kort | type:<br>integerMaximum:2^15<br>minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Kort | System.Int16 | Getal | int | Geheel | int32 |
| byte | type:<br>integerMaximum:2^7<br>minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | Byte | System.SByte | Getal | int | Geheel | int32 |
| boolean | type:boolean | BOOLEAN | BooleanType | java.lang.Boolean | Boolean | System.Boolean | Boolean | bool | Geheel | Geheel | bool |
| date | type:<br>stringformat:date<br>(RFC 3339, sectie 5.6) | INT32/DATE | DateType | java.util.Date | java.util.Date | System.DateTime | String | date | Geheel getal<br>(unix millis) | int64<br>(unix millis) |
| date-time | type:<br>stringnotatie:date-time<br>(RFC 3339, sectie 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | String | tijdstempel | Geheel getal<br>(unix millis) | int64<br>(unix millis) |
| map | object | MAP geannoteerde groep<br><br>&lt;<span>key_type</span>> MOET STRING<br><br>&lt;<span>value_type</span>> type kaartwaarden zijn | MapType<br><br>&quot;keyType&quot; MOET StringType<br><br>&quot;valueType&quot; zijn type toewijzingswaarden. | java.util.Map | Kaart | --- | object | object | map | map&lt;<span>key_type, value_type</span>> |
