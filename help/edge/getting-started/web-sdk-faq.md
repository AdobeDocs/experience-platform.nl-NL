---
title: Veelgestelde vragen over de SDK van Web
seo-title: Veelgestelde vragen over Adobe Experience Platform Web SDK
description: Veelgestelde vragen over Adobe Experience Platform Web SDK
seo-description: Veelgestelde vragen over Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 8cd9c52acd981c92d3959e12d91ebb65b2c3cec8
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 1%

---


# Veelgestelde vragen over Adobe Experience Platform Web SDK

Deze veelgestelde vragen bevatten vragen die vaak worden gesteld over de Adobe Web SDK/

## Wat is Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK is een JavaScript-bibliotheek aan de clientzijde waarmee klanten van de Adobe Experience Cloud kunnen communiceren met de verschillende services in de Experience Cloud.

Het verzendt gegevens op een oplossing-agnostische manier (XDM) naar het Netwerk van de Rand van Adobe Experience Platform, dat dan de gegevens aan oplossing specifieke formaten en bestemmingen in kaart brengt en het in real time verzendt.

**Meer informatie**[Adobe Top](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Hoe verschilt Adobe Experience Platform Web SDK van eerdere oplossingen?

### Vóór Adobe Experience Platform SDK

Momenteel moet u verschillende JavaScript-bibliotheken implementeren op basis van elke afzonderlijke oplossing.

* Elke oplossing heeft een eigen JavaScript-bibliotheek, -schema en -domein.
* Geen van deze bibliotheken is gemaakt om met elkaar te werken.
* Bij gebruik in oplossingen en Adobe Experience Platform moeten deze verschillende bibliotheken onderling afhankelijk zijn, waardoor implementatiewrijving optreedt.

Hoewel Adobe Experience Platform Launch het zo eenvoudig mogelijk maakt om deze bibliotheken te implementeren en te beheren, zijn er nog steeds problemen met:

* Bibliotheekgrootte (te veel Adobe-code op een pagina)
* Prestaties (het laden van sites duurt te lang)
* Meerdere aanroepen voor één gebruiksgeval
* Wachten op ECID-return vóór personalisatie-aanroepen (veroorzaakt vertraging)
* Gefractioneerde gegevensverzameling (wat is een fout?)
* Schema-verwarring tussen oplossingen (A4T)
* Veel andere minder optimale dingen

Er is momenteel ook geen JavaScript-bibliotheek die gegevens rechtstreeks naar Adobe Experience Platform verzendt.

### Met Adobe Experience Platform Web SDK

De nieuwe SDK van het Web verzendt gegevens voor de volgende oplossingen naar één enkele bestemming (het Netwerk van de Rand van AEP) en lost voor de gemeenschappelijkste bovengenoemde gevallen van het oplossingsgebruik op.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Bezoekers-id
* Adobe Experience Platform

Andere oplossingen zullen later dit jaar volgen.

Adobe Experience Platform Web SDK kan gegevens ook rechtstreeks naar Adobe Experience Platform verzenden. Dit gegeven is in XDM en aan het server-zijoplossingsschema in kaart gebracht.

## Wat is de waarde van deze nieuwe web-SDK?

**Prestaties:** De web-SDK is kleiner dan alle huidige Adobe-bibliotheken en biedt aanzienlijk snellere paginaladingen.

**Eenvoud:** Met de combinatie van XDM, Web SDK, Launch, Experience Edge, Adobe Experience Cloud-oplossingen en Adobe Experience Platform wordt een eenvoudig te begrijpen en eenvoudig te volgen artikel voor gegevensverzameling gemaakt.

* **XDM:** Het oplossing-agnostische schema u gebruikt om gegevens naar Adobe te verzenden. Geen codes meer voor verkenners of vakjes.
* **Web SDK:** Hiermee kunt u eenvoudig gegevens naar het Adobe Experience Platform Edge-netwerk verzenden en ontvangen.
* **Starten:** Vereenvoudigt plaatsing en configuratie van Web SDK (en om het even welke andere markeringen JavaScript) op een plaats.
* **Geniet van rand:** Verstuur de gegevens gemakkelijk naar Adobe Experience Platform en de oplossingen in het formaat dat zij nodig hebben.
* **Adobe Experience Platform- en Adobe-oplossingen:** Schakel hun waardevoorstel in.

**Besturingselement:** Omdat alle gegevens één enkele en verbonden stroom van gegevens gebruiken, kunt u logisch gezien volgen en controleren hoe de gegevens bij elke milliseconde van zijn reis, aan en van toepassingen kijken.

**Modern en klaar voor de toekomst:** De SDK van het Web en zijn verbinding aan het Netwerk van de Rand van de Ervaring hebben Adobe toegelaten om beduidend te moderniseren hoe Adobe zich met gegevensinzameling, verpersoonlijking, toestemming en de toekomst van derdekoekjes behandelt. (Het laat een eerste partijdomein toe, dat door Adobe wordt beheerd.)

**Tijd-aan-waarde:** Adobe heeft hard gewerkt (en zal blijven) om het zo gemakkelijk mogelijk te maken om het Web SDK via Lancering en kaart cliënt-zijgegevens aan XDM op te stellen.  Nadat dat werk wordt gedaan, kunnen alle andere Adobe oplossingen en de diensten van Adobe Experience Platform worden aangezet of van server-kant. Als u dit bijvoorbeeld gebruikt voor Adobe Analytics en u Target of Experience Platform wilt inschakelen, kunt u gewoon een schakeloptie voor de configuratie Experience Edge draaien en die gebruikstoepassingen oplichten.

## Wat is `alloy.js`?

`Alloy.js` is de bestandsnaam voor de Adobe Experience Platform Web SDK. Adobe Experience Platform Web SDK is de officiële naam, maar veel ontwikkelaars noemen het &quot;legering.&quot;

## Moeten klanten Adobe Experience Platform kopen om de SDK van het Web te gebruiken?

Nee. Elke Adobe Digital Experience die klant kan gebruiken. Volledig gratis. Om het even welke klant die SDK van het Web wil gebruiken zal toegang worden verleend om schema&#39;s en datasets in Adobe Experience Platform UI tot stand te brengen.

## Wie zou SDK van het Web moeten gebruiken?

De SDK van het Web van Adobe Experience Platform is ontwikkeld voor de volgende mensen:

* Adobe Experience Platform-gebruikers

   Als u gegevens rechtstreeks van een apparaat naar Adobe Experience Platform moet verzenden, is dit de officieel aanbevolen manier.

   Adobe is zich ervan bewust dat het gebruik van de Adobe Analytics-aansluiting sneller is als de klant al over Adobe Analytics beschikt, maar het is niet de langetermijnstrategie voor gegevensverzameling.

* Klanten met Adobe Experience Cloud-oplossingen

   Nieuwe Adobe Analytics-, Adobe Audience Manager- en Adobe Target-klanten moeten beginnen met de nieuwe Web SDK en geen oude bibliotheken gebruiken.

   Bestaande klanten die de meest geoptimaliseerde implementatie mogelijk willen krijgen, moeten de nieuwe Web SDK gebruiken.


## Hoe krijg ik toegang om te beginnen de SDK van het Web van Adobe Experience Platform te gebruiken?

De SDK van het Web is momenteel beschikbaar aan het grote publiek en kan worden gebruikt om gegevens naar de producten van Adobe Experience Cloud te verzenden. De capaciteit om gegevens naar derdeoplossingen te verzenden komt in de nabije toekomst. Als u toegang tot het Web SDK zou willen krijgen contacteer uw CSM om het verzoekproces te beginnen.

## Welke gebruiksgevallen worden momenteel ondersteund door de Web SDK?

De SDK van het Web evolueert snel. Er wordt gewerkt aan meer gebruiksgevallen. Hier vindt u de [lijst met gebruiksgevallen die momenteel worden ondersteund.](https://github.com/adobe/alloy/projects/5)

## Moeten de huidige klanten hun plaatsen in de detailhandel brengen?

Dat hangt ervan af. De SDK van het Web van Adobe Experience Platform kan in twee verschillende stijlen worden opgesteld. Een toekomstig migratiedocument zal extra details verstrekken.

* **Nog een tag:** Als de site al is gelabeld voor oplossingen en u kunt deze niet opnieuw labelen, maar u wilt gegevens naar het Adobe Experience Platform Edge Network verzenden voor gebruik van Experience Platforms of naar de volgende functies op de server (zie hieronder), kunt u de `alloy.js` tag toevoegen aan de site, waar deze werkt als &quot;gewoon een andere tag&quot;.

* **Het enige label:** Als u het Web SDK voor een oplossing van Experience Cloud wilt gebruiken, moet u het voor _alle_ oplossingen op die pagina gebruiken. Als uw site bijvoorbeeld al is gecodeerd voor Analytics en u deze wilt gebruiken voor Target, moet u deze zowel voor als voor andere sites in de toekomst gebruiken.

Met andere woorden, als u besluit om het Web SDK van Adobe Experience Platform voor niet-oplossingsgebruiksgevallen te gebruiken, kunt u de plaats etiketteren met `alloy.js` en zich bewegen alsof het een nieuwe oplossing is. Als u het voor Adobe Analytics, Doel, of Audience Manager, of voor toepassingsgebruiksgevallen wilt gebruiken, zou u om het even welke erfeniscode op uw pagina kunnen moeten verwijderen.

## Kan ik de ECID&#39;s migreren wanneer ik Alloy ga gebruiken, zodat mijn websitebezoekers niet beginnen op te dagen als nieuwe bezoekers?

Ja, de SDK van het Web van Adobe Experience Platform verstrekt een eigenschap van de Migratie van de Identiteit. Volg de instructies in [dit document](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/identity.html#id-migration) voor meer informatie.

## Hoe is de SDK van het Web anders dan Adobe Experience Platform Launch?

* **Launch** is het apparaatcodebeheer. Gebruik het om de code gemakkelijker op te stellen. Het is vrij en krachtig.

* **Adobe Experience Platform Web SDK** is de officiële naam van de nieuwe code die door Lancering voor het gebruiksgevallen van de Adobe zou worden opgesteld. Het is ook vrij en krachtig.

* **`alloy.js`** is de bestandsnaam van de Adobe Experience Platform Web SDK-code.

## Moet ik Adobe Experience Platform Launch gebruiken om Web SDK op te stellen?

Nee. U kunt het `alloy.js` bestand zelf downloaden.

Echter:

* De Adobe Experience Platform Web SDK vereist iets genoemd een de configuratieidentiteitskaart van de Rand van de Ervaring zodat kan het randnetwerk de stroom identificeren en bepalen wat met de gegevens te doen. Deze id wordt gemaakt in Launch. Dit betekent niet dat u Launch moet gebruiken om eigenschappen te maken of de JavaScript-code te implementeren, maar u moet Launch gebruiken om een configuratie-id te maken.

* Adobe Experience Platform Launch is niet alleen de beste beschikbare tag en SDK-manager, maar maakt het heel eenvoudig om gegevens te implementeren `alloy.js` en toe te wijzen aan XDM-schema&#39;s. Als u besluit om Lancering niet te gebruiken, zult u het opstellen `alloy.js`, het verhinderen, en het in kaart brengen van uw gegevens in XDM moeten beheren alvorens het te verzenden. Dit is een _veel_ lastiger proces dan het gebruiken van Lancering.

* U wordt aangeraden Launch te gebruiken voor implementatie `alloy.js`, zelfs als dit de enige tag is waarvoor u het gebruikt.

## Wat is XDM en moet ik aan het Web SDK gebruiken?

XDM is het gegevensformaat dat wordt gebruikt om gegevens naar Adobe Experience Platform en het Web SDK te verzenden. De documentatie [van SDK van het](https://docs.adobe.com/content/help/en/experience-platform/edge/get-started/quick-start-with-launch.html#prepare-a-schema) Web begeleidt u door hoe te opstelling gemakkelijk een schema dat u aan uw specifieke behoeften kunt dan aanpassen.

## Wat is &quot;Adobe Experience Platform Launch Server Side&quot;?

Later in 2020, zal de Lancering server-kant het door:sturen eigenschappen vrijgeven. Als u onze SDK&#39;s gebruikt en XDM naar de Experience Edge verzendt, kunt u met deze nieuwe functies nieuwe serverextensies installeren en die gegevens toewijzen aan alles—en ze overal verzenden—vanaf ons Edge-netwerk. Beschouw het als &quot;gegevensverzameling als een service&quot;.  Dit zal beschikbaar zijn voor kosten, en als deel van Adobe Experience Platform worden gebundeld.

**Meer informatie**[Adobe Top](https://adobe.bluejeans.com/playback/s/9LhauPOnRSUTYg6RMHAw4oJekhYfOQgdBLlNekVJdWevYktpxqX2IYyl5fz2Wxh9)

## Wat is een CNAME of een Domein van de Eerste Partij en waarom maakt het van belang?

Meer informatie over een CNAME is beschikbaar in de documentatie van [Adobe](https://docs.adobe.com/content/help/en/id-service/using/reference/analytics-reference/cname.html)

## Waar kan ik meer informatie krijgen over Adobe Experience Platform Web SDK?

* [Documentatie](https://docs.adobe.com/content/help/nl-NL/experience-platform/edge/home.html)
* [Broncode](https://github.com/adobe/alloy)
