---
keywords: Experience Platform;huis;populaire onderwerpen;dataset;Dataset;tijd om te leven;ttl;tijd-aan-levende;
solution: Experience Platform
title: Verlopen van gebeurtenissen ervaren
description: Dit document biedt algemene richtlijnen voor het configureren van vervaltijden voor afzonderlijke Experience Events in een Adobe Experience Platform-gegevensset.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---

# Verlopen van gebeurtenissen beleven

In Adobe Experience Platform, kunt u vervaltijden voor alle Gebeurtenissen van de Ervaring vormen die in een dataset worden opgenomen die voor wordt toegelaten [Klantprofiel in realtime](./home.md). Hiermee kunt u automatisch gegevens uit het datumpomeer en de profielopslag verwijderen die niet meer geldig of nuttig zijn voor uw gebruiksgevallen.

Verlopen van ervaringsgebeurtenissen kunnen niet worden geconfigureerd via de gebruikersinterface of API&#39;s van het Platform. In plaats daarvan, moet u steun contacteren om de Verlopen van de Gebeurtenis van de Ervaring op uw vereiste datasets toe te laten.

>[!IMPORTANT]
>
>Verlopen van de Gebeurtenis van de ervaring moeten niet met datasettermijnen worden verward, die de volledige dataset schrappen nadat de vervaldatum wordt bereikt. Deze worden manueel gevormd door [Adobe Experience Platform Data Hygiene](../hygiene/home.md).

## Geautomatiseerd vervalproces

Nadat de Verlopen van de Gebeurtenis van de Ervaring op een profiel-Toegelaten dataset zijn toegelaten, past het Platform automatisch de vervalwaarden voor elke gevangen gebeurtenis in een proces in twee stappen toe:

1. Voor alle nieuwe gegevens die in de gegevensset worden opgenomen, wordt de vervalwaarde toegepast tijdens de opname.
1. Alle bestaande gegevens in de dataset hebben de vervalwaarde met terugwerkende kracht wordt toegepast als eenmalig backfill systeembaan. Zodra de vervalwaarde op de dataset is geplaatst, zullen de gebeurtenissen die ouder zijn dan de vervalwaarde onmiddellijk worden gelaten vallen zodra de systeembaan loopt. Alle andere gebeurtenissen worden geannuleerd zodra ze hun vervalwaarden uit de tijdstempel van de gebeurtenis bereiken.

>[!WARNING]
>
>Na toepassing worden alle gegevens die ouder zijn dan het aantal dagen dat door de vervalwaarde is toegewezen, gebruikt **permanent verwijderd** en kan niet worden hersteld.

Als u bijvoorbeeld op 15 mei een vervalwaarde van 30 dagen hebt toegepast, worden de volgende stappen uitgevoerd:

1. Alle nieuwe gebeurtenissen krijgen een vervalwaarde van 30 dagen toegepast aangezien zij worden opgenomen.
1. Alle bestaande gebeurtenissen met een tijdstempel die ouder is dan 15 april worden onmiddellijk verwijderd met de systeemtaak.
1. Alle bestaande gebeurtenissen met een tijdstempel die nieuwer is dan 15 april, hebben een vervalwaarde 30 dagen na hun tijdstempel voor de gebeurtenis. Als een gebeurtenis dus een tijdstempel van 18 april heeft, wordt deze 30 dagen na de datum van die tijdstempel verwijderd, hetgeen 18 mei zou zijn.

## Effecten op segmentatie

U moet ervoor zorgen dat de raadplegingsvensters voor uw segmenten binnen de vervalgrenzen van hun afhankelijke datasets zijn om resultaten nauwkeurig te houden. Als u bijvoorbeeld een vervalwaarde van 30 dagen toepast en een segment hebt dat probeert gegevens van maximaal 45 dagen geleden weer te geven, is het resulterende publiek waarschijnlijk onjuist.

Daarom zou u de zelfde waarde van de Vervaltijd van de Gebeurtenis van de Ervaring voor alle datasets, indien mogelijk, moeten houden om het effect van verschillende vervalwaarden over verschillende datasets in uw segmenteringslogica te vermijden.
