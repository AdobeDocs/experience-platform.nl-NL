---
keywords: Experience Platform;home;populaire onderwerpen;sandbox;sandbox;testen;testen
solution: Experience Platform
title: Sandboxoverzicht
description: Sandboxen zijn virtuele partities binnen één exemplaar van Experience Platform, die naadloze integratie met het ontwikkelingsproces van uw digitale ervaringstoepassingen mogelijk maken.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 1%

---

# Overzicht van sandboxen

Adobe Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen.

Om aan deze behoefte tegemoet te komen, biedt Experience Platform sandboxen die één Experience Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Dit document biedt een overzicht op hoog niveau van sandboxen in Experience Platform.

## Sandboxen

Sandboxen zijn virtuele partities binnen één exemplaar van Experience Platform, die naadloze integratie met het ontwikkelingsproces van uw digitale ervaringstoepassingen mogelijk maken. Alle inhoud en handelingen die in een sandbox worden uitgevoerd, blijven beperkt tot alleen die sandbox en hebben geen invloed op andere sandboxen. Op Experience Platform worden twee soorten sandboxen ondersteund:

* **zandbak van de Productie**: Een productiestandaard wordt bedoeld om met profielen in uw productiemilieu te worden gebruikt. Met Experience Platform kunt u meerdere productie-sandboxen maken om de juiste functionaliteit voor gegevens te bieden terwijl de operationele isolatie behouden blijft. Met deze functie kunt u specifieke productiesandboxen toewijzen aan verschillende bedrijfsonderdelen, merken, projecten of regio&#39;s. Productiesandboxen ondersteunen een volume productieprofielen tot aan uw gelicentieerde [!DNL Profile] toezegging (cumulatief gemeten over al uw geoorloofde productie-sandboxen). U hebt het recht om uw volledige gelicentieerde Totale Volume van Gegevens te gebruiken (cumulatief die over al uw geautoriseerde productiesanddozen worden gemeten).

* **zandbak van de Ontwikkeling**: Een ontwikkelingszandbak is een zandbak die exclusief voor ontwikkeling en het testen met niet-productieprofielen kan worden gebruikt. Ontwikkelingssandboxen ondersteunen een volume niet-productieprofielen tot 10% van uw gelicentieerde [!DNL Profile] -betrokkenheid (cumulatief gemeten in alle geautoriseerde ontwikkelingssandboxen). U hebt recht op maximaal:
   * één batchsegmentatietaak per dag, per ontwikkelingssandbox;
   * Gemiddeld 120 [!DNL Profile] API-aanroepen per [!DNL Profile] per jaar (cumulatief gemeten in al uw geautoriseerde ontwikkelingssandboxen).

