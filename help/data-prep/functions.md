---
keywords: Experience Platform;home;populaire onderwerpen;map csv;map csv-bestand;map csv-bestand toewijzen aan xdm;map csv aan xdm;ui-gids;mapper;mapping;toewijzingsvelden;toewijzingsfuncties;
solution: Experience Platform
title: Toewijzingsfuncties voor gegevenspremies
topic: ' - overzicht'
description: In dit document worden de toewijzingsfuncties geïntroduceerd die worden gebruikt met Data Prep.
translation-type: tm+mt
source-git-commit: fd2dffd5b8957833b670e9cb434517bcb0f886a3
workflow-type: tm+mt
source-wordcount: '3625'
ht-degree: 2%

---


# Toewijzingsfuncties van Data Prep

De functies van de Prep van gegevens kunnen worden gebruikt om waarden te berekenen en te berekenen die op wat in brongebieden zijn ingegaan.

## Velden

Een veldnaam kan elke geldige id zijn: een reeks van Unicode-letters en -cijfers met een onbeperkte lengte, te beginnen met een letter, het dollarteken (`$`) of het onderstrepingsteken (`_`). De namen van variabelen zijn ook hoofdlettergevoelig.

Als deze conventie niet wordt gevolgd door een veldnaam, moet de veldnaam worden teruggeplaatst met `${}`. Als de veldnaam bijvoorbeeld &quot;Voornaam&quot; of &quot;Voornaam&quot; is, moet de naam als respectievelijk `${First Name}` of `${First.Name}` worden omwikkeld.

