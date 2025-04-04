---
title: Adobe Experience Platform Assurance - Overzicht
description: Met Adobe Experience Platform Assurance kunt u controleren, testen, simuleren en valideren hoe u gegevens verzamelt of ervaringen aanbiedt in uw mobiele toepassingen.
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 4%

---

# Adobe Experience Platform Assurance

Adobe Experience Platform Assurance is een product van [ Adobe Experience Cloud ](https://www.adobe.com/experience-cloud.html) om u te helpen inspecteren, beproeven, simuleren, en bevestigen hoe u gegevens verzamelt of ervaringen in uw mobiele app dient.

>[!IMPORTANT]
>
> Griffon van het project is nu gekend als **Assurance**!
>
> Griffon van het project is nu over het algemeen beschikbaar aan **alle** klanten van Adobe Experience Cloud als Assurance. Om meer over deze overgang te leren, te lezen gelieve de [ gids van de gebruikerstoegang ](./user-access.md).

>[!INFO]
>
>Assurance Public API&#39;s zijn beschikbaar!
>
>[ Assurance APIs ](https://developer.adobe.com/adobe-assurance-public-apis/) is een inzameling van APIs die gebruikers machtigen om hun Web en mobiele apps te testen en te zuiveren, wanneer uitgerust met Adobe Assurance Mobile SDK.

## Algemene beschikbaarheid

Vanaf 15 oktober 2022 is Assurance algemeen beschikbaar voor alle Adobe Experience Cloud.

### Wat verandert er?

Op 15 oktober - de toegang tot Assurance wordt beheerd via Admin Console. Gelieve te lezen de [ gids van de gebruikerstoegang ](./user-access.md) om ervoor te zorgen u ononderbroken toegang blijft hebben.

Er worden geen andere wijzigingen of onderbrekingen verwacht voor bestaande Assurance-integratie, -sessies en -gebeurtenissen. Assurance kan verder worden betreden via [ https://griffon.adobe.com ](https://griffon.adobe.com) **of** u kunt gebruiken (en referentie) [ https://experience.adobe.com/assurance ](https://experience.adobe.com/assurance).

## Wat kan Assurance voor je doen?

### Snelle installatie

Ga snel aan de slag met weinig coderegels. Voor mobiele apps werkt Assurance samen met Adobe Experience Platform Mobile SDK om u te helpen bij het inspecteren, simuleren en valideren van toepassingsgebeurtenissen, locatiesignalen, configuratieparameters, SDK-logboeken, apparaatinformatie en meer.

### Verbinding zonder probleem

Met Assurance is het eenvoudig en betrouwbaar om uw app te verbinden met Experience Platform. U te hoeven om geen netwerkvolmachten, [ MiTM ](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) te gebruiken, en andere netwerk gymnastiek - verbindend uw app met Assurance is zo gemakkelijk zoals het aftasten van een code QR of het tikken van een knoop.

![](./images/index/no-hassle-connection.png)

### Controle, simulatie en validatie in realtime

Nadat u verbinding hebt gemaakt met Assurance, kunt u livegestreamde toepassingsgebeurtenissen en -activiteit inspecteren en filteren en zoeken om ruis te verwijderen. Gebeurtenissen bevatten informatie over het valideren, opsporen van fouten en het oplossen van problemen met de implementatie van uw mobiele app. Met Assurance kunt u ook schermafbeeldingen maken, locatiesignalen simuleren en meer in real-time.

![](./images/index/real-time-insepction.png)

### Integratie met Adobe Experience Cloud

Gegevens en ervaringen aan de clientzijde worden in de context weergegeven door de manier waarop gebruikers regels, activiteiten en campagnes voor de rapportage van hun gebruikers op markeerpuntgebaseerde gebruikersinterfaces instellen. Om u te helpen de punten tussen beide verbinden, integreren wij met oplossingen van Adobe Experience Cloud zoals Adobe Experience Platform, Adobe Analytics, Adobe Target, Plaatsen Service, en meer.

![](./images/index/integration.png)

## Functies

### Adobe Experience Platform Mobile SDK Events, logs en meer

Assurance helpt u onbewerkte SDK-gebeurtenissen die zijn gegenereerd door de Adobe Experience Platform Mobile SDK te inspecteren. Alle gebeurtenissen die door de SDK zijn verzameld, kunnen worden geïnspecteerd. SDK-gebeurtenissen worden geladen in een lijstweergave, gesorteerd op tijd. Elke gebeurtenis heeft een gedetailleerde weergave met meer details. Er zijn ook extra weergaven beschikbaar voor het bladeren door de SDK-configuratie, gegevenselementen, gedeelde statussen en SDK-extensieversies.

### Adobe Analytics

De weergave Adobe Analytics > Analytics Events is een gefocuste weergave waarin gebeurtenissen worden weergegeven die betrekking hebben op uw mobiele Adobe Analytics-implementatie. De lijstweergave toont de levenscyclus of actie-/statusgebeurtenissen, nabewerkte &#39;status&#39;, samen met de vereiste gebeurtenisdetails in een speciaal opgemaakte weergave. Met de status Na verwerking kunt u zien hoe de gebeurtenis door Adobe Analytics is verwerkt nadat verwerkingsregels op de gebeurtenis zijn toegepast.

### Adobe Analytics for Streaming Media

In de weergave Adobe Analytics > Media Analytics Events worden gebeurtenissen voor de implementatie van uw audio- en videoanalysemogelijkheden weergegeven. In de gedetailleerde weergave van gebeurtenissen worden standaard- en aangepaste metagegevens weergegeven die voor elke afspeelsessie worden bijgehouden. Bovendien kunt u de status na verwerking en de gegevens van de analyse van de media, zoals de mediatijd die is doorgebracht of de totale bufferduur, weergeven.

### Plaatsen (Locatieservices)

De mening van de Diensten van de Plaats is een mening op apparaat die de ingang en de uitgangsgebeurtenissen van de gebruikersplaats voor gemakkelijke bevestiging toont. Deze handige weergave biedt een handige interface voor het weergeven van locatie-specifieke gegevenspunten voor inspectie op de client voor foutopsporing in de context.

## Is Assurance veilig?

Assurance beschikt over de volgende beveiligingsmaatregelen:

* Zowel Assurance als het Web UI van Assurance hebben een veilige, op SPELD-Gebaseerde handdruk voor een verbinding. De gebruiker moet uitdrukkelijk een handdruk tot stand brengen, die &quot;toevallige&quot;verbindingen van Assurance om door een eindgebruiker verhindert worden gecreeerd.
* Alleen verbindingen tussen Assurance en de Assurance-webinterface die tot dezelfde Adobe Experience Cloud-organisatie-id behoren, worden ondersteund.
* Gebeurtenissen van Adobe Experience Platform Mobile SDK&#39;s worden via HTTPS verzonden.
* Assurance en Adobe Experience Platform Mobile SDK&#39;s gebruiken TLS 1.2
* Assurance-sessies worden na 30 dagen verwijderd.
* Assurance-sessiegegevens worden in rust gecodeerd volgens de best practices voor opslag.

## Aan de slag

Als u Assurance wilt instellen, moet u eerst de Assurance-extensie in uw toepassing installeren. Leren hoe te om dit te doen, te lezen gelieve het leerprogramma op [ uitvoerend de uitbreiding van Assurance ](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

Nadat u Assurance aan uw app hebt toegevoegd, kunt u een Assurance-sessie maken die op uw apparaat kan worden aangesloten. Leren hoe te om Assurance te gebruiken, te lezen gelieve de [ gids bij het gebruiken van Assurance ](./tutorials/using-assurance.md).
