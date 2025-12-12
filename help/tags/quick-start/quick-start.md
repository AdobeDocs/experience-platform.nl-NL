---
title: Snelstartgids
description: Leer hoe u snel aan de slag kunt met tags in Adobe Experience Platform.
exl-id: 490ee344-3b18-4189-9293-2378f86fb10d
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 0%

---

# Snelstartgids

Tags zijn Adobe Experience Platform van de volgende generatie technologie voor tagbeheer. Het is vanaf de grond opgebouwd om een open en duurzaam ecosysteem te steunen waar iedereen zijn eigen integraties kan bouwen die klanten van Adobe aan hun plaatsen kunnen opstellen. Het is een eerste API-toepassing, dus alles wat u via de UI kunt doen, kunt u ook via programmacode doen via een API.

De basisworkflow voor labels:

1. Groepen en gebruikers instellen.
2. Log in.
3. Maak een eigenschap.
4. Extensies installeren.
5. Maak gegevenselementen en regels.
6. Test in uw ontwikkelomgeving.
7. Bevorderen tot de productie.

## &#x200B;1. Groepen en gebruikers instellen

Tags zijn volledig geïntegreerd met uw Adobe ID. Gebruikersmachtigingen worden via de Admin Console beheerd met andere Adobe-producten en -oplossingen van de [!DNL Creative Cloud] , [!DNL Document Cloud] en Experience Cloud.

Tags hebben een op rechten gebaseerd gebruikersbeheersysteem. Dit betekent dat individuele rechten expliciet moeten worden toegekend. Deze rechten worden toegewezen aan groepen, en gebruikers worden toegevoegd aan de juiste groepen om toegang te krijgen. Zelfs als uw organisatie toegang tot de Inzameling van Gegevens heeft, kunnen de individuele gebruikers niets doen tot een beheerder hen uitdrukkelijk sommige rechten verleent.

