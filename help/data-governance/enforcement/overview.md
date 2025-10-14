---
keywords: Experience Platform;home;populaire onderwerpen;Beleidshandhaving;Automatische handhaving;API-gebaseerde handhaving;gegevensbeheer
solution: Experience Platform
title: Overzicht van beleidshandhaving
description: Leer hoe het beleid voor gegevensgebruik wordt afgedwongen op Adobe Experience Platform.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Overzicht van beleidshandhaving

Zodra [&#x200B; de etiketten van het gegevensgebruik &#x200B;](../labels/overview.md) zijn toegepast en [&#x200B; het beleid van het gegevensgebruik &#x200B;](../policies/overview.md) zijn bepaald, kunt u dat beleid afdwingen om gegevensverrichtingen te verhinderen die beleidsschendingen vormen.

>[!NOTE]
>
>In dit document wordt de nadruk gelegd op de handhaving van het beleid voor gegevensgebruik. Voor informatie over toegangsbeheerbeleid, verwijs naar de gids op [&#x200B; op attributen-gebaseerde toegangsbeheer &#x200B;](../../access-control/abac/overview.md).

Er zijn twee methoden voor beleidshandhaving op Adobe Experience Platform: automatische handhaving en op API gebaseerde handhaving.

## Automatische handhaving

Het Experience Platform maakt gebruik van gegevenslijn, gegevensclassificatie en mogelijkheden voor beleidsbeheer om beleidsovertredingen automatisch te evalueren en aan te geven. Zie het overzicht op [&#x200B; automatische beleidshandhaving &#x200B;](./auto-enforcement.md) voor meer informatie.

## Op API gebaseerde handhaving

De API van [!DNL Policy Service] verstrekt eindpunten die u toestaan om marketing acties tegen datasets of willekeurige combinaties etiketten van het gegevensgebruik te testen om als om het even welke beleidsschendingen te controleren. Op basis van de API-reactie kunt u vervolgens protocollen in uw ervaringstoepassing instellen om de naleving van het gegevensbeheerbeleid op de juiste manier af te dwingen.

Zie het leerprogramma op [&#x200B; API-Gebaseerde handhaving &#x200B;](./api-enforcement.md) voor stappen op hoe te om beleid te evalueren gebruikend API.
