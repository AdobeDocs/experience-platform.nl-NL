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

De API [!DNL Sandbox] biedt verschillende eindpunten waarmee u programmatisch alle sandboxen kunt beheren die binnen uw organisatie beschikbaar zijn. Deze eindpunten worden hieronder beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar [ begonnen gids ](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

Om alle beschikbare eindpunten en verrichtingen te zien CRUD, bezoek de [[!DNL Sandbox]  API verwijzing ](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Beschikbare sandboxen

Met het beschikbare sandboxeindpunt kunt u een lijst weergeven met alle beschikbare sandboxen voor de huidige gebruiker, inclusief informatie over de naam, titel, status, type en regio van elke sandbox. Het beschikbare zandbakeneindpunt in [!DNL Sandbox] API kan door alle gebruikers, met inbegrip van die zonder de toegangstoestemmingen van het Beleid Sandbox worden betreden. Zie de [ beschikbare gids van het zandbakeindpunt ](./available.md) om te leren hoe te om beschikbare zandbakken in API te bekijken.

## Sandboxbeheer

Een sandbox is een virtuele partitie binnen één instantie van Adobe Experience Platform, die naadloze integratie met het ontwikkelingsproces van uw digitale ervaringstoepassingen mogelijk maakt. Met het eindpunt `/sandboxes` kunt u productie- en ontwikkelingssandboxen maken, weergeven, bewerken, opnieuw instellen en verwijderen. Leren hoe te om dit eindpunt te gebruiken, zie de [ gids van het zandbakeindpunt ](./sandboxes.md).

## Typen sandbox

Momenteel zijn de ondersteunde sandboxtypen op Experience Platform productie- en ontwikkelingssandboxen. Een standaardplatformlicentie geeft u in totaal vijf sandboxen, die u kunt classificeren als productie of ontwikkeling. U kunt extra pakketten van 10 sandboxen een licentie geven tot een maximum van 75 sandboxen in totaal. Zie de [ gids van het de types van zandbak eindseindpunt ](./types.md) leren hoe te om gesteunde zandbaktypes voor uw organisatie in API te bekijken.

## Volgende stappen

Begin makend vraag gebruikend [!DNL Sandbox] API, lees [ begonnen gids ](./getting-started.md) toen selecteren één van de eindpuntgidsen om te leren hoe te om specifieke eindpunten te gebruiken.
