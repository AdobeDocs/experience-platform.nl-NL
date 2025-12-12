---
title: Extension Manifest
description: Leer hoe u een JSON-manifestbestand configureert dat Adobe Experience Platform informeert over de juiste manier om uw extensie te gebruiken.
exl-id: 7cac020b-3cfd-4a0a-a2d1-edee1be125d0
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '2607'
ht-degree: 0%

---

# Extensie manifest

In de basismap van de extensie moet u een bestand met de naam `extension.json` maken. Dit bevat belangrijke informatie over uw extensie waarmee Adobe Experience Platform deze correct kan gebruiken. Sommige inhoud wordt gevormd na de manier van [ npm `package.json` ](https://docs.npmjs.com/files/package.json).

Een voorbeeld `extension.json` kan de [ uitbreiding van de Wereld van Hello ](https://github.com/adobe/reactor-helloworld-extension/blob/master/extension.json) bewaarplaats GitHub worden gevonden.

Een extensiemanifest moet uit het volgende bestaan:

| Eigenschap | Beschrijving |
|--------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name` | De naam van de extensie. Het moet van alle andere uitbreidingen uniek zijn en moet [ het noemen regels ](#naming-rules) naleven. **dit wordt gebruikt door markeringen als herkenningsteken en zou niet moeten worden veranderd nadat u uw uitbreiding publiceert.** |
| `platform` | Het platform voor uw extensie. De enige waarde die op dit moment wordt geaccepteerd, is `web` . |
| `version` | De versie van uw extensie. Het moet het [ semver ](https://semver.org/) versioning formaat volgen. Dit is verenigbaar met [ npm versiegebied ](https://docs.npmjs.com/files/package.json#version). |
| `displayName` | De leesbare naam van de extensie. Dit wordt weergegeven aan Experience Platform-gebruikers. Het is niet nodig om &quot;tags&quot; of &quot;extensie&quot; te vermelden. Gebruikers weten dan al dat ze naar een extensie voor tags kijken. |
| `description` | De beschrijving van de extensie. Dit wordt weergegeven aan Experience Platform-gebruikers. Als uw extensie gebruikers de mogelijkheid biedt om uw product te implementeren op hun website, moet u beschrijven wat uw product doet. Het is niet nodig om &quot;tags&quot; of &quot;extensie&quot; te vermelden. Gebruikers weten dan al dat ze naar een extensie voor tags kijken. |
| `iconPath` *(Optioneel)* | Het relatieve pad naar het pictogram dat voor de extensie wordt weergegeven. Het mag niet beginnen met een slash. Het moet verwijzen naar een SVG-bestand met een `.svg` -extensie. De SVG moet vierkant zijn en kan door Experience Platform worden geschaald. |
| `author` | De &quot;auteur&quot; is een object met de volgende structuur: <ul><li>`name`: De naam van de auteur van de extensie. De bedrijfsnaam kan hier ook worden gebruikt.</li><li>`url` *(Facultatief)*: Een URL waar u meer over de uitbreidingsauteur kunt weten.</li><li>`email` *(Facultatief)*: Het e-mailadres van de auteur van de uitbreiding.</li></ul>Dit is verenigbaar met [ npm auteursgebied ](https://docs.npmjs.com/files/package.json#people-fields-author-contributors) regels. |
| `releaseNotesUrl` *(Optioneel)* | De URL naar de releaseopmerkingen van uw extensie als u over een locatie beschikt om deze gegevens te publiceren. Deze URL wordt gebruikt in de gebruikersinterface voor Adobe-tags om deze koppeling weer te geven tijdens de installatie en upgrade van de extensie. Deze eigenschap wordt alleen ondersteund voor Web- en Edge-extensies. |
| `exchangeUrl` *(Vereist voor openbare extensies)* | De URL naar de aanbieding van je extensie op Adobe Exchange. Deze moet overeenkomen met het patroon `https://www.adobeexchange.com/experiencecloud.details.######.html` . |
| `viewBasePath` | Het relatieve pad naar de submap met al uw weergaven en aan de weergave gerelateerde bronnen (HTML, JavaScript, CSS, afbeeldingen). Experience Platform host deze map op een webserver en laadt er iframe-inhoud uit. Dit is een verplicht veld en mag niet beginnen met een schuine streep. Als bijvoorbeeld al uw weergaven zich in `src/view/` bevinden, is de waarde van `viewBasePath` gelijk aan `src/view/` . |
| `hostedLibFiles` *(Optioneel)* | Veel van onze gebruikers hebben de voorkeur aan het hosten van alle op tags betrekking hebbende dossiers op hun eigen server. Dit biedt gebruikers meer zekerheid over de beschikbaarheid van bestanden tijdens runtime en kan de code gemakkelijk scannen op beveiligingskwetsbaarheden. Als het bibliotheekgedeelte van uw extensie JavaScript-bestanden tijdens runtime moet laden, wordt u aangeraden deze eigenschap te gebruiken om deze bestanden weer te geven. De weergegeven bestanden worden samen met de tagruntimebibliotheek gehost. Uw uitbreiding kan de dossiers via URL dan laden die gebruikend [ wordt teruggewonnen getHostedLibFileUrl ](./turbine.md#get-hosted-lib-file) methode.<br><br> deze optie bevat een serie met relatieve wegen van derdebibliotheekdossiers die moeten worden ontvangen. |
| `main` *(Optioneel)* | Het relatieve pad van een bibliotheekmodule die bij uitvoering moet worden uitgevoerd.<br><br> deze module zal altijd inbegrepen in de runtime bibliotheek en uitgevoerd zijn. Omdat de module altijd is opgenomen in de runtimebibliotheek, raden we u aan alleen een &#39;main&#39;-module te gebruiken als dit absoluut noodzakelijk is en de codegrootte minimaal te houden.<br><br> Deze module wordt gegarandeerd niet eerst worden uitgevoerd; andere modules kunnen vóór het worden uitgevoerd. |
| `configuration` *(Optioneel)* | Dit beschrijft het [ gedeelte van de uitbreidingsconfiguratie ](./configuration.md) van de uitbreiding. Dit is nodig als u wilt dat gebruikers algemene instellingen voor de extensie opgeven. Zie [ bijlage ](#config-object) voor details op hoe dit gebied zou moeten worden gestructureerd. |
| `events` *(Optioneel)* | Een serie van [ gebeurtenis ](./web/event-types.md) typedefinities. Zie de bijlage sectie op [ typedefinities ](#type-definitions) voor de structuur van elk voorwerp in de serie. |
| `conditions` *(Optioneel)* | Een serie van [ voorwaarde ](./web/condition-types.md) typedefinities. Zie de bijlage sectie op [ typedefinities ](#type-definitions) voor de structuur van elk voorwerp in de serie. |
| `actions` *(Optioneel)* | Een serie van [ actie ](./web/action-types.md) typedefinities. Zie de bijlage sectie op [ typedefinities ](#type-definitions) voor de structuur van elk voorwerp in de serie. |
| `dataElements` *(Optioneel)* | Een serie van [ gegevens element ](./web/data-element-types.md) typedefinities. Zie de bijlage sectie op [ typedefinities ](#type-definitions) voor de structuur van elk voorwerp in de serie. |
| `sharedModules` *(Optioneel)* | Een array van gezamenlijke moduledefinitieobjecten. Elk gezamenlijk moduleobject in de array moet als volgt zijn gestructureerd: <ul><li>`name`: De naam van de gedeelde module. Merk op dat deze naam zal worden gebruikt wanneer het van verwijzingen voorzien van gedeelde modules van andere uitbreidingen zoals die in [ Gedeelde Modules ](./web/shared.md) worden beschreven. Deze naam wordt nooit weergegeven in een gebruikersinterface. Het zou van de namen van andere gedeelde modules binnen uw uitbreiding uniek moeten zijn en moet [ het noemen regels ](#naming-rules) naleven. **dit wordt gebruikt door markeringen als herkenningsteken en zou niet moeten worden veranderd nadat u uw uitbreiding publiceert.**</li><li>`libPath`: Het relatieve pad naar de gedeelde module. Het mag niet beginnen met een slash. Er moet worden verwezen naar een JavaScript-bestand met een extensie `.js` .</li></ul> |

## Bijlage

### Naamgevingsregels {#naming-rules}

De waarde van elk `name` veld in `extension.json` moet aan de volgende regels voldoen:

* Moet uit maximaal 214 tekens bestaan
* Mag niet met een punt of een onderstrepingsteken beginnen
* Mag geen hoofdletters bevatten
* Alleen URL-veilige tekens bevatten

Deze zijn verenigbaar met [ npm pakketnaam ](https://docs.npmjs.com/files/package.json#name) regels.

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
      <td>De relatieve URL naar de configuratieweergave van de extensie. Deze moet relatief zijn ten opzichte van <code>viewBasePath</code> en mag niet beginnen met een schuine streep. Het moet verwijzen naar een HTML-bestand met een <code>.html</code> -extensie. Achtervoegsels van queryreeksen en -fragmenten (hashes) zijn acceptabel.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Een voorwerp van <a href="https://json-schema.org/"> JSON Schema </a> beschrijvend het formaat van een geldig voorwerp dat van de mening van de uitbreidingsconfiguratie wordt bewaard. Aangezien u de ontwikkelaar van de configuratiemening bent, is het uw verantwoordelijkheid om ervoor te zorgen dat om het even welk die montagesvoorwerp aan dit schema aanpast. Dit schema wordt ook gebruikt voor validatie wanneer gebruikers gegevens proberen op te slaan met Experience Platform-services.<br><br> een voorwerp van het voorbeeldschema is als volgt:
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "number",
      "minimum": 1
    }
  },
  "required": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      Wij adviseren gebruikend een hulpmiddel zoals <a href="https://www.jsonschemavalidator.net/"> JSON- Schema validator </a> om uw schema manueel te testen.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Optioneel)</em></td>
      <td>Een array van objecten waarin elk object een transformatie vertegenwoordigt die op elk overeenkomend instellingsobject moet worden uitgevoerd wanneer het wordt uitgestraald in de runtimebibliotheek. Zie <a href="#transforms"> transformeert </a> sectie voor meer informatie over waarom dit kan nodig zijn en hoe het wordt gebruikt.</td>
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
      <td>De naam van het type. Dit moet een unieke naam zijn binnen de extensie. De naam moet <a href="#naming-rules"> het noemen regels </a> naleven. <strong> dit wordt gebruikt door markeringen als herkenningsteken en zou niet moeten worden veranderd nadat u uw uitbreiding publiceert.</strong></td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>De tekst die zal worden gebruikt om het type binnen het gebruikersinterface van de Inzameling van Gegevens te vertegenwoordigen. Het moet leesbaar zijn voor de mens.</td>
    </tr>
    <tr>
      <td><code>categoryName</code> <em>(Optioneel)</em></td>
      <td>Als deze optie wordt opgegeven, wordt de <code>displayName</code> weergegeven onder <code>categoryName</code> in de gebruikersinterface. Alle typen met dezelfde <code>categoryName</code> worden in dezelfde categorie vermeld. Als uw extensie bijvoorbeeld een gebeurtenistype <code>keyUp</code> en een gebeurtenistype <code>keyDown</code> heeft en beide een <code>categoryName</code> van <code>Keyboard</code> hebben, worden beide gebeurtenistypen weergegeven onder de categorie Keyboard terwijl de gebruiker een optie selecteert uit de lijst met beschikbare gebeurtenistypen wanneer een regel wordt gemaakt. De waarde van <code>categoryName</code> moet leesbaar zijn voor de mens.</td>
    </tr>
    <tr>
      <td><code>libPath</code></td>
      <td>Het relatieve pad naar de bibliotheekmodule van de tekst. Het mag niet beginnen met een slash. Er moet worden verwezen naar een JavaScript-bestand met een extensie <code>.js</code> .</td>
    </tr>
    <tr>
      <td><code>viewPath</code> <em>(Optioneel)</em></td>
      <td>De relatieve URL ten opzichte van de tekstweergave. Deze moet relatief zijn ten opzichte van <code>viewBasePath</code> en mag niet beginnen met een schuine streep. Het moet verwijzen naar een HTML-bestand met een <code>.html</code> -extensie. Zoektekenreeksen en fragmentid's (hashes) zijn acceptabel. Als de bibliotheekmodule van uw type geen instellingen van een gebruiker gebruikt, kunt u deze eigenschap uitsluiten en geeft Experience Platform in plaats daarvan een tijdelijke aanduiding weer die aangeeft dat geen configuratie nodig is.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Een voorwerp van <a href="https://json-schema.org/"> JSON Schema </a> beschrijvend het formaat van een geldig montagesvoorwerp dat door de gebruiker kan worden bewaard. De montages worden gewoonlijk gevormd en door een gebruiker bewaard gebruikend het gebruikersinterface van de Inzameling van Gegevens. In deze gevallen kan de weergave van de extensie de nodige stappen ondernemen om door de gebruiker opgegeven instellingen te valideren. Anderzijds kiezen sommige gebruikers ervoor om tags-API's rechtstreeks te gebruiken zonder de hulp van een gebruikersinterface. Het doel van dit schema is om Experience Platform toe te staan correct te bevestigen dat de montagesobjecten die door gebruikers worden bewaard, ongeacht of een gebruikersinterface wordt gebruikt, in een formaat zijn dat met de bibliotheekmodule compatibel is die op het montagesobject tijdens runtime zal handelen.<br><br> een voorwerp van het voorbeeldschema is als volgt:<br>
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "number",
      "minimum": 1
    }
  },
  "required": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      Wij adviseren gebruikend een hulpmiddel zoals <a href="https://www.jsonschemavalidator.net/"> JSON- Schema validator </a> om uw schema manueel te testen.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Optioneel)</em></td>
      <td>Een array van objecten waarin elk object een transformatie vertegenwoordigt die op elk overeenkomend instellingsobject moet worden uitgevoerd wanneer het wordt uitgestraald in de runtimebibliotheek. Zie de sectie op <a href="#transforms"> transformeert </a> voor meer informatie over waarom dit kan nodig zijn en hoe het wordt gebruikt.</td>
    </tr>
  </tbody>
</table>

### Transformaties {#transforms}

Voor bepaalde specifieke gebruiksgevallen hebben extensies nodig dat de instellingsobjecten die zijn opgeslagen vanuit een weergave, door Experience Platform worden getransformeerd voordat ze worden uitgestraald in de runtimebibliotheek van de tag. U kunt vragen dat een of meer van deze transformaties plaatsvinden door de eigenschap `transforms` in te stellen wanneer u een typedefinitie definieert binnen uw `extension.json` . De eigenschap `transforms` is een array van objecten waarin elk object een transformatie vertegenwoordigt die moet plaatsvinden.

Voor alle transformaties zijn een `type` en een `propertyPath` vereist. De instructie `type` moet `function` , `remove` en `file` zijn en beschrijft welke transformatie Experience Platform op het instellingsobject moet toepassen. `propertyPath` is een door een punt gescheiden tekenreeks die tags doorgeeft waar de eigenschap moet worden gevonden die binnen het instellingsobject moet worden gewijzigd. Hier is een voorwerp van voorbeeldmontages en sommige `propertyPath` s:

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

* Als u een `propertyPath` van `foo.bar` instelt, transformeert u de `"A string"` -waarde.
* Als u een `propertyPath` van `foo.baz[]` instelt, transformeert u elke waarde in de `baz` -array.
* Als u een `propertyPath` van `foo.baz` instelt, transformeert u de array `baz` .

Eigenschapspaden kunnen elke combinatie van array- en objectnotatie gebruiken om transformaties toe te passen op elk niveau van het instellingsobject.

>[!WARNING]
>
>Het gebruik van arraynotatie in het kenmerk `propertyPath` (bijvoorbeeld `foo.baz[]` ) wordt nog niet ondersteund in de uitbreidingssandbox*tool.

In de onderstaande secties worden de beschikbare transformaties beschreven en hoe u deze kunt gebruiken.

#### Functietransformatie

Met de functie-transformatie kan code die door Experience Platform-gebruikers is geschreven, worden uitgevoerd door een bibliotheekmodule in de uitgestraalde runtimebibliotheek.

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

Op het punt dat het instellingsobject wordt opgeslagen vanuit de weergave van het handelingstype, is de code van de gebruiker gewoon een tekenreeks. Dit is goed omdat het behoorlijk aan en van JSON kan behoorlijk in series worden vervaardigd; nochtans, is het ook slecht omdat het typisch in de markering runtime bibliotheek als koord evenals in plaats van een uitvoerbare functie zou worden uitgestoten. Hoewel u kon proberen om de code binnen de de bibliotheekmodule van uw actietype uit te voeren gebruikend [`eval` ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval) of de aannemer van de Functie van a [ ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function), is het hoogst ontmoedigd toe te schrijven aan [ inhoudsveiligheidsbeleid ](https://developer.mozilla.org/en-US/docs/Web/Security/CSP) potentieel blokkerend uitvoering.

Als tussenoplossing voor deze situatie, vertelt het gebruiken van de functietransformatie Experience Platform om de code van de gebruiker in een uitvoerbare functie te verpakken wanneer het in de markering runtime bibliotheek wordt uitgegeven. Om ons voorbeeldprobleem op te lossen, zouden wij de transformatie op de typedefinitie in `extension.json` als volgt bepalen:

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
* `propertyPath` is een door een punt gescheiden tekenreeks die Experience Platform opgeeft waar de eigenschap moet worden gevonden die binnen het instellingsobject moet worden gewijzigd.
* `parameters` is een array met parameternamen die moeten worden opgenomen in de handtekening van de functie wrapping.

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

Uw bibliotheekmodule kan vervolgens de functie met de code van de gebruiker aanroepen en het argument `username` doorgeven.

#### Bestandstransformatie

Met de bestandstransformatie kan code die door Experience Platform-gebruikers is geschreven, worden verzonden naar een bestand dat losstaat van de runtimebibliotheek. Het bestand wordt samen met de tagruntime-bibliotheek gehost en kan vervolgens tijdens runtime naar wens worden geladen door de extensie.

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

We willen dat de code van de gebruiker in een afzonderlijk bestand wordt geplaatst in plaats van in de runtimebibliotheek van de tag. Wanneer een regel die onze actie gebruikt in de tagruntime-bibliotheek wordt geactiveerd, willen we de code van de gebruiker laden door een scriptelement aan de hoofdtekst van het document toe te voegen. Om ons voorbeeldprobleem op te lossen, zouden wij de transformatie op de definitie van actietype in `extension.json` als volgt bepalen:

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
* `propertyPath` is een door een punt gescheiden tekenreeks die Experience Platform opgeeft waar de eigenschap moet worden gevonden die binnen het instellingsobject moet worden gewijzigd.

Wanneer het instellingsobject wordt uitgestraald in de tagruntime-bibliotheek, wordt het als volgt getransformeerd:

```javascript
{
  foo: {
    bar: "//launch.cdn.com/path/abc.js"
  }
}
```

In dit geval is de waarde van `foo.bar` getransformeerd naar een URL. De exacte URL wordt bepaald op het moment dat de bibliotheek wordt gemaakt. Het bestand krijgt altijd de extensie `.js` en wordt geleverd met een JavaScript-georiënteerd MIME-type. In de toekomst kunnen we ondersteuning toevoegen voor andere MIME-typen.

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

De eigenschap `bar` wordt niet opgenomen in de runtimebibliotheek van de tag. Om ons voorbeeldprobleem op te lossen, zouden wij de transformatie op de definitie van actietype in `extension.json` als volgt bepalen:

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
* `propertyPath` is een door een punt gescheiden tekenreeks die Experience Platform opgeeft waar de eigenschap moet worden gevonden die binnen het instellingsobject moet worden gewijzigd.

Wanneer het instellingsobject wordt uitgestraald in de tagruntime-bibliotheek, wordt het als volgt getransformeerd:

```js
{
  foo: {
  }
}
```

In dit geval is de waarde van `foo.bar` verwijderd uit het instellingenobject.
