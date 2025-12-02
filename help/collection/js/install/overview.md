---
title: Overzicht van Web SDK-installatie
description: Leer hoe u de Experience Platform Web SDK installeert.
keywords: web sdk installatie;installeren web sdk;Internet Explorer;promise;npm pakket
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: a490c429047f5e5997d69f30a51e6b78debe2d5d
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Overzicht van Web SDK-installatie

Er zijn drie ondersteunde manieren om Adobe Experience Platform Web SDK te gebruiken:

1. **[de markeringsuitbreiding van SDK van het Web](/help/tags/extensions/client/web-sdk/overview.md)**: Adobe adviseert gebruikend deze methode. Installeer een tagloader op uw site en gebruik vervolgens de gebruikersinterface van de Adobe Experience Platform-gegevensverzameling om uw implementatie te configureren.
1. **[de bibliotheek van JavaScript van SDK van het Web](library.md)**: Verwijzing een CDN-ontvangen bibliotheekdossier, of gastheer het bibliotheekdossier gebruikend uw eigen infrastructuur. Aanroepen vanuit de code op uw site naar de bibliotheek uitvoeren.
1. **[NPM](npm.md)**: Installeer het Web SDK op uw plaats gebruikend NPM pakketmanager.

## Vereisten

Voordat u de SDK voor het web kunt gebruiken of installeren, moet u aan de volgende vereisten voldoen:

* De architectuur in Adobe Experience Platform moet eerst worden gevormd. Deze instellingen omvatten alle benodigde schema&#39;s, identiteiten en gegevensstromen.
* U moet de juiste toestemmingen hebben die worden gevormd om tot de aangewezen hulpmiddelen toegang te hebben. Als uw organisatie bijvoorbeeld besluit om de tagextensie te gebruiken, moet u over de juiste machtigingen beschikken om de UI voor gegevensverzameling te openen. Zie [ de inzamelingstoestemmingen van Gegevens ](../../permissions.md) voor meer informatie.
* Het heeft van een 1st-partijdomein (CNAME) wordt geadviseerd. Als je al een CNAME voor Adobe Analytics hebt, kun je die gebruiken. Het testen in ontwikkeling werkt zonder een CNAME, maar Adobe raadt aan om er een te hebben voordat het publiceert naar productie. Zie [ Eerste partij apparaat IDs ](../../use-cases/identity/first-party-device-ids.md) voor meer informatie.
