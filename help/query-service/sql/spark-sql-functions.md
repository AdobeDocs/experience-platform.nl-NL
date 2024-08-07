---
keywords: Experience Platform;thuis;populaire onderwerpen;de vraagdienst;de dienst van de Vraag;spark sql;Spark sql;spark;spark sql functies;functies;
solution: Experience Platform
title: SQL-functies in Query Service parkeren
description: Leer over de gesteunde functies van SQL van de Vonk die SQL functionaliteit uitbreiden.
exl-id: 59e6d82b-3317-456d-8c56-3efd5978433a
source-git-commit: 7ac1521adb916313c8b53fe2a095821d756480be
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 0%

---

# [!DNL Spark] SQL-functies

U kunt verscheidene ingebouwde functies van SQL van de Vonk gebruiken om SQL functionaliteit met de Dienst van de Vraag van Adobe Experience Platform uit te breiden. Dit document maakt een lijst van de SQL functies van de Vonk die door de Dienst van de Vraag worden gesteund.

Voor meer gedetailleerde informatie over de functies, met inbegrip van hun syntaxis, gebruik, en voorbeelden, lees de [ SQL van de Vonk functiedocumentatie ](https://spark.apache.org/docs/latest/api/sql/index.html).

>[!NOTE]
>
>Niet alle functies in de externe documentatie worden ondersteund.

## Math- en statistische operatoren en functies {#math}

| Operator/functie | Beschrijving |
| ----------------- | ----------- |
| [`%`](https://spark.apache.org/docs/latest/api/sql/index.html#_3) | Retourneert de rest van de twee getallen |
| [`*`](https://spark.apache.org/docs/latest/api/sql/index.html#_5) | Vermenigvuldigt de twee getallen |
| [`+`](https://spark.apache.org/docs/latest/api/sql/index.html#_6) | Hiermee worden de twee getallen toegevoegd |
| [`-`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | Trekt de twee getallen af |
| [`/`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Hiermee worden de twee getallen gedeeld |
| [`abs`](https://spark.apache.org/docs/latest/api/sql/index.html#abs) | Retourneert de absolute waarde van de invoer |
| [`acos`](https://spark.apache.org/docs/latest/api/sql/index.html#acos) | Retourneert de omgekeerde cosinuswaarde |
| [`approx_count_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_count_distinct) | Hiermee wordt de geschatte kardinaliteit door HyperLog++ geretourneerd |
| [`approx_percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_percentile) | Geeft als resultaat de ongeveer percentiele waarde bij het opgegeven percentage |
| [`asin`](https://spark.apache.org/docs/latest/api/sql/index.html#asin) | Retourneert de omgekeerde sinuswaarde |
| [`atan`](https://spark.apache.org/docs/latest/api/sql/index.html#atan) | Hiermee wordt de waarde van de omgekeerde raaklijn geretourneerd |
| [`atan2`](https://spark.apache.org/docs/latest/api/sql/index.html#atan2) | Hiermee wordt de hoek geretourneerd tussen het positieve x-asvlak en de punten die door de coördinaten worden aangegeven |
| [`avg`](https://spark.apache.org/docs/latest/api/sql/index.html#avg) | Retourneert de gemiddelde waarde |
| [`cbrt`](https://spark.apache.org/docs/latest/api/sql/index.html#cbrt) | Hiermee wordt de hoofdkubus geretourneerd |
| [`ceil` ](https://spark.apache.org/docs/latest/api/sql/index.html#ceil) of [`ceiling` ](https://spark.apache.org/docs/latest/api/sql/index.html#ceiling) | Retourneert het kleinste gehele getal dat niet groter is dan de ingevoerde waarde |
| [`conv`](https://spark.apache.org/docs/latest/api/sql/index.html#conv) | Omzetten van basis naar basis |
| [`corr`](https://spark.apache.org/docs/latest/api/sql/index.html#corr) | Retourneert de Pearson-coëfficiënt tussen de getallen |
| [`cos`](https://spark.apache.org/docs/latest/api/sql/index.html#cos) | Retourneert de cosinuswaarde |
| [`cosh`](https://spark.apache.org/docs/latest/api/sql/index.html#cosh) | Hiermee wordt de waarde van de hyperbolische cosinus geretourneerd |
| [`cot`](https://spark.apache.org/docs/latest/api/sql/index.html#cot) | Retourneert de inhoudswaarde |
| [`dense_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#dense_rank) | Retourneert de rang van een waarde in een groep waarden |
| [`e`](https://spark.apache.org/docs/latest/api/sql/index.html#e) | Retourneert het nummer van Euler |
| [`exp`](https://spark.apache.org/docs/latest/api/sql/index.html#exp) | Retourneert e tot de macht van de waarde |
| [`expm1`](https://spark.apache.org/docs/latest/api/sql/index.html#expm1) | Retourneert e tot de macht van de waarde minus 1 |
| [`factorial`](https://spark.apache.org/docs/latest/api/sql/index.html#factorial) | Retourneert de factorial van de waarde |
| [`floor`](https://spark.apache.org/docs/latest/api/sql/index.html#floor) | Retourneert het grootste gehele getal dat niet kleiner is dan de waarde |
| [`greatest`](https://spark.apache.org/docs/latest/api/sql/index.html#greatest) | Retourneert de hoogste waarde van alle parameters |
| [`hypot`](https://spark.apache.org/docs/latest/api/sql/index.html#hypot) | Geeft als resultaat de hypotensie van de twee gegeven waarden. |
| [`kurtosis`](https://spark.apache.org/docs/latest/api/sql/index.html#kurtosis) | Hiermee wordt de kurtosewaarde van de groep geretourneerd |
| [`least`](https://spark.apache.org/docs/latest/api/sql/index.html#least) | Retourneert de laagste waarde van alle parameters |
| [`ln`](https://spark.apache.org/docs/latest/api/sql/index.html#ln) | Retourneert de natuurlijke logaritme van de waarde |
| [`log`](https://spark.apache.org/docs/latest/api/sql/index.html#log) | Retourneert de logaritme van de waarde |
| [`log10`](https://spark.apache.org/docs/latest/api/sql/index.html#log10) | Retourneert de logaritme, in basis 10, van de waarde |
| [`log1p`](https://spark.apache.org/docs/latest/api/sql/index.html#log1p) | Retourneert de logaritme van de waarde plus 1 |
| [`log2`](https://spark.apache.org/docs/latest/api/sql/index.html#log2) | Retourneert de logaritme, in basis 2, van de waarde |
| [`max`](https://spark.apache.org/docs/latest/api/sql/index.html#max) | Retourneert de maximumwaarde van de expressie |
| [`mean`](https://spark.apache.org/docs/latest/api/sql/index.html#mean) | Hiermee wordt het gemiddelde geretourneerd dat met de waarden is berekend |
| [`min`](https://spark.apache.org/docs/latest/api/sql/index.html#min) | Hiermee wordt de minimumwaarde van de expressie geretourneerd |
| [`monotonically_increasing_id`](https://spark.apache.org/docs/latest/api/sql/index.html#monotonically_increasing_id) | Retourneert monotonisch verhogende id&#39;s |
| [`negative`](https://spark.apache.org/docs/latest/api/sql/index.html#negative) | Retourneert de genegeerde waarde |
| [`percent_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#percent_rank) | Hiermee wordt de percentagepositie van een waarde geretourneerd |
| [`percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile) | Hiermee wordt het exacte percentiel als een bepaald percentage geretourneerd |
| [`percentile_approx`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile_approx) | Geeft als resultaat het benaderende percentiel bij een bepaald percentage |
| [`pi`](https://spark.apache.org/docs/latest/api/sql/index.html#pi) | Retourneert pi |
| [`pmod`](https://spark.apache.org/docs/latest/api/sql/index.html#pmod) | Retourneert de positieve modulo tussen twee waarden |
| [`positive`](https://spark.apache.org/docs/latest/api/sql/index.html#positive) | Retourneert de positieve waarde |
| [`pow` ](https://spark.apache.org/docs/latest/api/sql/index.html#pow), [`power` ](https://spark.apache.org/docs/latest/api/sql/index.html#power) | Retourneert de eerste waarde tot de macht van de tweede waarde |
| [`radians`](https://spark.apache.org/docs/latest/api/sql/index.html#radians) | Zet de waarde om in radialen |
| [`rand`](https://spark.apache.org/docs/latest/api/sql/index.html#rand) | Retourneert een willekeurig getal tussen 0 en 1 |
| [`randn`](https://spark.apache.org/docs/latest/api/sql/index.html#randn) | Retourneert een willekeurige waarde |
| [`rint`](https://spark.apache.org/docs/latest/api/sql/index.html#rint) | Hiermee wordt de dichtstbijzijnde dubbele waarde geretourneerd |
| [`round`](https://spark.apache.org/docs/latest/api/sql/index.html#round) | Retourneert de dichtstbijzijnde afgeronde waarde |
| [`sign` ](https://spark.apache.org/docs/latest/api/sql/index.html#sign), [`signum` ](https://spark.apache.org/docs/latest/api/sql/index.html#signum) | Retourneert het numerieke teken |
| [`sin`](https://spark.apache.org/docs/latest/api/sql/index.html#sin) | Retourneert sinus van de waarde |
| [`sinh`](https://spark.apache.org/docs/latest/api/sql/index.html#sinh) | Retourneert een hyperbolische sinus van de waarde |
| [`sqrt`](https://spark.apache.org/docs/latest/api/sql/index.html#sqrt) | Retourneert de vierkantswortel van de waarde |
| [`stddev`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev) | Retourneert de standaardafwijking van de waarde |
| [`sttdev_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#sttdev_pop) | Retourneert de standaardafwijking van de waarde voor de populatie |
| [`stddev_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev_samp) | Retourneert de standaardafwijking van de waarde in het voorbeeld |
| [`sum`](https://spark.apache.org/docs/latest/api/sql/index.html#sum) | Retourneert de som van de waarden |
| [`tan`](https://spark.apache.org/docs/latest/api/sql/index.html#tan) | Retourneert tangens van de waarde |
| [`tanh`](https://spark.apache.org/docs/latest/api/sql/index.html#tanh) | Hiermee wordt de hyperbolische tangens van de waarde geretourneerd |
| [`var_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#var_pop) | Retourneert de berekende bevolkingsvariatie |
| [`var_samp` ](https://spark.apache.org/docs/latest/api/sql/index.html#var_samp), [`variance` ](https://spark.apache.org/docs/latest/api/sql/index.html#variance) | Retourneert de berekende samplevariatie |

### Logische operatoren en functies {#logical-operators}

| Operator/functie | Beschrijving |
| ----------------- | ----------- |
| [`!` ](https://spark.apache.org/docs/latest/api/sql/index.html#_1) of [`not` ](https://spark.apache.org/docs/latest/api/sql/index.html#not) | Logisch niet |
| [`<`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Minder dan |
| [`<=`](https://spark.apache.org/docs/latest/api/sql/index.html#_9) | Kleiner dan of gelijk aan |
| [`=`](https://spark.apache.org/docs/latest/api/sql/index.html#_12) | Gelijk aan |
| [`>`](https://spark.apache.org/docs/latest/api/sql/index.html#_14) | Groter dan |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_15) | Groter dan of gelijk aan |
| [`^`](https://spark.apache.org/docs/latest/api/sql/index.html#_16) | Bitsgewijs exclusief of |
| [`\|`](https://spark.apache.org/docs/latest/api/sql/index.html#_17) | Bitsgewijs of |
| [`~`](https://spark.apache.org/docs/latest/api/sql/index.html#_19) | Bitsgewijs niet |
| [`arrays_overlap`](https://spark.apache.org/docs/latest/api/sql/index.html#arrays_overlap) | Hiermee worden de algemene elementen geretourneerd |
| [`assert_true`](https://spark.apache.org/docs/latest/api/sql/index.html#assert_true) | Hiermee wordt bevestigd of de expressie waar is |
| [`if`](https://spark.apache.org/docs/latest/api/sql/index.html#if) | Als de expressie true oplevert, retourneert u de tweede expressie. Anders, keer de derde uitdrukking terug. |
| [`ifnull`](https://spark.apache.org/docs/latest/api/sql/index.html#ifnull) | Als de expressie null is, wordt de tweede expressie geretourneerd. Anders wordt de eerste expressie geretourneerd. |
| [`in`](https://spark.apache.org/docs/latest/api/sql/index.html#in) | Retourneert true als de eerste expressie zich in een van de volgende expressies bevindt. |
| [`isnan`](https://spark.apache.org/docs/latest/api/sql/index.html#isnan) | Retourneert true als de waarde geen getal is |
| [`isnotnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnotnull) | Retourneert true als de waarde niet null is. |
| [`isnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnull) | Retourneert true als de waarde null is |
| [`nanvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nanvl) | Retourneert de eerste expressie als dit geen getal is, anders de tweede expressie. |
| [`or`](https://spark.apache.org/docs/latest/api/sql/index.html#or) | Logisch of |
| [`when`](https://spark.apache.org/docs/latest/api/sql/index.html#when) | Wanneer kan worden gebruikt om takvoorwaarden voor vergelijking tot stand te brengen |
| [`xpath_boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_boolean) | Retourneert true als de XPath-expressie true oplevert of als een overeenkomend knooppunt wordt gevonden |

### Datum-/tijdfuncties {#datetime-functions}

| Functie | Beschrijving |
| -------- | ----------- |
| [`add_months`](https://spark.apache.org/docs/latest/api/sql/index.html#add_months) | Maanden op datum toevoegen |
| [`date_add`](https://spark.apache.org/docs/latest/api/sql/index.html#date_add) | Aantal dagen toevoegen aan datum |
| [`date_format`](https://spark.apache.org/docs/latest/api/sql/index.html#date_format) | Datumnotatie wijzigen |
| [`date_sub`](https://spark.apache.org/docs/latest/api/sql/index.html#date_sub) | Aantal dagen uit datum verwijderen |
| [`date_trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#date_trunc) | Retourneert de afgebroken datum naar de opgegeven eenheid |
| [`datediff`](https://spark.apache.org/docs/latest/api/sql/index.html#datediff) | Hiermee wordt het verschil tussen datums in dagen geretourneerd |
| [`day` ](https://spark.apache.org/docs/latest/api/sql/index.html#day), [`dayofmonth` ](https://spark.apache.org/docs/latest/api/sql/index.html#dayofmonth) | Retourneert de dag van de maand |
| [`dayofweek`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofweek) | Retourneert de dag van de week (1-7) |
| [`dayofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofyear) | Retourneert de dag van het jaar |
| [`from_unixtime`](https://spark.apache.org/docs/latest/api/sql/index.html#from_unixtime) | Retourneert de datum in UNIX®-tijd |
| [`from_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#from_utc_timestamp) | Retourneert de datum in UTC-tijd |
| [`hour`](https://spark.apache.org/docs/latest/api/sql/index.html#hour) | Retourneert het uur van de invoer |
| [`last_day`](https://spark.apache.org/docs/latest/api/sql/index.html#last_day) | Retourneert de laatste dag van de maand waartoe de datum behoort |
| [`minute`](https://spark.apache.org/docs/latest/api/sql/index.html#minute) | Retourneert de minuut van de invoer |
| [`month`](https://spark.apache.org/docs/latest/api/sql/index.html#month) | Retourneert de maand van de invoer |
| [`months_between`](https://spark.apache.org/docs/latest/api/sql/index.html#months_between) | Aantal maanden tussen |
| [`next_day`](https://spark.apache.org/docs/latest/api/sql/index.html#next_day) | Retourneert de eerste dag na de invoer |
| [`quarter`](https://spark.apache.org/docs/latest/api/sql/index.html#quarter) | Retourneert het kwartaal van de invoer |
| [`second`](https://spark.apache.org/docs/latest/api/sql/index.html#second) | Retourneert de tweede tekenreeks |
| [`to_date`](https://spark.apache.org/docs/latest/api/sql/index.html#to_date) | Zet de tekenreeks om in een datum. **Nota:** het koord **moet** in het formaat `yyyy-mm-ddTHH24:MM:SS` zijn. |
| [`to_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_timestamp) | Zet de tekenreeks om in een tijdstempel. **Nota:** het koord **moet** in het formaat `yyyy-mm-ddTHH24:MM:SS` zijn. |
| [`to_unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_unix_timestamp) | Zet de tekenreeks om in een UNIX®-tijdstempel |
| [`to_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_utc_timestamp) | Zet de tekenreeks om in een UTC-tijdstempel |
| [`trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#trunc) | Kort de datum in |
| [`unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#unix_timestamp) | Retourneert de UNIX®-tijdstempel |
| [`weekday`](https://spark.apache.org/docs/latest/api/sql/index.html#weekday) | Dag van de week (0-6) |
| [`weekofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#weekofyear) | Geeft als resultaat de week van het jaar voor een bepaalde datum |
| [`year`](https://spark.apache.org/docs/latest/api/sql/index.html#year) | Retourneert het jaar van de tekenreeks |

### Arrays {#arrays}

| Functie | Beschrijving |
| -------- | ----------- |
| [`array`](https://spark.apache.org/docs/latest/api/sql/index.html#array) | Maakt een array met de opgegeven elementen |
| [`array_contains`](https://spark.apache.org/docs/latest/api/sql/index.html#array_contains) | Controleert of de array de waarde bevat |
| [`array_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#array_distinct) | Hiermee worden dubbele waarden uit de array verwijderd |
| [`array_except`](https://spark.apache.org/docs/latest/api/sql/index.html#array_except) | Retourneert een array van de elementen in de eerste array, maar niet de tweede |
| [`array_intersect`](https://spark.apache.org/docs/latest/api/sql/index.html#array_intersect) | Hiermee wordt de doorsnede van de twee arrays geretourneerd |
| [`array_join`](https://spark.apache.org/docs/latest/api/sql/index.html#array_join) | Voegt twee arrays samen |
| [`array_max`](https://spark.apache.org/docs/latest/api/sql/index.html#array_max) | Retourneert de maximumwaarde van de array |
| [`array_min`](https://spark.apache.org/docs/latest/api/sql/index.html#array_min) | Retourneert de minimumwaarde van de array |
| [`array_position`](https://spark.apache.org/docs/latest/api/sql/index.html#array_position) | Retourneert de op 1 gebaseerde positie van het element |
| [`array_remove`](https://spark.apache.org/docs/latest/api/sql/index.html#array_remove) | Hiermee worden alle elementen verwijderd die gelijk zijn aan het element |
| [`array_repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#array_repeat) | Hiermee wordt een array gemaakt die de geteld waardetijden bevat |
| [`array_sort`](https://spark.apache.org/docs/latest/api/sql/index.html#array_sort) | Sorteert de array |
| [`array_union`](https://spark.apache.org/docs/latest/api/sql/index.html#array_union) | Hiermee wordt de array samengevoegd, zonder duplicaten |
| [`arrays_zip`](https://spark.apache.org/docs/latest/api/sql/index.html#array_zip) | Hiermee worden de waarden van een bepaalde array gecombineerd met de waarden van de oorspronkelijke verzameling op een opgegeven index |
| [`cardinality`](https://spark.apache.org/docs/latest/api/sql/index.html#cardinality) | Hiermee wordt de grootte van de array geretourneerd |
| [`element_at`](https://spark.apache.org/docs/latest/api/sql/index.html#element_at) | Het element op de positie retourneren |
| [`explode`](https://spark.apache.org/docs/latest/api/sql/index.html#explode) | Afzonderlijke elementen van een array in meerdere rijen, met uitzondering van null |
| [`explode_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#explode_outer) | Afzonderlijke elementen van een array in meerdere rijen, inclusief null |
| [`find_in_set`](https://spark.apache.org/docs/latest/api/sql/index.html#find_in_set) | Retourneert de op 1 gebaseerde positie van de array |
| [`flatten`](https://spark.apache.org/docs/latest/api/sql/index.html#flatten) | Hiermee wordt een array van arrays afgevlakt |
| [`inline`](https://spark.apache.org/docs/latest/api/sql/index.html#inline) | Afzonderlijke array van structs in een tabel, met uitzondering van null |
| [`inline_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#inline_outer) | Afzonderlijke array van structs in een tabel, inclusief null |
| [`posexplode`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplode) | Afzonderlijke elementen van een array in meerdere rijen met posities, met uitzondering van null |
| [`reverse`](https://spark.apache.org/docs/latest/api/sql/index.html#reverse) | Elementen in de array omkeren |
| [`shuffle`](https://spark.apache.org/docs/latest/api/sql/index.html#shuffle) | Hiermee wordt een willekeurige permutatie van de array geretourneerd |
| [`slice`](https://spark.apache.org/docs/latest/api/sql/index.html#slice) | Hiermee wordt een array gesubsets |
| [`sort_array`](https://spark.apache.org/docs/latest/api/sql/index.html#sort_array) | Een array sorteren op basis van een volgorde |
| [`zip_with`](https://spark.apache.org/docs/latest/api/sql/index.html#zip_with) | Voegt de twee arrays samen tot één array voordat een functie wordt toegepast |

### Datatype casting-functies {#datatype-casting}

| Functie | Beschrijving |
| -------- | ----------- |
| [`bigint`](https://spark.apache.org/docs/latest/api/sql/index.html#bigint) | Het gegevenstype wijzigen in bigint |
| [`binary`](https://spark.apache.org/docs/latest/api/sql/index.html#binary) | Het gegevenstype wijzigen in binair |
| [`boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#boolean) | Het gegevenstype wijzigen in Boolean |
| [`type`](https://spark.apache.org/docs/latest/api/sql/index.html#type) | Het gegevenstype wijzigen in het opgegeven type |
| [`date`](https://spark.apache.org/docs/latest/api/sql/index.html#date) | Het gegevenstype wijzigen in date |
| [`decimal`](https://spark.apache.org/docs/latest/api/sql/index.html#decimal) | Het gegevenstype wijzigen in decimaal |
| [`double`](https://spark.apache.org/docs/latest/api/sql/index.html#double) | Het gegevenstype wijzigen in dubbel |
| [`float`](https://spark.apache.org/docs/latest/api/sql/index.html#float) | Het gegevenstype wijzigen in zwevend |
| [`int`](https://spark.apache.org/docs/latest/api/sql/index.html#int) | Het gegevenstype wijzigen in int |
| [`smallint`](https://spark.apache.org/docs/latest/api/sql/index.html#smallint) | Het gegevenstype wijzigen in kleinint |
| [`str_to_map`](https://spark.apache.org/docs/latest/api/sql/index.html#str_to_map) | Een kaart maken van een tekenreeks |
| [`string`](https://spark.apache.org/docs/latest/api/sql/index.html#string) | Het gegevenstype wijzigen in een tekenreeks |
| [`struct`](https://spark.apache.org/docs/latest/api/sql/index.html#struct) | Een structuur maken |
| [`tinyint`](https://spark.apache.org/docs/latest/api/sql/index.html#tinyint) | Het gegevenstype wijzigen in tinten |

### Conversie- en opmaakfuncties {#conversion}

| Functie | Beschrijving |
| -------- | ----------- |
| [`ascii`](https://spark.apache.org/docs/latest/api/sql/index.html#ascii) | Hiermee wordt de numerieke waarde (ASCII) geretourneerd |
| [`base64`](https://spark.apache.org/docs/latest/api/sql/index.html#base64) | Het argument wijzigen in een base64-tekenreeks |
| [`bin`](https://spark.apache.org/docs/latest/api/sql/index.html#bin) | Het argument wijzigen in een binaire waarde |
| [`bit_length`](https://spark.apache.org/docs/latest/api/sql/index.html#bit_length) | De bitlengte retourneren |
| [`char` ](https://spark.apache.org/docs/latest/api/sql/index.html#char), [`chr` ](https://spark.apache.org/docs/latest/api/sql/index.html#chr) | Het ASCII-teken retourneren |
| [`char_length` ](https://spark.apache.org/docs/latest/api/sql/index.html#char_length), [`character_length` ](https://spark.apache.org/docs/latest/api/sql/index.html#character_length) | Hiermee wordt de tekenreekslengte geretourneerd |
| [`crc32`](https://spark.apache.org/docs/latest/api/sql/index.html#crc32) | Hiermee wordt de controlewaarde voor cyclische redundantie geretourneerd |
| [`degrees`](https://spark.apache.org/docs/latest/api/sql/index.html#degrees) | Radialen omzetten in graden |
| [`format_number`](https://spark.apache.org/docs/latest/api/sql/index.html#format_number) | De getalnotatie wijzigen |
| [`from_json` ](https://spark.apache.org/docs/latest/api/sql/index.html#from_json), [`get_json_object` ](https://spark.apache.org/docs/latest/api/sql/index.html#get_json_object) | Gegevens ophalen van JSON |
| [`hash`](https://spark.apache.org/docs/latest/api/sql/index.html#hash) | De hashwaarde retourneren |
| [`hex`](https://spark.apache.org/docs/latest/api/sql/index.html#hex) | Zet het argument om in een hexadecimale waarde |
| [`initcap`](https://spark.apache.org/docs/latest/api/sql/index.html#initcap) | Hiermee wordt de tekenreeks gewijzigd in titelhoofdletter |
| [`lcase` ](https://spark.apache.org/docs/latest/api/sql/index.html#lcase), [`lower` ](https://spark.apache.org/docs/latest/api/sql/index.html#lower) | Hiermee wordt de tekenreeks gewijzigd in kleine letters |
| [`lpad`](https://spark.apache.org/docs/latest/api/sql/index.html#lpad) | Hiermee wordt de linkerzijde van een tekenreeks geplakt |
| [`map`](https://spark.apache.org/docs/latest/api/sql/index.html#map) | Een kaart maken |
| [`map_from_arrays`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_arrays) | Een kaart maken van een array |
| [`map_from_entries`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_entries) | Een kaart maken op basis van een array met constructies |
| [`md5`](https://spark.apache.org/docs/latest/api/sql/index.html#md5) | Hiermee wordt de md5-waarde geretourneerd |
| [`rpad`](https://spark.apache.org/docs/latest/api/sql/index.html#rpad) | Hiermee wordt de rechterzijde van een tekenreeks geplakte |
| [`rtrim`](https://spark.apache.org/docs/latest/api/sql/index.html#rtrim) | Hiermee verwijdert u volgspaties |
| [`sha` ](https://spark.apache.org/docs/latest/api/sql/index.html#sha), [`sha1` ](https://spark.apache.org/docs/latest/api/sql/index.html#sha1) | De SHA1-waarde retourneren |
| [`sha2`](https://spark.apache.org/docs/latest/api/sql/index.html#sha2) | De SHA2-waarde retourneren |
| [`soundex`](https://spark.apache.org/docs/latest/api/sql/index.html#soundex) | De soundex-code retourneren |
| [`stack`](https://spark.apache.org/docs/latest/api/sql/index.html#stack) | Waarden scheiden in rijen |
| [`substr` ](https://spark.apache.org/docs/latest/api/sql/index.html#substr), [`substring` ](https://spark.apache.org/docs/latest/api/sql/index.html#substring) | De subtekenreeks retourneren |
| [`to_json`](https://spark.apache.org/docs/latest/api/sql/index.html#to_json) | Retourneert een JSON-tekenreeks |
| [`translate`](https://spark.apache.org/docs/latest/api/sql/index.html#translate) | Waarden binnen tekenreeks vervangen |
| [`trim`](https://spark.apache.org/docs/latest/api/sql/index.html#trim) | Voorlooptekens en navolgende tekens verwijderen |
| [`ucase` ](https://spark.apache.org/docs/latest/api/sql/index.html#ucase), [`upper` ](https://spark.apache.org/docs/latest/api/sql/index.html#upper) | De tekenreeks wijzigen in hoofdletters |
| [`unbase64`](https://spark.apache.org/docs/latest/api/sql/index.html#unbase64) | Zet de base64-tekenreeks om in binair getal |
| [`unhex`](https://spark.apache.org/docs/latest/api/sql/index.html#unhex) | Hexadecimaal converteren naar binair |
| [`uuid`](https://spark.apache.org/docs/latest/api/sql/index.html#uuid) | UUID retourneren |

### Gegevensevaluatie {#data-evaluation}

| Functie | Beschrijving |
| -------- | ----------- |
| [`coalesce`](https://spark.apache.org/docs/latest/api/sql/index.html#coalesce) | Retourneer het eerste argument dat niet gelijk is aan null |
| [`collect_list`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_list) | Een lijst met niet-unieke elementen retourneren |
| [`collect_set`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_set) | Een set unieke elementen retourneren |
| [`concat`](https://spark.apache.org/docs/latest/api/sql/index.html#concat) | Samenvoegen |
| [`concat_ws`](https://spark.apache.org/docs/latest/api/sql/index.html#concat_ws) | Samenvoegen met scheidingsteken |
| [`count`](https://spark.apache.org/docs/latest/api/sql/index.html#count) | Hiermee wordt het totale aantal rijen geretourneerd |
| [`decode`](https://spark.apache.org/docs/latest/api/sql/index.html#decode) | Decoderen met een tekenset |
| [`elt`](https://spark.apache.org/docs/latest/api/sql/index.html#elt) | Terugkeer [`n` ](https://spark.apache.org/docs/latest/api/sql/index.html#n) de input |
| [`encode`](https://spark.apache.org/docs/latest/api/sql/index.html#encode) | Coderen met een tekenset |
| [`first` ](https://spark.apache.org/docs/latest/api/sql/index.html#first), [`first_value` ](https://spark.apache.org/docs/latest/api/sql/index.html#first_value) | Retourneert de eerste waarde |
| [`grouping`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping) | Hiermee wordt aangegeven of een kolom is gegroepeerd |
| [`grouping_id`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping_id) | Retourneert het niveau van groepering |
| [`instr`](https://spark.apache.org/docs/latest/api/sql/index.html#instr) | Retourneert een op 1 gebaseerde index van het voorkomen van tekens |
| [`json_tuple`](https://spark.apache.org/docs/latest/api/sql/index.html#json_tuple) | Retourneert een tuple van een JSON-invoer |
| [`lag` ](https://spark.apache.org/docs/latest/api/sql/index.html#lag), [`lead` ](https://spark.apache.org/docs/latest/api/sql/index.html#lead) | Hiermee wordt de waarde vóór de verschuiving geretourneerd |
| [`last` ](https://spark.apache.org/docs/latest/api/sql/index.html#last), [`last_value` ](https://spark.apache.org/docs/latest/api/sql/index.html#last_value) | Retourneert de laatste waarde |
| [`left`](https://spark.apache.org/docs/latest/api/sql/index.html#left) | Retourneert de eerste [`n` ](https://spark.apache.org/docs/latest/api/sql/index.html#n) -tekens |
| [`length`](https://spark.apache.org/docs/latest/api/sql/index.html#length) | Retourneert de lengte van de tekenreeks |
| [`levenshtein`](https://spark.apache.org/docs/latest/api/sql/index.html#levenshtein) | Retourneert de Levenshtein-afstand tussen tekenreeksen |
| [`locate` ](https://spark.apache.org/docs/latest/api/sql/index.html#locate), [`position` ](https://spark.apache.org/docs/latest/api/sql/index.html#position) | Retourneert de positie van de eerste instantie van een subtekenreeks |
| [`map_concat`](https://spark.apache.org/docs/latest/api/sql/index.html#map_concat) | Een kaart samenvoegen |
| [`map_keys`](https://spark.apache.org/docs/latest/api/sql/index.html#map_keys) | Kaarttoetsen retourneren |
| [`map_values`](https://spark.apache.org/docs/latest/api/sql/index.html#map_values) | De waarden van een kaart retourneren |
| [`ntile`](https://spark.apache.org/docs/latest/api/sql/index.html#ntile) | Rijen splitsen in partities |
| [`nullif`](https://spark.apache.org/docs/latest/api/sql/index.html#nullif) | Retourneert null indien true |
| [`nvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl) | Retourneert waarde indien null |
| [`nvl2`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl2) | Retourneert waarde indien niet null |
| [`parse_url`](https://spark.apache.org/docs/latest/api/sql/index.html#parse_url) | Hiermee wordt een deel van een URL opgehaald |
| [`rank`](https://spark.apache.org/docs/latest/api/sql/index.html#rank) | Berekent de positie van een waarde |
| [`regexp_extract`](https://spark.apache.org/docs/latest/api/sql/index.html#regexp_extract) | Extraheert iets dat overeenkomt met regex |
| [`regex_replace`](https://spark.apache.org/docs/latest/api/sql/index.html#regex_replace) | Hiermee vervangt u iets dat overeenkomt met de regex |
| [`repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#repeat) | Retourneert een tekenreeks die wordt herhaald |
| [`replace`](https://spark.apache.org/docs/latest/api/sql/index.html#replace) | Alle instanties van een tekenreeks vervangen |
| [`rollup`](https://spark.apache.org/docs/latest/api/sql/index.html#rollup) | Een multidimensionale rollup maken |
| [`row_number`](https://spark.apache.org/docs/latest/api/sql/index.html#row_number) | Hiermee wijst u een uniek rijnummer toe |
| [`schema_of_json`](https://spark.apache.org/docs/latest/api/sql/index.html#schema_of_json) | Retourneert het schema van de JSON |
| [`sentences`](https://spark.apache.org/docs/latest/api/sql/index.html#sentences) | Hiermee wordt een tekenreeks opgedeeld in een array van woorden |
| [`sequence`](https://spark.apache.org/docs/latest/api/sql/index.html#sequence) | Genereert een array met elementen |
| [`shiftleft`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftleft) | Bitsgewijs naar links ondertekend |
| [`shiftright`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftright) | Bitsgewijs naar rechts verplaatsen ondertekend |
| [`shiftrightunsigned`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftrightunsigned) | Bitsgewijs zonder teken naar rechts verplaatsen |
| [`size`](https://spark.apache.org/docs/latest/api/sql/index.html#size) | Hiermee wordt de grootte van de array geretourneerd |
| [`space`](https://spark.apache.org/docs/latest/api/sql/index.html#space) | Een tekenreeks met [`n` ](https://spark.apache.org/docs/latest/api/sql/index.html#n) spaties retourneren |
| [`split`](https://spark.apache.org/docs/latest/api/sql/index.html#split) | Gesplitste tekenreeks |
| [`substring_index`](https://spark.apache.org/docs/latest/api/sql/index.html#substring_index) | Retourindex van subtekenreeks |
| [`window`](https://spark.apache.org/docs/latest/api/sql/index.html#window) | Venster |
| [`xpath`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath) | XML-knooppunten parseren |
| [`xpath_double` ](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_double), [`xpath_number` ](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_number) | XML-knooppunten parseren voor dubbel |
| [`xpath_float`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_float) | XML-knooppunten parseren voor float |
| [`xpath_int`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_int) | XML-knooppunten parseren voor geheel getal |
| [`xpath_long`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_long) | XML-knooppunten lange parseren |
| [`xpath_short`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_short) | XML-knooppunten parseren voor kort geheel getal |
| [`xpath_string`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_string) | XML-knooppunten parseren voor tekenreeks |

### Huidige informatie {#current-information}

| Functie | Beschrijving |
| -------- | ----------- |
| [`current_database`](https://spark.apache.org/docs/latest/api/sql/index.html#current_database) | Hiermee wordt de huidige database geretourneerd |
| [`current_date`](https://spark.apache.org/docs/latest/api/sql/index.html#current_date) | Hiermee wordt de huidige datum geretourneerd |
| [`current_timestamp` ](https://spark.apache.org/docs/latest/api/sql/index.html#current_timestamp), [`now` ](https://spark.apache.org/docs/latest/api/sql/index.html#now) | Hiermee wordt de huidige tijdstempel geretourneerd |

### Functies met hogere volgorde {#higher-order}

| Functie | Beschrijving |
| -------- | ----------- |
| [`transform`](https://spark.apache.org/docs/latest/api/sql/index.html#transform) | Elementen transformeren in een array |
| [`exists`](https://spark.apache.org/docs/latest/api/sql/index.html#exists) | Controleren of element bestaat |
| [`filter`](https://spark.apache.org/docs/latest/api/sql/index.html#filter) | De invoerarray filteren |
| [`aggregate`](https://spark.apache.org/docs/latest/api/sql/index.html#aggregate) | Een binaire operator toepassen op alle elementen |
