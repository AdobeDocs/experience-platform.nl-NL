---
keywords: reclame, bureau voor de handel, reclamebureau
title: De verbinding van de handelsbureau
description: De Trade Desk is een zelfbedieningsplatform waarmee adverteerders doelgerichte digitale campagnes kunnen voeren op het hele scherm, de video en mobiele inventarisatiebronnen.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 138bfe721bb20fe3ba614a73ffffca3e00979acb
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 0%

---

# [!DNL The Trade Desk]-verbinding

## Overzicht {#overview}

Gebruik deze doelconnector om profielgegevens naar [!DNL The Trade Desk] te verzenden. Deze schakelaar verzendt gegevens naar het [!DNL The Trade Desk] eerste partijeindpunt. De integratie tussen Adobe Experience Platform en [!DNL The Trade Desk] biedt geen ondersteuning voor het exporteren van gegevens naar het eindpunt van derden voor [!DNL The Trade Desk] .

[!DNL The Trade Desk] is een zelfbedieningsplatform dat kopers van advertenties in staat stelt doelgerichte digitale campagnes uit te voeren voor alle weergave-, video- en mobiele-inventarisbronnen.

Als u profielgegevens naar [!DNL The Trade Desk] wilt verzenden, moet u eerst verbinding maken met het doel, zoals wordt beschreven in de volgende secties van deze pagina.

## Gebruiksscenario’s {#use-cases}

Als markator, wil ik publiek kunnen gebruiken dat van [!DNL Trade Desk IDs] of apparaat IDs wordt gebouwd om het richten of publiek-gerichte digitale campagnes te creëren.

## Ondersteunde identiteiten {#supported-identities}

[!DNL The Trade Desk] ondersteunt de activering van soorten publiek op basis van de identiteiten in de onderstaande tabel. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

Hieronder ziet u de identiteiten die worden ondersteund door het doel van [!DNL The Trade Desk] . Deze identiteiten kunnen worden gebruikt om het publiek te activeren naar [!DNL The Trade Desk] .

