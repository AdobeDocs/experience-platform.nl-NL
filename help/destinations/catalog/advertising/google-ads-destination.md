---
keywords: Google-advertenties;Google-advertenties;Google AdWords;Google Adwords
title: Google Ads-verbinding
description: Google Ads, voorheen bekend als Google AdWords, is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten, grafische beeldschermen, YouTube-video's en mobiele displays in de app.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: f04ea9aed586c8582286de82bfeee3f6f04cc360
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 1%

---

# [!DNL Google Ads] verbinding

## Overzicht {#overview}

[!DNL Google Ads], voorheen bekend als  [!DNL Google AdWords], is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten op tekstbasis, grafische weergaven,  [!DNL YouTube] video&#39;s en mobiele weergaven in de app.

## Doelspecificaties {#specifics}

Neem nota van de volgende details die voor [!DNL Google Ads] bestemmingen specifiek zijn:

* Geactiveerd publiek wordt gecreeerd programmatically in het [!DNL Google] platform.
* [!DNL Platform] bevat momenteel geen metrische waarde om een geslaagde activering te valideren. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en inzicht te krijgen in doelgroepen.

>[!IMPORTANT]
>
>Als u uw eerste bestemming met [!DNL Google Ads] wilt maken en de [ID-synchronisatiefunctionaliteit](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in het verleden (met Audience Manager of andere toepassingen) niet hebt ingeschakeld, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder Google-integraties in Audience Manager had ingesteld, worden de id-synchronisaties die u hebt ingesteld overgedragen naar Platform.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Google Ad Manager] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Selecteer deze doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | [!DNL Apple ID for Advertisers] | Selecteer deze doelidentiteit wanneer uw bronidentiteit een IDFA-naamruimte is. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), ook bekend als  [!DNL Device ID]. Een numerieke apparaat-id van 38 cijfers waarmee de Audience Manager werkt. | Google gebruikt [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) om gebruikers in Californië aan te wijzen, en Google Cookie ID voor alle andere gebruikers. |
| [!DNL Google] cookie-id | [!DNL Google] cookie-id | [!DNL Google] gebruikt deze id om gebruikers buiten Californië als doel in te stellen. |
| RIDA | Roku ID for Advertising. Deze id identificeert unieke Roku-apparaten. |  |
| GEMAAKT | Microsoft Advertising ID. Deze id identificeert apparaten waarop Windows 10 wordt uitgevoerd op unieke wijze. |  |
| Amazon Fire TV ID | Deze id is uniek voor Amazon Fire TV&#39;s. |  |

## Exporttype {#export-type}

**Segmentexport** : u exporteert alle leden van een segment (publiek) naar de Google-bestemming.

## Vereisten {#prerequisites}

### Bestaande [!DNL Google Ads]-account

>[!IMPORTANT]
>
> [!DNL Google] heeft nieuwe  [!DNL Google Ads] cookieintegratie met derde verkopers vervangen. Voor het uitvoeren van de stappen van de lijst van gewenste personen in de volgende sectie, moet u bestaande integratie met [!DNL Google Ads] hebben. Het gevolg hiervan is dat de aanbevolen benadering voor het gebruik van [!DNL Google Ads] het instellen van een [!DNL Google Customer Match]-integratie is. Lees de zelfstudie over het maken van een [!DNL Google Customer Match]-verbinding voor meer informatie over het maken van een [[!DNL Google Customer Match]](./google-customer-match.md)-verbinding.

### Aanbieding toestaan {#allow-listing}

>[!NOTE]
>
>De lijst van gewenste personen is verplicht alvorens uw eerste [!DNL Google Ads] bestemming in Platform te plaatsen. Controleer of het hieronder beschreven proces voor lijst van gewenste personen is voltooid door [!DNL Google] voordat u een doel maakt.

Voordat u de [!DNL Google Ads]-bestemming in Platform maakt, moet u contact opnemen met [!DNL Google] om Adobe op de lijst met toegestane gegevensproviders te plaatsen en om uw account aan de lijst van gewenste personen toe te voegen. Neem contact op met [!DNL Google] en geef de volgende informatie op:

* **Account-id**: Adobe-account-id met Google. Account-id: 87933855.
* **Klant-id**: Adobe&#39;s klant account-id met Google. Klant-id: 89690775.
* Je accounttype: **AdWords**
* **Google AdWords-id**: Dit is je ID met  [!DNL Google]. De id-indeling heeft doorgaans de notatie 123-456-7890.

## Verbinden met de bestemming {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [vestiging](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Account Type]**: De enige beschikbare optie is AdvertentieWoorden.
* **[!UICONTROL Account ID]**: Vul je account-id in met  [!DNL Google Ads]. De id-indeling heeft doorgaans de notatie 123-456-7890.

## Segmenten naar dit doel activeren {#activate}

Zie [De publieksgegevens van Activate aan het stromen segment de uitvoerbestemmingen ](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiekssegmenten aan deze bestemming.

## Geëxporteerde gegevens

Controleer uw [!DNL Google Ads]-account om te controleren of gegevens naar de [!DNL Google Ads]-bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.

## Problemen oplossen {#troubleshooting}

### 400 Onjuist aanvraagfoutbericht {#bad-request}

Wanneer het vormen van deze bestemming, kunt u de volgende fout ontvangen:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Deze fout treedt op wanneer de klantenaccounts niet voldoen aan de [voorwaarden](#prerequisites) of wanneer klanten de bestemming proberen te configureren zonder een bestaande [!DNL Google Ads]-account.

[!DNL Google] heeft nieuwe  [!DNL Google Ads] cookieintegratie met derde verkopers vervangen. Als u de stappen [allow-list](#allow-listing) wilt uitvoeren, moet u een bestaande integratie met [!DNL Google Ads] hebben.

De geadviseerde benadering voor het gebruiken van [!DNL Google Ads] is vestiging een [[!DNL Google Customer Match]](google-customer-match.md) integratie.
