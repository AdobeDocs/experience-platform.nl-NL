---
title: Doel van Google Ad Manager
seo-title: Doel van Google Ad Manager
description: 'Google Ad Manager, voorheen bekend als DoubleClick voor uitgevers of DoubleClick AdX, is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren. '
seo-description: 'Google Ad Manager, voorheen bekend als DoubleClick voor uitgevers of DoubleClick AdX, is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren. '
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---


# [!DNL Google Ad Manager Destination]

## Overzicht

[!DNL Google Ad Manager], voorheen bekend [!DNL DoubleClick] bij Publishers of [!DNL DoubleClick AdX], is een advertentieplatform van [!DNL Google] uitgevers dat uitgevers de middelen geeft om de weergave van advertenties op hun websites te beheren, via video en in mobiele apps.

## Doelspecificaties

Let op de volgende details die specifiek zijn voor [!DNL Google Ad Manager] bestemmingen:

* U kunt de volgende [identiteiten](../../identity-service/namespaces.md) naar [!DNL Google Ad Manager] bestemmingen verzenden: **Google-cookie-id, IDFA, GAID, Roku-id&#39;s, Microsoft-id&#39;s, Amazon Fire TV-id&#39;s**.
* Geactiveerd publiek wordt programmatically gecreeerd op het [!DNL Google] platform.
* Adobe Real-time CDP bevat momenteel geen metrische waarde om succesvolle activering te valideren. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en inzicht te krijgen in doelgroepen.

>[!IMPORTANT]
>
>Als u uw eerste bestemming wilt maken met [!DNL Google Ad Manager] en in het verleden (met Audience Manager of andere toepassingen) de functionaliteit [voor het synchroniseren van](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) id&#39;s niet hebt ingeschakeld in de Experience Cloud-id-service, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder [!DNL Google] integraties in Audience Manager had ingesteld, worden de synchronisaties van de id die u had ingesteld overgedragen naar Adobe Real-time CDP.

## Vereisten

### Lijst van gewenste personen

>[!NOTE]
>
>De lijst van gewenste personen is verplicht voordat u uw eerste [!DNL Google Ad Manager] bestemming instelt in Adobe Real-time CDP. Controleer of het hieronder beschreven lijst van gewenste personen-proces is voltooid door [!DNL Google] voordat u een doel maakt.

Voordat u de [!DNL Google Ad Manager] bestemming maakt in Adobe Real-time CDP, moet u contact opnemen [!DNL Google] om Adobe op de lijst met toegestane gegevensproviders te plaatsen en om uw account aan de lijst van gewenste personen toe te voegen. Neem contact op met [!DNL Google] en geef de volgende informatie op:

* **Account-id** : Dit is de account-id van Adobe met [!DNL Google]. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* **Klant-id** : Dit is de Adobe-id voor de klantenaccount met [!DNL Google]. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* **Netwerk-id** : dit is je account met [!DNL Google Ad Manager]
* **Koppelings-id** publiek: dit is je account met [!DNL Google Ad Manager]
* Je accounttype. **DFP door Google** - of **AdX-koper**.

## Doel maken

1. Selecteer in **[!UICONTROL Verbindingen > Doelen]** de optie [!DNL Google Ad Manager]en selecteer **[!UICONTROL Doel]**maken.
   ![Doel van Google Ad Manager verbinden](/help/rtcdp/destinations/assets/google-1-destination.png)

2. In de stap van de **Opstelling** van creeer bestemmingswerkschema, vul de [!UICONTROL BasisInformatie] voor de bestemming in. <br>

   ![Basisinformatie Google Ad Manager](/help/rtcdp/destinations/assets/google-1-destination-setup-step.png)
* **[!UICONTROL Naam]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Omschrijving]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Accounttype]**: Selecteer een optie, afhankelijk van uw account bij Google:
   * Gebruiken `DFP by Google` voor [!DNL DoubleClick] uitgevers
   * Gebruiken `AdX buyer` voor [!DNL Google AdX]
* **[!UICONTROL Account-id]**: Vul je account-id in met [!DNL Google]. Dit kan uw identiteitskaart van het Netwerk of uw identiteitskaart van de Verbinding van het publiek zijn. Dit is doorgaans een id van acht cijfers.
* **[!UICONTROL Geval]** voor gebruik bij het in de handel brengen: Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde gevallen voor marketinggebruik of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Voor meer informatie over het op de markt brengen van gebruiksgevallen, zie de [Governance van Gegevens in Echte tijd CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) pagina. Zie het overzicht [van het beleid voor](/help/data-governance/policies/overview.md#core-actions)gegevensgebruik voor informatie over de afzonderlijke door Adobe gedefinieerde gevallen van marketinggebruik.

> [!NOTE]
>
> Wanneer u een [!DNL Google Ad Manager] bestemming instelt, werkt u samen met uw [!DNL Google Account Manager] of Adobe-vertegenwoordiger om te begrijpen welk accounttype u hebt.

## Segmenten activeren om [!DNL Google Ad Manager]

Voor instructies op hoe te om segmenten te activeren, zie [!DNL Google Ad Manager]Gegevens aan Doelen [](/help/rtcdp/destinations/activate-destinations.md)activeren.