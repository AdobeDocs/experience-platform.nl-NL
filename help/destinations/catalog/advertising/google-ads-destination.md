---
title: Google Ads-verbinding
description: Google Ads, voorheen bekend als Google AdWords, is een online advertentieservice waarmee bedrijven per klik reclame kunnen betalen voor zoekopdrachten, grafische weergaven, YouTube-video's en mobiele displays in de app.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# [!DNL Google Ads] verbinding

## Overzicht {#overview}

[!DNL Google Ads], voorheen bekend als [!DNL Google AdWords], een onlinereclame is die bedrijven in staat stelt om per klik reclame te betalen voor zoekopdrachten in tekstvorm en voor beeldschermen, [!DNL YouTube] video&#39;s en mobiele displays in de app.

## Doelspecificaties {#specifics}

Let op de volgende details die specifiek zijn voor [!DNL Google Ads] bestemmingen:

* Geactiveerd publiek wordt programmatically gecreeerd in [!DNL Google] platform.
* [!DNL Platform] bevat momenteel geen metrische waarde om een geslaagde activering te valideren. Raadpleeg het aantal gebruikers in Google om de integratie te valideren en te begrijpen waar de doelgroep zich op richt.

>[!IMPORTANT]
>
>Als u uw eerste bestemming wilt maken met [!DNL Google Ads] en hebben de [ID-synchronisatiefunctie](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in het verleden (met Audience Manager of andere toepassingen), bereik aan de Raadpleging van de Adobe of de Zorg van de Klant om de syncs van identiteitskaart toe te laten. Als u eerder Google-integratie in Audience Manager had ingesteld, worden de id-syncs die u hebt ingesteld, overgedragen naar Platform.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Google Ads] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Selecteer deze doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | [!DNL Apple ID for Advertisers] | Selecteer deze doelidentiteit wanneer uw bronidentiteit een IDFA-naamruimte is. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), ook bekend als [!DNL Device ID]. Een numerieke apparaat-id van 38 cijfers waarmee de Audience Manager werkt. | Google gebruikt [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) om gebruikers in Californië te richten, en identiteitskaart van de Koek van Google voor alle andere gebruikers. |
| [!DNL Google] cookie-id | [!DNL Google] cookie-id | [!DNL Google] gebruikt deze id om gebruikers buiten Californië als doel in te stellen. |
| RIDA | Roku ID for Advertising. Deze id identificeert unieke Roku-apparaten. |  |
| GEMAAKT | Microsoft-advertentie-id. Deze id identificeert apparaten waarop Windows 10 wordt uitgevoerd op unieke wijze. |  |
| Amazon Fire TV ID | Deze id is uniek voor Amazon Fire TV&#39;s. |  |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek naar de Google-bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

### Bestaande [!DNL Google Ads] account

>[!IMPORTANT]
>
> [!DNL Google] heeft nieuwe [!DNL Google Ads] cookie-integratie met externe leveranciers. Voor het uitvoeren van de stappen van de lijst van gewenste personen in de volgende sectie moet u bestaande integratie hebben met [!DNL Google Ads]. De aanbevolen aanpak voor het gebruik van [!DNL Google Ads] een [!DNL Google Customer Match] integratie. Voor meer informatie over het maken van een [!DNL Google Customer Match] integratie, lees de zelfstudie over het maken van een [[!DNL Google Customer Match]](./google-customer-match.md) verbinding.

### Aanbieding toestaan {#allow-listing}

>[!NOTE]
>
>Aanbieding toestaan is verplicht voordat je eerste aanbieding wordt ingesteld [!DNL Google Ads] doel in Platform. Zorg ervoor dat het hieronder beschreven proces voor het aanbieden van objecten in een aanbieding is voltooid door [!DNL Google] voordat u een doel maakt.
>De uitzondering op deze regel is [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) klanten. Als je al een verbinding met deze Google-bestemming in Audience Manager hebt gemaakt, is het niet nodig om het proces voor het toestaan van aanbiedingen opnieuw te doorlopen en je kunt doorgaan met de volgende stappen.

Voordat u het dialoogvenster [!DNL Google Ads] doel in Platform, u moet contact opnemen [!DNL Google] voor Adobe die op de lijst van toegestane gegevensleveranciers moet worden gezet, en voor uw rekening die aan de lijst van gewenste personen moet worden toegevoegd. Contact [!DNL Google] en verstrekt de volgende informatie:

* **Account-id**: De account-id van de Adobe met Google. Account-ID: 87933855.
* **Klant-id**: De klant-id van de Adobe met Google. Klant-id: 89690775.
* Je accounttype: **AdWords**
* **Google AdWords-id**: Dit is je id met [!DNL Google]. De id-indeling heeft doorgaans de notatie 123-456-7890.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Account Type]**: AdWords is de enige beschikbare optie.
* **[!UICONTROL Account ID]**: Vul uw account-id in met [!DNL Google Ads]. De id-indeling heeft doorgaans de notatie 123-456-7890.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](../../ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

## Geëxporteerde gegevens

Controleren of gegevens zijn geëxporteerd naar de [!DNL Google Ads] doel, controleer uw [!DNL Google Ads] account. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.

## Problemen oplossen {#troubleshooting}

### 400 Onjuist aanvraagfoutbericht {#bad-request}

Wanneer het vormen van deze bestemming, kunt u de volgende fout ontvangen:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Deze fout treedt op als de klantenaccounts niet voldoen aan de [voorwaarden](#prerequisites) of wanneer de klanten proberen de bestemming zonder het bestaan te vormen [!DNL Google Ads] account.

[!DNL Google] heeft nieuwe [!DNL Google Ads] cookie-integratie met externe leveranciers. Om het [lijst van gewenste personen](#allow-listing) stappen, u moet een bestaande integratie hebben met [!DNL Google Ads].

De aanbevolen aanpak voor het gebruik van [!DNL Google Ads] een [[!DNL Google Customer Match]](google-customer-match.md) integratie.
