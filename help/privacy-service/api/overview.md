---
title: Handleiding voor Privacy Service-API
description: Leer hoe u de Privacy Service-API kunt gebruiken voor het programmatisch beheren van privacytaken voor ondersteunde Adobe Experience Cloud-toepassingen.
role: Developer
exl-id: 665466ac-2447-4a9d-a8cf-62092c09e431
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# [!DNL Privacy Service] API-handleiding

De Privacy Service-API bevat verschillende eindpunten waarmee u via programmacode privacytaken voor uw organisatie kunt beheren. Deze eindpunten worden hieronder beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar [ begonnen gids ](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

>[!NOTE]
>
>In deze handleiding wordt uitgelegd hoe u de API van [!DNL Privacy Service] gebruikt. Voor details op hoe te om UI te gebruiken, zie het [ overzicht van de Privacy Service UI ](../ui/overview.md).

Om alle beschikbare eindpunten en verrichtingen te bekijken CRUD, bezoek de [ Privacy Service API verwijzing ](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Privacytaken

Wanneer de Privacy Service een verzoek ontvangt om toegang te krijgen tot of de persoonsgegevens van een onderwerp te verwijderen, creëert het systeem privacytaken om aan dat verzoek te voldoen. Elke privacytaak bevat identiteitsgegevens die betrekking hebben op de betrokkene, metagegevens over het Adobe Experience Cloud-product waarop de taak van toepassing is en de verwerkingsstatus van de taak.

Met het `/jobs` -eindpunt kunt u privacytaken voor uw organisatie maken en ophalen. Leren hoe te om dit eindpunt te gebruiken, zie de [ gids van het de baaneindpunt van de privacy ](./privacy-jobs.md).

## Toestemming

Bepaalde voorschriften vereisen uitdrukkelijke toestemming van de klant voordat de persoonsgegevens kunnen worden verzameld. Met het `/consent` -eindpunt kunt u verzoeken om toestemming van klanten verwerken en deze integreren in uw privacyworkflow. Zie de [ gids van het toestemmings eindpunt ](./consent.md) om meer te leren.

## Volgende stappen

Begin makend vraag gebruikend de Privacy Service API, lees [ begonnen gids ](./getting-started.md) toen selecteren één van de eindpuntgidsen om te leren hoe te om specifieke eindpunten te gebruiken.
