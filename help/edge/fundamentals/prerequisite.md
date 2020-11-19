---
title: Vereisten voor het gebruik van Adobe Experience Platform Web SDK
seo-title: Vereisten voor het gebruik van Adobe Experience Platform Web SDK
description: Vereisten voor het gebruik van Adobe Experience Platform Web SDK
seo-description: Vereisten voor het gebruik van Adobe Experience Platform Web SDK
keywords: 1st-party domain;CNAME;schema;create schema;launch;aep web sdk extension;extension;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;
translation-type: tm+mt
source-git-commit: a0ede8c7d3088fe80d6ea014b4a4f9f08ee8a7aa
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Vereisten voor het gebruik van Adobe Experience Platform Web SDK

Als u deze SDK wilt gebruiken, moet u eerst:

- Zorg ervoor dat uw organisatie over deze functie beschikt. (Als u op de wachtlijst wilt staan, neemt u contact op met uw Certified Software Manager (CSM)).
- Heb een 1st-partijdomein (CNAME) toegelaten. Als je al een CNAME voor Adobe Analytics hebt, moet je die gebruiken. Het testen in ontwikkeling werkt zonder een CNAME, maar u hebt één nodig alvorens u aan productie gaat.

>[!IMPORTANT]
>
>**Houd er rekening mee dat vanaf 11/10/20 de 1st-party CNAME-implementaties 7 dagen verlopen op alle Safari-browsers en mobiele iOS-apparaten.**

- Mag Adobe Experience Platform gebruiken. Als u Adobe Experience Platform niet hebt aangeschaft, zal Adobe u zonder extra kosten voorzien van de Stichting van de Diensten van de Gegevens van het Experience Platform voor gebruik op een beperkte manier met SDK.
- Als uw website de [Experience Cloud ID-service](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) al op uw website gebruikt (via de Bezoeker-API of de extensie voor Experience Cloud-id-service in Adobe Experience Platform Launch) en u wilt deze blijven gebruiken tijdens de migratie naar Adobe Experience Platform Web SDK, moet u de nieuwste versie van de Bezoeker-API of de Experience Cloud ID-service-extensie gebruiken. Zie [ID-migratie](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) voor meer informatie.
