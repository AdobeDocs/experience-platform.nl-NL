---
title: Vereisten voor het Gebruiken van het Web SDK van Adobe Experience Platform
description: Leer over de eerste vereisten voor het gebruiken van SDK van het Web van Adobe Experience Platform.
keywords: 1st-partijdomein;CNAME;schema;creeer schema;lancering;aep Web sdk uitbreiding;uitbreiding;configuratie identiteitskaart;configuratiehulpmiddel;gegevenselement;creeer gegevenselement;XDM Voorwerp;sendEvent;send Gebeurtenis;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 5f3b82edbc52d96cad13932be1d201e275780f3c
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Vereisten voor het gebruik van de Adobe Experience Platform Web SDK

Om SDK van het Web van het Platform te gebruiken, moet u eerst:

- Uw organisatie voorzien hebben voor deze eigenschap. (De toegang tot het Web SDK van het Platform is vrij, als u toegang zou willen krijgen gelieve te bereiken tot uw Manager van het Succes van de Klant (CSM)).
- Het wordt aanbevolen om domein van de eerste partij (CNAME) ingeschakeld te hebben. Als je al een CNAME voor Adobe Analytics hebt, moet je die gebruiken. Het testen in ontwikkeling werkt zonder een CNAME, maar Adobe adviseert om één te hebben alvorens u aan productie gaat. Hoewel een CNAME-implementatie geen voordelen biedt in termen van de levensduur van cookies, kan het voorkomen dat bepaalde advertentieblokkers en minder gebruikelijke browsers SDK-aanvragen blokkeren. In die gevallen, zou het gebruiken van een NAAM uw gegevensinzameling voor gebruikers kunnen verhinderen worden verstoord die deze hulpmiddelen gebruiken.

>[!IMPORTANT]
>
>**Houd er rekening mee dat vanaf 11/10/20 de 1st-party CNAME-implementaties 7 dagen verlopen op alle Safari-browsers en mobiele iOS-apparaten.**

- Mag Adobe Experience Platform gebruiken. Als u Adobe Experience Platform niet hebt aangeschaft, biedt Adobe u zonder extra kosten de benodigde toegang om op beperkte wijze met de SDK te gebruiken.
- Als uw website de [Experience Cloud ID Service](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) al op uw website gebruikt—via de Bezoeker-API of de Experience Cloud ID Service-extensie in Adobe Experience Platform Launch—en u wilt deze blijven gebruiken tijdens het migreren naar Adobe Experience Platform Web SDK, moet u de nieuwste versie van de Bezoeker-API of de Experience Cloud ID Service-extensie gebruiken. Zie [ID-migratie](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) voor meer informatie.
