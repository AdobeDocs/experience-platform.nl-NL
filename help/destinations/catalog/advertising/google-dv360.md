---
title: Google Display & Video 360-verbinding
description: Display & Video 360, voorheen bekend als DoubleClick Bodmanager, is een hulpmiddel dat wordt gebruikt om herrichtings- en doelgerichte digitale campagnes uit te voeren in verschillende bronnen voor weergave, video en mobiele inventaris.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---

# [!DNL Google Display & Video 360] verbinding

## Overzicht {#overview}

[!DNL Display & Video 360], voorheen bekend als [!DNL DoubleClick Bid Manager], is een hulpprogramma waarmee u doelgerichte digitale campagnes voor weergave, video en mobiele inventarisbronnen kunt uitvoeren.

## Doelspecificaties {#specifics}

Let op de volgende details die specifiek zijn voor [!DNL Google Display & Video 360] bestemmingen:

* Geactiveerd publiek wordt programmatically gecreeerd in het platform van Google.
* De activering van publieksback-ups voor de [!DNL Google Display & Video 360] De bestemming zal 24-48 uur voorkomen nadat een publiek voor het eerst aan een bestemmingsverbinding in kaart wordt gebracht. Deze update is een reactie op het beleid van Google om 24 uur te wachten tot er gegevens zijn ingevoerd en is bedoeld om de overeenkomst tussen Real-Time CDP en [!DNL Google Display & Video 360]. Dit is een achtergrondconfiguratie die op deze bestemming slechts van toepassing is en die niet met om het even welke klant-configureerbare het plannen opties in UI verwant is.

>[!IMPORTANT]
>
>Als u uw eerste bestemming wilt maken met Google Display &amp; Video 360 en de optie [ID-synchronisatiefunctie](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in het verleden (met Adobe Audience Manager of andere toepassingen), dient u contact op te nemen met de Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u eerder Google-integratie in Audience Manager had ingesteld, worden de id-syncs die u hebt ingesteld, overgedragen naar Platform.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Google Display & Video 360] ondersteunt de activering van het publiek op basis van de in de onderstaande tabel weergegeven identiteiten. Meer informatie over [identiteiten](/help/identity-service/features/namespaces.md).

| Identiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), ook bekend als [!DNL Device ID]. Een numerieke apparaat-id van 38 cijfers waarmee de Audience Manager werkt. | Google gebruikt [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) om gebruikers in Californië te richten, en identiteitskaart van de Koek van Google voor alle andere gebruikers. |
| [!DNL Google] cookie-id | [!DNL Google] cookie-id | [!DNL Google] gebruikt deze id om gebruikers buiten Californië als doel in te stellen. |
| RIDA | Roku ID for Advertising. Deze id identificeert unieke Roku-apparaten. |  |
| GEMAAKT | Microsoft-advertentie-id. Deze id identificeert apparaten waarop Windows 10 wordt uitgevoerd op unieke wijze. |  |
| Amazon Fire TV ID | Deze id is uniek voor Amazon Fire TV&#39;s. |  |

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

## Vereisten {#prerequisites}

### Aanbieding toestaan {#allow-listing}

>[!NOTE]
>
>Aanbieding toestaan is verplicht voordat je eerste aanbieding wordt ingesteld [!DNL Google Display & Video 360] doel in Platform. Controleer of het hieronder beschreven proces voor het aanbieden van een aanbieding is voltooid door [!DNL Google] voordat u een doel maakt.
>De uitzondering op deze regel is [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) klanten. Als je al een verbinding met deze Google-bestemming in Audience Manager hebt gemaakt, is het niet nodig om het proces voor het toestaan van aanbiedingen opnieuw te doorlopen en je kunt doorgaan met de volgende stappen.

Voordat u het dialoogvenster [!DNL Google Display & Video 360] Als u een account wilt maken in Platform, moet u contact opnemen met Google en vragen of Adobe moet worden opgenomen in de lijst met toegestane gegevensproviders en dat uw account moet worden toegevoegd aan de lijst van gewenste personen. Neem contact op met Google en geef de volgende informatie op:

* **Account-id**: De account-id van de Adobe met Google. Account-ID: 87933855.
* **Klant-id**: De klant-id van de Adobe met Google. Klant-id: 89690775.
* **Je accounttype**: use **[!DNL Invite advertiser]** om het publiek alleen te laten delen naar een specifiek merk in uw Display &amp; Video 360-account of -gebruik **[!DNL Invite partner]** om het publiek te laten delen naar alle merken in uw Display &amp; Video 360-account.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Account Type]**: Selecteer een optie, afhankelijk van uw account bij Google:
   * Gebruiken `Invite Advertiser` om het publiek alleen te laten delen naar een specifiek merk in uw Display &amp; Video 360-account.
   * Gebruiken `Invite Partner` om het publiek te laten delen naar alle merken in uw Display &amp; Video 360-account.
* **[!UICONTROL Account ID]**: Vul uw **[!DNL Invite partner]** of **[!DNL Invite advertiser]** account-id met Google. Dit is doorgaans een ID van zes of zeven cijfers.

>[!NOTE]
>
>Wanneer u een [!DNL Google Display & Video 360] doel, werken met uw [!DNL Google Account Manager] of een Adobe die representatief is voor het accounttype dat u hebt.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](../../ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

## Geëxporteerde gegevens

Controleren of gegevens zijn geëxporteerd naar de [!DNL Google Display & Video 360] doel, controleer uw [!DNL Google Display & Video 360] account. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.

## Problemen oplossen {#troubleshooting}

### 400 Onjuist aanvraagfoutbericht {#bad-request}

Wanneer het vormen van deze bestemming, kunt u de volgende fout ontvangen:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Deze fout treedt op wanneer de klantenrekeningen niet aan [voorwaarden](#prerequisites). Neem contact op met Google om dit probleem op te lossen en zorg ervoor dat je account op de lijst staat.