---
keywords: Experience Platform;thuis;populaire onderwerpen;
title: Handleiding voor het oplossen van problemen met Data Prep
topic-legacy: troubleshooting
description: Dit document geeft antwoorden op veelgestelde vragen over Adobe Experience Platform Data Prep.
source-git-commit: e96263847f53ea2c884c273fd7986855d4c478c1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# [!DNL Data Prep] gids voor problemen

Dit document geeft antwoorden op veelgestelde vragen over Adobe Experience Platform [!DNL Data Prep]en een gids voor probleemoplossing voor algemene fouten. Voor vragen en het oplossen van problemeninformatie betreffende Platform APIs in het algemeen, zie [Handleiding voor problemen met de Adobe Experience Platform API](../landing/troubleshooting.md).

## Veelgestelde vragen

Hieronder volgt een lijst met veelgestelde vragen over [!DNL Data Prep] en hun antwoorden.

### Hoe worden transformatiefouten opgelost?

[!DNL Data Prep] lokaliseert alle transformatiefouten aan de kolom waarin zij voorkwamen. Dientengevolge, wordt die kolom nietig verklaard en de rest van de rij zal verder worden verwerkt. Deze transformatieproblemen zijn vastgelegd als **Waarschuwingen**. U wordt aangeraden de waarschuwingen regelmatig te controleren en de transformatielogica aan te passen om rekening te houden met de transformatieproblemen. Dit zal de kwaliteit van de gegevens verhogen die in Experience Platform worden opgenomen.

Als de kolommen gemarkeerd zijn als **Vereist** worden geannuleerd vanwege transformatieproblemen, wordt de rij niet ingevoegd. Wanneer gedeeltelijke gegevensopname wordt toegelaten, kunt u de drempel van dergelijke verwerpingen plaatsen alvorens de volledige stroom ontbreekt. Als het ongeldig gemaakte attribuut geen bevestigingen van het schemaniveau beïnvloedde, zal de rij blijven worden opgenomen.

Alle rijen die ongeldig zijn, zelfs zonder transformatiefouten, worden eveneens afgewezen. Een gegevensinvoerstroom kan bijvoorbeeld een doorvoertoewijzing (geen transformatielogica) naar een vereist veld hebben en er is geen binnenkomende waarde voor dat kenmerk. Deze rij wordt afgewezen.