---
title: Array- en kaartgegevenstypen beheren met functies voor hogere volgorde
description: Leer hoe te om serie en kaartgegevenstypes met hoger-ordefuncties in de Dienst van de Vraag te beheren. Voorbeelden worden gegeven met veelvoorkomende gebruiksgevallen.
exl-id: dec4e4f6-ad6b-4482-ae8c-f10cc939a634
source-git-commit: d2bc580ba1cacdfab45bdc6356c630a63e7d0f6e
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# Array- en kaartgegevenstypen beheren met functies voor hogere volgorde

In deze handleiding leert u hoe functies met een hogere volgorde complexe gegevenstypen, zoals arrays en kaarten, kunnen verwerken. Deze functies verwijderen de noodzaak om de array te exploderen, een functie uit te voeren en het resultaat vervolgens te combineren. Hogere functies zijn vooral handig voor het analyseren of verwerken van tijdreeksen, gegevenssets en analyses, die vaak bestaan uit complexe geneste structuren, arrays, kaarten en verschillende gebruiksgevallen.

De volgende lijst met gebruiksgevallen bevat voorbeelden van functies voor array- en kaartmanipulatie in hogere volgorde.

## Transformatie gebruiken om het totaal van de prijs met n aan te passen {#adjust-price-total}

`transform(array<T>, function<T, U>): array<U>`

Het bovenstaande fragment past een functie toe op elk element van de array en retourneert een nieuwe array van getransformeerde elementen. Met name de functie `transform` neemt een array van type T en converteert elk element van type T naar type U. Vervolgens wordt een array van het type U geretourneerd. De daadwerkelijke types T en U hangen van het specifieke gebruik van de transformatiefunctie af.

`transform(array<T>, function<T, Int, U>): array<U>`

Deze arraytransformatiefunctie is vergelijkbaar met het vorige voorbeeld, maar er zijn twee argumenten voor de functie. Het tweede argument in deze functie ontvangt ook de index van het element in de array naast de transformatie.

**Voorbeeld**

In het onderstaande SQL-voorbeeld wordt dit geval geïllustreerd. De query haalt een beperkte set rijen op uit de opgegeven tabel, waarbij de array `productListItems` wordt getransformeerd door het kenmerk `priceTotal` van elk item met 73 te vermenigvuldigen. Het resultaat omvat de kolommen `_id` , `productListItems` en `price_in_inr` getransformeerd. De selectie is gebaseerd op een specifiek tijdstempelbereik.

```sql
SELECT _id,
       productListItems,
       Transform(productListItems, value -> value.priceTotal * 73) AS
       price_in_inr
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Resultaat**

De resultaten voor deze SQL zouden vergelijkbaar zijn met die hieronder worden weergegeven.

```console
 productListItems | price_in_inr
-------------------+----------------
(8376, NULL, NULL) | 611448.0
{(Burbank Hills Jeans, NULL, NULL), (Thermomax Steel, NULL, NULL), (Bruin Point Shearling Boots, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL), (Timberline Survival Knife, NULL, NULL), (Thermomax Steel, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Lost Prospector Beanie, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL)} | {0.0,0.0.0.0,0,0,0,0,0,0,0,0,0,0,0,0,0.0}
(84763,NULL, NULL) | 6187699.0
(843765, NULL, NULL) | 6.1594845E7
(199684, NULL, NULL) | 1.4576932E7

(10 rows)
```

## Het gebruik bestaat om te ontdekken of een product met een specifieke SKU bestaat {#confirm-product-exists}

`exists(array<T>, function<T, boolean>): boolean`

In het bovenstaande fragment wordt de functie `exists` toegepast op elk element van de array en wordt een booleaanse waarde geretourneerd. De booleaanse waarde geeft aan of er een of meer elementen in de array zijn die aan een opgegeven voorwaarde voldoen. In dit geval wordt bevestigd of een product met een specifieke SKU bestaat.

**Voorbeeld**

In het onderstaande SQL-voorbeeld haalt de query `productListItems` op van de `geometrixxx_999_xdm_pqs_1batch_10k_rows` -tabel en evalueert deze of een element met een SKU gelijk aan `123679` in de `productListItems` -array bestaat. Vervolgens worden de resultaten gefilterd op basis van een specifieke reeks tijdstempels en worden de uiteindelijke resultaten beperkt tot tien rijen.

```sql
SELECT productListItems
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE EXISTS( productListItems, value -> value.sku == 123679)
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')limit 10;
```

**Resultaat**

De resultaten voor deze SQL zouden vergelijkbaar zijn met die hieronder worden weergegeven.

```console
productListItems
-----------------
{(123679, NULL,NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL,NULL)}
{(123679,NULL, NULL)}

