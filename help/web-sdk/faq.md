---
title: Veelgestelde vragen over Adobe Experience Platform Web SDK
description: Hiermee krijgt u antwoorden op veelgestelde vragen over de Adobe Experience Platform Web SDK.
source-git-commit: ed22c76b2805f1baab2ae3c82e1133e1fd8c9f72
workflow-type: tm+mt
source-wordcount: '2033'
ht-degree: 1%

---


# Veelgestelde vragen

Deze handleiding geeft antwoorden op vragen die vaak worden gesteld over de SDK van Adobe Experience Platform Web.

## Wat is Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK is een client-side JavaScript-bibliotheek waarmee u kunt communiceren met de verschillende services in Adobe Experience Cloud.

SDK van het Web verzendt gegevens op een oplossing-agnostische manier (XDM) naar de Edge Network van het Experience Platform, die dan de gegevens aan oplossing-specifieke formaten en bestemmingen in real time in kaart brengt en het verzendt.

Zie de volgende video voor meer informatie over het Web SDK: [ ontmoeten Alloy.js en nooit markering voor een eVar of Mbox opnieuw ](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html).

## Hoe verschilt Adobe Experience Platform Web SDK van eerdere oplossingen?

### Voorafgaand aan Experience Platform Web SDK

Momenteel moet u verschillende JavaScript-bibliotheken implementeren op basis van elke afzonderlijke oplossing.

* Elke oplossing heeft zijn eigen bibliotheek, schema, en domein van JavaScript.
* Geen van deze bibliotheken is gemaakt om met elkaar te werken.
* Bij gebruik in oplossingen en Adobe Experience Platform moeten deze verschillende bibliotheken onderling afhankelijk zijn, waardoor implementatiewrijving optreedt.

Hoewel de markeringen in Platform het zo gemakkelijk mogelijk maken om deze bibliotheken op te stellen en te beheren, zijn er nog kwesties met:

* Bibliotheekgrootte (te veel Adobe code op een pagina)
* Prestaties (het laden van sites duurt te lang)
* Meerdere aanroepen voor één gebruiksgeval
* Wachten op ECID-return vóór personalisatie-aanroepen (veroorzaakt vertraging)
* Gefractioneerde gegevensverzameling (wat is een fout?)
* Schema-verwarring tussen oplossingen (A4T)
* Veel andere minder optimale dingen

Er is momenteel ook geen JavaScript-bibliotheek die gegevens rechtstreeks naar Adobe Experience Platform verzendt.

### Met Experience Platform Web SDK

De nieuwe SDK van het Web verzendt gegevens voor de volgende oplossingen naar één enkele bestemming (de Edge Network van het Experience Platform) en lost voor de gemeenschappelijkste bovengenoemde gevallen van het oplossingsgebruik op.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Bezoeker-id
* Adobe Experience Platform

Andere oplossingen zullen volgen.

Adobe Experience Platform Web SDK kan gegevens ook rechtstreeks naar Adobe Experience Platform verzenden. Dit gegeven is in formaat XDM en aan het server-zijoplossingsschema in kaart gebracht.

## Wat is de waarde van dit nieuwe Web SDK?

**Prestaties:** Web SDK is kleiner dan het gebruiken van alle huidige bibliotheken van de Adobe en verstrekt beduidend snellere paginaladingen.

**Eenvoud:** de combinatie XDM, Web SDK, markeringen, Edge Network, de oplossingen van Adobe Experience Cloud, en Adobe Experience Platform leidt tot een makkelijk te begrijpen en eenvoudig-aan-volgt verhaal van de gegevensinzameling.

* **XDM:** het oplossing-agnostische schema u gebruikt om gegevens naar Adobe te verzenden. Geen codes meer voor verkenners of vakjes.
* **SDK van het Web:** maakt het gemakkelijk om gegevens naar de Edge Network van Adobe Experience Platform te verzenden en te ontvangen.
* **Markeringen:** vereenvoudigt plaatsing en configuratie van het Web SDK (en om het even welke andere markeringen van JavaScript) op een plaats.
* **Edge Network:** leidt gemakkelijk de gegevens aan Adobe Experience Platform en de oplossingen in het formaat zij nodig hebben.
* **Adobe Experience Platform en de oplossingen van de Adobe:** laat hun waardevoorstel toe.

