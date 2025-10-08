---
title: Weergave van inhoudskaarten
description: In deze handleiding vindt u informatie over de weergave Content Cards in Adobe Experience Platform Assurance.
source-git-commit: fa5dbbfcc0c178c8886000479f44afd5d63c8c34
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# Weergave Inhoudskaarten in Assurance

In de weergave Berichten in de app in Adobe Experience Platform Assurance kunt u uw app valideren, de inhoudskaarten controleren die aan uw apparaat worden geleverd en voorvertoningskaarten.

## Inhoudskaarten

Boven aan het tabblad **[!UICONTROL Content Cards]** bevindt zich een **[!UICONTROL Content Card]** -vervolgkeuzelijst. Hier worden alle inhoudskaarten weergegeven die in de Assurance-sessie zijn ontvangen. Als een kaart niet in deze lijst voorkomt, betekent dit dat de app deze nooit heeft ontvangen.

![ dropdown van de Kaart van de Inhoud die een lijst van kaarten ](./images/content-cards/dropdown.png) bevat

Als u een inhoudskaart selecteert, wordt veel informatie over die kaart weergegeven, zoals in de onderstaande secties wordt beschreven.

### Kaartvoorvertoning

In het rechterdeelvenster vindt u een deelvenster **[!UICONTROL Card Preview]** waarin wordt weergegeven hoe een kaart wordt weergegeven in algemene sjablonen: Kleine afbeelding, Grote afbeelding en Alleen afbeelding.

![ Voorproef van geselecteerde Kaart van de Inhoud ](./images/content-cards/preview.png)

Met de schakeloptie **[!UICONTROL Theme]** kunt u de kaart in lichte of donkere modus bekijken.

![ Voorproef van geselecteerde Kaart van de Inhoud in Donker Thema ](./images/content-cards/preview-dark.png)

### Beschikbare tabbladen

In de linkersectie zijn de beschikbare tabbladen afhankelijk van de geselecteerde kaart. Als de kaart regels bevat, ziet u drie tabbladen: **[!UICONTROL Info]**, **[!UICONTROL Interactions]** en **[!UICONTROL Analyze Rules]** .

![ Beschikbare lusjes wanneer de regels aanwezig zijn: Info, Interacties, Analyseer Regels ](./images/content-cards/tabs-with-rules.png)

Als de kaart geen regels bevat, ziet u twee tabbladen: **[!UICONTROL Info]** en **[!UICONTROL Interactions]** .

![ Beschikbare lusjes wanneer geen regels: Info en Interacties ](./images/content-cards/tabs-no-rules.png)

### Het tabblad Info

Op het tabblad **[!UICONTROL Info]** wordt de sectie **[!UICONTROL Card Properties]** boven weergegeven, inclusief badges voor de **[!UICONTROL Current State]** -component (trigger, display, dismiss, diskwalificeren) plus metagegevens zoals **[!UICONTROL Template]** (Small Image, Large Image of Image Only) **[!UICONTROL Surface]** en eventuele aangepaste sleutel-waardeparen.

![ Eigenschappen van de Kaart die huidige staatsbadges, malplaatje, oppervlakte, en zeer belangrijke paren tonen ](./images/content-cards/card-properties.png)

Hieronder ziet u in de sectie **[!UICONTROL Campaign Properties]** informatie die is geladen uit Adobe Journey Optimizer (AJO).

U kunt ook **[!UICONTROL View Campaign]** selecteren om de kaart in AJO te openen voor inspectie of bewerking.

![ sectie van de Eigenschappen van de Campagne met knoop aan de Campagne van de Mening ](./images/content-cards/campaign-properties.png)

### Tabblad Interacties

Het tabblad **[!UICONTROL Interactions]** geeft een overzicht van de levenscyclus van elke kaart als een reeks badges: het begint altijd met **[!UICONTROL trigger]** , gevolgd door het resultaat dat de regels opleveren— **[!UICONTROL display]** , **[!UICONTROL dismiss]** of **[!UICONTROL disqualify]** .

