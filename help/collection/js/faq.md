---
title: Veelgestelde vragen over Adobe Experience Platform Web SDK
description: U krijgt antwoorden op veelgestelde vragen over de Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 66105ca19ff1c75f1185b08b70634b7d4a6fd639
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 1%

---

# Veelgestelde vragen

Deze handleiding geeft antwoorden op vragen die vaak worden gesteld over de Adobe Experience Platform Web SDK.

## Hoe verschilt Adobe Experience Platform Web SDK van eerdere oplossingen?

### Voor Experience Platform Web SDK

Momenteel moet u verschillende JavaScript-bibliotheken implementeren op basis van elke afzonderlijke oplossing.

* Elke oplossing heeft zijn eigen bibliotheek, schema, en domein van JavaScript.
* Geen van deze bibliotheken is gemaakt om met elkaar te werken.
* Bij gebruik in oplossingen en Adobe Experience Platform moeten deze verschillende bibliotheken onderling afhankelijk zijn, waardoor implementatiewrijving optreedt.

Hoewel het zo eenvoudig mogelijk is om deze bibliotheken te implementeren en te beheren met tags in Experience Platform, zijn er nog steeds problemen met:

* Bibliotheekgrootte (te veel Adobe-code op een pagina)
* Prestaties (het laden van sites duurt te lang)
* Meerdere aanroepen voor één gebruiksgeval
* Wachten op ECID-return vóór personalisatie-aanroepen (veroorzaakt vertraging)
* Gefractioneerde gegevensverzameling (wat is een fout?)
* Schema-verwarring tussen oplossingen (A4T)
* Veel andere minder optimale dingen

Er is momenteel ook geen JavaScript-bibliotheek die gegevens rechtstreeks naar Adobe Experience Platform verzendt.

### Met Experience Platform Web SDK

Het nieuwe Web SDK verzendt gegevens voor de volgende oplossingen naar één enkele bestemming (Experience Platform Edge Network) en lost voor de gemeenschappelijkste bovengenoemde gevallen van het oplossingsgebruik op.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Bezoeker-id
* Adobe Experience Platform

Andere oplossingen zullen volgen.

Adobe Experience Platform Web SDK kan gegevens ook rechtstreeks naar Adobe Experience Platform verzenden. Dit gegeven is in formaat XDM en aan het server-zijoplossingsschema in kaart gebracht.

## Wat is de waarde van deze nieuwe Web SDK?

**Prestaties:** het Web SDK is kleiner dan het gebruiken van alle huidige bibliotheken van Adobe en verstrekt beduidend snellere paginaladingen.

**Eenvoud:** de combinatie XDM, Web SDK, markeringen, Edge Network, de oplossingen van Adobe Experience Cloud, en Adobe Experience Platform leidt tot een makkelijk te begrijpen en eenvoudig-aan-volgt verhaal van de gegevensinzameling.

* **XDM:** het oplossing-agnostische schema u gebruikt om gegevens naar Adobe te verzenden. Geen codes meer voor verkenners of vakjes.
* **SDK van het Web:** maakt het gemakkelijk om gegevens naar Adobe Experience Platform Edge Network te verzenden en te ontvangen.
* **Markeringen:** vereenvoudigt plaatsing en configuratie van het Web SDK (en om het even welke andere markeringen van JavaScript) op een plaats.
* **Edge Network:** leiden gemakkelijk de gegevens aan Adobe Experience Platform en de oplossingen in het formaat dat zij nodig hebben.
* **de oplossingen van Adobe Experience Platform en van Adobe:** laat hun waardevoorstel toe.

**Controle:** omdat alle gegevens één enkele en verbonden stroom van gegevens gebruiken, kunt u logisch gezien volgen en controleren hoe de gegevens in elke milliseconde van zijn reis, aan en van toepassingen kijken.

**Modern en klaar voor de toekomst:** Het Web SDK en zijn verbinding met Edge Network hebben Adobe toegelaten om beduidend te moderniseren hoe Adobe met gegevensinzameling, verpersoonlijking, toestemming en de toekomst van derdekoekjes behandelt. (Het laat een eerste partijdomein toe, dat door Adobe wordt beheerd.)

**tijd-aan-waarde:** Adobe heeft hard gewerkt (en zal) het zo gemakkelijk mogelijk maken om het Web SDK via markeringen en kaart cliënt-zijgegevens aan XDM op te stellen. Nadat dat werk is voltooid, kunnen alle andere Adobe-oplossingen en Adobe Experience Platform-services aan- of uitgeschakeld worden. Bijvoorbeeld, als u dit voor Adobe Analytics gebruikt en u Doel of Experience Platform wilt aanzetten, kunt u eenvoudig een knevel op de configuratie van de Datasstream draaien en die gebruiksgevallen oplichten.

