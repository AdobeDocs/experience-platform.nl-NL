---
keywords: google en manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google en manager; DFP
title: Google Ad Manager-verbinding
description: Google Ad Manager, voorheen bekend als DoubleClick voor Publishers of DoubleClick AdX, is een advertentieplatform uit Google dat uitgevers de mogelijkheid biedt om de weergave van advertenties op hun websites, via video en in mobiele apps te beheren.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 1%

---

# [!DNL Google Ad Manager] verbinding

## Overzicht {#overview}

[!DNL Google Ad Manager], voorheen bekend als [!DNL DoubleClick for Publishers] (DFP) of [!DNL DoubleClick AdX], is een platform voor advertenties van [!DNL Google] uitgevers krijgen de middelen om de weergave van advertenties op hun websites , via video en in mobiele apps te beheren .

## Doelspecificaties {#specifics}

Let op de volgende details die specifiek zijn voor [!DNL Google Ad Manager] bestemmingen:

* Geactiveerd publiek wordt programmatically gecreeerd in [!DNL Google] platform.
* [!DNL Platform] bevat momenteel geen metrische waarde om een geslaagde activering te valideren. Raadpleeg het aantal gebruikers in Google om de integratie te valideren en te begrijpen waar de doelgroep zich op richt.
* Na het toewijzen van een publiek aan een [!DNL Google Ad Manager] doel, verschijnt de publieksnaam onmiddellijk in [!DNL Google Ad Manager] gebruikersinterface.
* De segmentpopulatie heeft 24-48 uur nodig om te verschijnen in [!DNL Google Ad Manager]. Bovendien moeten doelgroepen een publieksgrootte hebben van ten minste 50 profielen om te kunnen worden weergegeven in [!DNL Google Ad Manager]. Soorten publiek met een grootte kleiner dan 50 profielen worden niet ingevuld in [!DNL Google Ad Manager].

## Ondersteunde identiteiten {#supported-identities}

[!DNL Google Ad Manager] ondersteunt de activering van het publiek op basis van de in de onderstaande tabel weergegeven identiteiten. Meer informatie over [identiteiten](/help/identity-service/features/namespaces.md).

| Identiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
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

Als u uw eerste bestemming wilt maken met [!DNL Google Ad Manager] en hebben de [ID-synchronisatiefunctie](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in het verleden (met Audience Manager of andere toepassingen), gelieve te richten aan de Raadpleging van de Adobe of de Zorg van de Klant om identiteitskaart syncs toe te laten. Als u al eerder was ingesteld [!DNL Google] Als u integreert in Audience Manager, worden de id-syncs die u hebt ingesteld, overgedragen naar Platform.

### Aanbieding toestaan {#allow-listing}

Aanbieding toestaan is verplicht voordat je eerste aanbieding wordt ingesteld [!DNL Google Ad Manager] doel in Platform. Voltooi de hieronder beschreven procedure voor het aanbieden van objecten in een geldige plaats voordat je de bestemming maakt.

1. Voer de stappen uit die in het dialoogvenster [Google Ad Manager-documentatie](https://support.google.com/admanager/answer/3289669?hl=en) Adobe toevoegen als een gekoppeld gegevensbeheerplatform (DMP).
2. In de [!DNL Google Ad Manager] interface, ga naar **[!UICONTROL Admin]** > **[!UICONTROL Global Settings]** > **[!UICONTROL Network Settings]** en de **[!UICONTROL API Access]** schuifregelaar

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

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
* **[!UICONTROL Append audience ID to audience name]**: Selecteer deze optie als u de publieksnaam in Google Ad Manager wilt laten opnemen in de gebruikers-id van het Experience Platform, bijvoorbeeld: `Audience Name (Audience ID)`.

>[!NOTE]
>
>Wanneer u een [!DNL Google Ad Manager] bestemming, gelieve met uw te werken [!DNL Google Account Manager] of een Adobe die representatief is voor het accounttype dat u hebt.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [De publieksgegevens van de activering aan het stromen publiek de uitvoerbestemmingen](../../ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

## Geëxporteerde gegevens {#exported-data}

Controleren of gegevens zijn geëxporteerd naar de [!DNL Google Ad Manager] doel, controleer uw [!DNL Google Ad Manager] account. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.

## Problemen oplossen {#troubleshooting}

Voor het geval u om het even welke fouten terwijl het gebruiken van deze bestemming tegenkomt en moet uit naar of Adobe of Google reiken, houd de volgende IDs bij.

Dit zijn Google-account-id&#39;s van Adobe:

* **[!UICONTROL Account ID]**: 87933855
* **[!UICONTROL Customer ID]**: 89690775