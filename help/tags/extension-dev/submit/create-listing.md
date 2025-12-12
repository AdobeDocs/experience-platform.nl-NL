---
title: Een Exchange-aanbieding voor een extensie maken
description: Leer hoe u uw extensie toevoegt aan de openbare catalogus in Adobe Experience Platform.
exl-id: 0395fc99-5e2b-46d6-a067-f8f167733e02
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---

# Een uitwisselingslijst maken voor een extensie

Adobe Experience Platform heeft één enkele verenigde catalogus waar de gebruikers markeringsuitbreidingen kunnen bekijken die voor installatie beschikbaar zijn. Deze catalogus is beschikbaar in het product en bevat extensies van drie typen:

1. **Openbare uitbreidingen**: Deze voltooide uitbreidingen die voor productiegebruik door om het even welke gebruiker worden ontworpen.
1. **Privé uitbreidingen**: Deze voltooide uitbreidingen die voor productie worden ontworpen, maar door andere gebruikers in uw bedrijf werden ontwikkeld en slechts beschikbaar aan gebruikers binnen uw bedrijf zijn.
1. **uitbreidingen van de Ontwikkeling**: Deze uitbreidingen zijn onder actieve ontwikkeling en zijn slechts beschikbaar binnen uw bedrijf en slechts op een bezit dat specifiek als bezit van de Ontwikkeling wordt aangewezen.

