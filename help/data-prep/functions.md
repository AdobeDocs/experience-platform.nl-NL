---
keywords: Experience Platform;home;populaire onderwerpen;map csv;map csv-bestand;map csv-bestand toewijzen aan xdm;map csv aan xdm;ui-gids;mapper;mapping;toewijzingsvelden;toewijzingsfuncties;
solution: Experience Platform
title: Toewijzingsfuncties voor gegevenspremies
topic-legacy: overview
description: In dit document worden de toewijzingsfuncties geïntroduceerd die worden gebruikt met Data Prep.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: 7cb940019905240b36e96b834b9e5d0166c1324d
workflow-type: tm+mt
source-wordcount: '4286'
ht-degree: 2%

---

# Toewijzingsfuncties van Data Prep

De functies van de Prep van gegevens kunnen worden gebruikt om waarden te berekenen en te berekenen die op wat in brongebieden zijn ingegaan.

## Velden

Een veldnaam kan elke geldige id zijn: een reeks van Unicode-letters en -cijfers met een onbeperkte lengte, te beginnen met een letter, het dollarteken (`$`), of het onderstrepingsteken (`_`). De namen van variabelen zijn ook hoofdlettergevoelig.

Als deze conventie niet wordt gevolgd door een veldnaam, moet de veldnaam worden omwikkeld met `${}`. Als de veldnaam bijvoorbeeld &quot;Voornaam&quot; of &quot;Voornaam&quot; is, moet de naam als volgt worden omwikkeld `${First Name}` of `${First.Name}` respectievelijk.

