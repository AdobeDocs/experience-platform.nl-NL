---
title: Overzicht van Adobe Experience Platform Assurance
description: Met Adobe Experience Platform Assurance kunt u controleren, testen, simuleren en valideren hoe u gegevens verzamelt of ervaringen aanbiedt in uw mobiele toepassingen.
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 4%

---

# Adobe Experience Platform Assurance

Adobe Experience Platform Assurance is een product van [Adobe Experience Cloud](https://www.adobe.com/experience-cloud.html) om u te helpen bij het inspecteren, testen, simuleren en valideren van de manier waarop u gegevens verzamelt of ervaringen opdoet in uw mobiele app.

>[!IMPORTANT]
>
> Projectgriffon wordt nu aangeduid als **Betrouwbaarheid**!
>
> Projectgriffon is nu over het algemeen beschikbaar voor **alles** Adobe Experience Cloud-klanten als garantie. Lees voor meer informatie over deze overgang de [gebruikerstoegang](./user-access.md).

>[!INFO]
>
>De openbare API&#39;s van de Verzekering zijn beschikbaar!
>
>[De API&#39;s voor betrouwbaarheid](https://developer.adobe.com/adobe-assurance-public-apis/) Dit zijn een verzameling API&#39;s waarmee gebruikers hun web- en mobiele apps kunnen testen en er fouten in kunnen opsporen wanneer deze zijn uitgerust met de SDK van Adobe Assurance Mobile.

## Algemene beschikbaarheid

Vanaf 15 oktober 2022 is de garantie algemeen beschikbaar voor alle Adobe Experience Cloud.

### Wat verandert er?

Op 15 oktober - de toegang tot de verzekering zal via Admin Console worden beheerd. Lees de [gebruikerstoegang](./user-access.md) om ervoor te zorgen dat u ononderbroken toegang hebt.

Er worden geen andere wijzigingen of onderbrekingen verwacht voor bestaande Assurance-integratie, -sessies en -gebeurtenissen. Betrouwbaarheid kan worden voortgezet via [https://griffon.adobe.com](https://griffon.adobe.com) **of** u kunt gebruiken (en bladwijzer) [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance).

## Wat kan Verzekering voor u doen?

### Snelle installatie

Ga snel aan de slag met weinig coderegels. Voor mobiele apps werkt de Verzekering samen met de SDK van Adobe Experience Platform Mobile om u te helpen toepassingsgebeurtenissen, locatiesignalen, configuratieparameters, SDK-logboeken, apparaatinformatie, en meer inspecteren, simuleren en valideren.

### Verbinding zonder probleem

Met de garantie is het eenvoudig en betrouwbaar om uw app aan te sluiten met Platform. U hoeft geen netwerkproxy&#39;s te gebruiken, [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)) en andere gymnastiekfuncties in het netwerk: het is net zo eenvoudig om uw app aan te sluiten op Betrouwbaarheid als een QR-code scannen of op een knop tikken.

![](./images/index/no-hassle-connection.png)

### Controle, simulatie en validatie in realtime

Nadat u verbinding hebt gemaakt met Betrouwbaarheid, kunt u live streamed-toepassingsgebeurtenissen en -activiteit inspecteren en filteren en zoeken om ruis te voorkomen. Gebeurtenissen bevatten informatie over het valideren, opsporen van fouten en het oplossen van problemen met de implementatie van uw mobiele app. De verzekering laat u ook screenshot, simuleert plaatssignalen, en meer in real time.

![](./images/index/real-time-insepction.png)

### Integratie met Adobe Experience Cloud

Gegevens en ervaringen aan de clientzijde worden in de context weergegeven door de manier waarop gebruikers regels, activiteiten en campagnes voor de rapportage van hun gebruikers op markeerpuntgebaseerde gebruikersinterfaces instellen. Om u te helpen de punten tussen beide verbinden, integreren wij met oplossingen van Adobe Experience Cloud zoals Adobe Experience Platform, Adobe Analytics, Adobe Target, Plaatsen Service, en meer.

![](./images/index/integration.png)

## Functies

### Gebeurtenissen, logbestanden en meer van Adobe Experience Platform Mobile SDK

Met de optie Betrouwbaarheid kunt u onbewerkte SDK-gebeurtenissen controleren die zijn gegenereerd door de Adobe Experience Platform Mobile SDK. Alle gebeurtenissen die door de SDK worden verzameld, zijn beschikbaar voor inspectie. SDK-gebeurtenissen worden geladen in een lijstweergave, gesorteerd op tijd. Elke gebeurtenis heeft een gedetailleerde weergave met meer details. Er worden ook extra weergaven geboden voor het bladeren in de SDK-configuratie, gegevenselementen, gedeelde statussen en SDK-extensieversies.

### Adobe Analytics

De weergave Adobe Analytics > Analytics Events is een gefocuste weergave waarin gebeurtenissen worden weergegeven die betrekking hebben op uw mobiele Adobe Analytics-implementatie. De lijstweergave toont de levenscyclus of actie-/statusgebeurtenissen, nabewerkte &#39;status&#39;, samen met de vereiste gebeurtenisdetails in een speciaal opgemaakte weergave. Met de status Na verwerking kunt u zien hoe de gebeurtenis door Adobe Analytics is verwerkt nadat verwerkingsregels op de gebeurtenis zijn toegepast.

### Adobe Analytics for Streaming Media

In de weergave Adobe Analytics > Media Analytics Events worden gebeurtenissen weergegeven voor de implementatie van uw audio- en videoanalyse. In de gedetailleerde weergave van gebeurtenissen worden standaard- en aangepaste metagegevens weergegeven die voor elke afspeelsessie worden bijgehouden. Bovendien kunt u de status na verwerking en de gegevens van de analyse van de media, zoals de mediatijd die is doorgebracht of de totale bufferduur, weergeven.

### Plaatsen (Locatieservices)

De mening van de Diensten van de Plaats is een mening op apparaat die de ingang en de uitgangsgebeurtenissen van de gebruikersplaats voor gemakkelijke bevestiging toont. Deze handige weergave biedt een handige interface voor het weergeven van locatie-specifieke gegevenspunten voor inspectie op de client voor foutopsporing in de context.

## Is de verzekering veilig?

Voor de zekerheid gelden de volgende beveiligingsmaatregelen:

* Zowel hebben de Verzekering als het Web UI van de Verzekering een veilige, op SPELD-Gebaseerde handdruk voor een verbinding. De gebruiker moet een handdruk uitdrukkelijk tot stand brengen, die &quot;toevallige&quot;verbindingen van de Verzekering verhindert om door een eindgebruiker worden gecreeerd.
* Alleen verbindingen tussen Verzekering en de Assurance-webinterface die tot dezelfde Adobe Experience Cloud-organisatie-id behoren, worden ondersteund.
* Gebeurtenissen van Adobe Experience Platform Mobile SDK&#39;s worden via HTTPS verzonden.
* De SDK&#39;s voor Betrouwbaarheid en Adobe Experience Platform Mobile maken gebruik van TLS 1.2
* Verzekeringssessies worden na 30 dagen verwijderd.
* Gegevens van de betrouwbaarheidssessie worden in rust gecodeerd volgens de best practices voor opslag.

## Aan de slag

Als u de optie Verzekering wilt instellen, moet u eerst de extensie Verzekering in uw toepassing installeren. Lees de zelfstudie voor meer informatie hierover [de uitvoering van de verlenging van de betrouwbaarheidsverklaring](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

Nadat u de garantie aan uw app hebt toegevoegd, kunt u een betrouwbaarheidssessie maken die op uw apparaat kan worden aangesloten. Lees voor meer informatie over het gebruik van Verzekering de [handleiding voor het gebruik van Betrouwbaarheid](./tutorials/using-assurance.md).