Afzonderlijk van de uitbreidingen in de productcatalogus, hebben de openbare uitbreidingen ook lijsten in de [ Marketplace van de Uitwisseling van Experience Cloud App ](https://exchange.adobe.com/apps/browse/ec).

Met deze aanbiedingen kunnen extensieontwikkelaars beschrijvingen van functies plaatsen, koppelingen naar aanvullende ondersteuning en documentatie aanbieden en extensies op de markt brengen voor toekomstige gebruikers die wellicht niet op de hoogte zijn van uw bedrijf of de functionaliteit van uw extensie. Op deze markt heeft je extensie een openbare aanbieding die kan worden weergegeven zonder dat de gebruiker op Experience Platform is geverifieerd. Voor openbare extensies is het maken van deze Exchange-lijst een vereiste stap.

>[!TIP]
>
>Wanneer je Exchange-aanbieding wordt gepubliceerd, wordt er automatisch een koppeling toegevoegd aan de aanbiedingsinhoud waarmee je klanten en vooruitzichten kunnen klikken en `Connect with publisher` voor meer informatie over je producten en services. Uw contact e-mailadres wordt niet getoond aangezien deze berichten aan u door:sturen door het systeem van de Uitwisseling.

Als u geen bedrijf hebt om uw extensiepakket te uploaden en te testen, moet u zich registreren voor het Exchange-programma en een aanbieding starten. Hierdoor wordt een bedrijfsaccount gemaakt (het duurt even voordat u een e-mail ontvangt wanneer deze is voltooid) waarmee u uw extensie kunt uploaden en testen. Wissellijsten zijn alleen vereist voor openbare extensies.

Als u reeds een bedrijfrekening hebt, of als u geen lijst van de Uitwisseling (privé uitbreidingen slechts) nodig hebt, kunt u de rest van deze stap overslaan en aan [ te werk gaan uploaden en uw uitbreiding ](./upload-and-test.md) testen.

## Een aanbieding maken

>[!NOTE]
>
>Hieronder wordt beschreven hoe u een toepassingslijst maakt in het Adobe Exchange-programma. Dit is de term die wordt gebruikt voor de verschillende integraties en extensies in Adobe Experience Platform.

![ de verbindingsplaats van de Manager van de Experience Cloud App ](../images/getting-started/app-mgr-link.png)

1. Teken binnen aan de [ plaats van de Partner van de Uitwisseling ](https://partners.adobe.com/exchangeprogram/experiencecloud). Zodra ondertekend binnen, selecteer de **verbinding van de Manager van de App** naast uw naam.
1. Selecteer **Nieuwe Toepassing** tabel creëren, en selecteer dan **Nieuwe App** voor een aangepaste oplossing creëren, of een toepasselijk malplaatje selecteren.
1. Geef je objectgegevens op. Voor gedetailleerde informatie over de controle van de Manager van de App uit het volledige [ artikel ](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931). De informatie van de lijst zou zeer duidelijk moeten zijn over wat de uitbreiding doet en waarom het nuttig is. Deze aanbieding fungeert als marketingruimte voor uw app. Promoot hier uw extensie met duidelijke beschrijvingen, koppelingen naar bestemmingspagina&#39;s op uw site, koppelingen naar Help-documenten of ondersteuning van e-mailadressen enzovoort. Hoewel de ruimte in uitbreidingsmeningen beperkt is, biedt de lijst van de Uitwisseling een kans om zowel uw uitbreiding als uw bedrijf te bevorderen. Hieronder volgen suggesties om de uitbreiding beter te promoten:
   - **Pictogram van de Toepassing** - zorg ervoor het pictogram voor de lijst van de Uitwisseling de aangewezen dimensies, 512 x 512 voor png of 1 :1 aspectverhouding voor jpg heeft.

     >[!NOTE]
     >
     >Dit is een andere bestandsindeling dan de extensiecode. De uitbreiding zelf zal een svg- dossier als [ pictogram ](../manifest.md) bevatten.

   - **Aanbevolen Beeld** - krijg aandacht door een beeld te gebruiken dat zelfstandig kan staan en uw merk zal tonen en uw toepassing zal benadrukken. De aanbevolen afbeelding is de afbeelding die wordt weergegeven wanneer iemand een link naar je aanbieding op de beurs deelt of er berichten over plaatst op sociale media. Het moet daarom een modelweergave van uw merk zijn.
   - **Logo van de Uitgever van de App** - dit is uw collectief embleem, zorg ervoor het pictogram de aangewezen afmetingen van 1280 x 720, of 2560 x 1440 (16 :9) in png of jpg formaat heeft.
   - **de Instructies van de Configuratie** - Informeer klanten hoe te om uw uitbreiding van Adobe Experience Platform te vormen. Zorg ervoor zij om het even welke vereiste montages en volgende stappen begrijpen wanneer uw [ configuratiemening ](../configuration.md) onmiddellijk na het installeren van uw uitbreiding in een bezit verschijnt.
   - **Markeringen** - op de eerste pagina van het uitgeven van uw lijst, gelieve te zijn zeker om het woord &quot;Lancering&quot;in het gebied van de Markeringen van de Douane te omvatten. Zo wordt je aanbieding weergegeven in zoekopdrachten naar tags op de Exchange-markt:
     ![](../images/getting-started/custom-tags.jpg)
   - **Sandboxes** - Uw toegang tot de Oplossingen van Adobe is door een rekening van Sandbox waar u toegang tot een volledig werkende versie van Adobe Experience Platform hebt. Deze Sandbox-accounts worden aangevraagd terwijl u uw toepassingslijst maakt. In de **sectie van Verbindingen** selecteert de specifieke verbindingen die voor de toepassing van toepassing zijn u creeerde (uw markeringsuitbreiding), en wanneer u **sparen** raakt, zal het zandbakverzoek indien nodig worden geproduceerd.
1. Verzend je aanbieding. Het Adobe Exchange-team evalueert uw toepassing en geeft feedback als updates vereist zijn. Als u **merkt publiceer onmiddellijk** checkbox wanneer u uw lijst indient, zal het onmiddellijk op goedkeuring worden gepubliceerd. Als u de toepassing later wilt publiceren, schakelt u het selectievakje uit. Wanneer uw uitbreidingslijst wordt goedgekeurd, zal een blauwe **publiceren** knoop naast het op uw app (uitbreiding) lijstenpagina verschijnen.

### Een effectieve aanbieding maken

Gelieve te nemen een blik bij de [ Richtsnoer van de Indiening van de Toepassing ](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html) voor gedetailleerde informatie over hoe te om tot de het meest het in dienst nemen lijst te leiden.

#### Na het verzenden van je aanbieding op de beurs

Na verzending zal het Adobe Exchange-team de toepassing beoordelen en de toepassing goedkeuren of reageren met opmerkingen over wijzigingen. Dit proces wordt beschreven in de richtlijnen voor het indienen van toepassingen.

Als u geen login aan de plaats van de Uitwisseling hebt, zorg ervoor dat uw e-mail voor het programma van de Uitwisseling door de instructies in de [ Gids van de Registratie van het Programma te volgen ](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html) wordt geregistreerd. Elke gebruiker moet zijn e-mail met de partnerrekening voor hun bedrijf associëren. Vragen over dit proces kunnen via e-mail naar <ExchangeHelpEC@adobe.com> worden gestuurd.

#### Je ruilaanbieding bijwerken na eerste goedkeuring

Wanneer u uw uitbreiding bijwerkt, of enkel uw lijst van de Uitwisseling moet bijwerken, login aan het [ Portaal van de Partner ](https://partners.adobe.com/exchangeprogram/experiencecloud), en de knoop van de Manager van de App naast uw naam selecteren. Selecteer vervolgens uw toepassing en volg de bovenstaande flow die oorspronkelijk is gebruikt om de aanbieding te maken. Nadat het Adobe Exchange-team opnieuw is verzonden, controleert het de wijzigingen en keurt het de wijzigingen goed of reageert het met opmerkingen over de wijzigingen.

## Het extensiepakket aan je aanbieding koppelen

Nadat je aanbieding is goedgekeurd en openbaar is gemaakt, raden we je aan een koppeling naar de openbare aanbieding op te geven in het veld `exchange_url` van het bestand `extension.json` in het extensiepakket.  Hiermee wordt een koppeling Meer informatie gemaakt in de tagextensiecatalogus, zodat gebruikers in het product je aanbieding kunnen vinden en er extra informatie over is.
