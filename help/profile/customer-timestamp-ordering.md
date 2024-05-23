---
title: Volgorde tijdstempel van klant
description: Leer hoe u tijdstempelvolgorde van klanten toevoegt aan uw gegevenssets om consistentie in uw profielgegevens te verzekeren.
badgePrivateBeta: label="Private Bèta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c5789b872be49c3bd4a1ca61a2d44392ebd4a746
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Tijdstempel van klant bestellen

In Adobe Experience Platform wordt de gegevensvolgorde niet automatisch gegarandeerd wanneer gegevens via streaming worden ingevoerd in de profielopslag. Met de tijdstempelvolgorde van de klant kunt u garanderen dat het laatste bericht, volgens de opgegeven tijdstempel van de klant, behouden blijft in de profielopslag. Hierdoor kunnen uw profielgegevens consistent zijn en blijven uw profielgegevens synchroon met uw bronsystemen.

Als u tijdstempelbestelling van klanten wilt inschakelen, moet u de opdracht `lastUpdatedDate` in het veld [Gegevenstype Kenmerken externe bronsysteemcontrole](../xdm/data-types/external-source-system-audit-attributes.md) en neem contact op met de technische accountmanager van de Adobe of de klantenservice van de Adobe met uw sandbox- en datasetgegevens.

## Restricties

Tijdens deze persoonlijke bètaversie zijn de volgende beperkingen van toepassing wanneer u tijdstempelbestellingen van klanten gebruikt:

- U kunt de tijdstempelvolgorde van klanten alleen gebruiken met **profielkenmerken** ingesloten met **streaming opname**.
- U kunt de tijdstempelvolgorde van de klant alleen gebruiken op **niet-productie** sandboxen.
- U kunt de tijdstempelvolgorde van klanten alleen toepassen op **5** datasets per sandbox.
- De `lastUpdatedDate` moet in het veld [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) gebruiken.
- Alle rijen met gegevens die worden ingevoerd **moet** bevatten `lastUpdatedDate` veld. Als dit veld ontbreekt of een onjuiste indeling heeft, mislukt de opname.
- Om het even welke dataset die voor klant timestamp het opdracht geven wordt toegelaten **moet** zijn een nieuwe dataset zonder om het even welke eerder opgenomen gegevens.
- Voor een bepaald profielfragment alleen rijen die een recentere versie bevatten `lastUpdatedDate` wordt opgenomen. Als de rij geen recentere rij bevat `lastUpdatedDate`, wordt de rij genegeerd.

## Recommendations

Houd rekening met het volgende wanneer u tijdstempelbestellingen voor klanten implementeert:

- U bent verantwoordelijk voor het synchroniseren van de klokken op alle interne systemen die gegevens verzenden naar de profielopslag.
- De tijdstempels in de indeling ISO 8061 moeten een precisie op millisecondenniveau hebben.
- Het gebruik van Data Prep in coördinatie met de tijdstempelvolgorde van de klant is **sterk aanbevolen**, maakt het een kopie van alle opgenomen rijen samen met hun tijdstempels, waardoor het foutopsporing kan worden verbeterd als zich problemen voordoen.
