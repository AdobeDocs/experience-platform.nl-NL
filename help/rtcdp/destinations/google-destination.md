---
title: Google-bestemming
seo-title: Google-bestemming
description: Adobe Real-time CDP kan worden geïntegreerd met Google, zodat u uw gegevens kunt uitvoeren en activeren in DV360, Google Ad Manager, Google AdWords en Google AdX.
seo-description: Adobe Real-time CDP kan worden geïntegreerd met Google, zodat u uw gegevens kunt uitvoeren en activeren in DV360, Google Ad Manager, Google AdWords en Google AdX.
translation-type: tm+mt
source-git-commit: 5396bee00044e5046bd768a863fceca0aec1d24e

---


# Google-bestemming

## Overzicht

Adobe Real-time CDP kan worden geïntegreerd met Google, zodat u uw gegevens kunt uitvoeren en activeren in DV360, Google Ad Manager, Google AdWords Display en Google AdX.

## Doelspecificaties

Let op de volgende details die specifiek zijn voor Google-doelen:

* U kunt de volgende [identiteiten](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) naar Google-bestemmingen verzenden: **Google cookie ID, IDFA, GAID**.
* Geactiveerd publiek wordt via programmacode gemaakt in het Google-platform.
* Adobe Real-time CDP bevat momenteel geen metrische waarde om succesvolle activering te valideren. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en de gegevensdrop-off te begrijpen.

## Vereisten

### Whitelisting

Voordat u verbinding maakt met de Google-bestemming in Adobe Real-time CDP, moet u contact opnemen met Google om te vragen dat uw account wordt gewhitelist. Neem contact op met Google en geef de volgende informatie op:

* **Account-id** : Dit is de account-id van Adobe bij Google. Neem contact op met de Technische Ondersteuning van Adobe voor deze id.
* **Klant-id** : Dit is de Adobe-id voor de klantenaccount bij Google. Neem contact op met de Technische Ondersteuning van Adobe voor deze id.
* **Partner-id** : Dit is uw driecijferige partner-id met Google.
* **Netwerk-id** : dit is uw account bij Google;
* **Koppelings-id** publiek: dit is uw account bij Google;
* Je accounttype. Dit kan adverteerder **van de** Uitnodiging, partner **van de** Uitnodiging, **DFP**, **AdWords**, **AdX** zijn.


## Connect-doel

1. Selecteer Google in **[!UICONTROL Verbindingen > Doelen]** en selecteer **[!UICONTROL Doel]**maken.
   ![Google-doel verbinden](/help/rtcdp/destinations/assets/google-destination.png)

2. Vul in de wizard Connect-bestemming de basisgegevens voor het doel in.
   ![Basisinformatie Google](/help/rtcdp/destinations/assets/google-basic-information.png)
* **Naam**: Vul de voorkeursnaam voor dit doel in.
* **Omschrijving**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **Accounttype**: Selecteer een optie, afhankelijk van uw account bij Google:
   * Gebruiken `Invite advertiser` voor Google DV360
   * Gebruiken `Invite partner` voor Google DV360
   * Gebruiken `DFP by Google` voor Google Ad Manager
   * Gebruiken `AdWords` voor weergave van Google AdWords
   * Gebruiken `AdX buyer` voor Google AdX
* **Account-id**: Vul uw account-id in met Google.

>[!NOTE]
>
>Wanneer u een Google-bestemming instelt, werkt u samen met uw Google-accountmanager of Adobe-vertegenwoordiger om te weten onder welk producttype uw account valt. Voor Google DV360 vraagt u uw Google-accountmanager welk producttype uw account onder valt. 

## Segmenten activeren op Google

Zie Gegevens naar bestemmingen [activeren voor instructies over het activeren van segmenten op Google](/help/rtcdp/destinations/activate-destinations.md).