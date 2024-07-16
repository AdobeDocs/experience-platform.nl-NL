---
keywords: reclame, bureau voor de handel, reclamebureau
title: De verbinding van de handelsbureau
description: De Trade Desk is een zelfbedieningsplatform waarmee adverteerders doelgerichte digitale campagnes kunnen voeren op het hele scherm, de video en mobiele inventarisatiebronnen.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---

# [!DNL The Trade Desk] verbinding

## Overzicht {#overview}

[!DNL The Trade Desk] -doel helpt u profielgegevens naar [!DNL The Trade Desk] te verzenden.

[!DNL The Trade Desk] is een zelfbedieningsplatform waarmee adverteerders doelgerichte digitale campagnes kunnen uitvoeren voor verschillende soorten weergave, video en mobiele inventarisatiebronnen.

Als u profielgegevens naar [!DNL Trade Desk] wilt verzenden, moet u eerst verbinding maken met het doel.

## Gebruiksscenario’s {#use-cases}

Als een markeerteken wil ik publiek dat is opgebouwd uit [!DNL Trade Desk IDs] of apparaat-id&#39;s kunnen gebruiken om doelgerichte digitale campagnes te maken.

## Ondersteunde identiteiten {#supported-identities}

[!DNL The Trade Desk] ondersteunt de activering van soorten publiek op basis van de identiteiten in de onderstaande tabel. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Identiteit | Beschrijving |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| Handelsbureau-id | Advertiser-id in het Trade Desk-platform |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van het Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek naar de bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
>Als u uw eerste bestemming met [!DNL The Trade Desk] wilt tot stand brengen en niet de [ functionaliteit van de Synchronisatie van identiteitskaart ](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in de Dienst van identiteitskaart van het Experience Cloud in het verleden (met Adobe Audience Manager of andere toepassingen) hebt toegelaten, gelieve uit te reiken aan Adobe Consulting of de Zorg van de Klant om de syncs van identiteitskaart toe te laten. Als u eerder [!DNL The Trade Desk] -integratie hebt ingesteld in Audience Manager, worden de id-syncs die u hebt ingesteld, overgedragen naar Platform.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [ vestiging ](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL Trade Desk] [!UICONTROL Account ID] .
* **[!UICONTROL Server Location]**: Vraag uw [!DNL Trade Desk] -vertegenwoordiger welke regionale server u moet gebruiken. Dit zijn de beschikbare regionale servers waaruit u kunt kiezen:
   * **[!UICONTROL Europe]**
   * **[!UICONTROL Singapore]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL North America East]**
   * **[!UICONTROL North America West]**
   * **[!UICONTROL Latin America]**

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [ publieksgegevens aan het stromen publiek de uitvoerbestemmingen ](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

In het [ programma van het Publiek ](../../ui/activate-segment-streaming-destinations.md#scheduling) stap, moet u uw publiek aan hun overeenkomstige identiteitskaart of vriendschappelijke naam in het bestemmingsplatform manueel in kaart brengen.

Wanneer het in kaart brengen van segmenten, adviseren wij u de het publieksnaam van het Platform of een kortere vorm van het, voor gebruiksgemak gebruiken. De gebruikers-id of naam in uw bestemming hoeft echter niet overeen te komen met de naam in uw platformaccount. Elke waarde die u in het toewijzingsveld invoegt, wordt weerspiegeld door het doel.

Als u meerdere apparaattoewijzingen gebruikt (cookie-id&#39;s, [!DNL IDFA], [!DNL GAID] ), moet u voor alle drie toewijzingen dezelfde toewijzingswaarde gebruiken. [!DNL The Trade Desk] zal alle hen in één enkel segment, met een apparaat-vlakke onderbreking bijeenvoegen.

![ Identiteitskaart van de Afbeelding van het Segment ](../../assets/common/segment-mapping-id.png)

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL Trade Desk] -account om te controleren of gegevens zijn geëxporteerd naar [!DNL The Trade Desk] -doel. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.
