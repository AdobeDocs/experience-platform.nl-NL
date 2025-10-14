---
keywords: Experience Platform;home;populaire onderwerpen;sandbox-ontwikkelaarsgids
solution: Experience Platform
title: API-handleiding voor sandbox
description: Sandboxen in Adobe Experience Platform bieden geïsoleerde ontwikkelomgevingen waarmee u functies kunt testen, experimenten kunt uitvoeren en aangepaste configuraties kunt maken zonder dat dit gevolgen heeft voor uw productieomgeving.
role: Developer
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# [!DNL Sandbox] API-handleiding

De API [!DNL Sandbox] biedt verschillende eindpunten waarmee u programmatisch alle sandboxen kunt beheren die binnen uw organisatie beschikbaar zijn. Deze eindpunten worden hieronder beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar [&#x200B; begonnen gids &#x200B;](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

Om alle beschikbare eindpunten en verrichtingen te zien CRUD, bezoek de [[!DNL Sandbox]  API verwijzing &#x200B;](https://www.adobe.io/experience-platform-apis/references/sandbox).

## Beschikbare sandboxen

Met het beschikbare sandboxeindpunt kunt u een lijst weergeven met alle beschikbare sandboxen voor de huidige gebruiker, inclusief informatie over de naam, titel, status, type en regio van elke sandbox. Het beschikbare zandbakeneindpunt in [!DNL Sandbox] API kan door alle gebruikers, met inbegrip van die zonder de toegangstoestemmingen van het Beleid Sandbox worden betreden. Zie de [&#x200B; beschikbare gids van het zandbakeindpunt &#x200B;](./available.md) om te leren hoe te om beschikbare zandbakken in API te bekijken.

## Sandboxbeheer

Een sandbox is een virtuele partitie binnen één instantie van Adobe Experience Platform, die naadloze integratie met het ontwikkelingsproces van uw digitale ervaringstoepassingen mogelijk maakt. Met het eindpunt `/sandboxes` kunt u productie- en ontwikkelingssandboxen maken, weergeven, bewerken, opnieuw instellen en verwijderen. Leren hoe te om dit eindpunt te gebruiken, zie de [&#x200B; gids van het zandbakeindpunt &#x200B;](./sandboxes.md).

## Typen sandbox

Momenteel zijn de ondersteunde sandboxtypen op Experience Platform productie- en ontwikkelingssandboxen. Een Experience Platform-standaardlicentie geeft u in totaal vijf sandboxen, die u kunt indelen als productie of ontwikkeling. U kunt extra pakketten van 10 sandboxen een licentie geven tot een maximum van 75 sandboxen in totaal. Zie de [&#x200B; gids van het de types van zandbak eindseindpunt &#x200B;](./types.md) leren hoe te om gesteunde zandbaktypes voor uw organisatie in API te bekijken.

## Volgende stappen

Begin makend vraag gebruikend [!DNL Sandbox] API, lees [&#x200B; begonnen gids &#x200B;](./getting-started.md) toen selecteren één van de eindpuntgidsen om te leren hoe te om specifieke eindpunten te gebruiken.
