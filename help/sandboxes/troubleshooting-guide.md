---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Richtlijnen voor het oplossen van problemen met sandboxen
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: f15049ca917818d325b5783c70faaa53ba669aba

---


# Richtlijnen voor het oplossen van problemen met sandboxen

Dit document bevat antwoorden op veelgestelde vragen over sandboxen in het Adobe Experience Platform. Voor vragen en het oplossen van problemen met betrekking tot andere diensten van het Platform, gelieve te verwijzen naar de het oplossen van problemengids [van het Platform van de](../landing/troubleshooting.md)Ervaring.

Sandboxen verdelen één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s om digitale ervaringstoepassingen te ontwikkelen en te evolueren. Zie het [sandboxoverzicht](home.md) voor meer informatie.

## Wat is een sandbox?

Sandboxen zijn virtuele partities binnen één exemplaar van Experience Platform. Elke zandbak handhaaft zijn eigen onafhankelijke bibliotheek van de middelen van het Platform (met inbegrip van schema&#39;s, datasets, profielen, etc.). Alle inhoud en handelingen die in een sandbox worden uitgevoerd, blijven beperkt tot alleen die sandbox en hebben geen invloed op andere sandboxen. Zie het [sandboxoverzicht](home.md) voor meer informatie.

## Welke typen sandboxen zijn beschikbaar en wat zijn de verschillen tussen deze typen?

Er zijn twee sandboxtypen beschikbaar in het Experience Platform:

* Productiesandbox
* Niet-productiesandbox

Experience Platform beschikt over één **productiesandbox** die niet kan worden verwijderd of opnieuw ingesteld. Er kan slechts één productiesandbox bestaan voor één platforminstantie.

Daarentegen kunnen er meerdere **niet-productiesandboxen** worden gemaakt door sandboxbeheerders voor één platforminstantie. Met niet-productiesandboxen kunt u functies testen, experimenten uitvoeren en aangepaste configuraties maken zonder dat dit invloed heeft op de productiesandbox. Daarnaast beschikken niet-productiesandboxen over een functie voor het opnieuw instellen die alle door de klant gemaakte bronnen uit de sandbox verwijdert. Niet-productiesandboxen kunnen niet worden omgezet in productiesandboxen.

Zie het [sandboxoverzicht](./home.md) voor meer informatie.

## Kan ik toegang krijgen tot een bron van meerdere sandboxen?

Sandboxen zijn geïsoleerde partities van één instantie Platform, waarbij elke sandbox zijn eigen onafhankelijke bibliotheek met bronnen behoudt. Een bron die in een sandbox bestaat, kan niet worden benaderd vanuit een andere sandbox, ongeacht het type sandbox (productie of niet-productie).

## Hoeveel productiesandboxen kan ik hebben?

Het Experience Platform ondersteunt slechts één productiesandbox per IMS-organisatie, die buiten de box wordt geleverd. Hoewel de naam van de productiesandbox kan worden gewijzigd, kan deze niet worden verwijderd of opnieuw ingesteld. De gebruikers met de toestemmingen van het Beleid Sandbox kunnen slechts tot stand brengen, terugstellen, en schrappen niet-productiezandbakken.

## Hoeveel niet-productiesandboxen kan ik hebben?

Met het ervaringsplatform kunnen momenteel maximaal 15 niet voor productie bestemde sandboxen actief zijn binnen één IMS-organisatie.

## Ik heb zojuist een zandbak gemaakt. Hoe kan ik machtigingen instellen voor de gebruikers die met deze sandbox gaan werken?

In de Adobe Admin Console worden gebruikers via het gebruik van **productprofielen** gekoppeld aan sandboxen en machtigingen. Nadat u een nieuwe sandbox hebt gemaakt, navigeert u naar het tabblad _Machtigingen_ van het productprofiel waartoe u toegang wilt verlenen en klikt u op **Sandboxen**. Van hieruit kunt u op dezelfde manier als andere machtigingen toegang tot de nieuwe sandbox toevoegen of verwijderen.

Als u unieke machtigingen wilt toevoegen aan gebruikers van een bepaalde sandbox, moet u mogelijk een nieuw productprofiel maken met de desbetreffende sandboxen en machtigingen die zijn toegepast, en die gebruikers toewijzen aan dat profiel.

Zie de gebruikershandleiding voor [toegangsbeheer](../access-control/ui/overview.md) voor meer informatie over het beheer van sandboxen en machtigingen in de beheerconsole.