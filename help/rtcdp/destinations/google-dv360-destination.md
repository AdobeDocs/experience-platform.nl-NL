---
title: Bestemming Google Display en Video 360
seo-title: Bestemming Google Display en Video 360
description: Display & Video 360, voorheen bekend als DoubleClick Bodmanager, is een hulpmiddel dat wordt gebruikt om heroriënterende en doelgerichte digitale campagnes uit te voeren over de inventarisbronnen voor weergave, video en mobiele apparaten.
seo-description: 'Display & Video 360, voorheen bekend als DoubleClick Bodmanager, is een hulpmiddel dat wordt gebruikt om heroriënterende en doelgerichte digitale campagnes uit te voeren over de inventarisbronnen voor weergave, video en mobiele apparaten. '
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---


# Bestemming Google Display en Video 360

## Overzicht

Display &amp; Video 360, voorheen bekend als DoubleClick Bid Manager, is een hulpmiddel dat wordt gebruikt voor het uitvoeren van herrichtings- en doelgerichte digitale campagnes in verschillende inventarisbronnen voor weergave, video en mobiele apparaten.

## Doelspecificaties

Let op de volgende details die specifiek zijn voor Google Display &amp; Video 360-doelen:

* U kunt de volgende [identiteiten](../../identity-service/namespaces.md) naar de bestemmingen van Google Display &amp; Video 360 verzenden: **Google-cookie-id, IDFA, GAID, Roku-id&#39;s, Microsoft-id&#39;s, Amazon Fire TV-id&#39;s**.
* Geactiveerd publiek wordt via programmacode gemaakt in het Google-platform.
* Adobe Real-time CDP bevat momenteel geen metrische waarde om succesvolle activering te valideren. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en inzicht te krijgen in doelgroepen.

>[!IMPORTANT]
>
>Als u uw eerste bestemming wilt maken met Google Display &amp; Video 360 en in het verleden (met Adobe Audience Manager of andere toepassingen) de functionaliteit [voor het synchroniseren van](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) id&#39;s niet hebt ingeschakeld in de Experience Cloud ID Service, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder Google-integraties in Audience Manager had ingesteld, worden de synchronisaties van de id die u had ingesteld overgedragen naar Adobe Real-time CDP.

## Vereisten

### Lijst toestaan

>[!NOTE]
>
>De lijst Toestaan is verplicht voordat u de eerste Google Display &amp; Video 360-bestemming instelt in Adobe Real-time CDP. Controleer of Google het hieronder beschreven proces voor het toestaan van lijsten heeft voltooid voordat u een bestemming maakt.

Voordat u de Google Display &amp; Video 360-bestemming maakt in Adobe Real-time CDP, moet u contact opnemen met Google om Adobe te vragen op de lijst met toegestane gegevensproviders te plaatsen en uw account toe te voegen aan de lijst met toegestane gegevens. Neem contact op met Google en geef de volgende informatie op:

* **Account-id** : Dit is de account-id van Adobe bij Google. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* **Klant-id** : Dit is de Adobe-id voor de klantenaccount bij Google. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* **Je accounttype**: gebruiken **[!DNL Invite advertiser]** om het publiek alleen te laten delen naar een specifiek merk in uw Display &amp; Video 360-account of gebruik **[!DNL Invite partner]** om het publiek te laten delen naar alle merken in uw Display &amp; Video 360-account.

## Doel maken

1. Selecteer Google Display &amp; Video 360 in **[!UICONTROL Verbindingen > Doelen]** en selecteer **[!UICONTROL Doel]**maken.
   ![Connect Google Display en Video 360-doel](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. In de stap van de **Opstelling** van creeer bestemmingswerkschema, vul de [!UICONTROL BasisInformatie] voor de bestemming, evenals de marketing gebruiksgevallen in die op deze bestemming zouden moeten van toepassing zijn. <br>
   ![Basisinformatie over Google Display en Video 360](/help/rtcdp/destinations/assets/dv360-setup-step.png)
* **[!UICONTROL Naam]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Omschrijving]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Accounttype]**: Selecteer een optie, afhankelijk van uw account bij Google:
   * Gebruik deze optie `Invite Advertiser` om het publiek alleen naar een specifiek merk in uw Display &amp; Video 360-account te laten delen.
   * Gebruik deze optie `Invite Partner` om het publiek te laten delen naar alle merken in uw Display &amp; Video 360-account.
* **[!UICONTROL Account-id]**: Vul uw **[!DNL Invite partner]** of **[!DNL Invite advertiser]** account-id in met Google. Dit is doorgaans een ID van zes of zeven cijfers.
* **[!UICONTROL Geval]** voor gebruik bij het in de handel brengen: Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde gevallen voor marketinggebruik of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Voor meer informatie over het op de markt brengen van gebruiksgevallen, zie de [Governance van Gegevens in Echte tijd CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) pagina. Zie het overzicht [van het beleid voor](/help/data-governance/policies/overview.md#core-actions)gegevensgebruik voor informatie over de afzonderlijke door Adobe gedefinieerde gevallen van marketinggebruik.

>[!NOTE]
>
>Wanneer u een Google Display &amp; Video 360-bestemming instelt, werkt u samen met uw Google-accountmanager of Adobe-vertegenwoordiger om te begrijpen welk accounttype u hebt.

## Segmenten activeren op Google Display en Video 360

Zie Gegevens [naar doelen](/help/rtcdp/destinations/activate-destinations.md)activeren voor instructies over het activeren van segmenten op Google Display en Video 360.