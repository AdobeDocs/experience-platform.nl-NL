---
title: Adobe Campaign Managed Cloud Services-verbinding
description: Adobe Campaign Managed Cloud Services biedt een platform voor het ontwerpen van de ervaringen van klanten over meerdere kanalen en een omgeving voor visuele campagneorchestratie, real-time interactiebeheer en uitvoering via meerdere kanalen.
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: f0db626401d76997e19632c3e27a133f577bc571
workflow-type: tm+mt
source-wordcount: '1610'
ht-degree: 0%

---

# Adobe Campaign Managed Cloud Services-verbinding {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>Deze integratie werkt met [ versie 8.4 van Adobe Campaign of hoger ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1).

## Overzicht {#overview}

Adobe Campaign Managed Cloud Services biedt een platform voor het ontwerpen van de ervaringen van klanten over meerdere kanalen en een omgeving voor visuele campagneorchestratie, real-time interactiebeheer en uitvoering via meerdere kanalen. [ krijgen Begonnen met Campagne ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

Campagne gebruiken om:

* De personalisatie en de betrokkenheid van de aandrijving door één enkele toegankelijk mening van de klant;
* E-mail, mobiel, online en offline kanalen integreren in de reis van de klant,
* Automatiseer de levering van betekenisvolle en geschikte berichten en aanbiedingen.

## Guardrails {#guardrails}

Houd rekening met de volgende instructies wanneer u de Adobe Campaign Managed Cloud Services-verbinding gebruikt:

* U kunt [ ](#activate) een maximum van 25 publiek aan deze bestemming activeren.

  U kunt deze grens veranderen door de waarde van **NmsCdp_Aep_Audience_List_Limit** optie in **[!UICONTROL Administration]** > **[!UICONTROL Platform]** > **[!UICONTROL Options]** omslag van de ontdekkingsreiziger van de Campagne bij te werken. Deze garantie beperkt het totale aantal Experience Platform-doelgroepen dat naar één Campagneexemplaar kan worden geëxporteerd voor alle geconfigureerde doelen.

* Voor elk publiek, kunt u tot 20 gebieden aan [ kaart ](#map) aan Adobe Campaign toevoegen.

  U kunt deze grens veranderen door de waarde van **NmsCdp_Aep_Destures_Max_Columns** optie in **[!UICONTROL Administration]** > **[!UICONTROL Platform]** > **[!UICONTROL Options]** omslag van de ontdekkingsreiziger van de Campagne bij te werken.

* Gegevensbewaring op Azure Blob Storage Data Landing Zone (DLZ): 7 dag.
* De activeringsfrequentie bedraagt minimaal 3 uur.
* De maximale lengte van de bestandsnaam die door deze verbinding wordt ondersteund, is 255 tekens. Wanneer u [ het uitgevoerde dossier - naam ](../../ui/activate-batch-profile-destinations.md#configure-file-names) vormt, zorg ervoor het dossier - naam 255 karakters niet overschrijdt. Als u de maximale lengte van de bestandsnaam overschrijdt, treden activeringsfouten op.
* Segmenten/publiek met speciale tekens (bijvoorbeeld: `&`) worden niet ondersteund bij het exporteren van soorten publiek naar Adobe Campaign.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de bestemming van de Dienst van de Beheer van Adobe Campaign zou moeten gebruiken, is hier een geval van het steekproefgebruik dat de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

* Adobe Experience Platform maakt een klantprofiel dat informatie bevat zoals de identiteitsgrafiek, gedragsgegevens van analyses, het samenvoegen van offline- en onlinegegevens, enzovoort. Dankzij deze integratie kunt u de segmentatiemogelijkheden die al in Adobe Campaign bestaan, uitbreiden met die door Adobe Experience Platform aangedreven doelgroepen. U kunt die gegevens dus activeren in Campaign.

  Een sportattierbedrijf wil bijvoorbeeld het door Adobe Experience Platform aangedreven publiek aantrekken en activeren met Adobe Campaign om op de verschillende door Adobe Campaign ondersteunde kanalen naar de klantenbasis te reiken. Zodra de berichten worden verzonden, willen zij het klantenprofiel in Adobe Experience platform met ervaringsgegevens van Adobe Campaign zoals verzenden, openen en klikken verbeteren.

  Het resultaat is kanaalcampagnes die consistenter zijn in het Adobe Experience cloud-ecosysteem en een rijk klantprofiel dat zich snel aanpast en leert.


* Naast activering van het publiek in Campagne, kunt u de bestemming van Adobe Campaign Managed Services gebruiken om extra profielattributen in te brengen die aan een profiel op Adobe Experience Platform worden gebonden en een synchronisatieproces op zijn plaats hebben zodat zij in het gegevensbestand van Adobe Campaign worden bijgewerkt.

  Stel bijvoorbeeld dat u waarden voor opt-in en opt-out vastlegt in Adobe Experience Platform. Met deze verbinding kunt u deze waarden overbrengen naar Adobe Campaign en een synchronisatieproces uitvoeren zodat ze regelmatig worden bijgewerkt.

  >[!NOTE]
  >
  >Synchronisatie van profielkenmerken is beschikbaar voor profielen die al aanwezig zijn in de Adobe Campaign-database.

[ Leer meer op de integratie van Adobe Campaign met Adobe Experience Platform ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html)

## Ondersteunde identiteiten {#supported-identities}

*Adobe Campaign Managed Cloud Services* steunt de activering van identiteiten die in de hieronder lijst worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| external_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. Wij adviseren gebruikend deze identiteit en het in kaart brengen aan identiteitskaart in uw instantie van de Campagne die klant (loyalty_ID, account_ID, customer_ID...) vertegenwoordigt |
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Deze naamruimte kan ook worden aangeduid met de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [ ECID ](/help/identity-service/features/ecid.md) voor meer informatie. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| phone_sha256 | Telefoonnummers die zijn hashed met het SHA256-algoritme | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-telefoonnummers. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| GAID | GOOGLE ADVERTISING ID | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |

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

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Select instance]**: Uw **[!DNL Campaign]** marketinginstantie.
* **[!UICONTROL Target mapping]**: selecteer de doeltoewijzing die u in **[!DNL Adobe Campaign]** gebruikt om leveringen te verzenden. [Meer informatie](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html).
* **[!UICONTROL Select sync type]**:

   * **[!UICONTROL Audience sync]**: gebruik deze optie om Adobe Experience Platform-publiek naar Adobe Campaign te sturen.
   * **[!UICONTROL Profile sync (Update only)]**: gebruik deze optie om Adobe Experience Platform-profielkenmerken over te brengen naar Adobe Campaign en een synchronisatieproces te laten uitvoeren zodat ze regelmatig kunnen worden bijgewerkt.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, verwijs naar de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

### Beleid en handhavingsmaatregelen voor bestuur {#governance}

Selecteer de marketingacties die van toepassing zijn op de gegevens die u naar de bestemming wilt exporteren. Voor Adobe Campaign raden we u aan de marketingactie **[!UICONTROL Email Targeting]** te selecteren.

Voor meer informatie over marketing acties, zie de [ pagina van het het beleidsoverzicht van het gegevensgebruik ](/help/data-governance/policies/overview.md).

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer publieksgegevens aan de uitvoerbestemmingen van het partijprofiel ](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html) voor instructies bij het activeren van publieksgegevens aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

Selecteer XDM-velden om met de profielen te exporteren en deze toe te wijzen aan de corresponderende Adobe Campaign-velden.[ leer meer op identiteit en attributenselectie voor e-mail marketing bestemmingen ](overview.md)

1. Bronvelden selecteren:

   * Selecteer een **herkenningsteken** (bijvoorbeeld: het e-mailgebied) als bronidentiteit die uniek een profiel in Adobe Experience Platform en Adobe Campaign identificeert.

   * Selecteer alle andere **attributen van het bronprofiel XDM** die naar Adobe Campaign moeten worden uitgevoerd.

   >[!NOTE]
   >
   >Het &quot;segmentMembershipStatus&quot;gebied is een vereiste afbeelding om segmentMembership status te weerspiegelen. Dit veld wordt standaard toegevoegd en kan niet worden gewijzigd of verwijderd.

1. Wijs elk gebied met zijn doelgebied in Adobe Campaign toe. De beschikbare doelgebieden worden bepaald door de geselecteerde doelafbeelding wanneer [ het creëren van de bestemming ](#destination-details).

1. Verplichte kenmerken en deduplicatietoetsen identificeren. Waarden in kenmerken die zijn gemarkeerd als &quot;Verplicht&quot; of &quot;Deduplication key&quot;, mogen niet null zijn.

   * [ Verplicht attributen ](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) zorgen ervoor dat alle profielverslagen de geselecteerde attributen(s) bevatten. Alle geëxporteerde profielen bevatten bijvoorbeeld een e-mailadres. De aanbeveling moet zowel het identiteitsveld als het als deduplicatietoets gebruikte veld verplicht stellen.
   * [ de deduplicatiesleutel van A ](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) is een primaire sleutel die de identiteit bepaalt waardoor de gebruikers hun profielen willen worden gededupliceerd.

     >[!IMPORTANT]
     >
     >Zorg ervoor dat de naam van het deduplicatietoetskenmerk overeenkomt met de kolomnaam van de geselecteerde doeltoewijzing.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. Nadat de toewijzing is uitgevoerd, kunt u de doelconfiguratie controleren en voltooien om te beginnen met het verzenden van gegevens naar **[!DNL Campaign]** .
   [ Leer hoe te om bestemmingsconfiguratie ](/help/destinations/destination-types.md#review) te herzien en te voltooien.

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Nadat een doel is geactiveerd, kunt u de bijbehorende taak openen en de gegevens exporteren in Campagne.

### Exporttaken voor gegevens controleren {#jobs}

Navigeer naar het menu **[!UICONTROL Administration]** > **[!UICONTROL Audit]** > **[!UICONTROL Audience load jobs]** om alle exporttaken te controleren die vanuit Adobe Experience Platform zijn geactiveerd.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### Geëxporteerde gegevens openen {#data}

Voor **[!UICONTROL Audience sync]** kunt u het geëxporteerde publiek controleren door naar het menu **[!UICONTROL Profile and target]** > **[!UICONTROL List]** > **[!UICONTROL AEP audiences]** te navigeren.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

Voor **[!UICONTROL Profile sync (Update only)]** worden gegevens automatisch bijgewerkt naar de Campagne-database voor elk profiel dat wordt geactiveerd door het publiek dat in de bestemming is geactiveerd.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).
