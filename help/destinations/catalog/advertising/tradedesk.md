---
keywords: reclame, bureau voor de handel, reclamebureau
title: De verbinding van de handelsbureau
description: De Trade Desk is een zelfbedieningsplatform waarmee adverteerders doelgerichte digitale campagnes kunnen voeren op het hele scherm, de video en mobiele inventarisatiebronnen.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 1%

---

# [!DNL The Trade Desk]-verbinding

## Overzicht {#overview}


>[!IMPORTANT]
>
> Na de [&#x200B; interne verbetering &#x200B;](../../../release-notes/2025/july-2025.md#destinations) aan de bestemmingsdienst van juli 2025, kunt u a **daling in het aantal geactiveerde profielen** in uw dataflows [!DNL The Trade Desk] ervaren.
> &#x200B;> Dit daling wordt veroorzaakt door de introductie van het **ECID afbeeldingsvereiste** voor alle activiteiten aan dit bestemmingsplatform. Zie de [&#x200B; verplichte afbeelding &#x200B;](#mandatory-mappings) sectie in deze pagina voor gedetailleerde informatie.
>
>**wat veranderde:**
>
>* De afbeelding van ECID (identiteitskaart van Experience Cloud) is nu **verplicht** voor alle profielactiviteiten.
>* Profielen zonder ECID-toewijzing zullen **weggelaten worden** uit bestaande activeringsgegevens.
>
>**wat u moet doen:**
>
>* Controleer de publieksgegevens om te controleren of profielen geldige ECID-waarden hebben.
>* Controleer de activeringsgegevens om te controleren of het profiel wordt verwacht.


Gebruik deze doelconnector om profielgegevens naar [!DNL The Trade Desk] te verzenden. Deze schakelaar verzendt gegevens naar het [!DNL The Trade Desk] eerste partijeindpunt. De integratie tussen Adobe Experience Platform en [!DNL The Trade Desk] biedt geen ondersteuning voor het exporteren van gegevens naar het eindpunt van derden voor [!DNL The Trade Desk] .

[!DNL The Trade Desk] is een zelfbedieningsplatform dat kopers van advertenties in staat stelt doelgerichte digitale campagnes uit te voeren voor alle weergave-, video- en mobiele-inventarisbronnen.

Als u profielgegevens naar [!DNL The Trade Desk] wilt verzenden, moet u eerst verbinding maken met het doel, zoals wordt beschreven in de volgende secties van deze pagina.

## Gebruiksscenario’s {#use-cases}

Als markator, wil ik publiek kunnen gebruiken dat van [!DNL Trade Desk IDs] of apparaat IDs wordt gebouwd om het richten of publiek-gerichte digitale campagnes te creëren.

## Ondersteunde identiteiten {#supported-identities}

[!DNL The Trade Desk] ondersteunt de activering van soorten publiek op basis van de identiteiten in de onderstaande tabel. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

Hieronder ziet u de identiteiten die worden ondersteund door het doel van [!DNL The Trade Desk] . Deze identiteiten kunnen worden gebruikt om het publiek te activeren naar [!DNL The Trade Desk] .

Alle identiteiten in de onderstaande tabel zijn verplichte toewijzingen.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |
| ECID | Experience Cloud-id | Deze identiteit is verplicht voor de integratie, maar wordt niet gebruikt voor activering van het publiek. |
| Handelsbureau-id | Advertiser-id in het [!DNL The Trade Desk] -platform | Gebruik deze identiteit wanneer het activeren van publiek dat op bedrijfseigen identiteitskaart van het Bureau wordt gebaseerd. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek naar de bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
>Als u uw eerste bestemming met [!DNL The Trade Desk] wilt tot stand brengen en niet de [&#x200B; functionaliteit van de Synchronisatie van identiteitskaart &#x200B;](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/idsync) in de Dienst van identiteitskaart van Experience Cloud in het verleden (met Adobe Audience Manager of andere toepassingen) hebt toegelaten, te bereiken gelieve uit aan Adobe Consulting of de Zorg van de Klant om de syncs van identiteitskaart toe te laten. Als u eerder [!DNL The Trade Desk] -integraties hebt ingesteld in Audience Manager, worden de id-syncs die u hebt ingesteld, overgedragen naar Experience Platform.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [&#x200B; vestiging &#x200B;](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw [!DNL The Trade Desk] [!UICONTROL Account ID] .
* **[!UICONTROL Server Location]**: Vraag uw [!DNL The Trade Desk] -vertegenwoordiger welke regionale server u moet gebruiken. Hieronder ziet u de beschikbare regionale servers waaruit u kunt kiezen:

   * **[!UICONTROL APAC]**
   * **[!UICONTROL China]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL UK/EU]**
   * **[!UICONTROL US East Coast]**
   * **[!UICONTROL US West Coast]**

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [&#x200B; publieksgegevens aan het stromen publiek de uitvoerbestemmingen &#x200B;](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

In het [&#x200B; programma van het Publiek &#x200B;](../../ui/activate-segment-streaming-destinations.md#scheduling) stap, moet u uw publiek aan hun overeenkomstige identiteitskaart of vriendschappelijke naam in het bestemmingsplatform manueel in kaart brengen.

Bij het toewijzen van soorten publiek raadt Adobe u aan de Experience Platform-publieksnaam of een kortere vorm ervan te gebruiken, zodat u deze eenvoudig kunt gebruiken. De gebruikers-id of naam in uw bestemming hoeft echter niet overeen te komen met de naam in uw Experience Platform-account. Elke waarde die u in het toewijzingsveld invoegt, wordt weerspiegeld door het doel.

### Verplichte toewijzingen {#mandatory-mappings}

Alle die doelidentiteiten in de [&#x200B; worden beschreven gesteunde identiteiten &#x200B;](#supported-identities) sectie moeten in de afbeeldingsstap van het werkschema van de publiekactivering worden in kaart gebracht. Dit omvat het volgende:

* [!DNL GAID] (Google Advertising-id)
* [!DNL IDFA] (Apple-id voor adverteerders)
* [!DNL ECID] (Experience Cloud-id)
* [!DNL The Trade Desk ID]

![&#x200B; Schermschot die de verplichte afbeeldingen &#x200B;](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png) tonen

Als u alle doelidentiteiten toewijst, zorgt u ervoor dat de activering correct kan worden gesplitst en dat profielen kunnen worden geleverd met elke aanwezige identiteit. Dit betekent niet dat alle identiteiten op elk profiel aanwezig moeten zijn.

Om te kunnen exporteren naar de Trade Desk, moet een profiel het volgende bevatten:

* [!DNL ECID] en
* ten minste een van: [!DNL GAID], [!DNL IDFA] of [!DNL The Trade Desk ID]

Voorbeelden:

* [!DNL ECID] alleen: niet geëxporteerd
* [!DNL ECID] + [!DNL The Trade Desk ID] : geëxporteerd
* [!DNL ECID] + [!DNL IDFA] : geëxporteerd
* [!DNL ECID] + [!DNL GAID] : geëxporteerd
* [!DNL IDFA] + [!DNL The Trade Desk ID] (geen [!DNL ECID]): niet geëxporteerd

>[!NOTE]
> 
>Na de [&#x200B; verbetering van juli 2025 &#x200B;](/help/release-notes/2025/july-2025.md#destinations) aan de bestemmingsdienst, [!DNL ECID] afbeelding wordt afgedwongen. Profielen die ontbreken [!DNL ECID] , worden nu weggelaten zoals u had verwacht, waardoor het aantal activeringen lager kan uitvallen dan bij verouderd gedrag.

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL The Trade Desk] -account om te controleren of gegevens naar de [!DNL The Trade Desk] -bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.