**Controle:** omdat alle gegevens één enkele en verbonden stroom van gegevens gebruiken, kunt u logisch gezien volgen en controleren hoe de gegevens in elke milliseconde van zijn reis, aan en van toepassingen kijken.

**Modern en klaar voor de toekomst:** SDK van het Web en zijn verbinding met de Edge Network heeft Adobe toegelaten om beduidend te moderniseren hoe de Adobe gegevensinzameling, verpersoonlijking, toestemming en de toekomst van derdekoekjes behandelt. (Het laat een eerste partijdomein toe, dat door Adobe wordt beheerd.)

**tijd-aan-waarde:** de Adobe heeft hard gewerkt (en zal) blijven om het zo gemakkelijk mogelijk te maken om het Web SDK via markeringen op te stellen en cliënt-zijgegevens in kaart te brengen aan XDM. Nadat dat werk wordt gedaan, kunnen alle andere oplossingen van de Adobe en de diensten van Adobe Experience Platform worden aangezet of van server-kant. Bijvoorbeeld, als u dit voor Adobe Analytics gebruikt en u Doel of Experience Platform wilt aanzetten, kunt u eenvoudig een knevel op de configuratie van DataStream draaien en die gebruiksgevallen oplichten.

## Wat is [!DNL alloy.js]?

[!DNL alloy.js] is de naam van de Web SDK JavaScript-bibliotheek. Er wordt naar verwezen in de SDK-broncode en -bestandsnaam.

## Moeten klanten Adobe Experience Platform kopen om de [!DNL Web SDK] te kunnen gebruiken?

Nee. Elke Adobe Digital Experience klant kan de Adobe Experience Platform Web SDK gratis gebruiken. Klanten die [!DNL Web SDK] wensen te gebruiken zullen de juiste toestemmingen moeten vormen om schema&#39;s, datasets, identiteitsnamespaces, en gegevensstromen in de UI van de Inzameling van Gegevens of UI van het Experience Platform tot stand te brengen.

