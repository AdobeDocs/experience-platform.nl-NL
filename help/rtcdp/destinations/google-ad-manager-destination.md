---
title: Doel van Google Ad Manager
seo-title: Doel van Google Ad Manager
description: 'Google Ad Manager, voorheen bekend als DoubleClick voor uitgevers of DoubleClick AdX, is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren. '
seo-description: 'Google Ad Manager, voorheen bekend als DoubleClick voor uitgevers of DoubleClick AdX, is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren. '
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---


# Doel van Google Ad Manager

## Overzicht

Google Ad Manager, voorheen bekend als DoubleClick voor uitgevers of DoubleClick AdX, is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren.

## Doelspecificaties

Let op de volgende details die specifiek zijn voor de doelen van Google Ad Manager:

* U kunt de volgende [identiteiten](../../identity-service/namespaces.md) naar de bestemmingen van Google Ad Manager verzenden: **Google-cookie-id, IDFA, GAID, Roku-id&#39;s, Microsoft-id&#39;s, Amazon Fire TV-id&#39;s**.
* Geactiveerd publiek wordt via programmacode gemaakt in het Google-platform.
* Adobe Real-time CDP bevat momenteel geen metrische waarde om succesvolle activering te valideren. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en inzicht te krijgen in doelgroepen.

>[!IMPORTANT]
>
>Als u uw eerste bestemming wilt maken met Google Ad Manager en in het verleden (met Audience Manager of andere toepassingen) de functionaliteit [voor het synchroniseren van](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) id&#39;s niet hebt ingeschakeld in de Experience Cloud ID Service, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder Google-integraties in Audience Manager had ingesteld, worden de synchronisaties van de id die u had ingesteld overgedragen naar Adobe Real-time CDP.

## Vereisten

### Lijst toestaan

>[!NOTE]
>
>De lijst Toestaan is verplicht voordat u de eerste bestemming van Google Ad Manager in Adobe Real-time CDP instelt. Controleer of Google het hieronder beschreven proces voor het toestaan van lijsten heeft voltooid voordat u een bestemming maakt.

Voordat u de bestemming Google Ad Manager maakt in Adobe Real-time CDP, moet u contact opnemen met Google om Adobe op te nemen in de lijst met toegestane gegevensproviders en om uw account toe te voegen aan de lijst met toegestane gegevensproviders. Neem contact op met Google en geef de volgende informatie op:

* **Account-id** : Dit is de account-id van Adobe bij Google. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* **Klant-id** : Dit is de Adobe-id voor de klantenaccount bij Google. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* **Netwerk-id** : Dit is je account bij Google Ad Manager
* **Koppelings-id** publiek: Dit is je account bij Google Ad Manager
* Je accounttype. **DFP door Google** - of **AdX-koper**.

## Doel maken

1. Selecteer in **[!UICONTROL Verbindingen > Doelen]** de optie Google Ad Manager en selecteer **[!UICONTROL Doel]**maken.
   ![Doel van Google Ad Manager verbinden](/help/rtcdp/destinations/assets/google-1-destination.png)

2. In de stap van de **Opstelling** van creeer bestemmingswerkschema, vul de [!UICONTROL BasisInformatie] voor de bestemming in. <br>

   ![Basisinformatie Google Ad Manager](/help/rtcdp/destinations/assets/ad-manager-setup-step.png)
* **[!UICONTROL Naam]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Omschrijving]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Accounttype]**: Selecteer een optie, afhankelijk van uw account bij Google:
   * Gebruiken `DFP by Google` voor DoubleClick voor uitgevers
   * Gebruiken `AdX buyer` voor Google AdX
* **[!UICONTROL Account-id]**: Vul uw account-id in met Google. Dit kan uw identiteitskaart van het Netwerk of uw identiteitskaart van de Verbinding van het publiek zijn. Dit is doorgaans een id van acht cijfers.
* **[!UICONTROL Geval]** voor gebruik bij het in de handel brengen: Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde gevallen voor marketinggebruik of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Voor meer informatie over het op de markt brengen van gebruiksgevallen, zie de [Governance van Gegevens in Echte tijd CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) pagina. Zie het overzicht [van het beleid voor](/help/data-governance/policies/overview.md#core-actions)gegevensgebruik voor informatie over de afzonderlijke door Adobe gedefinieerde gevallen van marketinggebruik.

> [!NOTE]
>
> Wanneer u een Google Ad Manager-bestemming instelt, werkt u samen met uw Google-accountmanager of Adobe-vertegenwoordiger om te weten welk accounttype u hebt.

## Segmenten activeren op Google Ad Manager

Zie Gegevens naar bestemmingen [activeren voor instructies over het activeren van segmenten op Google Ad Manager](/help/rtcdp/destinations/activate-destinations.md).