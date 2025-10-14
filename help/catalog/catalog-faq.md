---
keywords: catalogusservice; vragen; vaak gestelde vragen; vk; datasets faq
title: Veelgestelde vragen
description: Antwoorden op de vaakst gestelde vragen over de Dienst en datasets van de Catalogus van Adobe Experience Platform.
exl-id: 70d2a352-75bd-4bbc-98e6-aeea16306f63
source-git-commit: 38f63f1fc985601c53925a529e603f47dc7fb58b
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# Veelgestelde vragen {#faq}

Dit document geeft antwoorden op veelgestelde vragen over de Catalogusservice en gegevenssets van Adobe Experience Platform. Voor vragen en het oplossen van problemen met betrekking tot andere diensten van Experience Platform, met inbegrip van kwesties die over alle Experience Platform APIs worden ontmoet, gelieve te verwijzen naar de [&#x200B; het oplossen van problemengids van Experience Platform &#x200B;](../landing/troubleshooting.md).

## Beleid en regels voor bewaring {#retention-policies-and-rules}

### Op welke soorten datasets kan ik de regels van het behoudbeleid toepassen?

+++Antwoord

U kunt het beleid van het ophoudbehoud op datasets plaatsen die gebruikend de klasse van ExperienceEvent XDM worden gecreeerd. Voor de Dienst van het Profiel, kan het behoudbeleid slechts op datasets worden toegepast ExperienceEvent nadat zij voor Profiel zijn toegelaten.

+++

### Kan ik verschillende behoudsbeleid voor de dienst van het gegevensmeer en van het Profiel plaatsen?

+++Antwoord

>[!NOTE]
>
>De bewaartermijn voor de Dienst van het Profiel kan slechts om de 30 dagen worden bijgewerkt.

Ja, kunt u verschillende bewaarbeleid voor de gegevens toepassen meer en de Dienst van het Profiel.

+++

## Uitvoering en timing van taken behouden {#retention-job-execution-and-timing}

### Hoe snel zal de datasetbehoudbaan gegevens van de diensten van het gegevensmeer schrappen?

+++Antwoord

Verlopen van gegevenssets worden wekelijks geëvalueerd en verwerkt, waarbij alle verlopen records worden verwijderd. Een gebeurtenis wordt als verlopen beschouwd als deze langer dan 30 dagen (innamedatum > 30 dagen) in Experience Platform is ingeslikt en de datum van de gebeurtenis de gedefinieerde retentieperiode overschrijdt.

+++

### Hoe snel zal de datasetbewaarbaan gegevens van de diensten van het Profiel schrappen?

+++Antwoord

Nadat een retentiebeleid is ingesteld, worden bestaande gebeurtenissen direct uit Experience Platform verwijderd als de tijdstempel van de gebeurtenis de retentieperiode overschrijdt. Nieuwe gebeurtenissen worden verwijderd als de tijdstempel langer is dan de retentieperiode.

Als u bijvoorbeeld op 15 mei een vervalbeleid van 30 dagen toepast, gebeurt het volgende:

- Nieuwe gebeurtenissen krijgen een vervaldatum van 30 dagen wanneer ze worden opgenomen.
- Bestaande gebeurtenissen met een tijdstempel die ouder is dan 15 april, worden onmiddellijk verwijderd.
- Bestaande gebeurtenissen met een tijdstempel na 15 april verlopen 30 dagen na hun tijdstempel. Een gebeurtenis vanaf 18 april wordt bijvoorbeeld op 18 mei verwijderd.

+++

## Gebruik van gegevensset en controle

### Hoe kan ik mijn huidige gegevenssetgebruik controleren?

+++Antwoord

U kunt de nieuwste opslaggrootte op gegevensniveau in een datumpeer en profiel bekijken als afzonderlijke maatstaven op de inventarispagina van [!UICONTROL Datasets] . U kunt de kolommen ook sorteren om de grootste datasets te identificeren en ervoor te zorgen dat het behoudbeleid wordt toegepast. Het gebruik op het niveau van de zandbak is beschikbaar in het dashboard van het Gebruik van de Vergunning. Gelieve te verwijzen naar de [&#x200B; documentatie van het Gebruik van de Vergunning &#x200B;](../dashboards/guides/license-usage.md) voor details.

+++

### Hoe kan ik controleren of de functie voor het bewaren van gegevens is gelukt?

+++Antwoord

U kunt timestamp van de laatste baan van het gegevensbehoud in de [&#x200B; configuratie UI van het het behoud van de Dataset &#x200B;](./datasets/user-guide.md#data-retention-policy) en op de [!UICONTROL Datasets] inventarispagina controleren. Rapporten voor historisch gegevenssetgebruik zijn momenteel niet beschikbaar maar zijn gepland voor toekomstige versies.

+++

## Gegevensherstel {#data-recovery}

### Kan ik verwijderde gegevens herstellen?

+++Antwoord

Neen, zodra het bewaarbeleid wordt toegepast, worden om het even welke gegevens ouder dan de bewaarperiode permanent geschrapt en kunnen niet worden teruggekregen.

+++
