---
title: Veelgestelde vragen over Adobe Experience Platform Web SDK
description: Hiermee krijgt u antwoorden op veelgestelde vragen over de Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: a8f6bb8c3e35f4c17812ef944440210b7fe3f87b
workflow-type: tm+mt
source-wordcount: '2104'
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

Nee. Elke Adobe Digital Experience-klant kan de Adobe Experience Platform Web SDK gratis gebruiken. Klanten die de [!DNL Web SDK] zal de juiste toestemmingen moeten vormen om schema&#39;s, datasets, identiteitsnamespaces, en gegevensstromen in de Inzameling UI van Gegevens of Experience Platform UI tot stand te brengen.

Voor meer informatie over het configureren van deze machtigingen raadpleegt u onze documentatie over [beheer van gegevensverzamelingsmachtigingen](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).

## Wie zou SDK van het Web moeten gebruiken?

Adobe Experience Platform Web SDK is ontwikkeld voor de volgende personen:

* Adobe Experience Platform-gebruikers
   * Als u gegevens rechtstreeks van een apparaat naar Adobe Experience Platform moet verzenden, is dit de officieel aanbevolen manier.
   * Adobe is zich ervan bewust dat het gebruik van de Adobe Analytics-aansluiting sneller is als de klant al over Adobe Analytics beschikt, maar het is niet de langetermijnstrategie voor gegevensverzameling.

* Klanten met Adobe Experience Cloud-oplossingen
   * Nieuwe Adobe Analytics-, Adobe Audience Manager- en Adobe Target-klanten moeten beginnen met de nieuwe Web SDK en geen oude bibliotheken gebruiken.
   * Bestaande klanten die de meest geoptimaliseerde implementatie mogelijk willen krijgen, moeten de nieuwe Web SDK gebruiken.


## Hoe krijg ik toegang om te beginnen Adobe Experience Platform Web SDK te gebruiken?

De SDK van het Web is momenteel beschikbaar aan het grote publiek en kan worden gebruikt om gegevens naar de producten van Adobe Experience Cloud te verzenden. De capaciteit om gegevens naar derdeoplossingen te verzenden komt in de nabije toekomst. Er zijn geen kosten voor de SDK en deze worden gratis door Adobe gehost. Indien nodig, kunt u het downloaden en op uw eigen servers hosten zonder kosten. Het Web SDK van het Platform van het Web vereist toegang tot configuraties DataStream en Adobe Experience Platform XDM, voor het schema bouwer Adobe om binnenkomende van SDK behoorlijk te behandelen. Als u toegang wilt krijgen, neemt u contact op met uw Adobe-accountteam om het aanvraagproces te starten.

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

* Adobe Experience Platform Web SDK vereist iets genoemd een identiteitskaart DataStream zodat kan het randnetwerk de stroom identificeren en bepalen wat met de gegevens te doen. Deze id wordt gemaakt in het Experience Platform. Dit betekent niet dat u de interface moet gebruiken om eigenschappen te maken of de JavaScript-code te implementeren, maar dat u wel tags moet gebruiken om een configuratie-id te maken.

* Tags zijn niet alleen de beste beschikbare tag en SDK-manager, maar maken het erg eenvoudig om te implementeren `alloy.js` en kaartgegevens naar XDM-schema&#39;s. Als u besluit geen labels te gebruiken, moet u de implementatie beheren `alloy.js`, het voorkomen, en het in kaart brengen van uw gegevens in XDM alvorens het te verzenden. Dit is een _veel_ moeilijker te verwerken dan het gebruik van labels.

* U wordt aangeraden tags te gebruiken voor de implementatie `alloy.js`, zelfs als het de enige markering is u het voor gebruikt.

## Wat is gebeurtenis door:sturen?

Als u onze SDKs gebruikt en XDM naar de Rand van de Ervaring verzendt, staat deze nieuwe eigenschapgebeurtenis door:sturen u toe om nieuwe server-zijuitbreidingen te installeren en die gegevens in kaart te brengen aan wat-en het te verzenden overal-van ons randnetwerk. Beschouw het als &quot;gegevensverzameling als een service&quot;. Dit zal beschikbaar zijn voor kosten, en als deel van Adobe Experience Platform worden gebundeld.

