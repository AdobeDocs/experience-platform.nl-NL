---
description: Leer hoe het Experience Platform verschillende soorten fouten behandelt die door het stromen bestemmingen zijn teruggekeerd en hoe het opnieuw probeert om gegevens naar het bestemmingsplatform te verzenden.
title: Het beperken van snelheid en herprobeert beleid voor het stromen bestemmingen die met Destination SDK worden gebouwd
source-git-commit: ec50608f6454dd619c30b6337f454561844183ba
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# Het beperken van snelheid en herprobeert beleid voor het stromen bestemmingen die met Destination SDK worden gebouwd

## Overzicht {#overview}

De partner-gebouwde bestemmingen kunnen diverse fouten terugkeren en verschillend tarief beperkend beleid hebben. Deze pagina verklaart hoe het Experience Platform verschillende soorten fouten behandelt die door het stromen bestemmingen zijn teruggekeerd.

Wanneer het vormen van een bestemming die Destination SDK gebruikt, kunt u tussen twee samenvoegingstypes selecteren - [beste inspanningsaggregatie](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation) en [configureerbare samenvoeging](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation). Afhankelijk van het aggregatietype dat u selecteert, leest u hieronder hoe Experience Platform fouten en tariefbeperkingen behandelt.

## Beste inspanningsaggregatie {#best-effort-aggregation}

Voor om het even welke vraag van HTTP die aan uw bestemming wordt gemaakt die ontbreekt, probeert het Experience Platform om de vraag opnieuw één keer onmiddellijk na de eerste vraag te maken. Als de vraag nog op de tweede poging ontbreekt, laat het Experience Platform de vraag vallen en niet het een derde keer opnieuw proberen.

## Configureerbare samenvoeging {#configurable-aggregation}

In het geval van bestemmingsplatforms opstelling met configureerbare samenvoeging, maakt het Experience Platform onderscheid tussen het foutentype dat door uw platform is teruggekeerd:

* Fouten waarbij het Experience Platform de gegevens opnieuw naar het platform probeert te verzenden:
   * HTTP-responscodes 420 en 429
   * HTTP-responscodes groter dan 500
* Fouten bij Experience Platform *niet* probeer de gegevens opnieuw naar uw platform te verzenden: alle andere die door uw platform worden teruggegeven

### beschreven procedure voor opnieuw proberen {#retry-approach}

De benadering van het Experience Platform voor configureerbare samenvoeging wordt hieronder beschreven. In dit voorbeeld wordt ervan uitgegaan dat Experience Platform gegevens verzendt naar een doelplatform dat 429 foutcodes begint te retourneren als het meer dan 50 k verzoeken per minuut ontvangt:

* Minuut 1: Experience Platform voegt 40.000 batches samen met profielen voor verzending naar uw doelplatform. Experience Platform maakt 40.000 HTTP-aanvragen en alle aanvragen zijn succesvol.
* Minuut 2: Experience Platform voegt 70.000 batches samen met profielen voor verzending naar uw doelplatform. Experience Platform maakt 70.000 HTTP-aanvragen en 50.000 aanvragen zijn geslaagd. De andere 20k ontvangt een tarief beperkende fout van uw eindpunt en zal over 30 minuten worden opnieuw gebracht.
* Minuut 3: Experience Platform voegt 30.000 batches samen met profielen voor verzending naar het doelplatform. Experience Platform maakt 30.000 HTTP-aanvragen en alle aanvragen zijn succesvol.
* ...
* ...
* Minuut 32: Experience Platform probeert de 20k partijen te verzenden die op minuut 2 hebben gefaald. Alle vraag is succesvol.

## Volgende stappen {#next-steps}

U weet nu hoe het Experience Platform fouten en tarief het beperken van bestemmingsplatforms, afhankelijk van het samenvoegingsbeleid behandelt u selecteerde toen u uw het stromen bestemming vormde. Hierna kunt u de volgende documentatie bekijken:

* [De doelconfiguratie testen](/help/destinations/destination-sdk/test-destination.md)
* [Ter controle een bestemming verzenden die is geschreven in Destination SDK](/help/destinations/destination-sdk/submit-destination.md)
