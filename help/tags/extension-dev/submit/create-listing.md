---
title: Een Exchange-aanbieding voor een extensie maken
description: Leer hoe u uw extensie toevoegt aan de openbare catalogus in Adobe Experience Platform.
exl-id: 0395fc99-5e2b-46d6-a067-f8f167733e02
source-git-commit: fcc586034317fb31122721fa9754b580c761a1da
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 0%

---

# Een uitwisselingslijst maken voor een extensie

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Adobe Experience Platform heeft één enkele verenigde catalogus waar de gebruikers markeringsuitbreidingen kunnen bekijken die voor installatie beschikbaar zijn. Deze catalogus is beschikbaar in het product en bevat extensies van drie typen:

1. **Openbare extensies**: Dit zijn voltooide extensies die zijn ontworpen voor productiegebruik door elke gebruiker.
1. **Persoonlijke extensies**: Dit zijn voltooide extensies die zijn ontworpen voor productie, maar die zijn ontwikkeld door andere gebruikers in uw bedrijf en die alleen beschikbaar zijn voor gebruikers binnen uw bedrijf.
1. **Ontwikkeluitbreidingen**: Deze uitbreidingen zijn onder actieve ontwikkeling en zijn slechts beschikbaar binnen uw bedrijf en slechts op een bezit dat specifiek als bezit van de Ontwikkeling wordt aangewezen.

