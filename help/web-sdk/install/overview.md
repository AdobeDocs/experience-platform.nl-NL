---
title: Overzicht van de installatie van Web SDK
description: Leer hoe te om het Web SDK van het Experience Platform te installeren.
keywords: web sdk installatie;installeren web sdk;Internet Explorer;promise;npm pakket
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Overzicht van de installatie van Web SDK

Er zijn drie ondersteunde manieren om Adobe Experience Platform Web SDK te gebruiken:

1. **[de markeringsuitbreiding van SDK van het Web](extension.md)**: Adobe adviseert gebruikend deze methode. Installeer een tagloader op uw site en gebruik vervolgens de gebruikersinterface van de Adobe Experience Platform-gegevensverzameling om uw implementatie te configureren.
1. **[de bibliotheek van SDK van het Web JavaScript](library.md)**: Verwijzing een CDN-ontvangen bibliotheekdossier, of gastheer het bibliotheekdossier gebruikend uw eigen infrastructuur. Aanroepen vanuit de code op uw site naar de bibliotheek uitvoeren.
1. **[NPM](npm.md)**: Installeer SDK van het Web op uw plaats gebruikend de NPM pakketmanager.

## Vereisten

Voordat u de SDK van het Web kunt gebruiken of installeren, moet u aan de volgende vereisten voldoen:

* De architectuur in Adobe Experience Platform moet eerst worden gevormd. Deze instellingen omvatten alle benodigde schema&#39;s, identiteiten en gegevensstromen.
* U moet de juiste toestemmingen hebben die worden gevormd om tot de aangewezen hulpmiddelen toegang te hebben. Als uw organisatie bijvoorbeeld besluit om de tagextensie te gebruiken, moet u over de juiste machtigingen beschikken om de UI voor gegevensverzameling te openen. Zie [ het beheer van de toestemmingen van de gegevensinzameling ](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=nl-NL) voor meer informatie.
* Het heeft van een 1st-partijdomein (CNAME) wordt geadviseerd. Als je al een CNAME voor Adobe Analytics hebt, kun je die gebruiken. Het testen in ontwikkeling werkt zonder een CNAME, maar de Adobe adviseert om één te hebben alvorens aan productie te publiceren. Zie [ Eerste partij apparaat IDs ](../identity/first-party-device-ids.md) voor meer informatie.
