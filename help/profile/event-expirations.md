---
keywords: Experience Platform;home;populaire onderwerpen;dataset;Dataset;tijd om te leven;ttl;tijd-aan-levende;
solution: Experience Platform
title: Verlopen van gebeurtenissen ervaren
description: Dit document biedt algemene richtlijnen voor het configureren van vervaltijden voor afzonderlijke Experience Events in een Adobe Experience Platform-gegevensset.
exl-id: a91f2cd2-3a5d-42e6-81c3-0ec5bc644f5f
source-git-commit: e85122a0f6acf2f3cb3960d89faa70220692ac23
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---

# Verlopen van gebeurtenissen beleven

In Adobe Experience Platform, kunt u vervaltijden voor alle Gebeurtenissen van de Ervaring vormen die in een dataset worden opgenomen die voor [&#x200B; in real time wordt toegelaten Profiel van de Klant &#x200B;](./home.md). Hiermee kunt u automatisch gegevens verwijderen uit het profielarchief die niet meer geldig of nuttig zijn voor uw gebruiksgevallen.

Leren hoe te om uw Verlopen van de Gebeurtenis van de Ervaring in uw datasets te beheren, lees de [&#x200B; gids UI van de dataset &#x200B;](../catalog/datasets/user-guide.md#data-retention-policy).

![&#x200B; een dialoog die het gegevenssetbehoud evenals de beschikbare montages toont.](./images/event-expirations/set-data-retention-dialog.png) {width="500" zoomable="yes"}

>[!IMPORTANT]
>
>Verlopen van de Gebeurtenis van de ervaring moeten niet met datasettermijnen worden verward, die de volledige dataset schrappen nadat de vervaldatum wordt bereikt. Deze worden manueel gevormd door [&#x200B; Hygiene van Gegevens van Adobe Experience Platform &#x200B;](../hygiene/home.md).

## Geautomatiseerd vervalproces

Nadat de Verlopen van de Gebeurtenis van de Ervaring op een profiel-Toegelaten dataset zijn toegelaten, past Experience Platform automatisch de vervalwaarden voor elke gevangen gebeurtenis in een proces in twee stappen toe:

1. Voor alle nieuwe gegevens die in de gegevensset worden opgenomen, wordt de vervalwaarde toegepast op de ingangstijd op basis van de tijdstempel van de gebeurtenis.
1. Alle bestaande gegevens in de dataset hebben de vervalwaarde met terugwerkende kracht wordt toegepast als eenmalig backfill systeembaan. Zodra de vervalwaarde op de dataset is geplaatst, zullen de gebeurtenissen die ouder zijn dan de vervalwaarde onmiddellijk worden gelaten vallen zodra de systeembaan loopt. Alle andere gebeurtenissen worden geannuleerd zodra ze hun vervalwaarden uit de tijdstempel van de gebeurtenis bereiken. Als alle Experience Events zijn verwijderd en het profiel geen profielkenmerken meer heeft, bestaat het profiel niet meer.

>[!WARNING]
>
>Zodra toegepast, wordt om het even welke gegevens die ouder zijn dan het aantal dagen dat door de vervalwaarde wordt toegewezen permanent geschrapt **&#x200B;**&#x200B;en kan niet worden hersteld.

Als u bijvoorbeeld op 15 mei een vervalwaarde van 30 dagen hebt toegepast, worden de volgende stappen uitgevoerd:

1. Alle nieuwe gebeurtenissen krijgen een vervalwaarde van 30 dagen toegepast aangezien zij worden opgenomen.
1. Alle bestaande gebeurtenissen met een tijdstempel die ouder is dan 15 april worden onmiddellijk verwijderd met de systeemtaak.
1. Alle bestaande gebeurtenissen met een tijdstempel die nieuwer is dan 15 april, hebben een vervalwaarde 30 dagen na hun tijdstempel voor de gebeurtenis. Als een gebeurtenis dus een tijdstempel van 18 april heeft, wordt deze 30 dagen na de datum van die tijdstempel verwijderd, hetgeen 18 mei zou zijn.

## Effecten op segmentatie

U moet ervoor zorgen dat de raadplegingsvensters voor uw publiek binnen de vervalgrenzen van hun afhankelijke datasets zijn om resultaten nauwkeurig te houden. Als u bijvoorbeeld een vervalwaarde van 30 dagen toepast en een publiek hebt dat probeert gegevens van maximaal 45 dagen geleden te bekijken, is het resulterende publiek waarschijnlijk onjuist.

Daarom zou u de zelfde waarde van de Vervaltijd van de Gebeurtenis van de Ervaring voor alle datasets, indien mogelijk, moeten houden om het effect van verschillende vervalwaarden over verschillende datasets in uw segmenteringslogica te vermijden.

## Veelgestelde vragen {#faq}

In de volgende sectie worden vaak gestelde vragen over het verlopen van Experience Event-gegevens weergegeven:

### Wat is de minimale duur waarvoor ik een gegevensvervaldatum van de Gebeurtenis van de Ervaring kan plaatsen?

De minimumduur voor een de gegevensvervaldatum van de Gebeurtenis van de Ervaring is **één dag**.

### Hoe vervalt de geldigheidstermijn van de gegevens van de Gebeurtenis van de gegevensvervaldatum van het Pseudoniem Profiel?

De de gegevensvervaldatum van de Ervaring van de Gebeurtenisgegevens en de gegevensvervaldatum van het Pseudoniem Profiel zijn complementaire eigenschappen.

#### Korreligheid

De gegevensvervaldatum van de Gebeurtenis van de ervaring werkt op het niveau van de a **dataset**. Dientengevolge, kan elke dataset een verschillende het aflopen van gegevens hebben plaatsen.

De pseudoniem gegevens van het Profiel vervalsen werken op a **zandbak** niveau. Als gevolg hiervan is het verlopen van de gegevens van invloed op alle profielen in de sandbox.

#### Identiteitstypen

De gegevensvervaldatum van de Gebeurtenis van de ervaring verwijdert gebeurtenissen **slechts** die op timestamp van het gebeurtenisverslag wordt gebaseerd. De inbegrepen identiteitsnamespaces zijn **genegeerd** voor vervaldoeleinden.

De pseudoniem gegevens van het Profiel verlopen **slechts** overweegt profielen die identiteitsgrafieken hebben die identiteitsnamespaces bevatten die door de klant, zoals `ECID`, `AAID`, of andere soorten koekjes werden geselecteerd. Als het profiel **om het even welke** extra identiteitsnamespace bevat die **niet** in de geselecteerde lijst van de klant was, zal het profiel **&#x200B;**&#x200B;niet worden geschrapt.

#### Verwijderde items

De gegevensvervaldatum van de Gebeurtenis van de ervaring **slechts** verwijdert gebeurtenissen en **verwijdert** geen gegevens van de profielklasse. De gegevens van de profielklasse worden slechts verwijderd wanneer alle gegevens over **alle** datasets worden verwijderd en er **geen** dossiers van de profielklasse blijven voor het profiel.

De pseudoniem gegevensvervaldatum van het Profiel verwijdert **zowel** gebeurtenis als profielverslagen. Hierdoor worden ook de profielklassegegevens verwijderd.

### Hoe kan de gegevensvervaldatum van het Pseudoniem Profiel samen met de gegevensvervaldatum van de Gebeurtenis van de Ervaring worden gebruikt?

De vervaldatum van Pseudoniem Profielgegevens en Experience Event-gegevens kunnen worden gebruikt om elkaar aan te vullen.

U zou **altijd** de gegevensvervaldatum van de Gebeurtenis van de opstellingsErvaring in uw datasets, die op uw behoeften worden gebaseerd om gegevens over uw bekende klanten te behouden. Als de geldigheids-gebeurtenisgegevensvervaldatum is ingesteld, kunt u de gegevensvervaldatum van het Pseudoniem-profiel gebruiken om automatisch Pseudoniem-profielen te verwijderen. Doorgaans is de vervalperiode van de gegevens voor Pseudoniem Profielen korter dan de vervalperiode van de gegevens voor Experience Events.

In een typisch geval kunt u de gegevensvervaldatum van de Experience-gebeurtenis instellen op basis van de waarden van uw bekende gebruikersgegevens en u kunt de gegevensvervaldatum van het Pseudoniem-profiel instellen op een veel kortere duur om de invloed van Pseudoniem-profielen op de naleving van de Experience Platform-licentie te beperken.