![ lijst van Interacties die levenscyclusbadges van trekker tonen om te tonen, te sluiten, of te diskwalificeren ](./images/content-cards/interactions-tab.png)

### Het tabblad Regels analyseren

Het tabblad **[!UICONTROL Analyze]** toont een gebeurtenissentabel met maximaal drie regelkolommen— **[!UICONTROL Display]**, **[!UICONTROL Dismiss]** en **[!UICONTROL Disqualify]** - op basis van de regels van de kaart. Als de kaart slechts één regel definieert, wordt alleen die kolom weergegeven.

Elke rij vertegenwoordigt een zittingsgebeurtenis, en elke kolom wijst erop of de regel van de kaart voor de voorwaarden van die gebeurtenis paste. Een 0% score betekent dat er geen voorwaarden zijn die overeenkomen. 100% is een volledige overeenkomst (de regel wordt genegeerd).

Als de gebeurtenis overeenkomt met een voorwaarde, wordt een groen vinkje weergegeven. Als de gebeurtenis niet overeenkomt, wordt er een rood pictogram weergegeven.

![ analyseer lusjegebeurtenissen lijst met Vertoning, Ontwerpen, en ontkwalificeer regelkolommen ](./images/content-cards/rules-tab.png)

Gebruik de schuifregelaar **[!UICONTROL Match Threshold]** om gebeurtenissen te filteren op basis van een minimumpercentage.

![ de schuif van de Drempel van de Gelijke aan filtergebeurtenissen door minimumgelijke percentage ](./images/content-cards/match-threshold.png)

Wanneer u een gebeurtenis selecteert, wordt rechts een deelvenster met details geopend met een accordeon met de drie regels: **[!UICONTROL Display]**, **[!UICONTROL Dismiss]** en **[!UICONTROL Disqualify]** .

![ de details van de Gebeurtenis het paneellijst van Vertoning, Ontkenning, en ontkwalificeert regels ](./images/content-cards/rules-panel.png)

Breid om het even welke sectie uit om de voorwaarden van de regel te zien, welke voorwaarden, en het berekende gelijke percentage voor dat resultaat aanstemden.

![ Uitgebreide regelaccordion die gematchte voorwaarden tonen en percentage aanpassen ](./images/content-cards/expanded-accordion.png)

## Tabblad Verzoeken

Op het tabblad **[!UICONTROL Requests]** ziet u welke inhoudskaarten zijn aangevraagd en op welk oppervlak.

![ lusje van Verzoeken die de verzoeken van de Kaart van de Inhoud tonen ](./images/content-cards/requests-tab.png)

Gebruik de knop **[!UICONTROL View Card]** om terug te gaan naar het tabblad Informatie van een specifieke inhoudskaart.

## Tabblad Gebeurtenislijst

Het tabblad **[!UICONTROL Event List]** bevat sessiegebeurtenissen die relevant zijn voor inhoudskaarten, zoals AJO-propositieaanvragen/-reacties, gebeurtenissen over de levenscyclus van kaarten en het bijhouden van interactie. U kunt naar kolommen zoeken, deze filteren, sorteren en aanpassen, en u kunt resultaten exporteren.

Als u een gebeurtenis selecteert, wordt een detailvenster aan de rechterkant geopend met de onbewerkte payload en de belangrijkste kenmerken. U kunt gebeurtenissen ook markeren voor follow-up. Deze weergave is handig voor correlerende verzoeken, regelresultaten en interacties tijdens de sessie.

![ het lusje van de Lijst van de Gebeurtenis met doorzoekbare, filterbare zittingsgebeurtenissen voor de Kaarten van de Inhoud ](./images/content-cards/event-list.png)

## Tabblad Validatie

Op het tabblad **[!UICONTROL Validation]** worden validaties uitgevoerd op basis van uw huidige sessie. Hierbij wordt gecontroleerd of de app correct is geconfigureerd voor berichten:

![ de resultaten van het lusje van de Bevestiging die de configuratie van het Overseinen voor de huidige zitting controleren ](./images/content-cards/validation.png)
