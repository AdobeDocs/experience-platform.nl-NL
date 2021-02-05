---
keywords: Experience Platform;home;populaire onderwerpen;problemen met sandbox
solution: Experience Platform
title: Handleiding voor probleemoplossing voor sandboxen
topic: troubleshooting guide
description: Dit document bevat antwoorden op veelgestelde vragen over sandboxen in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# Richtlijnen voor het oplossen van problemen met sandboxen

Dit document bevat antwoorden op veelgestelde vragen over sandboxen in Adobe Experience Platform. Raadpleeg de [handleiding voor het oplossen van Experience Platforms](../landing/troubleshooting.md) voor vragen en het oplossen van problemen met betrekking tot andere services van Platforms.

Sandboxen verdelen één enkele instantie van het Platform in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen. Zie het [overzicht van sandboxen](home.md) voor meer informatie.

## Wat is een sandbox?

Sandboxen zijn virtuele partities binnen één instantie van Experience Platform. Elke zandbak handhaaft zijn eigen onafhankelijke bibliotheek van de middelen van het Platform (met inbegrip van schema&#39;s, datasets, profielen, etc.). Alle inhoud en handelingen die in een sandbox worden uitgevoerd, blijven beperkt tot alleen die sandbox en hebben geen invloed op andere sandboxen. Zie het [overzicht van sandboxen](home.md) voor meer informatie.

## Welke typen sandboxen zijn beschikbaar en wat zijn de verschillen tussen deze typen?

Het Experience Platform bevat twee sandboxtypen:

* Productiesandbox
* Niet-productiesandbox

Experience Platform biedt één productiesandbox die niet kan worden verwijderd of opnieuw ingesteld. Er kan slechts één productiesandbox bestaan voor één enkele instantie van het Platform.

Daarentegen kunnen sandboxbeheerders voor één Platform-instantie meerdere niet-productiesandboxen maken. Met niet-productiesandboxen kunt u functies testen, experimenten uitvoeren en aangepaste configuraties maken zonder dat dit invloed heeft op de productiesandbox. Daarnaast beschikken niet-productiesandboxen over een functie voor het opnieuw instellen die alle door de klant gemaakte bronnen uit de sandbox verwijdert. Niet-productiesandboxen kunnen niet worden omgezet in productiesandboxen. Een standaardlicentie voor Experience Platforms geeft u vijf sandboxen (één productie en vier niet-productie). U kunt maximaal 75 sandboxen toevoegen voor maximaal tien niet-productiesandboxen. Neem voor meer informatie contact op met uw IMS Org Administrator of uw Adobe-vertegenwoordiger.

Zie het [overzicht van sandboxen](./home.md) voor meer informatie.

## Kan ik toegang krijgen tot een bron van meerdere sandboxen?

Sandboxen zijn geïsoleerde partities van één Platform-instantie, waarbij elke sandbox zijn eigen onafhankelijke bibliotheek met bronnen behoudt. Een bron die in een sandbox bestaat, kan niet worden benaderd vanuit een andere sandbox, ongeacht het type sandbox (productie of niet-productie).

## Hoeveel productiesandboxen kan ik hebben?

Experience Platform ondersteunt slechts één productiesandbox per IMS-organisatie, die buiten de box wordt geleverd. Hoewel de naam van de productiesandbox kan worden gewijzigd, kan deze niet worden verwijderd of opnieuw ingesteld. De gebruikers met de toestemmingen van het Beleid Sandbox kunnen slechts tot stand brengen, terugstellen, en schrappen niet-productiezandbakken.

## Hoeveel niet-productiesandboxen kan ik hebben?

Met Experience Platform kunnen momenteel maximaal 15 niet voor productie bestemde sandboxen actief zijn binnen één IMS-organisatie.

## Ik heb zojuist een zandbak gemaakt. Hoe kan ik machtigingen instellen voor de gebruikers die met deze sandbox gaan werken?

De Adobe Admin Console koppelt gebruikers aan sandboxen en machtigingen via het gebruik van productprofielen. Nadat u een nieuwe sandbox hebt gemaakt, navigeert u naar het tabblad **Machtigingen** van het productprofiel waartoe u toegang wilt verlenen en klikt u op **Sandboxen**. Van hieruit kunt u op dezelfde manier als andere machtigingen toegang tot de nieuwe sandbox toevoegen of verwijderen.

Als u unieke machtigingen wilt toevoegen aan gebruikers van een bepaalde sandbox, moet u mogelijk een nieuw productprofiel maken met de desbetreffende sandboxen en machtigingen die zijn toegepast, en die gebruikers toewijzen aan dat profiel.

Zie de [gebruikershandleiding voor toegangsbeheer](../access-control/ui/overview.md) voor meer informatie over het beheren van sandboxen en machtigingen in de Admin Console.