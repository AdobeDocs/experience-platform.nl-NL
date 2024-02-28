---
keywords: Experience Platform;home;populaire onderwerpen;sandbox-ontwikkelaarsgids
solution: Experience Platform
title: API-handleiding voor sandbox
description: Sandboxen in Adobe Experience Platform bieden geïsoleerde ontwikkelomgevingen waarmee u functies kunt testen, experimenten kunt uitvoeren en aangepaste configuraties kunt maken zonder dat dit gevolgen heeft voor uw productieomgeving.
role: Developer
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# [!DNL Sandbox] API-handleiding

De [!DNL Sandbox] API biedt verschillende eindpunten waarmee u programmatisch alle sandboxen kunt beheren die binnen uw organisatie beschikbaar zijn. Deze eindpunten worden hieronder beschreven. Ga naar de afzonderlijke eindpunthulplijnen voor meer informatie en raadpleeg de [gids Aan de slag](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lees steekproefAPI vraag, en meer.

Ga naar de [[!DNL Sandbox] API-referentie](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Beschikbare sandboxen

Met het beschikbare sandboxeindpunt kunt u een lijst weergeven met alle beschikbare sandboxen voor de huidige gebruiker, inclusief informatie over de naam, titel, status, type en regio van elke sandbox. Het beschikbare sandboxeindpunt in het dialoogvenster [!DNL Sandbox] API kan door alle gebruikers worden betreden, met inbegrip van die zonder de toegangstoestemmingen van het Beleid Sandbox. Zie de [beschikbare sandboxeindhulplijn](./available.md) voor informatie over het weergeven van beschikbare sandboxen in de API.

## Sandboxbeheer

Een sandbox is een virtuele partitie binnen één instantie van Adobe Experience Platform, die naadloze integratie met het ontwikkelingsproces van uw digitale ervaringstoepassingen mogelijk maakt. U kunt productie- en ontwikkelingssandboxen maken, weergeven, bewerken, opnieuw instellen en verwijderen met de `/sandboxes` eindpunt. Om te leren hoe te om dit eindpunt te gebruiken, zie [sandboxeindhulplijn](./sandboxes.md).

## Typen sandbox

Momenteel zijn de ondersteunde sandboxtypen op Experience Platform productie- en ontwikkelingssandboxen. Een standaardplatformlicentie geeft u in totaal vijf sandboxen, die u kunt classificeren als productie of ontwikkeling. U kunt extra pakketten van 10 sandboxen een licentie geven tot een maximum van 75 sandboxen in totaal. Zie de [eindhulplijn sandbox-typen](./types.md) voor informatie over het weergeven van ondersteunde sandboxtypen voor uw organisatie in de API.

## Volgende stappen

Beginnen het maken vraag gebruikend [!DNL Sandbox] API, lees de [gids Aan de slag](./getting-started.md) Selecteer vervolgens een van de eindpunthulplijnen om te leren hoe u specifieke eindpunten kunt gebruiken.
