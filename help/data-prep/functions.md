---
keywords: Experience Platform;home;populaire onderwerpen;map csv;map csv-bestand;map csv-bestand toewijzen aan xdm;map csv aan xdm;ui-gids;mapper;mapping;toewijzingsvelden;toewijzingsfuncties;
solution: Experience Platform
title: Toewijzingsfuncties voor gegevenspremies
description: Dit document introduceert de toewijzingsfuncties die worden gebruikt met Data Prep.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: 6509447ff2e67eac7b6b41754981cd18eb52562e
workflow-type: tm+mt
source-wordcount: '5805'
ht-degree: 1%

---

# Toewijzingsfuncties van Data Prep

De functies van de Prep van gegevens kunnen worden gebruikt om waarden te berekenen en te berekenen die op wat in brongebieden zijn ingegaan.

## Velden

Een veldnaam kan elke geldige id zijn: een reeks van Unicode-letters en -cijfers met een onbeperkte lengte, te beginnen met een letter, het dollarteken (`$`) of het onderstrepingsteken (`_`). De namen van variabelen zijn ook hoofdlettergevoelig.

Als deze conventie niet wordt gevolgd door een veldnaam, moet de veldnaam worden teruggekoppeld met `${}` . Als de veldnaam bijvoorbeeld &quot;Voornaam&quot; of &quot;Voornaam&quot; is, moet de naam als `${First Name}` respectievelijk `${First\.Name}` worden omwikkeld.

