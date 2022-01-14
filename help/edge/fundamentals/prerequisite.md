---
title: Vereisten voor het Gebruiken van het Web SDK van Adobe Experience Platform
description: Meer informatie over de voorwaarden voor het gebruik van Adobe Experience Platform Web SDK.
keywords: 1st-partijdomein;CNAME;schema;creeer schema;lancering;aep Web sdk uitbreiding;uitbreiding;configuratie identiteitskaart;configuratiehulpmiddel;gegevenselement;creeer gegevenselement;XDM Voorwerp;sendEvent;send Gebeurtenis;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 072e1968fa152454f4df6e88fcf7de5c03494030
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Vereisten voor het gebruik van de Adobe Experience Platform Web SDK

Als u de Adobe Experience Platform Web SDK wilt gebruiken, moet u eerst:

- Uw organisatie voorzien hebben voor deze eigenschap. Vul het volgende in als u toegang wilt krijgen [formulier](http://adobe.ly/websdkaccess) en Adobe krijgt u toegang tot Datatstreams en Adobe Experience Platform (indien nodig). Houd er rekening mee dat Adobe u zonder extra kosten toegang biedt tot de SDK, zodat u deze in beperkte mate kunt gebruiken.
- Het wordt aanbevolen om domein van de eerste partij (CNAME) ingeschakeld te hebben. Als je al een CNAME voor Adobe Analytics hebt, moet je die gebruiken. Het testen in ontwikkeling werkt zonder een CNAME, maar Adobe adviseert om één te hebben alvorens u aan productie gaat. Hoewel een CNAME-implementatie geen voordelen biedt in termen van de levensduur van cookies, kan het voorkomen dat bepaalde advertentieblokkers en minder gebruikelijke browsers SDK-aanvragen blokkeren. In die gevallen, zou het gebruiken van een NAAM uw gegevensinzameling voor gebruikers kunnen verhinderen worden verstoord die deze hulpmiddelen gebruiken.

>[!IMPORTANT]
>
>**Houd er rekening mee dat vanaf 11/10/20 de 1st-party CNAME-implementaties 7 dagen verlopen op alle Safari-browsers en mobiele iOS-apparaten.**

- Als uw website al het [Experience Cloud ID-service](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) op uw website-of door Bezoeker API of de uitbreiding van de Dienst van identiteitskaart van de Experience Cloud binnen Adobe Experience Platform Launch-en u zou het willen blijven gebruiken terwijl het migreren aan de SDK van het Web van Adobe Experience Platform, moet u de recentste versie van Bezoeker API of de uitbreiding van de Dienst van identiteitskaart van de Experience Cloud gebruiken. Zie [ID-migratie](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) voor meer informatie .

## Machtigingen beheren voor Adobe Experience Platform Web SDK

Als je Adobe Experience Platform wilt gaan gebruiken, moet je het recht hebben [machtigingen](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=en) om uw schema&#39;s te maken en identiteiten te beheren. U vindt de minimale machtigingen die nodig zijn in de categorie Gegevensmodellering en identiteiten.

![](../images/AEP-permission-categories.png)

Geef gebruikers binnen de categorie Gegevensmodellering de machtigingen Schema&#39;s beheren en Schema&#39;s weergeven.

![](../images/data-modeling-permissions.png)

Geef gebruikers binnen de categorie Identity Management de machtigingen Naamruimten beheren en Identiteitsnaamruimten weergeven.

![](../images/identity-management-permissions.png)
