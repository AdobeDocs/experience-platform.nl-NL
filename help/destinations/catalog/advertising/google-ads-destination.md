---
keywords: Google-advertenties;Google-advertenties;Google AdWords;Google Adwords
title: Google Ads-verbinding
description: Google Ads, voorheen bekend als Google AdWords, is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten op tekstbasis, grafische beeldschermen, YouTube-video's en mobiele displays in de app.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---


# [!DNL Google Ads] verbinding

[!DNL Google Ads], voorheen bekend als  [!DNL Google AdWords], is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten op tekstbasis, grafische weergaven,  [!DNL YouTube] video&#39;s en mobiele weergaven in de app.

## Doelspecificaties {#specifics}

Neem nota van de volgende details die voor [!DNL Google Ads] bestemmingen specifiek zijn:

* Geactiveerd publiek wordt gecreeerd programmatically in het [!DNL Google] platform.
* Platform bevat momenteel geen metrische waarde om succesvolle activering te valideren. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en inzicht te krijgen in doelgroepen.

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

## Vereisten

### Bestaande [!DNL Google Ads]-account

>[!IMPORTANT]
>
> [!DNL Google] heeft nieuwe  [!DNL Google Ads] cookieintegratie met derde verkopers vervangen. Voor het uitvoeren van de stappen van de lijst van gewenste personen in de volgende sectie, moet u bestaande integratie met [!DNL Google Ads] hebben. Het gevolg hiervan is dat de aanbevolen benadering voor het gebruik van [!DNL Google Ads] het instellen van een [!DNL Google Customer Match]-integratie is. Lees de zelfstudie over het maken van een [!DNL Google Customer Match]-verbinding voor meer informatie over het maken van een [[!DNL Google Customer Match]](./google-customer-match.md)-verbinding.

### Lijst van gewenste personen

>[!NOTE]
>
>De lijst van gewenste personen is verplicht alvorens uw eerste [!DNL Google Ads] bestemming in Platform te plaatsen. Controleer of het hieronder beschreven proces voor lijst van gewenste personen is voltooid door [!DNL Google] voordat u een doel maakt.

Voordat u de [!DNL Google Ads]-bestemming in Platform maakt, moet u contact opnemen met [!DNL Google] om Adobe op de lijst met toegestane gegevensproviders te plaatsen en om uw account aan de lijst van gewenste personen toe te voegen. Neem contact op met [!DNL Google] en geef de volgende informatie op:

* **Account-id** : Dit is Adobe account-ID met  [!DNL Google]. Neem contact op met de klantenservice van Adobe of uw Adobe om deze id te verkrijgen.
* **Klant-id** : Dit is Adobe-klant-id met  [!DNL Google]. Neem contact op met de klantenservice van Adobe of uw Adobe om deze id te verkrijgen.
* Je accounttype: **AdWords**
* **Google AdWords-id** : Dit is je ID met  [!DNL Google]. De id-indeling heeft doorgaans de notatie 123-456-7890.

## Doel configureren

Selecteer [!DNL Google Ads] in **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteer **[!UICONTROL Configure]**.

![Google Ads-doel verbinden](../../assets/catalog/advertising/google-ads-destination/catalog.png)

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL Activate]** knop op de doelkaart zien. Raadpleeg voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]** de sectie [Catalog](../../ui/destinations-workspace.md#catalog) van de documentatie van de doelwerkruimte.

In **Opstelling** stap van creeer bestemmingswerkschema, vul [!UICONTROL Basic Information] voor de bestemming in.

![Basisinformatie over Google Ads](../../assets/catalog/advertising/google-ads-destination/setup.png)

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Account Type]**: De enige beschikbare optie is AdvertentieWoorden.
* **[!UICONTROL Account ID]**: Vul je account-id in met  [!DNL Google Ads]. De id-indeling heeft doorgaans de notatie 123-456-7890.
* **[!UICONTROL Marketing action]**: Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Voor meer informatie over marketing acties, zie [Overzicht van het beleid van het gebruik van Gegevens](../../../data-governance/policies/overview.md).

## Segmenten activeren naar [!DNL Google Ads]

Zie [Gegevens naar doelen activeren](../../ui/activate-destinations.md) voor instructies over het activeren van segmenten naar [!DNL Google Ads].

## Geëxporteerde gegevens

Controleer uw [!DNL Google Ads]-account om te controleren of gegevens naar de [!DNL Google Ads]-bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.