(10 rows)
```

## Filter gebruiken om producten te zoeken waarbij de SKU > 100000 {#find-specific-products}

`filter(array<T>, function<T, boolean>): array<T>`

Deze functie filtert een array met elementen op basis van een bepaalde voorwaarde die elk element als een booleaanse waarde evalueert. Vervolgens wordt een nieuwe array geretourneerd die alleen elementen bevat waar de voorwaarde een werkelijke waarde heeft geretourneerd.

**Voorbeeld**

Met de onderstaande query wordt de kolom `productListItems` geselecteerd, wordt een filter toegepast om alleen elementen met een SKU groter dan 100000 op te nemen en wordt de resultaatset beperkt tot rijen binnen een specifiek tijdstempelbereik. De gefilterde array wordt vervolgens als `_filter` in de uitvoer gealiased.

```sql
SELECT productListItems,
    Filter(productListItems, value -> value.sku > 100000) AS _filter
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**Resultaat**

De resultaten voor deze SQL zouden vergelijkbaar zijn met die hieronder worden weergegeven.

```console
productListItems | _filter
-----------------+---------
(123679, NULL, NULL) (123679, NULL, NULL)
(1346, NULL, NULL) |
(98347, NULL, NULL) |
(176015, NULL, NULL) | (176015, NULL, NULL)

(10 rows)
```

## Samenvoegen gebruiken om de SKU&#39;s van alle items in de productlijst die aan een specifieke id zijn gekoppeld, op te tellen en het resulterende totaal te verdubbelen {#sum-specific-skus-and-double-the-resulting-total}

`aggregate(array<T>, A, function<A, T, A>[, function<A, R>]): R`

Deze statistische bewerking past een binaire operator toe op een begintoestand en alle elementen in de array. Het vermindert ook veelvoudige waarden tot één enkele staat. Na deze reductie wordt de uiteindelijke status omgezet in het uiteindelijke resultaat met behulp van een afwerkingsfunctie. De afwerkingsfunctie neemt de laatste status verkregen na het toepassen van de binaire operator op alle arrayelementen en doet er iets mee om het eindresultaat te produceren.

**Voorbeeld**

In dit queryvoorbeeld wordt de maximale SKU-waarde berekend uit de array `productListItems` binnen het opgegeven tijdstempelbereik en wordt het resultaat verdubbeld. De uitvoer bevat de oorspronkelijke `productListItems` -array en de berekende `max_value` .

```sql
SELECT productListItems,
aggregate(productListItems, 0, (acc, value) ->
case
WHEN (
value.sku > acc) THEN cast(value.sku AS int)
ELSE cast(acc AS int)
END, acc -> acc * 2) AS max_value
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 50;
```

**Resultaat**

De resultaten voor deze SQL zouden vergelijkbaar zijn met die hieronder worden weergegeven.

```console
productListItems | max_value
-----------------+---------
(123679, NULL, NULL) | 247358
(1346,NULL, NULL) | 2692
(98347, NULL, NULL) | 196694
(176015, NULL, NULL) | 352030

(10 rows)
```

## ZIP_with gebruiken om een volgnummer toe te wijzen aan alle items in de productlijst {#assign-a-sequence-number}

`zip_with(array<T>, array<U>, function<T, U, R>): array<R>`

Dit fragment combineert de elementen van twee arrays tot één nieuwe array. De bewerking wordt onafhankelijk uitgevoerd op elk element van de array en genereert waardeparen. Als één array korter is, worden null-waarden toegevoegd om overeen te komen met de lengte van de langere array. Dit gebeurt voordat de functie wordt toegepast.

**Voorbeeld**

De volgende query gebruikt de functie `zip_with` om paren waarden te maken van twee arrays. Dit gebeurt door de SKU-waarden van de array `productListItems` toe te voegen aan een reeks gehele getallen, die is gegenereerd met de functie `Sequence` . Het resultaat wordt samen met de oorspronkelijke kolom `productListItems` geselecteerd en is beperkt op basis van een tijdstempelbereik.

