---
keywords: Experience Platform;home;populaire onderwerpen;problemen met sandbox
solution: Experience Platform
title: Handleiding voor probleemoplossing voor sandboxen
description: Dit document bevat antwoorden op veelgestelde vragen over sandboxen in Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 2%

---

# Richtlijnen voor het oplossen van problemen met sandboxen

Dit document bevat antwoorden op veelgestelde vragen over sandboxen in Adobe Experience Platform. Voor vragen en problemen met betrekking tot andere platformservices raadpleegt u de [Handleiding voor het oplossen van problemen met Experience Platforms](../landing/troubleshooting.md).

Sandboxen verdelen één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s om digitale ervaringstoepassingen te ontwikkelen en te evolueren. Zie het [sandboxoverzicht](home.md) voor meer informatie.

## Wat is een sandbox?

Sandboxen zijn virtuele partities binnen één instantie van Experience Platform. Elke zandbak handhaaft zijn eigen onafhankelijke bibliotheek van de middelen van het Platform (met inbegrip van schema&#39;s, datasets, profielen, etc.). Alle inhoud en handelingen die in een sandbox worden uitgevoerd, blijven beperkt tot alleen die sandbox en hebben geen invloed op andere sandboxen. Zie het [sandboxoverzicht](home.md) voor meer informatie.

## Welke typen sandboxen zijn beschikbaar en wat zijn de verschillen tussen deze typen? {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="Sandbox-type"
>abstract="Het type sandbox geeft aan of dit een productie- of ontwikkelingssandbox is. Productiesandboxen bevatten live data- en ontwikkelingssandboxen die worden gebruikt voor testen en ontwikkelen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html#create" text="Een sandbox maken in de gebruikersinterface"

Het Experience Platform bevat twee sandboxtypen:

* **Productiesandbox**: Een productiesandbox moet worden gebruikt met profielen in uw productieomgeving. Met Platform kunt u meerdere productiesandboxen maken om de juiste functionaliteit voor gegevens te bieden terwijl de operationele isolatie behouden blijft. Met deze functie kunt u specifieke productiesandboxen toewijzen aan verschillende bedrijfsonderdelen, merken, projecten of regio&#39;s. Productiesandboxen ondersteunen een volume productieprofielen tot aan uw licentie [!DNL Profile] verbintenis (cumulatief gemeten over al uw geautoriseerde productiesandboxen). U hebt het recht om een gemiddeld profiel met licentie te gebruiken per geautoriseerde [!DNL Profile] (cumulatief gemeten over al uw geoorloofde productie sandboxen).
* **Ontwikkelingssandbox**: Een ontwikkelingssandbox is een sandbox die uitsluitend kan worden gebruikt voor ontwikkeling en testen met niet-productieprofielen. De zandbakken van de ontwikkeling steunen een hoeveelheid non-production profielen tot 10% van uw vergunning [!DNL Profile] verbintenis (cumulatief gemeten over al uw geautoriseerde ontwikkelingssandboxen). U hebt recht op maximaal:
   * een gemiddelde rijkheid van het non-production profiel van 75 kilobytes per geautoriseerd niet-productieprofiel (cumulatief gemeten over al uw geautoriseerde ontwikkelingssandboxen);
   * één batchsegmentatietaak per dag, per ontwikkelingssandbox;
   * Gemiddeld 120 [!DNL Profile] API-aanroepen, per [!DNL Profile], per jaar (cumulatief gemeten over al uw geautoriseerde ontwikkelingssandboxen.

Zie het [sandboxoverzicht](./home.md) voor meer informatie.

## Kan ik toegang krijgen tot een bron van meerdere sandboxen?

Sandboxen zijn geïsoleerde partities van één instantie Platform, waarbij elke sandbox zijn eigen onafhankelijke bibliotheek met bronnen behoudt. Een bron die in een sandbox bestaat, is niet toegankelijk vanuit een andere sandbox, ongeacht het type sandbox (productie of niet-productie).

## Wat is de standaardproductiesandbox?

De standaardproductiesandbox is de eerste productiesandbox die wordt gecreeerd wanneer een organisatie eerst provisioned is. Met de standaardproductiesandbox kunt u gegevens van het platform invoeren of gebruiken en kunt u aanvragen accepteren die geen waarden voor de naam van een sandbox of een sandbox-id bevatten. De standaardproductiesandbox kan worden opnieuw ingesteld maar niet worden verwijderd.

## Hoeveel productiesandboxen kan ik hebben?

Een instantie van het Experience Platform steunt veelvoudige productie en ontwikkelingszandbakken, met elke zandbak die zijn eigen onafhankelijke bibliotheek van de middelen van het Platform (met inbegrip van schema&#39;s, datasets, en profielen) handhaaft.

Een standaardlicentie voor Experience Platforms kent u in totaal vijf sandboxen toe, die u kunt classificeren als productie of ontwikkeling. U kunt extra pakketten van 10 sandboxen een licentie geven tot een maximum van 75 sandboxen in totaal.

De zandbakken van de productie kunnen worden teruggesteld of worden geschrapt, behalve productie zandbakken die ook door Adobe Analytics voor de [Cross-Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=nl) -functie, of als de identiteitsgrafiek die erin wordt gehost, ook door Adobe Audience Manager wordt gebruikt voor de [Op mensen gebaseerde Doelen (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=nl) gebruiken.

U kunt de titel van een productiesandbox bijwerken. De naam van een productiesandbox kan echter niet worden gewijzigd.

>[!NOTE]
>
>De naam van de sandbox wordt gebruikt voor opzoekdoeleinden in API-aanroepen, terwijl de titel van de sandbox als weergavenaam wordt gebruikt.

## Hoeveel ontwikkelingssandboxen kan ik hebben?

Met Experience Platform kunnen momenteel maximaal 75 sandboxen (productie en ontwikkeling) actief zijn binnen één organisatie.

Ontwikkelingssandboxen bieden ondersteuning voor functies voor opnieuw instellen en verwijderen.

## Ik heb zojuist een zandbak gemaakt. Hoe kan ik machtigingen instellen voor de gebruikers die met deze sandbox gaan werken?

De Adobe Admin Console koppelt gebruikers aan sandboxen en machtigingen via het gebruik van productprofielen. Nadat u een nieuwe sandbox hebt gemaakt, navigeert u naar de **Machtigingen** tabblad van het productprofiel waaraan u toegang wilt verlenen, klikt u op **Sandboxen**. Van hieruit kunt u op dezelfde manier als andere machtigingen toegang tot de nieuwe sandbox toevoegen of verwijderen.

Als u unieke machtigingen wilt toevoegen aan gebruikers van een bepaalde sandbox, moet u mogelijk een nieuw productprofiel maken met de desbetreffende sandboxen en machtigingen die zijn toegepast, en die gebruikers toewijzen aan dat profiel.

Zie de [gebruikershandleiding voor toegangsbeheer](../access-control/ui/overview.md) voor meer informatie over het beheer van sandboxen en machtigingen in de Admin Console.
