---
title: Adobe Campaign Managed Cloud Services-verbinding
description: Adobe Campaign Managed Cloud Services biedt een platform voor het ontwerpen van de ervaringen van klanten over meerdere kanalen en een omgeving voor visuele campagneorchestratie, real-time interactiebeheer en uitvoering via meerdere kanalen.
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '1721'
ht-degree: 0%

---

# [!DNL Adobe Campaign Managed Cloud Services]-verbinding {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>Deze integratie werkt met [[!DNL Adobe Campaign]  versie 8.4 of hoger ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1).

## Overzicht {#overview}

[!DNL Adobe Campaign Managed Cloud Services] biedt een platform voor het ontwerpen van de ervaringen van klanten over meerdere kanalen en een omgeving voor visuele campagneorchestratie, realtime interactiebeheer en uitvoering via meerdere kanalen. [ krijgen Begonnen met Campagne ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

Campagne gebruiken om:

* De personalisatie en de betrokkenheid van de aandrijving door één enkele toegankelijk mening van de klant;
* E-mail, mobiel, online en offline kanalen integreren in de reis van de klant,
* Automatiseer de levering van betekenisvolle en geschikte berichten en aanbiedingen.

## Beveiligingsmechanismen {#guardrails}

Houd rekening met de volgende instructies wanneer u de [!DNL Adobe Campaign Managed Cloud Services] -verbinding gebruikt:

* U kunt [ ](#activate) een maximum van 25 publiek aan deze bestemming activeren.

  U kunt deze grens veranderen door de waarde van **NmsCdp_Aep_Audience_List_Limit** optie in **[!UICONTROL Administration]** > **[!UICONTROL Platform]** > **[!UICONTROL Options]** omslag van de ontdekkingsreiziger van de Campagne bij te werken. Deze garantie beperkt het totale aantal Experience Platform-doelgroepen dat naar één Campagneexemplaar kan worden geëxporteerd voor alle geconfigureerde doelen.

* Voor elk publiek, kunt u tot 20 gebieden aan [ kaart ](#map) aan [!DNL Adobe Campaign] toevoegen.

  U kunt deze grens veranderen door de waarde van **NmsCdp_Aep_Destures_Max_Columns** optie in **[!UICONTROL Administration]** > **[!UICONTROL Platform]** > **[!UICONTROL Options]** omslag van de ontdekkingsreiziger van de Campagne bij te werken.

* Gegevensbewaring op Azure Blob Storage Data Landing Zone (DLZ): 7 dagen.
* De activeringsfrequentie bedraagt minimaal 3 uur.
* De maximale lengte van de bestandsnaam die door deze verbinding wordt ondersteund, is 255 tekens. Wanneer u [ het uitgevoerde dossier - naam ](../../ui/activate-batch-profile-destinations.md#configure-file-names) vormt, zorg ervoor het dossier - naam 255 karakters niet overschrijdt. Als u de maximale lengte van de bestandsnaam overschrijdt, treden activeringsfouten op.
* Segmenten/publiek met speciale tekens (bijvoorbeeld: `&`) worden niet ondersteund bij het exporteren van soorten publiek naar [!DNL Adobe Campaign] .

## Gebruiksscenario&#39;s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u [!DNL Adobe Campaign] zou moeten gebruiken leidt de bestemming van de Dienst, hier een geval van het steekproefgebruik dat [!DNL Adobe Experience Platform] klanten kunnen oplossen door deze bestemming te gebruiken.

* [!DNL Adobe Experience Platform] maakt een klantprofiel dat informatie bevat zoals de identiteitsgrafiek, gedragsgegevens van analyses, het samenvoegen van offline- en onlinegegevens, enzovoort. Met deze integratie kunt u de segmentatiemogelijkheden die al in [!DNL Adobe Campaign] bestaan, uitbreiden met die [!DNL Adobe Experience Platform] -gebruikers. U kunt die gegevens dus activeren in Campagne.

  Een sportattierbedrijf wil bijvoorbeeld het publiek met [!DNL Adobe Experience Platform] bevoegdheden aanspreken en deze activeren met [!DNL Adobe Campaign] om naar het klantenbestand te reiken via de verschillende kanalen die worden ondersteund door [!DNL Adobe Campaign] . Zodra de berichten zijn verzonden, willen ze het klantprofiel in [!DNL Adobe Experience Platform] verbeteren met ervaringsgegevens uit [!DNL Adobe Campaign] , zoals verzenden, openen en klikken.

  Het resultaat is kanaalcampagnes die consistenter zijn in het Adobe Experience cloud-ecosysteem en een rijk klantprofiel dat zich snel aanpast en leert.


* Naast activering van het publiek in Campagne, kunt u [!DNL Adobe Campaign Managed Services] bestemming gebruiken om extra profielattributen in te brengen die aan een profiel op [!DNL Adobe Experience Platform] worden gebonden en een synchronisatieproces op zijn plaats hebben zodat zij in het [!DNL Adobe Campaign] gegevensbestand worden bijgewerkt.

  Stel bijvoorbeeld dat u waarden voor opt-in en opt-out vastlegt in [!DNL Adobe Experience Platform] . Met deze verbinding kunt u deze waarden overbrengen naar [!DNL Adobe Campaign] en een synchronisatieproces uitvoeren zodat ze regelmatig worden bijgewerkt.

  >[!NOTE]
  >
  >Synchronisatie van profielkenmerken is beschikbaar voor profielen die al aanwezig zijn in de [!DNL Adobe Campaign] -database.

[ leer meer op  [!DNL Adobe Campaign]  integratie met  [!DNL Adobe Experience Platform] ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html)

## Ondersteunde identiteiten {#supported-identities}

*[!DNL Adobe Campaign Managed Cloud Services]* ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| external_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. Wij adviseren gebruikend deze identiteit en het in kaart brengen aan identiteitskaart in uw instantie van de Campagne die klant (loyalty_ID, account_ID, customer_ID...) vertegenwoordigt |
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Deze namespace kan ook door de volgende aliassen worden bedoeld: &quot;identiteitskaart van Adobe Marketing Cloud&quot;, &quot;[!DNL Adobe Experience Cloud] identiteitskaart&quot;, &quot;[!DNL Adobe Experience Platform] identiteitskaart&quot;. Zie het volgende document op [ ECID ](/help/identity-service/features/ecid.md) voor meer informatie. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Zowel platte tekst als gehashte e-mailadressen van SHA256 worden ondersteund door [!DNL Adobe Experience Platform]. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| phone_sha256 | Telefoonnummers die zijn hashed met het SHA256-algoritme | Onbewerkte tekst en via SHA256 gehashte telefoonnummers worden ondersteund door [!DNL Adobe Experience Platform] . Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| GAID | GOOGLE ADVERTISING ID | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [ ](../../../segmentation/home.md). |
| Alle andere doelgroepen | Nee | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [ diverse publieksoorsprong ](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere Experience Platform-toepassingen, zoals [!DNL Adobe Journey Optimizer] , </li><li> en meer. </li></ul> |

{style="table-layout:auto"}



Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
|--------------------|-----------|-------------|-----------|
| [ het publiek van Mensen ](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantenprofielen, die u toestaan om specifieke groepen mensen voor marketing campagnes te richten. | Frequente kopers, winkeliers |
| [ publiek van de Rekening ](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [ Het publiek van het Vooruitzicht ](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [ de uitvoer van de Dataset ](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het [!DNL Adobe Experience Platform] Data Lake. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}


## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een publiek, samen met de gewenste schemagebieden (bijvoorbeeld: e-mailadres, telefoonaantal, achternaam), zoals gekozen in het uitgezochte scherm van profielkenmerken van het [ werkschema van de bestemmingsactivering ](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Lees meer over [ partij op dossier-gebaseerde bestemmingen ](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![[!DNL Adobe Campaign Managed Cloud Services] formulier met doeldetails waarin de velden Naam, Beschrijving, Instantie selecteren, Doeltoewijzing en Synchronisatietype worden weergegeven. ](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Select instance]**: Uw **[!DNL Campaign]** marketinginstantie.
* **[!UICONTROL Target mapping]**: selecteer de doeltoewijzing die u in **[!DNL Adobe Campaign]** gebruikt om leveringen te verzenden. [Meer info](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html).
* **[!UICONTROL Select sync type]** :

   * **[!UICONTROL Audience sync]**: gebruik deze optie om [!DNL Adobe Experience Platform] publiek naar [!DNL Adobe Campaign] te sturen.
   * **[!UICONTROL Profile sync (Update only)]**: gebruik deze optie om [!DNL Adobe Experience Platform] profielkenmerken over te brengen naar [!DNL Adobe Campaign] en een synchronisatieproces te laten uitvoeren, zodat deze regelmatig kunnen worden bijgewerkt.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, verwijs naar de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

### Beleid en handhavingsmaatregelen voor bestuur {#governance}

Selecteer de marketingacties die van toepassing zijn op de gegevens die u naar de bestemming wilt exporteren. Voor [!DNL Adobe Campaign] raden we u aan de handeling **[!UICONTROL Email Targeting]** marketing te selecteren.

Voor meer informatie over marketing acties, zie de [ pagina van het het beleidsoverzicht van het gegevensgebruik ](/help/data-governance/policies/overview.md).

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer publieksgegevens aan de uitvoerbestemmingen van het partijprofiel ](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html) voor instructies bij het activeren van publieksgegevens aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

Selecteer XDM-velden om met de profielen te exporteren en deze toe te wijzen aan de corresponderende [!DNL Adobe Campaign] -velden.[ leer meer op identiteit en attributenselectie voor e-mail marketing bestemmingen ](overview.md)

1. Bronvelden selecteren:

   * Selecteer een **herkenningsteken** (bijvoorbeeld: het e-mailgebied) als bronidentiteit die uniek een profiel in [!DNL Adobe Experience Platform] en [!DNL Adobe Campaign] identificeert.

   * Selecteer alle andere **attributen van het bronprofiel XDM** die naar [!DNL Adobe Campaign] moeten worden uitgevoerd.

   >[!NOTE]
   >
   >Het &quot;segmentMembershipStatus&quot;gebied is een vereiste afbeelding om segmentMembership status te weerspiegelen. Dit veld wordt standaard toegevoegd en kan niet worden gewijzigd of verwijderd.

1. Koppel elk veld met het doelveld in [!DNL Adobe Campaign] . De beschikbare doelgebieden worden bepaald door de geselecteerde doelafbeelding wanneer [ het creëren van de bestemming ](#destination-details).

1. Verplichte kenmerken en deduplicatietoetsen identificeren. Waarden in kenmerken die zijn gemarkeerd als &quot;Verplicht&quot; of &quot;Deduplication key&quot;, mogen niet null zijn.

   * [ Verplicht attributen ](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) zorgen ervoor dat alle profielverslagen de geselecteerde attributen(s) bevatten. Alle geëxporteerde profielen bevatten bijvoorbeeld een e-mailadres. De aanbeveling moet zowel het identiteitsveld als het als deduplicatietoets gebruikte veld verplicht stellen.
   * [ de deduplicatiesleutel van A ](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) is een primaire sleutel die de identiteit bepaalt waardoor de gebruikers hun profielen willen worden gededupliceerd.

     >[!IMPORTANT]
     >
     >Zorg ervoor dat de naam van het deduplicatietoetskenmerk overeenkomt met de kolomnaam van de geselecteerde doeltoewijzing.

   ![ het kaartscherm dat van Attributen XDM brongebieden toont aan [!DNL Adobe Campaign] doelgebieden, met verplichte en deduplicatie zeer belangrijke indicatoren in kaart worden gebracht.](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. Nadat de toewijzing is uitgevoerd, kunt u de doelconfiguratie controleren en voltooien om te beginnen met het verzenden van gegevens naar **[!DNL Campaign]** .
   [ Leer hoe te om bestemmingsconfiguratie ](/help/destinations/destination-types.md#destination-types-and-categories) te herzien en te voltooien.

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Nadat een doel is geactiveerd, kunt u de bijbehorende taak openen en de gegevens exporteren in Campagne.

### Exporttaken voor gegevens controleren {#jobs}

Navigeer naar het menu **[!UICONTROL Administration]** > **[!UICONTROL Audit]** > **[!UICONTROL Audience load jobs]** om alle exporttaken te controleren die vanuit [!DNL Adobe Experience Platform] zijn geactiveerd.

![[!DNL Adobe Campaign] Scherm met doeltaken weergeven waarop uitvoertaken zijn geactiveerd vanuit [!DNL Adobe Experience Platform] . ](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### Geëxporteerde gegevens openen {#data}

Voor **[!UICONTROL Audience sync]** kunt u het geëxporteerde publiek controleren door naar het menu **[!UICONTROL Profile and target]** > **[!UICONTROL List]** > **[!UICONTROL AEP audiences]** te navigeren.

![[!DNL Adobe Campaign] De lijstweergave van AEP-soorten publiek toont het geëxporteerde publiek uit Experience Platform dat beschikbaar is onder Profiel en doel. ](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

Voor **[!UICONTROL Profile sync (Update only)]** worden gegevens automatisch bijgewerkt naar de Campagne-database voor elk profiel dat wordt geactiveerd door het publiek dat in de bestemming is geactiveerd.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).
