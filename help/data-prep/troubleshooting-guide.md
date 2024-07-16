---
keywords: Experience Platform;thuis;populaire onderwerpen;
title: Handleiding voor het oplossen van problemen met Data Prep
description: Dit document geeft antwoorden op veelgestelde vragen over Adobe Experience Platform Data Prep.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# [!DNL Data Prep] gids voor probleemoplossing

Dit document bevat antwoorden op veelgestelde vragen over Adobe Experience Platform [!DNL Data Prep] en een gids voor probleemoplossing voor algemene fouten. Voor vragen en het oplossen van problemeninformatie betreffende Platform APIs in het algemeen, zie de [ het oplossen van problemengids van Adobe Experience Platform API ](../landing/troubleshooting.md).

## Veelgestelde vragen

Hieronder volgt een lijst met veelgestelde vragen over [!DNL Data Prep] en de bijbehorende antwoorden.

### Hoe worden transformatiefouten opgelost?

[!DNL Data Prep] lokaliseert alle transformatiefouten naar de kolom waarin zij voorkwamen. Dientengevolge, wordt die kolom nietig verklaard en de rest van de rij zal verder worden verwerkt. Deze transformatiekwesties worden geregistreerd als **Waarschuwingen**. U wordt aangeraden de waarschuwingen regelmatig te controleren en de transformatielogica aan te passen om rekening te houden met de transformatieproblemen. Dit zal de kwaliteit van de gegevens verhogen die in Experience Platform worden opgenomen.

Als de kolommen die als **worden gemerkt Vereist** wegens transformatiekwesties ongeldig worden gemaakt, dan zal de rij niet worden opgenomen. Wanneer gedeeltelijke gegevensopname wordt toegelaten, kunt u de drempel van dergelijke verwerpingen plaatsen alvorens de volledige stroom ontbreekt. Als het ongeldig gemaakte attribuut geen bevestigingen van het schemaniveau beïnvloedde, zal de rij blijven worden opgenomen.

Alle rijen die ongeldig zijn, zelfs zonder transformatiefouten, worden eveneens afgewezen. Een gegevensinvoerstroom kan bijvoorbeeld een doorvoertoewijzing (geen transformatielogica) naar een vereist veld hebben en er is geen binnenkomende waarde voor dat kenmerk. Deze rij wordt afgewezen.

### Hoe kan ik aan speciale tekens in een veld ontsnappen?

Met `${...}` kunt u speciale tekens in een veld verwijderen. JSON-bestanden die velden met een punt (`.`) bevatten, worden echter niet ondersteund door dit mechanisme. Wanneer het in wisselwerking staan met hiërarchieën, als een kindattribuut een periode (`.`) heeft, moet u backslash (`\`) gebruiken om speciale karakters te ontsnappen. `address` is bijvoorbeeld een object dat het kenmerk `street.name` bevat. U kunt dit vervolgens `address.street\.name` in plaats van `address.street.name` noemen.

### Wat is de maximumlengte van berekende velden?

Berekende velden mogen maximaal 4096 tekens lang zijn.