Openbare extensies hebben, los van de extensies in de productcatalogus, ook vermeldingen in de [Experience Cloud Exchange App Marketplace](https://exchange.adobe.com/apps/browse/ec).

Met deze aanbiedingen kunnen extensieontwikkelaars beschrijvingen van functies plaatsen, koppelingen naar aanvullende ondersteuning en documentatie aanbieden en extensies op de markt brengen voor toekomstige gebruikers die wellicht niet op de hoogte zijn van uw bedrijf of de functionaliteit van uw extensie. Op deze markt is er een openbare aanbieding voor je extensie die kan worden weergegeven zonder dat de gebruiker op het Platform is geverifieerd. Voor openbare extensies is het maken van deze Exchange-lijst een vereiste stap.

>[!TIP]
>
>Wanneer je aanbieding op de beurs wordt gepubliceerd, wordt er automatisch een koppeling toegevoegd aan de inhoud van de aanbieding waardoor je klanten en vooruitzichten kunnen klikken en `Connect with publisher` voor meer informatie over uw producten en services. Uw contact e-mailadres wordt niet getoond aangezien deze berichten aan u door:sturen door het systeem van de Uitwisseling.

Als u geen bedrijf hebt om uw extensiepakket te uploaden en te testen, moet u zich registreren voor het Exchange-programma en een aanbieding starten. Hierdoor wordt een bedrijfsaccount gemaakt (het duurt even voordat u een e-mail ontvangt wanneer deze is voltooid) waarmee u uw extensie kunt uploaden en testen. Wissellijsten zijn alleen vereist voor openbare extensies.

Als u al een bedrijfsaccount hebt of als u geen Exchange-lijst nodig hebt (alleen privéextensies), kunt u de rest van deze stap overslaan en doorgaan naar [uw extensie uploaden en testen](./upload-and-test.md).

## Een aanbieding maken

>[!NOTE]
>
>Het volgende proces detailleert de verwezenlijking van een toepassingslijst in het programma van de Uitwisseling van de Adobe. Dit is de term die wordt gebruikt voor de verschillende integraties en extensies in Adobe Experience Platform.

![Koppelingslocatie Experience Cloud App Manager](../images/getting-started/app-mgr-link.png)

1. Aanmelden bij de [Exchange Partner-site](https://partners.adobe.com/exchangeprogram/experiencecloud). Selecteer de optie **App Manager** naast uw naam.
1. Selecteer **Nieuwe toepassing maken** en selecteert u vervolgens **Nieuwe app maken** voor een aangepaste oplossing, of selecteer een toepasselijk malplaatje.
1. Geef je objectgegevens op. Voor gedetailleerde informatie over App Manager checkt u de volledige [artikel](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931). De informatie van de lijst zou zeer duidelijk moeten zijn over wat de uitbreiding doet en waarom het nuttig is. Deze aanbieding fungeert als marketingruimte voor uw app. Promoot hier uw extensie met duidelijke beschrijvingen, koppelingen naar bestemmingspagina&#39;s op uw site, koppelingen naar Help-documenten of ondersteuning van e-mailadressen enzovoort. Hoewel de ruimte in uitbreidingsmeningen beperkt is, biedt de lijst van de Uitwisseling een kans om zowel uw uitbreiding als uw bedrijf te bevorderen. Hieronder volgen suggesties om de uitbreiding beter te promoten:
   - **App-pictogram** - Zorg ervoor dat het pictogram voor de Exchange-aanbieding de juiste afmetingen heeft, 512 x 512 voor png of een hoogte-breedteverhouding van 1:1 voor jpg.

      >[!NOTE]
      >
      >Dit is een andere bestandsindeling dan de extensiecode. De extensie zelf bevat een svg-bestand als de [pictogram](../manifest.md).

   - **Aanbevolen afbeelding** - Let op door een afbeelding te gebruiken die zelfstandig kan worden weergegeven en waarmee uw merk wordt weergegeven en uw toepassing wordt gemarkeerd. De aanbevolen afbeelding is de afbeelding die wordt weergegeven wanneer iemand een koppeling deelt naar je aanbieding op de beurs of er berichten over plaatst op sociale media. Het moet daarom een modelweergave van uw merk zijn.
   - **Logo van App Publisher** - Dit is uw bedrijfslogo. Zorg ervoor dat het pictogram de juiste afmetingen heeft van 1280 x 720 of 2560 x 1440 (16:9) in de PNG- of JPG-indeling.
   - **Configuratieinstructies** - Stel klanten op de hoogte van de configuratie van uw Adobe Experience Platform-extensie. Zorg ervoor dat ze de vereiste instellingen en volgende stappen begrijpen wanneer uw [configuratieweergave](../configuration.md) wordt direct na het installeren van de extensie in een eigenschap weergegeven.
   - **Tags** - Op de eerste pagina van het bewerken van je aanbieding moet je het woord &#39;Starten&#39; opnemen in het veld &#39;Aangepaste tags&#39;. Zo wordt je aanbieding weergegeven in zoekopdrachten naar tags op de Exchange-markt:
      ![](../images/getting-started/custom-tags.jpg)
   - **Sandboxen** - Uw toegang tot Adobe Solutions verloopt via een Sandbox-account, waar u toegang hebt tot een volledig functionerende versie van Adobe Experience Platform. Deze Sandbox-accounts worden aangevraagd terwijl u uw toepassingslijst maakt. In de **Verbindingen** selecteert u de specifieke verbindingen die van toepassing zijn op de toepassing die u hebt gemaakt (de tagextensie) en wanneer u op **Opslaan** wordt de sandboxaanvraag indien nodig gegenereerd.
1. Verzend je aanbieding. Het team van de Uitwisseling van de Adobe zal uw toepassing herzien en zal verstrekken terugkoppelen als de updates worden vereist. Als u de **direct publiceren** als je je aanbieding verzendt, wordt deze meteen na goedkeuring gepubliceerd. Als u de toepassing later wilt publiceren, schakelt u het selectievakje uit. Wanneer uw extensielijst is goedgekeurd, blauw **Publiceren** wordt er naast weergegeven op de pagina met aanbiedingen in uw app (extensie).

### Een effectieve aanbieding maken

Kijk eens naar de [Richtlijnen voor toezending van app](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html) voor gedetailleerde informatie over hoe u de meest interessante lijst kunt maken.

#### Na het verzenden van je aanbieding op de beurs

Zodra voorgelegd, zal het team van de Uitwisseling van de Adobe de toepassing herzien en of de toepassing goedkeuren, of met commentaren over veranderingen antwoorden. Dit proces wordt beschreven in de richtlijnen voor het indienen van toepassingen.

Als u geen login aan de plaats van de Uitwisseling hebt, zorg ervoor dat uw e-mail voor het programma van de Uitwisseling door de instructies in te volgen wordt geregistreerd [Registratiehandleiding voor programma](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html). Elke gebruiker moet zijn e-mail met de partnerrekening voor hun bedrijf associëren. Vragen over dit proces kunnen via e-mail worden gestuurd naar <ExchangeHelpEC@adobe.com>.

#### Je ruilaanbieding bijwerken na eerste goedkeuring

Meld u aan bij de [Partner Portal](https://partners.adobe.com/exchangeprogram/experiencecloud)en selecteer de knop App Manager naast uw naam. Selecteer vervolgens uw toepassing en volg de bovenstaande flow die oorspronkelijk is gebruikt om de aanbieding te maken. Zodra opnieuw voorgelegd, zal het team van de Uitwisseling van de Adobe de veranderingen herzien en of de veranderingen goedkeuren, of met commentaren over de veranderingen antwoorden.

## Het extensiepakket aan je aanbieding koppelen

Nadat je aanbieding is goedgekeurd en openbaar is gemaakt, raden we je aan een link naar de openbare aanbieding in het `exchange_url` van het `extension.json` in het extensiepakket.  Hiermee wordt een koppeling Meer informatie gemaakt in de tagextensiecatalogus, zodat gebruikers in het product uw aanbieding kunnen vinden en het is extra informatie.
