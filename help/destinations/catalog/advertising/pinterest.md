---
title: Verbinding met Pinterest Customer List
description: Maak een publiek op basis van uw klantlijsten, personen die uw site hebben bezocht of personen die al met uw inhoud hebben gewerkt op Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 1%

---

# [!DNL Pinterest Customer List]-verbinding

## Overzicht {#overview}

Maak een publiek op basis van uw klantlijsten, personen die uw site hebben bezocht of personen die al met uw inhoud hebben gewerkt op Pinterest.

>[!IMPORTANT]
>
>Deze bestemming werd gebouwd door het team van Pinterest. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen met de afdeling https://help.pinterest.com/en/contact.

## Vereisten {#prerequisites}

* De gebruiker moet zich verifiëren met een Pinterest-account dat toegang heeft tot het advertentieaccount waaraan hij of zij een publiek wil toevoegen. De details op het delen van adverteerderrekeningen kunnen [ hier ](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts) worden gevonden. Specifiek, zou de gebruiker de &quot;publiek&quot;toegangsniveaus nodig hebben.
* De details over de identiteitsformaten van de klantenlijst kunnen [ hier ](https://help.pinterest.com/en/business/article/audience-targeting) worden gevonden.

## Ondersteunde identiteiten {#supported-identities}

Het doel van [!DNL Pinterest Customer List] ondersteunt de activering van de identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=nl-NL#getting-started).

In de [ toewijzingsstap ](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) van het werkschema van de bestemmingsactivering, kaart de gewenste identiteiten aan het doelgebied *pinterest_publiek* in kaart. Identiteiten worden onderscheiden en opgelost na gegevensinvoer in Pinterest.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Wijs *GAID* bronIdentiteit namespace aan het gebied van de doelidentiteit *toe pinterest_publiek*. |
| IDFA | [!DNL Apple ID for Advertisers] | Wijs *IDFA* bronidentiteit namespace aan het gebied van de doelidentiteit *toe pinterest_publiek*. |
| EMAIL | E-mailadressen (tekst wissen of hashed met het algoritme SHA256) | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. <br> Kaart *E-mail* of *Email_LC_SHA256* bron identiteitsnaamruimte aan het gebied van de doelidentiteit *pinterest_publiek* in kaart. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in de Pinterest Customer List-bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL Pinterest Customer List] bestemming zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Hoofdletters en kleine letters gebruiken 1

Maak een publiek op basis van uw klantlijsten, personen die uw site hebben bezocht of personen die al met uw inhoud hebben gewerkt op Pinterest.

## Verbinden met doel {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Wanneer [ vestiging ](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Ad Account ID]**: Je Pinterest-advertentie-id.

### Verificatiegegevens vernieuwen {#refresh-authentication-credentials}

Pinterest-tokens verlopen elke 30 dagen. Zodra het teken is verlopen, de gegevensuitvoer naar de bestemming houdt op werkend. Om deze situatie te verhinderen, verifieer opnieuw door de volgende stappen uit te voeren:

1. Ga naar **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]**
2. (Optioneel) Gebruik de beschikbare filters op de pagina om alleen Pinterest-accounts weer te geven.
   ![ Filter om slechts de rekeningen van Pinterest te tonen ](/help/destinations/assets/catalog/advertising/pinterest-customer-list/refresh-oauth-filters.png)
3. Selecteer de account die u wilt vernieuwen, selecteer de ellips en selecteer **[!UICONTROL Edit details]** .
   ![ uitgezocht geef detailcontrole ](/help/destinations/assets/catalog/advertising/pinterest-customer-list/refresh-oauth-edit-details.png) uit
4. Selecteer **[!UICONTROL Reconnect OAuth]** in het modaal venster en verifieer het opnieuw met uw Pinterest-referenties.
   ![ Modal venster met Opnieuw verbinden optie OAuth ](/help/destinations/assets/catalog/advertising/pinterest-customer-list/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>Uw verificatiereferenties worden vernieuwd en de vervaltijd wordt ingesteld op 30 dagen.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [ overzicht van het Beleid van Gegevens ](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=nl-NL).

## Aanvullende bronnen {#additional-resources}

Gelieve te verwijzen naar de [ pagina van het Centrum van de Hulp van Pinterest ](https://help.pinterest.com/en/business/article/audience-targeting) voor extra informatie.

+++ Wijzigingen weergeven


| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| November 2023 | Bijwerken van functionaliteit en documentatie | De Pinterest-bestemming in Real-Time CDP gebruikt nu de v5 Advertiser-API. |

{style="table-layout:auto"}


+++
