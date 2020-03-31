---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: SQL-functies in Spark
topic: spark sql functions
translation-type: tm+mt
source-git-commit: a23ee02a9e801531a38b5ff70ef07497aa21b174

---


# SQL-functies in Spark

De SQL helpers van de Vonk verstrekken ingebouwde functies van de Vonk SQL om SQL functionaliteit uit te breiden.

Referentie: Documentatie over de SQL-functie [Spark](https://spark.apache.org/docs/2.4.0/api/sql/index.html)

>[!NOTE] Niet alle functies in de externe documentatie worden ondersteund.

## Categorieën

- [Math- en statistische operatoren en functies](#math-and-statistical-operators-and-functions)
- [Logische operatoren](#logical-operators)
- [Datum-/tijdfuncties](#date/time-functions)
- [Samengevoegde functies](#aggregate-functions)
- [Arrays](#arrays)
- [Datatype casting-functies](#datatype-casting-functions)
- [Conversie- en opmaakfuncties](#conversion-and-formatting-functions)
- [Gegevensevaluatie](#data-evaluation)
- [Huidige informatie](#current-information)

### Math- en statistische operatoren en functies

#### Modulo

`expr1 % expr2`: Retourneert de rest na `expr1`/`expr2`.

Voorbeelden:

```
> SELECT 2 % 1.8;
 0.2
> SELECT MOD(2, 1.8);
 0.2
```

#### Vermenigvuldigen

`expr1 * expr2`: Retourneert `expr1`*`expr2`.

Voorbeeld:

```
> SELECT 2 * 3;
 6
```

#### Toevoegen

`expr1 + expr2`: Retourneert `expr1`+`expr2`.

Voorbeeld:

```
> SELECT 1 + 2;
 3
```

#### Aftrekken

`expr1 - expr2`: Retourneert `expr1`-`expr2`.

Voorbeeld:

```
> SELECT 2 - 1;
 1
```

#### Verdelen

`expr1 / expr2`: Retourneert `expr1`/`expr2`. Er wordt altijd een drijvende-kommagedelen uitgevoerd.

Voorbeelden:

```
> SELECT 3 / 2;
 1.5
> SELECT 2L / 2L;
 1.0
```

#### abs

`abs(expr)`: Retourneert de absolute waarde van de numerieke waarde.

Voorbeeld:

```
> SELECT abs(-1);
  1
```

#### acos

`acos(expr)`: Geeft de omgekeerde cosinus (ook bekend als arcosinus) van `expr`, alsof berekend door `java.lang.Math.acos`.

Voorbeelden:

```
> SELECT acos(1);
 0.0
> SELECT acos(2);
 NaN
```

#### circa_percentiel

`approx_percentile(col, percentage [, accuracy])`: Geeft als resultaat de ongeveer percentiele waarde van de numerieke kolom `col` met het opgegeven percentage. De waarde van het percentage moet liggen tussen 0,0 en 1,0. De `accuracy` parameter (standaardwaarde): 10000) is een positief letterlijk getal dat de nauwkeurigheid bij benadering bepaalt ten koste van het geheugen. Hoe hoger de waarde van `accuracy` retourneert, hoe nauwkeuriger `1.0/accuracy` de benadering, hoe onjuist deze is. Wanneer `percentage` een array is, moet elke waarde van de array met percentages tussen 0,0 en 1,0 liggen. In dit geval wordt de ongeveer percentiele array van de kolom `col` bij de opgegeven percentagearray geretourneerd.

Voorbeelden:

```
> SELECT approx_percentile(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT approx_percentile(10.0, 0.5, 100);
 10.0
```

#### asin

`asin(expr)`: Geeft de inverse sinus (ook bekend als arcosinus), de arcosinus van `expr`, alsof berekend door `java.lang.Math.asin`.

Voorbeelden:

```
> SELECT asin(0);
 0.0
> SELECT asin(2);
 NaN
```

#### atan

`atan(expr)`: Retourneert de inverse tangens (ook wel arc tangent genoemd) van `expr`, alsof deze berekend zijn door `java.lang.Math.atan`

Voorbeeld:

```
> SELECT atan(0);
 0.0
```

#### atan2

`atan2(exprY, exprX)`: Geeft als resultaat de hoek in radialen tussen de positieve x-as van een vlak en het punt opgegeven door de coördinaten (`exprX`, `exprY`), alsof deze berekend zijn door `java.lang.Math.atan2`.

Argumenten:

`exprY`: Coördinaat op y-as`exprX`: Coördinaat op x-as

Voorbeeld:

```
> SELECT atan2(0, 0);
 0.0
```

#### avg

`avg(expr)`: Retourneert het gemiddelde dat is berekend op basis van waarden van een groep.

#### kardinaal

`cardinality(expr)`: Retourneert de grootte van een array of een kaart. De functie retourneert -1 als de invoer ervan null is en op true `spark.sql.legacy.sizeOfNull` is ingesteld (standaardwaarde). Als deze waarde op false `spark.sql.legacy.sizeOfNull` is ingesteld, retourneert de functie null voor null-invoer.

Voorbeelden:

```
> SELECT cardinality(array('b', 'd', 'c', 'a'));
 4
> SELECT cardinality(map('a', 1, 'b', 2));
 2
> SELECT cardinality(NULL);
 -1
```

#### cbrt

`cbrt(expr)`: Retourneert de kuburoot van `expr`.

Voorbeeld:

```
> Select cbrt(27.0);
 3.0
```

#### ceil

`ceil(expr)`: Retourneert het kleinste gehele getal dat niet kleiner is dan `expr`.

Voorbeelden:

```
> SELECT ceil(-0.1);
 0
> SELECT ceil(5);
 5
```

#### maximum

`ceiling(expr)`: Retourneert het kleinste gehele getal dat niet kleiner is dan `expr`.

Voorbeelden:

```
> SELECT ceiling(-0.1);
 0
> SELECT ceiling(5);
 5
```

#### conv

`conv(num, from_base, to_base)`: Omzetten `num` van `from_base` in `to_base`

Voorbeelden:

```
> SELECT conv('100', 2, 10);
 4
> SELECT conv(-10, 16, -10);
 -16
```

#### corr

`corr(expr1, expr2)`: Retourneert de Pearson-correlatiecoëfficiënt tussen een set getalparen.

#### cos

`cos(expr)`: Retourneert de cosinus van `expr`, alsof berekend door `java.lang.Math.cos`.

Voorbeeld:

```
> SELECT cos(0);
 1.0
```

#### koel

`cosh(expr)`: Geeft de hyperbolische cosinus van `expr`, alsof berekend door `java.lang.Math.cosh`.

Argumenten:
- `expr`: Hyperbolische hoek

Voorbeeld:

```
> SELECT cosh(0);
 1.0
```

#### cot

`cot(expr)`: Retourneert de inhoud van `expr`, alsof deze is berekend door `1/java.lang.Math.cot`.

Argumenten:
- `expr`: Hoek in radialen

Voorbeeld:

```
> SELECT cot(1);
 0.6420926159343306
```

#### dense_rank

`dense_rank()`: Berekent de positie van een waarde in een groep waarden. Het resultaat is één plus de eerder toegewezen rangtelwaarde. In tegenstelling tot de functie `rank`, `dense_rank` veroorzaakt geen hiaten in het rangschikken opeenvolging.

#### e

`e()`: Retourneert het nummer van Euler, e.

Voorbeeld:

```
> SELECT e();
 2.718281828459045
```

#### exp

`exp(expr)`: Keert e terug tot de macht van `expr`.

Voorbeeld:

```
> SELECT exp(0);
 1.0
```

#### expml

`expm1(expr)`: Retourneert exp(`expr`) - 1.

Voorbeeld:

```
> SELECT expm1(0);
 0.0
```

#### faculteit

`factorial(expr)`: Geeft de factorial van `expr`. `expr` is [0..20]. Anders null.

Voorbeeld:

```
> SELECT factorial(5);
 120
```

#### verdieping

`floor(expr)`: Retourneert het grootste gehele getal dat niet groter is dan `expr`.

Voorbeelden:

```
> SELECT floor(-0.1);
 -1
> SELECT floor(5);
 5
```

#### grootste

`greatest(expr, ...)`: Retourneert de hoogste waarde van alle parameters, waarbij null-waarden worden overgeslagen.

Voorbeeld:

```
> SELECT greatest(10, 9, 2, 4, 3);
 10
```

#### hypothese

`hypot(expr1, expr2)`: Retourneert sqrt(`expr1`<sup>2</sup> + `expr2`<sup>2</sup>).

Voorbeeld:

```
> SELECT hypot(3, 4);
 5.0
```

#### kurtosis

`kurtosis(expr)`: Retourneert de kurtose-waarde die is berekend op basis van waarden van een groep.


#### minimaal

`least(expr, ...)`: Retourneert de laagste waarde van alle parameters, waarbij null-waarden worden overgeslagen.

Voorbeeld:

```
> SELECT least(10, 9, 2, 4, 3);
 2
```

#### elfshtein

`levenshtein(str1, str2)`: Geeft als resultaat de Levenshtein-afstand tussen de twee opgegeven tekenreeksen.

Voorbeelden:

```
> SELECT levenshtein('kitten', 'sitting');
 3
```

#### ln

`ln(expr)`: Retourneert de natuurlijke logaritme (basis e) van `expr`.

Voorbeeld:

```
> SELECT ln(1);
 0.0
```

#### log

`log(base, expr)`: Retourneert de logaritme van `expr` met `base`.

Voorbeeld:

```
> SELECT log(10, 100);
 2.0
```

#### log10

`log10(expr)`: Retourneert de logaritme van `expr` met basis 10.

Voorbeeld:

```
> SELECT log10(10);
 1.0
```

#### log1p

`log1p(expr)`: Retourneert `log(1 + expr)`.

Voorbeeld:

```
> SELECT log1p(0);
 0.0
```

#### log2

`log2(expr)`: Retourneert de logaritme van `expr` met basis 2.

Voorbeeld:

```
> SELECT log2(2);
 1.0
```

#### max

`max(expr)`: Retourneert de maximumwaarde van `expr`.

#### gemiddelde

`mean(expr)`: Retourneert het gemiddelde dat is berekend op basis van waarden van een groep.

#### min

`min(expr)`: Retourneert de minimumwaarde van `expr`.

#### monotonisch_oplopend_id

`monotonically_increasing_id()`: Geeft monotonisch toenemende 64-bits gehele getallen. De gegenereerde id wordt gegarandeerd monotonisch verhoogd en uniek, maar niet opeenvolgend. De huidige implementatie zet verdelingsidentiteitskaart in hogere 31 beetjes, en lagere 33 beetjes vertegenwoordigen het verslagaantal binnen elke verdeling. De veronderstelling is dat het gegevenskader minder dan 1 miljard verdelingen heeft, en elke verdeling heeft minder dan 8 miljard verslagen. De functie is niet deterministisch omdat het resultaat ervan afhankelijk is van partitie-id&#39;s.

#### negatief

`negative(expr)`: Retourneert de genegeerde waarde van `expr`.

Voorbeeld:

```
> SELECT negative(1);
 -1
```

#### percent_rank

`percent_rank()`: Berekent de percentagevolgorde van een waarde in een groep waarden.

#### percentiel

`percentile(col, percentage [, frequency])`: Geeft als resultaat de exacte percentagewaarde van de numerieke kolom `col` met het opgegeven percentage. De waarde van `percentage` moet tussen 0,0 en 1,0 liggen. De waarde van `frequency` moet positief zijn.

`percentile(col, array(percentage1 [, percentage2]...) [, frequency])`: Geeft als resultaat de exacte percentielwaardenarray van de numerieke kolom `col` met de opgegeven percentages. Elke waarde van de array met percentages moet tussen 0,0 en 1,0 liggen. De waarde van `frequency` moet positief zijn.

#### percentile_Approx

`percentile_approx(col, percentage [, accuracy])`: Geeft als resultaat de ongeveer percentiele waarde van de numerieke kolom `col` met het opgegeven percentage. De waarde van `percentage` moet tussen 0,0 en 1,0 liggen. De `accuracy` parameter (standaardwaarde): 10000) is een positief letterlijk getal dat de nauwkeurigheid bij benadering bepaalt ten koste van het geheugen. Hoe hoger de waarde van `accuracy` retourneert, hoe nauwkeuriger `1.0/accuracy` de benadering, hoe onjuist deze is. Wanneer `percentage` een array is, moet elke waarde van de array met percentages tussen 0,0 en 1,0 liggen. In dit geval wordt bij benadering de percentielarray van de kolom geretourneerd `col` bij de opgegeven array met percentages.

Voorbeelden:

```
> SELECT percentile_approx(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT percentile_approx(10.0, 0.5, 100);
 10.0
```

#### pi

`pi()`: Retourneert pi.

Voorbeeld:

```
> SELECT pi();
 3.141592653589793
```

#### pmod

`pmod(expr1, expr2)`: Retourneert de positieve waarde van `expr1` mod `expr2`.

Voorbeelden:

```
> SELECT pmod(10, 3);
 1
> SELECT pmod(-10, 3);
 2
```

#### positief

`positive(expr)`: Retourneert de positieve waarde van `expr`

#### pow

`pow(expr1, expr2)`: Verhoogt `expr1` de kracht van `expr2`.

Voorbeeld:

```
> SELECT pow(2, 3);
 8.0
```

#### macht

`power(expr1, expr2)`: Verhoogt `expr1` de kracht van `expr2`.

Voorbeelden:

```
> SELECT power(2, 3);
 8.0
```

#### radiaal

`radians(expr)`: Graden worden omgezet in radialen.

Argumenten:

- `expr`: Hoek in graden

Voorbeeld:

```
> SELECT radians(180);
 3.141592653589793
```

#### rand

`rand([seed])`: Retourneert een willekeurige waarde met onafhankelijke en identieke (i.i.d.) gelijkmatig verdeelde waarden in (0, 1).

Voorbeelden:

```
> SELECT rand();
 0.9629742951434543
> SELECT rand(0);
 0.8446490682263027
> SELECT rand(null);
 0.8446490682263027
```

>[!NOTE] Deze functie is in het algemeen niet deterministisch.

#### willekeurig

`randn([seed])`: Retourneert een willekeurige waarde met onafhankelijke en identiek verdeelde (i.i.d.) waarden die zijn ontleend aan de normale standaarddistributie.

Voorbeelden:

```
> SELECT randn();
 -0.3254147983080288
> SELECT randn(0);
 1.1164209726833079
> SELECT randn(null);
 1.1164209726833079
```

>[!NOTE] Deze functie is in het algemeen niet deterministisch.

#### afdruk

`rint(expr)`: Retourneert de dubbele waarde die het dichtst bij het argument ligt en gelijk is aan een wiskundig geheel getal.

Voorbeelden:

```
> SELECT rint(12.3456);
 12.0
```

#### rond

`round(expr, d)`: Retourneert `expr` afgerond tot op `d` decimalen met de afrondingsmodus HALF_UP.

Voorbeeld:

```
> SELECT round(2.5, 0);
 3.0
```

#### ondertekenen

`sign(expr)`: Retourneert -1,0, 0,0 of 1,0 als `expr` negatief, 0 of positief.

Voorbeeld:

```
> SELECT sign(40);
 1.0
```

#### signum

`signum(expr)`: Retourneert -1,0, 0,0 of 1,0 als negatief, 0 of positief. `expr`

Voorbeeld:

```
> SELECT signum(40);
 1.0
```

#### sin

`sin(expr)`: Retourneert de sinus van `expr`, alsof berekend door `java.lang.Math.sin`.

Argumenten:

- `expr`: Hoek in radialen

Voorbeeld:

```
> SELECT sin(0);
 0.0
```

#### sinh

`sinh(expr)`: Geeft hyperbolische sinus van `expr`, alsof berekend door `java.lang.Math.sinh`.

Argumenten:

- `expr`: Hyperbolische hoek

Voorbeeld:

```
> SELECT sinh(0);
 0.0
```

#### sqrt

`sqrt(expr)`: Retourneert de vierkantswortel van `expr`.

Voorbeeld:

```
> SELECT sqrt(4);
 2.0
```

#### stddev

`stddev(expr)`: Retourneert de standaardafwijking van het voorbeeld, berekend op basis van waarden van een groep.

#### stddev_pop

`sttdev_pop(expr)`: Retourneert de standaardafwijking van de populatie, berekend op basis van waarden van een groep.

#### stddev_samp

`stddev_samp(expr)`: Retourneert de standaardafwijking van het voorbeeld, berekend op basis van waarden van een groep.

#### som

`sum(expr)`: Retourneert de som die is berekend op basis van waarden van een groep.

#### tan

`tan(expr)`: Retourneert de tangens van `expr`, alsof deze berekend zijn door `java.lang.Math.tan`.

Argumenten:

- `expr`: Hoek in radialen

Voorbeeld:

```
> SELECT tan(0);
 0.0
```

#### tanker

`tanh(expr)`: Geeft de hyperbolische tangens van `expr`, alsof berekend door `java.lang.Math.tanh`.

Argumenten:

- `expr`: Hyperbolische hoek

Voorbeeld:

```
> SELECT tanh(0);
 0.0
```

#### Var_pop

`var_pop(expr)`: Geeft als resultaat de variantie van de populatie die is berekend op basis van waarden van een groep.

#### Var_samp

`var_samp(expr)`: Retourneert de samplevariantie die is berekend op basis van waarden van een groep.

#### variantie

`variance(expr)`: Retourneert de samplevariantie die is berekend op basis van waarden van een groep.

### Logische operatoren

#### Logisch niet

`! expr`: Logisch niet.

#### Minder dan

`expr1 < expr2`: Retourneert true als `expr1` minder is dan `expr2`.

Argumenten:

- `expr1, expr2`: De twee expressies moeten van hetzelfde type zijn of kunnen worden gecast naar een gemeenschappelijk type. Het moet een type zijn dat kan worden geordend. Bijvoorbeeld, is het kaarttype niet bestelbaar, zodat wordt het niet gesteund. Voor complexe typen zoals array/struct moeten de gegevenstypen van velden kunnen worden geordend.

Voorbeelden:

```
> SELECT 1 < 2;
 true
> SELECT 1.1 < '1';
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-08-01 04:17:52');
 true
> SELECT 1 < NULL;
 NULL
```

#### Kleiner dan of gelijk aan

`expr1 <= expr2`: Retourneert true als `expr1` kleiner dan of gelijk aan `expr2`.

Argumenten:

- `expr1, expr2`: De twee expressies moeten van hetzelfde type zijn of kunnen worden gecast naar een gemeenschappelijk type. Het moet een type zijn dat kan worden geordend. Bijvoorbeeld, is het kaarttype niet bestelbaar, zodat wordt het niet gesteund. Voor complexe typen zoals array/struct moeten de gegevenstypen van velden kunnen worden geordend.

Voorbeelden:

```
> SELECT 2 <= 2;
 true
> SELECT 1.0 <= '1';
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-08-01 04:17:52');
 true
> SELECT 1 <= NULL;
 NULL
```

#### Gelijk aan

`expr1 = expr2`: Retourneert true als `expr1` gelijk is `expr2`aan, anders false.

Argumenten:

- `expr1, expr2`: De twee expressies moeten van hetzelfde type zijn of kunnen worden gecast naar een gemeenschappelijk type. Het moet een type zijn dat kan worden gebruikt in een gelijkheidsvergelijking. Kaarttype wordt niet ondersteund. Voor complexe typen zoals array/struct moeten de gegevenstypen van velden kunnen worden geordend.

Voorbeelden:

```
> SELECT 2 = 2;
 true
> SELECT 1 = '1';
 true
> SELECT true = NULL;
 NULL
> SELECT NULL = NULL;
 NULL
```

#### Groter dan

`expr1 > expr2`: Retourneert true als `expr1` groter is dan `expr2`.

Argumenten:

- `expr1, expr2`: De twee expressies moeten van hetzelfde type zijn of kunnen worden gecast naar een gemeenschappelijk type. Het moet een type zijn dat kan worden geordend. Bijvoorbeeld, is het kaarttype niet bestelbaar, zodat wordt het niet gesteund. Voor complexe typen zoals array/struct moeten de gegevenstypen van velden kunnen worden geordend.

Voorbeelden:

```
> SELECT 2 > 1;
 true
> SELECT 2 > '1.1';
 true
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-08-01 04:17:52');
 false
> SELECT 1 > NULL;
 NULL
```

#### Groter dan of gelijk aan

`expr1 >= expr2`: Retourneert true als `expr1` groter dan of gelijk aan `expr2`.

Argumenten:

- `expr1, expr2`: De twee expressies moeten van hetzelfde type zijn of kunnen worden gecast naar een gemeenschappelijk type. Het moet een type zijn dat kan worden geordend. Bijvoorbeeld, is het kaarttype niet bestelbaar, zodat wordt het niet gesteund. Voor complexe typen zoals array/struct moeten de gegevenstypen van velden kunnen worden geordend.

Voorbeelden:

```
> SELECT 2 >= 1;
 true
> SELECT 2.0 >= '2.1';
 false
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-08-01 04:17:52');
 false
> SELECT 1 >= NULL;
 NULL
```

#### Bitsgewijs exclusief of

`expr1 ^ expr2`: Retourneert het resultaat van bitsgewijze exclusieve OR van `expr1` en `expr2`.

Voorbeeld:

```
> SELECT 3 ^ 5;
 2
```

#### en

`expr1 and expr2`: Logische AND.

#### arrays_overlap

`arrays_overlap(a1, a2)`: Retourneert true als a1 ten minste een element bevat dat niet gelijk is aan null en dat zich ook in a2 bevindt. Als de arrays geen gemeenschappelijk element hebben en beide niet-leeg zijn en een van beide een null-element bevatten, wordt null geretourneerd. Anders wordt false geretourneerd.

Voorbeeld:

```
> SELECT arrays_overlap(array(1, 2, 3), array(3, 4, 5));
 true
```

Sinds: 2.4.0.

#### assert_true

`assert_true(expr)`: Hiermee wordt een uitzondering gegenereerd als deze niet true `expr` is.

Voorbeeld:

```
> SELECT assert_true(0 < 1);
 NULL
```

#### indien

`if(expr1, expr2, expr3)`: Indien `expr1` true, wordt de waarde geretourneerd `expr2`; anders retourneert `expr3`.

Voorbeeld:

```
> SELECT if(1 < 2, 'a', 'b');
 a
```

#### ifnull

`ifnull(expr1, expr2)`: Retourneert `expr2` of `expr1` null is of `expr1` anders.

Voorbeeld:

```
> SELECT ifnull(NULL, array('2'));
 ["2"]
```

#### in

`expr1 in(expr2, expr3, ...)`: Retourneert true als dit gelijk is `expr` aan een valN.

Argumenten:
- `expr1, expr2, expr3, ...`: De argumenten moeten van hetzelfde type zijn.

Voorbeelden:

```
> SELECT 1 in(1, 2, 3);
 true
> SELECT 1 in(2, 3, 4);
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 1), named_struct('a', 1, 'b', 3));
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 2), named_struct('a', 1, 'b', 3));
 true
```

#### isnan

`isnan(expr)`: Retourneert true als NaN `expr` is, anders false.

Voorbeeld:

```
> SELECT isnan(cast('NaN' as double));
 true
```

#### isnotnull

`isnotnull(expr)`: Retourneert true als de waarde niet null `expr` is, anders false.

Voorbeelden:

```
> SELECT isnotnull(1);
 true
```

#### isnull

`isnull(expr)`: Retourneert true als de waarde null `expr` is, anders false.

Voorbeeld:

```
> SELECT isnull(1);
 false
```

#### nanvl

`nanvl(expr1, expr2)`: Retourneert `expr1` of het geen NaN is, of `expr2` anders.

Voorbeeld:

```
> SELECT nanvl(cast('NaN' as double), 123);
 123.0
```

#### niet

`not expr`: Logisch niet.

#### of

`expr1 or expr2`: Logisch of.

#### xpath_boolean

`xpath_boolean(xml, xpath)`: Retourneert true als de XPath-expressie true oplevert of als een overeenkomend knooppunt wordt gevonden.

Voorbeeld:

```
> SELECT xpath_boolean('<a><b>1</b></a>','a/b');
 true
```

### Datum-/tijdfuncties

#### add_month

`add_months(start_date, num_months)`: Retourneert de datum die `num_months` volgt `start_date`.

Voorbeeld:

```
> SELECT add_months('2016-08-31', 1);
 2016-09-30
```

Sinds: 1.5.0.

#### date_add

`date_add(start_date, num_days)`: Retourneert de datum die `num_days` volgt `start_date`.

Voorbeeld:

```
> SELECT date_add('2016-07-30', 1);
 2016-07-31
```

Sinds: 1.5.0.

#### date_format

`date_format(timestamp, fmt)`: Zet `timestamp` om in een tekenreekswaarde in de notatie die wordt opgegeven door de datumnotatie `fmt`.

Voorbeeld:

```
> SELECT date_format('2016-04-08', 'y');
 2016
```

Sinds: 1.5.0.

#### date_sub

`date_sub(start_date, num_days)`: Retourneert de datum die `num_days` eerder is `start_date`.

Voorbeeld:

```
> SELECT date_sub('2016-07-30', 1);
 2016-07-29
```

Sinds: 1.5.0.

#### date_trunc

`date_trunc(fmt, ts)`: Retourneert tijdstempels die zijn afgekapt naar de eenheid die is opgegeven in het indelingsmodel `fmt`. `fmt` moet één van [&quot;JAAR&quot;, &quot;YYYY&quot;, &quot;YY&quot;, &quot;MON&quot;, &quot;MONTH&quot;, &quot;MM&quot;, &quot;DAY&quot;, &quot;DD&quot;, &quot;UUR&quot;, &quot;MINUTE&quot;, &quot;SECOND&quot;, &quot;WEEK&quot;, &quot;QUARTER&quot; zijn]

Voorbeelden:

```
> SELECT date_trunc('YEAR', '2015-03-05T09:32:05.359');
 2015-01-01 00:00:00
> SELECT date_trunc('MM', '2015-03-05T09:32:05.359');
 2015-03-01 00:00:00
> SELECT date_trunc('DD', '2015-03-05T09:32:05.359');
 2015-03-05 00:00:00
> SELECT date_trunc('HOUR', '2015-03-05T09:32:05.359');
 2015-03-05 09:00:00
```

Sinds: 2.3.0.

#### datediff

`datediff(endDate, startDate)`: Retourneert het aantal dagen van `startDate` tot `endDate`.

Voorbeelden:

```
> SELECT datediff('2009-07-31', '2009-07-30');
 1

> SELECT datediff('2009-07-30', '2009-07-31');
 -1
```

Sinds: 1.5.0.

#### dag

`day(date)`: Retourneert de dag van de maand van de datum/tijdstempel.

Voorbeeld:

```
> SELECT day('2009-07-30');
 30
```

Sinds: 1.5.0.

#### dagmaand

`dayofmonth(date)`: Retourneert de dag van de maand van de datum/tijdstempel.

Voorbeeld:

```
> SELECT dayofmonth('2009-07-30');
 30
```

Sinds: 1.5.0.

#### dag

`dayofweek(date)`: Retourneert de dag van de week voor datum/tijdstempel (1 = zondag, 2 = maandag, ..., 7 = zaterdag).

Voorbeeld:

```
> SELECT dayofweek('2009-07-30');
 5
```

Sinds: 2.3.0.

#### dagboek

`dayofyear(date)`: Retourneert de dag van het jaar van de datum/tijdstempel.

Voorbeeld:

```
> SELECT dayofyear('2016-04-09');
 100
```

Sinds: 1.5.0.

#### from_unixtime

`from_unixtime(unix_time, format)`: Returns `unix_time` in the specified `format`.

Voorbeeld:

```
> SELECT from_unixtime(0, 'yyyy-MM-dd HH:mm:ss');
 1970-01-01 00:00:00
```

Sinds: 1.5.0.

#### from_utc_timestamp

`from_utc_timestamp(timestamp, timezone)`: Interpreteert een timestamp zoals &quot;2017-07-14 02:40:00.0&quot;als tijd in UTC, en geeft die tijd als timestamp in de bepaalde tijdzone terug. &#39;GMT+1&#39; levert bijvoorbeeld &#39;2017-07-14 03:40:00.0&#39; op.

Voorbeeld:

```
> SELECT from_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-31 09:00:00
```

Sinds: 1.5.0.

#### uur

`hour(timestamp)`: Retourneert de uurcomponent van de tekenreeks/tijdstempel.

Voorbeeld:

```
> SELECT hour('2009-07-30 12:58:59');
 12
```

Sinds: 1.5.0.

#### last_day

`last_day(date):` Retourneert de laatste dag van de maand waartoe de datum behoort.

Voorbeeld:

```
> SELECT last_day('2009-01-12');
 2009-01-31
```

Sinds: 1.5.0.

#### minuut

`minute(timestamp)`: Retourneert de minutcomponent van de tekenreeks/tijdstempel.

Voorbeeld:

```
> SELECT minute('2009-07-30 12:58:59');
 58
```

Sinds: 1.5.0.

#### maand

`month(date)` Retourneert de maandcomponent van de datum/tijdstempel.

Voorbeeld:

```
> SELECT month('2016-07-30');
 7
```

Sinds: 1.5.0.

#### month_between

`months_between(timestamp1, timestamp2[, roundOff])`: Als `timestamp1` het later is dan `timestamp2`, is het resultaat positief. Als `timestamp1` en `timestamp2` zijn op dezelfde dag van de maand, of beide de laatste dag van de maand zijn, zal het tijdstip van de dag worden genegeerd. Anders wordt het verschil berekend op basis van 31 dagen per maand en afgerond naar 8 cijfers, tenzij `roundOff=false`.

Voorbeelden:

```
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30');
 3.94959677
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30', false);
 3.9495967741935485
```

Sinds: 1.5.0.

#### next_day

`next_day(start_date, day_of_week)`: Retourneert de eerste datum die later is dan `start_date` en een naam heeft gekregen zoals aangegeven.

Voorbeeld:

```
> SELECT next_day('2015-01-14', 'TU');
 2015-01-20
```

Sinds: 1.5.0.

#### kwartaal

`quarter(date)`: Retourneert het kwartaal van het jaar voor datum, in het bereik 1 tot en met 4.

Voorbeeld:

```
> SELECT quarter('2016-08-31');
 3
```

Sinds: 1.5.0.

#### seconde

`second(timestamp)`: Retourneert de tweede component van de tekenreeks/tijdstempel.

Voorbeeld:

```
> SELECT second('2009-07-30 12:58:59');
 59
```

Sinds: 1.5.0.

#### to_date

`to_date(date_str[, fmt])`: Parseert de `date_str` expressie met de `fmt` expressie met een datum. Retourneert null met ongeldige invoer. Standaard worden de regels voor het casten toegepast op een datum als de code `fmt` wordt weggelaten.

Voorbeelden:

```
> SELECT to_date('2009-07-30 04:17:52');
 2009-07-30
> SELECT to_date('2016-12-31', 'yyyy-MM-dd');
 2016-12-31
```

Sinds: 1.5.0.

#### to_timestamp

`to_timestamp(timestamp[, fmt])`: Hiermee wordt de `timestamp` expressie met de `fmt` expressie geparseerd met een tijdstempel. Retourneert null met ongeldige invoer. Standaard worden de regels voor het casten toegepast op een tijdstempel als de code `fmt` wordt weggelaten.

Voorbeelden:

```
> SELECT to_timestamp('2016-12-31 00:12:00');
 2016-12-31 00:12:00
> SELECT to_timestamp('2016-12-31', 'yyyy-MM-dd');
 2016-12-31 00:00:00
```

Sinds: 2.2.0.

#### to_unix_timestamp

`to_unix_timestamp(expr[, pattern])`: Retourneert de UNIX-tijdstempel van de opgegeven tijd.

Voorbeeld:

```
> SELECT to_unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Sinds: 1.6.0.

#### to_utc_timestamp

`to_utc_timestamp(timestamp, timezone)`: Interpreteert een timestamp zoals &quot;2017-07-14 02:40:00.0&quot;als tijd in de bepaalde tijdzone, en geeft die tijd als timestamp in UTC terug. &#39;GMT+1&#39; levert bijvoorbeeld &#39;2017-07-14 01:40:00.0&#39; op.

Voorbeeld:

```
> SELECT to_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-30 15:00:00
```

Sinds: 1.5.0.

#### trunc

`trunc(date, fmt)`: Retourneert de datum met het tijdgedeelte van de dag ingekort tot de eenheid die is opgegeven door het indelingsmodel `fmt`. `fmt` is één van [&quot;jaar&quot;, &quot;jjjj&quot;, &quot;jj&quot;, &quot;mon&quot;, &quot;maand&quot;, &quot;mm&quot;]

Voorbeelden:

```
> SELECT trunc('2009-02-12', 'MM');
 2009-02-01
> SELECT trunc('2015-10-27', 'YEAR');
 2015-01-01
```

Sinds: 1.5.0.

#### unix_timestamp

`unix_timestamp([expr[, pattern]])`: Retourneert de UNIX-tijdstempel van de huidige of opgegeven tijd.

Voorbeelden:

```
> SELECT unix_timestamp();
 1476884637
> SELECT unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Sinds: 1.5.0.

#### weekdag

`weekday(date)`: Retourneert de dag van de week voor datum/tijdstempel (0 = maandag, 1 = dinsdag, ..., 6 = zondag).

Voorbeeld:

```
> SELECT weekday('2009-07-30');
 3
```

Sinds: 2.4.0.

#### week_van_jaar

`weekofyear(date)`: Geeft als resultaat de week van het jaar van de opgegeven datum. Een week begint op maandag en week 1 is de eerste week met > 3 dagen.

Voorbeeld:

```
> SELECT weekofyear('2008-02-20');
 8
```

Sinds: 1.5.0.

#### wanneer

`CASE WHEN expr1 THEN expr2 [WHEN expr3 THEN expr4]* [ELSE expr5] END`: Indien `expr1` = true, wordt geretourneerd `expr2`; else if `expr3` = true, retourneert `expr4`; else retourneert `expr5`.

Argumenten:

- `expr1`, `expr3`: De takvoorwaardenuitdrukkingen zouden allen booleaanse type moeten zijn.
- `expr2`, `expr4`, `expr5`: De takwaardeuitdrukkingen en anders waardeuitdrukking zouden allen het zelfde type of dwingbaar aan een gemeenschappelijk type moeten zijn.

Voorbeelden:

```
> SELECT CASE WHEN 1 > 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 1
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 2
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 < 0 THEN 2.0 END;
 NULL
```

#### jaar

`year(date)`: Retourneert de jaarcomponent van de datum/tijdstempel.

Voorbeeld:

```
> SELECT year('2016-07-30');
 2016
```

Sinds: 1.5.0.

### Samengevoegde functies

#### Approx_count_different

`approx_count_distinct(expr[, relativeSD])`: Retourneert de geschatte kardinaliteit door HyperLog++. `relativeSD` definieert de maximaal toegestane schattingsfout.

### Arrays

#### array

`array(expr, ...)`: Geeft als resultaat een array met de opgegeven elementen.

Voorbeeld:

```
> SELECT array(1, 2, 3);
 [1,2,3]
```

#### array_contains

`array_contains(array, value)`: Retourneert true als de array de waarde bevat.

Voorbeeld:

```
> SELECT array_contains(array(1, 2, 3), 2);
 true
```

#### array_different

`array_distinct(array)`: Hiermee worden dubbele waarden uit de array verwijderd.

Voorbeeld:

```
> SELECT array_distinct(array(1, 2, 3, null, 3));
 [1,2,3,null]
```

Sinds: 2.4.0.

#### array_but

`array_except(array1, array2)`: Retourneert een array van de elementen in `array1` maar niet in `array2`, zonder duplicaten.

Voorbeeld:

```
> SELECT array_except(array(1, 2, 3), array(1, 3, 5));
 [2]
```

Sinds: 2.4.0.

#### array_intersect

`array_intersect(array1, array2)`: Retourneert een array van de elementen in de doorsnede van `array1` en `array2`, zonder duplicaten.

Voorbeeld:

```
> SELECT array_intersect(array(1, 2, 3), array(1, 3, 5));
 [1,3]
```

Sinds: 2.4.0.

#### array_join

`array_join(array, delimiter[, nullReplacement])`: Voegt de elementen van de bepaalde array samen met behulp van het scheidingsteken en een optionele tekenreeks ter vervanging van null. Wanneer geen waarde is ingesteld voor `nullReplacement`, wordt een willekeurige null-waarde gefilterd.

Voorbeelden:

```
> SELECT array_join(array('hello', 'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ', ',');
 hello , world
```

Sinds: 2.4.0.

#### array_max

`array_max(array)`: Retourneert de maximumwaarde in de array. Null-elementen worden overgeslagen.

Voorbeeld:

```
> SELECT array_max(array(1, 20, null, 3));
 20
```

Sinds: 2.4.0.

#### array_min

`array_min(array)`: Retourneert de minimumwaarde in de array. Null-elementen worden overgeslagen.

Voorbeeld:

```
> SELECT array_min(array(1, 20, null, 3));
 1
```

Sinds: 2.4.0.

#### array_position

`array_position(array, element)`: Retourneert de (1-gebaseerde) index van het eerste element van de array zolang.

Voorbeeld:

```
> SELECT array_position(array(3, 2, 1), 1);
 3
```

Sinds: 2.4.0.

#### array_remove

`array_remove(array, element)`: Verwijder alle elementen die gelijk zijn aan element uit de array.

Voorbeeld:

```
> SELECT array_remove(array(1, 2, 3, null, 3), 3);
 [1,2,null]
```

Sinds: 2.4.0.

#### array_repeat

`array_repeat(element, count)`: Retourneert de array met daarin de teltijden van elementen.

Voorbeeld:

```
> SELECT array_repeat('123', 2);
 ["123","123"]
```

Sinds: 2.4.0.

#### array_sort

`array_sort(array)`: Hiermee wordt de invoerarray in oplopende volgorde gesorteerd. De elementen van de invoerarray moeten kunnen worden geordend. Null-elementen worden aan het einde van de geretourneerde array geplaatst.

Voorbeeld:

```
> SELECT array_sort(array('b', 'd', null, 'c', 'a'));
 ["a","b","c","d",null]
```

Sinds: 2.4.0.

#### array_union

`array_union(array1, array2)`: Retourneert een array van de elementen in de samenvoeging van `array1` en `array2`, zonder duplicaten.

Voorbeeld:

```
> SELECT array_union(array(1, 2, 3), array(1, 3, 5));
 [1,2,3,5]
```

Sinds: 2.4.0.

#### array_zip

`arrays_zip(a1, a2, ...)`: Retourneert een samengevoegde array van structs waarin de N-th struct alle N-de waarden van invoerarrays bevat.

Voorbeelden:

```
> SELECT arrays_zip(array(1, 2, 3), array(2, 3, 4));
 [{"0":1,"1":2},{"0":2,"1":3},{"0":3,"1":4}]
> SELECT arrays_zip(array(1, 2), array(2, 3), array(3, 4));
 [{"0":1,"1":2,"2":3},{"0":2,"1":3,"2":4}]
```

Sinds: 2.4.0.

#### element_at

`element_at(array, index)`: Retourneert het element van de array bij de opgegeven (op 1 gebaseerde) index. Als `index < 0`, heeft toegang tot elementen van het laatste tot het eerste. Retourneert NULL als de index de lengte van de array overschrijdt.

`element_at(map, key)`: Retourneert de waarde voor de opgegeven toets of NULL als de toets niet in de kaart is opgenomen

Voorbeelden:

```
> SELECT element_at(array(1, 2, 3), 2);
 2
> SELECT element_at(map(1, 'a', 2, 'b'), 2);
 b
```

Sinds: 2.4.0.

#### ontploffen

`explode(expr)`: Scheidt de elementen van de array `expr` in meerdere rijen of de elementen van de kaart `expr` in meerdere rijen en kolommen.

Voorbeelden:

```
> SELECT explode(array(10, 20));
 10
 20
```

#### explode_outer

`explode_outer(expr)`: Scheidt de elementen van de array `expr` in meerdere rijen of de elementen van de kaart `expr` in meerdere rijen en kolommen.

Voorbeeld:

```
> SELECT explode_outer(array(10, 20));
 10
 20
```

#### find_in_set

`find_in_set(str, str_array)`: Retourneert de index (1 gebaseerd) van de opgegeven tekenreeks (`str`) in de lijst met komma&#39;s als scheidingsteken (`str_array`). Geeft 0 terug, als de tekenreeks niet is gevonden of als de opgegeven tekenreeks (`str`) een komma bevat.

Voorbeeld:

```
> SELECT find_in_set('ab','abc,b,ab,c,def');
 3
```

#### afvlakken

`flatten(arrayOfArrays)`: Transformeert een array van arrays naar één array.

Voorbeeld:

```
> SELECT flatten(array(array(1, 2), array(3, 4)));
 [1,2,3,4]
```

Sinds: 2.4.0.

#### inline

`inline(expr)`: Explodeert een array van structs naar een tabel.

Voorbeeld:

```
> SELECT inline(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### inline_outer

`inline_outer(expr)`: Explodeert een array van structs naar een tabel.

Voorbeeld:

```
> SELECT inline_outer(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### gepoëerd

`posexplode(expr)`: Scheidt de elementen van de array `expr` in meerdere rijen met posities, of de elementen van de kaart `expr` in meerdere rijen en kolommen met posities.

Voorbeeld:

```
> SELECT posexplode(array(10,20));
 0  10
 1  20
```

#### posexplode_outer

`posexplode_outer(expr)`: Scheidt de elementen van de array `expr` in meerdere rijen met posities, of de elementen van de kaart `expr` in meerdere rijen en kolommen met posities.

Voorbeeld:

```
> SELECT posexplode_outer(array(10,20));
 0  10
 1  20
```

#### omkeren

`reverse(array)`: Retourneert een omgekeerde tekenreeks of een array met omgekeerde volgorde van elementen.

Voorbeelden:

```
> SELECT reverse('Spark SQL');
 LQS krapS
> SELECT reverse(array(2, 1, 4, 3));
 [3,4,1,2]
```

Sinds: 1.5.0.
>[!NOTE] rse logic for arrays is beschikbaar vanaf 2.4.0.

#### schudden

`shuffle(array)`: Geeft een willekeurige permutatie van de opgegeven array.

Voorbeelden:

```
> SELECT shuffle(array(1, 20, 3, 5));
 [3,1,5,20]
> SELECT shuffle(array(1, 20, null, 3));
 [20,null,3,1]
```

Sinds: 2.4.0.
>[!NOTE] niet deterministisch is.

#### segment

`slice(x, start, length)`: Subsets van array x vanaf het begin van de index (of vanaf het einde als start negatief is) met de opgegeven lengte.

Voorbeelden:

```
> SELECT slice(array(1, 2, 3, 4), 2, 2);
 [2,3]
> SELECT slice(array(1, 2, 3, 4), -2, 2);
 [3,4]
```

Sinds: 2.4.0.

#### sort_array

`sort_array(array[, ascendingOrder])`: Sorteert de invoerarray in oplopende of aflopende volgorde volgens de natuurlijke volgorde van de arrayelementen. Null-elementen worden in oplopende volgorde aan het begin van de geretourneerde array geplaatst of aan het einde van de geretourneerde array in aflopende volgorde.

Voorbeelden:

```
> SELECT sort_array(array('b', 'd', null, 'c', 'a'), true);
 [null,"a","b","c","d"]
```

#### zip_with

`zip_with(left, right, func)`: Voegt de twee gegeven arrays, elemetaal, samen tot één array met behulp van functie. Wanneer één array korter is, worden null&#39;s aan het einde toegevoegd, zodat deze overeenkomen met de lengte van de langere array, voordat functie wordt toegepast.

Voorbeelden:

```
> SELECT zip_with(array(1, 2, 3), array('a', 'b', 'c'), (x, y) -> (y, x));
 [{"y":"a","x":1},{"y":"b","x":2},{"y":"c","x":3}]
> SELECT zip_with(array(1, 2), array(3, 4), (x, y) -> x + y);
 [4,6]
> SELECT zip_with(array('a', 'b', 'c'), array('d', 'e', 'f'), (x, y) -> concat(x, y));
 ["ad","be","cf"]
```

Sinds: 2.4.0.

### Datatype casting-functies

#### onbeschaamdheid

`bigint(expr)`: Casts the value `expr` to the target data type `bigint`.

#### binair

`binary(expr)`: Casts the value `expr` to the target data type `binary`.

#### boolean

`boolean(expr)`: Casts the value `expr` to the target data type `boolean`.

#### gieten

`cast(expr AS type)`: Casts the value `expr` to the target data type `type`.

Voorbeeld:

```
> SELECT cast('10' as int);
 10
```

#### date

`date(expr)`: Casts the value `expr` to the target data type `date`.

#### decimaal

`decimal(expr)`: Casts the value `expr` to the target data type `decimal`.

#### double

`double(expr)`: Casts the value `expr` to the target data type `double`.

#### zweven

`float(expr)`: Casts the value `expr` to the target data type `float`.

#### int

`int(expr)`: Casts the value `expr` to the target data type `int`.

#### map

`map(key0, value0, key1, value1, ...)`: Hiermee maakt u een kaart met de opgegeven sleutel-/waardeparen.

Voorbeeld:

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### kleinste

`smallint(expr)`: Casts the value `expr` to the target data type `smallint`.

#### str_to_map

`str_to_map(text[, pairDelim[, keyValueDelim]])`: Maakt een kaart nadat de tekst met behulp van scheidingstekens is gesplitst in sleutel-/waardeparen. Standaardscheidingstekens zijn &#39;,&#39; for `pairDelim` en &#39;:&#39; for `keyValueDelim`.

Voorbeelden:

```
> SELECT str_to_map('a:1,b:2,c:3', ',', ':');
 map("a":"1","b":"2","c":"3")
> SELECT str_to_map('a');
 map("a":null)
```

#### string

`string(expr)`: Casts the value `expr` to the target data type `string`.

#### struct

`struct(col1, col2, col3, ...)`: Maakt een structuur met de opgegeven veldwaarden.

#### tinyint

`tinyint(expr)`: Casts the value `expr` to the target data type `tinyint`.

### Conversie- en opmaakfuncties

#### ascii

`ascii(str)`: Retourneert de numerieke waarde van het eerste teken van `str`.

Voorbeelden:

```
> SELECT ascii('222');
 50
> SELECT ascii(2);
 50
```

#### base64

`base64(bin)`: Converteert het argument van binair `bin` in een basis 64 koord.

Voorbeeld:

```
> SELECT base64('Spark SQL');
 U3BhcmsgU1FM
```

#### bin

`bin(expr)`: Retourneert de tekenreeksrepresentatie van de lange waarde `expr` die in binair getal wordt vertegenwoordigd.

Voorbeelden:

```
> SELECT bin(13);
 1101
> SELECT bin(-13);
 1111111111111111111111111111111111111111111111111111111111110011
> SELECT bin(13.3);
 1101
```

#### bit_length

`bit_length(expr)`: Retourneert de bitlengte van tekenreeksgegevens of het aantal bits van binaire gegevens.

Voorbeeld:

```
> SELECT bit_length('Spark SQL');
 72
```

#### char

`char(expr)`: Retourneert het ASCII-teken met het binaire equivalent aan `expr`. Als n groter is dan 256, is het resultaat gelijk aan `chr(n % 256)`.

Voorbeeld:

```
> SELECT char(65);
 A
```

#### char_length

`char_length(expr)`: Retourneert de tekenlengte van tekenreeksgegevens of het aantal bytes van binaire gegevens. De lengte van tekenreeksgegevens bevat de volgende spaties. De lengte van binaire gegevens omvat binaire nullen.

Voorbeelden:

```
> SELECT char_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### character_length

`character_length(expr)`: Retourneert de tekenlengte van tekenreeksgegevens of het aantal bytes van binaire gegevens. De lengte van tekenreeksgegevens bevat de volgende spaties. De lengte van binaire gegevens omvat binaire nullen.

Voorbeelden:

```
> SELECT character_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### chr

`chr(expr)`: Retourneert het ASCII-teken met het binaire equivalent aan expr. Als n groter is dan 256, is het resultaat gelijk aan `chr(n % 256)`

Voorbeeld:

```
> SELECT chr(65);
 A
```

#### graden

`degrees(expr)`: Zet radialen om in graden.

Argumenten:
- `expr`: Hoek in radialen

Voorbeeld:

```
> SELECT degrees(3.141592653589793);
 180.0
```

#### format_number

`format_number(expr1, expr2)`: Hiermee wordt het nummer opgemaakt `expr1` als &#39;#,###,###.##&#39;, afgerond tot op `expr2` decimalen. Als `expr2` 0 is, heeft het resultaat geen decimaalteken of fractioneel deel. `expr2` accepteert ook een door de gebruiker opgegeven indeling. Dit is bedoeld om als MySQL&#39;s te functioneren `FORMAT`.

Voorbeelden:

```
> SELECT format_number(12332.123456, 4);
 12,332.1235
> SELECT format_number(12332.123456, '##################.###');
 12332.123
```

#### from_json

`from_json(jsonStr, schema[, options])`: Geeft als resultaat een struct-waarde met de opgegeven `jsonStr` en `schema`.

Voorbeelden:

```
> SELECT from_json('{"a":1, "b":0.8}', 'a INT, b DOUBLE');
 {"a":1, "b":0.8}
> SELECT from_json('{"time":"26/08/2015"}', 'time Timestamp', map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"2015-08-26 00:00:00.0"}
```

Sinds: 2.2.0.

#### hash

`hash(expr1, expr2, ...)`: Retourneert een hashwaarde van de argumenten.

Voorbeeld:

```
> SELECT hash('Spark', array(123), 2);
 -1321691492
```

#### hex

`hex(expr)`: Converteert `expr` naar hexadecimaal.

Voorbeelden:

```
> SELECT hex(17);
 11
> SELECT hex('Spark SQL');
 537061726B2053514C
```

#### initcap

`initcap(str)`: Retourneert `str` de eerste letter van elk woord in hoofdletters. Alle andere letters zijn in kleine letters. Woorden worden gescheiden door witruimte.

Voorbeeld:

```
> SELECT initcap('sPark sql');
 Spark Sql
```

#### lcase

`lcase(str)`: Retourneert `str` met alle tekens gewijzigd in kleine letters.

Voorbeeld:

```
> SELECT lcase('SparkSql');
 sparksql
```

#### lager

`lower(str)`: Retourneert `str` met alle tekens gewijzigd in kleine letters.

Voorbeeld:

```
> SELECT lower('SparkSql');
 sparksql
```

#### lpad

`lpad(str, len, pad)`: Retourneert `str`, links opgevuld `pad` met een lengte van `len`. Als `str` het langer is dan `len`, wordt de geretourneerde waarde ingekort tot `len` tekens.

Voorbeelden:

```
> SELECT lpad('hi', 5, '??');
 ???hi
> SELECT lpad('hi', 1, '??');
 h
```

#### map

`map(key0, value0, key1, value1, ...)`: Hiermee maakt u een kaart met de opgegeven sleutel-/waardeparen.

Voorbeeld:

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### map_from_arrays

`map_from_arrays(keys, values)`: Maakt een kaart met een paar van de opgegeven sleutel-/waardearrays. Elementen in toetsen mogen niet null zijn.

Voorbeeld:

```
> SELECT map_from_arrays(array(1.0, 3.0), array('2', '4'));
 {1.0:"2",3.0:"4"}
```

Sinds: 2.4.0.

#### map_from_entries

`map_from_entries(arrayOfEntries)`: Geeft als resultaat een map die is gemaakt op basis van de opgegeven array van items.

Voorbeeld:

```
> SELECT map_from_entries(array(struct(1, 'a'), struct(2, 'b')));
 {1:"a",2:"b"}
```

Sinds: 2.4.0.

#### md5

`md5(expr)`: Retourneert een MD5 128-bits controlesom als een hexadecimale tekenreeks van `expr`.

Voorbeeld:

```
> SELECT md5('Spark');
 8cde774d6f7333752ed72cacddb05126
```

#### rpad

`rpad(str, len, pad)`: Retourneert `str`, rechts opgevuld met `pad` een lengte van `len`. Als `str` het langer is dan `len`, wordt de geretourneerde waarde ingekort tot `len` tekens.

Voorbeelden:

```
> SELECT rpad('hi', 5, '??');
 hi???
> SELECT rpad('hi', 1, '??');
 h
```

#### rtrim

`rtrim(str)`: Hiermee verwijdert u de spatietekens aan het einde uit `str`het palet.

`rtrim(trimStr, str)`: Verwijdert de volgende tekenreeks, die de tekens uit de bijsnijdtekenreeks uit de `str`tekenreeks bevat.

Argumenten:
- `str`: Een tekenreeksexpressie
- `trimStr`: De bij te snijden tekenreekstekens. De standaardwaarde is één spatie

Voorbeelden:

```
> SELECT rtrim('    SparkSQL   ');
 SparkSQL
> SELECT rtrim('LQSa', 'SSparkSQLS');
 SSpark
```

#### sha

`sha(expr)`: Retourneert een `sha1` hashwaarde als een hexadecimale tekenreeks van de `expr`.

Voorbeeld:

```
> SELECT sha('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha1

`sha1(expr)`: Retourneert een `sha1` hashwaarde als een hexadecimale tekenreeks van de `expr`.

Voorbeeld:

```
> SELECT sha1('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha2

`sha2(expr, bitLength)`: Retourneert een controlesom van SHA-2-familie als een hexadecimale tekenreeks van `expr`. SHA-224, SHA-256, SHA-384, en SHA-512 worden gesteund. De bitlengte 0 komt overeen met 256.

Voorbeeld:

```
> SELECT sha2('Spark', 256);
 529bc3b07127ecb7e53a4dcf1991d9152c24537d919178022b2c42657f79a26b
```

#### soundex

`soundex(str)`: Geeft Soundex-code van de tekenreeks.

Voorbeeld:

```
> SELECT soundex('Miller');
 M460
```

#### stapel

`stack(n, expr1, ..., exprk)`: Scheidt `expr1`... `exprk` in `n` rijen.

Voorbeeld:

```
> SELECT stack(2, 1, 2, 3);
 1  2
 3  NULL
```

#### substr

`substr(str, pos[, len])`: Retourneert de subtekenreeks van `str` die begint bij `pos` en lengte heeft `len`, of het segment van de bytearray dat begint bij `pos` en lengte heeft `len`.

Voorbeelden:

```
> SELECT substr('Spark SQL', 5);
 k SQL
> SELECT substr('Spark SQL', -3);
 SQL
> SELECT substr('Spark SQL', 5, 1);
 k
```

#### substring

`substring(str, pos[, len])`: Retourneert de subtekenreeks van `str` die begint bij `pos` en lengte heeft `len`, of het segment van de bytearray dat begint bij `pos` en lengte heeft `len`.

Voorbeelden:

```
> SELECT substring('Spark SQL', 5);
 k SQL
> SELECT substring('Spark SQL', -3);
 SQL
> SELECT substring('Spark SQL', 5, 1);
 k
```

#### to_json

`to_json(expr[, options])`: Geeft als resultaat een JSON-tekenreeks met een opgegeven struct-waarde.

Voorbeelden:

```
> SELECT to_json(named_struct('a', 1, 'b', 2));
 {"a":1,"b":2}
> SELECT to_json(named_struct('time', to_timestamp('2015-08-26', 'yyyy-MM-dd')), map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"26/08/2015"}
> SELECT to_json(array(named_struct('a', 1, 'b', 2)));
 [{"a":1,"b":2}]
> SELECT to_json(map('a', named_struct('b', 1)));
 {"a":{"b":1}}
> SELECT to_json(map(named_struct('a', 1),named_struct('b', 2)));
 {"[1]":{"b":2}}
> SELECT to_json(map('a', 1));
 {"a":1}
> SELECT to_json(array((map('a', 1))));
 [{"a":1}]
```

Sinds: 2.2.0.

#### vertalen

`translate(input, from, to)`: Zet de `input` tekenreeks om door de tekens in de `from` tekenreeks te vervangen door de corresponderende tekens in de `to` tekenreeks.

Voorbeeld:

```
> SELECT translate('AaBbCc', 'abc', '123');
 A1B2C3
```

#### bijsnijden

`trim(str)`: Hiermee verwijdert u de spatietekens vóór en achter de spatie uit `str`.

`trim(BOTH trimStr FROM str)`: Verwijder de voorlooptekens en navolgende `trimStr` tekens uit `str`.

`trim(LEADING trimStr FROM str)`: Verwijder de voorlooptekens `trimStr` uit `str`.

`trim(TRAILING trimStr FROM str)`: Verwijder de navolgende `trimStr` tekens uit `str`.

Argumenten:
- `str`: Een tekenreeksexpressie
- `trimStr`: De bij te snijden tekenreekstekens hebben als standaardwaarde één spatie.
- `BOTH`, `FROM`: Dit zijn trefwoorden om het bijsnijden van tekenreekstekens vanaf beide uiteinden van de tekenreeks op te geven
- `LEADING`, `FROM`: Dit zijn trefwoorden om het bijsnijden van tekenreekstekens vanaf het linkeruiteinde van de tekenreeks op te geven
- `TRAILING`, `FROM`: Dit zijn trefwoorden om het bijsnijden van tekenreekstekens vanaf het rechtereinde van de tekenreeks op te geven

Voorbeelden:

```
> SELECT trim('    SparkSQL   ');
 SparkSQL
> SELECT trim('SL', 'SSparkSQLS');
 parkSQ
> SELECT trim(BOTH 'SL' FROM 'SSparkSQLS');
 parkSQ
> SELECT trim(LEADING 'SL' FROM 'SSparkSQLS');
 parkSQLS
> SELECT trim(TRAILING 'SL' FROM 'SSparkSQLS');
 SSparkSQ
```

#### kauwen

`ucase(str)`: Retourneert `str` met alle tekens gewijzigd in hoofdletters.

Voorbeeld:

```
> SELECT ucase('SparkSql');
 SPARKSQL
```

#### unbase64

`unbase64(str)`: Zet het argument van een basis 64 koord `str` in een binair getal om.

Voorbeeld:

```
> SELECT unbase64('U3BhcmsgU1FM');
 Spark SQL
```

#### unhex

`unhex(expr)`: Hexadecimaal converteert `expr` naar binair.

Voorbeeld:

```
> SELECT decode(unhex('537061726B2053514C'), 'UTF-8');
 Spark SQL
```

#### bovenste

`upper(str)`: Retourneert `str` met alle tekens gewijzigd in hoofdletters.

Voorbeeld:

```
> SELECT upper('SparkSql');
 SPARKSQL
```

#### uuid

`uuid()`: Retourneert een universeel unieke id-tekenreeks (UUID). De waarde wordt geretourneerd als een canonieke UUID-tekenreeks van 36 tekens.

Voorbeeld:

```
> SELECT uuid();
 46707d92-02f4-4817-8116-a4c3b23e6266
```

>[!NOTE] Functie is niet deterministisch.

### Gegevensevaluatie

#### samenvoegen

`coalesce(expr1, expr2, ...)`: Retourneert het eerste argument anders dan null als dit bestaat. Anders null.

Voorbeeld:

```
> SELECT coalesce(NULL, 1, NULL);
 1
```

#### collect_list

`collect_list(expr)`: Hiermee wordt een lijst met niet-unieke elementen verzameld en geretourneerd.

#### collection_set

`collect_set(expr)`: Hiermee wordt een set unieke elementen verzameld en geretourneerd.

#### concat

`concat(col1, col2, ..., colN)`: Keert de aaneenschakeling van col1, col2, ..., colN terug.

Voorbeelden:

```
> SELECT concat('Spark', 'SQL');
 SparkSQL
> SELECT concat(array(1, 2, 3), array(4, 5), array(6));
 [1,2,3,4,5,6]
```

>[!NOTE] logica `concat` voor arrays is beschikbaar sinds 2.4.0.

#### concat_ws

`concat_ws(sep, [str | array(str)]+)`: Retourneert de samenvoeging van de tekenreeksen gescheiden door `sep`.

Voorbeeld:

```
> SELECT concat_ws(' ', 'Spark', 'SQL');
  Spark SQL
```

#### aantal

`count(*)`: Retourneert het totale aantal opgehaalde rijen, inclusief rijen met null.

`count(expr[, expr...])`: Retourneert het aantal rijen waarvoor de opgegeven expressies allemaal niet null zijn.

`count(DISTINCT expr[, expr...])`: Retourneert het aantal rijen waarvoor de opgegeven expressies uniek en niet-null zijn.

#### crc32

`crc32(expr)`: Retourneert een cyclische waarde voor overtolligheidscontrole van de eigenschap `expr` als een bigint.

Voorbeeld:

```
> SELECT crc32('Spark');
 1557323817
```

#### decoderen

`decode(bin, charset)`: Decodeert het eerste argument met de tweede argumenttekenset.

Voorbeeld:

```
> SELECT decode(encode('abc', 'utf-8'), 'utf-8');
 abc
```

#### vilt

`elt(n, input1, input2, ...)`: Retourneert de `n`de invoer, bijvoorbeeld retourneert `input2` wanneer `n` de waarde 2 is.

Voorbeeld:

```
> SELECT elt(1, 'scala', 'java');
 scala
```

#### coderen

`encode(str, charset)`: Codeert het eerste argument met de tweede argumenttekenset.

Voorbeeld:

```
> SELECT encode('abc', 'utf-8');
 abc
```

#### first

`first(expr[, isIgnoreNull])`: Retourneert de eerste waarde van `expr` voor een groep rijen. Als `isIgnoreNull` true is, worden alleen waarden geretourneerd die niet gelijk zijn aan null.

#### first_value

`first_value(expr[, isIgnoreNull])`: Retourneert de eerste waarde van `expr` voor een groep rijen. Als `isIgnoreNull` true is, worden alleen waarden geretourneerd die niet gelijk zijn aan null.

#### get_json_object

`get_json_object(json_txt, path)`: Extraheert een json-object van `path`.

Voorbeeld:

```
> SELECT get_json_object('{"a":"b"}', '$.a');
 b
```

#### groeperen

<!-- was blank --->

#### grouping_id

<!-- was blank --->

#### instr

`instr(str, substr)`: Retourneert de (1-gebaseerde) index van de eerste instantie van `substr` in `str`.

Voorbeeld:

```
> SELECT instr('SparkSQL', 'SQL');
 6
```

#### json_tuple

`json_tuple(jsonStr, p1, p2, ..., pn)`: Retourneert een tegel zoals de functie `get_json_object`, maar er zijn meerdere namen voor nodig. Alle invoerparameters en typen uitvoerkolommen zijn tekenreeksen.

Voorbeeld:

```
> SELECT json_tuple('{"a":1, "b":2}', 'a', 'b');
 1  2
```

#### aanwijzen

`lag(input[, offset[, default]])`: Retourneert de waarde van `input` bij de `offset`e rij vóór de huidige rij in het venster. De standaardwaarde van `offset` is 1 en de standaardwaarde van `default` is ongeldig. Als de waarde van `input` bij de `offset`rij null is, wordt null geretourneerd. Als er geen dergelijke compensatierij is (bijvoorbeeld, wanneer de compensatie 1 is, heeft de eerste rij van het venster geen vorige rij), en `default` is teruggekeerd.

#### last

`last(expr[, isIgnoreNull])`: Retourneert de laatste waarde van `expr` voor een groep rijen. Als `isIgnoreNull` true is, worden alleen waarden geretourneerd die niet gelijk zijn aan null.

#### last_value

`last_value(expr[, isIgnoreNull])`: Retourneert de laatste waarde van `expr` voor een groep rijen. Als `isIgnoreNull` true is, worden alleen waarden geretourneerd die niet gelijk zijn aan null.

#### leiden

`lead(input[, offset[, default]])`: Retourneert de waarde van `input` bij de `offset`e rij na de huidige rij in het venster. De standaardwaarde van `offset` is 1 en de standaardwaarde van `default` is ongeldig. Als de waarde van `input` bij de `offset`rij null is, wordt null geretourneerd. Als er geen dergelijke verschuivingsrij is (bijvoorbeeld als de verschuiving 1 is, heeft de laatste rij van het venster geen volgende rij) en `default` wordt deze geretourneerd.


#### left

`left(str, len)`: Retourneert de meest linkse `len` (`len` kan tekenreekstype zijn) tekens van de tekenreeks `str`. Als `len` kleiner dan of gelijk aan 0 is, is het resultaat een lege tekenreeks.

Voorbeeld:

> SELECT left(&#39;Spark SQL&#39;, 3);
Spa


#### length

`length(expr)`: Retourneert de tekenlengte van tekenreeksgegevens of het aantal bytes van binaire gegevens. De lengte van tekenreeksgegevens bevat de volgende spaties. De lengte van binaire gegevens omvat binaire nullen.

Voorbeelden:

```
> SELECT length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### lokaliseren

`locate(substr, str[, pos])`: Retourneert de positie van het eerste exemplaar van `substr` in `str` de volgende positie `pos`. De gegeven `pos` en terugkeerwaarde zijn 1-gebaseerd.

Voorbeelden:

```
> SELECT locate('bar', 'foobarbar');
 4
> SELECT locate('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### map_concat

`map_concat(map, ...)`: Geeft als resultaat de samenvoeging van alle opgegeven kaarten.

Voorbeeld:

```
> SELECT map_concat(map(1, 'a', 2, 'b'), map(2, 'c', 3, 'd'));
 {1:"a",2:"c",3:"d"}
```

Sinds: 2.4.0.

#### map_keys

`map_keys(map)`: Retourneert een ongeordende array met de toetsen van de kaart.

Voorbeeld:

```
> SELECT map_keys(map(1, 'a', 2, 'b'));
 [1,2]
```

#### map_values

`map_values(map)`: Retourneert een ongeordende array met de waarden van de kaart.

Voorbeeld:

```
> SELECT map_values(map(1, 'a', 2, 'b'));
 ["a","b"]
```

#### ntegel

`ntile(n)`: Verdeelt de rijen voor elke vensterverdeling in `n` emmers die zich van 1 tot hoogstens uitstrekken `n`.

#### nullif

`nullif(expr1, expr2)`: Retourneert null als `expr1` gelijk is aan `expr2`, of `expr1` anderszins.

Voorbeeld:

```
> SELECT nullif(2, 2);
 NULL
```

#### nvl

`nvl(expr1, expr2)`: Retourneert `expr2` of `expr1` null is of `expr1` anders.

Voorbeeld:

```
> SELECT nvl(NULL, array('2'));
 ["2"]
```

#### nvl2

`nvl2(expr1, expr2, expr3)`: Retourneert `expr2` of `expr1` de waarde null is of `expr3` anders.

Voorbeeld:

```
> SELECT nvl2(NULL, 2, 1);
 1
```

#### parse_url

`parse_url(url, partToExtract[, key])`: Extraheert een onderdeel van een URL.

Voorbeelden:

```
> SELECT parse_url('http://spark.apache.org/path?query=1', 'HOST')
 spark.apache.org
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY')
 query=1
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY', 'query')
 1
```

#### positie

`position(substr, str[, pos])`: Retourneert de positie van het eerste exemplaar van `substr` in `str` de volgende positie `pos`. De gegeven `pos` en terugkeerwaarde zijn 1-gebaseerd.

Voorbeelden:

```
> SELECT position('bar', 'foobarbar');
 4
> SELECT position('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### rangschikken

`rank()`: Berekent de positie van een waarde in een groep waarden. Het resultaat is één plus het aantal rijen voorafgaand aan of gelijk aan de huidige rij in het orde van de verdeling. De waarden produceren hiaten in de opeenvolging.

#### regexp_extract

`regexp_extract(str, regexp[, idx])`: Extraheert een groep die overeenkomt `regexp`.

Voorbeeld:

```
> SELECT regexp_extract('100-200', '(\\d+)-(\\d+)', 1);
 100
```

#### regex_replace

`regexp_replace(str, regexp, rep)`: Hiermee worden alle subtekenreeksen van `str` die overeenkomen vervangen `regexp` met `rep`.

Voorbeeld:

```
> SELECT regexp_replace('100-200', '(\\d+)', 'num');
 num-num
```

#### herhalen

`repeat(str, n)`: Geeft de tekenreeks die de opgegeven tekenreekswaarde in keer herhaalt.

Voorbeeld:

```
> SELECT repeat('123', 2);
 123123
```

#### vervangen

`replace(str, search[, replace])`: Vervangt alle exemplaren van `search` het bestand door `replace`.

Argumenten:
- `str`: Een tekenreeksexpressie
- `search`: Een tekenreeksexpressie. Als `search` niet gevonden in `str`, `str` wordt ongewijzigd geretourneerd.
- `replace`: Een tekenreeksexpressie. Wanneer `replace` geen tekenreeks is opgegeven of een lege tekenreeks is, vervangt niets de tekenreeks die is verwijderd `str`.

Voorbeeld:

```
> SELECT replace('ABCabc', 'abc', 'DEF');
 ABCDEF
```

#### rollup

<!-- was blank -->

#### row_number

`row_number()`: Wijst een uniek, opeenvolgend aantal aan elke rij toe, die met één begint, volgens de orde van rijen binnen de vensterverdeling.

#### schema_of_json

`schema_of_json(json[, options])`: Retourneert het schema in de DDL-indeling van de JSON-tekenreeks.

Voorbeeld:

```
> SELECT schema_of_json('[{"col":0}]');
 array<struct<col:int>>
```

Sinds: 2.4.0.

#### straffen

`sentences(str[, lang, country])`: Splitst `str` in een array van woorden.

Voorbeeld:

```
> SELECT sentences('Hi there! Good morning.');
 [["Hi","there"],["Good","morning"]]
```

#### opeenvolging

`sequence(start, stop, step)`: Genereert een array met elementen van begin tot einde (inclusief), stapsgewijs verhoogd. Het type van de geretourneerde elementen is hetzelfde als het type argumentexpressies.

Ondersteunde typen zijn: byte, short, integer, long, date, timestamp.

De expressies `start` en `stop` expressies moeten hetzelfde type hebben. Als `start` en `stop` expressies het type &#39;date&#39; of &#39;timestamp&#39; hebben, moet de `step` expressie het type &#39;interval&#39; omzetten. anders wordt het omgezet in hetzelfde type als de expressies `start` en de `stop` expressies.

Argumenten:
- `start`: Een expressie. Het begin van het bereik.
- `stop`: Een expressie. Het einde van het bereik (inclusief).
- `step`: Een optionele expressie. De stap van het bereik. Standaard `step` is 1 als `start` kleiner dan of gelijk aan `stop`, anders -1. Voor de tijdsequenties is het respectievelijk 1 dag en -1 dag. Als `start` groter dan `stop`, `step` moet negatief zijn, en vice versa.

Voorbeelden:

```
> SELECT sequence(1, 5);
 [1,2,3,4,5]
> SELECT sequence(5, 1);
 [5,4,3,2,1]
> SELECT sequence(to_date('2018-01-01'), to_date('2018-03-01'), interval 1 month);
 [2018-01-01,2018-02-01,2018-03-01]
```

Sinds: 2.4.0.

#### shiftLeft

`shiftleft(base, expr)`: Bitsgewijs naar links verplaatsen.

Voorbeeld:

```
> SELECT shiftleft(2, 1);
 4
```

#### schuifrecht

`shiftright(base, expr)`: Bitsgewijs (ondertekend) naar rechts verplaatsen.

Voorbeeld:

```
> SELECT shiftright(4, 1);
 2
```

#### shiftTrighouted

`shiftrightunsigned(base, expr)`: Bitsgewijs zonder teken naar rechts verplaatsen.

Voorbeeld:

```
> SELECT shiftrightunsigned(4, 1);
 2
```

#### size

`size(expr)`: Retourneert de grootte van een array of een kaart. De functie retourneert -1 als de invoer null is en op true `spark.sql.legacy.sizeOfNull` is ingesteld. Als deze waarde op false `spark.sql.legacy.sizeOfNull` is ingesteld, retourneert de functie null voor null-invoer. Standaard is de `spark.sql.legacy.sizeOfNull` parameter ingesteld op true.

Voorbeelden:

```
> SELECT size(array('b', 'd', 'c', 'a'));
 4
> SELECT size(map('a', 1, 'b', 2));
 2
> SELECT size(NULL);
 -1
```

#### spatie

`space(n)`: Retourneert een tekenreeks die bestaat uit `n` spaties.

Voorbeeld:

```
> SELECT concat(space(2), '1');
   1
```

#### splitsen

`split(str, regex)`: Splitst `str` `regex`op overeenkomende exemplaren.

Voorbeeld:

```
> SELECT split('oneAtwoBthreeC', '[ABC]');
 ["one","two","three",""]
```

#### substring_index

`substring_index(str, delim, count)`: Retourneert de subtekenreeks van `str` vóór het `count` voorkomen van het scheidingsteken `delim`. Als `count` dit positief is, wordt alles links van het laatste scheidingsteken (geteld vanaf links) geretourneerd. Als dit negatief `count` is, wordt alles rechts van het laatste scheidingsteken (geteld vanaf rechts) geretourneerd. De functie `substring_index` voert een case-sensitive gelijke uit wanneer het zoeken naar `delim`.

Voorbeeld:

```
> SELECT substring_index('www.apache.org', '.', 2);
 www.apache
```

#### venster

<!-- was blank -->

#### xpath

`xpath(xml, xpath)`: Retourneert een tekenreeks met waarden binnen de knooppunten van xml die overeenkomen met de XPath-expressie.

Voorbeeld:

```
> SELECT xpath('<a><b>b1</b><b>b2</b><b>b3</b><c>c1</c><c>c2</c></a>','a/b/text()');
 ['b1','b2','b3']
```

#### xpath_double

`xpath_double(xml, xpath)`: Retourneert een dubbele waarde, de waarde nul als er geen overeenkomst is gevonden, of NaN als een overeenkomst is gevonden maar de waarde niet numeriek is.

Voorbeeld:

```
> SELECT xpath_double('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_float

`xpath_float(xml, xpath)`: Retourneert een drijvende-kommawaarde, de waarde nul als er geen overeenkomst wordt gevonden, of NaN als een overeenkomst wordt gevonden, maar de waarde niet numeriek is.

Voorbeeld:

```
> SELECT xpath_float('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_int

`xpath_int(xml, xpath)`: Retourneert een geheel getal of de waarde nul als er geen overeenkomst is gevonden of als er een overeenkomst is gevonden maar de waarde niet numeriek is.

Voorbeeld:

```
> SELECT xpath_int('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_long

`xpath_long(xml, xpath)`: Retourneert een lange geheel-getalwaarde, of de waarde nul als er geen overeenkomst is gevonden, of een overeenkomst is gevonden maar de waarde niet-numeriek is.

Voorbeeld:

```
> SELECT xpath_long('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_number

`xpath_number(xml, xpath)`: Retourneert een dubbele waarde, de waarde nul als er geen overeenkomst is gevonden, of NaN als een overeenkomst is gevonden maar de waarde niet numeriek is.

Voorbeeld:

```
> SELECT xpath_number('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_short

`xpath_short(xml, xpath)`: Retourneert een korte geheel-getalwaarde, of de waarde nul als er geen overeenkomst is gevonden, of een overeenkomst is gevonden maar de waarde niet-numeriek is.

Voorbeeld:

```
> SELECT xpath_short('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_string

`xpath_string(xml, xpath)`: Retourneert de tekstinhoud van het eerste XML-knooppunt dat overeenkomt met de XPath-expressie.

Voorbeeld:

```
> SELECT xpath_string('<a><b>b</b><c>cc</c></a>','a/c');
 cc
```

### Huidige informatie

#### current_database

`current_database()`: Retourneert de huidige database.

Voorbeeld:

```
> SELECT current_database();
 default
```

#### current_date

`current_date()`: Keert de huidige datum bij het begin van vraagevaluatie terug.

Sinds: 1.5.0.

#### current_timestamp

`current_timestamp()`: Retourneert de huidige tijdstempel aan het begin van de query-evaluatie.

Sinds: 1.5.0.

#### now

`now()`: Retourneert de huidige tijdstempel aan het begin van de query-evaluatie.

Sinds: 1.5.0.
