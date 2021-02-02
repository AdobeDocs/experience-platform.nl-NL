---
keywords: Google-advertenties;Google-advertenties;Google AdWords;Google Adwords
title: Google AdsDestination
seo-title: Bestemming voor Google-advertenties
description: Google Ads, voorheen bekend als Google AdWords, is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten op tekstbasis, grafische beeldschermen, YouTube-video's en mobiele displays in de app.
seo-description: Google Ads, voorheen bekend als Google AdWords, is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten op tekstbasis, grafische beeldschermen, YouTube-video's en mobiele displays in de app.
translation-type: tm+mt
source-git-commit: bb2fc2658d32c59b476dd9d526eb8bc2f055a1af
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---


# [!DNL Google Ads] Bestemming

## Overzicht

[!DNL Google Ads], voorheen bekend als  [!DNL Google AdWords], is een onlinereclame die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten op tekstbasis, grafische weergaven,  [!DNL YouTube] video&#39;s en mobiele weergaven in de app.

## Doelspecificaties

Neem nota van de volgende details die voor [!DNL Google Ads] bestemmingen specifiek zijn:

* U kunt de volgende [identiteiten](../../../identity-service/namespaces.md) naar [!DNL Google Ads] bestemmingen verzenden: [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en), Google cookie-id, IDFA, GAID, Roku-id&#39;s, Microsoft-id&#39;s en Amazon Fire TV-id&#39;s.
   * Google gebruikt [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) om gebruikers in Californië als doelgroep op te nemen, en de Google Cookie-id voor alle andere gebruikers.
* Geactiveerd publiek wordt gecreeerd programmatically in het [!DNL Google] platform.
* Platform bevat momenteel geen metrische waarde om succesvolle activering te valideren. Raadpleeg de tellingen van het publiek in Google om de integratie te valideren en inzicht te krijgen in doelgroepen.

>[!IMPORTANT]
>
>Als u uw eerste bestemming met [!DNL Google Ads] wilt maken en de [ID-synchronisatiefunctionaliteit](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in het verleden (met Audience Manager of andere toepassingen) niet hebt ingeschakeld, neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder Google-integraties in Audience Manager had ingesteld, worden de id-synchronisaties die u hebt ingesteld overgedragen naar Platform.

### Exporttype {#export-type}

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
* Je accounttype: **Advertentiewoorden**
* **Google AdWords-id** : Dit is je ID met  [!DNL Google]. De id-indeling heeft doorgaans de notatie 123-456-7890.

## Doel configureren

Selecteer **[!UICONTROL Verbindingen]** > **[!UICONTROL Doelen]** en selecteer [!DNL Google Ads] en **[!UICONTROL Configureren]**.

![Google Ads-doel verbinden](../../assets/catalog/advertising/google-ads-destination/catalog.png)

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL knop Activeer]** op de doelkaart zien. Voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]**, verwijs naar [Catalog](../../ui/destinations-workspace.md#catalog) sectie van de documentatie van de bestemmingswerkruimte.

In **Opstelling** stap van creeer bestemmingswerkschema, vul [!UICONTROL BasisInformatie] voor de bestemming in.

![Basisinformatie over Google Ads](../../assets/catalog/advertising/google-ads-destination/setup.png)

* **[!UICONTROL Naam]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Omschrijving]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Accounttype]**: De enige beschikbare optie is AdvertentieWoorden.
* **[!UICONTROL Account-id]**: Vul je account-id in met  [!DNL Google Ads]. De id-indeling heeft doorgaans de notatie 123-456-7890.
* **[!UICONTROL Geval]** voor gebruik bij het in de handel brengen: Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door de Adobe gedefinieerde gebruiksgevallen voor marketingdoeleinden of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Zie [Overzicht van beleidsregels voor gegevensgebruik](../../../data-governance/policies/overview.md) voor meer informatie over gevallen van marketinggebruik.

## Segmenten activeren naar [!DNL Google Ads]

Zie [Gegevens naar doelen activeren](../../ui/activate-destinations.md) voor instructies over het activeren van segmenten naar [!DNL Google Ads].

## Geëxporteerde gegevens

Controleer uw [!DNL Google Ads]-account om te controleren of gegevens naar de [!DNL Google Ads]-bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.