Voor meer informatie bij het vormen van deze toestemmingen zie onze documentatie over [ het beheer van de toestemmingen van de gegevensinzameling ](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## Wie zou SDK van het Web moeten gebruiken?

Adobe Experience Platform Web SDK is ontwikkeld voor de volgende klanten:

* Adobe Experience Platform-gebruikers
   * Als u gegevens rechtstreeks van een apparaat naar Adobe Experience Platform moet verzenden, is dit de officieel aanbevolen manier.
   * De Adobe is zich ervan bewust dat het gebruik van de Adobe Analytics-connector sneller is als u al Adobe Analytics hebt, maar het is niet de langetermijnstrategie voor gegevensverzameling.

* Klanten met Adobe Experience Cloud-oplossingen
   * Nieuwe Adobe Analytics-, Adobe Audience Manager- en Adobe Target-klanten moeten beginnen met de nieuwe Web SDK en geen oude bibliotheken gebruiken.
   * Bestaande klanten die de meest geoptimaliseerde implementatie mogelijk willen krijgen, moeten de nieuwe Web SDK gebruiken.

## Hoe krijg ik toegang tot het Web SDK?

De SDK van het Web is momenteel beschikbaar aan het grote publiek en kan worden gebruikt om gegevens naar de producten van Adobe Experience Cloud te verzenden. De capaciteit om gegevens naar derdeoplossingen te verzenden komt in de nabije toekomst.

Er zijn geen kosten voor de SDK en deze wordt gratis door de Adobe gehost. Indien nodig, kunt u het downloaden en op uw eigen servers hosten zonder kosten.

SDK van het Web vereist toegang tot [ datastreamconfiguraties ](../datastreams/overview.md) en de Experience Platform [ XDM schemabouwer ](../xdm/tutorials/create-schema-ui.md), zodat de servers van de Adobe binnenkomende gegevens behoorlijk behandelen die uit SDK komen. Als u toegang wilt krijgen, neemt u contact op met het accountteam van de Adobe om het aanvraagproces te starten.

## Welke gebruiksgevallen worden momenteel ondersteund door de Web SDK?

De SDK van het Web evolueert snel. Er wordt gewerkt aan meer gebruiksgevallen. U kunt de [ lijst van gebruiksgevallen vinden momenteel hier gesteund.](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## Moeten de huidige klanten hun plaatsen in de detailhandel brengen?

Het hangt ervan af. Adobe Experience Platform Web SDK kan in twee verschillende stijlen worden opgesteld. Een toekomstig migratiedocument zal extra details verstrekken.

* **enkel nog een markering:** als de plaats reeds voor oplossingen wordt geëtiketteerd en u niet kunt opnieuw coderen, maar u gegevens naar de Edge Network van Adobe Experience Platform voor de gebruiksgevallen van het Experience Platform of de aanstaande gebeurtenis die eigenschappen (zie hieronder) door:sturen wilt verzenden, kunt u de `alloy.js` markering aan de plaats toevoegen, waar het als &quot;enkel een andere markering&quot;werkt.

* **en slechts markering:** als u het Web SDK voor een oplossing van het Experience Cloud wilt gebruiken, moet u het voor _gebruiken allen_ van de oplossingen op die pagina. Als uw site bijvoorbeeld al gelabeld is voor Adobe Analytics en u deze wilt gebruiken voor Target, moet u deze zowel voor als voor andere sites in de toekomst gebruiken.

Met andere woorden, als u besluit om Adobe Experience Platform Web SDK voor niet-oplossingsgebruiksgevallen te gebruiken, kunt u de plaats etiketteren met `alloy.js` en zich bewegen alsof het een nieuwe oplossing is. Als u het voor Adobe Analytics, Doel, of Audience Manager, of voor toepassingsgebruiksgevallen wilt gebruiken, zou u om het even welke erfeniscode op uw pagina kunnen moeten verwijderen.

## Kan ik de ECID&#39;s migreren wanneer ik Web SDK ga gebruiken zodat mijn websitebezoekers niet beginnen op te roepen als nieuwe bezoekers?

Ja, Adobe Experience Platform Web SDK beschikt over de functie Identiteitsmigratie. Volg de instructies voor de migratie van identiteitskaart in de [ identiteitsdocumentatie van SDK van het Web van het Platform ](/help/web-sdk/identity/overview.md#id-migration) voor meer details.

## Hoe is SDK van het Web verschillend dan markeringen?

* **de Markeringen in Experience Platform** leiden de apparatencode. Gebruik hen om de code gemakkelijker op te stellen. Ze zijn vrij en krachtig.

* **SDK van het Web van Adobe Experience Platform** is de officiële naam van de nieuwe code die door markeringen voor de gebruiksgevallen van de Adobe zou worden opgesteld. Het is ook vrij en krachtig.

* **`alloy.js`** is de bestandsnaam van de Adobe Experience Platform Web SDK-code.

## Moet ik markeringen gebruiken om het Web SDK op te stellen?

Nee. U kunt het `alloy.js` -bestand zelf downloaden.

Echter:

* Adobe Experience Platform Web SDK vereist iets genoemd een identiteitskaart DataStream zodat kan het randnetwerk de stroom identificeren en bepalen wat met de gegevens te doen. Deze id wordt gemaakt in het Experience Platform. Dit betekent niet u UI moet gebruiken om eigenschappen tot stand te brengen of de code van JavaScript op te stellen, maar u moet markeringen gebruiken om een configuratie-identiteitskaart tot stand te brengen.

* Tags zijn niet alleen de beste beschikbare tag en SDK-beheer, maar maken het heel eenvoudig om `alloy.js` -gegevens te implementeren en toe te wijzen aan XDM-schema&#39;s. Als u besluit geen tags te gebruiken, moet u de implementatie van `alloy.js` , de gebeurtenis en de toewijzing van uw gegevens aan XDM beheren voordat u deze verzendt. Dit is a _veel_ moeilijker proces dan het gebruiken van markeringen.

* U wordt aangeraden tags te gebruiken om `alloy.js` te implementeren, zelfs als dit de enige tag is waarvoor u deze gebruikt.

## Wat is gebeurtenis door:sturen?

Als u onze SDKs gebruikt en XDM naar de Edge Network verzendt, staat deze nieuwe eigenschapgebeurtenis door:sturen u toe om nieuwe server-zijuitbreidingen te installeren en die gegevens in kaart te brengen aan om het even wat-en het te verzenden overal-van ons randnetwerk. Beschouw het als &quot;gegevensverzameling als een service&quot;. Dit zal beschikbaar zijn voor kosten, en als deel van Adobe Experience Platform worden gebundeld.

## Wat is een CNAME of een Domein van de Eerste Partij en waarom maakt het van belang?

Meer informatie over een NAAM is beschikbaar in de [ documentatie van de Adobe ](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Gebruikt de Adobe Experience Platform Web SDK cookies? Zo ja, welke cookies gebruikt zij?

Ja, gebruikt momenteel SDK van het Web overal tussen één tot zeven koekjes afhankelijk van uw implementatie. Hieronder volgt een lijst van de koekjes die u met het Web SDK en de manier zou kunnen zien dat zij worden gebruikt:

| **Naam** | **maxAge** | **Vriendelijke leeftijd** | **Beschrijving** |
|---|---|---|---|
| **kCt_orgid_identity** | 34128000 | 395 dagen | In het identiteitscookie wordt de ECID opgeslagen, evenals andere informatie over de ECID. |
| **kndctr_orgid_permission_check** | 7200 | 2 uur | Deze op zitting-gebaseerde koekje geeft de server aan om de server van de toestemmingsvoorkeur omhoog te kijken. |
| **kndctr_orgid_permission** | 15552000 | 180 dagen | In dit cookie wordt de voorkeur van de gebruiker voor toestemming voor de website opgeslagen. |
| **kndctr_orgid_cluster** | 1800 | 30 minuten | In dit cookie wordt het gebied met de Edge Network opgeslagen dat de verzoeken van de huidige gebruiker weergeeft. Het gebied wordt gebruikt in de weg URL zodat de Edge Network het verzoek aan het correcte gebied kan leiden. Dit koekje heeft een leven van 30 minuten, zodat als een gebruiker met een verschillend IP adres verbindt, het verzoek aan het dichtste gebied kan worden verpletterd. |
| **mbox** | 63072000 | 2 jaar | Dit cookie wordt weergegeven wanneer de migratie-instelling Doel is ingesteld op true. Dit zal het 3} mbox koekje van het Doel ](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) toestaan om door het Web SDK worden geplaatst.[ |
| **mboxEdgeCluster** | 1800 | 30 minuten | Dit cookie wordt weergegeven wanneer de migratie-instelling Doel is ingesteld op true. Met dit cookie kan de SDK van het Web de juiste Edge-cluster meedelen aan at.js, zodat de doelprofielen synchroon kunnen blijven terwijl gebruikers door een site navigeren. |
| **AMCV_##@AdobeOrg** | 34128000 | 395 dagen | Dit cookie wordt alleen weergegeven wanneer ID-migratie op de Adobe Experience Platform Web SDK is ingeschakeld. Dit koekje helpt wanneer het overgaan naar Web SDK terwijl sommige delen van de plaats nog bezoekor.js gebruiken. Zie [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md) voor meer informatie. |

Wanneer het gebruiken van SDK van het Web, plaatst de Edge Network één of meerdere hierboven koekjes. De Edge Network stelt alle cookies in met de kenmerken `secure` en `sameSite="none"` .

Als u momenteel zowel beveiligde als niet-beveiligde secties op uw website hebt, kan dit problemen opleveren met de gebruikersidentificatie. Wanneer een gebruiker van een beveiligde sectie van de site naar een niet-beveiligde sectie navigeert, genereert de Edge Network een nieuwe `ECID` met de aanvraag.

## Welke browsers steunt het Web SDK van Adobe Experience Platform?

De SDK van Adobe Experience Platform Web is ontworpen om optimaal te werken in de nieuwste versies van Google Chrome, Safari, Firefox en Microsoft Edge Chromium. Het kan lastig zijn om bepaalde functies te gebruiken in oudere versies van browsers of verouderde browsers, zoals Internet Explorer.

## Waar kan ik meer informatie krijgen over Adobe Experience Platform Web SDK?

* [Documentatie](/help/web-sdk/home.md)
* [ de Code van Source ](https://github.com/adobe/alloy)