---
title: Snelstartgids
description: Leer hoe u snel aan de slag kunt met tags in Adobe Experience Platform.
exl-id: 490ee344-3b18-4189-9293-2378f86fb10d
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1523'
ht-degree: 0%

---

# Snelstartgids

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Tags zijn Adobe Experience Platform van de volgende generatie technologie voor tagbeheer. Het wordt van de grond opgebouwd om een open en duurzaam ecosysteem te steunen waar iedereen zijn eigen integraties kan bouwen die de klanten van de Adobe aan hun plaatsen kunnen opstellen. Het is een eerste API-toepassing, dus alles wat u kunt doen via de UI, kunt u ook programmatisch doen via een API.

De basisworkflow voor labels:

1. Groepen en gebruikers instellen.
2. Meld u aan.
3. Maak een eigenschap.
4. Extensies installeren.
5. Maak gegevenselementen en regels.
6. Test in uw ontwikkelomgeving.
7. Bevorderen tot de productie.

## 1. Groepen en gebruikers instellen

Tags zijn volledig geïntegreerd met uw Adobe ID. De toestemmingen van de gebruiker worden beheerd door de Admin Console met andere producten en oplossingen van Adobe van de [!DNL Creative Cloud], [!DNL Document Cloud]en Experience Cloud.

Tags hebben een op rechten gebaseerd gebruikersbeheersysteem. Dit betekent dat individuele rechten expliciet moeten worden toegekend. Deze rechten worden toegewezen aan groepen, en gebruikers worden toegevoegd aan de juiste groepen om toegang te krijgen. Zelfs als uw organisatie toegang tot de Inzameling van Gegevens heeft, kunnen de individuele gebruikers niets doen tot een beheerder hen uitdrukkelijk sommige rechten verleent.

Voor gedetailleerde instructies over het maken van groepen en het toevoegen van gebruikers voor tags raadpleegt u de [machtigingengids voor gegevensverzameling](../../collection/permissions.md).

## 2. Aanmelden