```sql
SELECT productListItems,
zip_with(Sequence(1,5), Transform(productListItems, p -> p.sku), (x,y) -> struct(x, y)) AS zip_with
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**Resultaat**

De resultaten voor deze SQL zouden vergelijkbaar zijn met die hieronder worden weergegeven.

```console
productListItems     | zip_with
---------------------+---------
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(123679, NULL, NULL) | {(1,123679), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3, NULL),(4,NULL), (5,NULL)}
(1346,NULL, NULL)    | {(1,1346), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(98347, NULL, NULL)  | {(1,98347), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
(176015, NULL, NULL) | {(1,176015),(2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}

(10 rows)
```

## Map_from_entries gebruiken om een opeenvolgingsaantal aan elk punt in de productlijst toe te wijzen en het definitieve resultaat als kaart te verkrijgen {#assign-a-sequence-number-return-result-as-map}

`map_from_entries(array<struct<K, V>>): map<K, V>`

Dit fragment zet een array van sleutelwaardeparen om in een kaart. Het is nuttig wanneer het behandelen van zeer belangrijk-waardepaargegevens die van een meer georganiseerde en efficiënte structuur zouden kunnen profiteren.

**Voorbeeld**

De volgende vraag leidt tot paren van waarden van een opeenvolging en de productListItems serie, zet deze paren in een kaart gebruikend map_from_entries om, en selecteert dan de originele productListItems kolom samen met de pas gemaakte map_from_entries kolom. Het resultaat wordt gefilterd en beperkt op basis van het opgegeven tijdstempelbereik.

```sql
SELECT productListItems,      map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))) AS map_from_entries
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > to_timestamp('2017-11-01 00:00:00')
AND    timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**Resultaat**

De resultaten voor deze SQL zouden vergelijkbaar zijn met die hieronder worden weergegeven.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Map_form_arrays gebruiken om reeksnummers toe te wijzen aan items in de productlijst en het resultaat als een kaart te retourneren {#assign-sequence-numbers-to-items-return-the-result-as-a-map}

`map_form_arrays(array<K>, array<V>): map<K, V>`

De functie `map_form_arrays` maakt een kaart met behulp van gekoppelde waarden uit twee arrays.

>[!IMPORTANT]
>
>De toetsen mogen geen null-elementen bevatten.

**Voorbeeld**

In de onderstaande SQL-code wordt een kaart gemaakt waar de sleutels volgnummers zijn die met de functie `Sequence` zijn gegenereerd en de waarden elementen van de array `productListItems` zijn. De query selecteert de kolom `productListItems` en gebruikt de functie `Map_from_arrays` om de map te maken op basis van de gegenereerde reeks getallen en de elementen van de array. Het resultaat is beperkt tot tien rijen en gefilterd op basis van een tijdstempelbereik.

```sql
SELECT productListItems,
       Map_from_arrays(Sequence(1, Size(productListItems)), productListItems) AS
       map_from_arrays
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  Size(productListItems) > 0
       AND timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Resultaat**

De resultaten voor deze SQL zouden vergelijkbaar zijn met die hieronder worden weergegeven.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Map_concat gebruiken om twee maps samen te voegen tot één kaart {#concatenate-two-maps-into-as-single-map}

`map_concat(map<K, V>, ...): map<K, V>`

De functie `map_concat` in het bovenstaande fragment neemt meerdere maps als argumenten en retourneert een nieuwe map waarin alle sleutel-waardeparen van de invoermaps worden gecombineerd. De functie voegt meerdere toewijzingen samen tot één kaart en de resulterende kaart bevat alle sleutel-waardeparen van de invoertoewijzingen.

**Voorbeeld**

In de onderstaande SQL-code wordt een kaart gemaakt waaraan elk item in `productListItems` is gekoppeld met een volgnummer. Deze wordt vervolgens samengevoegd met een andere kaart waar toetsen in een bepaald bereik van reeksen worden gegenereerd.

```sql
SELECT productListItems,
      map_concat(           
         map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))),
         map_from_arrays(sequence(size(productListItems) + 1, size(productListItems) + size(productListItems)), productListItems) )
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE size(productListItems) > 0
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**Resultaat**

De resultaten voor deze SQL zouden vergelijkbaar zijn met die hieronder worden weergegeven.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)",2 -> "(123679, NULL, NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)",2 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)",2 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)",2 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)",2 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)",2 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)",2 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)",2 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Element_at gebruiken om een waarde op te halen die overeenkomt met &#39;AID&#39; in de identiteitslijst voor verdere berekeningen {#retrieve-a-corresponding-value}

`element_at(array<T>, Int): T / element_at(map<K, V>, K): V`

Voor arrays retourneert het fragment het element bij een opgegeven (op 1 gebaseerde) index of de waarde die aan een sleutel in een kaart is gekoppeld. Als de index &lt; 0 is, heeft deze toegang tot elementen van de laatste naar de eerste en retourneert deze null als de index de lengte van de array overschrijdt.