Een Experience Platform-instantie ondersteunt meerdere productie- en ontwikkelingssandboxen, waarbij elke sandbox een eigen onafhankelijke bibliotheek van Experience Platform-bronnen bijhoudt (zoals schema&#39;s, datasets, profielen, enzovoort). Bovendien hebben zowel productie als ontwikkelingszandbakken een terugstellende eigenschap die alle klant-gecreeerde middelen uit de zandbak verwijdert. Ontwikkelingssandboxen kunnen niet worden geconverteerd naar productiesandboxen.

Een Experience Platform-standaardlicentie geeft u in totaal vijf sandboxen, die u kunt indelen als productie of ontwikkeling. U kunt extra pakketten van 10 sandboxen een licentie geven tot een maximum van 75 sandboxen in totaal. Deze extra sandboxen kunnen worden gebruikt om zowel productie- als ontwikkelingssandboxen te maken. Neem voor meer informatie contact op met uw systeembeheerder van de organisatie of uw Adobe-vertegenwoordiger.

Tot slot is de standaardproductiesandbox de eerste productiesandbox die wordt gecreeerd wanneer een organisatie eerst wordt gecreeerd. Met de standaardproductiesandbox kunt u gegevens van Experience Platform invoeren of gebruiken en kunt u aanvragen accepteren die geen waarden voor de naam van een sandbox of een sandbox-id bevatten.

>[!NOTE]
>
>Wanneer een sandbox voor het eerst wordt gemaakt, bevat deze geen gegevens. Aangezien elke zandbak zijn eigen geïsoleerde gegevensopslag handhaaft, moeten zij ook hun gegevens onafhankelijk innemen.

Samengevat bieden sandboxen de volgende voordelen:

* **Levenscyclusbeheer van de Toepassing**: Creeer afzonderlijke virtuele milieu&#39;s om digitale ervaringstoepassingen te ontwikkelen en te evolueren.
* **Project en merkbeheer**: sta veelvoudige projecten toe om parallel binnen de zelfde organisatie te lopen, terwijl het verstrekken van isolatie en toegangscontrole.
* **Flexibel ontwikkelings ecosysteem**: Verstrek zandbakken op een naadloze, scalable, en rendabele manier voor exploratie, enablement, en demonstratiedoeleinden.

## Toegangsbeheer voor sandboxen

Standaard hebben alle gebruikers van een organisatie toegang tot een productiesandbox. De toegang tot niet productiestanddozen moet door een systeembeheerder, productbeheerder, of de beheerder van het productprofiel door [ Adobe Admin Console ](https://adminconsole.adobe.com) worden verleend.

Voor het weergeven, maken, bijwerken of verwijderen van niet-productiesandboxen moeten gebruikers ook de bevoegdheden van Sandbox-beheer hebben.

Voor meer informatie bij het beheren van rollen en toestemmingen voor zandbakken, zie het [ overzicht van de toegangscontrole ](../access-control/home.md).

## Sandboxen in de gebruikersinterface van Experience Platform

In het [ gebruikersinterface van Experience Platform ](https://platform.adobe.com), kunnen de gebruikers tussen de zandbakken schakelen zij toegang hebben tot door de **zandbakschakelaar** controle op top-left van het scherm te gebruiken.  Gebruikers met bevoegdheden voor Sandboxbeheer hebben ook toegang tot het tabblad **[!UICONTROL Sandboxes]** in de linkernavigatie, waar ze sandboxen voor hun organisatie kunnen weergeven en beheren. Voor meer informatie over hoe te met zandbakken in UI te werken, zie de [ gids van de zandbakgebruiker ](ui/overview.md).

## Sandboxen in Experience Platform API&#39;s

Bij het aanroepen van Experience Platform API&#39;s moet een naam van een sandbox worden opgegeven onder de header `x-sandbox-name` . Bijvoorbeeld, wanneer het doen van een vraag aan [[!DNL Catalog Service API] ](https://www.adobe.io/experience-platform-apis/references/catalog/) om alle datasets binnen de zandbak van de Productie te bekijken, wordt de naam van de zandbak (&quot;prod&quot;) verstrekt als kopbal in het API verzoek:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

Als `x-sandbox-name` niet is opgenomen in een API-aanroep, gebruikt het systeem een standaardsandbox. De beste manier is echter om deze header altijd op te nemen in alle API-aanroepen, zelfs wanneer de standaardsandbox wordt gebruikt. Daarom wordt `x-sandbox-name` in de API-documentatie voor Experience Platform beschouwd als een vereiste header.

### Sandbox-API

Met de sandbox-API kunt u sandboxen beheren met behulp van RESTful-API-bewerkingen. Zie de [ gids van de zandbakontwikkelaar ](api/overview.md) voor gedetailleerde informatie over hoe te om API, met inbegrip van behoorlijk geformatteerde verzoeken en voorbeeldreacties te gebruiken.

## Volgende stappen

Door dit document te lezen, hebt u kennis genomen van de belangrijkste concepten voor sandboxen in Experience Platform. Voor gedetailleerde stappen op hoe te om zandbakken te beheren, zie de [ gebruikersgids ](ui/overview.md) voor UI of de [ ontwikkelaarsgids ](./api/getting-started.md) voor API.

Hoewel sandboxen een waardevol hulpmiddel zijn om Experience Platform-omgevingen voor uw ontwikkelingsteam te isoleren, kunt u ook meer korrelige toegangscontrole beheren met de Adobe Admin Console. Zie het [ overzicht van de toegangscontrole ](../access-control/home.md) voor meer informatie.