Nadat de markeringsrechten aan uw Adobe ID zijn toegevoegd, moet u login aan het Experience Platform UI of UI van de Inzameling van Gegevens. U kunt dit doen door rechtstreeks naar de [Aanmeldingsscherm Experience Cloud](https://experience.adobe.com/)en selecteert u **[!UICONTROL Data Collection]** of **[!UICONTROL Experience Platform]**.

>[!NOTE]
>
>Als u één account met rechten voor meerdere organisaties hebt, kunt u de organisatie wijzigen door de naam van de organisatie te selecteren in de besturingsbalk boven in het scherm en een andere organisatie te kiezen in de vervolgkeuzelijst.

## 3. Een eigenschap maken

Nadat u zich hebt aangemeld bij de gebruikersinterface, maakt u eerst een eigenschap. Een eigenschap is in feite een container die u vult met extensies, regels, gegevenselementen en bibliotheken wanneer u tags op uw site implementeert. Veel mensen maken een eigenschap voor elke website (of groep nauw verwante sites) waar ze dezelfde set tags willen implementeren.

Zie voor meer informatie over het maken van eigenschappen [Een eigenschap maken](../ui/administration/companies-and-properties.md).

## 4. Extensies installeren

Een uitbreiding is een integratie die door Adobe of een partner van Adobe wordt gebouwd die nieuwe en eindeloze opties voor de markeringen toevoegt die u aan uw plaatsen kunt opstellen. Als u een tag ziet als een besturingssysteem, zijn extensies de apps die u installeert om de specifieke taken uit te voeren die u nodig hebt.

Alle nieuwe eigenschappen worden geleverd met de [Kernextensie](../extensions/web/core/overview.md) geïnstalleerd. Mobiele eigenschappen worden geleverd met extra extensies. De uitbreiding van de Kern wordt gebouwd door Adobe om een robuuste standaardreeks gegevenselementtypes voor uw gegevenslaag en gebeurtenistypen voor uw regels te verstrekken. De meeste handelingen die u wilt uitvoeren (een ECID ophalen, verzenden [!DNL Adobe Analytics] bakens, laadt de [!DNL Target] global mbox, enz.) zijn afkomstig van extensies die u installeert vanuit de catalogus.

Wat tags in Platform echt uniek maakt, is dat deze extensies door iedereen kunnen worden gemaakt. Moet u een Facebook-hermarketingpixel op uw site neerzetten? Bekijk de extensie die Facebook heeft gemaakt. Wilt u hetzelfde voor Twitter of Gekoppeld in? Gebruik deze extensies. Moet u een enquête uitvoeren? Kijk naar Vraag Pro of Voorzien. Moet u privacy beheren en toestemming van uw eindgebruikers geven om mee te werken? [!DNL GDPR]? Kijk goed naar Evidon en Vertrouwboog. Wilt u een gedetailleerd inzicht zien in het gedrag van individuele gebruikers op uw site? Kijk eens naar Clicktale. Zie de sectie over [toevoegen, nieuwe extensie](../ui/managing-resources/extensions/overview.md#add-a-new-extension).

## 5. Gegevenselementen en regels maken

**Gegevenselementen** Dit zijn aanwijzingen voor de informatie die u wilt verzamelen en naar verschillende plaatsen op uw pagina wilt verzenden:

* Een gedefinieerde gegevenslaag in JSON
* DOM-elementen
* Cookies
* Sessie en lokale opslag
* Alleen over alles

Nadat het gegevenselement wordt bepaald, kunt u het element overal in UI voor om het even welke uitbreiding gebruiken. Zie de documentatie op [Gegevenselementen](../ui/managing-resources/data-elements.md) voor meer gedetailleerde informatie.

**Regels** bevinden zich in de logische kern van uw implementatie en bepalen wat, wanneer, waar en hoe alle tags op uw site worden gebruikt. Definieer een gebeurtenis, stel voorwaarden en uitzonderingen in en definieer vervolgens de handelingen en volgorde. Tot slot publiceer uw veranderingen om de resultaten te zien. Zie voor meer informatie [Regels](../ui/managing-resources/rules.md).

## 6. Testen in uw ontwikkelomgeving

### Bibliotheken en builds

Tagbuilds worden nooit automatisch gepubliceerd. Elke set wijzigingen die u aanbrengt, wordt ingekapseld in een [bibliotheek](../ui/publishing/libraries.md). Elke bibliotheek u creeert erft automatisch om het even wat stroomopwaarts (gepubliceerd, goedgekeurd, of voorgelegd) als basislijn, zodat moet u slechts de veranderingen bepalen u wilt maken. Deze bibliotheek fungeert als blauwdruk voor een [build](../ui/publishing/builds.md). Een build is de feitelijke set JavaScript-bestanden die worden geïmplementeerd en gebruikt.

Het is belangrijk dat u de relatie begrijpt tussen uw webpagina, de hostlocatie en tags.

1. Uw hostserver biedt een locatie voor het publiceren van de build. De build zelf bevat de JavaScript-bestanden die door de bibliotheek worden vereist.

   Elk milieu heeft een verhouding met een gastheer, en de gastheer verstrekt een eindpunt erop wijst die waar te om de bouwstijl te leveren. De gastheer kan tot slechts één bezit behoren, hoewel een bezit vele gastheren kan hebben.

2. Er wordt een insluitcode in het formulier opgegeven  `<script>` -tag die in de `<head>` secties van uw website HTML.

   Wanneer u een milieu creeert en een gastheer vastmaakt, produceert het milieu automatisch een unieke inbedcode die u toestaat om zijn toegewezen bouwstijl in uw plaats te integreren. De `<script>` code wordt gebruikt om de bibliotheekbouwstijl bij runtime op te stellen.

3. Wanneer een gebruiker door uw site bladert, wordt de insluitcode `<script>` tag haalt de build op van uw hostserver en voert de gedefinieerde handelingen uit in de browser.

### Gastheren

Een host is een verbinding tussen een tag-eigenschap en uw hostlocatie. Tags bieden momenteel ondersteuning voor door Adobe beheerde hosting via een [!DNL Akamai] host of zelf-hosting via een SFTP-host. Tags maken verbinding met de server die door de host is gedefinieerd en leveren de build wanneer u een build maakt.

Als u zelf host, kan een tagbuild rechtstreeks via SFTP naar uw servers gaan of naar uw servers gaan [!DNL Akamai] en download deze met de optie Archiveren van uw omgeving.

Zie voor meer informatie [Gastheren](../ui/publishing/hosts/hosts-overview.md).

### Omgevingen

Elke bibliotheek wordt binnen een omgeving gemaakt. Een milieu bepaalt hoe u uw bouwstijl wilt kijken wanneer het wordt gepubliceerd. U kunt het volgende opgeven:

* **Host:** Elk milieu heeft een gastheer nodig die het eindpunt bepaalt waar om het even welke bouwstijlen die in dit milieu worden gecreeerd zullen worden geduwd.
* **Archief:** Standaard het plaatsen moet uw bouwstijl als geminificeerde .js dossier opstellen. Als u aangepaste code gebruikt, kunnen er meerdere bestanden zijn die naar elkaar verwijzen. Deze kunnen worden gecombineerd in één zip-bestand en gecodeerd.

Nadat u de omgeving hebt opgeslagen, wordt de insluitcode gegenereerd die u kunt kopiëren en in uw website kunt plakken. De insluitcode werkt pas nadat u een bibliotheek hebt gemaakt en een build hebt gemaakt. Zie voor meer informatie [Omgevingen](../ui/publishing/environments.md).

### Een build publiceren naar Dev

Het publicatieproces wordt in de onderstaande stappen beschreven.

1. Maak een host.
1. Maak een ontwikkelomgeving met de host die u hebt gemaakt.
1. Implementeer de insluitcode van uw ontwikkelomgeving naar uw testsite voor ontwikkelaars.
1. Maak een bibliotheek en wijs deze toe aan de ontwikkelomgeving die u hebt gemaakt.
1. Bouw uw bibliotheek.

## 7. Bevorderen tot productie

Nadat u uw bouwstijl in uw ontwikkelomgeving hebt getest, zorg ervoor om uw stadium en productiemilieu&#39;s tot stand te brengen en de ingebedde codes op de noodzakelijke plaatsen te zetten. Voor dit doel kunt u bestaande hosts opnieuw gebruiken.

Voor de bevordering van een bibliotheek tot aan de productie is meestal coördinatie tussen verschillende mensen met de juiste rechten nodig.

* Een ontwikkelaar (iemand met de ontwikkelaar naar rechts) verzendt de bibliotheek, die de bibliotheek naar de verzendstatus verplaatst.
* Een fiatteur (iemand met het recht Goedkeuren) kan de bibliotheek bouwen in de werkgebiedomgeving en deze na het testen goedkeuren. Hierdoor wordt de bibliotheek naar de goedgekeurde status verplaatst. Er kan slechts één bibliotheek tegelijk worden verzonden en goedgekeurd.
* Een uitgever (iemand met het recht Publiceren) kan de bibliotheek aan het productiemilieu bouwen.

U kunt al deze rechten aan één persoon toewijzen.

Voor meer informatie over de verschillende staten en opties beschikbaar tijdens het publicatieproces raadpleegt u [Goedkeuringswerkstroom](../ui/publishing/publishing-flow.md).

## Aanvullende bronnen

Raadpleeg de volgende bronnen voor meer informatie over tags:

* **[Gemeenschap voor gegevensverzameling](https://forums.adobe.com/community/experience-cloud/platform/launch)**: Stel vragen en beantwoord vragen, geef ideeën en stem over de ideeën van anderen. Meld u aan bij uw Adobe ID.
* **[Developer Docs](https://developer.adobelaunch.com/)**: Neem contact op met de ontwikkelaarscommunity voor tags om extensies te maken of de tags-API&#39;s te gebruiken
* **[Overzicht Tutorials](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/overview.html)**: Deze documenten introduceren u aan etiketteringsconcepten met inbegrip van gebeurtenis het door:sturen en Mobiele SDK in Android Apps.
