---
title: Google AdsDestination
seo-title: Bestemming voor Google-advertenties
description: Google Ads, voorheen bekend als Google AdWords, is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten op tekstbasis, grafische beeldschermen, YouTube-video's en mobiele displays in de app.
seo-description: Google Ads, voorheen bekend als Google AdWords, is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten op tekstbasis, grafische beeldschermen, YouTube-video's en mobiele displays in de app.
translation-type: tm+mt
source-git-commit: 3e510c891c84fb3dc1632bd1182ef1e010ea898f

---


# Bestemming voor Google-advertenties

## Overzicht

Google Ads, voorheen bekend als Google AdWords, is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten op tekstbasis, grafische beeldschermen, YouTube-video&#39;s en mobiele displays in de app.

## Doelspecificaties

Let op de volgende details die specifiek zijn voor Google Ads-doelen:

* U kunt de volgende [identiteiten](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) naar de bestemmingen van Google Ads verzenden: Google-cookie-id, IDFA, GAID, Roku-id&#39;s, Microsoft-id&#39;s, Amazon Fire TV-id&#39;s ****.
* Geactiveerd publiek wordt via programmacode gemaakt in het Google-platform.
* Adobe Real-time CDP bevat momenteel geen metrische waarde om succesvolle activering te valideren. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en inzicht te krijgen in doelgroepen.

>[!IMPORTANT]
>
>Als u uw eerste bestemming met Google Ads wilt maken en in het verleden (met Audience Manager of andere toepassingen) de [id-synchronisatiefunctie](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service niet hebt ingeschakeld, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder Google-integratie hebt ingesteld in Audience Manager, worden de id-synchronisaties die u hebt ingesteld, overgedragen naar Adobe Real-time CDP.

## Vereisten

### Bestaande Google Ads-account

Google heeft alle nieuwe Google Ads-integraties met externe leveranciers gepauzeerd. U moet een bestaande integratie met Google Ads hebben om de whitelingstappen in de volgende sectie te kunnen uitvoeren en een Google Ads-bestemming in Adobe Real-time CDP te kunnen creëren.

### Whitelisting

>[!NOTE]
>
>Whitelisting is verplicht voordat u uw eerste Google Ads-bestemming in Adobe Real-time CDP instelt. Controleer of het hieronder beschreven whitelistingproces door Google is voltooid voordat u een bestemming maakt.

Voordat u de Google Ads-bestemming maakt in Adobe Real-time CDP, moet u contact opnemen met Google om Adobe te vragen om te worden gewhitelliseerd als gegevensaanbieder en om uw account te worden gewhitelisterd. Neem contact op met Google en geef de volgende informatie op:

* **Account-id** : Dit is de account-id van Adobe bij Google. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* **Klant-id** : Dit is de Adobe-id voor de klantenaccount bij Google. Neem contact op met de klantenservice van Adobe of uw Adobe-vertegenwoordiger voor deze id.
* Je accounttype: **AdWords**
* **Google AdWords-id** : Dit is uw id met Google. De id-indeling heeft doorgaans de notatie 123-456-7890.

## Doel maken

1. Selecteer Google Ads in **[!UICONTROL Verbindingen > Doelen]** en selecteer **[!UICONTROL Doel]**maken.
   ![Google Ads-doel verbinden](/help/rtcdp/destinations/assets/google-2-destination.png)

2. In de Create bestemmingstovenaar, vul de BasisInformatie voor de bestemming in.
   ![Basisinformatie over Google Ads](/help/rtcdp/destinations/assets/google-2-basic-information.png)
* **Naam**: Vul de voorkeursnaam voor dit doel in.
* **Omschrijving**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **Accounttype**: De enige beschikbare optie is AdvertentieWoorden.
* **Account-id**: Vul je account-id in met Google Ads. De id-indeling heeft doorgaans de notatie 123-456-7890.

## Segmenten activeren op Google Ads

Zie Gegevens naar bestemmingen [activeren voor instructies over het activeren van segmenten op Google Ads](/help/rtcdp/destinations/activate-destinations.md).

