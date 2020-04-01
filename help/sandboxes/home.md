---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van sandboxen
topic: overview
translation-type: tm+mt
source-git-commit: 564940f37b66159c84ca7402bd3648010232182b

---


# Overzicht van sandboxen

Het Adobe Experience Platform is ontworpen om toepassingen voor digitale ervaringen wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen.

Om aan deze behoefte tegemoet te komen, biedt het Experience Platform **sandboxen** die één platforminstantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Dit document biedt een overzicht op hoog niveau van sandboxen in het Experience Platform.

## Sandboxen

Sandboxen zijn virtuele partities binnen één exemplaar van het Experience Platform, waarmee u naadloze integratie met het ontwikkelingsproces van uw digitale ervaringstoepassingen mogelijk maakt. Een instantie van het Platform van de Ervaring steunt één productie zandbak en veelvoudige niet productiesandboxen, waarbij elke zandbak zijn eigen onafhankelijke bibliotheek van de middelen van het Platform (met inbegrip van schema&#39;s, datasets, profielen, etc.) handhaaft.  Alle inhoud en handelingen die in een sandbox worden uitgevoerd, blijven beperkt tot alleen die sandbox en hebben geen invloed op andere sandboxen.

Met niet-productiesandboxen kunt u functies testen, experimenten uitvoeren en aangepaste configuraties maken zonder dat dit invloed heeft op de productiesandbox. Daarnaast beschikken niet-productiesandboxen over een functie voor het opnieuw instellen die alle door de klant gemaakte bronnen uit de sandbox verwijdert. Niet-productiesandboxen kunnen niet worden omgezet in productiesandboxen.

>[!NOTE] Wanneer een sandbox voor het eerst wordt gemaakt, bevat deze geen gegevens. Aangezien elke zandbak zijn eigen geïsoleerde gegevensopslag handhaaft, moeten zij ook hun gegevens onafhankelijk innemen.

Samengevat bieden sandboxen de volgende voordelen:

* **Levenscyclusbeheer** van toepassingen: Maak afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.
* **Project- en merkbeheer**: Toestaan dat meerdere projecten parallel lopen binnen dezelfde IMS-organisatie, terwijl isolatie en toegangsbeheer worden geboden. De toekomstige versies zullen steun voor het opstellen in veelvoudige regio&#39;s verstrekken.
* **Flexibel ontwikkelings-ecosysteem**: Biedt sandboxen op een naadloze, schaalbare en voordelige manier voor exploratie, activering en demonstratie.

## Toegangsbeheer voor sandboxen

Standaard hebben alle gebruikers van een organisatie toegang tot een productiesandbox. Toegang tot niet-productiesandboxen moet worden verleend door een systeembeheerder, productbeheerder of beheerder van het productprofiel via de [Adobe Admin Console](https://adminconsole.adobe.com).

Voor het weergeven, maken, bijwerken of verwijderen van niet-productiesandboxen moeten gebruikers ook de bevoegdheden van Sandbox-beheer hebben.

Voor meer informatie over het beheren van rollen en toestemmingen voor zandbakken, zie het overzicht [van de](../access-control/home.md)toegangscontrole.

## Sandboxen in de gebruikersinterface van het Experience Platform

In de gebruikersinterface [van het Platform van de](https://platform.adobe.com)Ervaring, kunnen de gebruikers tussen de zandbakken schakelen zij tot toegang hebben door de **zandbakschakelaar** op de top-linker van het scherm te gebruiken.  Gebruikers met bevoegdheden voor Sandboxbeheer hebben ook toegang tot het tabblad **Sandboxen** in de linkernavigatie, waar ze sandboxen voor hun organisatie kunnen weergeven en beheren. Raadpleeg de gebruikershandleiding bij de [sandbox voor meer informatie over het werken met sandboxen in de gebruikersinterface](ui/overview.md).

## Sandboxen in Experience Platform-API&#39;s

Bij het aanroepen van Experience Platform API&#39;s moet een naam voor de sandbox worden opgegeven onder de header `x-sandbox-name`. Wanneer u bijvoorbeeld de API [van de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) Catalogusservice aanroept om alle gegevenssets in de productiesandbox weer te geven, wordt de naam van de sandbox (&quot;prod&quot;) als een header weergegeven in de API-aanvraag:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

Als een API-aanroep `x-sandbox-name` niet wordt opgenomen, gebruikt het systeem een standaardsandbox. De beste manier is echter om deze header altijd op te nemen in alle API-aanroepen, zelfs wanneer de standaardsandbox wordt gebruikt. Daarom wordt in de API-documentatie voor Experience Platform `x-sandbox-name` een vereiste header gebruikt.

### Sandbox-API

Met de sandbox-API kunt u sandboxen beheren met behulp van RESTful-API-bewerkingen. Zie de handleiding voor [sandboxontwikkelaars](api/getting-started.md) voor gedetailleerde informatie over het gebruik van de API, inclusief correct opgemaakte aanvragen en antwoorden op voorbeelden.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd in de essentiële concepten over sandboxen in Experience Platform. Zie de [gebruikershandleiding](ui/overview.md) voor de gebruikersinterface of de [ontwikkelaarsgids](./api/getting-started.md) voor de API voor gedetailleerde stappen voor het beheren van sandboxen.

Hoewel sandboxen een waardevol hulpmiddel zijn voor het isoleren van platformomgevingen voor uw ontwikkelingsteam, kunt u ook meer korrelige toegangscontrole beheren met de Adobe Admin Console. Zie het [toegangsbeheeroverzicht](../access-control/home.md) voor meer informatie.