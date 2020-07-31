---
title: Bestemming Google Display en Video 360
seo-title: Bestemming Google Display en Video 360
description: Display & Video 360, voorheen bekend als DoubleClick Bodmanager, is een hulpmiddel dat wordt gebruikt om heroriënterende en doelgerichte digitale campagnes uit te voeren over de inventarisbronnen voor weergave, video en mobiele apparaten.
seo-description: 'Display & Video 360, voorheen bekend als DoubleClick Bodmanager, is een hulpmiddel dat wordt gebruikt om heroriënterende en doelgerichte digitale campagnes uit te voeren over de inventarisbronnen voor weergave, video en mobiele apparaten. '
translation-type: tm+mt
source-git-commit: 7f3df12da5e93c3d0cc53eed1aa603ddbafdb0b2
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] Bestemming

## Overzicht

[!DNL Display & Video 360], voorheen bekend onder de naam [!DNL DoubleClick Bid Manager], is een hulpmiddel dat wordt gebruikt voor het uitvoeren van herrichtings- en doelgerichte digitale campagnes in verschillende bronnen voor weergave, video en mobiele inventaris.

## Doelspecificaties

Let op de volgende details die specifiek zijn voor [!DNL Google Display & Video 360] bestemmingen:

* U kunt de volgende [identiteiten](../../identity-service/namespaces.md) naar [!DNL Google Display & Video 360] bestemmingen verzenden: **Google-cookie-id, IDFA, GAID, Roku-id&#39;s, Microsoft-id&#39;s, Amazon Fire TV-id&#39;s**.
* Geactiveerd publiek wordt via programmacode gemaakt in het Google-platform.
* Adobe In real time CDP omvat momenteel geen metrisch om succesvolle activering te bevestigen. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en inzicht te krijgen in doelgroepen.

>[!IMPORTANT]
>
>Als u uw eerste bestemming wilt maken met Google Display &amp; Video 360 en in het verleden (met Adobe Audience Manager of andere toepassingen) de functionaliteit [voor het synchroniseren van](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) id&#39;s niet hebt ingeschakeld in de Experience Cloud ID-service, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder Google-integraties in Audience Manager had ingesteld, worden de id-syncs die u hebt ingesteld, overgedragen naar Adobe Real-Time CDP.

## Vereisten

### Lijst van gewenste personen

>[!NOTE]
>
>De lijst van gewenste personen is verplicht alvorens uw eerste [!DNL Google Display & Video 360] bestemming in Adobe in real time CDP te vestigen. Controleer of Google het hieronder beschreven lijst van gewenste personen-proces heeft voltooid voordat u een bestemming maakt.

Voordat u de [!DNL Google Display & Video 360] bestemming maakt in CDP in real-time Adobe, moet u contact opnemen met Google om Adobe op de lijst met toegestane gegevensproviders te plaatsen en om uw account aan de lijst van gewenste personen toe te voegen. Neem contact op met Google en geef de volgende informatie op:

* **Account-id** : Dit is Adobe account-ID bij Google. Neem contact op met de klantenservice van Adobe of uw Adobe om deze id te verkrijgen.
* **Klant-id** : Dit is Adobe-klant-id bij Google. Neem contact op met de klantenservice van Adobe of uw Adobe om deze id te verkrijgen.
* **Je accounttype**: gebruiken **[!DNL Invite advertiser]** om het publiek alleen te laten delen naar een specifiek merk in uw Display &amp; Video 360-account of gebruik **[!DNL Invite partner]** om het publiek te laten delen naar alle merken in uw Display &amp; Video 360-account.

## Doel maken

1. Selecteer in **[!UICONTROL Verbindingen > Doelen]** de optie [!DNL Google Display & Video 360]en selecteer **[!UICONTROL Doel]**maken.
   ![Connect Google Display en Video 360-doel](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. In de stap van de **Opstelling** van creeer bestemmingswerkschema, vul de [!UICONTROL BasisInformatie] voor de bestemming, evenals de marketing gebruiksgevallen in die op deze bestemming zouden moeten van toepassing zijn. <br>

   ![Basisinformatie over Google Display en Video 360](/help/rtcdp/destinations/assets/dv360-setup-step.png)
* **[!UICONTROL Naam]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Omschrijving]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Accounttype]**: Selecteer een optie, afhankelijk van uw account bij Google:
   * Gebruik deze optie `Invite Advertiser` om het publiek alleen naar een specifiek merk in uw Display &amp; Video 360-account te laten delen.
   * Gebruik deze optie `Invite Partner` om het publiek te laten delen naar alle merken in uw Display &amp; Video 360-account.
* **[!UICONTROL Account-id]**: Vul uw **[!DNL Invite partner]** of **[!DNL Invite advertiser]** account-id in met Google. Dit is doorgaans een ID van zes of zeven cijfers.
* **[!UICONTROL Geval]** voor gebruik bij het in de handel brengen: Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door de Adobe gedefinieerde gebruiksgevallen voor marketingdoeleinden of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Voor meer informatie over het op de markt brengen van gebruiksgevallen, zie de [Governance van Gegevens in Echte tijd CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) pagina. Voor informatie over de individuele Adobe-bepaalde het in de handel brengen gebruiksgevallen, zie het overzicht [van het het gebruiksbeleid van](/help/data-governance/policies/overview.md#core-actions)Gegevens.

>[!NOTE]
>
>Wanneer u een [!DNL Google Display & Video 360] bestemming instelt, werkt u samen met uw vertegenwoordiger [!DNL Google Account Manager] of Adobe om te begrijpen welk accounttype u hebt.

## Segmenten activeren om [!DNL Google Display & Video 360]

Voor instructies op hoe te om segmenten te activeren, zie [!DNL Google Display & Video 360]Gegevens aan Doelen [](/help/rtcdp/destinations/activate-destinations.md)activeren.

## Geëxporteerde gegevens

Controleer uw [!DNL Google Display & Video 360] account om te controleren of gegevens naar de [!DNL Google Display & Video 360] bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.