---
title: Vereisten voor het Gebruiken van het Web SDK van Adobe Experience Platform
description: Meer informatie over de voorwaarden voor het gebruik van Adobe Experience Platform Web SDK.
keywords: 1st-partijdomein;CNAME;schema;creeer schema;lancering;aep Web sdk uitbreiding;uitbreiding;configuratie identiteitskaart;configuratiehulpmiddel;gegevenselement;creeer gegevenselement;XDM Voorwerp;sendEvent;send Gebeurtenis;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 853c0a662592939c280c7e7ede8235d1b6155b2f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Vereisten voor het gebruik van de Adobe Experience Platform Web SDK

Als u de Adobe Experience Platform Web SDK wilt gebruiken, moet u eerst:

- Uw organisatie voorzien hebben voor deze eigenschap. Vul het volgende in als u toegang wilt krijgen [formulier](https://adobe.ly/websdkaccess) en Adobe geeft u (indien nodig) toegang tot gegevensstreams en Adobe Experience Platform. Houd er rekening mee dat Adobe u zonder extra kosten toegang biedt tot de SDK, zodat u deze in beperkte mate kunt gebruiken.
- Het wordt aanbevolen om domein van de eerste partij (CNAME) ingeschakeld te hebben. Als je al een CNAME voor Adobe Analytics hebt, moet je die gebruiken. Het testen in ontwikkeling werkt zonder een CNAME, maar Adobe adviseert om één te hebben alvorens u aan productie gaat. Hoewel een CNAME-implementatie geen voordelen biedt in termen van de levensduur van cookies, kan het voorkomen dat bepaalde advertentieblokkers en minder gebruikelijke browsers SDK-aanvragen blokkeren. In die gevallen, zou het gebruiken van een NAAM uw gegevensinzameling voor gebruikers kunnen verhinderen worden verstoord die deze hulpmiddelen gebruiken.

>[!IMPORTANT]
>
>**Houd er rekening mee dat vanaf 11/10/20 de 1st-party CNAME-implementaties 7 dagen verlopen op alle Safari-browsers en mobiele iOS-apparaten.**

- Als uw website al het [Experience Cloud ID-service](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) op uw website-of door Bezoeker API of de uitbreiding van de Dienst van identiteitskaart van de Experience Cloud binnen Adobe Experience Platform Launch-en u zou het willen blijven gebruiken terwijl het migreren aan de SDK van het Web van Adobe Experience Platform, moet u de recentste versie van Bezoeker API of de uitbreiding van de Dienst van identiteitskaart van de Experience Cloud gebruiken. Zie [ID-migratie](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) voor meer informatie .

## Machtigingen beheren voor Adobe Experience Platform Web SDK

Als u Adobe Experience Platform Web SDK wilt gaan gebruiken, moet u de juiste machtigingen hebben geconfigureerd. Raadpleeg onze documentatie voor meer informatie over het instellen van uw configuratie [beheer van gegevensverzamelingsmachtigingen](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).
