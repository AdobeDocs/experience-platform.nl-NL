---
keywords: Experience Platform;home;populaire onderwerpen;problemen met sandbox
solution: Experience Platform
title: Handleiding voor probleemoplossing voor sandboxen
description: Dit document bevat antwoorden op veelgestelde vragen over sandboxen in Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 2%

---

# Richtlijnen voor het oplossen van problemen met sandboxen

Dit document bevat antwoorden op veelgestelde vragen over sandboxen in Adobe Experience Platform. Voor vragen en het oplossen van problemen met betrekking tot andere diensten van Experience Platform, gelieve te verwijzen naar de [ het oplossen van problemengids van Experience Platform ](../landing/troubleshooting.md).

Sandboxen verdelen één Experience Platform-instantie in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen. Zie het [sandboxoverzicht](home.md) voor meer informatie.

## Wat is een sandbox?

Sandboxen zijn virtuele partities binnen één instantie van Experience Platform. Elke zandbak handhaaft zijn eigen onafhankelijke bibliotheek van de middelen van Experience Platform (met inbegrip van schema&#39;s, datasets, profielen, etc.). Alle inhoud en handelingen die in een sandbox worden uitgevoerd, blijven beperkt tot alleen die sandbox en hebben geen invloed op andere sandboxen. Zie het [sandboxoverzicht](home.md) voor meer informatie.

## Welke typen sandboxen zijn beschikbaar en wat zijn de verschillen tussen deze typen? {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="Sandbox-type"
>abstract="Het type sandbox geeft aan of dit een productie- of ontwikkelingssandbox is. Productiesandboxen bevatten live data- en ontwikkelingssandboxen die worden gebruikt voor testen en ontwikkelen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html#create" text="Een sandbox maken in de gebruikersinterface"

Er zijn twee sandboxtypen beschikbaar in Experience Platform:

* **zandbak van de Productie**: Een productiestandaard wordt bedoeld om met profielen in uw productiemilieu te worden gebruikt. Met Experience Platform kunt u meerdere productie-sandboxen maken om de juiste functionaliteit voor gegevens te bieden terwijl de operationele isolatie behouden blijft. Met deze functie kunt u specifieke productiesandboxen toewijzen aan verschillende bedrijfsonderdelen, merken, projecten of regio&#39;s. Productiesandboxen ondersteunen een volume productieprofielen tot aan uw gelicentieerde [!DNL Profile] toezegging (cumulatief gemeten over al uw geoorloofde productie-sandboxen). U hebt het recht om uw volledige gelicentieerde Totale Volume van Gegevens te gebruiken (cumulatief die over al uw geautoriseerde productiesanddozen worden gemeten).

* **zandbak van de Ontwikkeling**: Een ontwikkelingszandbak is een zandbak die exclusief voor ontwikkeling en het testen met niet-productieprofielen kan worden gebruikt. Ontwikkelingssandboxen ondersteunen een volume niet-productieprofielen tot 10% van uw gelicentieerde [!DNL Profile] -betrokkenheid (cumulatief gemeten in alle geautoriseerde ontwikkelingssandboxen). U hebt recht op maximaal:
   * één batchsegmentatietaak per dag, per ontwikkelingssandbox;
   * Gemiddeld 120 [!DNL Profile] API-aanroepen per [!DNL Profile] per jaar (cumulatief gemeten in al uw geautoriseerde ontwikkelingssandboxen).

Zie het [sandboxoverzicht](./home.md) voor meer informatie.

## Kan ik toegang krijgen tot een bron van meerdere sandboxen?

Sandboxen zijn geïsoleerde partities van één Experience Platform-instantie, waarbij elke sandbox zijn eigen onafhankelijke bibliotheek met bronnen bijhoudt. Een bron die in een sandbox bestaat, is niet toegankelijk vanuit een andere sandbox, ongeacht het type sandbox (productie of niet-productie).

## Wat is de standaardproductiesandbox?

De standaardproductiesandbox is de eerste productiesandbox die wordt gecreeerd wanneer een organisatie eerst provisioned is. Met de standaardproductiesandbox kunt u gegevens van Experience Platform invoeren of gebruiken en kunt u aanvragen accepteren die geen waarden voor de naam van een sandbox of een sandbox-id bevatten. De standaardproductiesandbox kan worden opnieuw ingesteld maar niet worden verwijderd.

## Hoeveel productiesandboxen kan ik hebben?

Een Experience Platform-instantie ondersteunt meerdere productie- en ontwikkelingssandboxen, waarbij elke sandbox een eigen onafhankelijke bibliotheek met Experience Platform-bronnen bijhoudt (inclusief schema&#39;s, gegevenssets en profielen).

Een Experience Platform-standaardlicentie geeft u in totaal vijf sandboxen, die u kunt indelen als productie of ontwikkeling. U kunt extra pakketten van 10 sandboxen een licentie geven tot een maximum van 75 sandboxen in totaal.

De zandbakken van de productie kunnen worden teruggesteld of worden geschrapt, behalve productiezandbakken die ook door Adobe Analytics voor de [ Analyse van het Apparaat kruis (CDA) ](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=nl) eigenschap worden gebruikt, of als de identiteitsgrafiek binnen het ook wordt ontvangen door Adobe Audience Manager voor de [ Mensen Gebaseerde Eigenschappen (PBD) ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=nl) eigenschap.

U kunt de titel van een productiesandbox bijwerken. De naam van een productiesandbox kan echter niet worden gewijzigd.

>[!NOTE]
>
>De naam van de sandbox wordt gebruikt voor opzoekdoeleinden in API-aanroepen, terwijl de titel van de sandbox als weergavenaam wordt gebruikt.

## Hoeveel ontwikkelingssandboxen kan ik hebben?

In Experience Platform kunnen momenteel maximaal 75 sandboxen (productie en ontwikkeling) actief zijn binnen één organisatie.

Ontwikkelingssandboxen bieden ondersteuning voor functies voor opnieuw instellen en verwijderen.

## Ik heb zojuist een zandbak gemaakt. Hoe kan ik machtigingen instellen voor de gebruikers die met deze sandbox gaan werken?

De Adobe Admin Console koppelt gebruikers aan sandboxen en machtigingen via het gebruik van productprofielen. Na het creëren van een nieuwe zandbak, navigeer aan het **lusje van Toestemmingen** van het productprofiel u toegang tot wenst te verlenen, dan klik **Sandboxes**. Van hieruit kunt u op dezelfde manier als andere machtigingen toegang tot de nieuwe sandbox toevoegen of verwijderen.

Als u unieke machtigingen wilt toevoegen aan gebruikers van een bepaalde sandbox, moet u mogelijk een nieuw productprofiel maken met de desbetreffende sandboxen en machtigingen die zijn toegepast, en die gebruikers toewijzen aan dat profiel.

Zie de [ gebruikershandleiding van de toegangscontrole ](../access-control/ui/overview.md) voor meer informatie bij het beheren van zandbakken en toestemmingen in Admin Console.
