---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Richtlijnen voor het oplossen van problemen met sandboxen
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: f15049ca917818d325b5783c70faaa53ba669aba
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# Richtlijnen voor het oplossen van problemen met sandboxen

Dit document biedt antwoorden op veelgestelde vragen over sandboxen in Adobe Experience Platform. Voor vragen en het oplossen van problemen met betrekking tot andere diensten van de Platform, gelieve te verwijzen naar de het oplossen van problemengids [van het](../landing/troubleshooting.md)Experience Platform.

Sandboxen verdelen één enkele instantie van het Platform in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen. Zie het [sandboxoverzicht](home.md) voor meer informatie.

## Wat is een sandbox?

Sandboxen zijn virtuele partities binnen één instantie van Experience Platform. Elke zandbak handhaaft zijn eigen onafhankelijke bibliotheek van de middelen van het Platform (met inbegrip van schema&#39;s, datasets, profielen, etc.). Alle inhoud en handelingen die in een sandbox worden uitgevoerd, blijven beperkt tot alleen die sandbox en hebben geen invloed op andere sandboxen. Zie het [sandboxoverzicht](home.md) voor meer informatie.

## Welke typen sandboxen zijn beschikbaar en wat zijn de verschillen tussen deze typen?

Het Experience Platform bevat twee sandboxtypen:

* Productiesandbox
* Niet-productiesandbox

Experience Platform biedt één **productiesandbox** die niet kan worden verwijderd of opnieuw ingesteld. Er kan slechts één productiesandbox bestaan voor één enkele instantie van het Platform.

Daarentegen kunnen **niet-productiesandboxen** door sandboxbeheerders voor één Platform-instantie worden gemaakt. Met niet-productiesandboxen kunt u functies testen, experimenten uitvoeren en aangepaste configuraties maken zonder dat dit invloed heeft op de productiesandbox. Daarnaast beschikken niet-productiesandboxen over een functie voor het opnieuw instellen die alle door de klant gemaakte bronnen uit de sandbox verwijdert. Niet-productiesandboxen kunnen niet worden omgezet in productiesandboxen.

Zie het [sandboxoverzicht](./home.md) voor meer informatie.

## Kan ik toegang krijgen tot een bron van meerdere sandboxen?

Sandboxen zijn geïsoleerde partities van één Platform-instantie, waarbij elke sandbox zijn eigen onafhankelijke bibliotheek met bronnen behoudt. Een bron die in een sandbox bestaat, kan niet worden benaderd vanuit een andere sandbox, ongeacht het type sandbox (productie of niet-productie).

## Hoeveel productiesandboxen kan ik hebben?

Experience Platform ondersteunt slechts één productiesandbox per IMS-organisatie, die buiten de box wordt geleverd. Hoewel de naam van de productiesandbox kan worden gewijzigd, kan deze niet worden verwijderd of opnieuw ingesteld. De gebruikers met de toestemmingen van het Beleid Sandbox kunnen slechts tot stand brengen, terugstellen, en schrappen niet-productiezandbakken.

## Hoeveel niet-productiesandboxen kan ik hebben?

Met Experience Platform kunnen momenteel maximaal 15 niet voor productie bestemde sandboxen actief zijn binnen één IMS-organisatie.

## Ik heb zojuist een zandbak gemaakt. Hoe kan ik machtigingen instellen voor de gebruikers die met deze sandbox gaan werken?

De Adobe Admin Console koppelt gebruikers aan sandboxen en machtigingen via het gebruik van **productprofielen**. Nadat u een nieuwe sandbox hebt gemaakt, navigeert u naar het tabblad _Machtigingen_ van het productprofiel waartoe u toegang wilt verlenen en klikt u op **Sandboxen**. Van hieruit kunt u op dezelfde manier als andere machtigingen toegang tot de nieuwe sandbox toevoegen of verwijderen.

Als u unieke machtigingen wilt toevoegen aan gebruikers van een bepaalde sandbox, moet u mogelijk een nieuw productprofiel maken met de desbetreffende sandboxen en machtigingen die zijn toegepast, en die gebruikers toewijzen aan dat profiel.

Zie de gebruikershandleiding voor [toegangsbeheer](../access-control/ui/overview.md) voor meer informatie over het beheer van sandboxen en machtigingen in de Admin Console.