## Wat is `alloy.js`?

`alloy.js` is de naam van de Web SDK JavaScript-bibliotheek. Er wordt naar verwezen in de SDK-broncode en -bestandsnaam.

## Moeten klanten Adobe Experience Platform kopen om de [!DNL Web SDK] te kunnen gebruiken?

Nee. Elke Adobe Digital Experience-klant kan de Adobe Experience Platform Web SDK gratis gebruiken.

* De klanten die ** hebben geen toegang tot Experience Platform of in real time CDP en wensen te gebruiken [!DNL Web SDK] zullen de juiste toestemmingen moeten vormen om schema&#39;s en gegevensstromen in de Inzameling UI van Gegevens of UI te creëren Experience Platform.
* Klanten die toegang hebben tot Experience Platform of Real-time CDP en [!DNL Web SDK] willen gebruiken, moeten de juiste machtigingen configureren om schema&#39;s, gegevenssets, naamruimten en gegevensstromen te maken in de gebruikersinterface van de gegevensverzameling of de gebruikersinterface van Experience Platform.

Voor meer informatie bij het vormen van deze toestemmingen zie onze documentatie over [&#x200B; het beheer van de toestemmingen van de gegevensinzameling &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## Wie moet de Web SDK gebruiken?

Adobe Experience Platform Web SDK is ontwikkeld voor de volgende klanten:

* Adobe Experience Platform-gebruikers
   * Als u gegevens rechtstreeks van een apparaat naar Adobe Experience Platform moet verzenden, is dit de officieel aanbevolen manier.
   * Adobe is zich ervan bewust dat het gebruik van de Adobe Analytics-connector sneller is als u al Adobe Analytics hebt, maar het is niet de langetermijnstrategie voor gegevensverzameling.

* Klanten met Adobe Experience Cloud-oplossingen
   * Nieuwe Adobe Analytics-, Adobe Audience Manager- en Adobe Target-klanten moeten beginnen met de nieuwe Web SDK en geen oude bibliotheken gebruiken.
   * Bestaande klanten die de meest geoptimaliseerde implementatie mogelijk willen krijgen, moeten de nieuwe Web SDK gebruiken.

## Hoe krijg ik toegang tot het Web SDK?

Het Web SDK is momenteel beschikbaar voor het grote publiek en kan worden gebruikt om gegevens naar Adobe Experience Cloud-producten te verzenden. De capaciteit om gegevens naar derdeoplossingen te verzenden komt in de nabije toekomst.

Er is geen vergoeding voor de SDK en deze wordt gratis door Adobe gehost. Indien nodig, kunt u het downloaden en op uw eigen servers hosten zonder kosten.

SDK van het Web vereist toegang tot [&#x200B; datastreamconfiguraties &#x200B;](/help/datastreams/overview.md) en Experience Platform [&#x200B; XDM schemabouwer &#x200B;](/help/xdm/tutorials/create-schema-ui.md), zodat de servers van Adobe binnenkomende gegevens behoorlijk behandelen die uit SDK komen. Als u toegang wilt krijgen, neemt u contact op met uw Adobe-accountteam om het aanvraagproces te starten.

## Welke gebruiksgevallen worden momenteel ondersteund door de Web SDK?

De Web SDK ontwikkelt zich snel. Er wordt gewerkt aan meer gebruiksgevallen. U kunt de [&#x200B; lijst van gebruiksgevallen vinden momenteel hier gesteund.](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## Moeten de huidige klanten hun plaatsen in de detailhandel brengen?

Het hangt ervan af. Adobe Experience Platform Web SDK kan in twee verschillende stijlen worden geïmplementeerd. Een toekomstig migratiedocument zal extra details verstrekken.

* **enkel nog een markering:** als de plaats reeds voor oplossingen wordt geëtiketteerd en u kunt niet opnieuw coderen, maar u wilt gegevens naar Adobe Experience Platform Edge Network voor Experience Platform gebruiksgevallen of de aanstaande gebeurtenis verzenden die eigenschappen (zie hieronder) door:sturen, kunt u de `alloy.js` markering aan de plaats toevoegen, waar het als &quot;enkel een andere markering&quot;werkt.

* **en slechts markering:** Als u het Web SDK voor een oplossing van Experience Cloud wilt gebruiken, moet u het voor _gebruiken allen_ van de oplossingen op die pagina. Als uw site bijvoorbeeld al gelabeld is voor Adobe Analytics en u deze wilt gebruiken voor Target, moet u deze zowel voor als voor andere sites in de toekomst gebruiken.

Met andere woorden, als u besluit Adobe Experience Platform Web SDK te gebruiken voor niet-oplossingsgevallen, kunt u de site labelen met `alloy.js` en verder gaan alsof het een nieuwe oplossing is. Als u het voor Adobe Analytics, Doel, of Audience Manager, of voor toepassingsgebruiksgevallen wilt gebruiken, zou u om het even welke erfeniscode op uw pagina kunnen moeten verwijderen.

## Kan ik de ECID&#39;s migreren als ik Web SDK ga gebruiken, zodat mijn websitebezoekers niet beginnen op te roepen als nieuwe bezoekers?

Ja, Adobe Experience Platform Web SDK beschikt over de functie Identiteitsmigratie. Volg de instructies voor de migratie van identiteitskaart in de [&#x200B; identiteitsdocumentatie van SDK van het Web van Experience Platform &#x200B;](/help/collection/use-cases/identity/id-overview.md#migrating-visitor-api-ecid) voor meer details.

## Hoe is het Web SDK anders dan tags?

* **de Markeringen in Experience Platform** leiden de apparatencode. Gebruik hen om de code gemakkelijker op te stellen. Ze zijn vrij en krachtig.

* **SDK van het Web van Adobe Experience Platform** is de officiële naam van de nieuwe code die door markeringen voor de gebruiksgevallen van Adobe zou worden opgesteld. Het is ook vrij en krachtig.

* **`alloy.js`** is de bestandsnaam van de Adobe Experience Platform Web SDK-code.

## Moet ik tags gebruiken om het Web SDK te implementeren?

Nee. U kunt het `alloy.js` -bestand zelf downloaden.

Echter:

* Adobe Experience Platform Web SDK vereist iets genoemd een identiteitskaart DataStream zodat kan het randnetwerk de stroom identificeren en bepalen wat met de gegevens te doen. Deze id is gemaakt in Experience Platform. Dit betekent niet u UI moet gebruiken om eigenschappen tot stand te brengen of de code van JavaScript op te stellen, maar u moet markeringen gebruiken om een configuratie-identiteitskaart tot stand te brengen.

* Tags zijn niet alleen de beste beschikbare tag en SDK-manager, maar maken het heel eenvoudig om `alloy.js` -gegevens te implementeren en toe te wijzen aan XDM-schema&#39;s. Als u besluit geen tags te gebruiken, moet u de implementatie van `alloy.js` , de gebeurtenis en de toewijzing van uw gegevens aan XDM beheren voordat u deze verzendt. Dit is a _veel_ moeilijker proces dan het gebruiken van markeringen.

* U wordt aangeraden tags te gebruiken om `alloy.js` te implementeren, zelfs als dit de enige tag is waarvoor u deze gebruikt.

## Wat is gebeurtenis door:sturen?

Als u onze SDKs gebruikt en XDM naar Edge Network verzendt, staat deze nieuwe eigenschapgebeurtenis door:sturen u toe om nieuwe server-zijuitbreidingen te installeren en dat gegeven in kaart te brengen aan om het even wat-en het te verzenden overal-van ons randnetwerk. Beschouw het als &quot;gegevensverzameling als een service&quot;. Dit zal beschikbaar zijn voor kosten, en als deel van Adobe Experience Platform worden gebundeld.

## Wat is een CNAME of een Domein van de Eerste Partij en waarom maakt het van belang?

Zie het [&#x200B; Adobe-Beheerde certificaatprogramma &#x200B;](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert) in de gids van de Diensten van de Kern.

## Gebruikt de Adobe Experience Platform Web SDK cookies? Zo ja, welke cookies gebruikt zij?

Zie {de koekjes van SDK van het Web van Adobe Experience Platform 1} in de gids van de Diensten van de Kern.[&#128279;](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk)

## Welke browsers worden door de Adobe Experience Platform Web SDK ondersteund?

De Adobe Experience Platform Web SDK is ontworpen om optimaal te werken in de nieuwste versies van Google Chrome, Safari, Firefox en Microsoft Edge Chromium. Het kan lastig zijn om bepaalde functies te gebruiken in oudere versies van browsers of verouderde browsers, zoals Internet Explorer.

## Waar kan ik de broncode aan het Web SDK krijgen?

Zie de [&#x200B; plaats van het Alloy &#x200B;](https://github.com/adobe/alloy) op GitHub.
