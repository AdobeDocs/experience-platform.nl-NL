---
title: Doel van Google Ad Manager
seo-title: Doel van Google Ad Manager
description: 'Google Ad Manager, voorheen bekend als DoubleClick voor uitgevers of DoubleClick AdX, is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren. '
seo-description: 'Google Ad Manager, voorheen bekend als DoubleClick voor uitgevers of DoubleClick AdX, is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren. '
translation-type: tm+mt
source-git-commit: 3e510c891c84fb3dc1632bd1182ef1e010ea898f

---


# Doel van Google Ad Manager

## Overzicht

Google Ad Manager, voorheen bekend als DoubleClick voor uitgevers of DoubleClick AdX, is een advertentieplatform van Google dat uitgevers de middelen geeft om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren.

## Doelspecificaties

Let op de volgende details die specifiek zijn voor de doelen van Google Ad Manager:

* U kunt de volgende [identiteiten](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) naar de bestemmingen van Google Ad Manager verzenden: Google-cookie-id, IDFA, GAID, Roku-id&#39;s, Microsoft-id&#39;s, Amazon Fire TV-id&#39;s ****.
* Geactiveerd publiek wordt via programmacode gemaakt in het Google-platform.
* Adobe Real-time CDP bevat momenteel geen metrische waarde om succesvolle activering te valideren. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en inzicht te krijgen in doelgroepen.

>[!IMPORTANT]
>
>Als u uw eerste bestemming wilt maken met Google Ad Manager en in het verleden (met Audience Manager of andere toepassingen) de functionaliteit [voor het synchroniseren van](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) id&#39;s niet hebt ingeschakeld in Experience Cloud ID Service, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder Google-integratie hebt ingesteld in Audience Manager, worden de id-synchronisaties die u hebt ingesteld, overgedragen naar Adobe Real-time CDP.

## Vereisten

### Whitelisting

>[!NOTE]
>
>Whitelisting is verplicht voordat u de eerste bestemming van Google Ad Manager in Adobe Real-time CDP instelt. Controleer of het hieronder beschreven whitelistingproces door Google is voltooid voordat u een bestemming maakt.

Voordat u de bestemming Google Ad Manager maakt in Adobe Real-time CDP, moet u contact opnemen met Google om te vragen dat Adobe wordt gewhitelisterd als gegevensaanbieder en dat uw account wordt gewhitelliseerd. Neem contact op met Google en geef de volgende informatie op:

* **Account-id** : Dit is de account-id van Adobe bij Google. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* **Klant-id** : Dit is de Adobe-id voor de klantenaccount bij Google. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* **Netwerk-id** : Dit is je account bij Google Ad Manager
* **Koppelings-id** publiek: Dit is je account bij Google Ad Manager
* Je accounttype. **DFP door Google** - of **AdX-koper**.

## Doel maken

1. Selecteer in **[!UICONTROL Connections > Destinations]** Google Ad Manager en selecteer **[!UICONTROL Create destination]**.
   ![Doel van Google Ad Manager verbinden](/help/rtcdp/destinations/assets/google-1-destination.png)

2. In de Create bestemmingstovenaar, vul de BasisInformatie voor de bestemming in.
   ![Basisinformatie Google Ad Manager](/help/rtcdp/destinations/assets/google-1-basic-information.png)
* **Naam**: Vul de voorkeursnaam voor dit doel in.
* **Omschrijving**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **Accounttype**: Selecteer een optie, afhankelijk van uw account bij Google:
   * Gebruiken `DFP by Google` voor DoubleClick voor uitgevers
   * Gebruiken `AdX buyer` voor Google AdX
* **Account-id**: Vul uw account-id in met Google. Dit kan uw identiteitskaart van het Netwerk of uw identiteitskaart van de Verbinding van het publiek zijn. Dit is doorgaans een id van acht cijfers.

>[!NOTE]
>
>Wanneer u een Google Ad Manager-bestemming instelt, werkt u samen met uw Google-accountmanager of Adobe-vertegenwoordiger om te weten welk accounttype u hebt.

## Segmenten activeren op Google Ad Manager

Zie Gegevens naar bestemmingen [activeren voor instructies over het activeren van segmenten op Google Ad Manager](/help/rtcdp/destinations/activate-destinations.md).