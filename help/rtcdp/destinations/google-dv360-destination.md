---
title: Bestemming Google Display en Video 360
seo-title: Bestemming Google Display en Video 360
description: Display & Video 360, voorheen bekend als DoubleClick Bodmanager, is een hulpmiddel dat wordt gebruikt om heroriënterende en doelgerichte digitale campagnes uit te voeren over de inventarisbronnen voor weergave, video en mobiele apparaten.
seo-description: 'Display & Video 360, voorheen bekend als DoubleClick Bodmanager, is een hulpmiddel dat wordt gebruikt om heroriënterende en doelgerichte digitale campagnes uit te voeren over de inventarisbronnen voor weergave, video en mobiele apparaten. '
translation-type: tm+mt
source-git-commit: 810028edc662a7f52484e37cf0fbdfafe5db650f

---


# Bestemming Google Display en Video 360

## Overzicht

Display &amp; Video 360, voorheen bekend als DoubleClick Bid Manager, is een hulpmiddel dat wordt gebruikt voor het uitvoeren van herrichtings- en doelgerichte digitale campagnes in verschillende inventarisbronnen voor weergave, video en mobiele apparaten.

## Doelspecificaties

Let op de volgende details die specifiek zijn voor Google Display &amp; Video 360-doelen:

* U kunt de volgende [identiteiten](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) naar de bestemmingen van Google Display &amp; Video 360 verzenden: Google-cookie-id, IDFA, GAID, Roku-id&#39;s, Microsoft-id&#39;s, Amazon Fire TV-id&#39;s ****.
* Geactiveerd publiek wordt via programmacode gemaakt in het Google-platform.
* Adobe Real-time CDP bevat momenteel geen metrische waarde om succesvolle activering te valideren. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en inzicht te krijgen in doelgroepen.

>[!IMPORTANT]
>
>Als u uw eerste bestemming wilt maken met Google Display en Video 360 en in het verleden de functionaliteit [voor](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) id-synchronisatie niet hebt ingeschakeld in Experience Cloud ID Service (met Adobe Audience Manager of andere toepassingen), neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder Google-integratie hebt ingesteld in Audience Manager, worden de id-synchronisaties die u hebt ingesteld, overgedragen naar Adobe Real-time CDP.

## Vereisten

### Whitelisting

>[!NOTE]
>
>Whitelisting is verplicht voordat u de eerste Google Display &amp; Video 360-bestemming instelt in Adobe Real-time CDP. Controleer of het hieronder beschreven whitelistingproces door Google is voltooid voordat u een bestemming maakt.

Voordat u de bestemming Google Display &amp; Video 360 maakt in Adobe Real-time CDP, moet u contact opnemen met Google om te vragen dat Adobe wordt gewhitelliseerd als gegevensaanbieder en dat uw account wordt gewhitelist. Neem contact op met Google en geef de volgende informatie op:

* **Account-id** : Dit is de account-id van Adobe bij Google. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* **Klant-id** : Dit is de Adobe-id voor de klantenaccount bij Google. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* **Je accounttype**: gebruiken **[!DNL Invite advertiser]** om het publiek alleen te laten delen naar een specifiek merk in uw Display &amp; Video 360-account of gebruik **[!DNL Invite partner]** om het publiek te laten delen naar alle merken in uw Display &amp; Video 360-account.

## Doel maken

1. Selecteer in **[!UICONTROL Connections > Destinations]** Google Display &amp; Video 360 en selecteer **[!UICONTROL Create destination]**.
   ![Connect Google Display en Video 360-doel](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. In de Create bestemmingstovenaar, vul de BasisInformatie voor de bestemming in.
   ![Basisinformatie over Google Display en Video 360](/help/rtcdp/destinations/assets/google-dv360-basic-information.png)
* **Naam**: Vul de voorkeursnaam voor dit doel in.
* **Omschrijving**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **Accounttype**: Selecteer een optie, afhankelijk van uw account bij Google:
   * Gebruik deze optie `Invite Advertiser` om het publiek alleen naar een specifiek merk in uw Display &amp; Video 360-account te laten delen.
   * Gebruik deze optie `Invite Partner` om het publiek te laten delen naar alle merken in uw Display &amp; Video 360-account.
* **Account-id**: Vul uw **[!DNL Invite partner]** of **[!DNL Invite advertiser]** account-id in met Google. Dit is doorgaans een ID van zes of zeven cijfers.

>[!NOTE]
>
>Wanneer u een Google Display &amp; Video 360-bestemming instelt, werkt u samen met uw Google-accountmanager of Adobe-vertegenwoordiger om te begrijpen welk accounttype u hebt.

## Segmenten activeren op Google Display en Video 360

Zie Gegevens [naar doelen](/help/rtcdp/destinations/activate-destinations.md)activeren voor instructies over het activeren van segmenten op Google Display en Video 360.