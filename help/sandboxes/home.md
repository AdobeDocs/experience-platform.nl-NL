---
keywords: Experience Platform;home;popular topics;sandbox;Sandbox;testing;Testing
solution: Experience Platform
title: Overzicht van sandboxen
topic: overview
description: Sandboxen zijn virtuele partities binnen één exemplaar van het Experience Platform, die naadloze integratie met het ontwikkelingsproces van uw digitale ervaringstoepassingen mogelijk maken.
translation-type: tm+mt
source-git-commit: fa667d86c089c692f22cfd1b46f3f11b6e9a68d7
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 0%

---


# Overzicht van sandboxen

Adobe Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen.

Om aan deze behoefte tegemoet te komen, biedt Experience Platform sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Dit document biedt een overzicht op hoog niveau van sandboxen in Experience Platform.

## Sandboxen

Sandboxen zijn virtuele partities binnen één exemplaar van het Experience Platform, die naadloze integratie met het ontwikkelingsproces van uw digitale ervaringstoepassingen mogelijk maken. Een instantie van het Experience Platform steunt één productie zandbak en veelvoudige niet productiesandboxen, waarbij elke zandbak zijn eigen onafhankelijke bibliotheek van de middelen van het Platform (met inbegrip van schema&#39;s, datasets, profielen, etc.) handhaaft.  Alle inhoud en handelingen die in een sandbox worden uitgevoerd, blijven beperkt tot alleen die sandbox en hebben geen invloed op andere sandboxen.

Met niet-productiesandboxen kunt u functies testen, experimenten uitvoeren en aangepaste configuraties maken zonder dat dit invloed heeft op de productiesandbox. Daarnaast beschikken niet-productiesandboxen over een functie voor het opnieuw instellen die alle door de klant gemaakte bronnen uit de sandbox verwijdert. Niet-productiesandboxen kunnen niet worden omgezet in productiesandboxen. Een standaardlicentie voor Experience Platforms geeft u vijf sandboxen (één productie en vier niet-productie). U kunt in totaal maximaal 75 sandboxen toevoegen aan pakketten van tien niet-productiesandboxen. Neem voor meer informatie contact op met uw IMS Org Administrator of uw Adobe-vertegenwoordiger.

>[!NOTE]
>
>Wanneer een sandbox voor het eerst wordt gemaakt, bevat deze geen gegevens. Aangezien elke zandbak zijn eigen geïsoleerde gegevensopslag handhaaft, moeten zij ook hun gegevens onafhankelijk innemen.

Samengevat bieden sandboxen de volgende voordelen:

* **Levenscyclusbeheer** van toepassingen: Maak afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.
* **Project- en merkbeheer**: Toestaan dat meerdere projecten parallel lopen binnen dezelfde IMS-organisatie, terwijl isolatie en toegangsbeheer worden geboden. De toekomstige versies zullen steun voor het opstellen in veelvoudige regio&#39;s verstrekken.
* **Flexibel ontwikkelings-ecosysteem**: Biedt sandboxen op een naadloze, schaalbare en voordelige manier voor exploratie, activering en demonstratie.

## Toegangsbeheer voor sandboxen

Standaard hebben alle gebruikers van een organisatie toegang tot een productiesandbox. Toegang tot niet-productiesandboxen moet worden verleend door een systeembeheerder, productbeheerder of productprofielbeheerder via de [Adobe Admin Console](https://adminconsole.adobe.com).

Voor het weergeven, maken, bijwerken of verwijderen van niet-productiesandboxen moeten gebruikers ook de bevoegdheden van Sandbox-beheer hebben.

Voor meer informatie over het beheren van rollen en toestemmingen voor zandbakken, zie het overzicht [van de](../access-control/home.md)toegangscontrole.

## Sandboxen in de gebruikersinterface van het Experience Platform

In de gebruikersinterface [van het](https://platform.adobe.com)Experience Platform, kunnen de gebruikers tussen de zandbakken schakelen zij tot toegang hebben door de **zandbakschakelaar** op de top-left van het scherm te gebruiken.  Gebruikers met bevoegdheden voor Sandboxbeheer hebben ook toegang tot het tabblad **[!UICONTROL Sandboxen]** in de linkernavigatie, waar ze sandboxen voor hun organisatie kunnen weergeven en beheren. Raadpleeg de gebruikershandleiding bij de [sandbox voor meer informatie over het werken met sandboxen in de gebruikersinterface](ui/overview.md).

## Sandboxen in Experience Platform-API&#39;s

Bij het aanroepen van Experience Platform-API&#39;s moet een naam voor de sandbox worden opgegeven onder de koptekst `x-sandbox-name`. Wanneer u bijvoorbeeld een aanroep naar de component maakt [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) om alle gegevenssets in de productiesandbox weer te geven, wordt de naam van de sandbox (&quot;prod&quot;) als een header weergegeven in de API-aanvraag:

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

Door dit document te lezen, hebt u kennis genomen van de belangrijkste concepten met betrekking tot sandboxen in Experience Platform. Zie de [gebruikershandleiding](ui/overview.md) voor de gebruikersinterface of de [ontwikkelaarsgids](./api/getting-started.md) voor de API voor gedetailleerde stappen voor het beheren van sandboxen.

Terwijl zandbakken als waardevol hulpmiddel dienen om de milieu&#39;s van het Platform voor uw ontwikkelingsteam te isoleren, kunt u meer korrelige toegangscontrole ook beheren door Adobe Admin Console te gebruiken. Zie het [toegangsbeheeroverzicht](../access-control/home.md) voor meer informatie.