Bovendien, als een gebiedsnaam is **alle** van de volgende gereserveerde trefwoorden: `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

Gegevens binnen subvelden zijn toegankelijk met behulp van de puntnotatie. Als er bijvoorbeeld een `name` -object, om toegang te krijgen tot `firstName` veld, gebruiken `name.firstName`.

## Lijst met functies

In de volgende tabellen worden alle ondersteunde toewijzingsfuncties weergegeven, inclusief voorbeeldexpressies en de resulterende uitvoer.

### Reeksfuncties {#string}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | Voegt de opgegeven tekenreeksen samen. | <ul><li>TEKENREEKS: De tekenreeksen die worden samengevoegd.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| ontploffen | Splitst de tekenreeks op basis van een regex en retourneert een array met onderdelen. Kan optioneel regex opnemen om de tekenreeks te splitsen. Standaard wordt de splitsing omgezet in &quot;,&quot;. De volgende scheidingstekens **behoefte** te ontsnappen `\`: `+, ?, ^, \|, ., [, (, {, ), *, $, \` Als u meerdere tekens opneemt als scheidingsteken, wordt het scheidingsteken behandeld als een scheidingsteken voor meerdere tekens. | <ul><li>TEKENREEKS: **Vereist** De tekenreeks die moet worden gesplitst.</li><li>REGEX: *Optioneel* De reguliere expressie die kan worden gebruikt om de tekenreeks te splitsen.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hallo, daar!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Retourneert de locatie/index van een subtekenreeks. | <ul><li>INVOER: **Vereist** De tekenreeks die wordt doorzocht.</li><li>SUBTEKENREEKS: **Vereist** De subtekenreeks waarnaar wordt gezocht binnen de tekenreeks.</li><li>START_POSITION: *Optioneel* De locatie waar moet worden gezocht in de tekenreeks.</li><li>VOORVALLEN: *Optioneel* De nde instantie die vanaf de beginpositie moet worden gezocht. Standaard is dit 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| vervanger | Vervangt de zoektekenreeks indien aanwezig in de oorspronkelijke tekenreeks. | <ul><li>INVOER: **Vereist** De invoertekenreeks.</li><li>TO_FIND: **Vereist** De tekenreeks die binnen de invoer moet worden opgezocht.</li><li>TO_REPLACE: **Vereist** De tekenreeks die de waarde binnen &quot;TO_FIND&quot; vervangt.</li></ul> | replacer(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Dit is een test ter vervanging van een tekenreeks |
| substr | Retourneert een subtekenreeks van een bepaalde lengte. | <ul><li>INVOER: **Vereist** De invoertekenreeks.</li><li>START_INDEX: **Vereist** De index van de invoertekenreeks waar de subtekenreeks begint.</li><li>LENGTE: **Vereist** De lengte van de subtekenreeks.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lager /<br>lcase | Zet een tekenreeks om in kleine letters. | <ul><li>INVOER: **Vereist** De tekenreeks die wordt omgezet in kleine letters.</li></ul> | lower (INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hallo&quot; |
| upper /<br>kauwen | Zet een tekenreeks om in hoofdletters. | <ul><li>INVOER: **Vereist** De tekenreeks die wordt omgezet in hoofdletters.</li></ul> | upper(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HELLO&quot; |
| split | Splitst een invoertekenreeks op een scheidingsteken. Het volgende scheidingsteken **behoeften** te ontsnappen `\`: `\`. Als u meerdere scheidingstekens opneemt, wordt de tekenreeks gesplitst **alle** van de scheidingstekens in de tekenreeks. | <ul><li>INVOER: **Vereist** De invoertekenreeks die wordt gesplitst.</li><li>SCHEIDINGSTEKEN: **Vereist** De tekenreeks die wordt gebruikt om de invoer te splitsen.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Hiermee wordt een lijst met objecten samengevoegd met het scheidingsteken. | <ul><li>SCHEIDINGSTEKEN: **Vereist** De tekenreeks die wordt gebruikt om de objecten met elkaar te verbinden.</li><li>OBJECTEN: **Vereist** Een array van tekenreeksen die worden gekoppeld.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | Hiermee wordt de linkerzijde van een tekenreeks met de andere opgegeven tekenreeks geplakt. | <ul><li>INVOER: **Vereist** De tekenreeks die wordt opgevuld. Deze tekenreeks kan null zijn.</li><li>TELLING: **Vereist** De grootte van de tekenreeks die moet worden opgevuld.</li><li>TOEVOEGEN: **Vereist** De tekenreeks waarmee de invoer moet worden geplakt. Als deze null of leeg is, wordt deze behandeld als één spatie.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzyzybat&quot; |
| rpad | Hiermee wordt de rechterzijde van een tekenreeks overgeladen met de andere opgegeven tekenreeks. | <ul><li>INVOER: **Vereist** De tekenreeks die wordt opgevuld. Deze tekenreeks kan null zijn.</li><li>TELLING: **Vereist** De grootte van de tekenreeks die moet worden opgevuld.</li><li>TOEVOEGEN: **Vereist** De tekenreeks waarmee de invoer moet worden geplakt. Als deze null of leeg is, wordt deze behandeld als één spatie.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Haalt de eerste &#39;n&#39;-tekens van de opgegeven tekenreeks op. | <ul><li>TEKENREEKS: **Vereist** De tekenreeks waarvoor u de eerste &#39;n&#39;-tekens ontvangt.</li><li>TELLING: **Vereist** De &#39;n&#39; tekens die u uit de tekenreeks wilt halen.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | Haalt de laatste &#39;n&#39;-tekens van de opgegeven tekenreeks op. | <ul><li>TEKENREEKS: **Vereist** De tekenreeks waarvoor u de laatste &#39;n&#39;-tekens ontvangt.</li><li>TELLING: **Vereist** De &#39;n&#39; tekens die u uit de tekenreeks wilt halen.</li></ul> | right (STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Verwijdert de witruimte aan het begin van de tekenreeks. | <ul><li>TEKENREEKS: **Vereist** De tekenreeks waaruit u de witruimte wilt verwijderen.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hallo&quot; |
| rtrim | Verwijdert de witruimte aan het einde van de tekenreeks. | <ul><li>TEKENREEKS: **Vereist** De tekenreeks waaruit u de witruimte wilt verwijderen.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hallo&quot; |
| trim | Verwijdert de witruimte van het begin en het einde van de tekenreeks. | <ul><li>TEKENREEKS: **Vereist** De tekenreeks waaruit u de witruimte wilt verwijderen.</li></ul> | trim (STRING) | trim(&quot; hello &quot;) | &quot;hallo&quot; |
| equals | Vergelijkt twee tekenreeksen om te bevestigen of deze gelijk zijn. Deze functie is hoofdlettergevoelig. | <ul><li>STRING1: **Vereist** De eerste tekenreeks die u wilt vergelijken.</li><li>STRING2: **Vereist** De tweede tekenreeks die u wilt vergelijken.</li></ul> | TEKENREEKS1. &#x200B;equals( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;equals &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Vergelijkt twee tekenreeksen om te bevestigen of deze gelijk zijn. Deze functie is **niet** hoofdlettergevoelig. | <ul><li>STRING1: **Vereist** De eerste tekenreeks die u wilt vergelijken.</li><li>STRING2: **Vereist** De tweede tekenreeks die u wilt vergelijken.</li></ul> | TEKENREEKS1. &#x200B;equalsIgnoreCase &#x200B;(STRING2) | &quot;string1&quot;. &#x200B;equalsIgnoreCase &#x200B;(&quot;STRING1) | true |

{style=&quot;table-layout:auto&quot;}

### Gewone expressiefuncties

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | Haalt groepen uit de invoertekenreeks op basis van een reguliere expressie. | <ul><li>TEKENREEKS: **Vereist** De tekenreeks waaruit de groepen worden geëxtraheerd.</li><li>REGEX: **Vereist** De reguliere expressie die moet overeenkomen met de groep.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;()[^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| match_regex | Controleert of de tekenreeks overeenkomt met de ingevoerde reguliere expressie. | <ul><li>TEKENREEKS: **Vereist** De tekenreeks die u controleert, komt overeen met de reguliere expressie.</li><li>REGEX: **Vereist** De reguliere expressie die u vergelijkt.</li></ul> | match_regex(STRING, REGEX) | match_regex(&quot;E259,E259B_009,1_1&quot;, &quot;()[^,]+),[^,]*,([^,]+)&quot;) | true |

{style=&quot;table-layout:auto&quot;}

### Hashingfuncties {#hashing}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | Neemt een input en veroorzaakt een knoeiboelwaarde gebruikend Veilig algoritme 1 van de Hash (SHA-1). | <ul><li>INVOER: **Vereist** The plain text to be hashed.</li><li>TEKEN: *Optioneel* De naam van de tekenset. Mogelijke waarden zijn UTF-8, UTF-16, ISO-8859-1 en US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Neemt een input en veroorzaakt een knoeiboelwaarde gebruikend Veilig algoritme 256 van de Hash (SHA-256). | <ul><li>INVOER: **Vereist** The plain text to be hashed.</li><li>TEKEN: *Optioneel* De naam van de tekenset. Mogelijke waarden zijn UTF-8, UTF-16, ISO-8859-1 en US-ASCII.</li></ul> | sha256 (INPUT, CHARSET) | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Neemt een input en veroorzaakt een knoeiboelwaarde gebruikend Veilig algoritme 512 van de Hash (SHA-512). | <ul><li>INVOER: **Vereist** The plain text to be hashed.</li><li>TEKEN: *Optioneel* De naam van de tekenset. Mogelijke waarden zijn UTF-8, UTF-16, ISO-8859-1 en US-ASCII.</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd07 88a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Gebruikt invoer en produceert een knoeiboelwaarde gebruikend MD5. | <ul><li>INVOER: **Vereist** The plain text to be hashed.</li><li>TEKEN: *Optioneel* De naam van de tekenset. Mogelijke waarden zijn UTF-8, UTF-16, ISO-8859-1 en US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Gebruikt een input een algoritme van de cyclische overtolligheidscontrole (CRC) om een cyclische code met 32 bits te produceren. | <ul><li>INVOER: **Vereist** The plain text to be hashed.</li><li>TEKEN: *Optioneel* De naam van de tekenset. Mogelijke waarden zijn UTF-8, UTF-16, ISO-8859-1 en US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style=&quot;table-layout:auto&quot;}

### URL-functies {#url}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Retourneert het protocol van de opgegeven URL. Als de invoer ongeldig is, wordt null geretourneerd. | <ul><li>URL: **Vereist** De URL waaruit het protocol moet worden geëxtraheerd.</li></ul> | get_url_protocol &#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | Geeft als resultaat de host van de opgegeven URL. Als de invoer ongeldig is, wordt null geretourneerd. | <ul><li>URL: **Vereist** De URL waarvan de host moet worden opgehaald.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Retourneert de poort van de opgegeven URL. Als de invoer ongeldig is, wordt null geretourneerd. | <ul><li>URL: **Vereist** De URL waarvan de poort moet worden geëxtraheerd.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | Retourneert het pad van de opgegeven URL. Standaard wordt het volledige pad geretourneerd. | <ul><li>URL: **Vereist** De URL waaruit het pad moet worden geëxtraheerd.</li><li>FULL_PATH: *Optioneel* Een Booleaanse waarde die bepaalt of het volledige pad wordt geretourneerd. Indien ingesteld op false, wordt alleen het einde van het pad geretourneerd.</li></ul> | get_url_path &#x200B;(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B; employee.csv&quot; |
| get_url_query_str | Retourneert de querytekenreeks van een opgegeven URL als een kaart met de naam van de queryreeks en de waarde van de queryreeks. | <ul><li>URL: **Vereist** De URL waarvan u de queryreeks probeert te verkrijgen.</li><li>ANKER: **Vereist** Bepaalt wat met het anker in het vraagkoord zal worden gedaan. Kan een van de volgende drie waarden hebben: &quot;preserve&quot;, &quot;remove&quot; of &quot;append&quot;.<br><br>Als de waarde &quot;preserve&quot; is, wordt het anker aan de geretourneerde waarde gekoppeld.<br>Als de waarde &quot;remove&quot; is, wordt het anker verwijderd van de geretourneerde waarde.<br>Als de waarde &quot;append&quot; is, wordt het anker geretourneerd als een aparte waarde.</li></ul> | get_url_query_str &#x200B;(URL, ANCHOR) | get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/there?name= &#x200B; ferret#nose&quot;, &quot;preserve&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/there?name= &#x200B; ferret#nose&quot;, &quot;remove&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com &#x200B;:8042/over/there &#x200B;?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

{style=&quot;table-layout:auto&quot;}

### Datum- en tijdfuncties {#date-and-time}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven. Meer informatie over de `date` functie is te vinden in de datumsectie van [handleiding voor gegevensverwerking](./data-handling.md#dates).

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Hiermee wordt de huidige tijd opgehaald. |  | now() | now() | `2021-10-26T10:10:24Z` |
| timestamp | Hiermee wordt de huidige Unix-tijd opgehaald. |  | timestamp() | timestamp() | 1571850624571 |
| format | Hiermee wordt de invoerdatum opgemaakt volgens een opgegeven notatie. | <ul><li>DATUM: **Vereist** De invoerdatum, als een ZonedDateTime-object, die u wilt opmaken.</li><li>INDELING: **Vereist** De notatie waarin de datum moet worden gewijzigd.</li></ul> | format(DATE, FORMAT) | formaat (2019-10-23T11):24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | `2019-10-23 11:24:35` |
| dformat | Converteert een tijdstempel naar een datumtekenreeks volgens een opgegeven notatie. | <ul><li>TIJDSTEMPEL: **Vereist** Het tijdstempel dat u wilt opmaken. Dit wordt geschreven in milliseconden.</li><li>INDELING: **Vereist** De indeling die u wilt instellen als tijdstempel.</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875000, &quot;yyyy-MM-dd&#39;T&#39;HH:mm:ss.SSSX&quot;) | `2019-10-23T11:24:35.000Z` |
| date | Converteert een datumtekenreeks naar een ZonedDateTime-object (ISO 8601-indeling). | <ul><li>DATUM: **Vereist** De tekenreeks die de datum vertegenwoordigt.</li><li>INDELING: **Vereist** De tekenreeks die staat voor de indeling van de brondatum.**Opmerking:** Dit doet **niet** vertegenwoordigen de notatie waarin u de datumtekenreeks wilt omzetten. </li><li>DEFAULT_DATE: **Vereist** De geretourneerde standaarddatum als de opgegeven datum null is.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | `2019-10-23T11:24:00Z` |
| date | Converteert een datumtekenreeks naar een ZonedDateTime-object (ISO 8601-indeling). | <ul><li>DATUM: **Vereist** De tekenreeks die de datum vertegenwoordigt.</li><li>INDELING: **Vereist** De tekenreeks die staat voor de indeling van de brondatum.**Opmerking:** Dit doet **niet** vertegenwoordigen de notatie waarin u de datumtekenreeks wilt omzetten. </li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | `2019-10-23T11:24:00Z` |
| date | Converteert een datumtekenreeks naar een ZonedDateTime-object (ISO 8601-indeling). | <ul><li>DATUM: **Vereist** De tekenreeks die de datum vertegenwoordigt.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24:00Z&quot; |
| date_part | Hiermee worden de delen van de datum opgehaald. De volgende componentwaarden worden ondersteund: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;kwartaal&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;dag&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;weekdag&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;uur&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisecond&quot;<br>&quot;ms&quot; | <ul><li>COMPONENT: **Vereist** Een tekenreeks die het deel van de datum vertegenwoordigt. </li><li>DATUM: **Vereist** De datum, in een standaardformaat.</li></ul> | date_part &#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11):55:12 inch) | 10 |
| set_date_part | Hiermee vervangt u een component in een bepaalde datum. De volgende onderdelen worden geaccepteerd: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dag&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;uur&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>COMPONENT: **Vereist** Een tekenreeks die het deel van de datum vertegenwoordigt. </li><li>WAARDE: **Vereist** De waarde die voor de component voor een bepaalde datum moet worden ingesteld.</li><li>DATUM: **Vereist** De datum, in een standaardformaat.</li></ul> | set_date_part &#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11):44:44,797 inch) | &quot;2016-04-09T11:44:44Z&quot; |
| make_date_time | Hiermee maakt u een datum op basis van onderdelen. Deze functie kan ook worden geïnduceerd met make_timestamp. | <ul><li>JAAR: **Vereist** Het jaar, geschreven in vier cijfers.</li><li>MAAND: **Vereist** De maand. De toegestane waarden zijn 1 tot en met 12.</li><li>DAG: **Vereist** De dag. De toegestane waarden zijn 1 tot en met 31.</li><li>UUR: **Vereist** Het uur. De toegestane waarden zijn 0 tot en met 23.</li><li>MINUUT: **Vereist** De minuut. De toegestane waarden zijn 0 tot en met 59.</li><li>NANOSECOND: **Vereist** De tweede nanowaarden. De toegestane waarden zijn 0 tot en met 999999999.</li><li>TIJDZONE: **Vereist** De tijdzone voor de datumtijd.</li></ul> | make_date_time &#x200B;(JAAR, MAAND, DAG, UUR, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time &#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | Converteert een datum in een tijdzone naar een datum in UTC. | <ul><li>DATUM: **Vereist** De datum die u wilt omzetten.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | Converteert een datum van één tijdzone naar een andere tijdzone. | <ul><li>DATUM: **Vereist** De datum die u wilt omzetten.</li><li>ZONE: **Vereist** De tijdzone waarnaar u de datum wilt converteren.</li></ul> | zone_date_to_zone &#x200B;(DATE, ZONE) | `zone_date_to_utc&#x200B;(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style=&quot;table-layout:auto&quot;} &#x200B;

### Hiërarchieën - Objecten {#objects}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | Controleert of een object leeg is. | <ul><li>INVOER: **Vereist** Het object dat u wilt controleren, is leeg.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| arrays_to_object | Hiermee maakt u een lijst met objecten. | <ul><li>INVOER: **Vereist** Een groepering van sleutel- en arrayparen.</li></ul> | arrays_to_object(INPUT) | monster nodig | monster nodig |
| to_object | Hiermee maakt u een object op basis van de opgegeven platte sleutel/waardeparen. | <ul><li>INVOER: **Vereist** Een platte lijst met sleutel/waardeparen.</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Maakt een object van de invoertekenreeks. | <ul><li>TEKENREEKS: **Vereist** De tekenreeks die wordt geparseerd om een object te maken.</li><li>VALUE_DELIMITER: *Optioneel* Het scheidingsteken dat een veld van de waarde scheidt. Het standaardscheidingsteken is `:`.</li><li>FIELD_DELIMITER: *Optioneel* Het scheidingsteken dat de waardeparen van het gebied scheidt. Het standaardscheidingsteken is `,`.</li></ul> | str_to_object &#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName=John,lastName=Doe,phone=123 456 7890&quot;, &quot;=&quot;, &quot;,&quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| contains_key | Controleert of het object bestaat in de brongegevens. **Opmerking:** Deze functie vervangt de vervangen `is_set()` functie. | <ul><li>INVOER: **Vereist** Het pad dat moet worden gecontroleerd als het bestaat in de brongegevens.</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | true |
| opheffen | Hiermee wordt de waarde van het kenmerk ingesteld op `null`. Dit zou moeten worden gebruikt wanneer u niet het gebied aan het doelschema wilt kopiëren. |  | nullify() | nullify() | `null` |
| get_keys | Parseert de sleutel/waardeparen en retourneert alle sleutels. | <ul><li>OBJECT: **Vereist** Het object waaruit de sleutels worden geëxtraheerd.</li></ul> | get_keys(OBJECT) | get_keys({&quot;boek1&quot;: &quot;Pride and Prerechterlijke&quot;, &quot;book2&quot;: &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | Parseert de sleutel/waardeparen en retourneert de waarde van de tekenreeks op basis van de opgegeven sleutel. | <ul><li>TEKENREEKS: **Vereist** De tekenreeks die u wilt parseren.</li><li>SLEUTEL: **Vereist** De sleutel waarvoor de waarde moet worden geëxtraheerd.</li><li>VALUE_DELIMITER: **Vereist** Het scheidingsteken tussen het veld en de waarde. Indien `null` Als er een lege tekenreeks wordt opgegeven, is deze waarde `:`.</li><li>FIELD_DELIMITER: *Optioneel* Het scheidingsteken tussen veld- en waardeparen. Indien `null` Als er een lege tekenreeks wordt opgegeven, is deze waarde `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John , lastName - Cena, phone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | John |

{style=&quot;table-layout:auto&quot;}

Zie de sectie voor informatie over de functie voor het kopiëren van objecten [onder](#object-copy).

### Hiërarchieën - arrays {#arrays}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| samenvoegen | Retourneert het eerste niet-null-object in een opgegeven array. | <ul><li>INVOER: **Vereist** De array waarvan u het eerste object met een andere waarde dan null wilt zoeken.</li></ul> | kool(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | Hiermee wordt het eerste element van de opgegeven array opgehaald. | <ul><li>INVOER: **Vereist** De array waarvan u het eerste element wilt zoeken.</li></ul> | first (INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Hiermee wordt het laatste element van de opgegeven array opgehaald. | <ul><li>INVOER: **Vereist** De array waarvan u het laatste element wilt zoeken.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | Voegt elementen aan het einde van de array toe. | <ul><li>ARRAY: **Vereist** De array waaraan u elementen toevoegt.</li><li>WAARDEN: De elementen die u aan de array wilt toevoegen.</li></ul> | add_to_array &#x200B;(ARRAY, VALUES) | add_to_array &#x200B;([&quot;a&quot;, &quot;b&quot;], &quot;c&quot;, &quot;d&quot;) | [&quot;a&quot;, &quot;b&quot;, &quot;c&quot;, &quot;d&quot;] |
| join_arrays | Combineert de arrays met elkaar. | <ul><li>ARRAY: **Vereist** De array waaraan u elementen toevoegt.</li><li>WAARDEN: De array(s) die u aan de bovenliggende array wilt toevoegen.</li></ul> | join_arrays &#x200B;(ARRAY, VALUES) | join_arrays &#x200B;([&quot;a&quot;, &quot;b&quot;], [&quot;c&quot;], [&quot;d&quot;, &quot;e&quot;]) | [&quot;a&quot;, &quot;b&quot;, &quot;c&quot;, &quot;d&quot;, &quot;e&quot;] |
| to_array | Neemt een lijst van input en zet het in een serie om. | <ul><li>INCLUDE_NULLS: **Vereist** Een booleaanse waarde die aangeeft of null al dan niet moet worden opgenomen in de responsarray.</li><li>WAARDEN: **Vereist** De elementen die in een array moeten worden omgezet.</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |
| size_of | Retourneert de grootte van de invoer. | <ul><li>INVOER: **Vereist** Het object waarvan u de grootte wilt vinden.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | Deze functie wordt gebruikt om alle elementen in de volledige invoerarray toe te voegen aan het einde van de array in Profile. Deze functie is **alleen** van toepassing tijdens updates. Indien gebruikt in de context van tussenvoegsels, keert deze functie de input zoals is terug. | <ul><li>ARRAY: **Vereist** De array die moet worden toegevoegd aan de array in het profiel.</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123 456] |
| upsert_array_replace | Deze functie wordt gebruikt om elementen in een array te vervangen. Deze functie is **alleen** van toepassing tijdens updates. Indien gebruikt in de context van tussenvoegsels, keert deze functie de input zoals is terug. | <ul><li>ARRAY: **Vereist** De array die de array in het profiel moet vervangen.</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [123 456] |

{style=&quot;table-layout:auto&quot;}

### Logische operatoren {#logical-operators}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decoderen | Op basis van een sleutel en een lijst met sleutelwaardeparen die als een array zijn samengevoegd, retourneert de functie de waarde als een sleutel wordt gevonden of retourneert deze een standaardwaarde als deze aanwezig is in de array. | <ul><li>SLEUTEL: **Vereist** De sleutel die moet worden aangepast.</li><li>OPTIONS: **Vereist** Een samengevoegde array van sleutel/waardeparen. Optioneel kan een standaardwaarde aan het einde worden geplaatst.</li></ul> | decoderen (SLEUTEL, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N.v.t.&quot;) | Als stateCode gegeven &quot;ca&quot;, &quot;Californië&quot; is.<br>Als stateCode gegeven &quot;pa&quot; is, &quot;Pennsylvania&quot;.<br>Als stateCode niet het volgende aanpast, &quot;n.v.t.&quot;. |
| iif | Evalueert een bepaalde booleaanse expressie en retourneert de opgegeven waarde op basis van het resultaat. | <ul><li>EXPRESSIE: **Vereist** De booleaanse expressie die wordt geëvalueerd.</li><li>TRUE_VALUE: **Vereist** De waarde die wordt geretourneerd als de expressie true oplevert.</li><li>FALSE_VALUE: **Vereist** De waarde die wordt geretourneerd als de expressie false oplevert.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;Waar&quot; |

{style=&quot;table-layout:auto&quot;}

### Samenvoeging {#aggregation}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Geeft als resultaat het minimum van de opgegeven argumenten. Gebruikt natuurlijke volgorde. | <ul><li>OPTIONS: **Vereist** Een of meer objecten die met elkaar kunnen worden vergeleken.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Geeft als resultaat het maximum van de opgegeven argumenten. Gebruikt natuurlijke volgorde. | <ul><li>OPTIONS: **Vereist** Een of meer objecten die met elkaar kunnen worden vergeleken.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style=&quot;table-layout:auto&quot;}

### Typeomzettingen {#type-conversions}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Zet een tekenreeks om in een BigInteger. | <ul><li>TEKENREEKS: **Vereist** De tekenreeks die moet worden omgezet in een BigInteger.</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;1000000.34&quot;) | 1000000,34 |
| to_decimal | Zet een tekenreeks om in een double. | <ul><li>TEKENREEKS: **Vereist** De tekenreeks die in een Double moet worden omgezet.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20,5 |
| to_float | Zet een tekenreeks om in een zwevende waarde. | <ul><li>TEKENREEKS: **Vereist** De tekenreeks die moet worden omgezet in een zwevende waarde.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12,34566 |
| to_integer | Zet een tekenreeks om in een geheel getal. | <ul><li>TEKENREEKS: **Vereist** De tekenreeks die in een geheel getal moet worden omgezet.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style=&quot;table-layout:auto&quot;}

### JSON-functies {#json}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Maak JSON-inhoud deserialize vanuit de opgegeven tekenreeks. | <ul><li>TEKENREEKS: **Vereist** De JSON-tekenreeks die moet worden gedeserialiseerd.</li></ul> | json_to_object &#x200B;(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;: &quot;Doe&quot;}) | Een object dat de JSON vertegenwoordigt. |

{style=&quot;table-layout:auto&quot;}

### Bijzondere verrichtingen {#special-operations}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | Hiermee genereert u een pseudo-willekeurige id. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fcda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

{style=&quot;table-layout:auto&quot;}

### Functies van gebruikersagent {#user-agent}

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Extraheert de naam van het besturingssysteem uit de userAgent-tekenreeks. | <ul><li>USER_AGENT: **Vereist** De userAgent-tekenreeks.</li></ul> | ua_os_name &#x200B;(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1, zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extraheert de belangrijkste versie van het besturingssysteem uit de userAgent-tekenreeks. | <ul><li>USER_AGENT: **Vereist** De userAgent-tekenreeks.</li></ul> | ua_os_version_major &#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1, zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Extraheert de versie van het besturingssysteem uit de userAgent-tekenreeks. | <ul><li>USER_AGENT: **Vereist** De userAgent-tekenreeks.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1, zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1. |
| ua_os_name_version | Extraheert de naam en versie van het besturingssysteem uit de userAgent-tekenreeks. | <ul><li>USER_AGENT: **Vereist** De userAgent-tekenreeks.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1, zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extraheert de agentenversie uit het koord van de gebruikersagent. | <ul><li>USER_AGENT: **Vereist** De userAgent-tekenreeks.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1, zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5,1 |
| ua_agent_version_major | Extraheert de agentennaam en belangrijkste versie van het koord van de gebruikersagent. | <ul><li>USER_AGENT: **Vereist** De userAgent-tekenreeks.</li></ul> | ua_agent_version_major &#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1, zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extraheert de agentennaam uit het koord van de gebruikersagent. | <ul><li>USER_AGENT: **Vereist** De userAgent-tekenreeks.</li></ul> | ua_agent_name &#x200B;(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1, zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extraheert de apparaatklasse uit de userAgent-tekenreeks. | <ul><li>USER_AGENT: **Vereist** De userAgent-tekenreeks.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1, zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefoon |

{style=&quot;table-layout:auto&quot;}

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

In het bovenstaande voorbeeld wordt `city` en `state` kenmerken worden ook automatisch bij uitvoering ingevoerd omdat de `address` object is toegewezen aan `addr`. Als u een `line2` -kenmerk in de XDM-structuur en uw invoergegevens bevatten ook een `line2` in de `address` -object, wordt deze automatisch opgenomen zonder dat de toewijzing handmatig hoeft te worden gewijzigd.

Om ervoor te zorgen dat de automatische mapping werkt, moet aan de volgende voorwaarden worden voldaan:

* Objecten op hoofdniveau moeten worden toegewezen;
* Nieuwe kenmerken moeten zijn gemaakt in het XDM-schema.
* Nieuwe kenmerken moeten overeenkomende namen hebben in het bronschema en het XDM-schema.

Als aan om het even welke voorwaarden niet wordt voldaan, dan moet u het bronschema aan het XDM schema manueel in kaart brengen gebruikend gegevens prep.