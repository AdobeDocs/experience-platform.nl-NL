---
keywords: Experience Platform;home;populaire onderwerpen;sandbox;sandbox;testen;testen
solution: Experience Platform
title: Overzicht van sandboxen
topic-legacy: overview
description: Sandboxen zijn virtuele partities binnen één exemplaar van het Experience Platform, die naadloze integratie met het ontwikkelingsproces van uw digitale ervaringstoepassingen mogelijk maken.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
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

* **Productiesandbox**: Een productiesandbox is bedoeld voor gebruik met profielen in uw productieomgeving. Met Platform kunt u meerdere productie-sandboxen maken om de juiste functionaliteit voor gegevens te bieden terwijl de operationele isolatie behouden blijft. Met deze functie kunt u specifieke productiesandboxen toewijzen aan verschillende bedrijfsonderdelen, merken, projecten of regio&#39;s. De zandbakken van de productie steunen een volume productieprofielen tot uw vergunning [!DNL Profile] verplichting (die cumulatief over al uw geoorloofde productiesanddozen wordt gemeten). U hebt het recht om een gemiddeld profiel met licentie te gebruiken per geautoriseerde [!DNL Profile] (cumulatief gemeten in al uw geautoriseerde productiesandboxen).
* **Ontwikkelingssandbox**: Een ontwikkelingssandbox is een sandbox die uitsluitend kan worden gebruikt voor ontwikkeling en testen met niet-productieprofielen. De zandbakken van de ontwikkeling steunen een volume van non-production profielen tot 10% van uw vergunning [!DNL Profile] verplichting (die cumulatief over al uw erkende ontwikkelingszandbakken wordt gemeten). U hebt recht op maximaal:
   * een gemiddelde rijkheid van het non-production profiel van 75 kilobytes per geautoriseerd niet-productieprofiel (cumulatief gemeten over al uw geautoriseerde ontwikkelingssandboxen);
   * één batchsegmentatietaak per dag, per ontwikkelingssandbox;
   * Een gemiddelde van 120 [!DNL Profile] API vraag, per [!DNL Profile], per jaar (cumulatief die over al uw erkende ontwikkelingszandbakken wordt gemeten.

Een instantie van het Experience Platform steunt veelvoudige productie en ontwikkelingszandbakken, met elke zandbak die zijn eigen onafhankelijke bibliotheek van de middelen van het Platform (met inbegrip van schema&#39;s, datasets, profielen, etc.) handhaaft. Bovendien hebben zowel productie als ontwikkelingszandbakken een terugstellende eigenschap die alle klant-gecreeerde middelen uit de zandbak verwijdert. Ontwikkelingssandboxen kunnen niet worden geconverteerd naar productiesandboxen.

Een standaardlicentie voor Experience Platforms kent u in totaal vijf sandboxen toe, die u kunt classificeren als productie of ontwikkeling. U kunt extra pakketten van 10 sandboxen een licentie geven tot een maximum van 75 sandboxen in totaal. Deze extra sandboxen kunnen worden gebruikt om zowel productie- als ontwikkelingssandboxen te maken. Neem voor meer informatie contact op met uw IMS Org Administrator of uw Adobe-vertegenwoordiger.

Tot slot is de standaardproductiesandbox de eerste productiesandbox die wordt gecreeerd wanneer een IMS Org voor het eerst wordt gecreeerd. Met de standaardproductiesandbox kunt u gegevens van het Platform invoeren of gebruiken en kunt u aanvragen accepteren die geen waarden voor de naam van een sandbox of een sandbox-id bevatten.

>[!NOTE]
>
>Wanneer een sandbox voor het eerst wordt gemaakt, bevat deze geen gegevens. Aangezien elke zandbak zijn eigen geïsoleerde gegevensopslag handhaaft, moeten zij ook hun gegevens onafhankelijk innemen.

Samengevat bieden sandboxen de volgende voordelen:

* **Levenscyclusbeheer** van toepassingen: Maak afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.
* **Project- en merkbeheer**: Toestaan dat meerdere projecten parallel lopen binnen dezelfde IMS-organisatie, terwijl isolatie en toegangsbeheer worden geboden. De toekomstige versies zullen steun voor het opstellen in veelvoudige regio&#39;s verstrekken.
* **Flexibel ontwikkelings-ecosysteem**: Biedt sandboxen op een naadloze, schaalbare en voordelige manier voor exploratie, activering en demonstratie.

## Toegangsbeheer voor sandboxen

Standaard hebben alle gebruikers van een organisatie toegang tot een productiesandbox. Toegang tot niet-productie sandboxen moet worden verleend door een systeembeheerder, productbeheerder of productprofielbeheerder via de [Adobe Admin Console](https://adminconsole.adobe.com).

Voor het weergeven, maken, bijwerken of verwijderen van niet-productiesandboxen moeten gebruikers ook de bevoegdheden van Sandbox-beheer hebben.

Voor meer informatie over het beheren van rollen en toestemmingen voor zandbakken, zie [toegangsbeheer overzicht](../access-control/home.md).

## Sandboxen in de gebruikersinterface van het Experience Platform

In de [gebruikersinterface van het Experience Platform](https://platform.adobe.com), kunnen de gebruikers tussen de zandbakken schakelen zij tot toegang hebben door **zandbakschakelaar** controle op top-left van het scherm te gebruiken.  Gebruikers met de bevoegdheden van Sandboxbeheer hebben ook toegang tot het tabblad **[!UICONTROL Sandboxes]** in de linkernavigatie, waar ze sandboxen voor hun organisatie kunnen weergeven en beheren. Zie de [Gebruikershandleiding voor sandboxen](ui/overview.md) voor meer informatie over het werken met sandboxen in de gebruikersinterface.

## Sandboxen in Experience Platform-API&#39;s

Bij het aanroepen van Experience Platform-API&#39;s moet een naam voor een sandbox worden opgegeven onder de koptekst `x-sandbox-name`. Wanneer u bijvoorbeeld [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) aanroept om alle gegevenssets in de productiefandbox weer te geven, wordt de naam van de sandbox (&quot;prod&quot;) als een header weergegeven in de API-aanvraag:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

Als `x-sandbox-name` niet in een API vraag inbegrepen is, zal het systeem een standaardzandbak in plaats daarvan gebruiken. De beste manier is echter om deze header altijd op te nemen in alle API-aanroepen, zelfs wanneer de standaardsandbox wordt gebruikt. Daarom wordt `x-sandbox-name` in de API-documentatie voor Experience Platform behandeld als een vereiste header.

### Sandbox-API

Met de sandbox-API kunt u sandboxen beheren met behulp van RESTful-API-bewerkingen. Zie de [sandboxontwikkelaarsgids](api/overview.md) voor gedetailleerde informatie over het gebruik van de API, inclusief correct opgemaakte aanvragen en voorbeeldantwoorden.

## Volgende stappen

Door dit document te lezen, hebt u kennis genomen van de belangrijkste concepten met betrekking tot sandboxen in Experience Platform. Zie de [gebruikershandleiding](ui/overview.md) voor de gebruikersinterface of de [ontwikkelaarshandleiding](./api/getting-started.md) voor de API voor gedetailleerde stappen voor het beheren van sandboxen.

Terwijl zandbakken als waardevol hulpmiddel dienen om de milieu&#39;s van het Platform voor uw ontwikkelingsteam te isoleren, kunt u meer korrelige toegangscontrole ook beheren door Adobe Admin Console te gebruiken. Zie [toegangsbeheeroverzicht](../access-control/home.md) voor meer informatie.
