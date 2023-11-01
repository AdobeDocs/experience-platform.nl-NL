---
title: Vereisten voor het Gebruiken van het Web SDK van Adobe Experience Platform
description: Meer informatie over de voorwaarden voor het gebruik van Adobe Experience Platform Web SDK.
keywords: 1st-partijdomein;CNAME;schema;creeer schema;lancering;aep Web sdk uitbreiding;uitbreiding;configuratie identiteitskaart;configuratiehulpmiddel;gegevenselement;creeer gegevenselement;XDM Voorwerp;sendEvent;send Gebeurtenis;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Vereisten voor het gebruik van de Adobe Experience Platform Web SDK

Als u de Adobe Experience Platform Web SDK wilt gebruiken, moet u eerst:

- Heb de juiste toestemmingen die voor gebruikers in uw organisatie worden gevormd. Alle klanten van het Experience Cloud hebben toegang tot de hulpmiddelen van de Inzameling van Gegevens, zal elke gebruiker in uw organisatie enkel toestemmingen aan Schema&#39;s, Identiteiten, en de stromen van Gegevens vereisen. Zie onze documentatie over voor meer informatie over het instellen van deze machtigingen [beheer van gegevensverzamelingsmachtigingen](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).
- Het wordt aanbevolen om domein van de eerste partij (CNAME) ingeschakeld te hebben. Als je al een CNAME voor Adobe Analytics hebt, moet je die gebruiken. Het testen in ontwikkeling werkt zonder een CNAME, maar de Adobe adviseert hebbend één alvorens u naar productie gaat. Hoewel een CNAME-implementatie geen voordelen biedt in termen van de levensduur van cookies, kan het voorkomen dat bepaalde advertentieblokkers en minder gebruikelijke browsers SDK-aanvragen blokkeren. In die gevallen, zou het gebruiken van een NAAM uw gegevensinzameling voor gebruikers kunnen verhinderen worden verstoord die deze hulpmiddelen gebruiken.

>[!IMPORTANT]
>
>**Houd er rekening mee dat vanaf 11/10/20 de 1st-party CNAME-implementaties 7 dagen verlopen op alle Safari-browsers en mobiele iOS-apparaten.**

- Als uw website al het [Experience Cloud-id-service](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) op uw website-of door Bezoeker API of de uitbreiding van de Dienst van identiteitskaart van het Experience Cloud binnen Adobe Experience Platform Launch-en u zou het willen blijven gebruiken terwijl het migreren aan het Web SDK van Adobe Experience Platform, moet u de recentste versie van Bezoeker API of de uitbreiding van de Dienst van identiteitskaart van het Experience Cloud gebruiken. Zie [ID-migratie](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#identity) voor meer informatie .