Voor kaarten, keert het of een waarde voor de bepaalde sleutel terug of ongeldig als de sleutel niet in de kaart bevat is.

**Voorbeeld**

De query selecteert de `identitymap` kolom in de tabel `geometrixxx_999_xdm_pqs_1batch_10k_rows` en extraheert de waarde die aan de sleutel `AAID` voor elke rij is gekoppeld. De resultaten zijn beperkt tot rijen die binnen het opgegeven tijdstempelbereik vallen, en de query beperkt de uitvoer tot tien rijen.

```sql
SELECT identitymap,
              Element_at(identitymap, 'AAID')
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**Resultaat**

De resultaten voor deze SQL zouden vergelijkbaar zijn met die hieronder worden weergegeven.

```console
                                                                  identitymap                                            |  element_at(identitymap, AAID) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            | (3617FBB942466D79-5433F727AD6A0AD, false) 
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] | (533F56A682C059B1-396437F68879F61D, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             | (6A60527B9D66CCB9-29638A632B45E9, false) 
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           | (64FB4DC317E21B59-2A23602D234647E7, false) 
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           | (2E70E8CF6DB1DE86-270E55BBBA58B9C1, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           | (1CFB3297C3146F2F-28D6902A610BA3B1, false) 
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           | (533F56A682C059B1-396437F68879F61D, false) 
(10 rows)
```

## Kardinaliteit gebruiken om het aantal identiteiten in het identiteitsoverzicht te vinden {#find-the-number-of-identities-in-the-identity-map}

`cardinality(array<T>): Int / cardinality(map<K, V>): Int`

Dit fragment retourneert de grootte van een bepaalde array of kaart en biedt een alias. De waarde retourneert -1 als de waarde null is.

**Voorbeeld**

Met de onderstaande query wordt de kolom `identitymap` opgehaald en de functie `Cardinality` berekent het aantal elementen in elke kaart in de `identitymap` . De resultaten zijn beperkt tot tien rijen en worden gefilterd op basis van een opgegeven tijdstempelbereik.

```sql
SELECT identitymap,
       Cardinality(identitymap)
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Resultaat**

De resultaten voor deze SQL zouden vergelijkbaar zijn met die hieronder worden weergegeven.

```console
                                                                  identitymap                                            |  size(identitymap) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            |      2  
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             |      2  
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           |      2  
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           |      2  
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           |      2  
(10 rows)
```

## Gebruik array_different om de verschillende elementen in productListItems te zoeken {#find-distinct-elements}

`array_distinct(array<T>): array<T>`

Het bovenstaande fragment verwijdert dubbele waarden uit de opgegeven array.

**Voorbeeld**

Met de onderstaande query wordt de kolom `productListItems` geselecteerd, worden dubbele items uit de arrays verwijderd en wordt de uitvoer beperkt tot tien rijen op basis van een opgegeven tijdstempelbereik.

```sql
SELECT productListItems,
              Array_distinct(productListItems)
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**Resultaat**

De resultaten voor deze SQL zouden vergelijkbaar zijn met die hieronder worden weergegeven.

```console
productListItems     | array_distinct(productListItems)
---------------------+---------------------------------
                     |
(123679, NULL, NULL) | (123679, NULL, NULL)
                     |
                     |
(1346,NULL, NULL)    | (1346,NULL, NULL)
                     |
(98347, NULL, NULL)  | (98347, NULL, NULL)
                     |
(176015, NULL, NULL) | (176015, NULL, NULL)
                     |

(10 rows)
```

### Aanvullende functies met een hogere volgorde {#additional-higher-order-functions}

De volgende voorbeelden van hoger-ordefuncties worden verklaard als deel van terugwinnen gelijkaardig archiefgebruiksgeval. Een voorbeeld en uitleg van het gebruik van elke functie worden gegeven in de desbetreffende sectie van dat document.

Het [`transform` functievoorbeeld &#x200B;](../use-cases/retrieve-similar-records.md#length-adjustment) behandelt de verdeling van een productlijst.

Het [`filter` functievoorbeeld &#x200B;](../use-cases/retrieve-similar-records.md#filter-results) toont een verfijnde en nauwkeurige extractie van relevante informatie van tekstgegevens aan.

De [`reduce` functie &#x200B;](../use-cases/retrieve-similar-records.md#higher-order-function-solutions) verstrekt een manier om cumulatieve waarden of aggregaten af te leiden, die in diverse analytische en planningsprocessen kunnen centraal zijn.
