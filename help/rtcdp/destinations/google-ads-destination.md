---
title: Google AdsDestination
seo-title: Bestemming voor Google-advertenties
description: Google Ads, voorheen bekend als Google AdWords, is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten op tekstbasis, grafische beeldschermen, YouTube-video's en mobiele displays in de app.
seo-description: Google Ads, voorheen bekend als Google AdWords, is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten op tekstbasis, grafische beeldschermen, YouTube-video's en mobiele displays in de app.
translation-type: tm+mt
source-git-commit: db2084024f7c25cb1f914f9b8da35298691fd95f
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 0%

---


# Bestemming voor Google-advertenties

## Overzicht

Google Ads, voorheen bekend als Google AdWords, is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten op tekstbasis, grafische beeldschermen, YouTube-video&#39;s en mobiele displays in de app.

## Doelspecificaties

Let op de volgende details die specifiek zijn voor Google Ads-doelen:

* U kunt de volgende [identiteiten](../../identity-service/namespaces.md) naar de bestemmingen van Google Ads verzenden: **Google-cookie-id, IDFA, GAID, Roku-id&#39;s, Microsoft-id&#39;s, Amazon Fire TV-id&#39;s**.
* Geactiveerd publiek wordt via programmacode gemaakt in het Google-platform.
* Adobe Real-time CDP bevat momenteel geen metrische waarde om succesvolle activering te valideren. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en inzicht te krijgen in doelgroepen.

>[!IMPORTANT]
>
>Als u uw eerste bestemming met Google Ads wilt maken en in het verleden (met Audience Manager of andere toepassingen) de functionaliteit [voor het synchroniseren van](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) id&#39;s in Experience Cloud ID Service niet hebt ingeschakeld, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder Google-integraties in Audience Manager had ingesteld, worden de synchronisaties van de id die u had ingesteld overgedragen naar Adobe Real-time CDP.

## Vereisten

### Bestaande Google Ads-account

Google heeft alle nieuwe Google Ads-integraties met externe leveranciers gepauzeerd. U moet een bestaande integratie met Google Ads hebben om de toegestane lijststappen in de volgende sectie te kunnen uitvoeren en een bestemming van de Advertentie van Google in Echte-tijd CDP van Adobe tot stand te brengen.

### Lijst toestaan

>[!NOTE]
>
>De lijst Toestaan is verplicht voordat u uw eerste Google Ads-bestemming instelt in Adobe Real-time CDP. Controleer of Google het hieronder beschreven proces voor het toestaan van lijsten heeft voltooid voordat u een bestemming maakt.

Voordat u de Google Ads-bestemming maakt in Adobe Real-time CDP, moet u contact opnemen met Google om Adobe op te nemen in de lijst met toegestane gegevensproviders en om uw account toe te voegen aan de lijst voor toestaan. Neem contact op met Google en geef de volgende informatie op:

* **Account-id** : Dit is de account-id van Adobe bij Google. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* **Klant-id** : Dit is de Adobe-id voor de klantenaccount bij Google. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* Je accounttype: **AdWords**
* **Google AdWords-id** : Dit is uw id met Google. De id-indeling heeft doorgaans de notatie 123-456-7890.

## Doel maken

1. Selecteer Google Ads in **[!UICONTROL Verbindingen > Doelen]** en selecteer **[!UICONTROL Doel]**maken.
   ![Google Ads-doel verbinden](/help/rtcdp/destinations/assets/google-2-destination.png)

2. In de stap van de **Opstelling** van creeer bestemmingswerkschema, vul de [!UICONTROL BasisInformatie] voor de bestemming in. <br>

   ![Basisinformatie over Google Ads](/help/rtcdp/destinations/assets/google-2-destination-setup-step.png)
* **[!UICONTROL Naam]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Omschrijving]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Accounttype]**: De enige beschikbare optie is AdvertentieWoorden.
* **[!UICONTROL Account-id]**: Vul je account-id in met Google Ads. De id-indeling heeft doorgaans de notatie 123-456-7890.
* **[!UICONTROL Geval]** voor gebruik bij het in de handel brengen: Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde gevallen voor marketinggebruik of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Voor meer informatie over het op de markt brengen van gebruiksgevallen, zie de [Governance van Gegevens in Echte tijd CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) pagina. Zie het overzicht [van het beleid voor](/help/data-governance/policies/overview.md#core-actions)gegevensgebruik voor informatie over de afzonderlijke door Adobe gedefinieerde gevallen van marketinggebruik.

## Segmenten activeren op Google Ads

Zie Gegevens naar bestemmingen [activeren voor instructies over het activeren van segmenten op Google Ads](/help/rtcdp/destinations/activate-destinations.md).