Alle identiteiten in de onderstaande tabel zijn vooraf geconfigureerd en automatisch toegewezen tijdens de activering. U hoeft deze toewijzingen niet handmatig te configureren in de activeringsworkflow.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Wordt geactiveerd wanneer het profiel een GAID bevat. |
| IDFA | Apple-id voor adverteerders | Wordt geactiveerd wanneer een IDFA aanwezig is in het profiel. |
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Deze naamruimte kan ook worden aangeduid met de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Lees het volgende document op [&#x200B; ECID &#x200B;](/help/identity-service/features/ecid.md) voor meer informatie. |
| [!DNL Tradedesk] | [!DNL TDID] in het [!DNL The Trade Desk] -platform | Wordt geactiveerd wanneer een profiel een ECID heeft en er in Experience Platform een ECID-koppeling bestaat tussen de handels-ID. |

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

De vereisten hangen van welke identiteitstypes af u voor publieksactivering van plan bent te gebruiken:

**voor mobiele slechts de activering van identiteitskaart**, zijn er geen eerste vereisten. Zolang u id&#39;s (GAID en/of IDFA) voor uw klanten verzamelt en beheert, kunt u het publiek activeren op [!DNL The Trade Desk] .

**voor op cookie-gebaseerde het richten op[!DNL The Trade Desk]**, zorg ervoor dat een afbeelding tussen ECID en [!DNL Trade Desk ID] wordt gevestigd. Voer de onderstaande stappen uit om dit te doen:

1. **laat de synchronisatiefunctionaliteit van identiteitskaart** toe: Als dit uw eerste vestiging [!DNL The Trade Desk ID] activering is en u hebt niet de [&#x200B; functionaliteit van de de synchronisatieidentiteitskaart &#x200B;](https://experienceleague.adobe.com/nl/docs/id-service/using/id-service-api/methods/idsync) in de Dienst van identiteitskaart van Experience Cloud in het verleden (met Adobe Audience Manager of andere toepassingen) toegelaten, contacteer Adobe Consulting of de Zorg van de Klant om de syncs van identiteitskaart toe te laten.
   * Als u eerder [!DNL The Trade Desk] -integratie hebt ingesteld in Audience Manager, worden de bestaande ID-syncs automatisch overgedragen naar Experience Platform.

2. **Instrument uw Web-pagina&#39;s**: Voer code op uw Web-pagina&#39;s uit om afbeeldingen tussen [!DNL The Trade Desk ID] en Adobe ECID tot stand te brengen. Zo kan Experience Platform ID&#39;s van handelsvertegenwoordigingen koppelen aan uw klantprofielen.

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

### Vooraf geconfigureerde toewijzingen {#preconfigured-mappings}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_ttd"
>title="Vooraf geconfigureerde toewijzingssets"
>abstract="Wij hebben deze vier kaartreeksen voor u vooraf gevormd. Wanneer u gegevens activeert op de handelsbank, hoeven de profielen die voor het geactiveerde publiek worden gekwalificeerd niet noodzakelijkerwijs alle vier de identiteiten te hebben aanwezig op de profielen, aangezien deze bestemming met om het even welke doelidentiteiten zal werken die hier worden getoond. <br> Voor op cookies gebaseerde activering op basis van de handels-deskid hebt u ECID nodig die aanwezig is op het profiel en een id-synchronisatietoewijzing tussen de handelsbureau-id en ECID."
>additional-url="https://experienceleague.adobe.com/nl/docs/experience-platform/destinations/catalog/advertising/tradedesk#preconfigured-mappings" text="Lees meer over de vooraf geconfigureerde toewijzingen"

De volgende identiteitstoewijzingen zijn **vooraf gevormd en automatisch bevolkt** voor u in het werkschema van de publiekactivering:

* GAID (Google Advertising ID)
* IDFA (Apple-id voor adverteerders)
* ECID (Experience Cloud-ID)
* [!DNL The Trade Desk ID]

![&#x200B; Schermschot die de verplichte afbeeldingen &#x200B;](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png) tonen

Deze toewijzingen worden grijs en alleen-lezen weergegeven. U hoeft niets in deze stap te configureren. Selecteer **[!UICONTROL Next]** om door te gaan.

Experience Platform controleert automatisch elk profiel dat tot in de activeringswerkstroom toegewezen publiek behoort op alle ondersteunde identiteitstypen en activeert vervolgens het profiel met alle aanwezige identiteiten.

### Identiteitsvereisten per activeringstype

**Mobiele activering van identiteitskaart (GAID/IDFA):** Profielen met enkel GAID of IDFA zijn voldoende voor activering. Er zijn geen aanvullende identiteiten of voorwaarden vereist.

**Cookie-Gebaseerd die ([!DNL Trade Desk ID]) richt:** vereist allebei:

* ECID aanwezig op profiel
* Een synchronisatie van identiteitskaart afbeelding tussen [!DNL Trade Desk ID] en ECID (zoals die in de [&#x200B; wordt beschreven eerste vereisten &#x200B;](#prerequisites) sectie)

**Veelvoudig IDs gedrag:** als een profiel veelvoudige gesteunde identiteiten bevat, zal elke identiteit afzonderlijk aan [!DNL The Trade Desk] worden geactiveerd. Dit zorgt voor maximaal bereik en flexibiliteit bij de activering van uw publiek.

### Activeringsvoorbeelden

* **Mobiele profielen van identiteitskaart:** De Profielen met GAID en/of IDFA worden geactiveerd gebruikend hun respectieve advertentie IDs. Als een profiel zowel GAID als IDFA bevat, wordt elke id afzonderlijk geactiveerd.
* **op cookie-Gebaseerd profiel:** Een profiel met ECID en een overeenkomstige [!DNL Trade Desk ID] afbeelding zal worden geactiveerd gebruikend identiteitskaart van de Handelsplaats voor op koekje-gebaseerde het richten.
* **ECID-Enige profiel:** Een profiel met slechts ECID en geen [!DNL Trade Desk ID] afbeelding zal **niet worden uitgevoerd**. ECID alleen is onvoldoende voor activering.

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL The Trade Desk] -account om te controleren of gegevens naar de [!DNL The Trade Desk] -bestemming zijn geëxporteerd. Als de activering succesvol was, worden de soorten publiek in uw account ingevuld.
