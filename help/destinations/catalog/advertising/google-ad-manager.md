---
keywords: google en manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google en manager; DFP
title: Google Ad Manager-verbinding
description: Google Ad Manager, voorheen bekend als DoubleClick voor Publishers of DoubleClick AdX, is een advertentieplatform uit Google dat uitgevers de mogelijkheid biedt om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 1c9725c108d55aea5d46b086fbe010ab4ba6cf45
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 1%

---

# [!DNL Google Ad Manager] verbinding

## Overzicht {#overview}

[!DNL Google Ad Manager], voorheen bekend als [!DNL DoubleClick for Publishers] (DFP) of [!DNL DoubleClick AdX], is een platform voor advertenties van [!DNL Google] uitgevers krijgen de middelen om de weergave van advertenties op hun websites , via video en in mobiele apps te beheren .

## Doelspecificaties {#specifics}

Let op de volgende details die specifiek zijn voor [!DNL Google Ad Manager] bestemmingen:

* Geactiveerd publiek wordt programmatically gecreeerd in [!DNL Google] platform.
* [!DNL Platform] bevat momenteel geen metrische waarde om een geslaagde activering te valideren. Raadpleeg het aantal gebruikers in Google om de integratie te valideren en te begrijpen waar de doelgroep zich op richt.
* Nadat u een publiek aan een [!DNL Google Ad Manager] doel, verschijnt de publieksnaam onmiddellijk in [!DNL Google Ad Manager] gebruikersinterface.
* De segmentpopulatie heeft 24-48 uur nodig om te verschijnen in [!DNL Google Ad Manager]. Bovendien moeten doelgroepen een publieksgrootte hebben van ten minste 50 profielen om te kunnen worden weergegeven in [!DNL Google Ad Manager]. Soorten publiek met een grootte kleiner dan 50 profielen worden niet ingevuld in [!DNL Google Ad Manager].

## Ondersteunde identiteiten {#supported-identities}

[!DNL Google Ad Manager] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Selecteer deze doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | [!DNL Apple ID for Advertisers] | Selecteer deze doelidentiteit wanneer uw bronidentiteit een IDFA-naamruimte is. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), ook bekend als [!DNL Device ID]. Een numerieke apparaat-id van 38 cijfers waarmee de Audience Manager werkt. | Google gebruikt [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) om gebruikers in Californië te richten, en identiteitskaart van de Koek van Google voor alle andere gebruikers. |
| [!DNL Google] cookie-id | [!DNL Google] cookie-id | [!DNL Google] gebruikt deze id om gebruikers buiten Californië als doel in te stellen. |
| RIDA | Roku ID for Advertising. Deze id identificeert unieke Roku-apparaten. |  |
| GEMAAKT | Microsoft-advertentie-id. Deze id identificeert apparaten waarop Windows 10 wordt uitgevoerd op unieke wijze. |  |
| Amazon Fire TV ID | Deze id is uniek voor Amazon Fire TV&#39;s. |  |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie worden alle soorten publiek beschreven die u naar deze bestemming kunt exporteren.

Alle bestemmingen ondersteunen de activering van publiek dat door het Experience Platform wordt geproduceerd [Segmenteringsservice](../../../segmentation/home.md).

Bovendien ondersteunt deze bestemming ook de activering van het publiek dat in de onderstaande tabel wordt beschreven.

| Type publiek | Beschrijving |
---------|----------|
| Aangepaste uploads | Soorten publiek dat via CSV-bestanden in het Experience Platform wordt opgenomen. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek naar de Google-bestemming. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

Als u uw eerste bestemming wilt maken met [!DNL Google Ad Manager] en hebben de [ID-synchronisatiefunctie](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in het verleden (met Audience Manager of andere toepassingen), neemt u contact op met Adobe Consulting of de klantenservice om id-syncs in te schakelen. Als u al eerder was ingesteld [!DNL Google] Als u integreert in Audience Manager, worden de id-syncs die u hebt ingesteld, overgedragen naar Platform.

### Aanbieding toestaan {#allow-listing}

Aanbieding toestaan is verplicht voordat je eerste aanbieding wordt ingesteld [!DNL Google Ad Manager] bestemming in Platform. Voltooi de hieronder beschreven procedure voor het aanbieden van objecten in een geldige plaats voordat je de bestemming maakt.

1. Voer de stappen uit die in het dialoogvenster [Google Ad Manager-documentatie](https://support.google.com/admanager/answer/3289669?hl=en) om Adobe toe te voegen als een gekoppeld Platform voor gegevensbeheer (DMP).
2. In de [!DNL Google Ad Manager] interface, ga naar **[!UICONTROL Admin]** > **[!UICONTROL Global Settings]** > **[!UICONTROL Network Settings]** en de **[!UICONTROL API Access]** schuifregelaar.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="Id van publiek toevoegen aan publieksnaam"
>abstract="Selecteer deze optie als u de publieksnaam in Google Ad Manager de gebruikers-id uit het Experience Platform wilt laten opnemen, bijvoorbeeld: `Audience Name (Audience ID)`"

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Account ID]**: Voer uw [!DNL Audience Link ID] van uw [!DNL Google] account. Dit is een specifieke id die aan uw [!DNL Google Ad Manager] netwerk (niet uw [!DNL Network code]). U vindt dit onder **[!UICONTROL Admin > Global settings]** in de [!DNL Google Ad Manager] interface.
* **[!UICONTROL Account Type]**: Selecteer een optie, afhankelijk van uw account bij Google:
   * Gebruiken `DFP by Google` for [!DNL DoubleClick] voor uitgevers
   * Gebruiken `AdX buyer` for [!DNL Google AdX]
* **[!UICONTROL Append audience ID to audience name]**: Selecteer deze optie als u de publieksnaam in Google Ad Manager de gebruikers-id uit het Experience Platform wilt laten opnemen, bijvoorbeeld: `Audience Name (Audience ID)`.

>[!NOTE]
>
>Wanneer u een [!DNL Google Ad Manager] bestemming, gelieve met uw te werken [!DNL Google Account Manager] of Adobe om te begrijpen welk accounttype u hebt.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](../../ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

## Geëxporteerde gegevens {#exported-data}

Controleren of gegevens zijn geëxporteerd naar de [!DNL Google Ad Manager] doel, controleer uw [!DNL Google Ad Manager] account. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.

## Problemen oplossen {#troubleshooting}

Voor het geval u om het even welke fouten terwijl het gebruiken van deze bestemming tegenkomt en uit naar of Adobe of Google moet reiken, houd de volgende IDs bij.

Dit zijn Adobe Google-account-id&#39;s:

* **[!UICONTROL Account ID]**: 87933855
* **[!UICONTROL Customer ID]**: 89690775