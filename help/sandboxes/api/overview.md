---
keywords: Experience Platform;home;populaire onderwerpen;sandbox-ontwikkelaarsgids
solution: Experience Platform
title: API-handleiding voor sandbox
topic-legacy: developer guide
description: Sandboxen in Adobe Experience Platform bieden geïsoleerde ontwikkelomgevingen waarmee u functies kunt testen, experimenten kunt uitvoeren en aangepaste configuraties kunt maken zonder dat dit gevolgen heeft voor uw productieomgeving.
source-git-commit: f00e6161d82f1fd7ba442be9f06283f3c866573f
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# [!DNL Sandbox] API-handleiding

De [!DNL Sandbox] API verstrekt verscheidene eindpunten die u toestaan om alle zandbakken programmatically te beheren beschikbaar aan u binnen uw organisatie IMS. Deze eindpunten worden hieronder beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar [begonnen gids](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

Als u alle beschikbare eindpunten en CRUD-bewerkingen wilt zien, gaat u naar de [[!DNL Sandbox] API-referentie](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml).

## Beschikbare sandboxen

Met het beschikbare sandboxeindpunt kunt u een lijst weergeven met alle beschikbare sandboxen voor de huidige gebruiker, inclusief informatie over de naam, titel, status, type en regio van elke sandbox. Het beschikbare zandbakeneindpunt in [!DNL Sandbox] API kan door alle gebruikers, met inbegrip van die zonder de toegangstoestemmingen van het Beleid van Sandbox worden betreden. Zie [de beschikbare gids van het zandbakeindpunt ](./available.md) om te leren hoe te om beschikbare zandbakken in API te bekijken.

## Sandboxbeheer

Een sandbox is een virtuele partitie binnen één instantie van Adobe Experience Platform, die naadloze integratie met het ontwikkelingsproces van uw digitale ervaringstoepassingen mogelijk maakt. Met het eindpunt `/sandboxes` kunt u productie- en ontwikkelingssandboxen maken, weergeven, bewerken, herstellen en verwijderen. Leren hoe te om dit eindpunt te gebruiken, zie [zandbakeindgids](./sandboxes.md).

## Typen sandboxen

Momenteel zijn de ondersteunde sandboxtypen op Experience Platform productie- en ontwikkelingssandboxen. Een standaardlicentie voor Platforms kent u in totaal vijf sandboxen toe, die u kunt classificeren als productie of ontwikkeling. U kunt extra pakketten van 10 sandboxen een licentie geven tot een maximum van 75 sandboxen in totaal. Zie [sandbox types eindpuntgids](./types.md) om te leren hoe te om gesteunde zandbaktypes voor uw organisatie in API te bekijken.

## Volgende stappen

Wanneer u begint met het maken van aanroepen met de [!DNL Sandbox]-API, leest u de [gids Aan de slag](./getting-started.md) en selecteert u vervolgens een van de eindpunthulplijnen om te leren hoe u specifieke eindpunten kunt gebruiken.