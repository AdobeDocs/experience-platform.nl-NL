---
title: Overzicht van doorzending van gebeurtenissen
description: Leer over gebeurtenis door:sturen in Adobe Experience Platform, die u toestaat om de Edge Network van het Platform te gebruiken om taken uit te voeren zonder uw markeringsimplementatie te veranderen.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: 16f9ee9d14326f857b444c2361b894aca06b04d6
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 0%

---

# Overzicht van het doorsturen van gebeurtenissen

>[!NOTE]
>
>Het door:sturen van gebeurtenissen is een betaalde eigenschap die als deel van het de Verbindingen van Adobe Real-time Customer Data Platform, eerste, of Ultimate dienstenaanbod inbegrepen is.

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Door:sturen van gebeurtenissen in Adobe Experience Platform staat u toe om verzamelde gebeurtenisgegevens naar een bestemming voor server-zijverwerking te verzenden. Het doorsturen van gebeurtenissen vermindert het gewicht van de webpagina en de toepassing door Adobe Experience Platform Edge Network te gebruiken om taken uit te voeren die normaal op de client worden uitgevoerd. Geïmplementeerd op een gelijkaardige manier aan markeringen, gebeurtenis die regels door:sturen kan gegevens omzetten en verzenden naar nieuwe bestemmingen, maar in plaats van het verzenden van dit gegeven van een cliënttoepassing zoals Webbrowser, wordt het verzonden van de servers van de Adobe.

Dit document biedt een overzicht op hoog niveau van het doorsturen van gebeurtenissen in Platform.