Voor gedetailleerde instructies op hoe te om groepen tot stand te brengen en gebruikers voor markeringen toe te voegen, zie de [&#x200B; gids van de toestemmingen van de gegevensinzameling &#x200B;](../../collection/permissions.md).

## &#x200B;2. Aanmelden

Nadat u tagrechten hebt toegevoegd aan uw Adobe ID, moet u zich aanmelden bij de gebruikersinterface van Experience Platform of de gebruikersinterface voor gegevensverzameling. U kunt dit doen door rechtstreeks aan het [&#x200B; login van Experience Cloud scherm &#x200B;](https://experience.adobe.com/) te navigeren, en het selecteren van of **[!UICONTROL Data Collection]** of **[!UICONTROL Experience Platform]**.

>[!NOTE]
>
>Als u één account met rechten voor meerdere organisaties hebt, kunt u de organisatie wijzigen door de naam van de organisatie te selecteren in de besturingsbalk boven in het scherm en een andere organisatie te kiezen in de vervolgkeuzelijst.

## &#x200B;3. Een eigenschap maken

Nadat u zich hebt aangemeld bij de gebruikersinterface, maakt u eerst een eigenschap. Een eigenschap is in feite een container die u vult met extensies, regels, gegevenselementen en bibliotheken wanneer u tags op uw site implementeert. Veel mensen maken een eigenschap voor elke website (of groep nauw verwante sites) waar ze dezelfde set tags willen implementeren.

Voor meer over het creëren van eigenschappen, zie [&#x200B; een bezit &#x200B;](../ui/administration/companies-and-properties.md) creëren.

## &#x200B;4. Extensies installeren

Een extensie is een integratie die is gebouwd door Adobe of een Adobe-partner en die nieuwe en eindeloze opties toevoegt voor de tags die u kunt implementeren op uw sites. Als u een tag ziet als een besturingssysteem, zijn extensies de apps die u installeert om de specifieke taken uit te voeren die u nodig hebt.

Alle nieuwe eigenschappen komen met de [&#x200B; geïnstalleerde uitbreiding van de Kern &#x200B;](../extensions/client/core/overview.md). Mobiele eigenschappen worden geleverd met extra extensies. De uitbreiding van de Kern wordt gebouwd door Adobe om een robuuste standaardreeks gegevenselementtypes voor uw gegevenslaag en gebeurtenistypen voor uw regels te verstrekken. De meeste handelingen die u wilt uitvoeren (een ECID ophalen, [!DNL Adobe Analytics] -beacons verzenden, het globale vakje [!DNL Target] laden, enzovoort) komen uit extensies die u installeert vanuit de catalogus.

Wat tags in Experience Platform echt uniek maakt, is dat deze extensies door iedereen kunnen worden gemaakt. Moet u een opnieuw op de markt gebrachte pixel op Facebook op uw site neerzetten? Bekijk de extensie die Facebook heeft gemaakt. Wilt u hetzelfde voor Twitter of Gekoppeld in? Gebruik deze extensies. Moet u een onderzoek in werking stellen? Kijk naar Vraag Pro of Voorzien. Moet u privacy beheren en toestemming van uw eindgebruikers geven om uit te weg te gaan met [!DNL GDPR]? Kijk goed naar Evidon en Vertrouwboog. Wilt u korrelige insight weergeven in het gedrag van individuele gebruikers op uw site? Kijk eens naar Clicktale. Voor meer informatie, voor meer informatie, zie de sectie over [&#x200B; toevoegend een nieuwe uitbreiding &#x200B;](../ui/managing-resources/extensions/overview.md#add-a-new-extension).

## &#x200B;5. Gegevenselementen en regels maken

**elementen van Gegevens** zijn wijzers aan de informatie die u wilt verzamelen en verzenden naar verschillende plaatsen op uw pagina:

* Een gedefinieerde gegevenslaag in JSON
* DOM-elementen
* Cookies
* Sessie en lokale opslag
* Alleen maar over alles

Nadat het gegevenselement wordt bepaald, kunt u het element overal in UI voor om het even welke uitbreiding gebruiken. Zie de documentatie over [&#x200B; Elementen van Gegevens &#x200B;](../ui/managing-resources/data-elements.md) voor meer gedetailleerde informatie.

**Regels** zijn bij de logische kern van uw implementatie en controleren wat, wanneer, waar, en hoe van alle markeringen op uw plaats. Definieer een gebeurtenis, stel voorwaarden en uitzonderingen in en definieer vervolgens de handelingen en volgorde. Tot slot publiceer uw veranderingen om de resultaten te zien. Voor meer informatie, zie [&#x200B; Regels &#x200B;](../ui/managing-resources/rules.md).

## &#x200B;6. Test in uw ontwikkelomgeving

### Bibliotheken en builds

Tagbuilds worden nooit automatisch gepubliceerd. Elke reeks veranderingen u aanbrengt wordt ingekapseld in a [&#x200B; bibliotheek &#x200B;](../ui/publishing/libraries.md). Elke bibliotheek u creeert erft automatisch om het even wat stroomopwaarts (gepubliceerd, goedgekeurd, of voorgelegd) als basislijn, zodat moet u slechts de veranderingen bepalen u wilt maken. Deze bibliotheek dient als blauwdruk voor a [&#x200B; bouwt &#x200B;](../ui/publishing/builds.md). Een build is de werkelijke set JavaScript-bestanden die worden geïmplementeerd en gebruikt.

Het is belangrijk dat u de relatie begrijpt tussen uw webpagina, de hostlocatie en tags.

1. Uw hostserver biedt een locatie voor het publiceren van de build. De build zelf bevat de JavaScript-bestanden die door de bibliotheek worden vereist.

   Elk milieu heeft een verhouding met een gastheer, en de gastheer verstrekt een eindpunt erop wijst die waar te om de bouwstijl te leveren. De gastheer kan tot slechts één bezit behoren, hoewel een bezit vele gastheren kan hebben.

2. Er wordt een insluitcode opgegeven in de formuliertag `<script>` die naar de `<head>` -secties van uw website HTML gaat.

   Wanneer u een milieu creeert en een gastheer vastmaakt, produceert het milieu automatisch een unieke inbedcode die u toestaat om zijn toegewezen bouwstijl in uw plaats te integreren. De `<script>` -code wordt gebruikt om de build van de bibliotheek tijdens runtime te implementeren.

3. Wanneer een gebruiker door uw site bladert, haalt de tag embed code `<script>` de build op van uw hostserver op en voert de gedefinieerde handelingen uit in de browser.

### Gastheren

Een host is een verbinding tussen een tag-eigenschap en uw hostlocatie. Tags bieden momenteel ondersteuning voor door Adobe beheerde hosting via een [!DNL Akamai] -host of zelfhosting via een SFTP-host. Tags maken verbinding met de server die door de host is gedefinieerd en leveren de build wanneer u een build maakt.

Als u zelf host, kan een tagbuild rechtstreeks via SFTP naar uw servers gaan. U kunt ook naar [!DNL Akamai] gaan en deze downloaden met de archiefoptie van uw omgeving.

Voor meer informatie, zie [&#x200B; Gastheren &#x200B;](../ui/publishing/hosts/hosts-overview.md).

### Omgevingen

Elke bibliotheek wordt binnen een omgeving gemaakt. Een milieu bepaalt hoe u uw bouwstijl wilt kijken wanneer het wordt gepubliceerd. U kunt het volgende opgeven:

* **Gastheer:** Elk milieu heeft een gastheer nodig die het eindpunt bepaalt waar om het even welk bouwt die in dit milieu wordt gecreeerd zal worden geduwd.
* **Archief:** het gebrek dat moet uw bouwstijl als geminificeerde .js- dossier opstellen. Als u aangepaste code gebruikt, kunnen er meerdere bestanden zijn die naar elkaar verwijzen. Deze kunnen worden gecombineerd in één zip-bestand en gecodeerd.

Nadat u de omgeving hebt opgeslagen, wordt de insluitcode gegenereerd die u kunt kopiëren en in uw website kunt plakken. De insluitcode werkt pas nadat u een bibliotheek hebt gemaakt en een build hebt gemaakt. Voor meer informatie, zie [&#x200B; Milieu&#39;s &#x200B;](../ui/publishing/environments.md).

### Een build publiceren naar Dev

Het publicatieproces wordt in de onderstaande stappen beschreven.

1. Maak een host.
1. Maak een ontwikkelomgeving met de host die u hebt gemaakt.
1. Implementeer de insluitcode van uw ontwikkelomgeving naar uw testsite voor ontwikkelaars.
1. Maak een bibliotheek en wijs deze toe aan de ontwikkelomgeving die u hebt gemaakt.
1. Bouw uw bibliotheek.

## &#x200B;7. Bevordering van de productie

Nadat u uw bouwstijl in uw ontwikkelomgeving hebt getest, zorg ervoor om uw stadium en productiemilieu&#39;s tot stand te brengen en de ingebedde codes op de noodzakelijke plaatsen te zetten. Voor dit doel kunt u bestaande hosts opnieuw gebruiken.

Voor de bevordering van een bibliotheek tot aan de productie is meestal coördinatie tussen verschillende mensen met de juiste rechten nodig.

* Een ontwikkelaar (iemand met de ontwikkelaar naar rechts) verzendt de bibliotheek, die de bibliotheek naar de verzendstatus verplaatst.
* Een fiatteur (iemand met het recht Goedkeuren) kan de bibliotheek bouwen in de werkgebiedomgeving en deze na het testen goedkeuren. Hierdoor wordt de bibliotheek naar de goedgekeurde status verplaatst. Er kan slechts één bibliotheek tegelijk worden verzonden en goedgekeurd.
* Een uitgever (iemand met het recht Publiceren) kan de bibliotheek aan het productiemilieu bouwen.

U kunt al deze rechten aan één persoon toewijzen.

Voor meer informatie over de verschillende staten en de opties beschikbaar tijdens het het publiceren proces, zie [&#x200B; Werkschema van de Goedkeuring &#x200B;](../ui/publishing/publishing-flow.md).

## Aanvullende bronnen

Raadpleeg de volgende bronnen voor meer informatie over tags:

* **[Gemeenschap van de Inzameling van Gegevens &#x200B;](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/ct-p/adobe-launch-community)**: Vraag en beantwoord vragen, voorlegt ideeën, stem op de ideeën van anderen. Meld u aan bij uw Adobe ID.
* **[Docs van de Ontwikkelaar](../api/overview.md)**: Krijg betrokken met de gemeenschap van de markeringsontwikkelaar om uitbreidingen te bouwen of de markeringen APIs te gebruiken
* **[het Overzicht van Leerprogramma&#39;s &#x200B;](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/overview.html?lang=nl-NL)**: Deze documenten introduceren u aan markeringsconcepten met inbegrip van gebeurtenis door:sturen en Mobiele SDK in de Apps van Android.