Als een veldnaam **any** van de volgende gereserveerde trefwoorden is, moet deze bovendien worden verpakt met `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

Gegevens binnen subvelden zijn toegankelijk met behulp van de puntnotatie. Als er bijvoorbeeld een object `name` is, gebruikt u `name.firstName` om het veld `firstName` te openen.

## Lijst met functies

In de volgende tabellen worden alle ondersteunde toewijzingsfuncties weergegeven, inclusief voorbeeldexpressies en de resulterende uitvoer.

### Reeksfuncties

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
-------- | ----------- | ---------- | -------| ---------- | -------------
| concat | Voegt de opgegeven tekenreeksen samen. | <ul><li>TEKENREEKS: De tekenreeksen die worden samengevoegd.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| ontploffen | Splitst de tekenreeks op basis van een regex en retourneert een array met onderdelen. Kan optioneel regex opnemen om de tekenreeks te splitsen. Standaard wordt de splitsing omgezet in &quot;,&quot;. De volgende scheidingstekens **need** om met `\` te worden ontsnapt: `+, ?, ^, |, ., [, (, {, ), *, $, \` | <ul><li>TEKENREEKS: **Required** De tekenreeks die moet worden gesplitst.</li><li>REGEX: *Optioneel* De reguliere expressie die kan worden gebruikt om de tekenreeks te splitsen.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hallo, daar!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Retourneert de locatie/index van een subtekenreeks. | <ul><li>INVOER: **Required** De tekenreeks die wordt doorzocht.</li><li>SUBTEKENREEKS: **Required** Het substring waarnaar wordt gezocht binnen het koord.</li><li>START_POSITION: *Optioneel* De locatie waar moet worden gezocht in de tekenreeks.</li><li>VOORVALLEN: *Optioneel* Het nde exemplaar dat vanaf de beginpositie moet worden gezocht. Standaard is dit 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| vervanger | Vervangt de zoektekenreeks indien aanwezig in de oorspronkelijke tekenreeks. | <ul><li>INVOER: **Required** The input string.</li><li>TO_FIND: **Required** De tekenreeks die binnen de invoer moet worden opgezocht.</li><li>TO_REPLACE: **Required** The string that will replace the value within &quot;TO_FIND&quot;.</li></ul> | replacer(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Dit is een test ter vervanging van een tekenreeks |
| substr | Retourneert een subtekenreeks van een bepaalde lengte. | <ul><li>INVOER: **Required** The input string.</li><li>START_INDEX: **Required** De index van het inputkoord waar het substring begint.</li><li>LENGTE: **Required** The length of the substring.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | Zet een tekenreeks om in kleine letters. | <ul><li>INVOER: **Required** De tekenreeks die in kleine letters wordt omgezet.</li></ul> | lower (INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hallo&quot; |
| upper /<br>ucase | Zet een tekenreeks om in hoofdletters. | <ul><li>INVOER: **Required** De tekenreeks die wordt omgezet in hoofdletters.</li></ul> | upper(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HELLO&quot; |
| split | Splitst een invoertekenreeks op een scheidingsteken. Het volgende scheidingsteken **moet** worden beschermd met `\`: `\`. | <ul><li>INVOER: **Required** De invoertekenreeks die wordt gesplitst.</li><li>SCHEIDINGSTEKEN: **Required** The string that is used to split the input.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Hiermee wordt een lijst met objecten samengevoegd met het scheidingsteken. | <ul><li>SCHEIDINGSTEKEN: **Required** The string that will be used to join the objects.</li><li>OBJECTEN: **Required** Een serie van koorden die zullen worden aangesloten.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | Hiermee wordt de linkerzijde van een tekenreeks met de andere opgegeven tekenreeks geplakt. | <ul><li>INVOER: **Required** De tekenreeks die wordt opgevuld. Deze tekenreeks kan null zijn.</li><li>TELLING: **Required** The size of the string to be padding out.</li><li>TOEVOEGEN: **Required** The string to pad the input with. Als deze null of leeg is, wordt deze behandeld als één spatie.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzyzybat&quot; |
| rpad | Hiermee wordt de rechterzijde van een tekenreeks overgeladen met de andere opgegeven tekenreeks. | <ul><li>INVOER: **Required** De tekenreeks die wordt opgevuld. Deze tekenreeks kan null zijn.</li><li>TELLING: **Required** The size of the string to be padding out.</li><li>TOEVOEGEN: **Required** The string to pad the input with. Als deze null of leeg is, wordt deze behandeld als één spatie.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Haalt de eerste &#39;n&#39;-tekens van de opgegeven tekenreeks op. | <ul><li>TEKENREEKS: **Required** De tekenreeks waarvoor u de eerste &#39;n&#39;-tekens krijgt.</li><li>TELLING: **Required** The &quot;n&quot;karakters u van het koord wilt krijgen.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | Haalt de laatste &#39;n&#39;-tekens van de opgegeven tekenreeks op. | <ul><li>TEKENREEKS: **Required** The string you&#39;get the last &quot;n&quot; characters for.</li><li>TELLING: **Required** The &quot;n&quot;karakters u van het koord wilt krijgen.</li></ul> | right (STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Verwijdert de witruimte aan het begin van de tekenreeks. | <ul><li>TEKENREEKS: **Required** The string you want to remove the whitespace from.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hallo&quot; |
| rtrim | Verwijdert de witruimte aan het einde van de tekenreeks. | <ul><li>TEKENREEKS: **Required** The string you want to remove the whitespace from.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hallo&quot; |
| trim | Verwijdert de witruimte van het begin en het einde van de tekenreeks. | <ul><li>TEKENREEKS: **Required** The string you want to remove the whitespace from.</li></ul> | trim (STRING) | trim(&quot; hello &quot;) | &quot;hallo&quot; |
| equals | Vergelijkt twee tekenreeksen om te bevestigen of deze gelijk zijn. Deze functie is hoofdlettergevoelig. | <ul><li>STRING1: **Required** De eerste tekenreeks die u wilt vergelijken.</li><li>STRING2: **Required** De tweede tekenreeks die u wilt vergelijken.</li></ul> | TEKENREEKS1. &#x200B;equals( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;equals &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Vergelijkt twee tekenreeksen om te bevestigen of deze gelijk zijn. Deze functie is **niet** gevoelig geval. | <ul><li>STRING1: **Required** De eerste tekenreeks die u wilt vergelijken.</li><li>STRING2: **Required** De tweede tekenreeks die u wilt vergelijken.</li></ul> | TEKENREEKS1. &#x200B;equalsIgnoreCase &#x200B;(STRING2) | &quot;string1&quot;. &#x200B;equalsIgnoreCase &#x200B;(&quot;STRING1) | true |

&#x200B;

### Gewone expressiefuncties

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
-------- | ----------- | ---------- | -------| ---------- | -------------
| extract_regex | Haalt groepen uit de invoertekenreeks op basis van een reguliere expressie. | <ul><li>TEKENREEKS: **Required** De tekenreeks waaruit u de groepen extraheert.</li><li>REGEX: **Required** De regelmatige uitdrukking die u de groep wilt aanpassen.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| match_regex | Controleert of de tekenreeks overeenkomt met de ingevoerde reguliere expressie. | <ul><li>TEKENREEKS: **Required** De tekenreeks die u controleert, komt overeen met de reguliere expressie.</li><li>REGEX: **Required** De reguliere expressie die u vergelijkt.</li></ul> | match_regex(STRING, REGEX) | match_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | true |

### Hashingfuncties

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
-------- | ----------- | ---------- | -------| ---------- | -------------
| sha1 | Neemt een input en veroorzaakt een knoeiboelwaarde gebruikend Veilig algoritme 1 van de Hash (SHA-1). | <ul><li>INVOER: **Required** The plain text to be hashed.</li><li>TEKEN: *Optioneel* De naam van de tekenset. Mogelijke waarden zijn UTF-8, UTF-16, ISO-8859-1 en US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Neemt een input en veroorzaakt een knoeiboelwaarde gebruikend Veilig algoritme 256 van de Hash (SHA-256). | <ul><li>INVOER: **Required** The plain text to be hashed.</li><li>TEKEN: *Optioneel* De naam van de tekenset. Mogelijke waarden zijn UTF-8, UTF-16, ISO-8859-1 en US-ASCII.</li></ul> | sha256 (INPUT, CHARSET) | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Neemt een input en veroorzaakt een knoeiboelwaarde gebruikend Veilig algoritme 512 van de Hash (SHA-512). | <ul><li>INVOER: **Required** The plain text to be hashed.</li><li>TEKEN: *Optioneel* De naam van de tekenset. Mogelijke waarden zijn UTF-8, UTF-16, ISO-8859-1 en US-ASCII.</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd07 88a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Gebruikt invoer en produceert een knoeiboelwaarde gebruikend MD5. | <ul><li>INVOER: **Required** The plain text to be hashed.</li><li>TEKEN: *Optioneel* De naam van de tekenset. Mogelijke waarden zijn UTF-8, UTF-16, ISO-8859-1 en US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Gebruikt een input een algoritme van de cyclische overtolligheidscontrole (CRC) om een cyclische code met 32 bits te produceren. | <ul><li>INVOER: **Required** The plain text to be hashed.</li><li>TEKEN: *Optioneel* De naam van de tekenset. Mogelijke waarden zijn UTF-8, UTF-16, ISO-8859-1 en US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

### URL-functies

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
-------- | ----------- | ---------- | -------| ---------- | -------------
| get_url_protocol | Retourneert het protocol van de opgegeven URL. Als de invoer ongeldig is, wordt null geretourneerd. | <ul><li>URL: **Required** URL waarvan het protocol moet worden gehaald.</li></ul> | get_url_protocol &#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | Geeft als resultaat de host van de opgegeven URL. Als de invoer ongeldig is, wordt null geretourneerd. | <ul><li>URL: **Required** URL waarvan de gastheer moet worden gehaald.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Retourneert de poort van de opgegeven URL. Als de invoer ongeldig is, wordt null geretourneerd. | <ul><li>URL: **Required** URL waarvan de haven moet worden gehaald.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | Retourneert het pad van de opgegeven URL. Standaard wordt het volledige pad geretourneerd. | <ul><li>URL: **Required** URL waarvan de weg moet worden gehaald.</li><li>FULL_PATH: *Optioneel* Een booleaanse waarde die bepaalt of het volledige pad wordt geretourneerd. Indien ingesteld op false, wordt alleen het einde van het pad geretourneerd.</li></ul> | get_url_path &#x200B;(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B; employee.csv&quot; |
| get_url_query_str | Retourneert de queryreeks van een opgegeven URL. | <ul><li>URL: **Required** URL die u probeert om het vraagkoord van te krijgen.</li><li>ANKER: **Required** bepaalt wat met het anker in het vraagkoord zal worden gedaan. Kan een van de volgende drie waarden hebben: &quot;preserve&quot;, &quot;remove&quot; of &quot;append&quot;.<br><br>Als de waarde &quot;preserve&quot; is, wordt het anker aan de geretourneerde waarde gekoppeld.<br>Als de waarde &quot;remove&quot; is, wordt het anker verwijderd van de geretourneerde waarde.<br>Als de waarde &quot;append&quot; is, wordt het anker geretourneerd als een aparte waarde.</li></ul> | get_url_query_str &#x200B;(URL, ANCHOR) | get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/there name= &#x200B; ferret#nose&quot;, &quot;preserve&quot;)<br>get_url_query_str &#x200B;(&quot;&#x200B;/over/there?name= &#x200B; ferret#nose&quot;, &quot;a1/>get_url_query str &#x200B;(&quot;foo://example.com:804/over ?name=ferret#nose&quot;, &quot;append&quot;)<br> | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

### Datum- en tijdfuncties

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven. Meer informatie over de functie `date` vindt u in de [handleiding voor datumfuncties](./dates.md).

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
-------- | ----------- | ---------- | -------| ---------- | -------------
| now | Hiermee wordt de huidige tijd opgehaald. |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | Hiermee wordt de huidige Unix-tijd opgehaald. |  | timestamp() | timestamp() | 1571850624571 |
| format | Hiermee wordt de invoerdatum opgemaakt volgens een opgegeven notatie. | <ul><li>DATUM: **Required** De inputdatum, als voorwerp ZonedDateTime, die u wilt formatteren.</li><li>INDELING: **Required** Het formaat dat u de datum wilt veranderen in.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Converteert een tijdstempel naar een datumtekenreeks volgens een opgegeven notatie. | <ul><li>TIJDSTEMPEL: **Required** De tijdstempel u wilt formatteren. Dit wordt geschreven in milliseconden.</li><li>INDELING: **Required** De indeling waarin u de tijdstempel wilt wijzigen.</li></ul> | dformat &#x200B;(TIMESTAMP, FORMAT) | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23-okt-2019 11:24&quot; |
| date | Converteert een datumtekenreeks naar een ZonedDateTime-object (ISO 8601-indeling). | <ul><li>DATUM: **Required** De tekenreeks die de datum vertegenwoordigt.</li><li>INDELING: **Required** The string representing the format of the date.</li><li>DEFAULT_DATE: **Required** De teruggekeerde standaarddatum, als de verstrekte datum ongeldig is.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | &quot;2019-10-23T11:24Z&quot; |
| date | Converteert een datumtekenreeks naar een ZonedDateTime-object (ISO 8601-indeling). | <ul><li>DATUM: **Required** De tekenreeks die de datum vertegenwoordigt.</li><li>INDELING: **Required** The string representing the format of the date.</li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date | Converteert een datumtekenreeks naar een ZonedDateTime-object (ISO 8601-indeling). | <ul><li>DATUM: **Required** De tekenreeks die de datum vertegenwoordigt.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date_part | Hiermee worden de delen van de datum opgehaald. De volgende componentwaarden worden ondersteund: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarters&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot; a 11/>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;weekdag&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot; a28/>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisecond&quot;<br>&quot;ms&quot;<br><br><br> | <ul><li>COMPONENT: **Required** Een tekenreeks die het deel van de datum vertegenwoordigt. </li><li>DATUM: **Required** De datum, in een standaardformaat.</li></ul> | date_part &#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;) | 10 |
| set_date_part | Hiermee vervangt u een component in een bepaalde datum. De volgende onderdelen worden geaccepteerd: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;h&quot;&lt;a1 1/>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br> | <ul><li>COMPONENT: **Required** Een tekenreeks die het deel van de datum vertegenwoordigt. </li><li>WAARDE: **Required** De waarde die voor de component voor een bepaalde datum moet worden geplaatst.</li><li>DATUM: **Required** De datum, in een standaardformaat.</li></ul> | set_date_part &#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time | Hiermee maakt u een datum op basis van onderdelen. Deze functie kan ook worden geïnduceerd met make_timestamp. | <ul><li>JAAR: **Required** Het jaar, geschreven in vier cijfers.</li><li>MAAND: **Required** De maand. De toegestane waarden zijn 1 tot en met 12.</li><li>DAG: **Vereist** De dag. De toegestane waarden zijn 1 tot en met 31.</li><li>UUR: **Vereist** Het uur. De toegestane waarden zijn 0 tot en met 23.</li><li>MINUUT: **Required** De minuut. De toegestane waarden zijn 0 tot en met 59.</li><li>NANOSECOND: **Required** De nanotweede waarden. De toegestane waarden zijn 0 tot en met 999999999.</li><li>TIJDZONE: **Required** The timezone for the date time.</li></ul> | make_date_time &#x200B;(JAAR, MAAND, DAG, UUR, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time &#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | Converteert een datum in een tijdzone naar een datum in UTC. | <ul><li>DATUM: **Required** De datum die u probeert om te zetten.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12.000000999-&#x200B;07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | Converteert een datum van één tijdzone naar een andere tijdzone. | <ul><li>DATUM: **Required** De datum die u probeert om te zetten.</li><li>ZONE: **Required** De tijdzone die u probeert om de datum in om te zetten.</li></ul> | zone_date_to_zone &#x200B;(DATE, ZONE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:12&#x200B;.000000999-07:00&#x200B;[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

&#x200B;

### Hiërarchieën - Objecten

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
-------- | ----------- | ---------- | -------| ---------- | -------------
| size_of | Retourneert de grootte van de invoer. | <ul><li>INVOER: **Required** Het voorwerp dat u probeert om de grootte van te vinden.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | Controleert of een object leeg is. | <ul><li>INVOER: **Required** Het voorwerp dat u probeert te controleren is leeg.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| arrays_to_object | Hiermee maakt u een lijst met objecten. | <ul><li>INVOER: **Required** Een groepering van sleutel en serieparen.</li></ul> | arrays_to_object(INPUT) | monster nodig | monster nodig |
| to_object | Hiermee maakt u een object op basis van de opgegeven platte sleutel/waardeparen. | <ul><li>INVOER: **Required** Een vlakke lijst van sleutel/waardeparen.</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Maakt een object van de invoertekenreeks. | <ul><li>TEKENREEKS: **Required** De tekenreeks die wordt geparseerd om een object te maken.</li><li>VALUE_DELIMITER: *Optioneel* Het scheidingsteken dat een veld van de waarde scheidt. Het standaardscheidingsteken is `:`.</li><li>FIELD_DELIMITER: *Optioneel* Het scheidingsteken tussen waardeparen van velden. Het standaardscheidingsteken is `,`.</li></ul> | str_to_object &#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | phone - 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| is_set | Controleert of het object bestaat in de brongegevens. | <ul><li>INVOER: **Required** De weg om te controleren als het binnen de brongegevens bestaat.</li></ul> | is_set(INPUT) | is_set &#x200B;(&quot;evars.evar.field1&quot;) | true |
| opheffen | Stelt de waarde van het kenmerk in op `null`. Dit zou moeten worden gebruikt wanneer u niet het gebied aan het doelschema wilt kopiëren. |  | nullify() | nullify() | `null` |

### Hiërarchieën - arrays

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
-------- | ----------- | ---------- | -------| ---------- | -------------
| samenvoegen | Retourneert het eerste niet-null-object in een opgegeven array. | <ul><li>INVOER: **Required** De serie u het eerste niet-krachteloze voorwerp van wilt vinden.</li></ul> | kool(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | Hiermee wordt het eerste element van de opgegeven array opgehaald. | <ul><li>INVOER: **Required** De serie u het eerste element van wilt vinden.</li></ul> | first (INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Hiermee wordt het laatste element van de opgegeven array opgehaald. | <ul><li>INVOER: **Required** De serie u het laatste element van wilt vinden.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| to_array | Neemt een lijst van input en zet het in een serie om. | <ul><li>INCLUDE_NULLS: **Required** Een booleaanse waarde om erop te wijzen of om nulls in de reactierearray al dan niet te omvatten.</li><li>WAARDEN: **Required** De elementen die in een serie moeten worden omgezet.</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

### Logische operatoren

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
-------- | ----------- | ---------- | -------| ---------- | -------------
| decoderen | Op basis van een sleutel en een lijst met sleutelwaardeparen die als een array zijn samengevoegd, retourneert de functie de waarde als een sleutel wordt gevonden of retourneert deze een standaardwaarde als deze aanwezig is in de array. | <ul><li>SLEUTEL: **Vereist** De sleutel die moet worden aangepast.</li><li>OPTIONS: **Required** Een afgevlakte array van sleutel/waardeparen. Optioneel kan een standaardwaarde aan het einde worden geplaatst.</li></ul> | decoderen (SLEUTEL, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N.v.t.&quot;) | Als stateCode gegeven &quot;ca&quot;, &quot;Californië&quot; is.<br>Als stateCode gegeven &quot;pa&quot; is, &quot;Pennsylvania&quot;.<br>Als stateCode niet het volgende aanpast, &quot;n.v.t.&quot;. |
| iif | Evalueert een bepaalde booleaanse expressie en retourneert de opgegeven waarde op basis van het resultaat. | <ul><li>EXPRESSIE: **Required** De booleaanse uitdrukking die wordt geëvalueerd.</li><li>TRUE_VALUE: **Required** De waarde die is teruggekeerd als de uitdrukking aan waar evalueert.</li><li>FALSE_VALUE: **Required** De waarde die wordt geretourneerd als de expressie false oplevert.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;Waar&quot; |

### Samenvoeging

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
-------- | ----------- | ---------- | -------| ---------- | -------------
| min | Geeft als resultaat het minimum van de opgegeven argumenten. Gebruikt natuurlijke volgorde. | <ul><li>OPTIONS: **Required** Één of meerdere voorwerpen die met elkaar kunnen worden vergeleken.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Geeft als resultaat het maximum van de opgegeven argumenten. Gebruikt natuurlijke volgorde. | <ul><li>OPTIONS: **Required** Één of meerdere voorwerpen die met elkaar kunnen worden vergeleken.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

### Typeomzettingen

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
-------- | ----------- | ---------- | -------| ---------- | -------------
| to_bigint | Zet een tekenreeks om in een BigInteger. | <ul><li>TEKENREEKS: **Required** Het koord dat in een BigInteger moet worden omgezet.</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;1000000.34&quot;) | 1000000,34 |
| to_decimal | Zet een tekenreeks om in een double. | <ul><li>TEKENREEKS: **Required** Het koord dat in een Dubbel moet worden omgezet.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20,5 |
| to_float | Zet een tekenreeks om in een zwevende waarde. | <ul><li>TEKENREEKS: **Required** De tekenreeks die in een Float moet worden omgezet.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12,34566 |
| to_integer | Zet een tekenreeks om in een geheel getal. | <ul><li>TEKENREEKS: **Required** De tekenreeks die in een geheel getal moet worden omgezet.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

### JSON-functies

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
-------- | ----------- | ---------- | -------| ---------- | -------------
| json_to_object | Maak JSON-inhoud deserialize vanuit de opgegeven tekenreeks. | <ul><li>TEKENREEKS: **Required** The JSON string to be deserialized.</li></ul> | json_to_object &#x200B;(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;: &quot;Doe&quot;}) | Een object dat de JSON vertegenwoordigt. |

### Bijzondere verrichtingen

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
-------- | ----------- | ---------- | -------| ---------- | -------------
| uuid /<br>guid | Hiermee genereert u een pseudo-willekeurige id. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fcda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c20633 |

### Functies van gebruikersagent

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| -functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
-------- | ----------- | ---------- | -------| ---------- | -------------
| ua_os_name | Extraheert de naam van het besturingssysteem uit de userAgent-tekenreeks. | <ul><li>USER_AGENT: **Required** De userAgent-tekenreeks.</li></ul> | ua_os_name &#x200B;(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extraheert de belangrijkste versie van het besturingssysteem uit de userAgent-tekenreeks. | <ul><li>USER_AGENT: **Required** De userAgent-tekenreeks.</li></ul> | ua_os_version_major &#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Extraheert de versie van het besturingssysteem uit de userAgent-tekenreeks. | <ul><li>USER_AGENT: **Required** De userAgent-tekenreeks.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1. |
| ua_os_name_version | Extraheert de naam en versie van het besturingssysteem uit de userAgent-tekenreeks. | <ul><li>USER_AGENT: **Required** De userAgent-tekenreeks.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extraheert de agentenversie uit het koord van de gebruikersagent. | <ul><li>USER_AGENT: **Required** De userAgent-tekenreeks.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5,1 |
| ua_agent_version_major | Extraheert de agentennaam en belangrijkste versie van het koord van de gebruikersagent. | <ul><li>USER_AGENT: **Required** De userAgent-tekenreeks.</li></ul> | ua_agent_version_major &#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extraheert de agentennaam uit het koord van de gebruikersagent. | <ul><li>USER_AGENT: **Required** De userAgent-tekenreeks.</li></ul> | ua_agent_name &#x200B;(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extraheert de apparaatklasse uit de userAgent-tekenreeks. | <ul><li>USER_AGENT: **Required** De userAgent-tekenreeks.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1 zoals Mac OS X) AppleWebKit/534.46 (KHTML, zoals Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefoon |