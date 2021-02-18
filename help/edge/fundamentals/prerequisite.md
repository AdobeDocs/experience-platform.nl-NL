---
title: Vereisten voor het Gebruiken van het Web SDK van Adobe Experience Platform
description: Leer over de eerste vereisten voor het gebruiken van SDK van het Web van Adobe Experience Platform.
keywords: 1st-partijdomein;CNAME;schema;creeer schema;lancering;aep Web sdk uitbreiding;uitbreiding;configuratie identiteitskaart;configuratiehulpmiddel;gegevenselement;creeer gegevenselement;XDM Voorwerp;sendEvent;send Gebeurtenis;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# Vereisten voor het gebruik van de Adobe Experience Platform Web SDK

Om SDK van het Web van het Platform te gebruiken, moet u eerst:

- Uw organisatie voorzien hebben voor deze eigenschap. (De toegang tot het Web SDK van het Platform is vrij, als u toegang zou willen krijgen gelieve te bereiken tot uw Manager van het Succes van de Klant (CSM)).
- Heb een 1st-partijdomein (CNAME) toegelaten. Als je al een CNAME voor Adobe Analytics hebt, moet je die gebruiken. Het testen in ontwikkeling werkt zonder een CNAME, maar u hebt één nodig alvorens u aan productie gaat.

>[!IMPORTANT]
>
>**Houd er rekening mee dat vanaf 11/10/20 de 1st-party CNAME-implementaties 7 dagen verlopen op alle Safari-browsers en mobiele iOS-apparaten.**

- Mag Adobe Experience Platform gebruiken. Als u Adobe Experience Platform niet hebt aangeschaft, biedt Adobe u zonder extra kosten de benodigde toegang om op beperkte wijze met de SDK te gebruiken.
- Als uw website de [Experience Cloud ID Service](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) al op uw website gebruikt—via de Bezoeker-API of de Experience Cloud ID Service-extensie in Adobe Experience Platform Launch—en u wilt deze blijven gebruiken tijdens het migreren naar Adobe Experience Platform Web SDK, moet u de nieuwste versie van de Bezoeker-API of de Experience Cloud ID Service-extensie gebruiken. Zie [ID-migratie](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) voor meer informatie.
