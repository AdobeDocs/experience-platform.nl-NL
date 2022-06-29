---
title: Veelgestelde vragen over Adobe Experience Platform Web SDK
description: Hiermee krijgt u antwoorden op veelgestelde vragen over de Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 95305c0a5df71295e1321eb4c8c28baa66c5d94d
workflow-type: tm+mt
source-wordcount: '1955'
ht-degree: 1%

---

# Veelgestelde vragen

Deze handleiding geeft antwoorden op vragen die vaak worden gesteld over de SDK van Adobe Experience Platform Web.

## Wat is Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK is een JavaScript-bibliotheek aan de clientzijde waarmee klanten van Adobe Experience Cloud kunnen communiceren met de verschillende services in de Experience Cloud.

Het verzendt gegevens op een oplossing-agnostische manier (XDM) naar het Netwerk van de Rand van Adobe Experience Platform, dat dan de gegevens aan oplossing specifieke formaten en bestemmingen in kaart brengt en het in real time verzendt.

**Meer informatie**
[Adobe Summit](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Hoe verschilt Adobe Experience Platform Web SDK van eerdere oplossingen?

### Vóór Adobe Experience Platform SDK

Momenteel moet u verschillende JavaScript-bibliotheken implementeren op basis van elke afzonderlijke oplossing.

* Elke oplossing heeft een eigen JavaScript-bibliotheek, -schema en -domein.
* Geen van deze bibliotheken is gemaakt om met elkaar te werken.
* Bij gebruik in oplossingen en Adobe Experience Platform moeten deze verschillende bibliotheken onderling afhankelijk zijn, waardoor implementatiewrijving optreedt.

Hoewel de markeringen in Platform het zo gemakkelijk mogelijk maken om deze bibliotheken op te stellen en te beheren, zijn er nog kwesties met:

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

**Prestaties:** De web-SDK is kleiner dan alle huidige Adobe-bibliotheken en biedt aanzienlijk snellere paginaladingen.

**Eenvoud:** Met de combinatie van XDM, Web SDK, tags, Experience Edge, Adobe Experience Cloud-oplossingen en Adobe Experience Platform wordt een eenvoudig te begrijpen en eenvoudig te volgen artikel voor gegevensverzameling gemaakt.

* **XDM:** Het oplossing-agnostische schema u gebruikt om gegevens naar Adobe te verzenden. Geen codes meer voor verkenners of vakjes.
* **Adobe Experience Platform Web SDK:** Hiermee kunt u gegevens eenvoudig verzenden naar en ontvangen van Adobe Experience Platform Edge Network.
* **Tags:** Vereenvoudigt plaatsing en configuratie van Web SDK (en om het even welke andere markeringen JavaScript) op een plaats.
* **Geniet van rand:** Verstuur de gegevens gemakkelijk naar Adobe Experience Platform en de oplossingen in het formaat dat zij nodig hebben.
* **Adobe Experience Platform- en Adobe-oplossingen:** Schakel hun waardevoorstel in.

**Besturingselement:** Omdat alle gegevens één enkele en verbonden stroom van gegevens gebruiken, kunt u logisch gezien volgen en controleren hoe de gegevens bij elke milliseconde van zijn reis, aan en van toepassingen kijken.

**Modern en klaar voor de toekomst:** De SDK van het Web en zijn verbinding aan het Netwerk van de Rand van de Ervaring hebben Adobe toegelaten om beduidend te moderniseren hoe Adobe zich met gegevensinzameling, verpersoonlijking, toestemming en de toekomst van derdekoekjes behandelt. (Het laat een eerste partijdomein toe, dat door Adobe wordt beheerd.)

**Tijd-aan-waarde:** Adobe heeft hard gewerkt (en zal blijven) om het zo gemakkelijk mogelijk te maken om Web SDK via markeringen op te stellen en cliënt-zijgegevens aan XDM in kaart te brengen. Nadat dat werk wordt gedaan, kunnen alle andere Adobe oplossingen en de diensten van Adobe Experience Platform worden aangezet of van server-kant. Bijvoorbeeld, als u dit voor Adobe Analytics gebruikt en u Doel of Experience Platform wilt aanzetten, kunt u eenvoudig een knevel op de configuratie van DataStream draaien en die gebruiksgevallen oplichten.

## Wat is Alloy?

Alloy is de codenaam voor het Web SDK van Adobe Experience Platform. Het wordt gebruikt binnen de broncode en filename van SDK, hoewel het Web SDK van Adobe Experience Platform de officiële naam is.

## Moeten klanten Adobe Experience Platform kopen om de [!DNL Web SDK]?

Nee. Elke Adobe Digital Experience-klant kan de Adobe Experience Platform Web SDK gratis gebruiken. Om SDK van het Web te gebruiken, moet u uw organisatie hebben provisioned voor deze eigenschap. Vul het volgende in als u toegang wilt krijgen [formulier](https://adobe.ly/websdkaccess) en Adobe zal u toegang geven tot [Gebruikersinterface gegevensstromen](datastreams/overview.md) en de gebruikersinterface van Adobe Experience Platform (indien nodig).

Klanten die de [!DNL Web SDK] zal toegang worden verleend om schema&#39;s, datasets, en identiteitsnamespaces in Adobe Experience Platform UI tot stand te brengen.

## Wie zou SDK van het Web moeten gebruiken?

Adobe Experience Platform Web SDK is ontwikkeld voor de volgende personen:

* Adobe Experience Platform-gebruikers
   * Als u gegevens rechtstreeks van een apparaat naar Adobe Experience Platform moet verzenden, is dit de officieel aanbevolen manier.
   * Adobe is zich ervan bewust dat het gebruik van de Adobe Analytics-aansluiting sneller is als de klant al over Adobe Analytics beschikt, maar het is niet de langetermijnstrategie voor gegevensverzameling.

* Klanten met Adobe Experience Cloud-oplossingen
   * Nieuwe Adobe Analytics-, Adobe Audience Manager- en Adobe Target-klanten moeten beginnen met de nieuwe Web SDK en geen oude bibliotheken gebruiken.
   * Bestaande klanten die de meest geoptimaliseerde implementatie mogelijk willen krijgen, moeten de nieuwe Web SDK gebruiken.


## Hoe krijg ik toegang om te beginnen Adobe Experience Platform Web SDK te gebruiken?

De SDK van het Web is momenteel beschikbaar aan het grote publiek en kan worden gebruikt om gegevens naar de producten van Adobe Experience Cloud te verzenden. De capaciteit om gegevens naar derdeoplossingen te verzenden komt in de nabije toekomst. De SDK is gratis, wordt gratis door Adobe gehost en kan worden gedownload, zodat u deze desgewenst gratis op uw eigen servers kunt hosten. Het Web SDK van het Platform van het Web vereist toegang tot configuraties DataStream en Adobe Experience Platform XDM, voor het schema bouwer Adobe om binnenkomende van SDK behoorlijk te behandelen. Als u toegang wilt krijgen, neemt u contact op met de Customer Success Manager (CSM) om het aanvraagproces te starten.

## Welke gebruiksgevallen worden momenteel ondersteund door de Web SDK?

De SDK van het Web evolueert snel. Er wordt gewerkt aan meer gebruiksgevallen. U kunt de [lijst met gebruiksgevallen die momenteel hier worden ondersteund.](https://github.com/adobe/alloy/projects/5)

## Moeten de huidige klanten hun plaatsen in de detailhandel brengen?

Dat hangt ervan af. Adobe Experience Platform Web SDK kan in twee verschillende stijlen worden opgesteld. Een toekomstig migratiedocument zal extra details verstrekken.

* **Nog een tag:** Als de site al is gecodeerd voor oplossingen en u kunt deze niet opnieuw labelen, maar u wilt gegevens naar Adobe Experience Platform Edge Network verzenden voor gebruik van Experience Platforms of naar de volgende functies voor het doorsturen van gebeurtenissen (zie hieronder), kunt u de optie `alloy.js` tag naar de site, waar het werkt als &quot;gewoon een andere tag&quot;.

* **Het enige label:** Als u SDK van het Web voor een oplossing van Experience Cloud wilt gebruiken, moet u het voor gebruiken _alles_ van de oplossingen op die pagina. Als uw site bijvoorbeeld al gelabeld is voor Adobe Analytics en u deze wilt gebruiken voor Target, moet u deze zowel voor als voor andere sites in de toekomst gebruiken.

Met andere woorden, als u besluit Adobe Experience Platform Web SDK voor niet-oplossingsgebruikgevallen te gebruiken, kunt u de plaats etiketteren met `alloy.js` en ga verder alsof het een nieuwe oplossing is. Als u het voor Adobe Analytics, Doel, of Audience Manager, of voor toepassingsgebruiksgevallen wilt gebruiken, zou u om het even welke erfeniscode op uw pagina kunnen moeten verwijderen.

## Kan ik de ECID&#39;s migreren wanneer ik Alloy ga gebruiken, zodat mijn websitebezoekers niet beginnen op te dagen als nieuwe bezoekers?

Ja, Adobe Experience Platform Web SDK beschikt over de functie Identiteitsmigratie. Volg de instructies voor ID-migratie in het dialoogvenster [Platform Web SDK-identiteitsdocumentatie](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) voor meer informatie .

## Hoe is SDK van het Web verschillend dan markeringen?

* **Labels in Experience Platform** de apparaatcode beheren. Gebruik hen om de code gemakkelijker op te stellen. Ze zijn vrij en krachtig.

* **Adobe Experience Platform Web SDK** Dit is de officiële naam van de nieuwe code die wordt geïmplementeerd door tags voor het gebruik van Adobe. Het is ook vrij en krachtig.

* **`alloy.js`** is de bestandsnaam van de Adobe Experience Platform Web SDK-code.

## Moet ik markeringen gebruiken om het Web SDK op te stellen?

Nee. U kunt de `alloy.js` bestand zelf.

Echter:

* Adobe Experience Platform Web SDK vereist iets genoemd een identiteitskaart DataStream zodat kan het randnetwerk de stroom identificeren en bepalen wat met de gegevens te doen. Deze id wordt gemaakt in het Experience Platform. Dit betekent niet u de UI van de Inzameling van Gegevens moet gebruiken om eigenschappen tot stand te brengen of de code op te stellen JavaScript, maar u moet markeringen gebruiken om een configuratieidentiteitskaart tot stand te brengen.

* Tags zijn niet alleen de beste beschikbare tag en SDK-manager, maar maken het erg eenvoudig om te implementeren `alloy.js` en kaartgegevens naar XDM-schema&#39;s. Als u besluit geen labels te gebruiken, moet u de implementatie beheren `alloy.js`, het voorkomen, en het in kaart brengen van uw gegevens in XDM alvorens het te verzenden. Dit is een _veel_ moeilijker te verwerken dan het gebruik van labels.

* U wordt aangeraden tags te gebruiken voor de implementatie `alloy.js`, zelfs als het de enige markering is u het voor gebruikt.

## Wat is gebeurtenis door:sturen?

Als u onze SDKs gebruikt en XDM naar de Rand van de Ervaring verzendt, staat deze nieuwe eigenschapgebeurtenis door:sturen u toe om nieuwe server-zijuitbreidingen te installeren en die gegevens in kaart te brengen aan wat-en het te verzenden overal-van ons randnetwerk. Beschouw het als &quot;gegevensverzameling als een service&quot;. Dit zal beschikbaar zijn voor kosten, en als deel van Adobe Experience Platform worden gebundeld.

## Wat is een CNAME of een Domein van de Eerste Partij en waarom maakt het van belang?

Meer informatie over een CNAME is beschikbaar in het dialoogvenster [Adobe-documentatie](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Gebruikt de Adobe Experience Platform Web SDK cookies? Zo ja, welke cookies gebruikt zij?

Ja, gebruikt momenteel SDK van het Web overal tussen 1-4 koekjes afhankelijk van uw implementatie. Hieronder volgt een lijst van de 4 koekjes die u met het Web SDK en de manier zou kunnen zien dat zij worden gebruikt:

**kndct_orgid_identity:** Het identiteitscookie wordt gebruikt om de ECID op te slaan, evenals enige andere informatie met betrekking tot de ECID.

**kndctr_orgid_toestemming:** In dit cookie wordt de voorkeur van de gebruiker voor toestemming voor de website opgeslagen.

**kndctr_orgid_cluster:** In dit cookie wordt het gebied Experience Edge opgeslagen dat de verzoeken van de huidige gebruiker weergeeft. Het gebied wordt gebruikt in de weg URL zodat de Rand van de Ervaring de aanvraag naar het correcte gebied kan leiden. Dit koekje heeft een leven van 30 minuten, zodat als een gebruiker met een verschillend IP adres verbindt, het verzoek aan het dichtste gebied kan worden verpletterd.

Wanneer het gebruiken van SDK van het Web, plaatst het Netwerk van de Rand één of meerdere hierboven koekjes. Het netwerk van de Rand plaatst alle koekjes met `secure` en `sameSite="none"` kenmerken.

Als u momenteel zowel beveiligde als niet-beveiligde secties op uw website hebt, kan dit problemen opleveren met de gebruikersidentificatie. Wanneer een gebruiker van een veilige sectie van de plaats aan een onveilige sectie navigeert, produceert het Netwerk van de Rand een nieuw `ECID` met het verzoek.

## Welke browsers steunt het Web SDK van Adobe Experience Platform?

De SDK van Adobe Experience Platform Web is ontworpen om optimaal te werken in de nieuwste versies van Google Chrome, Safari, Firefox, Internet Explorer 11 en Microsoft Edge Chromium. Het kan lastig zijn om bepaalde functies te gebruiken in oudere versies van browsers.

## Waar kan ik meer informatie krijgen over Adobe Experience Platform Web SDK?

* [Documentatie](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Broncode](https://github.com/adobe/alloy)
