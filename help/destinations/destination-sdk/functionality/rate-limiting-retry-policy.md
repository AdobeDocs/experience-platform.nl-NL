---
description: Leer hoe Experience Platform verschillende soorten fouten behandelt die door het stromen bestemmingen zijn teruggekeerd en hoe het opnieuw probeert om gegevens naar het bestemmingsplatform te verzenden.
title: Het beperken van en herprobeert beleid van het tarief voor het stromen bestemmingen die met Destination SDK worden gebouwd
exl-id: aad10039-9957-4e9e-a0b7-7bf65eb3eaa9
source-git-commit: 75bee8fde648101335df7a66eae1907b267b4eb6
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Het beperken van en herprobeert beleid van het tarief voor het stromen bestemmingen die met Destination SDK worden gebouwd

De partner-gebouwde bestemmingen kunnen diverse fouten terugkeren en verschillend tarief beperkend beleid hebben. Op deze pagina wordt uitgelegd hoe Experience Platform omgaat met verschillende soorten fouten die worden geretourneerd door streamingdoelen.

Wanneer het vormen van een bestemming die Destination SDK gebruikt, kunt u tussen twee samenvoegingstypes selecteren - [&#x200B; beste inspanningssamenvoeging &#x200B;](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) en [&#x200B; configureerbare samenvoeging &#x200B;](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation). Afhankelijk van het aggregatietype dat u selecteert, leest u hieronder hoe Experience Platform fouten en tariefbeperkingen verwerkt.

## Beste inspanningsaggregatie {#best-effort-aggregation}

Experience Platform herprobeert vraag die de volgende de reactiecodes van HTTP terugkeert: **403, 408, 409, 429, 500, 502, 503, 504**. Twee pogingen worden uitgevoerd met de volgende intervallen:

* Eerste poging opnieuw proberen: na 15 seconden
* Tweede poging opnieuw: na 30 seconden

Experience Platform probeert ** geen vraag opnieuw die andere de reactiecodes van HTTP, zoals 400 terugkeert (Onjuist Verzoek). Als de aanroep nog steeds mislukt na beide pogingen om het opnieuw uit te voeren, laat Experience Platform de activering vallen en wordt deze niet opnieuw uitgevoerd.

Neem contact op met de Klantenondersteuning om een ander beleid voor het opnieuw proberen van specifieke gegevensstromen aan te vragen.

## Configureerbare samenvoeging {#configurable-aggregation}

In het geval van bestemmingsplatforms opstelling met configureerbare samenvoeging, maakt Experience Platform onderscheid tussen het foutentype dat door uw platform is teruggekeerd:

* Fouten waarbij Experience Platform opnieuw probeert de gegevens naar uw platform te verzenden:
   * HTTP-responscodes 420 en 429
   * HTTP-responscodes groter dan 500
* Fouten waar Experience Platform *niet* opnieuw probeert om de gegevens naar uw platform te verzenden: alle andere die door uw platform zijn teruggekeerd

### beschreven procedure voor opnieuw proberen {#retry-approach}

De Experience Platform-benadering voor configureerbare aggregatie wordt hieronder beschreven. In dit voorbeeld wordt ervan uitgegaan dat Experience Platform gegevens verzendt naar een doelplatform dat 429 foutcodes begint te retourneren wanneer het meer dan 50 k verzoeken per minuut ontvangt:

* Minuut 1: Experience Platform aggregeert 40.000 batches met profielen voor verzending naar uw doelplatform. Experience Platform maakt 40.000 HTTP-aanvragen en alles is geslaagd.
* Minuut 2: Experience Platform aggregeert 70.000 batches met profielen voor verzending naar uw doelplatform. Experience Platform doet 70.000 HTTP-aanvragen en 50.000 is geslaagd. De andere 20k ontvangt een tarief beperkende fout van uw eindpunt en zal over 30 minuten worden opnieuw gebracht.
* Minuut 3: Experience Platform voegt 30.000 batches samen met profielen die naar uw doelplatform worden verzonden. Experience Platform maakt 30.000 HTTP-aanvragen en alles is geslaagd.
* ...
* ...
* Minuut 32: Experience Platform probeert de 20k batches te verzenden die op minuut 2 zijn mislukt. Alle vraag is succesvol.

## Volgende stappen {#next-steps}

U weet nu hoe Experience Platform fouten en tariefbeperkingen vanaf doelplatforms verwerkt, afhankelijk van het samenvoegingsbeleid dat u hebt geselecteerd toen u uw streamingbestemming configureerde. Hierna kunt u de volgende documentatie bekijken:

* [De doelconfiguratie testen](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [Ter controle verzenden naar een bestemming die is geschreven in Destination SDK](../guides/submit-destination.md)
