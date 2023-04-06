---
keywords: gebeurtenis door:sturen uitbreiding;mixpanel;mixpanel gebeurtenis door:sturen uitbreiding
title: Mixpanel Track Events API Event Forwarding Extension
description: Deze Adobe Experience Platform-extensie voor het doorsturen van gebeurtenissen verzendt Adobe Experience Edge Network-gebeurtenissen naar Mixpanel.
source-git-commit: 8538e3a2899c3e2451519996cabeffc4b42d706c
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] API-extensie voor doorsturen van gebeurtenissen

[[!DNL Mixpanel]](https://www.mixpanel.com) is een hulpprogramma voor productanalyse waarmee u gegevens kunt vastleggen over de manier waarop gebruikers met een digitaal product werken. U kunt productgegevens analyseren met eenvoudige, interactieve rapporten die u de gegevens laten vragen en visualiseren met slechts een paar klikken. [!DNL Mixpanel] ontworpen om teams efficiënter te maken door iedereen toe te staan om gebruikersgegevens in echt te analyseren - tijd om tendensen te identificeren, gebruikersgedrag te begrijpen, en besluiten over uw product te nemen.

[!DNL Mixpanel] Gebruikt een op gebeurtenis-gebaseerd, gebruiker-centric model dat elke interactie met één enkele gebruiker verbindt. De [!DNL Mixpanel] het gegevensmodel wordt voortgebouwd op de concepten gebruikers, gebeurtenissen, en eigenschappen.

>[!NOTE]
>
>Zie de [!DNL Mixpanel] documentatie over [identiteitsbeheer](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) om te begrijpen hoe [!DNL Mixpanel] Voegt gebeurtenissen samen om identiteitsclusters te maken. U wordt ook aangeraden het document te controleren op [afzonderlijke id&#39;s](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) om te begrijpen hoe ze worden gebruikt om gebruikers in gebeurtenisgegevens te identificeren.

## Gebruiksscenario’s

Deze extensie moet worden gebruikt als u gegevens van het Edge-netwerk wilt gebruiken in [!DNL Mixpanel] om te profiteren van de mogelijkheden voor productanalyse.

Neem bijvoorbeeld een detailhandelsorganisatie met meerdere kanalen (website en mobiel). De organisatie vangt transactie of gespreksinvoer als gebeurtenisgegevens van hun platforms en laadt het in [!DNL Mixpanel] het gebruiken van de gebeurtenis die uitbreiding door:sturen.

De analyseteams kunnen vervolgens gebruikmaken van [!DNL Mixpanel's] mogelijkheden om de datasets te verwerken en bedrijfsinzichten af te leiden, die kunnen worden gebruikt om grafieken, dashboards, of andere visualisaties te produceren om bedrijfsbelanghebbenden te informeren.

Voor meer informatie over gebruiksgevallen die specifiek zijn voor [!DNL Mixpanel]Raadpleeg de volgende documentatie:

* [Nieuw bij [!DNL Mixpanel]](https://help.mixpanel.com/hc/en-us/sections/360008533532-New-to-Mixpanel)
* [Wat is [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [12 moet-try [!DNL Mixpanel] functies](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] voorwaarden {#prerequisites-mixpanel}

U moet een geldige [!DNL Mixpanel] om deze extensie te gebruiken. Ga naar de [[!DNL Mixpanel] registratiepagina](https://mixpanel.com/register/) als u nog geen account hebt, kunt u zich registreren en een account maken.

Zorg ervoor dat de [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) het plaatsen wordt toegelaten voor uw project. Navigeren naar **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** en schakelt u de instelling in.

### Identiteitsclusters begrijpen in [!DNL Mixpanel]

In [!DNL Mixpanel], bevat een identiteitscluster een verzameling van `distinct_id` waarden die verbinding maken met een individuele gebruiker. [!DNL Mixpanel] handelt de cluster van identiteiten voor elke gebruiker af, die één enkel canonicaal oplost `distinct_id` van elke cluster die bij de rapportage moet worden gebruikt. U kunt ook uw eigen id (ook wel een lokale id genoemd) opnemen `distinct_id`) voor anonieme gebeurtenissen die vóór een gebruikersidentificatie plaatsvinden.

[!DNL Mixpanel] Hiermee worden identiteitsclusters op twee manieren opgelost:

* **Identificeren** : [!DNL Mixpanel] verbindt uw gekozen herkenningsteken met anoniem `distinct_id`. Als uw website de [!DNL Mixpanel] SDK ingeschakeld, Platform gebruikt de `distinct_id` toegewezen aan de gebruiker die momenteel is aangemeld.
* **Alias**: [!DNL Mixpanel] combineert twee niet-anonieme `distinct id`s samen als aan extra fusiecriteria wordt voldaan.

>[!NOTE]
>
>Zie de [!DNL Mixpanel] document op [identiteitsbeheer](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) voor meer informatie over deze methoden .
>
>Bevestig dat u de [[!DNL Mixpanel] samenvoegfunctie](#prerequisites-mixpanel) ervoor te zorgen dat identiteitsclusters op passende wijze worden opgelost.

### Verzamel vereiste configuratiedetails {#configuration-details}

Om Experience Platform met te verbinden [!DNL Mixpanel] u moet de volgende input hebben:

| Type toets | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Projecttoken | Het projecttoken dat aan uw [!DNL Mixpanel] account. Zie de [!DNL Mixpanel] documentatie over [zoeken, projecttoken](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) ter begeleiding. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Installeer en configureer de [!DNL Mixpanel] extension {#install}

Als u de extensie wilt installeren, [een eigenschap voor het doorsturen van gebeurtenissen maken](../../../ui/event-forwarding/overview.md#properties) of kies een bestaande eigenschap die u wilt bewerken.

Selecteren **[!UICONTROL Extensions]** in de linkernavigatie. In de **[!UICONTROL Catalog]** tab, selecteert u **[!UICONTROL Install]** op de kaart voor de [!DNL Mixpanel] extensie.

![De installatie van de [!DNL Mixpanel] extensie.](../../../images/extensions/server/mixpanel/install-extension.png)

## Een [!DNL Send Event] regel

Begin creërend een nieuwe regel in uw gebeurtenis door:sturen bezit. Onder **[!UICONTROL Actions]** voegt u een nieuwe handeling toe en stelt u de extensie in op **[!UICONTROL Mixpanel]**. Stel vervolgens het handelingstype in op **[!UICONTROL Track Event]** om Adobe Experience Edge Network-gebeurtenissen naar [!DNL Mixpanel].

| Invoer | Beschrijving | Vereist |
| --- | --- | --- |
| [!UICONTROL Project Token] | Dit gebied zou aan het projectteken verbonden aan uw moeten in kaart worden gebracht [!DNL Mixpanel] account. | Ja |
| [!UICONTROL Event Type] | De naam van de gebeurtenis. | Ja |
| [!UICONTROL Event Time] | De tijd van de gebeurtenis. |  |
| [!UICONTROL Mixpanel Distinct ID] | De unieke id van de gebruiker die de gebeurtenis heeft uitgevoerd. |  |
| [!UICONTROL Insert ID] | Een unieke id voor de gebeurtenis, die wordt gebruikt voor deduplicatie. |  |
| [!UICONTROL Event Properties] | Een JSON-object dat aangepaste eigenschappen van de gebeurtenis bevat. Maak een keuze uit het opgeven van onbewerkte JSON of uit het gebruik van een vereenvoudigde set toetsinvoer. |  |

>[!NOTE]
>
>Voor meer informatie over de standaardvelden voor een [!DNL Mixpanel] gebeurtenis, raadpleegt u de [officiële documentatie](https://developer.mixpanel.com/reference/import-events#event).

![Voeg een gebeurtenis toe die de configuratie van de regelactie door:sturen.](../../../images/extensions/server/mixpanel/track-event-action.png)

Wanneer de [!UICONTROL Track Event] de actie wordt toegevoegd aan de regel, kunt u de voorwaarden van de regel vormen zodat het slechts voor bepaalde gebeurtenissen brandt, of u kunt de voorwaardesectie leeg verlaten om de regelbrand voor alle gebeurtenissen te maken.

>[!IMPORTANT]
>
>Als uw website de [!DNL Mixpanel] SDK, kunt u aan de volgende stap van verdergaan [valideren, uw gegevens binnen [!DNL Mixpanel]](#validate). Als u het [!DNL Mixpanel] SDK, u moet [een afzonderlijke regel voor het bijhouden van identiteiten maken](#create-an-identity-tracking-rule) ervoor te zorgen dat passende gebeurtenissen en `distinct_id` waarden worden verzonden naar [!DNL Mixpanel] wanneer een gebruikersidentificatie-gebeurtenis plaatsvindt.

## Gegevens valideren binnen [!DNL Mixpanel] {#validate}

Als uw implementatie succesvol is en gebeurtenissen worden verzameld, ziet u gebeurtenissen in het dialoogvenster [[!DNL Mixpanel] console](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Controleren of [!DNL Mixpanel] heeft de gebeurtenissen voor na aanmelding samengevoegd met e-mailwaarden en de gebeurtenissen die bij het gebruik zijn gemaakt **[!UICONTROL Send Event]**. Indien correct geïmplementeerd, [!DNL Mixpanel] zal hen met één enkele associëren [gebruikersprofiel](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Volgende stappen

In deze handleiding wordt beschreven hoe conversiegebeurtenissen naar [!DNL Mixpanel] het gebruiken van gebeurtenis door:sturen. Deze gebeurtenis die uitbreiding door:sturen hefboomwerkingen [!DNL Mixpanel] SDK en JavaScript API. Raadpleeg de officiële documentatie voor meer informatie over deze onderliggende technologieën:

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] JavaScript-API](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Voor meer informatie over gebeurtenis die mogelijkheden in Experience Platform door:sturen, verwijs naar [overzicht van gebeurtenissen doorsturen](../../../ui/event-forwarding/overview.md).
