---
keywords: Experience Platform;home;populaire onderwerpen;Beleidshandhaving;Automatische handhaving;API-gebaseerde handhaving;gegevensbeheer
solution: Experience Platform
title: Overzicht van beleidshandhaving
topic-legacy: guide
description: Leer hoe het beleid voor gegevensgebruik wordt afgedwongen op Adobe Experience Platform.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 6f79b1a03a75558d1a25f0375e8393ad56756d80
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Overzicht van beleidshandhaving

Eenmaal [gegevensgebruikslabels](../labels/overview.md) zijn toegepast en [beleid voor gegevensgebruik](../policies/overview.md) Als u een beleid hebt gedefinieerd, kunt u dat beleid toepassen om gegevensbewerkingen te voorkomen die beleidsovertredingen vormen.

>[!NOTE]
>
>Dit document is gericht op de handhaving van het beleid voor gegevensgebruik. Voor informatie over het beleid van de toegangscontrole, verwijs naar de gids over [attribuut-based toegangsbeheer](../../access-control/abac/overview.md).

Er zijn twee methoden voor de handhaving van het beleid in Adobe Experience Platform: automatische handhaving en op API gebaseerde handhaving.

## Automatische handhaving

Het Experience Platform maakt gebruik van gegevenslijn, gegevensclassificatie en mogelijkheden voor beleidsbeheer om beleidsovertredingen automatisch te evalueren en aan te geven. Zie het overzicht op [automatische beleidshandhaving](./auto-enforcement.md) voor meer informatie .

## Op API gebaseerde handhaving

De [!DNL Policy Service] API verstrekt eindpunten die u toestaan om marketing acties tegen datasets of willekeurige combinaties etiketten van het gegevensgebruik te testen om te controleren als om het even welke beleidsschendingen voorkomen. Op basis van de API-reactie kunt u vervolgens protocollen in uw ervaringstoepassing instellen om de naleving van het gegevensbeheerbeleid op de juiste manier af te dwingen.

Zie de zelfstudie aan [Op API gebaseerde handhaving](./api-enforcement.md) voor stappen over hoe te om beleid te evalueren gebruikend API.
