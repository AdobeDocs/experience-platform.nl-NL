---
title: Een Exchange-aanbieding voor een extensie maken
description: Leer hoe u uw extensie toevoegt aan de openbare catalogus in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 0%

---

# Een uitwisselingslijst maken voor een extensie

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Adobe Experience Platform heeft één enkele verenigde catalogus waar de gebruikers markeringsuitbreidingen kunnen bekijken die voor installatie beschikbaar zijn. Deze catalogus is beschikbaar in het product en bevat extensies van drie typen:

1. **Openbare extensies**: Dit zijn voltooide extensies die zijn ontworpen voor productiegebruik door elke gebruiker.
1. **Privéextensies**: Dit zijn voltooide extensies die zijn ontworpen voor productie, maar die zijn ontwikkeld door andere gebruikers in uw bedrijf en die alleen beschikbaar zijn voor gebruikers binnen uw bedrijf.
1. **Uitbreidingen** voor ontwikkeling: Deze uitbreidingen zijn onder actieve ontwikkeling en zijn slechts beschikbaar binnen uw bedrijf en slechts op een bezit dat specifiek als bezit van de Ontwikkeling wordt aangewezen.

Afzonderlijk van de extensies in de productcatalogus hebben sommige extensies ook lijsten in de [Experience Cloud Exchange Marketplace](https://exchange.adobe.com/experiencecloud.experience-platform-launch.html#product).

Met deze aanbiedingen kunnen extensieontwikkelaars beschrijvingen van functies plaatsen, koppelingen naar aanvullende ondersteuning en documentatie aanbieden en extensies op de markt brengen voor toekomstige gebruikers die wellicht niet op de hoogte zijn van uw bedrijf of de functionaliteit van uw extensie. Op deze markt is er een openbare aanbieding voor je extensie die kan worden weergegeven zonder dat de gebruiker op het Platform is geverifieerd.  Vele ontwikkelaars vinden het nuttig om een lijst van de Uitwisseling te ontwikkelen, maar dit is geen vereiste stap.

Als u geen bedrijf hebt om uw extensiepakket te uploaden en te testen, moet u zich registreren voor het Exchange-programma en een aanbieding starten.  Hierdoor wordt een bedrijfsaccount gemaakt (het duurt even voordat u een e-mail ontvangt wanneer deze is voltooid) waarmee u uw extensie kunt uploaden en testen.  Je hoeft de aanbieding nooit openbaar te maken.

Als u al een bedrijfsaccount hebt of als u niet van plan bent om uw aanbieding te voltooien, kunt u de rest van deze stap overslaan en doorgaan met het uploaden en testen van uw extensie](./upload-and-test.md).[

## Een aanbieding maken

>[!NOTE]
>
>Het volgende proces detailleert de verwezenlijking van een toepassingslijst in het programma van de Uitwisseling van de Adobe. Dit is de term die wordt gebruikt voor de verschillende integraties en extensies in Adobe Experience Platform.

![Koppelingslocatie Experience Cloud App Manager](../images/getting-started/app-mgr-link.png)

1. Meld u aan bij de [Exchange Partner-site](https://partners.adobe.com/exchangeprogram/experiencecloud). Als u bent aangemeld, selecteert u de koppeling **App Manager** naast uw naam.
1. Selecteer **Nieuwe toepassing maken** tabel en selecteer **Nieuwe toepassing maken** voor een aangepaste oplossing of selecteer een toepasselijke sjabloon.
1. Geef je objectgegevens op. Voor gedetailleerde informatie over App Manager checkt u het volledige [artikel](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931) uit. De informatie van de lijst zou zeer duidelijk moeten zijn over wat de uitbreiding doet en waarom het nuttig is. Deze aanbieding fungeert als marketingruimte voor uw app. Promoot hier uw extensie met duidelijke beschrijvingen, koppelingen naar bestemmingspagina&#39;s op uw site, koppelingen naar Help-documenten of ondersteuning van e-mailadressen enzovoort. Hoewel de ruimte in uitbreidingsmeningen beperkt is, biedt de lijst van de Uitwisseling een kans om zowel uw uitbreiding als uw bedrijf te bevorderen. Hieronder volgen suggesties om de uitbreiding beter te promoten:
   - **App-pictogram**  - zorg ervoor dat het pictogram voor de Exchange-lijst de juiste afmetingen heeft: 512 x 512 voor png of een hoogte-breedteverhouding van 1:1 voor jpg.

   >[!NOTE]
   >
   >Dit is een andere bestandsindeling dan de extensiecode. De extensie zelf bevat een svg-bestand als het [pictogram](../manifest.md).

   - **Aanbevolen afbeelding**  - Let op met een afbeelding die zelfstandig kan worden gebruikt en uw merk weergeeft en uw toepassing markeert. De aanbevolen afbeelding is de afbeelding die wordt weergegeven wanneer iemand een link naar je aanbieding op de beurs deelt of er berichten over plaatst op sociale media. Het moet daarom een modelweergave van uw merk zijn.
   - **Logo**  van uitgever van app - Dit is uw bedrijfslogo, zorg ervoor het pictogram de aangewezen afmetingen van 1280 x 720, of 2560 x 1440 (16:9) in png of jpg formaat heeft.
   - **Configuratieinstructies**  - Informeer klanten hoe u uw Adobe Experience Platform-extensie kunt configureren. Zorg ervoor zij om het even welke vereiste montages en volgende stappen begrijpen wanneer uw [configuratiemening](../configuration.md) onmiddellijk na het installeren van uw uitbreiding in een bezit verschijnt. 
   - **Tags**  - Op de eerste pagina van het bewerken van je aanbieding moet je het woord &quot;Starten&quot; opnemen in het veld &#39;Aangepaste tags&#39;. Zo wordt je aanbieding weergegeven in zoekopdrachten naar tags op de Exchange-markt:
      ![](../images/getting-started/custom-tags.jpg)
   - **Sandboxen**  - Uw toegang tot Adobe Solutions verloopt via een Sandbox-account, waar u toegang hebt tot een volledig functionerende versie van Adobe Experience Platform. Deze Sandbox-accounts worden aangevraagd terwijl u uw toepassingslijst maakt. Selecteer in de sectie **Verbindingen** de specifieke verbindingen die van toepassing zijn op de toepassing die u hebt gemaakt (uw tagextensie). Wanneer u **Save** kiest, wordt de sandboxaanvraag indien nodig gegenereerd.
1. Verzend je aanbieding. Het team van de Uitwisseling van de Adobe zal uw toepassing herzien en zal verstrekken terugkoppelen als de updates worden vereist. Als u het selectievakje **Publiceren direct** markeert wanneer u uw aanbieding verzendt, wordt deze direct na goedkeuring gepubliceerd. Als u de toepassing later wilt publiceren, schakelt u het selectievakje uit. Wanneer uw extensielijst wordt goedgekeurd, verschijnt er een blauwe knop **Publiceren** naast de pagina in uw app-aanbiedingen (extensie).

### Een effectieve aanbieding maken

Neem een blik bij [de Richtsnoer van de Indiening van de Toepassing](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html) voor gedetailleerde informatie over hoe te om tot de het meest boeiende lijst te leiden.

#### Na het verzenden van je aanbieding op de beurs

Zodra voorgelegd, zal het team van de Uitwisseling van de Adobe de toepassing herzien en of de toepassing goedkeuren, of met commentaren over veranderingen antwoorden. Dit proces wordt beschreven in de richtlijnen voor het indienen van toepassingen.

Als u geen login aan de plaats van de Uitwisseling hebt, zorg ervoor dat uw e-mail voor het programma van de Uitwisseling door de instructies in [Gids van de Registratie van het Programma ](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html) te volgen wordt geregistreerd. Elke gebruiker moet zijn e-mail met de partnerrekening voor hun bedrijf associëren. Vragen over dit proces kunnen via e-mail naar <ExchangeHelpEC@adobe.com> worden gestuurd.

#### Je ruilaanbieding bijwerken na eerste goedkeuring

Wanneer u uw uitbreiding bijwerkt, of enkel uw lijst van de Uitwisseling moet bijwerken, login aan [Partner Portal](https://partners.adobe.com/exchangeprogram/experiencecloud), en de knoop van de Manager van de App naast uw naam selecteren. Selecteer vervolgens uw toepassing en volg de bovenstaande flow die oorspronkelijk is gebruikt om de aanbieding te maken. Zodra opnieuw voorgelegd, zal het team van de Uitwisseling van de Adobe de veranderingen herzien en of de veranderingen goedkeuren, of met commentaren over de veranderingen antwoorden.

## Het extensiepakket aan je aanbieding koppelen

Nadat je aanbieding is goedgekeurd en openbaar is gemaakt, raden we je aan een koppeling naar de openbare aanbieding op te geven in het veld `exchange_url` van het bestand `extension.json` in het uitbreidingspakket.  Hiermee wordt een koppeling Meer informatie gemaakt in de tagextensiecatalogus, zodat gebruikers in het product je aanbieding kunnen vinden en er extra informatie over is.
