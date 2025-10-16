---
title: Overzicht van Capillary Streaming-gebeurtenissen
description: Leer hoe u gegevens kunt streamen van Capillary naar Experience Platform.
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: 428aed259343f56a2bf493b40ff2388340fffb7b
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>De bron [!DNL Capillary Streaming Events] is in bèta. Lees de [ termijnen en voorwaarden ](../../home.md#terms-and-conditions) in het bronoverzicht voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

[!DNL Capillary Technologies] is een toonaangevend platform voor loyaliteit en betrokkenheid dat door meer dan 300 merken over de hele wereld wordt vertrouwd. Gebruik de [!DNL Capillary Streaming Events] -bron om uw bedrijf in staat te stellen probleemloos klantenprofielen, loyaliteitsgegevens en transactionele gebeurtenissen van [!DNL Capillary] naar Adobe Experience Platform te streamen. Sluit de [!DNL Capillary] -bron aan om realtime personalisatie, geavanceerde publiekssegmentatie en omnichannel campagneorchestratie mogelijk te maken.

Door [!DNL Capillary] te integreren met Experience Platform kunt u:

* Synchroniseer **loyaliteitpunten, rijen, en beloningen** in real time.
* Verzend **transactiegegevens** in Experience Platform voor analyse en activering.
* Gebruik Real-Time CDP, Experience Platform en Adobe Journey Optimizer voor segmentatie, reisorchestratie en personalisatie.

## Vereisten

Voordat u [!DNL Capillary] verbindt met Adobe Experience Platform, moet u het volgende controleren:

* Een geldige **identiteitskaart van de Organisatie van Adobe** en toegang tot een toegelaten zandbak van Experience Platform.
* U moet zowel **[!UICONTROL View Sources]** - als **[!UICONTROL Manage Sources]** -machtigingen hebben ingeschakeld voor uw account om uw [!DNL Capillary] -account te kunnen verbinden met Experience Platform. Neem contact op met de productbeheerder om de benodigde machtigingen te verkrijgen. Voor meer informatie, lees de [ gids UI van de toegangscontrole ](../../../access-control/ui/overview.md).

### Een schema maken

U moet een schema van het Model van Gegevens van de Ervaring (XDM) creëren om een dataset te beschrijven die de mogelijke gebieden en gegevenstypes kan opslaan die van [!DNL Capillary] zullen worden verzonden.

1. Meld u aan bij Adobe Experience Platform en open de Experience Platform via de aanmeldingsgegevens van uw organisatie.
2. Selecteer in het navigatievenster aan de linkerkant **[!UICONTROL Schemas]** om de werkruimte van [!UICONTROL Schemas] te openen.
3. Selecteer **[!UICONTROL Create schema]** in de rechterbovenhoek.
4. Kies in het dialoogvenster Schema maken de optie tussen **[!UICONTROL Manual creation]** (Velden en veldgroepen zelf toevoegen) of **[!UICONTROL ML-assisted creation]** (Upload een CSV-bestand en gebruik computerlessen om een aanbevolen schema te genereren).
5. Kies een basisklasse voor het schema (bijvoorbeeld XDM Individual Profile, XDM ExperienceEvent of Other). Als u **[!UICONTROL Other]** selecteert, kunt u een keuze maken uit beschikbare aangepaste of standaardklassen.
6. Voer een mensvriendelijke naam en beschrijving in voor uw schema.
7. Gebruik de Schema-editor om: veldgroepen (herbruikbare blokken velden) toe te voegen, afzonderlijke velden te definiëren (namen, gegevenstypen en opties aan te passen) en desgewenst aangepaste gegevenstypen of veldgroepen te maken als de bestaande niet op uw behoeften zijn afgestemd.
8. Controleer de schemastructuur in het canvas. Selecteer **[!UICONTROL Finish]** om het schema te maken.
9. (Optioneel) Bewerk velden, voeg beschrijvingen toe en pas zo nodig veldgroepen aan in de Schema-editor.

Voor gedetailleerde instructies op hoe te om een schema te creëren XDM, lees de gids bij [ het creëren van een schema gebruikend de schemageditor ](../../../xdm/tutorials/create-schema-ui.md).

### Een gegevensset maken

Daarna, moet u een dataset tot stand brengen die verwijzingen het schema u enkel creeerde.

1. Selecteer in de gebruikersinterface van Experience Platform de optie [!UICONTROL Datasets] in de linkernavigatie om de werkruimte van [!UICONTROL Datasets] te openen.
2. Selecteer **[!UICONTROL Create dataset]** rechtsboven.
3. Selecteer **[!UICONTROL Create dataset from schema]** in de opties voor het maken.
4. Zoek in de lijst naar het XDM-schema dat u eerder hebt gemaakt en selecteer dit schema. Selecteer **[!UICONTROL Next]** wanneer u het schema hebt gevonden.
5. Ga een unieke, beschrijvende naam voor uw dataset in.
6. Voeg desgewenst een beschrijving toe waarmee toekomstige gebruikers de gegevensset kunnen identificeren.
7. Selecteer **[!UICONTROL Finish]** om de gegevensset te maken.

Voor gedetailleerde instructies op hoe te om een dataset tot stand te brengen, lees de [ gids UI van datasets ](../../../catalog/datasets/user-guide.md).

## Verbinden [!DNL Capillary Streaming Events] met Experience Platform

Zodra u de eerste vereiste opstelling voor [!DNL Capillary] hebt voltooid, lees het [[!DNL Capillary Streaming Events]  leerprogramma UI ](../../tutorials/ui/create/loyalty/capillary.md) om te leren hoe u uw rekening en stroomgegevens van [!DNL Capillary] met Experience Platform kunt verbinden.