## Wat is een CNAME of een Domein van de Eerste Partij en waarom maakt het van belang?

Meer informatie over een CNAME is beschikbaar in het dialoogvenster [Adobe-documentatie](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Gebruikt de Adobe Experience Platform Web SDK cookies? Zo ja, welke cookies gebruikt zij?

Ja, gebruikt momenteel SDK van het Web overal tussen één tot zeven koekjes afhankelijk van uw implementatie. Hieronder volgt een lijst van de koekjes die u met het Web SDK en de manier zou kunnen zien dat zij worden gebruikt:

| **Naam** | **maxAge** | **Vriendelijke leeftijd** | **Beschrijving** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 dagen | In het identiteitscookie wordt de ECID opgeslagen, evenals andere informatie over de ECID. |
| **kndctr_orgid_permission_check** | 7200 | 2 uur | In dit cookie wordt de voorkeur van de gebruiker voor toestemming voor de website opgeslagen. |
| **kndctr_orgid_permission** | 15552000 | 180 dagen | Deze op zitting-gebaseerde koekje geeft de server aan om de server van de toestemmingsvoorkeur omhoog te kijken. |
| **kndctr_orgid_cluster** | 1800 | 30 minuten | In dit cookie wordt het gebied Experience Edge opgeslagen dat de verzoeken van de huidige gebruiker weergeeft. Het gebied wordt gebruikt in de weg URL zodat de Rand van de Ervaring de aanvraag naar het correcte gebied kan leiden. Dit koekje heeft een leven van 30 minuten, zodat als een gebruiker met een verschillend IP adres verbindt, het verzoek aan het dichtste gebied kan worden verpletterd. |
| **mbox** | 63072000 | 2 jaar | Dit cookie wordt weergegeven wanneer de migratie-instelling Doel is ingesteld op true. Hierdoor wordt het doel [mbox cookie](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) in te stellen door de Web SDK. |
| **mboxEdgeCluster** | 1800 | 30 minuten | Dit cookie wordt weergegeven wanneer de migratie-instelling Doel is ingesteld op true. Met dit cookie kan de SDK van het Web de juiste Edge-cluster meedelen aan at.js, zodat de doelprofielen synchroon kunnen blijven terwijl gebruikers door een site navigeren. |
| **AMCV_##@AdobeOrg** | 34128000 | 395 dagen | Dit cookie wordt alleen weergegeven wanneer ID-migratie op de Adobe Experience Platform Web SDK is ingeschakeld. Dit koekje helpt wanneer het overgaan naar Web SDK terwijl sommige delen van de plaats nog bezoekor.js gebruiken. Zie de [idMigrationEnabled-documentatie](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#identity-options) voor meer informatie over deze instelling. |

Wanneer het gebruiken van SDK van het Web, plaatst het Netwerk van de Rand één of meerdere hierboven koekjes. Het netwerk van de Rand plaatst alle koekjes met `secure` en `sameSite="none"` kenmerken.

Als u momenteel zowel beveiligde als niet-beveiligde secties op uw website hebt, kan dit problemen opleveren met de gebruikersidentificatie. Wanneer een gebruiker van een veilige sectie van de plaats aan een onveilige sectie navigeert, produceert het Netwerk van de Rand een nieuw `ECID` met het verzoek.

## Welke browsers steunt het Web SDK van Adobe Experience Platform?

De SDK van Adobe Experience Platform Web is ontworpen om optimaal te werken in de nieuwste versies van Google Chrome, Safari, Firefox, Internet Explorer 11 en Microsoft Edge Chromium. Het kan lastig zijn om bepaalde functies te gebruiken in oudere versies van browsers.

## Waar kan ik meer informatie krijgen over Adobe Experience Platform Web SDK?

* [Documentatie](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Broncode](https://github.com/adobe/alloy)
