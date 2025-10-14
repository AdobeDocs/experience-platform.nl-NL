---
keywords: gebeurtenis door:sturen uitbreiding;mixpanel;mixpanel gebeurtenis door:sturen uitbreiding
title: Mixpanel Track Events API Event Forwarding Extension
description: Deze Adobe Experience Platform-gebeurtenis die een extensie doorstuurt, verzendt Edge Network-gebeurtenissen naar Mixpanel.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# [!DNL Mixpanel Track Events] API-gebeurtenis die extensie doorstuurt

[[!DNL Mixpanel] &#x200B;](https://www.mixpanel.com) is een hulpmiddel van de productanalyse dat u toestaat om gegevens te vangen over hoe de gebruikers met een digitaal product in wisselwerking staan. U kunt productgegevens analyseren met eenvoudige, interactieve rapporten die u de gegevens laten vragen en visualiseren met slechts een paar klikken. [!DNL Mixpanel] is ontworpen om teams efficiënter te maken door iedereen in staat te stellen gebruikersgegevens in real time te analyseren om tendensen te identificeren, gebruikersgedrag te begrijpen en besluiten over uw product te nemen.

[!DNL Mixpanel] maakt gebruik van een op gebeurtenissen gebaseerd, gebruikersgericht model dat elke interactie met één gebruiker verbindt. Het gegevensmodel van [!DNL Mixpanel] is gebaseerd op de concepten gebruikers, gebeurtenissen en eigenschappen.

>[!NOTE]
>
>Verwijs naar de [!DNL Mixpanel] documentatie over [&#x200B; identiteitsbeheer &#x200B;](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) om te begrijpen hoe [!DNL Mixpanel] gebeurtenissen samenvoegt om identiteitsclusters tot stand te brengen. Het wordt ook geadviseerd dat u het document op [&#x200B; verschillende IDs &#x200B;](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) herziet om te begrijpen hoe zij worden gebruikt om gebruikers in gebeurtenisgegevens te identificeren.

## Gebruiksscenario’s

Deze extensie moet worden gebruikt als u gegevens van de Edge Network in [!DNL Mixpanel] wilt gebruiken om te profiteren van de mogelijkheden voor productanalyse.

Neem bijvoorbeeld een detailhandelsorganisatie met meerdere kanalen (website en mobiel). De organisatie vangt transactie of gespreksinvoer als gebeurtenisgegevens van hun platforms en laadt het in [!DNL Mixpanel] gebruikend de gebeurtenis door:sturen uitbreiding.

De analyseteams kunnen vervolgens gebruikmaken van [!DNL Mixpanel's] -mogelijkheden om de gegevenssets te verwerken en bedrijfsinzichten af te leiden, die kunnen worden gebruikt om grafieken, dashboards of andere visualisaties te genereren om zakelijke belanghebbenden te informeren.

Raadpleeg de volgende documentatie voor meer informatie over gebruiksgevallen die specifiek zijn voor [!DNL Mixpanel] :

* [&#x200B; Nieuw aan  [!DNL Mixpanel] &#x200B;](https://docs.mixpanel.com/docs)
* [Wat is [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [&#x200B; 12 moet-probeer  [!DNL Mixpanel]  eigenschappen &#x200B;](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] voorwaarden {#prerequisites-mixpanel}

U moet een geldige [!DNL Mixpanel] -account hebben om deze extensie te kunnen gebruiken. Ga naar de [[!DNL Mixpanel]  registratiepagina &#x200B;](https://mixpanel.com/register/) om een rekening te registreren en tot stand te brengen als u niet reeds hebt.

Zorg ervoor dat het [[!DNL Identity Merge] &#x200B;](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) plaatsen voor uw project wordt toegelaten. Navigeer naar **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** en schakel de instelling in of uit.

### Identiteitsclusters begrijpen in [!DNL Mixpanel]

In [!DNL Mixpanel] bevat een identiteitscluster een verzameling `distinct_id` -waarden die verbinding maken met een individuele gebruiker. [!DNL Mixpanel] handelt de cluster met identiteiten voor elke gebruiker af, waarbij één canonicale `distinct_id` oplossing wordt gevonden voor elke cluster die bij de rapportage moet worden gebruikt. U kunt ook uw eigen id (ook wel een lokale `distinct_id` genoemd) opnemen voor anonieme gebeurtenissen die plaatsvinden vóór een gebruikersidentificatie-gebeurtenis.

[!DNL Mixpanel] verhelpt identiteitsclusters op twee manieren:

* **identificeer**: [!DNL Mixpanel] verbindt uw gekozen herkenningsteken met anoniem `distinct_id`. Als de [!DNL Mixpanel] SDK is ingeschakeld op uw website, gebruikt Experience Platform de `distinct_id` die is toegewezen aan de gebruiker die momenteel is aangemeld.
* **Alias**: [!DNL Mixpanel] combineert twee niet-anonieme `distinct id` s samen als de extra fusiecriteria worden voldaan.

>[!NOTE]
>
>Verwijs naar het [!DNL Mixpanel] document op [&#x200B; identiteitsbeheer &#x200B;](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) voor meer details op deze methodes.
>
>Bevestig dat u de [[!DNL Mixpanel]  eigenschap van de identiteitssamenvoeging &#x200B;](#prerequisites-mixpanel) hebt toegelaten om ervoor te zorgen dat de identiteitsclusters geschikt worden opgelost.

### Verzamel vereiste configuratiedetails {#configuration-details}

Als u Experience Platform wilt verbinden met [!DNL Mixpanel] , moet u over de volgende invoeren beschikken:

| Type toets | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Projecttoken | Het projecttoken dat aan uw [!DNL Mixpanel] -account is gekoppeld. Verwijs naar de [!DNL Mixpanel] documentatie op [&#x200B; het vinden van uw projectteken &#x200B;](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) voor begeleiding. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## De extensie [!DNL Mixpanel] installeren en configureren {#install}

Om de uitbreiding te installeren, [&#x200B; creeer een gebeurtenis door:sturen bezit &#x200B;](../../../ui/event-forwarding/overview.md#properties) of kies een bestaand bezit in plaats daarvan uit te geven.

Selecteer **[!UICONTROL Extensions]** in de linkernavigatie. Selecteer op het tabblad **[!UICONTROL Catalog]** **[!UICONTROL Install]** op de kaart voor de extensie [!DNL Mixpanel] .

![&#x200B; Installerend de [!DNL Mixpanel] uitbreiding.](../../../images/extensions/server/mixpanel/install-extension.png)

## Een [!DNL Send Event] -regel maken

Begin creërend een nieuwe regel in uw gebeurtenis door:sturen bezit. Voeg onder **[!UICONTROL Actions]** een nieuwe handeling toe en stel de extensie in op **[!UICONTROL Mixpanel]** . Stel vervolgens het handelingstype in op **[!UICONTROL Track Event]** om Edge Network-gebeurtenissen naar [!DNL Mixpanel] te verzenden.

| Invoer | Beschrijving | Vereist |
| --- | --- | --- |
| [!UICONTROL Project Token] | Dit veld moet worden toegewezen aan het projecttoken dat is gekoppeld aan uw [!DNL Mixpanel] -account. | Ja |
| [!UICONTROL Event Type] | De gebeurtenisnaam. | Ja |
| [!UICONTROL Event Time] | De gebeurtenistijd. | |
| [!UICONTROL Mixpanel Distinct ID] | De unieke id van de gebruiker die de gebeurtenis heeft uitgevoerd. | |
| [!UICONTROL Insert ID] | Een unieke id voor de gebeurtenis, die wordt gebruikt voor deduplicatie. | |
| [!UICONTROL Event Properties] | Een JSON-object dat aangepaste eigenschappen van de gebeurtenis bevat. Maak een keuze uit het opgeven van onbewerkte JSON of uit het gebruik van een vereenvoudigde set toetsinvoer. | |

>[!NOTE]
>
>Voor meer informatie over de standaardgebieden voor a [!DNL Mixpanel] gebeurtenis, verwijs naar de [&#x200B; officiële documentatie &#x200B;](https://developer.mixpanel.com/reference/import-events#event).

![&#x200B; voeg een gebeurtenis toe door:sturen de configuratie van de regelactie.](../../../images/extensions/server/mixpanel/track-event-action.png)

Zodra de [!UICONTROL Track Event] actie aan de regel wordt toegevoegd, kunt u de voorwaarden van de regel vormen zodat het slechts voor bepaalde gebeurtenissen brandt, of u kunt de voorwaardesectie leeg verlaten om de regelbrand voor alle gebeurtenissen te maken.

>[!IMPORTANT]
>
>Als uw website [!DNL Mixpanel] SDK gebruikt, kunt u aan de volgende stap van [&#x200B; blijven valideren uw gegevens binnen  [!DNL Mixpanel]](#validate). Als u niet [!DNL Mixpanel] SDK gebruikt, moet u [&#x200B; een afzonderlijke identiteit het volgen regel &#x200B;](#create-an-identity-tracking-rule) tot stand brengen om ervoor te zorgen dat de aangewezen gebeurtenissen en `distinct_id` waarden naar [!DNL Mixpanel] worden verzonden wanneer een gebeurtenis van de gebruikersidentificatie voorkomt.

## Gegevens valideren binnen [!DNL Mixpanel] {#validate}

Als uw implementatie succesvol is en de gebeurtenissen worden verzameld, zult u gebeurtenissen binnen de [[!DNL Mixpanel]  console &#x200B;](https://help.mixpanel.com/hc/en-us/articles/4402837164948) zien.

Controleer of [!DNL Mixpanel] de gebeurtenissen voor na aanmelding heeft samengevoegd die zijn gevuld met e-mailwaarden en de gebeurtenissen die zijn gemaakt bij het gebruik van **[!UICONTROL Send Event]** . Indien correct uitgevoerd, [!DNL Mixpanel] zal hen met één enkel [&#x200B; gebruikersprofiel &#x200B;](https://help.mixpanel.com/hc/en-us/articles/115004501966) associëren.

## Volgende stappen

In deze handleiding wordt beschreven hoe conversiegebeurtenissen naar [!DNL Mixpanel] kunnen worden verzonden via het doorsturen van gebeurtenissen. Deze extensie voor het doorsturen van gebeurtenissen maakt gebruik van de [!DNL Mixpanel] SDK en JavaScript API. Raadpleeg de officiële documentatie voor meer informatie over deze onderliggende technologieën:

* [[!DNL Mixpanel]  SDK &#x200B;](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel]  JavaScript API &#x200B;](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Voor meer informatie over gebeurtenis die mogelijkheden in Experience Platform door:sturen, verwijs naar de [&#x200B; gebeurtenis die overzicht &#x200B;](../../../ui/event-forwarding/overview.md) door:sturen.
