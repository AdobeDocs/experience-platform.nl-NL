---
title: Google AdsDestination
seo-title: Bestemming voor Google-advertenties
description: Google Ads, voorheen bekend als Google AdWords, is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten op tekstbasis, grafische beeldschermen, YouTube-video's en mobiele displays in de app.
seo-description: Google Ads, voorheen bekend als Google AdWords, is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten op tekstbasis, grafische beeldschermen, YouTube-video's en mobiele displays in de app.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---


# [!DNL Google Ads] Bestemming

## Overzicht

[!DNL Google Ads], voorheen bekend als [!DNL Google AdWords], is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten op tekstbasis, grafische weergaven, [!DNL YouTube] video&#39;s en mobiele weergaven in de app.

## Doelspecificaties

Let op de volgende details die specifiek zijn voor [!DNL Google Ads] bestemmingen:

* U kunt de volgende [identiteiten](../../identity-service/namespaces.md) naar [!DNL Google Ads] bestemmingen verzenden: **Google-cookie-id, IDFA, GAID, Roku-id&#39;s, Microsoft-id&#39;s, Amazon Fire TV-id&#39;s**.
* Geactiveerd publiek wordt programmatically gecreeerd op het [!DNL Google] platform.
* Adobe Real-time CDP bevat momenteel geen metrische waarde om succesvolle activering te valideren. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en inzicht te krijgen in doelgroepen.

>[!IMPORTANT]
>
>Als u uw eerste bestemming wilt maken met [!DNL Google Ads] en in het verleden (met Audience Manager of andere toepassingen) de functionaliteit [voor het synchroniseren van](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) id&#39;s niet hebt ingeschakeld in de Experience Cloud-id-service, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder Google-integraties in Audience Manager had ingesteld, worden de synchronisaties van de id die u had ingesteld overgedragen naar Adobe Real-time CDP.

## Vereisten

### Bestaande [!DNL Google Ads] account

[!DNL Google] heeft alle nieuwe [!DNL Google Ads] integraties met externe leveranciers gepauzeerd. U moet een bestaande integratie hebben met [!DNL Google Ads] om de stappen van de lijst van gewenste personen in de volgende sectie te kunnen uitvoeren en een [!DNL Google Ads] bestemming in Echte Adobe CDP te creëren.

### Lijst van gewenste personen

>[!NOTE]
>
>De lijst van gewenste personen is verplicht voordat u uw eerste [!DNL Google Ads] bestemming instelt in Adobe Real-time CDP. Controleer of het hieronder beschreven lijst van gewenste personen-proces is voltooid door [!DNL Google] voordat u een doel maakt.

Voordat u de [!DNL Google Ads] bestemming maakt in Adobe Real-time CDP, moet u contact opnemen [!DNL Google] om Adobe op de lijst met toegestane gegevensproviders te plaatsen en om uw account aan de lijst van gewenste personen toe te voegen. Neem contact op met [!DNL Google] en geef de volgende informatie op:

* **Account-id** : Dit is de account-id van Adobe met [!DNL Google]. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* **Klant-id** : Dit is de Adobe-id voor de klantenaccount met [!DNL Google]. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* Je accounttype: **AdWords**
* **Google AdWords-id** : Dit is je ID met [!DNL Google]. De id-indeling heeft doorgaans de notatie 123-456-7890.

## Doel maken

1. Selecteer in **[!UICONTROL Verbindingen > Doelen]** de optie [!DNL Google Ads]en selecteer **[!UICONTROL Doel]**maken.
   ![Google Ads-doel verbinden](/help/rtcdp/destinations/assets/google-2-destination.png)

2. In de stap van de **Opstelling** van creeer bestemmingswerkschema, vul de [!UICONTROL BasisInformatie] voor de bestemming in. <br>

   ![Basisinformatie over Google Ads](/help/rtcdp/destinations/assets/google-2-destination-setup-step.png)
* **[!UICONTROL Naam]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Omschrijving]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Accounttype]**: De enige beschikbare optie is AdvertentieWoorden.
* **[!UICONTROL Account-id]**: Vul je account-id in met [!DNL Google Ads]. De id-indeling heeft doorgaans de notatie 123-456-7890.
* **[!UICONTROL Geval]** voor gebruik bij het in de handel brengen: Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde gevallen voor marketinggebruik of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Voor meer informatie over het op de markt brengen van gebruiksgevallen, zie de [Governance van Gegevens in Echte tijd CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) pagina. Zie het overzicht [van het beleid voor](/help/data-governance/policies/overview.md#core-actions)gegevensgebruik voor informatie over de afzonderlijke door Adobe gedefinieerde gevallen van marketinggebruik.

## Segmenten activeren om [!DNL Google Ads]

Voor instructies op hoe te om segmenten te activeren, zie [!DNL Google Ads]Gegevens aan Doelen [](/help/rtcdp/destinations/activate-destinations.md)activeren.

