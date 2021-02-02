---
title: Veelgestelde vragen over de SDK van Web
seo-title: Veelgestelde vragen over Adobe Experience Platform Web SDK
description: Veelgestelde vragen over Adobe Experience Platform Web SDK
seo-description: Veelgestelde vragen over Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: f4f0b00dfd324f69aa2b4348740f6e767e86a6de
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 1%

---


# Veelgestelde vragen

Deze veelgestelde vragen bevatten vragen die vaak worden gesteld over de Adobe Web SDK.

## Wat is Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK is een JavaScript-bibliotheek aan de clientzijde waarmee klanten van Adobe Experience Cloud kunnen communiceren met de verschillende services in de Experience Cloud.

Het verzendt gegevens op een oplossing-agnostische manier (XDM) naar het Netwerk van de Rand van Adobe Experience Platform, dat dan de gegevens aan oplossing specifieke formaten en bestemmingen in kaart brengt en het in real time verzendt.

**Meer**
[informatiePresentatie van de Top van Adobe](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

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

De nieuwe SDK van het Web verzendt gegevens voor de volgende oplossingen naar één enkele bestemming (het Netwerk van de Rand van Adobe Experience Platform) en lost voor de gemeenschappelijkste bovengenoemde gevallen van het oplossingsgebruik op.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Bezoekers-id
* Adobe Experience Platform

Andere oplossingen zullen later dit jaar volgen.

Adobe Experience Platform Web SDK kan gegevens ook rechtstreeks naar Adobe Experience Platform verzenden. Dit gegeven is in XDM en aan het server-zijoplossingsschema in kaart gebracht.

## Wat is de waarde van dit nieuwe Web SDK?

**Prestaties:** de SDK van het web is kleiner dan het gebruik van alle huidige Adobe-bibliotheken en biedt aanzienlijk snellere paginaladingen.

**Eenvoudig:** de combinatie van XDM, Web SDK, Experience Platform Launch, Experience Edge, Adobe Experience Cloud-oplossingen en Adobe Experience Platform maakt een eenvoudig te begrijpen en eenvoudig te volgen artikel voor gegevensverzameling.

* **XDM:** Het oplossing-agnostische schema u gebruikt om gegevens naar Adobe te verzenden. Geen codes meer voor verkenners of vakjes.
* **Adobe Experience Platform Web SDK:** maakt het gemakkelijk om gegevens naar Adobe Experience Platform Edge Network te verzenden en te ontvangen.
* **Experience Platform Launch:** vereenvoudigt de implementatie en configuratie van de Web SDK (en andere JavaScript-tags) op een site.
* **Geniet van Edge:de gegevens** gemakkelijk naar Adobe Experience Platform en oplossingen verzenden in de gewenste indeling.
* **Adobe Experience Platform- en Adobe-oplossingen:** hun waardevoorstel inschakelen.

**Controle:** Omdat alle gegevens één enkele en verbonden stroom van gegevens gebruiken, kunt u logisch gezien volgen en controleren hoe de gegevens bij elke milliseconde van zijn reis, aan en van toepassingen kijken.

**Modern en klaar voor de toekomst:** De SDK van het Web en zijn verbinding aan het Netwerk van de Rand van de Ervaring hebben Adobe toegelaten om beduidend te moderniseren hoe Adobe zich met gegevensinzameling, verpersoonlijking, toestemming en de toekomst van derdekoekjes behandelt. (Het laat een eerste partijdomein toe, dat door Adobe wordt beheerd.)

**Tijd-aan-waarde:** Adobe heeft hard gewerkt (en zal) blijven om het zo gemakkelijk mogelijk te maken om het Web SDK via Experience Platform Launch en kaart cliënt-zijgegevens aan XDM op te stellen.  Nadat dat werk wordt gedaan, kunnen alle andere Adobe oplossingen en de diensten van Adobe Experience Platform worden aangezet of van server-kant. Als u dit bijvoorbeeld gebruikt voor Adobe Analytics en u Target of Experience Platform wilt inschakelen, kunt u gewoon een schakeloptie voor de configuratie Experience Edge draaien en die gebruikstoepassingen oplichten.

## Wat is Alloy?

Alloy is de codenaam voor het Web SDK van Adobe Experience Platform. Het wordt gebruikt binnen de broncode en filename van SDK, hoewel het Web SDK van Adobe Experience Platform de officiële naam is.

## Moeten klanten Adobe Experience Platform kopen om de SDK van het Web te gebruiken?

Nee. Elke Adobe Digital Experience die klant kan gebruiken. Volledig gratis. Om het even welke klant die SDK van het Web wil gebruiken zal toegang worden verleend om schema&#39;s en datasets in Adobe Experience Platform UI tot stand te brengen.

## Wie zou SDK van het Web moeten gebruiken?

Adobe Experience Platform Web SDK is ontwikkeld voor de volgende personen:

* Adobe Experience Platform-gebruikers

   Als u gegevens rechtstreeks van een apparaat naar Adobe Experience Platform moet verzenden, is dit de officieel aanbevolen manier.

   Adobe is zich ervan bewust dat het gebruik van de Adobe Analytics-aansluiting sneller is als de klant al over Adobe Analytics beschikt, maar het is niet de langetermijnstrategie voor gegevensverzameling.

* Klanten met Adobe Experience Cloud-oplossingen

   Nieuwe Adobe Analytics-, Adobe Audience Manager- en Adobe Target-klanten moeten beginnen met de nieuwe Web SDK en geen oude bibliotheken gebruiken.

   Bestaande klanten die de meest geoptimaliseerde implementatie mogelijk willen krijgen, moeten de nieuwe Web SDK gebruiken.


## Hoe krijg ik toegang om te beginnen Adobe Experience Platform Web SDK te gebruiken?

De SDK van het Web is momenteel beschikbaar aan het grote publiek en kan worden gebruikt om gegevens naar de producten van Adobe Experience Cloud te verzenden. De capaciteit om gegevens naar derdeoplossingen te verzenden komt in de nabije toekomst. De SDK is gratis, wordt gratis door Adobe gehost en kan worden gedownload, zodat u deze desgewenst gratis op uw eigen servers kunt hosten. De SDK van het Web van het Platform vereist toegang tot de configuraties van het Netwerk van de Rand van het Platform en Adobe Experience Platform XDM bouwer, voor schemaservers om binnenkomende gegevens behoorlijk te behandelen die van SDK komen. Als u toegang wilt krijgen, neemt u contact op met de Customer Success Manager (CSM) om het aanvraagproces te starten.

## Welke gebruiksgevallen worden momenteel ondersteund door de Web SDK?

De SDK van het Web evolueert snel. Er wordt gewerkt aan meer gebruiksgevallen. U kunt de [lijst van momenteel gesteunde gebruiksgevallen hier vinden.](https://github.com/adobe/alloy/projects/5)

## Moeten de huidige klanten hun plaatsen in de detailhandel brengen?

Dat hangt ervan af. Adobe Experience Platform Web SDK kan in twee verschillende stijlen worden opgesteld. Een toekomstig migratiedocument zal extra details verstrekken.

* **Nog een label:** Als de site al is gelabeld voor oplossingen en u kunt de site niet opnieuw labelen, maar u wilt gegevens naar Adobe Experience Platform Edge Network verzenden voor gebruik van Experience Platforms of de komende serverfuncties van het Experience Platform Launch (zie hieronder), kunt u de  `alloy.js` tag toevoegen aan de site, waar deze werkt als &quot;gewoon een andere tag&quot;.

* **De enige tag:** Als u de Web SDK voor een Experience Cloud-oplossing wilt gebruiken, moet u deze voor  __ alle oplossingen op die pagina gebruiken. Als uw site bijvoorbeeld al gelabeld is voor Adobe Analytics en u deze wilt gebruiken voor Target, moet u deze zowel voor als voor andere sites in de toekomst gebruiken.

Met andere woorden, als u besluit om het Web SDK van Adobe Experience Platform voor niet-oplossingsgebruiksgevallen te gebruiken, kunt u de plaats etiketteren met `alloy.js` en zich bewegen alsof het een nieuwe oplossing is. Als u het voor Adobe Analytics, Doel, of Audience Manager, of voor toepassingsgebruiksgevallen wilt gebruiken, zou u om het even welke erfeniscode op uw pagina kunnen moeten verwijderen.

## Kan ik de ECID&#39;s migreren wanneer ik Alloy ga gebruiken, zodat mijn websitebezoekers niet beginnen op te dagen als nieuwe bezoekers?

Ja, Adobe Experience Platform Web SDK beschikt over de functie Identiteitsmigratie. Volg de instructies voor de migratie van identiteitskaart in [de identiteitsdocumentatie van SDK van het Web van het Platform ](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) voor meer details.

## Hoe is de SDK van het Web anders dan Adobe Experience Platform Launch?

* **Experience Platform** start apparaatcodecanager. Gebruik het om de code gemakkelijker op te stellen. Het is vrij en krachtig.

* **Adobe Experience Platform Web** SDK is de officiële naam van de nieuwe code die door Experience Platform Launch voor de gebruiksgevallen van Adobe zou worden opgesteld. Het is ook vrij en krachtig.

* **`alloy.js`** is de bestandsnaam van de Adobe Experience Platform Web SDK-code.

## Moet ik Adobe Experience Platform Launch gebruiken om Web SDK op te stellen?

Nee. U kunt het `alloy.js` dossier zelf downloaden.

Echter:

* Adobe Experience Platform Web SDK vereist iets genoemd een de configuratieidentiteitskaart van de Rand van de Ervaring zodat kan het randnetwerk de stroom identificeren en bepalen wat met de gegevens te doen. Deze id wordt gemaakt in het Experience Platform Launch. Dit betekent niet u Experience Platform Launch moet gebruiken om eigenschappen tot stand te brengen of de code op te stellen JavaScript, maar u moet Experience Platform Launch gebruiken om een configuratie-identiteitskaart tot stand te brengen.

* Adobe Experience Platform Launch is niet alleen de beste beschikbare tag en SDK-manager, maar maakt het erg eenvoudig om `alloy.js` te implementeren en gegevens toe te wijzen aan XDM-schema&#39;s. Als u besluit om Experience Platform Launch niet te gebruiken, zult u het opstellen van `alloy.js`, gebeurtenis, en het in kaart brengen van uw gegevens in XDM moeten beheren alvorens het te verzenden. Dit is een _veel_ moeilijker proces dan het gebruiken van Experience Platform Launch.

* U wordt aangeraden Experience Platform Launch te gebruiken om `alloy.js` te implementeren, zelfs als dit de enige tag is waarvoor u het gebruikt.

## Wat is &quot;Adobe Experience Platform Launch Server Side&quot;?

Later in 2020, zal Experience Platform Launch server-kant het door:sturen eigenschappen vrijgeven. Als u onze SDK&#39;s gebruikt en XDM naar de Experience Edge verzendt, kunt u met deze nieuwe functies nieuwe serverextensies installeren en die gegevens toewijzen aan alles—en ze overal verzenden—vanaf ons Edge-netwerk. Beschouw het als &quot;gegevensverzameling als een service.&quot;  Dit zal beschikbaar zijn voor kosten, en als deel van Adobe Experience Platform worden gebundeld.

## Wat is een CNAME of een Domein van de Eerste Partij en waarom maakt het van belang?

Meer informatie over een CNAME is beschikbaar in de [Adobe documentatie](https://docs.adobe.com/content/help/en/id-service/using/reference/analytics-reference/cname.html)

## Gebruikt de Adobe Experience Platform Web SDK cookies? Zo ja, welke cookies gebruikt zij?

Ja, gebruikt momenteel SDK van het Web overal tussen 1-4 koekjes afhankelijk van uw implementatie. Hieronder volgt een lijst van de 4 koekjes die u met het Web SDK en de manier zou kunnen zien dat zij worden gebruikt:

**kndct_orgid_identity:** Het identiteitscookie wordt gebruikt om de ECID op te slaan, evenals enkele andere informatie met betrekking tot de ECID.

**kCtr_orgid_permission:** In dit cookie wordt de voorkeur van de gebruiker voor toestemming voor de website opgeslagen.

**kCtr_orgid_personalization:** Dit cookie bevat sessiegegevens die Adobe Target gebruikt om webpagina&#39;s aan te passen.

**kndctr_orgid_consentcheck:** Deze op sessie gebaseerde cookie geeft de server de opdracht om de server met voorkeuren voor toestemming op te zoeken.

## Waar kan ik meer informatie krijgen over Adobe Experience Platform Web SDK?

* [Documentatie](https://docs.adobe.com/content/help/nl-NL/experience-platform/edge/home.html)
* [Broncode](https://github.com/adobe/alloy)
