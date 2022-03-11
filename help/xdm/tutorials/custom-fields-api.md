---
title: XDM-velden definiëren in de API voor schemaregister
description: Leer hoe u verschillende velden definieert bij het maken van XDM-bronnen (Custom Experience Data Model) in de Schema Registry API.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 3723e305740f859247350bd312b8b55e26cf4c24
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---

# XDM-velden definiëren in de API voor het schemaregister

Alle velden van het Experience Data Model (XDM) worden gedefinieerd met de standaard [JSON Schema](https://json-schema.org/) beperkingen die van toepassing zijn op hun veldtype, met extra beperkingen voor veldnamen die door Adobe Experience Platform worden afgedwongen. Met de API voor het schemaregister kunt u aangepaste velden in uw schema&#39;s definiëren met behulp van indelingen en optionele beperkingen. De XDM gebiedstypes worden blootgesteld door het gebied-vlakke attribuut, `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` is een door het systeem gegenereerde waarde en daarom hoeft u deze eigenschap niet aan de JSON voor uw veld toe te voegen wanneer u de API gebruikt (behalve wanneer [aangepaste kaarttypen maken](#maps)). De beste manier is om JSON-schematypen te gebruiken (zoals `string` en `integer`) met de toepasselijke minimum/maximum-beperkingen zoals gedefinieerd in de onderstaande tabel.

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
    <td>Een toewijzingsveld is in feite een objecttype met een onbeperkte set sleutels. Kaarten hebben, net als objecten, een <code>type</code> waarde van <code>object</code>, maar <code>meta:xdmType</code> is expliciet ingesteld op <code>map</code>.<br><br>Een kaart <strong>mogen</strong> om het even welke eigenschappen bepalen. IT <strong>moet</strong> één <code>additionalProperties</code> schema om het type van waarden te beschrijven binnen de kaart (elke kaart kan slechts één enkel gegevenstype bevatten). De <code>type</code> waarde moet ofwel <code>string</code> of <code>integer</code>.<br/><br/>Een toewijzingsveld met tekenreekswaarden:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "meta:xdmType": "map", "additionalProperties":{ "type": "string" } }</pre>
    Zie de sectie hieronder voor meer informatie over het creëren van de types van douanekaart in XDM.
    </td>
  </tr>
</table>

## Aangepaste toewijzingstypen maken {#maps}

Om &quot;map-als&quot;gegevens efficiënt in XDM te steunen, kunnen de voorwerpen met a worden geannoteerd `meta:xdmType` instellen op `map` om duidelijk te maken dat een voorwerp zou moeten worden beheerd alsof de belangrijkste reeks onbeperkt was. XDM stelt de volgende beperkingen op het gebruik van deze opslagwenk:

* Type kaart MOET van het type zijn `object`
* Voor typen kaarten MOET GEEN eigenschap zijn gedefinieerd (met andere woorden: &quot;lege&quot; objecten worden gedefinieerd)
* Kaarttypen MOETEN één enkel `additionalProperties` schema dat de waarden beschrijft die binnen de kaart kunnen worden geplaatst

Zorg ervoor dat u kaart-type gebieden wanneer absoluut noodzakelijk slechts gebruikt, aangezien zij de volgende prestatiesnadelen dragen:

* De tijd van de reactie van de Dienst van de Vraag van Adobe Experience Platform degradeert van drie seconden aan tien seconden voor 100 miljoen verslagen
* Kaarten moeten minder dan 16 sleutels hebben of anders risico op verdere afbraak

De gebruikersinterface van het Platform heeft ook beperkingen in hoe het de sleutels van kaart-type gebieden kan halen. Terwijl objecttekstvelden kunnen worden uitgebreid, worden kaarten als één veld weergegeven.

## Volgende stappen

In deze handleiding wordt beschreven hoe u verschillende veldtypen in de API definieert. Zie de handleiding voor meer informatie over de opmaak van XDM-veldtypen [Beperkingen voor XDM-veldtypen](../schema/field-constraints.md).