![Het door:sturen van de gebeurtenis in het ecosysteem van de gegevensinzameling.](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>Voor informatie over hoe gebeurtenis het door:sturen binnen het ecosysteem van de gegevensinzameling in Platform past, zie [overzicht van gegevensverzameling](../../../collection/home.md).

Het door:sturen van de gebeurtenis gecombineerd met Adobe Experience Platform [Web SDK](/help/web-sdk/home.md) en [Mobile SDK](https://experienceleague.adobe.com/docs/platform-learn/data-collection/mobile-sdk/overview.html) biedt de volgende voordelen:

**Prestaties**:

* Maak één enkele vraag van een pagina die een nuttige lading van gegevens bevat die dan op de serverkant federeert om cliënt-zijnetwerkverkeer te verminderen en een snellere ervaring voor klanten te leveren.
* Verlaag de tijd die het duurt voordat webpagina&#39;s worden geladen om de prestaties van de site te verbeteren.
* Verlaag het aantal vereiste cliënt-zijtechnologieën om uw ervaring te leveren en gegevens naar vele bestemmingen te verzenden.

**Gegevensbeheer**:

* Verhoog de transparantie en controleer welke gegevens naar alle eigenschappen worden verzonden.

## Verschillen tussen het doorsturen van gebeurtenissen en tags {#differences-from-tags}

In termen van configuratie, gebruikt het door:sturen van gebeurtenissen veel van de zelfde concepten zoals markeringen [regels](../managing-resources/rules.md), [gegevenselementen](../managing-resources/data-elements.md), en [extensions](../managing-resources/extensions/overview.md). Het belangrijkste verschil tussen beide kan als volgt worden samengevat:

* Tags **verzamelingen** gebeurtenisgegevens van een website of een systeemeigen mobiele toepassing en deze naar Platform Edge Network verzenden.
* Gebeurtenis doorsturen **send** inkomende gebeurtenisgegevens van de Edge Network van het Platform aan een eindpunt dat een definitieve bestemming of een eindpunt vertegenwoordigt dat gegevens verstrekt die u de originele nuttige lading wilt verrijken met.

Terwijl de markeringen gebeurtenisgegevens direct van uw plaats of inheemse mobiele toepassing gebruikend het Web van het Platform en Mobiele SDKs verzamelt, vereist gebeurtenis het door:sturen gebeurtenisgegevens om reeds door de Edge Network van het Platform worden verzonden om het aan bestemmingen door te sturen. Met andere woorden, moet u het Web van het Platform of Mobiele SDK van het Platform op uw digitale bezit (of door markeringen of het gebruiken van ruwe code) uitvoeren om gebeurtenis te gebruiken door:sturen.

### Eigenschappen {#properties}

Het door:sturen van de gebeurtenis handhaaft zijn eigen opslag van eigenschappen los van markeringen, die u in de UI van het Experience Platform of UI van de Inzameling van Gegevens kunt bekijken door te selecteren **[!UICONTROL Event Forwarding]** in de linkernavigatie.

>[!TIP]
>
>Gebruik in product hulp in het juiste paneel om meer over gebeurtenis te leren door:sturen en extra beschikbare middelen te bekijken.

![Gebeurtenis die eigenschappen in de Inzameling UI door:sturen van Gegevens.](../../images/ui/event-forwarding/overview/properties.png)

Lijst met eigenschappen voor het doorsturen van gebeurtenissen **[!UICONTROL Edge]** als hun platform. Ze maken geen onderscheid tussen web en mobiele apparaten, omdat ze alleen gegevens verwerken die zijn ontvangen van Platform Edge Network, dat zelf gebeurtenisgegevens kan ontvangen van zowel internet- als mobiele platforms.

### Extensies {#extensions}

Het doorsturen van gebeurtenissen heeft een eigen catalogus met compatibele extensies, zoals de [Kern](../../extensions/server/core/overview.md) uitbreiding en [Adobe Cloud Connector](../../extensions/server/cloud-connector/overview.md) extensie. U kunt de beschikbare uitbreidingen voor gebeurtenis bekijken die eigenschappen door:sturen in UI door te selecteren **[!UICONTROL Extensions]** in de linkernavigatie, gevolgd door **[!UICONTROL Catalog]**.

U kunt aanvullende bronnen weergeven die beschikbaar zijn voor meer informatie over deze functie door ![info](../../images/ui/event-forwarding/overview/about.png) in het rechterdeelvenster.

![Gebeurtenis die uitbreidingen in de Inzameling UI door:sturen van Gegevens.](../../images/ui/event-forwarding/overview/extensions.png)

### Gegevenselementen {#data-elements}

De typen gegevenselementen die beschikbaar zijn in het doorsturen van gebeurtenissen zijn beperkt tot de compatibele catalogus [extensions](#extensions) die hen voorzien.

Terwijl de gegevenselementen zelf worden gecreeerd en gevormd de zelfde manier in gebeurtenis door:sturen aangezien zij voor markeringen zijn, zijn er sommige belangrijke syntaxisverschillen wanneer het over hoe zij gegevens van de Edge Network van het Platform van verwijzingen voorzien.

#### Verwijzen naar gegevens van Platform Edge Network {#data-element-path}

Als u wilt verwijzen naar gegevens van de Edge Network Platform, moet u een gegevenselement maken dat een geldig pad naar die gegevens biedt. Selecteer bij het maken van het gegevenselement in de interface **[!UICONTROL Core]** voor de verlenging en **[!UICONTROL Path]** voor het type.

De **[!UICONTROL Path]** waarde voor het gegevenselement moet het patroon volgen `arc.event.{ELEMENT}` (bijvoorbeeld: `arc.event.xdm.web.webPageDetails.URL`). Dit pad moet correct zijn opgegeven om gegevens te kunnen verzenden.

U kunt aanvullende bronnen weergeven die beschikbaar zijn voor meer informatie over deze functie door ![info](../../images/ui/event-forwarding/overview/about.png) in het rechterdeelvenster.

![Voorbeeld van een padgegevenselement voor het doorsturen van gebeurtenissen.](../../images/ui/event-forwarding/overview/data-reference.png)

### Regels {#rules}

Het maken van regels bij het doorsturen van eigenschappen voor gebeurtenissen werkt op vergelijkbare wijze als labels, waarbij het belangrijkste verschil is dat u geen gebeurtenissen als regelcomponenten kunt selecteren. In plaats daarvan verwerkt een gebeurtenis die regel door:sturen alle gebeurtenissen het van ontvangt [datastream](../../../datastreams/overview.md) en stuurt deze evenementen door naar bestemmingen indien aan bepaalde voorwaarden is voldaan.

Bovendien is er een onderbreking van 30 seconden die op één enkele gebeurtenis van toepassing is aangezien het over alle regels (en vandaar alle acties) binnen een gebeurtenis wordt verwerkt die bezit door:sturen. Dit betekent dat alle regels en alle handelingen voor één gebeurtenis binnen dit tijdsbestek moeten worden voltooid.

U kunt aanvullende bronnen weergeven die beschikbaar zijn voor meer informatie over deze functie door ![info](../../images/ui/event-forwarding/overview/about.png) in het rechterdeelvenster.

![Gebeurtenis die regels in de Inzameling UI door:sturen van Gegevens.](../../images/ui/event-forwarding/overview/rules.png)

#### Tokenisering gegevenselement {#tokenization}

In labelregels worden gegevenselementen gekoppeld aan een `%` aan het begin en einde van de naam van het gegevenselement (bijvoorbeeld: `%viewportHeight%`). In gebeurtenis die regels door:sturen, worden de gegevenselementen in plaats daarvan samengevoegd met `{{` aan het begin en `}}` aan het einde van de naam van het gegevenselement (bijvoorbeeld: `{{viewportHeight}}`).

U kunt aanvullende bronnen weergeven die beschikbaar zijn voor meer informatie over deze functie door ![info](../../images/ui/event-forwarding/overview/about.png) in het rechterdeelvenster.

![Voorbeeld van een padgegevenselement voor het doorsturen van gebeurtenissen.](../../images/ui/event-forwarding/overview/tokenization.png)

#### Reeks handelingen {#action-sequencing}

De [!UICONTROL Actions] sectie van een gebeurtenis die regel door:sturen wordt altijd opeenvolgend uitgevoerd. Bijvoorbeeld, als een regel twee acties heeft, zal de tweede actie niet met uitvoering beginnen tot de vorige actie volledig is (en in gevallen waar een reactie van een eindpunt wordt verwacht, heeft dat eindpunt geantwoord). Zorg ervoor dat de volgorde van de handelingen correct is wanneer u een regel opslaat. Deze uitvoeringsvolgorde kan niet asynchroon worden uitgevoerd, zoals wel mogelijk is met labelregels.

## Geheimen {#secrets}

Gebeurtenis door:sturen staat u toe om, geheimen tot stand te brengen te leiden en op te slaan die kunnen worden gebruikt om aan de servers voor authentiek te verklaren die u gegevens verzendt naar. Zie de handleiding op [geheimen](./secrets.md) over de verschillende soorten beschikbare geheime types en hoe zij in UI worden uitgevoerd.

## Video-overzicht {#video}

De volgende video is bedoeld om u te helpen Gebeurtenis door:sturen en de verbindingen van Real-Time CDP beter begrijpen.

>[!VIDEO](https://video.tv.adobe.com/v/3429308)

## Volgende stappen

Dit document verstrekte een inleiding op hoog niveau aan gebeurtenis het door:sturen. Voor meer informatie over hoe te opstelling deze eigenschap voor uw organisatie, zie [gids Aan de slag](./getting-started.md).
