---
keywords: Experience Platform;home;populaire onderwerpen;sandbox;sandbox;testen;testen
solution: Experience Platform
title: Overzicht van sandboxen
topic-legacy: overview
description: Sandboxen zijn virtuele partities binnen één exemplaar van het Experience Platform, die naadloze integratie met het ontwikkelingsproces van uw digitale ervaringstoepassingen mogelijk maken.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 0%

---

# Overzicht van sandboxen

Adobe Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen.

Om aan deze behoefte tegemoet te komen, biedt Experience Platform sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Dit document biedt een overzicht op hoog niveau van sandboxen in Experience Platform.

## Sandboxen

Sandboxen zijn virtuele partities binnen één exemplaar van het Experience Platform, die naadloze integratie met het ontwikkelingsproces van uw digitale ervaringstoepassingen mogelijk maken. Alle inhoud en handelingen die in een sandbox worden uitgevoerd, blijven beperkt tot alleen die sandbox en hebben geen invloed op andere sandboxen. Er worden twee soorten sandboxen ondersteund op het Experience Platform:

* **Productiesandbox**: Een productiesandbox is bedoeld voor gebruik met profielen in uw productieomgeving. Met Platform kunt u meerdere productie-sandboxen maken om de juiste functionaliteit voor gegevens te bieden terwijl de operationele isolatie behouden blijft. Met deze functie kunt u specifieke productiesandboxen toewijzen aan verschillende bedrijfsonderdelen, merken, projecten of regio&#39;s. Productiesandboxen ondersteunen een volume productieprofielen tot aan uw licentie [!DNL Profile] verbintenis (cumulatief gemeten over al uw geautoriseerde productiesandboxen). U hebt het recht om een gemiddeld profiel met licentie te gebruiken per geautoriseerde [!DNL Profile] (cumulatief gemeten over al uw geoorloofde productie sandboxen).
* **Ontwikkelingssandbox**: Een ontwikkelingssandbox is een sandbox die uitsluitend kan worden gebruikt voor ontwikkeling en testen met niet-productieprofielen. De zandbakken van de ontwikkeling steunen een hoeveelheid non-production profielen tot 10% van uw vergunning [!DNL Profile] verbintenis (cumulatief gemeten over al uw geautoriseerde ontwikkelingssandboxen). U hebt recht op maximaal:
   * een gemiddelde rijkheid van het non-production profiel van 75 kilobytes per geautoriseerd niet-productieprofiel (cumulatief gemeten over al uw geautoriseerde ontwikkelingssandboxen);
   * één batchsegmentatietaak per dag, per ontwikkelingssandbox;
   * Gemiddeld 120 [!DNL Profile] API-aanroepen, per [!DNL Profile], per jaar (cumulatief gemeten over al uw geautoriseerde ontwikkelingssandboxen.

Een instantie van het Experience Platform steunt veelvoudige productie en ontwikkelingszandbakken, met elke zandbak die zijn eigen onafhankelijke bibliotheek van de middelen van het Platform (met inbegrip van schema&#39;s, datasets, profielen, etc.) handhaaft. Bovendien hebben zowel productie als ontwikkelingszandbakken een terugstellende eigenschap die alle klant-gecreeerde middelen uit de zandbak verwijdert. Ontwikkelingssandboxen kunnen niet worden geconverteerd naar productiesandboxen.

Een standaardlicentie voor Experience Platforms kent u in totaal vijf sandboxen toe, die u kunt classificeren als productie of ontwikkeling. U kunt extra pakketten van 10 sandboxen een licentie geven tot een maximum van 75 sandboxen in totaal. Deze extra sandboxen kunnen worden gebruikt om zowel productie- als ontwikkelingssandboxen te maken. Neem voor meer informatie contact op met uw IMS Org Administrator of uw Adobe-vertegenwoordiger.

Tot slot is de standaardproductiesandbox de eerste productiesandbox die wordt gecreeerd wanneer een IMS Org voor het eerst wordt gecreeerd. Met de standaardproductiesandbox kunt u gegevens van het Platform invoeren of gebruiken en kunt u aanvragen accepteren die geen waarden voor de naam van een sandbox of een sandbox-id bevatten.

>[!NOTE]
>
>Wanneer een sandbox voor het eerst wordt gemaakt, bevat deze geen gegevens. Aangezien elke zandbak zijn eigen geïsoleerde gegevensopslag handhaaft, moeten zij ook hun gegevens onafhankelijk innemen.

Samengevat bieden sandboxen de volgende voordelen:

* **Levenscyclusbeheer van toepassingen**: Maak afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.
* **Project- en merkbeheer**: Toestaan dat meerdere projecten parallel lopen binnen dezelfde IMS-organisatie, terwijl isolatie en toegangsbeheer worden geboden. De toekomstige versies zullen steun voor het opstellen in veelvoudige regio&#39;s verstrekken.
* **Flexibele ontwikkeling-ecosysteem**: Biedt sandboxen op een naadloze, schaalbare en voordelige manier voor exploratie, activering en demonstratie.

## Toegangsbeheer voor sandboxen

Standaard hebben alle gebruikers van een organisatie toegang tot een productiesandbox. Toegang tot niet-productiesandboxen moet worden verleend door een systeembeheerder, productbeheerder of productprofielbeheerder via de [Adobe Admin Console](https://adminconsole.adobe.com).

Voor het weergeven, maken, bijwerken of verwijderen van niet-productiesandboxen moeten gebruikers ook de bevoegdheden van Sandbox-beheer hebben.

Voor meer informatie over het beheren van rollen en toestemmingen voor zandbakken, zie [toegangsbeheeroverzicht](../access-control/home.md).

## Sandboxen in de gebruikersinterface van het Experience Platform

In de [Gebruikersinterface Experience Platform](https://platform.adobe.com)kunnen gebruikers schakelen tussen de sandboxen waartoe ze toegang hebben via de **sandboxschakelaar** besturingselementen linksboven in het scherm.  Gebruikers met de bevoegdheden van Sandbox-beheer hebben ook toegang tot **[!UICONTROL Sandboxes]** in de linkernavigatie, waar zij sandboxen voor hun organisatie kunnen bekijken en beheren. Voor meer informatie over het werken met sandboxen in de gebruikersinterface raadpleegt u de [gebruikershandleiding sandbox](ui/overview.md).

## Sandboxen in Experience Platform-API&#39;s

Bij het aanroepen van Experience Platform-API&#39;s moet een sandboxnaam worden opgegeven onder de koptekst `x-sandbox-name`. Wanneer u bijvoorbeeld een aanroep naar de [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) Als u alle gegevenssets in de productiesandbox wilt weergeven, wordt de naam van de sandbox (&quot;prod&quot;) als een header weergegeven in de API-aanvraag:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

Indien `x-sandbox-name` is niet opgenomen in een API-aanroep, gebruikt het systeem in plaats daarvan een standaardsandbox. De beste manier is echter om deze header altijd op te nemen in alle API-aanroepen, zelfs wanneer de standaardsandbox wordt gebruikt. Daarom wordt in de API-documentatie voor Experience Platforms omgegaan met `x-sandbox-name` als een vereiste koptekst.

### Sandbox-API

Met de sandbox-API kunt u sandboxen beheren met behulp van RESTful-API-bewerkingen. Zie de [sandboxontwikkelaarshandleiding](api/overview.md) voor gedetailleerde informatie over het gebruik van de API, waaronder correct opgemaakte aanvragen en voorbeeldantwoorden.

## Volgende stappen

Door dit document te lezen, hebt u kennis genomen van de belangrijkste concepten met betrekking tot sandboxen in Experience Platform. Zie voor gedetailleerde stappen over het beheren van sandboxen de [gebruikershandleiding](ui/overview.md) voor de gebruikersinterface of de [ontwikkelaarsgids](./api/getting-started.md) voor de API.

Terwijl zandbakken als waardevol hulpmiddel dienen om de milieu&#39;s van het Platform voor uw ontwikkelingsteam te isoleren, kunt u meer korrelige toegangscontrole ook beheren door Adobe Admin Console te gebruiken. Zie de [toegangsbeheeroverzicht](../access-control/home.md) voor meer informatie .