>[!TIP]
>
>Wanneer het in wisselwerking staan met hiërarchieën, als een kindattribuut een periode (`.`) heeft, moet u backslash (`\`) gebruiken om speciale karakters te ontsnappen. Voor meer informatie, lees de gids op [ het ontsnapen speciale karakters ](home.md#escape-special-characters).

Als een gebiedsnaam **om het even welke** van de volgende gereserveerde sleutelwoorden is, moet het met `${}{}` worden verpakt:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors, do, function, empty, size
```

Daarnaast bevatten gereserveerde trefwoorden ook alle mapfuncties die op deze pagina worden vermeld.

Gegevens binnen subvelden zijn toegankelijk met behulp van de puntnotatie. Als er bijvoorbeeld een `name` -object is, gebruikt u `name.firstName` om toegang te krijgen tot het `firstName` -veld.

## Lijst met functies

In de volgende tabellen worden alle ondersteunde toewijzingsfuncties weergegeven, inclusief voorbeeldexpressies en de resulterende uitvoer.

### Reeksfuncties {#string}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | Voegt de opgegeven tekenreeksen samen. | <ul><li>STRING: De tekenreeksen die worden samengevoegd.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| ontploffen | Splitst de tekenreeks op basis van een regex en retourneert een array met onderdelen. Kan optioneel regex opnemen om de tekenreeks te splitsen. Standaard wordt de splitsing omgezet in &quot;,&quot;. De volgende scheidingstekens **moeten** met `\` worden ontsnapt: `+, ?, ^, \|, ., [, (, {, ), *, $, \` als u veelvoudige karakters als afbakening omvat, zal het scheidingsteken als multi-karakterscheidingsteken worden behandeld. | <ul><li>STRING: **Vereiste** het koord dat moet worden gesplitst.</li><li>REGEX: *Facultatieve* De regelmatige uitdrukking die kan worden gebruikt om het koord te verdelen.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hallo, daar!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Retourneert de locatie/index van een subtekenreeks. | <ul><li>INPUT: **Vereiste** het koord dat wordt gezocht.</li><li>SUBSTRING: **Vereiste** substring die binnen het koord wordt gezocht.</li><li>START_POSITION: *Facultatieve* de plaats van waar te beginnen in het koord te kijken.</li><li>VOORVALLEN: *Facultatieve* het nde voorkomen om van de beginpositie te zoeken. Standaard is dit 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| vervanger | Vervangt de zoektekenreeks indien aanwezig in de oorspronkelijke tekenreeks. | <ul><li>INPUT: **Vereiste** het inputkoord.</li><li>TO_FIND: **Vereiste** het koord om binnen de input omhoog te kijken.</li><li>TO_REPLACE: **Vereiste** het koord dat de waarde binnen &quot;TO_FIND&quot;zal vervangen.</li></ul> | replacer(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Dit is een test ter vervanging van een tekenreeks |
| substr | Retourneert een subtekenreeks van een bepaalde lengte. | <ul><li>INPUT: **Vereiste** het inputkoord.</li><li>START_INDEX: **Vereiste** de index van het inputkoord waar substring begint.</li><li>LENGTH: **Vereiste** de lengte van substring.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br> case | Zet een tekenreeks om in kleine letters. | <ul><li>INPUT: **Vereiste** het koord dat in kleine letters zal worden omgezet.</li></ul> | lower (INPUT) | lower (&quot;HeLLo&quot;) <br> geval (&quot;HeLLo&quot;) | &quot;hallo&quot; |
| upper /<br> ucase | Zet een tekenreeks om in hoofdletters. | <ul><li>INPUT: **Vereiste** het koord dat in hoofdletters zal worden omgezet.</li></ul> | upper(INPUT) | upper (&quot;HeLLo&quot;) <br> ucase (&quot;HeLLo&quot;) | HELLO |
| split | Splitst een invoertekenreeks op een scheidingsteken. Het volgende separator **moet** met `\` worden ontsnapt: `\`. Als u veelvoudige afbakeningen omvat, zal het koord op **om het even welk** van de afbakenaars huidig in het koord verdelen. **Nota:** Deze functie keert slechts niet-krachteloze indexen van het koord, ongeacht de aanwezigheid van separator terug. Wanneer alle indexen, inclusief null, in de resulterende array zijn vereist, gebruikt u in plaats daarvan de functie &quot;explode&quot;. | <ul><li>INPUT: **Vereiste** het inputkoord dat zal worden gesplitst.</li><li>SEPARATOR: **Vereist** het koord dat wordt gebruikt om de input te verdelen.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Hiermee wordt een lijst met objecten samengevoegd met het scheidingsteken. | <ul><li>SEPARATOR: **Vereiste** het koord dat zal worden gebruikt om zich bij de voorwerpen aan te sluiten.</li><li>OBJECTEN: **Vereiste** een serie van koorden die zullen worden aangesloten.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | Hiermee wordt de linkerzijde van een tekenreeks met de andere opgegeven tekenreeks geplakt. | <ul><li>INPUT: **Vereiste** het koord dat uit zal worden opgevuld. Deze tekenreeks kan null zijn.</li><li>COUNT: **Vereiste** de grootte van het uit te vullen koord.</li><li>PADDING: **Vereiste** het koord om de input met te stoten. Als deze null of leeg is, wordt deze behandeld als één spatie.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzyzybat&quot; |
| rpad | Hiermee wordt de rechterzijde van een tekenreeks overgeladen met de andere opgegeven tekenreeks. | <ul><li>INPUT: **Vereiste** het koord dat uit zal worden opgevuld. Deze tekenreeks kan null zijn.</li><li>COUNT: **Vereiste** de grootte van het uit te vullen koord.</li><li>PADDING: **Vereiste** het koord om de input met te stoten. Als deze null of leeg is, wordt deze behandeld als één spatie.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Haalt de eerste &#39;n&#39;-tekens van de opgegeven tekenreeks op. | <ul><li>STRING: **Vereiste** het koord u de eerste &quot;n&quot;karakters voor krijgt.</li><li>COUNT: **Vereiste** de &quot;n&quot;karakters u van het koord wilt krijgen.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | Haalt de laatste &#39;n&#39;-tekens van de opgegeven tekenreeks op. | <ul><li>STRING: **Vereiste** het koord u de laatste &quot;n&quot;karakters voor krijgt.</li><li>COUNT: **Vereiste** de &quot;n&quot;karakters u van het koord wilt krijgen.</li></ul> | right (STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Verwijdert de witruimte aan het begin van de tekenreeks. | <ul><li>STRING: **Vereiste** het koord u whitespace van wilt verwijderen.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hallo&quot; |
| rtrim | Verwijdert de witruimte aan het einde van de tekenreeks. | <ul><li>STRING: **Vereiste** het koord u whitespace van wilt verwijderen.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hallo&quot; |
| trim | Verwijdert de witruimte van het begin en het einde van de tekenreeks. | <ul><li>STRING: **Vereiste** het koord u whitespace van wilt verwijderen.</li></ul> | trim (STRING) | trim(&quot; hello &quot;) | &quot;hallo&quot; |
| equals | Vergelijkt twee tekenreeksen om te bevestigen of deze gelijk zijn. Deze functie is hoofdlettergevoelig. | <ul><li>STRING1: **Vereiste** het eerste koord u wilt vergelijken.</li><li>STRING2: **Vereiste** het tweede koord u wilt vergelijken.</li></ul> | TEKENREEKS1. &#x200B;equals( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;equals &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Vergelijkt twee tekenreeksen om te bevestigen of deze gelijk zijn. Deze functie is **niet** gevoelig geval. | <ul><li>STRING1: **Vereiste** het eerste koord u wilt vergelijken.</li><li>STRING2: **Vereiste** het tweede koord u wilt vergelijken.</li></ul> | TEKENREEKS1. &#x200B;equalsIgnoreCase &#x200B;(STRING2) | &quot;string1&quot;. &#x200B;equalsIgnoreCase &#x200B;(&quot;STRING1) | true |

{style="table-layout:auto"}

### Gewone expressiefuncties

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | Haalt groepen uit de invoertekenreeks op basis van een reguliere expressie. | <ul><li>STRING: **Vereiste** het koord dat u de groepen uit haalt.</li><li>REGEX: **Vereiste** de regelmatige uitdrukking die u de groep wilt aanpassen.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B; (&quot;E259, E259B_009, 1_1&quot;&#x200B;, &quot;([^, ]+), [^, ] *, ([^, ]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| match_regex | Controleert of de tekenreeks overeenkomt met de ingevoerde reguliere expressie. | <ul><li>STRING: **Vereiste** het koord dat u controleert past de regelmatige uitdrukking aan.</li><li>REGEX: **Vereiste** de regelmatige uitdrukking die u tegen vergelijkt.</li></ul> | match_regex(STRING, REGEX) | match_regex (&quot;E259,E259B_009,1_1&quot;, &quot;([^, ]+), [^, ] *, ([^, ]+)&quot;) | true |

{style="table-layout:auto"}

### Hashingfuncties {#hashing}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | Neemt een input en veroorzaakt een knoeiboelwaarde gebruikend Veilig algoritme 1 van de Hash (SHA-1). | <ul><li>INPUT: **Vereiste** de gewone tekst om worden gehakt.</li><li>CHARSET: *Facultatieve* De naam van de karakterreeks. Mogelijke waarden zijn UTF-8, UTF-16, ISO-8859-1 en US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Neemt een input en veroorzaakt een knoeiboelwaarde gebruikend Veilig algoritme 256 van de Hash (SHA-256). | <ul><li>INPUT: **Vereiste** de gewone tekst om worden gehakt.</li><li>CHARSET: *Facultatieve* De naam van de karakterreeks. Mogelijke waarden zijn UTF-8, UTF-16, ISO-8859-1 en US-ASCII.</li></ul> | sha256 (INPUT, CHARSET) | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Neemt een input en veroorzaakt een knoeiboelwaarde gebruikend Veilig algoritme 512 van de Hash (SHA-512). | <ul><li>INPUT: **Vereiste** de gewone tekst om worden gehakt.</li><li>CHARSET: *Facultatieve* De naam van de karakterreeks. Mogelijke waarden zijn UTF-8, UTF-16, ISO-8859-1 en US-ASCII.</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd07 88a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Gebruikt invoer en produceert een knoeiboelwaarde gebruikend MD5. | <ul><li>INPUT: **Vereiste** de gewone tekst om worden gehakt.</li><li>CHARSET: *Facultatieve* De naam van de karakterreeks. Mogelijke waarden zijn UTF-8, UTF-16, ISO-8859-1 en US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Gebruikt een input een algoritme van de cyclische overtolligheidscontrole (CRC) om een cyclische code met 32 bits te produceren. | <ul><li>INPUT: **Vereiste** de gewone tekst om worden gehakt.</li><li>CHARSET: *Facultatieve* De naam van de karakterreeks. Mogelijke waarden zijn UTF-8, UTF-16, ISO-8859-1 en US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style="table-layout:auto"}

### URL-functies {#url}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Retourneert het protocol van de opgegeven URL. Als de invoer ongeldig is, wordt null geretourneerd. | <ul><li>URL: **Vereiste** URL waarvan het protocol moet worden gehaald.</li></ul> | get_url_protocol &#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | Geeft als resultaat de host van de opgegeven URL. Als de invoer ongeldig is, wordt null geretourneerd. | <ul><li>URL: **Vereiste** URL waarvan de gastheer moet worden gehaald.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Retourneert de poort van de opgegeven URL. Als de invoer ongeldig is, wordt null geretourneerd. | <ul><li>URL: **Vereiste** URL waarvan de haven moet worden gehaald.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | Retourneert het pad van de opgegeven URL. Standaard wordt het volledige pad geretourneerd. | <ul><li>URL: **Vereiste** URL waarvan de weg moet worden gehaald.</li><li>FULL_PATH: *Facultatieve* een booleaanse waarde die bepaalt als de volledige weg is teruggekeerd. Indien ingesteld op false, wordt alleen het einde van het pad geretourneerd.</li></ul> | get_url_path &#x200B;(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B; employee.csv&quot; |
| get_url_query_str | Retourneert de querytekenreeks van een opgegeven URL als een kaart met de naam van de queryreeks en de waarde van de queryreeks. | <ul><li>URL: **Vereiste** URL die u probeert om het vraagkoord van te krijgen.</li><li>ANCHOR: **Vereiste** bepaalt wat met het anker in het vraagkoord zal worden gedaan. Kan één van drie waarden zijn: &quot;behouden&quot;, &quot;verwijderen&quot; of &quot;toevoegen&quot;.<br><br> als de waarde &quot;behoudt&quot;is, zal het anker aan de teruggekeerde waarde in bijlage zijn.<br> als de waarde &quot;verwijdert&quot;is, zal het anker uit de teruggekeerde waarde worden verwijderd.<br> als de waarde &quot;toevoegt&quot;is, zal het anker als afzonderlijke waarde zijn teruggekeerd.</li></ul> | get_url_query_str &#x200B;(URL, ANCHOR) | get_url_query_str &#x200B; (&quot;foo://example.com:8042 &#x200B;/over/daar?name= &#x200B; ferret#nose&quot;, &quot;behouden&quot;) <br> get_url_query_str &#x200B; (&quot;foo://example.com:8042 &#x200B;/over/daar?name= &#x200B; ferret#nose&quot;, &quot;remove&quot;) <br> get get_url_query_str &#x200B; (&quot;foo://example.com 2:04/over/daar?=daar ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |
| get_url_encoded | Deze functie gebruikt een URL als invoer en vervangt of codeert de speciale tekens met ASCII-tekens. Voor meer informatie over speciale karakters, te lezen gelieve de [ lijst van speciale karakters ](#special-characters) in bijlage van dit document. | <ul><li>URL: **Vereiste** input URL met speciale karakters die u met karakters wilt vervangen of coderen ASCII.</li></ul> | get_url_encoded(URL) | get_url_encoded(&quot;https </span>://example.com/partneralliance_asia-pacific_2022&quot;) | https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022 |
| get_url_decodeerd | Deze functie neemt een URL als invoer en decodeert de ASCII-tekens tot speciale tekens.  Voor meer informatie over speciale karakters, te lezen gelieve de [ lijst van speciale karakters ](#special-characters) in bijlage van dit document. | <ul><li>URL: **Vereiste** input URL met karakters ASCII die u in speciale karakters wilt decoderen.</li></ul> | get_url_decode(URL) | get_url_decoded(&quot;https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022&quot;) | https</span>://example.com/partnership_asia-pacific_2022 |

{style="table-layout:auto"}

### Datum- en tijdfuncties {#date-and-time}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven. Meer informatie over de `date` functie kan in de datumsectie van de [ gegeven worden gevonden behandelende gids ](./data-handling.md#dates).

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Hiermee wordt de huidige tijd opgehaald. | | now() | now() | `2021-10-26T10:10:24Z` |
| tijdstempel | Hiermee wordt de huidige Unix-tijd opgehaald. | | timestamp() | timestamp() | 1571850624571 |
| format | Hiermee wordt de invoerdatum opgemaakt volgens een opgegeven notatie. | <ul><li>DATUM: **Vereiste** de inputdatum, als voorwerp ZonedDateTime, die u wilt formatteren.</li><li>FORMAT: **Vereiste** het formaat dat u de datum wilt worden veranderd in.</li></ul> | format(DATE, FORMAT) | formaat (2019-10-23T11 :24: 00+00:00, &quot;`yyyy-MM-dd HH:mm:ss`&quot;) | `2019-10-23 11:24:35` |
| dformat | Converteert een tijdstempel naar een datumtekenreeks volgens een opgegeven notatie. | <ul><li>TIMESTAMP: **Vereiste** timestamp u wilt formatteren. Dit wordt geschreven in milliseconden.</li><li>FORMAT: **Vereiste** het formaat dat u timestamp wilt worden.</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875000, &quot;`yyyy-MM-dd'T'HH:mm:ss.SSSX`&quot;) | `2019-10-23T11:24:35.000Z` |
| date | Converteert een datumtekenreeks naar een ZonedDateTime-object (ISO 8601-indeling). | <ul><li>DATUM: **Vereiste** het koord dat de datum vertegenwoordigt.</li><li>FORMAT: **Vereiste** het koord dat het formaat van de brondatum vertegenwoordigt.**Nota:** dit **** vertegenwoordigt niet het formaat u het datumkoord in wilt omzetten. </li><li>DEFAULT_DATE: **Vereiste** de teruggekeerde standaarddatum, als de verstrekte datum ongeldig is.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | `2019-10-23T11:24:00Z` |
| date | Converteert een datumtekenreeks naar een ZonedDateTime-object (ISO 8601-indeling). | <ul><li>DATUM: **Vereiste** het koord dat de datum vertegenwoordigt.</li><li>FORMAT: **Vereiste** het koord dat het formaat van de brondatum vertegenwoordigt.**Nota:** dit **** vertegenwoordigt niet het formaat u het datumkoord in wilt omzetten. </li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | `2019-10-23T11:24:00Z` |
| date | Converteert een datumtekenreeks naar een ZonedDateTime-object (ISO 8601-indeling). | <ul><li>DATUM: **Vereiste** het koord dat de datum vertegenwoordigt.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11 :24: 00Z&quot; |
| date_part | Hiermee worden de delen van de datum opgehaald. De volgende componentenwaarden worden gesteund: <br><br> &quot;jaar&quot;<br> &quot;jjjj&quot;<br> &quot;jj&quot;<br><br> &quot;kwart&quot;<br> &quot;qq&quot;<br> &quot;q&quot;<br><br> &quot;maand&quot;<br> &quot;mm&quot;<br> &quot;m&quot;<br><br> &quot;dag-van-jaar&quot;<br> &quot;dag&quot;<br> &quot;y&quot;<br><br> &quot;dag&quot;<br> 3} &quot;dd&quot;<br> &quot;d&quot;<br><br> &quot;week&quot;<br> &quot;ww&quot;<br> &quot;w&quot;<br><br> &quot;weekdag&quot;<br> &quot;dw&quot;<br> &quot;w&quot;<br><br> &quot;uur&quot;<br> &quot;hh&quot;<br> &quot;hh24&quot;<br> &quot;hh12&quot;<br><br> &quot;minuut&quot;<br> &quot;mi&quot;<br> &quot;n&quot;<br><br> &quot;seconde&quot;<br> &quot;ss&quot;<br> &quot;s&quot;<br><br> &quot;millisecond&quot;<br> &quot;SSS&quot; | <ul><li>COMPONENT: **Vereiste** een koord dat het deel van de datum vertegenwoordigt. </li><li>DATUM: **Vereiste** de datum, in een standaardformaat.</li></ul> | date_part &#x200B;(COMPONENT, DATE) | date_part (&quot;MM&quot;, date (&quot;2019-10-17 11 :55: 12&quot;) | 10 |
| set_date_part | Hiermee vervangt u een component in een bepaalde datum. De volgende componenten worden goedgekeurd: <br><br> &quot;jaar&quot;<br> &quot;jjjj&quot;<br> &quot;yy&quot;<br><br> &quot;maand&quot;<br> &quot;mm&quot;<br> &quot;m&quot;<br><br> &quot;dag&quot;<br> &quot;dd&quot;<br> &quot;d&quot;<br><br> &quot;uur&quot;<br> &quot;hh&quot;<br><br> &quot;minuut&quot;<br> &quot;mi&quot;<br> &quot;n&quot;<br><br> &quot;seconde&quot;<br> &quot;ss&quot;<br> &quot;s&quot; | <ul><li>COMPONENT: **Vereiste** een koord dat het deel van de datum vertegenwoordigt. </li><li>WAARDE: **Vereiste** de waarde voor de component voor een bepaalde datum te plaatsen.</li><li>DATUM: **Vereiste** de datum, in een standaardformaat.</li></ul> | set_date_part &#x200B;(COMPONENT, VALUE, DATE) | set_date_part (&quot;m&quot;, 4, date (&quot;2016-11-09T11 :44: 44.797&quot;) | &quot;2016-04-09T11 :44: 44Z&quot; |
| make_date_time | Hiermee maakt u een datum op basis van onderdelen. Deze functie kan ook worden geïnduceerd met make_timestamp. | <ul><li>JAAR: **Vereiste** het jaar, die in vier cijfers wordt geschreven.</li><li>MAAND: **vereiste** de maand. De toegestane waarden zijn 1 tot 12.</li><li>DAG: **Vereiste** de dag. De toegestane waarden zijn 1 tot 31.</li><li>HOUR: **Vereiste** het uur. De toegestane waarden zijn 0 tot 23.</li><li>MINUUT: **Vereiste** de minuut. De toegestane waarden zijn 0 tot en met 59.</li><li>NANOSECOND: **Vereiste** de nanotweede waarden. De toegestane waarden zijn 0 tot en met 999999999.</li><li>TIMEZONE: **Vereiste** de timezone voor de datumtijd.</li></ul> | make_date_time &#x200B;(JAAR, MAAND, DAG, UUR, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time &#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | Converteert een datum in een tijdzone naar een datum in UTC. | <ul><li>DATUM: **Vereiste** de datum die u probeert om te zetten.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | Converteert een datum van de ene tijdzone naar een andere tijdzone. | <ul><li>DATUM: **Vereiste** de datum die u probeert om te zetten.</li><li>ZONE: **Vereiste** de timezone die u probeert om de datum in om te zetten.</li></ul> | zone_date_to_zone &#x200B;(DATE, ZONE) | `zone_date_to_utc&#x200B;(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style="table-layout:auto"}

### Hiërarchieën - Objecten {#objects}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | Controleert of een object leeg is. | <ul><li>INPUT: **Vereiste** het voorwerp dat u probeert te controleren is leeg.</li></ul> | is_empty(INPUT) | `is_empty([1, null, 2, 3])` | false |
| arrays_to_object | Maakt een lijst met objecten. | <ul><li>INPUT: **Vereiste** een groepering van sleutel en serieparen.</li></ul> | arrays_to_object(INPUT) | `arrays_to_objects('sku', explode("id1\|id2", '\\\|'), 'price', [22.5,14.35])` | ```[{ "sku": "id1", "price": 22.5 }, { "sku": "id2", "price": 14.35 }]``` |
| to_object | Hiermee maakt u een object op basis van de opgegeven platte sleutel/waardeparen. | <ul><li>INPUT: **Vereiste** een vlakke lijst van sleutel/waardeparen.</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Maakt een object van de invoertekenreeks. | <ul><li>STRING: **Vereiste** het koord dat wordt ontleed om een voorwerp tot stand te brengen.</li><li>VALUE_DELIMITER: *Facultatieve* afbakening die een gebied van de waarde scheidt. Het standaardscheidingsteken is `:` .</li><li>FIELD_DELIMITER: *Facultatieve* afbakening die de paren van de gebiedswaarde scheidt. Het standaardscheidingsteken is `,` .</li></ul> | str_to_object &#x200B; (STRING, VALUE_DELIMITER, FIELD_DELIMITER) **Nota**: U kunt de `get()` functie samen met `str_to_object()` gebruiken om waarden voor de sleutels in het koord terug te winnen. | <ul><li>Voorbeeld 1: str_to_object(&quot;firstName - John ; lastName - ; - 123 345 7890&quot;, &quot;-&quot;, &quot;;&quot;)</li><li>Voorbeeld 2: str_to_object(&quot;firstName - John ; lastName - ; phone - 123 456 7890&quot;, &quot;-&quot;, &quot;;&quot;).get(&quot;firstName&quot;)</li></ul> | <ul><li>Voorbeeld 1:`{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}`</li><li>Voorbeeld 2: &quot;John&quot;</li></ul> |
| contains_key | Controleert of het object bestaat in de brongegevens. **Nota:** Deze functie vervangt de afgekeurde `is_set()` functie. | <ul><li>INPUT: **Vereiste** de weg die moet worden gecontroleerd als het binnen de brongegevens bestaat.</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | true |
| opheffen | Stelt de waarde van het kenmerk in op `null` . Dit zou moeten worden gebruikt wanneer u niet het gebied aan het doelschema wilt kopiëren. | | nullify() | nullify() | `null` |
| get_keys | Parseert de sleutel/waardeparen en retourneert alle sleutels. | <ul><li>OBJECT: **Vereiste** het voorwerp waar de sleutels van zullen worden gehaald.</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;: &quot;Pride and Prerechterlijke&quot;, &quot;book2&quot;: &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | Parseert de sleutel/waardeparen en retourneert de waarde van de tekenreeks op basis van de opgegeven sleutel. | <ul><li>STRING: **Vereiste** het koord dat u wilt ontleden.</li><li>SLEUTEL: **Vereiste** de sleutel waarvoor de waarde moet worden gehaald.</li><li>VALUE_DELIMITER: **Vereiste** Scheidingsteken dat het gebied en de waarde scheidt. Wanneer een `null` of een lege tekenreeks wordt opgegeven, is deze waarde `:` .</li><li>FIELD_DELIMITER: *Facultatieve* afbakening die gebied en waardeparen scheidt. Wanneer een `null` of een lege tekenreeks wordt opgegeven, is deze waarde `,` .</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John , lastName - Cena, phone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | John |
| map_get_values | Neemt een kaart en een zeer belangrijke input. Als de invoer één toets is, retourneert de functie de waarde die aan die toets is gekoppeld. Als de invoer een tekenreeksarray is, retourneert de functie alle waarden die overeenkomen met de opgegeven sleutels. Als de inkomende kaart dubbele sleutels heeft, moet de terugkeerwaarde de sleutels dedupliceren en unieke waarden terugkeren. | <ul><li>MAP: **Vereiste** de gegevens van de inputkaart.</li><li>SLEUTEL: **Vereiste** de sleutel kan één enkel koord of een koordserie zijn. Als een ander primitief type (data/number) wordt opgegeven, wordt het behandeld als een tekenreeks.</li></ul> | get_values(MAP, KEY) | Gelieve te zien [ bijlage ](#map_get_values) voor een codesteekproef. | |
| map_has_keys | Als een of meer invoersleutels worden opgegeven, retourneert de functie true. Als een tekenreeks-array wordt opgegeven als invoer, retourneert de functie waar op de eerste key die wordt gevonden. | <ul><li>MAP: **Vereiste** de gegevens van de inputkaart</li><li>SLEUTEL: **Vereiste** de sleutel kan één enkel koord of een koordserie zijn. Als een ander primitief type (data/number) wordt opgegeven, wordt het behandeld als een tekenreeks.</li></ul> | map_has_keys(MAP, KEY) | Gelieve te zien [ bijlage ](#map_has_keys) voor een codesteekproef. | |
| add_to_map | Accepteert minstens twee invoeren. Om het even welk aantal kaarten kan als input worden verstrekt. De Prep van gegevens keert één enkele kaart terug die alle zeer belangrijk-waardeparen van alle input heeft. Als één of meerdere sleutels (in de zelfde kaart of over kaarten) worden herhaald, dedupliceert Prep van Gegevens de sleutels zodat het eerste zeer belangrijk-waardepaar in de orde voortduurt dat zij in de input werden overgegaan. | MAP: **Vereiste** de gegevens van de inputkaart. | add_to_map(MAP 1, MAP 2, MAP 3, ...) | Gelieve te zien [ bijlage ](#add_to_map) voor een codesteekproef. | |
| object_to_map (Syntaxis 1) | Gebruik deze functie om gegevenstypen Kaart te maken. | <ul><li>SLEUTEL: **Vereiste** Sleutels moeten een koord zijn. Als er andere primitieve waarden zijn opgegeven, zoals gehele getallen of datums, worden deze automatisch omgezet in tekenreeksen en worden ze als tekenreeksen behandeld.</li><li>ANY_TYPE: **Vereiste** verwijst naar om het even welk gesteund XDM gegevenstype behalve Kaarten.</li></ul> | object_to_map(KEY, ANY_TYPE, KEY, ANY_TYPE, ...) | Gelieve te zien [ bijlage ](#object_to_map) voor een codesteekproef. | |
| object_to_map (syntaxis 2) | Gebruik deze functie om gegevenstypen Kaart te maken. | <ul><li>OBJECT: **Vereiste** U kunt een inkomende voorwerp of objecten serie verstrekken en aan een attribuut binnen het voorwerp als sleutel richten.</li></ul> | object_to_map(OBJECT) | Gelieve te zien [ bijlage ](#object_to_map) voor een codesteekproef. |
| object_to_map (syntaxis 3) | Gebruik deze functie om gegevenstypen Kaart te maken. | <ul><li>OBJECT: **Vereiste** U kunt een inkomende voorwerp of objecten serie verstrekken en aan een attribuut binnen het voorwerp als sleutel richten.</li></ul> | object_to_map(OBJECT_ARRAY, ATTRIBUTE_IN_OBJECT_TO_BE_USED_AS_A_KEY) | Gelieve te zien [ bijlage ](#object_to_map) voor een codesteekproef. |

{style="table-layout:auto"}

Voor informatie over de eigenschap van het objecten exemplaar, zie hieronder de sectie [ ](#object-copy).

### Hiërarchieën - arrays {#arrays}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| samenvoegen | Retourneert het eerste niet-null-object in een opgegeven array. | <ul><li>INPUT: **Vereiste** de serie u het eerste niet-krachteloze voorwerp van wilt vinden.</li></ul> | kool(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | Hiermee wordt het eerste element van de opgegeven array opgehaald. | <ul><li>INPUT: **Vereiste** de serie u het eerste element van wilt vinden.</li></ul> | first (INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Hiermee wordt het laatste element van de opgegeven array opgehaald. | <ul><li>INPUT: **Vereiste** de serie u het laatste element van wilt vinden.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | Voegt elementen aan het einde van de array toe. | <ul><li>ARRAY: **Vereiste** de serie die u elementen aan toevoegt.</li><li>WAARDEN: de elementen die u aan de array wilt toevoegen.</li></ul> | add_to_array &#x200B;(ARRAY, VALUES) | add_to_array &#x200B;([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_arrays | Combineert de arrays met elkaar. | <ul><li>ARRAY: **Vereiste** de serie die u elementen aan toevoegt.</li><li>WAARDEN: de array(en) die u aan de bovenliggende array wilt toevoegen.</li></ul> | join_arrays &#x200B;(ARRAY, VALUES) | join_series &#x200B; ([ &quot;a&quot;, &quot;b&quot;], [ &quot;c&quot;], [ &quot;d&quot;, &quot;e&quot;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | Neemt een lijst van input en zet het in een serie om. | <ul><li>INCLUDE_NULLS: **Vereiste** een booleaanse waarde om erop te wijzen al dan niet om nul in de reactieserie te omvatten.</li><li>WAARDEN: **Vereiste** de elementen die in een serie moeten worden omgezet.</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |
| size_of | Retourneert de grootte van de invoer. | <ul><li>INPUT: **Vereiste** het voorwerp dat u probeert om de grootte van te vinden.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| update_array_append | Deze functie wordt gebruikt om alle elementen in de volledige invoerarray toe te voegen aan het einde van de array in Profile. Deze functie is **slechts** toepasselijk tijdens updates. Indien gebruikt in de context van tussenvoegsels, keert deze functie de input zoals is terug. | <ul><li>ARRAY: **Vereiste** de serie om de serie in het Profiel toe te voegen.</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [ 123, 456 ] |
| upsert_array_replace | Deze functie wordt gebruikt om elementen in een array te vervangen. Deze functie is **slechts** toepasselijk tijdens updates. Indien gebruikt in de context van tussenvoegsels, keert deze functie de input zoals is terug. | <ul><li>ARRAY: **Vereiste** de serie om de serie in het Profiel te vervangen.</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [ 123, 456 ] |

{style="table-layout:auto"}

### Hiërarchieën - Toewijzen {#map}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| array_to_map | Deze functie neemt een objectarray en een sleutel als invoer en retourneert een kaart van het veld van de sleutel met de waarde als sleutel en het arrayelement als waarde. | <ul><li>INPUT: **Vereiste** de objecten serie u het eerste niet-krachteloze voorwerp van wilt vinden.</li><li>SLEUTEL: **Vereiste** de sleutel moet een gebiedsnaam in de objecten serie en het voorwerp als waarde zijn.</li></ul> | array_to_map(OBJECT [] INPUTS, KEY) | Lees het [ bijlage ](#object_to_map) voor een codesteekproef. |
| object_to_map | Deze functie neemt een voorwerp als argument en keert een kaart van zeer belangrijk-waardeparen terug. | <ul><li>INPUT: **Vereiste** de objecten serie u het eerste niet-krachteloze voorwerp van wilt vinden.</li></ul> | object_to_map(OBJECT_INPUT) | &quot;object_to_map(address) where input is &quot; + &quot;address: {line1 : \&quot;345 park ave\&quot;,line2: \&quot;bldg 2\&quot;,City : \&quot;san jose\&quot;,State : \&quot;CA\&quot;,type: \&quot;office\&quot;} | Retourneert een kaart met opgegeven veldnaam- en waardeparen of null als de invoer null is. Bijvoorbeeld: `"{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"` |
| to_map | Deze functie neemt een lijst van ke-value paren en keert een kaart van zeer belangrijk-waardeparen terug. | | to_map(OBJECT_INPUT) | &quot;to_map(\&quot;firstName\&quot;, \&quot;John\&quot;, \&quot;lastName\&quot;, \&quot;Doe\&quot;)&quot; | Retourneert een kaart met opgegeven veldnaam- en waardeparen of null als de invoer null is. Bijvoorbeeld: `"{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"` |

{style="table-layout:auto"}

### Logische operatoren {#logical-operators}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decoderen | Op basis van een sleutel en een lijst met sleutelwaardeparen die als een array zijn samengevoegd, retourneert de functie de waarde als een sleutel wordt gevonden of retourneert deze een standaardwaarde als deze aanwezig is in de array. | <ul><li>SLEUTEL: **Vereiste** de sleutel die moet worden aangepast.</li><li>OPTIONS: **Vereiste** een samengevoegde serie van sleutel/waardeparen. Optioneel kan een standaardwaarde aan het einde worden geplaatst.</li></ul> | decoderen (SLEUTEL, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Als stateCode gegeven &quot;ca&quot;, &quot;Californië&quot; is.<br> als stateCode gegeven &quot;pa&quot;is, &quot;Pennsylvania&quot;.<br> als stateCode niet het volgende aanpast, &quot;n.v.t.&quot;. |
| iif | Evalueert een bepaalde booleaanse expressie en retourneert de opgegeven waarde op basis van het resultaat. | <ul><li>UITDRUKKING: **Vereiste** de booleaanse uitdrukking die wordt geëvalueerd.</li><li>TRUE_VALUE: **Vereiste** de waarde die is teruggekeerd als de uitdrukking aan waar evalueert.</li><li>FALSE_VALUE: **Vereiste** de waarde die is teruggekeerd als de uitdrukking aan vals evalueert.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;Waar&quot; |

{style="table-layout:auto"}

### Samenvoeging {#aggregation}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Geeft als resultaat het minimum van de opgegeven argumenten. Gebruikt natuurlijke volgorde. | <ul><li>OPTIONS: **Vereiste** Één of meerdere voorwerpen die met elkaar kunnen worden vergeleken.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Geeft als resultaat het maximum van de opgegeven argumenten. Gebruikt natuurlijke volgorde. | <ul><li>OPTIONS: **Vereiste** Één of meerdere voorwerpen die met elkaar kunnen worden vergeleken.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style="table-layout:auto"}

### Typeomzettingen {#type-conversions}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Zet een tekenreeks om in een BigInteger. | <ul><li>STRING: **Vereiste** het koord dat in een BigInteger moet worden omgezet.</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;1000000.34&quot;) | 1000000,34 |
| to_decimal | Zet een tekenreeks om in een double. | <ul><li>STRING: **Vereiste** het koord dat in een Dubbel moet worden omgezet.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20,5 |
| to_float | Zet een tekenreeks om in een zwevende waarde. | <ul><li>TEKENREEKS: **Vereiste** het koord dat in een Float moet worden omgezet.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12,34566 |
| to_integer | Zet een tekenreeks om in een geheel getal. | <ul><li>TEKENREEKS: **Vereiste** het koord dat in een Geheel moet worden omgezet.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style="table-layout:auto"}

### JSON-functies {#json}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Maak JSON-inhoud deserialize vanuit de opgegeven tekenreeks. | <ul><li>STRING: **vereiste** het koord JSON om worden gedeserialiseerd.</li></ul> | json_to_object &#x200B;(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;: &quot;Doe&quot;}) | Een object dat de JSON vertegenwoordigt. |

{style="table-layout:auto"}

### Bijzondere verrichtingen {#special-operations}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br> guid | Hiermee genereert u een pseudo-willekeurige id. | | uuid () <br> guid () | uuid () <br> guid () | 7c0267d2-bb74-4e1a-9275-3bf4fcda5f4<br> c7016dc7-3163-43f7-afc7-2e1c9c20633 |
| `fpid_to_ecid ` | Deze functie neemt een FPID-tekenreeks en zet deze om in een ECID die in Adobe Experience Platform- en Adobe Experience Cloud-toepassingen moet worden gebruikt. | <ul><li>STRING: **Vereiste** het koord FPID dat in ECID moet worden omgezet.</li></ul> | `fpid_to_ecid(STRING)` | `fpid_to_ecid("4ed70bee-b654-420a-a3fd-b58b6b65e991")` | `"28880788470263023831040523038280731744"` |

{style="table-layout:auto"}

### Functies van gebruikersagent {#user-agent}

Om het even welke gebruikersagent functies in de lijst hieronder kunnen één van beiden van de volgende waarden terugkeren:

* Telefoon - Een mobiel apparaat met een klein scherm (gewoonlijk &lt; 7 inch)
* Mobiel - Een mobiel apparaat dat nog moet worden geïdentificeerd. Dit mobiele apparaat kan een eReader, een tablet, een telefoon, een horloge, enz. zijn.

Voor meer informatie over de waarden van het apparatengebied, te lezen gelieve de [ lijst van de waarden van het apparatengebied ](#device-field-values) in bijlage van dit document.

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Extraheert de naam van het besturingssysteem uit de userAgent-tekenreeks. | <ul><li>USER_AGENT: **Vereiste** het koord van de gebruikersagent.</li></ul> | ua_os_name &#x200B;(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extraheert de belangrijkste versie van het besturingssysteem uit de userAgent-tekenreeks. | <ul><li>USER_AGENT: **Vereiste** het koord van de gebruikersagent.</li></ul> | ua_os_version_major &#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Extraheert de versie van het besturingssysteem uit de userAgent-tekenreeks. | <ul><li>USER_AGENT: **Vereiste** het koord van de gebruikersagent.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1. |
| ua_os_name_version | Extraheert de naam en de versie van het besturingssysteem uit de userAgent-tekenreeks. | <ul><li>USER_AGENT: **Vereiste** het koord van de gebruikersagent.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extraheert de agentenversie uit het koord van de gebruikersagent. | <ul><li>USER_AGENT: **Vereiste** het koord van de gebruikersagent.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5,1 |
| ua_agent_version_major | Extraheert de agentennaam en belangrijkste versie van het koord van de gebruikersagent. | <ul><li>USER_AGENT: **Vereiste** het koord van de gebruikersagent.</li></ul> | ua_agent_version_major &#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extraheert de agentennaam uit het koord van de gebruikersagent. | <ul><li>USER_AGENT: **Vereiste** het koord van de gebruikersagent.</li></ul> | ua_agent_name &#x200B;(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extraheert de apparaatklasse uit de userAgent-tekenreeks. | <ul><li>USER_AGENT: **Vereiste** het koord van de gebruikersagent.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefoon |

{style="table-layout:auto"}

### Analysefuncties {#analytics}

>[!NOTE]
>
>U mag de volgende analytische functies alleen gebruiken voor WebSDK- en Adobe Analytics-stromen.

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| aa_get_event_id | Extraheert de gebeurtenis-id uit een Analytics-gebeurtenistekenreeks. | <ul><li>EVENT_STRING: **Vereiste** het komma-gescheiden de gebeurteniskoord van de Analyse.</li><li>EVENT_NAME: **Vereiste** de gebeurtenisnaam om uit te halen en identiteitskaart van.</li></ul> | a_get_event_id(EVENT_STRING, EVENT_NAME) | aa_get_event_id(&quot;event101=5:123456,scOpen&quot;, &quot;event101&quot;) | 123456 |
| aa_get_event_value | Extraheert de gebeurteniswaarde uit een gebeurtenisreeks Analytics. Als de gebeurteniswaarde niet wordt opgegeven 1, wordt geretourneerd. | <ul><li>EVENT_STRING: **Vereiste** het komma-gescheiden de gebeurteniskoord van de Analyse.</li><li>EVENT_NAME: **Vereiste** de gebeurtenisnaam om een waarde uit te halen.</li></ul> | a_get_event_value(EVENT_STRING, EVENT_NAME) | aa_get_event_value(&quot;event101=5:123456,scOpen&quot;, &quot;event101&quot;) | 5 |
| aa_get_product_categorieën | Extraheert de productcategorie uit een productreeks van Analytics. | <ul><li>PRODUCTS_STRING: **Vereiste** het koord van de Producten van de Analyse.</li></ul> | a_get_product_Categorieën(PRODUCTS_STRING) | aa_get_product_category(&quot;;Voorbeeld product 1;1;3.50,Voorbeeld categorie 2;Voorbeeld product 2;1;5.99&quot;) | [ ongeldig, &quot;Categorie 2 van het Voorbeeld&quot;] |
| aa_get_product_names | Extraheert de productnaam uit een productreeks Analytics. | <ul><li>PRODUCTS_STRING: **Vereiste** het koord van de Producten van de Analyse.</li></ul> | a_get_product_names(PRODUCTS_STRING) | aa_get_product_names(&quot;;Voorbeeld product 1;1;3.50,Voorbeeld categorie 2;Voorbeeld product 2;1;5.99&quot;) | [ &quot;Voorbeeld product 1&quot;, &quot;Voorbeeld product 2&quot;] |
| aa_get_product_quantity | Extraheert de hoeveelheden uit een productreeks van Analytics. | <ul><li>PRODUCTS_STRING: **Vereiste** het koord van de Producten van de Analyse.</li></ul> | a_get_product_Quantities(PRODUCTS_STRING) | aa_get_product_Quantities(&quot;;Voorbeeld product 1;1;3.50,Voorbeeld categorie 2;Voorbeeld product 2&quot;) | [ &quot;1&quot;, ongeldig ] |
| aa_get_product_pricing | Extraheert de prijs uit een productreeks van Analytics. | <ul><li>PRODUCTS_STRING: **Vereiste** het koord van de Producten van de Analyse.</li></ul> | a_get_product_pricing(PRODUCTS_STRING) | aa_get_product_price(&quot;;Voorbeeld product 1;1;3.50,Voorbeeld categorie 2;Voorbeeld product 2&quot;) | [ &quot;3.50&quot;, null ] |
| aa_get_product_event_values | Extraheert waarden voor de benoemde gebeurtenis van de producttekenreeks als een array van tekenreeksen. | <ul><li>PRODUCTS_STRING: **Vereiste** het koord van de Producten van de Analyse.</li><li>EVENT_NAME: **Vereiste** de gebeurtenisnaam om waarden uit te halen.</li></ul> | a_get_product_event_values(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_values(&quot;;Voorbeeld product 1;1;4.20;event1=2.3\|event2=5:1;Voorbeeld product 2;1;4.20;event1=3\|event2=2:2&quot;, &quot;event1&quot;) | [ &quot;2.3&quot;, &quot;3&quot;] |
| aa_get_product_evars | Extraheert de var waarden voor de genoemde gebeurtenis van het productkoord als serie van koorden. | <ul><li>PRODUCTS_STRING: **Vereiste** het koord van de Producten van de Analyse.</li><li>EVAR_NAME: **Vereiste** de naam van eVar om te halen.</li></ul> | aa_get_product_evars(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_evars(&quot;;Voorbeeld product;1;6.69;;eVar1=Merchandising value&quot;, &quot;eVar1&quot;) | [ &quot;Merchandising value&quot;] |

{style="table-layout:auto"}

<!-- | aa_get_product_events | Extracts a named event from the products string as an array of objects. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_events(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_events(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | [`{"id": "1","value", "5"}`, `{"id": "2","value", "1"}`] |
| aa_get_product_event_ids | Extracts the IDs for the named event from the products string as an array of strings. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_event_ids(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_ids(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | ["1", "2"] | -->

### Objectkopie {#object-copy}

>[!TIP]
>
>De functie voor het kopiëren van objecten wordt automatisch toegepast wanneer een object in de bron wordt toegewezen aan een object in de XDM. Geen extra actie nodig van gebruikers.

U kunt de functie voor het kopiëren van objecten gebruiken om automatisch kenmerken van een object te kopiëren zonder wijzigingen aan te brengen in de toewijzing. Als uw brongegevens bijvoorbeeld een structuur hebben van:

```json
address{
        line1: 4191 Ridgebrook Way,
        city: San Jose,
        state: California
        }
```

en een XDM-structuur van:

```json
addr{
    addrLine1: 4191 Ridgebrook Way,
    city: San Jose,
    state: California
    }
```

Vervolgens wordt de toewijzing:

```json
address -> addr
address.line1 -> addr.addrLine1
```

In het bovenstaande voorbeeld worden de kenmerken `city` en `state` ook automatisch opgenomen bij uitvoering, omdat het object `address` wordt toegewezen aan `addr` . Als u een `line2` -kenmerk in de XDM-structuur moet maken en uw invoergegevens ook een `line2` in het `address` -object bevatten, wordt dit kenmerk automatisch opgenomen zonder dat u de toewijzing handmatig hoeft te wijzigen.

Om ervoor te zorgen dat de automatische mapping werkt, moet aan de volgende voorwaarden worden voldaan:

* Objecten op hoofdniveau moeten worden toegewezen;
* Nieuwe kenmerken moeten zijn gemaakt in het XDM-schema.
* Nieuwe kenmerken moeten overeenkomende namen hebben in het bronschema en het XDM-schema.

Als aan om het even welke voorwaarden niet wordt voldaan, dan moet u het bronschema aan het XDM schema manueel in kaart brengen gebruikend gegevens prep.

## Bijlage

Hieronder vindt u aanvullende informatie over het gebruik van Data Prep-toewijzingsfuncties

### Speciale tekens {#special-characters}

In de onderstaande tabel ziet u een lijst met gereserveerde tekens en de bijbehorende gecodeerde tekens.

| Gereserveerd teken | Gecodeerd teken |
| --- | --- |
| spatie | %20 |
| ! | %21 |
| ’ | %2 |
| Aantal | %23 |
| $ | %24 |
| % | %25 |
| &amp; | %26 |
| &#39; | %27 |
| ( | %28 |
| ) | %29 |
| * | %2A |
| + | %2B |
| , | %2C |
| / | %2F |
| : | %3A |
| ; | %3B |
| &lt; | %3C |
| = | %3D |
| > | %3E |
| ? | %3F |
| @ | %40 |
| [ | %5B |
| | | %5C |
| ] | %5D |
| ^ | %5E |
| ` | %6 |
| ~ | %7E |

{style="table-layout:auto"}

### Waarden voor apparaatvelden {#device-field-values}

In de onderstaande tabel wordt een lijst met apparaatveldwaarden en de bijbehorende beschrijvingen weergegeven.

| Apparaat | Beschrijving |
| --- | --- |
| Desktop | Een desktop of laptop. |
| Anonymiet | Een anoniem apparaat. In sommige gevallen zijn dit `useragents` die zijn gewijzigd door een anonymiisatiesoftware. |
| Onbekend | Een onbekend apparaat. Dit zijn meestal `useragents` die geen informatie over het apparaat bevatten. |
| Mobiel | Een mobiel apparaat dat nog moet worden geïdentificeerd. Dit mobiele apparaat kan een eReader, een tablet, een telefoon, een horloge, enz. zijn. |
| Tablet | Een mobiel apparaat met een groot scherm (gewoonlijk > 7 inch). |
| Telefoon | Een mobiel apparaat met een klein scherm (doorgaans &lt; 7 inch). |
| Controle | Een mobiel apparaat met een klein scherm (normaal &lt; 2 inch). Deze apparaten werken normaal als extra scherm voor een telefoon/tablettype van apparaat. |
| Augmented Reality | Een mobiel apparaat met AR-mogelijkheden. |
| Virtuele realiteit | Een mobiel apparaat met VR-mogelijkheden. |
| eReader | Een apparaat dat lijkt op een tablet, maar meestal met een [!DNL eInk] -scherm. |
| Vak Boven instellen | Een aangesloten apparaat dat interactie mogelijk maakt via een scherm ter grootte van een televisie. |
| TV | Een apparaat dat lijkt op de set-top box, maar dat in de tv is ingebouwd. |
| Toestel thuis | Een (gewoonlijk groot) huisapparaat, zoals een koelkast. |
| Gameconsole | Een vast gamesysteem zoals een [!DNL Playstation] of een [!DNL XBox] . |
| Handheldspelconsole | Een mobiel gamesysteem zoals een [!DNL Nintendo Switch] . |
| Stem | Een door spraak gestuurd apparaat zoals een [!DNL Amazon Alexa] of een [!DNL Google Home] . |
| Auto | Een op voertuigen gebaseerde browser. |
| Robot | Robots die een website bezoeken. |
| Robot Mobile | Robots die een website bezoeken, maar aangeven dat ze als een mobiele bezoeker willen worden beschouwd. |
| Robot Imitator | Robots die een website bezoeken, doen alsof dat robots zijn zoals [!DNL Google] , maar dat zijn ze niet. **Nota**: In de meeste gevallen, zijn de Imitators van Robot inderdaad robots. |
| Wolk | Een cloudgebaseerde toepassing. Dit zijn geen robots of hackers, maar toepassingen die verbinding moeten maken. Dit geldt ook voor [!DNL Mastodon] servers. |
| Hacker | Deze apparaatwaarde wordt gebruikt voor het geval dat scripts worden gedetecteerd in de `useragent` -tekenreeks. |

{style="table-layout:auto"}

### Codevoorbeelden {#code-samples}

#### map_get_values {#map-get-values}

+++Selecteren om voorbeeld weer te geven

```json
 example = "map_get_values(book_details,\"author\") where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "{\"author\": \"George R. R. Martin\"}"
```

+++

#### map_has_keys {#map_has_keys}

+++Selecteren om voorbeeld weer te geven

```json
 example = "map_has_keys(book_details,\"author\")where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "true"
```

+++

#### add_to_map {#add_to_map}

+++Selecteren om voorbeeld weer te geven

```json
example = "add_to_map(book_details, book_details2) where input is {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}" +
        "{\n" +
        "    \"book_details2\":\n" +
        "    {\n" +
        "        \"author\": \"Neil Gaiman\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-0-380-97365-0\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      result = "{\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      returns = "A new map with all elements from map and addends"
```

+++

#### object_to_map {#object_to_map}

**Syntaxis 1**

+++Selecteren om voorbeeld weer te geven

```json
example = "object_to_map(\"firstName\", \"John\", \"lastName\", \"Doe\")",
result = "{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"
```

+++

**Syntaxis 2**

+++Selecteren om voorbeeld weer te geven

```json
example = "object_to_map(address) where input is " +
  "address: {line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}",
result = "{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"
```

+++

**Syntaxis 3**

+++Selecteren om voorbeeld weer te geven

```json
example = "object_to_map(addresses,type)" +
        "\n" +
        "[\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "]" ,
result = "{\n" +
        "    \"home\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    \"work\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    \"office\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "}" 
```

+++

#### array_to_map {#array_to_map}

+++Selecteren om voorbeeld weer te geven

```json
example = "array_to_map(addresses, \"type\") where addresses is\n" +
  "\n" +
  "[\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "]" ,
result = "{\n" +
  "    \"home\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    \"work\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    \"office\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "}",
returns = "Returns a map with given field name and value pairs or null if input is null"
```

+++

