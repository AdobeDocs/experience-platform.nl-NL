---
title: Extension Manifest
description: Leer hoe u een JSON-manifestbestand configureert dat Adobe Experience Platform informeert over de juiste manier om uw extensie te gebruiken.
exl-id: 7cac020b-3cfd-4a0a-a2d1-edee1be125d0
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '2645'
ht-degree: 0%

---

# Extensie manifest

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

In de basismap van uw extensie moet u een bestand maken met de naam `extension.json`. Dit bevat belangrijke informatie over uw extensie waarmee Adobe Experience Platform deze correct kan gebruiken. Een deel van de inhoud wordt gevormd na de wijze van [npm&#39;s `package.json`](https://docs.npmjs.com/files/package.json).

Een voorbeeld `extension.json` kan de [Hello World-extensie](https://github.com/adobe/reactor-helloworld-extension/blob/master/extension.json) GitHub-opslagplaats.

Een extensiemanifest moet uit het volgende bestaan:

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de extensie. Het moet uniek zijn van alle andere uitbreidingen en moet voldoen aan [naamgevingsregels](#naming-rules). **Dit wordt gebruikt door tags als id en mag niet worden gewijzigd nadat u de extensie hebt gepubliceerd.** |
| `platform` | Het platform voor uw extensie. De enige waarde die op dit moment wordt geaccepteerd, is `web`. |
| `version` | De versie van uw extensie. Het moet de [semester](https://semver.org/) versieopmaak. Dit is in overeenstemming met [npm-versieveld](https://docs.npmjs.com/files/package.json#version). |
| `displayName` | De leesbare naam van de extensie. Dit zal aan de gebruikers van de Platform worden getoond. &quot;tags&quot; of &quot;extensie&quot; hoeven niet te worden vermeld; gebruikers weten al dat ze een tagextensie bekijken . |
| `description` | De beschrijving van de extensie. Dit zal aan de gebruikers van de Platform worden getoond. Als uw extensie gebruikers de mogelijkheid biedt om uw product te implementeren op hun website, moet u beschrijven wat uw product doet. &quot;tags&quot; of &quot;extensie&quot; hoeven niet te worden vermeld; gebruikers weten al dat ze een tagextensie bekijken . |
| `iconPath` *(Optioneel)* | Het relatieve pad naar het pictogram dat voor de extensie wordt weergegeven. Het mag niet beginnen met een schuine streep. Het moet verwijzen naar een SVG-bestand met een `.svg` extensie. De SVG moet vierkant zijn en kan met Platform worden geschaald. |
| `author` | De &quot;auteur&quot; is een object dat als volgt moet worden gestructureerd: <ul><li>`name`: De naam van de auteur van de extensie. De bedrijfsnaam kan hier ook worden gebruikt.</li><li>`url` *(Optioneel)*: Een URL waar u meer informatie kunt vinden over de auteur van de extensie.</li><li>`email` *(Optioneel)*: Het e-mailadres van de auteur van de extensie.</li></ul>Dit is in overeenstemming met [npm-auteurveld](https://docs.npmjs.com/files/package.json#people-fields-author-contributors) regels. |
| `exchangeUrl` *(Vereist voor openbare extensies)* | De URL naar de aanbieding van uw extensie op Adobe Exchange. Deze moet overeenkomen met het patroon `https://www.adobeexchange.com/experiencecloud.details.######.html`. |
| `viewBasePath` | Het relatieve pad naar de submap met al uw weergaven en aan de weergave gerelateerde bronnen (HTML, JavaScript, CSS, afbeeldingen). Platform host deze map op een webserver en laadt hierin iframe-inhoud. Dit is een verplicht veld en mag niet beginnen met een schuine streep. Als bijvoorbeeld al uw weergaven zijn opgenomen in `src/view/`, de waarde van `viewBasePath` zou `src/view/`. |
| `hostedLibFiles` *(Optioneel)* | Veel van onze gebruikers hebben de voorkeur aan het hosten van alle op tags betrekking hebbende dossiers op hun eigen server. Dit biedt gebruikers meer zekerheid over de beschikbaarheid van bestanden tijdens runtime en kan de code gemakkelijk scannen op beveiligingskwetsbaarheden. Als het bibliotheekgedeelte van uw extensie JavaScript-bestanden tijdens runtime moet laden, wordt u aangeraden deze eigenschap te gebruiken om deze bestanden weer te geven. De weergegeven bestanden worden samen met de tagruntimebibliotheek gehost. Uw extensie kan de bestanden vervolgens laden via een URL die is opgehaald met de [getHostedLibFileUrl](./turbine.md#get-hosted-lib-file) methode.<br><br>Deze optie bevat een array met relatieve paden van bibliotheekbestanden van derden die moeten worden gehost. |
| `main` *(Optioneel)* | Het relatieve pad van een bibliotheekmodule die bij uitvoering moet worden uitgevoerd.<br><br>Deze module wordt altijd opgenomen in de runtimebibliotheek en uitgevoerd. Omdat de module altijd is opgenomen in de runtimebibliotheek, raden we u aan alleen een &#39;main&#39;-module te gebruiken als dit absoluut noodzakelijk is en de codegrootte minimaal te houden.<br><br>Het is niet gegarandeerd dat deze module eerst wordt uitgevoerd; andere modules kunnen vóór het worden uitgevoerd. |
| `configuration` *(Optioneel)* | Dit beschrijft de [extensieconfiguratie](./configuration.md) deel van de extensie. Dit is nodig als u wilt dat gebruikers algemene instellingen voor de extensie opgeven. Zie de [aanhangsel](#config-object) voor meer informatie over de structuur van dit veld. |
| `events` *(Optioneel)* | Een array van [event](./web/event-types.md) typedefinities. Zie het aanhangsel over [typedefinities](#type-definitions) voor de structuur van elk object in de array. |
| `conditions` *(Optioneel)* | Een array van [voorwaarde](./web/condition-types.md) typedefinities. Zie het aanhangsel over [typedefinities](#type-definitions) voor de structuur van elk object in de array. |
| `actions` *(Optioneel)* | Een array van [action](./web/action-types.md) typedefinities. Zie het aanhangsel over [typedefinities](#type-definitions) voor de structuur van elk object in de array. |
| `dataElements` *(Optioneel)* | Een array van [gegevenselement](./web/data-element-types.md) typedefinities. Zie het aanhangsel over [typedefinities](#type-definitions) voor de structuur van elk object in de array. |
| `sharedModules` *(Optioneel)* | Een array van gezamenlijke moduledefinitieobjecten. Elk gezamenlijk module-object in de array moet als volgt zijn gestructureerd: <ul><li>`name`: De naam van de gedeelde module. Merk op dat deze naam zal worden gebruikt wanneer het van verwijzingen voorzien van gedeelde modules van andere uitbreidingen zoals die in [Gedeelde modules](./web/shared.md). Deze naam wordt nooit weergegeven in een gebruikersinterface. Het zou uniek van de namen van andere gedeelde modules binnen uw uitbreiding moeten zijn en moet voldoen aan [naamgevingsregels](#naming-rules). **Dit wordt gebruikt door tags als id en mag niet worden gewijzigd nadat u de extensie hebt gepubliceerd.**</li><li>`libPath`: Het relatieve pad naar de gedeelde module. Het mag niet beginnen met een schuine streep. Er moet worden verwezen naar een JavaScript-bestand met een `.js` extensie.</li></ul> |

## Aanhangsel

### Naamgevingsregels {#naming-rules}

De waarde van `name` veld binnen `extension.json` moeten voldoen aan de volgende voorschriften:

* Moet uit maximaal 214 tekens bestaan
* Mag niet met een punt of een onderstrepingsteken beginnen
* Mag geen hoofdletters bevatten
* Alleen URL-veilige tekens bevatten

Deze zijn in overeenstemming met [npm-pakketnaam](https://docs.npmjs.com/files/package.json#name) regels.

### Eigenschappen van Configuration-objecten {#config-object}

Het configuratieobject moet als volgt zijn gestructureerd:

<table>
  <thead>
    <tr>
      <th>Eigenschap</th>
      <th>Beschrijving</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>viewPath</code></td>
      <td>De relatieve URL naar de configuratieweergave van de extensie. Het moet in verhouding staan tot <code>viewBasePath</code> en mag niet met een schuine streep beginnen. Het moet verwijzen naar een HTML-bestand met een <code>.html</code> extensie. Achtervoegsels van queryreeksen en -fragmenten (hashes) zijn acceptabel.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Een object van <a href="https://json-schema.org/">JSON Schema</a> beschrijvend het formaat van een geldig voorwerp dat van de mening van de uitbreidingsconfiguratie wordt bewaard. Aangezien u de ontwikkelaar van de configuratiemening bent, is het uw verantwoordelijkheid om ervoor te zorgen dat om het even welk die montagesvoorwerp aan dit schema aanpast. Dit schema zal ook voor bevestiging worden gebruikt wanneer de gebruikers proberen om gegevens te bewaren gebruikend de diensten van het Platform.<br><br>Een voorbeeldschemaobject is als volgt:
<pre class="JSON language-JSON hljs">
{ "$schema": "http://json-schema.org/draft-04/schema#", "type": "object", "eigenschappen": { "delay": { "type": "number", "minimum": 1} }, "required": [ "delay" ], "additionalProperties": false }
</pre>
      We raden u aan een gereedschap te gebruiken zoals <a href="https://www.jsonschemavalidator.net/">JSON-schemavalidator</a> om het schema handmatig te testen.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Optioneel)</em></td>
      <td>Een array van objecten waarin elk object een transformatie vertegenwoordigt die op elk overeenkomend instellingsobject moet worden uitgevoerd wanneer het wordt uitgestraald in de runtimebibliotheek. Zie de <a href="#transforms">transformaties</a> voor meer informatie over waarom dit nodig kan zijn en hoe het wordt gebruikt.</td>
    </tr>
  </tbody>
</table>

### Typedefinities {#type-definitions}

Een typedefinitie is een voorwerp dat wordt gebruikt om een gebeurtenis, een voorwaarde, een actie, of type van gegevenselement te beschrijven. Het object bestaat uit het volgende:

<table>
  <thead>
    <tr>
      <th>Eigenschap</th>
      <th>Beschrijving</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>name</code></td>
      <td>De naam van het type. Dit moet een unieke naam zijn binnen de extensie. De naam moet voldoen aan <a href="#naming-rules">naamgevingsregels</a>. <strong>Dit wordt gebruikt door tags als id en mag niet worden gewijzigd nadat u de extensie hebt gepubliceerd.</strong></td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>De tekst die zal worden gebruikt om het type binnen het gebruikersinterface van de Inzameling van Gegevens te vertegenwoordigen. Het moet leesbaar zijn voor de mens.</td>
    </tr>
    <tr>
      <td><code>categoryName</code> <em>(Optioneel)</em></td>
      <td>Indien verstrekt, <code>displayName</code> wordt vermeld onder de <code>categoryName</code> in de gebruikersinterface. Alle typen met hetzelfde <code>categoryName</code> worden onder dezelfde rubriek vermeld. Als uw extensie bijvoorbeeld een <code>keyUp</code> gebeurtenistype en een <code>keyDown</code> gebeurtenistype en beide hadden een <code>categoryName</code> van <code>Keyboard</code>beide gebeurtenistypen worden vermeld onder de categorie Toetsenbord terwijl de gebruiker een regel maakt en een keuze maakt uit de lijst met beschikbare gebeurtenistypen. De waarde van <code>categoryName</code> moet leesbaar zijn voor de mens.</td>
    </tr>
    <tr>
      <td><code>libPath</code></td>
      <td>Het relatieve pad naar de bibliotheekmodule van de tekst. Het mag niet beginnen met een schuine streep. Er moet worden verwezen naar een JavaScript-bestand met een <code>.js</code> extensie.</td>
    </tr>
    <tr>
      <td><code>viewPath</code> <em>(Optioneel)</em></td>
      <td>De relatieve URL ten opzichte van de weergave van het type. Het moet in verhouding staan tot <code>viewBasePath</code> en mag niet met een schuine streep beginnen. Het moet verwijzen naar een HTML-bestand met een <code>.html</code> extensie. Zoektekenreeksen en fragmentid's (hashes) zijn acceptabel. Als de de bibliotheekmodule van uw type geen montages van een gebruiker gebruikt, kunt u dit bezit uitsluiten en het Platform zal in plaats daarvan placeholder tonen verklaren die dat geen configuratie noodzakelijk is.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Een object van <a href="https://json-schema.org/">JSON Schema</a> beschrijvend het formaat van een geldig montagesobject dat door de gebruiker kan worden bewaard. De montages worden gewoonlijk gevormd en door een gebruiker bewaard gebruikend het gebruikersinterface van de Inzameling van Gegevens. In deze gevallen kan de weergave van de extensie de nodige stappen ondernemen om door de gebruiker opgegeven instellingen te valideren. Anderzijds kiezen sommige gebruikers ervoor om tags-API's rechtstreeks te gebruiken zonder de hulp van een gebruikersinterface. Het doel van dit schema is Platform toe te staan om correct te bevestigen dat de montagesobjecten die door gebruikers worden bewaard, ongeacht of een gebruikersinterface wordt gebruikt, in een formaat zijn dat met de bibliotheekmodule compatibel is die op het montagesobject tijdens runtime zal handelen.<br><br>Een voorbeeldschemaobject is als volgt:<br>
<pre class="JSON language-JSON hljs">
{ "$schema": "http://json-schema.org/draft-04/schema#", "type": "object", "eigenschappen": { "delay": { "type": "number", "minimum": 1} }, "required": [ "delay" ], "additionalProperties": false }
</pre>
      We raden u aan een gereedschap te gebruiken zoals <a href="https://www.jsonschemavalidator.net/">JSON-schemavalidator</a> om het schema handmatig te testen.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Optioneel)</em></td>
      <td>Een array van objecten waarin elk object een transformatie vertegenwoordigt die op elk overeenkomend instellingsobject moet worden uitgevoerd wanneer het wordt uitgestraald in de runtimebibliotheek. Zie de sectie over <a href="#transforms">transformaties</a> voor meer informatie over waarom dit nodig kan zijn en hoe het wordt gebruikt .</td>
    </tr>
  </tbody>
</table>

### Transformaties {#transforms}

Voor bepaalde specifieke gebruiksgevallen moeten de instellingsobjecten die zijn opgeslagen vanuit een weergave, door het Platform worden getransformeerd voordat ze worden uitgestraald in de runtimebibliotheek van de tag. U kunt verzoeken dat een of meer van deze transformaties plaatsvinden door het instellen van de `transforms` eigenschap bij het definiëren van een typedefinitie binnen uw `extension.json`. De `transforms` eigenschap is een array van objecten waarin elk object een transformatie vertegenwoordigt die moet plaatsvinden.

Voor alle transformaties is een `type` en `propertyPath`. De `type` moet een van `function`, `remove`, en `file` en beschrijft welk Platform van de transformatie op het montagesobject zou moeten van toepassing zijn. De `propertyPath` is een door een punt gescheiden tekenreeks die tags opgeeft waar de eigenschap moet worden gevonden die binnen het instellingsobject moet worden gewijzigd. Hier volgt een voorbeeld van een instellingenobject en enkele `propertyPath`s:

```js
{
  foo: {
    bar: "A string",
    baz: [
      "A",
      "B",
      "C"
    ]
  }
}
```

* Als u een `propertyPath` van `foo.bar` u de `"A string"` waarde.
* Als u een `propertyPath` van `foo.baz[]` u zou elke waarde in `baz` array.
* Als u een `propertyPath` van `foo.baz` u de `baz` array.

Eigenschapspaden kunnen elke combinatie van array- en objectnotatie gebruiken om transformaties toe te passen op elk niveau van het instellingsobject.

>[!WARNING]
>
>Armatuurnotatie gebruiken in het dialoogvenster `propertyPath` kenmerk (bijvoorbeeld `foo.baz[]`) wordt nog niet ondersteund in de extensiesandbox*tool.

In de onderstaande secties worden de beschikbare transformaties beschreven en hoe u deze kunt gebruiken.

#### Functietransformatie

Met de functietransformatie kan code die door gebruikers van het Platform is geschreven, worden uitgevoerd door een bibliotheekmodule in de uitgestoten runtimebibliotheek.

Laten we aannemen dat we een handelingstype &#39;aangepast script&#39; willen opgeven. De actieweergave &quot;aangepast script&quot; kan een tekstgebied bevatten waarin de gebruiker code kan invoeren. Laten we aannemen dat een gebruiker de volgende code in het tekstgebied heeft ingevoerd:

`console.log('Welcome, ' + username +'. This is ZomboCom.');`

Wanneer de gebruiker de regel opslaat, ziet het instellingsobject dat in de weergave is opgeslagen er mogelijk als volgt uit:

```javascript
{
  foo: {
    bar: "console.log('Welcome, ' + username +'. This is ZomboCom.');"
  }
}
```

Wanneer een regel die onze actie gebruikt, in de runtimebibliotheek van de tag wordt geactiveerd, willen we de code van de gebruiker uitvoeren en deze een gebruikersnaam doorgeven.

Op het punt dat het instellingsobject wordt opgeslagen vanuit de weergave van het handelingstype, is de code van de gebruiker gewoon een tekenreeks. Dit is goed omdat het behoorlijk aan en van JSON kan worden geserialiseerd; het is echter ook ongeldig omdat het normaal gesproken ook als tekenreeks in de tagruntime-bibliotheek wordt weergegeven in plaats van als een uitvoerbare functie. Hoewel u kon proberen om de code binnen de de bibliotheekmodule van uw actietype uit te voeren gebruikend [`eval`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval) of [Constructor Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function), is het sterk ontmoedigd vanwege [beleid voor inhoudsbeveiliging](https://developer.mozilla.org/en-US/docs/Web/Security/CSP) mogelijk blokkerende uitvoering.

Als tussenoplossing voor deze situatie, vertelt het gebruiken van de functietransformatie Platform om de code van de gebruiker in een uitvoerbare functie te verpakken wanneer het in de markering runtime bibliotheek wordt uitgegeven. Om ons voorbeeldprobleem op te lossen, zouden wij de transformatie op de typedefinitie in `extension.json` als volgt:

```json
{
  "transforms": [
    {
      "type": "function",
      "propertyPath": "foo.bar",
      "parameters": ["username"]
    }
  ]
}
```

* `type` definieert het type transformatie dat op het instellingsobject moet worden toegepast.
* `propertyPath` is een door een punt gescheiden tekenreeks die het Platform opgeeft waar de eigenschap moet worden gevonden die binnen het instellingsobject moet worden gewijzigd.
* `parameters` is een array met parameternamen die moet worden opgenomen in de handtekening van de wrapping-functie.

Wanneer het instellingsobject wordt uitgestraald in de tagruntime-bibliotheek, wordt het als volgt getransformeerd:

```javascript
{
  foo: {
    bar: function(username) {
      console.log('Welcome, ' + username +'. This is ZomboCom.');
    }
  }
}
```

Uw bibliotheekmodule kan dan de functie aanroepen die de code van de gebruiker bevat en de `username` argument.

#### Bestandstransformatie

Met de bestandstransformatie kan code die door gebruikers van het Platform is geschreven, worden verzonden naar een bestand dat losstaat van de runtimebibliotheek van de tag. Het bestand wordt samen met de tagruntime-bibliotheek gehost en kan vervolgens tijdens runtime naar wens door de extensie worden geladen.

Laten we aannemen dat we een handelingstype &#39;aangepast script&#39; willen opgeven. De weergave van het handelingstype kan een tekstgebied bevatten waarin de gebruiker code kan invoeren. Laten we aannemen dat een gebruiker de volgende code in het tekstgebied heeft ingevoerd:

`console.log('This is ZomboCom.');`

Wanneer de gebruiker de regel opslaat, ziet het instellingsobject dat in de weergave is opgeslagen er mogelijk als volgt uit:

```js
{
  foo: {
    bar: "console.log('This is ZomboCom.');"
  }
}
```

We willen dat de code van de gebruiker in een afzonderlijk bestand wordt geplaatst in plaats van in de runtimebibliotheek van de tag. Wanneer een regel die onze actie gebruikt, binnen de tagruntime bibliotheek wordt geactiveerd, willen wij de code van de gebruiker laden door een scriptelement aan de documenttekst toe te voegen. Om ons voorbeeldprobleem op te lossen, zouden wij de transformatie op de definitie van actietype in `extension.json` als volgt:

```json
{
  "transforms": [
    {
      "type": "file",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` definieert het type transformatie dat op het instellingsobject moet worden toegepast.
* `propertyPath` is een door een punt gescheiden tekenreeks die het Platform opgeeft waar de eigenschap moet worden gevonden die binnen het instellingsobject moet worden gewijzigd.

Wanneer het instellingsobject wordt uitgestraald in de tagruntime-bibliotheek, wordt het als volgt getransformeerd:

```javascript
{
  foo: {
    bar: "//launch.cdn.com/path/abc.js"
  }
}
```

In dat geval moet de waarde van `foo.bar` is getransformeerd naar een URL. De exacte URL wordt bepaald op het moment dat de bibliotheek wordt gemaakt. Het bestand krijgt altijd een `.js` en geleverd met een JavaScript-georiënteerd MIME-type. In de toekomst kunnen we ondersteuning toevoegen voor andere MIME-typen.

#### Transformatie verwijderen

Standaard worden alle eigenschappen van het instellingsobject weergegeven in de runtimebibliotheek van de tag. Als bepaalde eigenschappen alleen worden gebruikt voor de extensieweergave, vooral als deze vertrouwelijke informatie bevatten (bijvoorbeeld geheime token), moet u de transformatie voor verwijderen gebruiken om te voorkomen dat de informatie wordt uitgestoten in de runtimebibliotheek van de tag.

Laten we aannemen dat we een nieuw actietype willen aanbieden. De weergave van het actietype kan een invoer bevatten waarin de gebruiker een geheime sleutel kan invoeren die verbinding met een specifieke API mogelijk maakt. Laten we aannemen dat een gebruiker de volgende tekst in de invoer heeft ingevoerd:

`ABCDEFG`

Wanneer de gebruiker de regel opslaat, ziet het instellingsobject dat in de weergave is opgeslagen er mogelijk als volgt uit:

```js
{
  foo: {
    bar: "ABCDEFG"
  }
}
```

We willen de eigendom niet opnemen `bar` in de runtimebibliotheek van de tag. Om ons voorbeeldprobleem op te lossen, zouden wij de transformatie op de definitie van actietype in `extension.json` als volgt:

```json
{
  "transforms": [
    {
      "type": "remove",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` definieert het type transformatie dat op het instellingsobject moet worden toegepast.
* `propertyPath` is een door een punt gescheiden tekenreeks die het Platform opgeeft waar de eigenschap moet worden gevonden die binnen het instellingsobject moet worden gewijzigd.

Wanneer het instellingsobject wordt uitgestraald in de tagruntime-bibliotheek, wordt het als volgt getransformeerd:

```js
{
  foo: {
  }
}
```

In dat geval moet de waarde van `foo.bar` is verwijderd uit het instellingenobject.
