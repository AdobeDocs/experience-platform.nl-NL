---
title: Soorten publiek activeren om exportdoelen voor batchprofielen te gebruiken
type: Tutorial
description: Leer hoe u het publiek in Adobe Experience Platform activeert door het naar batchbestemmingen te sturen.
exl-id: 82ca9971-2685-453a-9e45-2001f0337cda
source-git-commit: d7a530c5ec2cad37b93273f5843609110d61cbfc
workflow-type: tm+mt
source-wordcount: '3909'
ht-degree: 0%

---


# Soorten publiek activeren om exportdoelen voor batchprofielen te gebruiken

>[!IMPORTANT]
> 
> * Om publiek te activeren en de [ toewijzingsstap ](#mapping) van het werkschema toe te laten, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig.
> * Om publiek te activeren zonder door de [ toewijzingsstap ](#mapping) van het werkschema te gaan, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}
> 
> Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

## Overzicht {#overview}

In dit artikel wordt uitgelegd welke workflow wordt vereist om het publiek in Adobe Experience Platform te activeren voor batchbestanddoelen, zoals cloudopslag en marketingdoelen voor e-mail.

## Vereisten {#prerequisites}

Om publiek aan bestemmingen te activeren, moet u met succes [ verbonden aan een bestemming ](./connect-destination.md) hebben. Als u dit niet reeds hebt gedaan, ga naar de [ bestemmingscatalogus ](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

## Ondersteunde bestandsindelingen voor export {#supported-file-formats-export}

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_header"
>title="De einddatum voor deze gegevensstroom bijwerken"
>abstract="De einddatum voor deze gegevensstroom bijwerken"

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_body"
>title="De einddatum voor deze gegevensstroominhoud bijwerken"
>abstract="Vanwege recente updates voor deze bestemming is voor de gegevensstroom nu een einddatum vereist. Adobe heeft een standaardeinddatum ingesteld op 1 maart 2025. Werk de gegevens bij naar de gewenste einddatum. Anders worden de gegevens niet meer geëxporteerd op de standaarddatum."

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template"
>title="Mappad bewerken"
>abstract="Gebruik verschillende beschikbare macro&#39;s om het mappad aan te passen waarin de gegevensset wordt geëxporteerd."

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template_preview"
>title="Padvoorvertoning gegevensmap"
>abstract="Bekijk een voorvertoning van de mapstructuur die op uw opslaglocatie wordt gemaakt op basis van de macro&#39;s die u in dit venster hebt toegevoegd."

De volgende bestandsindelingen worden ondersteund bij het exporteren van soorten publiek:

* CSV
* JSON
* Parquet

Houd er rekening mee dat u bij het exporteren van CSV-bestanden flexibeler kunt omgaan met de structuur die u aan geëxporteerde bestanden wilt geven. Lees meer over [ dossier het formatteren configuratie voor Csv- dossiers ](/help/destinations/ui/batch-destinations-file-formatting-options.md#file-configuration).

Selecteer uw gewenste dossierformaat voor de uitvoer wanneer [ creërend een verbinding aan de op dossier-gebaseerde bestemming ](/help/destinations/ui/connect-destination.md).

## Kies uw bestemming {#select-destination}

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteer de tab **[!UICONTROL Catalog]** .

   ![ Beeld die hoe te om aan de catalogus tabel van bestemmingen te krijgen benadrukt.](../assets/ui/activate-batch-profile-destinations/catalog-tab.png)

1. Selecteer **[!UICONTROL Activate audiences]** op de kaart die overeenkomt met het doel waarvoor u het publiek wilt activeren, zoals in de onderstaande afbeelding wordt getoond.

   ![ activeer publiek controle die in de cataloguspagina wordt benadrukt.](../assets/ui/activate-batch-profile-destinations/activate-audiences-button.png)

1. Selecteer de doelverbinding die u wilt gebruiken om uw publiek te activeren en selecteer vervolgens **[!UICONTROL Next]** .

   ![ Bevestigde vakjes benadrukte om één of veelvoudige bestemmingen te selecteren om publiek aan te activeren.](../assets/ui/activate-batch-profile-destinations/select-destination.png)

1. De beweging aan de volgende sectie aan [ selecteert uw publiek ](#select-audiences).

## Uw publiek selecteren {#select-audiences}

Als u het publiek dat u wilt activeren naar het doel wilt selecteren, gebruikt u de selectievakjes links van de publieksnamen en selecteert u vervolgens **[!UICONTROL Next]** .

U kunt kiezen uit meerdere soorten publiek, afhankelijk van de oorsprong:

* **[!UICONTROL Segmentation Service]**: publiek dat binnen Experience Platform door de Segmenteringsdienst wordt geproduceerd. Zie de [ segmentatiedocumentatie ](../../segmentation/ui/overview.md) voor meer details.
* **[!UICONTROL Custom upload]**: buiten het Experience Platform gegenereerde soorten publiek die als CSV-bestanden naar Platform worden geüpload. Meer over extern publiek leren, zie de documentatie bij [ het invoeren van een publiek ](../../segmentation/ui/audience-portal.md#import-audience).
* Andere soorten publiek, afkomstig van andere oplossingen voor Adobe, zoals [!DNL Audience Manager] .

![ getoonde Selectievakjes wanneer het selecteren van één of veelvoudige publiek om te activeren.](../assets/ui/activate-batch-profile-destinations/select-audiences.png)

>[!TIP]
>
>Het selecteren van publiek uit **[!UICONTROL Custom uploads]** laat automatisch de [ Uitgezochte verrijkingsattributen ](#select-enrichment-attributes) stap toe.

>[!TIP]
>
>U kunt soorten publiek verwijderen uit bestaande activeringsstromen van de pagina **[!UICONTROL Activation data]** . Zie de [ specifieke documentatie ](../ui/destination-details-page.md#bulk-remove) voor details.

## Het exporteren van publiek plannen {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_schedule"
>title="Schema"
>abstract="Gebruik het potloodpictogram om het bestandstype (volledige bestanden of incrementele bestanden) en de exportfrequentie in te stellen."

[!DNL Adobe Experience Platform] exporteert gegevens voor e-mailmarketing en de bestemmingen van de wolkenopslag als [ verschillende dossiertypes ](#supported-file-formats-export). Op de pagina **[!UICONTROL Scheduling]** kunt u het schema en de bestandsnamen configureren voor elk publiek dat u exporteert.

Experience Platform stelt automatisch een standaardschema in voor elke bestandsuitvoer. U kunt het standaardschema aan uw behoeften aanpassen, door het potloodpictogram naast elk programma te selecteren, en een douaneschema te bepalen.

![ geeft programmacontrole uit die in de Plannende stap wordt benadrukt.](../assets/ui/activate-batch-profile-destinations/edit-default-schedule.png)

>[!TIP]
>
>U kunt de activeringsschema&#39;s voor het publiek voor bestaande activeringsstromen bewerken via de pagina **[!UICONTROL Activation data]** . Zie de documentatie op [ bulkhet uitgeven activeringsprogramma&#39;s ](../ui/destination-details-page.md#bulk-edit-schedule) voor details.

>[!IMPORTANT]
>
>[!DNL Adobe Experience Platform] splitst de exportbestanden automatisch op 5 miljoen records (rijen) per bestand. Elke rij vertegenwoordigt één profiel.
>
>Namen van gesplitste bestanden worden toegevoegd met een getal dat aangeeft dat het bestand deel uitmaakt van een grotere exportbewerking: `filename.csv` , `filename_2.csv` , `filename_3.csv` .

### Volledige bestanden exporteren {#export-full-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_exportoptions"
>title="Exportopties voor bestanden"
>abstract="Selecteer **de Uitvoer volledige dossiers** om een volledige momentopname van alle profielen uit te voeren die voor het publiek kwalificeren. Selecteer **de Incrementele dossiers van de Uitvoer** om slechts de profielen uit te voeren die voor het publiek sinds de laatste uitvoer kwalificeerden. <br> De eerste incrementele bestandsuitvoer bevat alle profielen die in aanmerking komen voor het publiek en die fungeren als backfill. Toekomstige incrementele bestanden bevatten alleen de profielen die voor het publiek in aanmerking zijn gekomen sinds de eerste incrementele bestandsexport."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#export-incremental-files" text="Incrementele bestanden exporteren"

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_aftersegmentevaluation"
>title="Activeren na publieksevaluatie"
>abstract="De activering wordt onmiddellijk uitgevoerd nadat de dagelijkse segmentatietaak is voltooid. Zo weet u zeker dat de meest actuele profielen worden geëxporteerd."

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_scheduled"
>title="Geplande activering"
>abstract="De activering wordt uitgevoerd op een vast tijdstip van de dag."

Selecteer **[!UICONTROL Export full files]** om het exporteren van een bestand met een volledige opname van alle profielkwalificaties voor het geselecteerde publiek te starten.

![ Uitvoer volledige geselecteerde dossiers van een knevel.](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. Gebruik de kiezer **[!UICONTROL Frequency]** om de exportfrequentie te selecteren:

   * **[!UICONTROL Once]**: plant een eenmalige volledige bestandsexport.
   * **[!UICONTROL Daily]**: plant de volledige bestandsexport eenmaal per dag, elke dag, op het opgegeven tijdstip.

2. Gebruik de schakeloptie **[!UICONTROL Time]** om te bepalen of het exporteren direct na de publieksevaluatie of op een geplande basis op een bepaald tijdstip moet plaatsvinden. Wanneer u de optie **[!UICONTROL Scheduled]** selecteert, kunt u met de kiezer de tijd van de dag kiezen, in [!DNL UTC] -indeling, waarop het exporteren moet plaatsvinden.

   >[!NOTE]
   >
   >De hieronder beschreven optie **[!UICONTROL After segment evaluation]** is alleen beschikbaar voor bepaalde Beta-klanten.

   Gebruik de optie **[!UICONTROL After segment evaluation]** om de activeringstaak direct uit te voeren nadat de dagelijkse batchsegmentatietaak van het Platform is voltooid. Met deze optie zorgt u ervoor dat de meest actuele profielen naar uw bestemming worden geëxporteerd wanneer de activeringstaak wordt uitgevoerd.

   <!-- Batch segmentation currently runs at {{insert time of day}} and lasts for an average {{x hours}}. Adobe reserves the right to modify this schedule. -->

   ![ Beeld die de Latere optie van de segmentevaluatie in de activeringsstroom voor partijbestemmingen benadrukt.](../assets/ui/activate-batch-profile-destinations/after-segment-evaluation-option.png)
Gebruik de optie **[!UICONTROL Scheduled]** om de activeringstaak op een vast tijdstip uit te voeren. Met deze optie zorgt u ervoor dat gegevens in het profiel Experience Platform elke dag op hetzelfde tijdstip worden geëxporteerd. De profielen die u exporteert, zijn echter mogelijk niet de meest actuele, afhankelijk van het feit of de batchsegmentatietaak is voltooid voordat de activeringstaak wordt uitgeschakeld.

   ![ Beeld dat de Geplande optie in de activeringsstroom voor partijbestemmingen benadrukt en de tijdselecteur toont.](../assets/ui/activate-batch-profile-destinations/scheduled-option.png)

3. Gebruik de kiezer van **[!UICONTROL Date]** om de dag of het interval te kiezen waarop het exporteren moet plaatsvinden. Voor dagelijkse exportbewerkingen kunt u het beste uw begin- en einddatum instellen zodat deze aansluiten op de duur van uw campagnes op de downstreamplatforms.

   >[!IMPORTANT]
   >
   > Wanneer u een exportinterval selecteert, wordt de laatste dag van het interval niet in de exportbewerking opgenomen. Als u bijvoorbeeld een interval van 4-11 januari selecteert, wordt het laatste bestand op 10 januari geëxporteerd.

4. Selecteer **[!UICONTROL Create]** om het schema op te slaan.

### Incrementele bestanden exporteren

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_something"
>title="Bestandsnaam configureren"
>abstract="Voor op een bestand gebaseerde doelen wordt een unieke bestandsnaam per publiek gegenereerd. Met de bestandsnaameditor kunt u een unieke bestandsnaam maken en bewerken of de standaardnaam behouden."

Selecteer **[!UICONTROL Export incremental files]** om een exportbewerking te starten waarbij het eerste bestand een volledige opname is van alle profielkwalificaties voor het geselecteerde publiek en volgende bestanden zijn incrementele profielkwalificaties sinds de vorige exportbewerking.

>[!IMPORTANT]
>
>Het eerste geëxporteerde incrementele bestand bevat alle profielen die in aanmerking komen voor een publiek en die als backfill functioneren.

![ Uitvoer stijgende geselecteerde dossiers van een knevel.](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. Gebruik de kiezer **[!UICONTROL Frequency]** om de exportfrequentie te selecteren:

   * **[!UICONTROL Daily]**: plant de incrementele bestandsexport eenmaal per dag, elke dag, op het opgegeven tijdstip.
   * **[!UICONTROL Hourly]**: plant het incrementele exporteren van bestanden om de 3, 6, 8 of 12 uur.

2. Gebruik de kiezer van **[!UICONTROL Time]** om in [!DNL UTC] -indeling de tijd van de dag te kiezen waarop het exporteren moet plaatsvinden.

3. Gebruik de kiezer van **[!UICONTROL Date]** om het interval te kiezen waarin het exporteren moet plaatsvinden. De beste manier is om uw begin- en einddatum in te stellen op de duur van uw campagnes op uw downstreamplatforms.

   >[!IMPORTANT]
   >
   >De laatste dag van het interval wordt niet in de uitvoer opgenomen. Als u bijvoorbeeld een interval van 4-11 januari selecteert, wordt het laatste bestand op 10 januari geëxporteerd.

4. Selecteer **[!UICONTROL Create]** om het schema op te slaan.

### Bestandsnamen configureren

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_filename"
>title="Bestandsnaam configureren"
>abstract="Voor op een bestand gebaseerde doelen wordt een unieke bestandsnaam per publiek gegenereerd. Met de bestandsnaameditor kunt u een unieke bestandsnaam maken en bewerken of de standaardnaam behouden."

Voor de meeste bestemmingen, bestaan de standaarddossiernamen uit bestemmingsnaam, publiek-identiteitskaart, en een datum en tijdindicator. U kunt bijvoorbeeld uw geëxporteerde bestandsnamen bewerken om onderscheid te maken tussen verschillende campagnes of om de exporttijd van de gegevens aan de bestanden toe te voegen. Merk op dat sommige bestemmingsontwikkelaars zouden kunnen selecteren om verschillende standaard dossier te hebben toevoegt opties voor hun bestemmingen worden getoond.

Als u een modaal venster wilt openen en de bestandsnamen wilt bewerken, selecteert u het potloodpictogram. Bestandsnamen mogen maximaal 255 tekens bevatten.

>[!NOTE]
>
>In de onderstaande afbeelding ziet u hoe bestandsnamen kunnen worden bewerkt voor [!DNL Amazon S3] -doelen, maar het proces is identiek voor alle batchbestemmingen (bijvoorbeeld SFTP, [!DNL Azure Blob Storage] of [!DNL Google Cloud Storage] ).

![ Beeld dat het potloodpictogram benadrukt, dat wordt gebruikt om dossiernamen te vormen.](../assets/ui/activate-batch-profile-destinations/configure-name.png)

In de bestandsnaameditor kunt u verschillende componenten selecteren om aan de bestandsnaam toe te voegen.

![ Beeld dat alle beschikbare opties van de dossiernaam toont.](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

De doelnaam en de gebruikers-id kunnen niet uit bestandsnamen worden verwijderd. Naast deze opties kunt u de volgende opties toevoegen:

| Bestandsnaam, optie | Beschrijving |
|---------|----------|
| **[!UICONTROL Audience name]** | De naam van het geëxporteerde publiek. |
| **[!UICONTROL Date and time]** | U kunt kiezen tussen het toevoegen van een `MMDDYYYY_HHMMSS` -indeling of een UNIX 10-cijferig tijdstempel van het tijdstip waarop de bestanden worden gegenereerd. Kies een van deze opties als u voor de bestanden een dynamische bestandsnaam wilt genereren bij elke incrementele exportbewerking. |
| **[!UICONTROL Custom text]** | Alle aangepaste tekst die u aan de bestandsnamen wilt toevoegen. |
| **[!UICONTROL Destination ID]** | De id van de doelgegevensstroom die u gebruikt om het publiek te exporteren. |
| **[!UICONTROL Destination name]** | De naam van de bestemmingsgegevensstroom u gebruikt om het publiek uit te voeren. |
| **[!UICONTROL Organization name]** | Uw organisatienaam binnen Experience Platform. |
| **[!UICONTROL Sandbox name]** | De id van de sandbox die u gebruikt om het publiek te exporteren. |

{style="table-layout:auto"}

Selecteer **[!UICONTROL Apply changes]** om uw selectie te bevestigen.

>[!IMPORTANT]
> 
>Als u de component **[!UICONTROL Date and Time]** niet selecteert, zijn de bestandsnamen statisch en overschrijft het nieuwe geëxporteerde bestand het vorige bestand op uw opslaglocatie met elke exportbewerking. Als u een terugkerende importtaak uitvoert vanaf een opslaglocatie naar een e-mailmarketingplatform, is dit de aanbevolen optie.

Nadat u alle soorten publiek hebt geconfigureerd, selecteert u **[!UICONTROL Next]** om door te gaan.

## Toewijzing {#mapping}

In deze stap moet u de profielkenmerken selecteren die u wilt toevoegen aan de bestanden die naar de doelbestemming zijn geëxporteerd. Profielkenmerken en -identiteiten selecteren voor exporteren:

1. Selecteer **[!UICONTROL Add new mapping]** op de pagina **[!UICONTROL Mapping]** .

   ![ voeg nieuwe gebiedscontrole toe die in het toewijzingswerkschema wordt benadrukt.](../assets/ui/activate-batch-profile-destinations/add-new-field-mapping.png)

1. Selecteer de pijl rechts van de **[!UICONTROL Source field]** -vermelding.

   ![ Uitgezochte controle van het brongebied die in het toewijzingswerkschema wordt benadrukt.](../assets/ui/activate-batch-profile-destinations/select-source-field.png)

1. Selecteer op de pagina **[!UICONTROL Select source field]** de profielkenmerken en -identiteiten die u wilt opnemen in de geëxporteerde bestanden naar de bestemming en kies vervolgens **[!UICONTROL Select]** .

   >[!TIP]
   > 
   >U kunt het zoekveld gebruiken om de selectie te verkleinen, zoals in de onderstaande afbeelding wordt getoond.

   Met de schakeloptie **[!UICONTROL Show only fields with data]** kunt u alleen schemavelden weergeven die zijn gevuld met waarden. Standaard worden alleen gevulde schemavelden weergegeven.

   ![ Modal venster dat profielattributen toont die naar de bestemming kunnen worden uitgevoerd.](../assets/ui/activate-batch-profile-destinations/select-source-field-modal.png)


1. Het veld dat u hebt geselecteerd voor export, wordt nu weergegeven in de toewijzingsweergave. Desgewenst kunt u de naam van de koptekst in het geëxporteerde bestand bewerken. Selecteer hiertoe het pictogram in het doelveld.

   ![ Modal venster dat profielattributen toont die naar de bestemming kunnen worden uitgevoerd.](../assets/ui/activate-batch-profile-destinations/mapping-step-select-target-field.png)

1. Typ op de pagina **[!UICONTROL Select target field]** de gewenste naam van de koptekst in het geëxporteerde bestand en kies vervolgens **[!UICONTROL Select]** .

   ![ Modal venster dat een getypte - in vriendschappelijke naam voor een kopbal toont.](../assets/ui/activate-batch-profile-destinations/select-target-field-mapping.png)

1. Het veld dat u hebt geselecteerd voor export, verschijnt nu in de toewijzingsweergave en toont de bewerkte koptekst in het geëxporteerde bestand.

   ![ Modal venster dat profielattributen toont die naar de bestemming kunnen worden uitgevoerd.](../assets/ui/activate-batch-profile-destinations/select-target-field-updated.png)

1. (Optioneel) De volgorde van de toegewezen velden in de gebruikersinterface is afhankelijk van de volgorde van de kolommen in het geëxporteerde CSV-bestand, van boven naar beneden, waarbij de bovenste rij de meest linkse kolom in het CSV-bestand is. U kunt de volgorde van de toegewezen velden op elke gewenste manier wijzigen door de toewijzingsrijen te slepen en neer te zetten, zoals hieronder wordt weergegeven.

   >[!NOTE]
   >
   >Deze functie is in bètaversie beschikbaar voor bepaalde klanten. Neem contact op met uw Adobe als u toegang tot deze functie wilt aanvragen.

   ![ Opname die de afbeeldingsgebieden toont die door belemmering en daling opnieuw in volgorde worden geplaatst.](../assets/ui/activate-batch-profile-destinations/reorder-fields.gif)

1. (Optioneel) U kunt uw geëxporteerde veld selecteren om a [ verplichte sleutel ](#mandatory-keys) of a [ deduplicatietoets ](#deduplication-keys) te zijn.

   ![ Modal venster dat profielattributen toont die naar de bestemming kunnen worden uitgevoerd.](../assets/ui/activate-batch-profile-destinations/select-mandatory-deduplication-key.png)

1. Herhaal bovenstaande stappen om meer velden voor exporteren toe te voegen.

### Verplichte kenmerken {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="Verplichte kenmerken"
>abstract="Selecteer de XDM-schemakenmerken die alle geëxporteerde profielen moeten bevatten. Profielen zonder de verplichte sleutel worden niet naar de bestemming geëxporteerd. Als u geen verplichte sleutel selecteert, worden alle gekwalificeerde profielen niet geëxporteerd, ongeacht de kenmerken ervan."

Een verplicht kenmerk is een selectievakje dat door de gebruiker wordt ingeschakeld en dat ervoor zorgt dat alle profielrecords het geselecteerde kenmerk bevatten. Alle geëxporteerde profielen bevatten bijvoorbeeld een e-mailadres. &#x200B;

U kunt kenmerken als verplicht markeren om ervoor te zorgen dat [!DNL Platform] alleen de profielen exporteert die het specifieke kenmerk bevatten. Het resultaat is dat het kan worden gebruikt als extra filtermethode. Het merken van een attribuut als verplicht is **niet** vereist.

Als u geen verplicht kenmerk selecteert, worden alle gekwalificeerde profielen geëxporteerd, ongeacht de kenmerken ervan.

Men adviseert dat één van de attributen a [ uniek herkenningsteken ](../../destinations/catalog/email-marketing/overview.md#identity) van uw schema is. Voor meer informatie over verplichte attributen, zie de identiteitssectie in de [ E-mail marketing bestemmingen ](../../destinations/catalog/email-marketing/overview.md#identity) documentatie.

### Deduplicatietoetsen {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="Deduplicatietoetsen"
>abstract="U kunt meerdere records van hetzelfde profiel uit de exportbestanden verwijderen door een deduplicatietoets te selecteren. Selecteer één naamruimte of maximaal twee XDM-schemakenmerken als een deduplicatietoets. Als u geen deduplicatietoets selecteert, kan dit leiden tot dubbele profielvermeldingen in de exportbestanden."

Een deduplicatiesleutel is een door de gebruiker gedefinieerde primaire sleutel waarmee de identiteit wordt bepaald waarmee gebruikers hun profielen willen dedupliceren. &#x200B;

Deduplicatietoetsen maken het onmogelijk meerdere records van hetzelfde profiel in één exportbestand te hebben.

Er zijn drie manieren waarop u deduplicatietoetsen kunt gebruiken in [!DNL Platform] :

* Eén naamruimte voor identiteit gebruiken als een [!UICONTROL deduplication key]
* Eén profielkenmerk van een [!DNL XDM] -profiel gebruiken als [!UICONTROL deduplication key]
* Een combinatie van twee profielkenmerken van een [!DNL XDM] -profiel gebruiken als een samengestelde sleutel

>[!IMPORTANT]
>
> U kunt één naamruimte voor identiteit exporteren naar een doel en de naamruimte wordt automatisch ingesteld als deduplicatietoets. Het verzenden van meerdere naamruimten naar een doel wordt niet ondersteund.
> 
> U kunt geen combinatie van naamruimten en profielkenmerken gebruiken als deduplicatietoetsen.

### Voorbeeld van deduplicatie {#deduplication-example}

Dit voorbeeld illustreert hoe deduplicatie werkt, afhankelijk van de geselecteerde deduplicatietoetsen.

Laten we eens kijken naar de volgende twee profielen.

**Profiel A**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "doejohn_1@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "realized",
        "lastQualificationTime": "2021-03-10 10:03:08"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "Doe",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

**Profiel B**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_2@example.com"
      },
      {
        "id": "doejohn_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "realized",
        "lastQualificationTime": "2021-04-10 11:33:28"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "D",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

### Gebruiksscenario voor deduplicatie 1: geen deduplicatie {#deduplication-use-case-1}

Als u geen deduplicatie gebruikt, bevat het exportbestand de volgende items.

| PersonalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | Doe |
| johndoe@example.com | John | D |


### Gebruiksscenario voor deduplicatie 2: deduplicatie gebaseerd op naamruimte voor identiteit {#deduplication-use-case-2}

Als deduplicatie wordt verondersteld door de naamruimte [!DNL Email] , bevat het exportbestand de volgende items. Profiel B is het meest recente profiel dat in aanmerking komt voor het publiek. Het is dus de enige profiel dat wordt geëxporteerd.

| E-mail* | PersonalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_2@example.com | johndoe@example.com | John | D |
| doejohn_2@example.com | johndoe@example.com | John | D |

### Gebruiksscenario voor deduplicatie 3: deduplicatie op basis van één profielkenmerk {#deduplication-use-case-3}

Als deduplicatie wordt verondersteld door het kenmerk `personal Email` , bevat het exportbestand de volgende vermelding. Profiel B is het meest recente profiel dat in aanmerking komt voor het publiek. Het is dus de enige profiel dat wordt geëxporteerd.

| PersonalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | D |


### Gebruiksscenario deduplicatie 4: deduplicatie op basis van twee profielkenmerken {#deduplication-use-case-4}

Als deduplicatie wordt verondersteld met de samengestelde sleutel `personalEmail + lastName` , bevat het exportbestand de volgende items.

| PersonalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | John |
| johndoe@example.com | Doe | John |

Adobe raadt u aan een naamruimte voor identiteiten, zoals een [!DNL CRM ID] - of e-mailadres, te selecteren als deduplicatietoets om ervoor te zorgen dat alle profielrecords op unieke wijze worden geïdentificeerd.

>[!NOTE]
> 
>Als er labels voor gegevensgebruik zijn toegepast op bepaalde velden in een gegevensset (in plaats van op de gehele gegevensset), wordt de toepassing van die labels op veldniveau bij activering uitgevoerd onder de volgende voorwaarden:
>
>* De velden worden gebruikt in de definitie van het publiek.
>* De velden worden geconfigureerd als geprojecteerde kenmerken voor de doelbestemming.
>
> Als het veld `person.name.firstName` bijvoorbeeld bepaalde labels voor gegevensgebruik heeft die conflicteren met de marketingactie van de bestemming, wordt in de revisiestap een schending van het gegevensgebruiksbeleid weergegeven. Voor meer informatie, zie [ de Governance van Gegevens in Adobe Experience Platform ](../../rtcdp/privacy/data-governance-overview.md#destinations).

### [!BADGE  Beta ] {type=Informative} de series van de Uitvoer door berekende gebieden {#export-arrays-calculated-fields}

Selecteer bèta-klanten kunnen arrayobjecten van Experience Platform naar cloudopslagdoelen exporteren. Lees meer over [ het uitvoeren van series en berekende gebieden ](/help/destinations/ui/export-arrays-calculated-fields.md) en contacteer uw vertegenwoordiger van de Adobe om toegang tot de functionaliteit te krijgen.

### Bekende beperkingen {#known-limitations}

De nieuwe **[!UICONTROL Mapping]** pagina heeft de volgende bekende beperkingen:

#### Het kenmerk Publiek-lidmaatschap kan niet worden geselecteerd via de toewijzingsworkflow

Vanwege een bekende beperking kunt u momenteel het venster **[!UICONTROL Select field]** niet gebruiken om `segmentMembership.seg_namespace.seg_id.status` toe te voegen aan het exporteren van bestanden. In plaats daarvan moet u de waarde `xdm: segmentMembership.seg_namespace.seg_id.status` handmatig in het schemaveld plakken, zoals hieronder wordt weergegeven.

![ opname die van het Scherm de werkruimte van het publiekslidmaatschap in de afbeeldingsstap van het activeringswerkschema toont.](../assets/ui/activate-batch-profile-destinations/segment-membership-mapping-step.gif)


>[!NOTE]
>
Voor de bestemmingen van de wolkenopslag, worden de volgende attributen toegevoegd aan de afbeelding door gebrek:
>
* `segmentMembership.seg_namespace.seg_id.status`
* `segmentMembership.seg_namespace.seg_id.lastQualificationTime`

Het exporteren van bestanden kan op de volgende manieren variëren, afhankelijk van het feit of `segmentMembership.seg_namespace.seg_id.status` is geselecteerd:

* Als het veld `segmentMembership.seg_namespace.seg_id.status` is geselecteerd, bevatten geëxporteerde bestanden **[!UICONTROL Active]** leden in de eerste volledige momentopname en nieuwe **[!UICONTROL Active]** en **[!UICONTROL Expired]** leden in volgende incrementele exportbewerkingen.
* Als het veld `segmentMembership.seg_namespace.seg_id.status` niet is geselecteerd, bevatten geëxporteerde bestanden alleen **[!UICONTROL Active]** -leden in de eerste volledige momentopname en in volgende incrementele exportbewerkingen.

Lees meer over [ het gedrag van de profieluitvoer voor op dossier-gebaseerde bestemmingen ](/help/destinations/how-destinations-work/profile-export-behavior.md#file-based-destinations).

#### Naamruimten kunnen momenteel niet worden geselecteerd voor exporteren

Het selecteren van naamruimten voor exporteren, zoals wordt weergegeven in de onderstaande afbeelding, wordt momenteel niet ondersteund. Als u naamruimten selecteert die u wilt exporteren, wordt een foutbericht weergegeven in de stap **[!UICONTROL Review]** .

![ niet gestaafde afbeelding die identiteitsuitvoer tonen.](../assets/ui/activate-batch-profile-destinations/unsupported-identity-mapping.png)

Als tijdelijke oplossing kunt u:
* Gebruik de oude opslagdoelen van de cloud voor de dataflows waar u naamruimten wilt opnemen in de exportbewerkingen
* Upload identiteiten als attributen in Experience Platform, dan voer hen naar uw bestemmingen van de wolkenopslag uit.

## Profielkenmerken selecteren {#select-attributes}

>[!IMPORTANT]
> 
Alle bestemmingen voor cloudopslag in de catalogus kunnen een verbeterde [[!UICONTROL Mapping] stap ](#mapping) weergeven die de stap **[!UICONTROL Select attributes]** vervangt die in deze sectie wordt beschreven.
>
Deze **[!UICONTROL Select attributes]** stap wordt nog getoond voor de e-mailmarketingbestemmingen van Adobe Campaign, Oracle Responsys, Oracle Eloqua en Salesforce Marketing Cloud.

Voor op profiel gebaseerde bestemmingen, moet u de profielattributen selecteren die u naar de doelbestemming wilt verzenden.

1. Selecteer **[!UICONTROL Add new field]** op de pagina **[!UICONTROL Select attributes]** .

   ![ Beeld die de Add nieuwe gebiedsknoop benadrukt.](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

2. Selecteer de pijl rechts van de **[!UICONTROL Schema field]** -vermelding.

   ![ Beeld die hoe te om een brongebied benadrukken te selecteren.](../assets/ui/activate-batch-profile-destinations/select-source-field.png)

3. Selecteer op de pagina **[!UICONTROL Select field]** de XDM-kenmerken of naamruimten die u naar het doel wilt verzenden en kies vervolgens **[!UICONTROL Select]** .

   ![ Beeld die de diverse gebieden tonen beschikbaar als brongebieden.](../assets/ui/activate-batch-profile-destinations/target-field-page.png)

4. Herhaal stap 1 tot en met 3 om meer toewijzingen toe te voegen.

>[!NOTE]
>
Adobe Experience Platform vult uw selectie voor met vier aanbevolen, veelgebruikte kenmerken uit uw schema: `person.name.firstName` , `person.name.lastName` , `personalEmail.address` , `segmentMembership.seg_namespace.seg_id.status` .

![ Beeld dat vooraf ingevulde geadviseerde attributen in de afbeeldingsstap van het werkschema van de publiekactivering toont.](../assets/ui/activate-batch-profile-destinations/prefilled-fields.png)

>[!IMPORTANT]
>
Vanwege een bekende beperking kunt u momenteel het venster **[!UICONTROL Select field]** niet gebruiken om `segmentMembership.seg_namespace.seg_id.status` toe te voegen aan het exporteren van bestanden. In plaats daarvan moet u de waarde `xdm: segmentMembership.seg_namespace.seg_id.status` handmatig in het schemaveld plakken, zoals hieronder wordt weergegeven.
>
![ opname die van het Scherm de werkruimte van het publiekslidmaatschap in de afbeeldingsstap van het activeringswerkschema toont.](..//assets/ui/activate-batch-profile-destinations/segment-membership.gif)

Het exporteren van bestanden kan op de volgende manieren variëren, afhankelijk van het feit of `segmentMembership.seg_namespace.seg_id.status` is geselecteerd:
* Als het veld `segmentMembership.seg_namespace.seg_id.status` is geselecteerd, bevatten geëxporteerde bestanden **[!UICONTROL Active]** leden in de eerste volledige momentopname en **[!UICONTROL Active]** en **[!UICONTROL Expired]** leden in volgende incrementele exportbewerkingen.
* Als het veld `segmentMembership.seg_namespace.seg_id.status` niet is geselecteerd, bevatten geëxporteerde bestanden alleen **[!UICONTROL Active]** -leden in de eerste volledige momentopname en in volgende incrementele exportbewerkingen.

## Verrijkingskenmerken selecteren {#select-enrichment-attributes}

[!CONTEXTUALHELP]
id="platform_destinations_activate_exclude_enrichment_attributes"
title="Verrijkingskenmerken uitsluiten"
abstract="Schakel deze optie in om de profielen van het geselecteerde aangepaste geüploade publiek naar uw bestemming te exporteren, zonder alle kenmerken ervan uit te sluiten."

>[!IMPORTANT]
>
Deze stap wordt getoond slechts als u **[!UICONTROL Custom upload]** publiek tijdens de [ stap van de publieksselectie ](#select-audiences) selecteerde.

Verrijkingskenmerken komen overeen met het aangepaste geüploade publiek dat in het Experience Platform wordt opgenomen als **[!UICONTROL Custom uploads]** . In deze stap kunt u voor elk geselecteerd extern publiek selecteren welke kenmerken u wilt exporteren naar uw doel.

![ beeld UI die de de selectiestap van de verrijkingsattributen toont.](../assets/ui/activate-batch-profile-destinations/select-enrichment-attributes-step.png)

Voer de onderstaande stappen uit om verrijkingskenmerken voor elk extern publiek te selecteren:

1. In de **[!UICONTROL Enrichment attributes]** kolom, selecteer ![ uitgeven knoop ](/help/images/icons/edit.png) (geef uit) knoop.
1. Selecteer **[!UICONTROL Add enrichment attribute]**. Er wordt een nieuw leeg schemaveld weergegeven.
   ![ beeld UI die het verrijkingsattributen modaal scherm tonen.](../assets/ui/activate-batch-profile-destinations/add-enrichment-attribute.png)
1. Selecteer de knop rechts van het lege veld om het selectiescherm van het veld te openen.
1. Selecteer de kenmerken die u voor het publiek wilt exporteren.
   ![ beeld UI die de lijst van de verrijkingsattributen toont.](../assets/ui/activate-batch-profile-destinations/select-enrichment-attributes.png)
1. Nadat u alle kenmerken hebt toegevoegd die u wilt exporteren, selecteert u **[!UICONTROL Save and close]** .
1. Herhaal deze stappen voor elk extern publiek.

Als u een extern publiek naar uw doelen wilt activeren zonder kenmerken te exporteren, schakelt u de schakeloptie **[!UICONTROL Exclude enrichment attributes]** in. Met deze optie exporteert u de profielen van het externe publiek, maar de bijbehorende kenmerken worden niet naar uw bestemming verzonden.

{het beeld van 0} UI die de knoop toont van de attributen van de exclusief verrijking.](../assets/ui/activate-batch-profile-destinations/exclude-enrichment-attributes.png)![

Selecteer **[!UICONTROL Next]** om aan de [ 2} stap van het Overzicht {te bewegen.](#review)

## Controleren {#review}

Op de pagina **[!UICONTROL Review]** ziet u een overzicht van uw selectie. Selecteer **[!UICONTROL Cancel]** om de stroom te verbreken, **[!UICONTROL Back]** om uw instellingen te wijzigen of **[!UICONTROL Finish]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

![ Samenvatting van de Selectie die in de overzichtsstap wordt getoond.](../assets/ui/activate-batch-profile-destinations/review.png)

### Goedkeuring van het beleid {#consent-policy-evaluation}

[!CONTEXTUALHELP]
id="platform_governance_policies_viewApplicableConsentPolicies"
title="Toepasselijk toestemmingsbeleid weergeven"
abstract="Als uw organisatie **het Schild van de Gezondheidszorg van de Adobe** of **de Privacy &amp; het Schild van de Veiligheid van de Adobe** kocht, selecteer **[!UICONTROL View applicable consent policies]** om te zien welk toestemmingsbeleid wordt toegepast en hoeveel profielen in de activering als resultaat van hen inbegrepen zijn. Deze controle is gehandicapt als uw bedrijf geen toegang tot hierboven vermelde SKUs heeft."

Als uw organisatie **het Schild van de Gezondheidszorg van de Adobe** of **de Privacy &amp; het Schild van de Veiligheid van de Adobe** kocht, selecteer **[!UICONTROL View applicable consent policies]** om te zien welk toestemmingsbeleid wordt toegepast en hoeveel profielen in de activering als resultaat van hen inbegrepen zijn. Lees over [ evaluatie van het toestemmingsbeleid ](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) voor meer informatie.

### Controle van het gegevensgebruiksbeleid {#data-usage-policy-checks}

In de stap **[!UICONTROL Review]** controleert het Experience Platform ook op overtredingen van het gegevensgebruiksbeleid. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor publieksactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe te om beleidsschendingen op te lossen, lees over [ schendingen van het beleid van het gegevensgebruik ](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) in de de documentatiesectie van het gegevensbeheer.

![ een voorbeeld van de de schending van het gegevensbeleid van A in het activeringswerkschema wordt getoond.](../assets/common/data-policy-violation.png)

### Filter publiek {#filter-audiences}

In deze stap kunt u ook de beschikbare filters op de pagina gebruiken om alleen de doelgroepen weer te geven waarvan het schema of de toewijzing is bijgewerkt als onderdeel van deze workflow. U kunt ook schakelen welke tabelkolommen u wilt zien.

![ opname die van het Scherm de beschikbare publieksfilters in de overzichtsstap toont.](../assets/ui/activate-batch-profile-destinations/filter-audiences-batch-review.gif)

Als u tevreden bent met de selectie en er zijn geen beleidsovertredingen vastgesteld, selecteert u **[!UICONTROL Finish]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

## Activering van publiek controleren {#verify}

Bij het exporteren van soorten publiek naar opslaglocaties in de cloud maakt Adobe Experience Platform een bestand `.csv` , `.json` of `.parquet` in de opslaglocatie die u hebt opgegeven. Er wordt een nieuw bestand verwacht dat op uw opslaglocatie wordt gemaakt volgens het schema dat u instelt in de workflow. Het standaarddossierformaat wordt getoond hieronder, maar u kunt [ de componenten van het dossier uitgeven - naam ](#file-names):
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

Als u bijvoorbeeld een dagelijkse exportfrequentie selecteert, kunnen de bestanden die u op drie opeenvolgende dagen ontvangt er als volgt uitzien:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

De aanwezigheid van deze bestanden op de opslaglocatie bevestigt dat de activering is gelukt. Om te begrijpen hoe de uitgevoerde dossiers gestructureerd zijn, kunt u [ een steekproef.csv- dossier ](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv) downloaden. Dit voorbeeldbestand bevat de profielkenmerken `person.firstname` , `person.lastname` , `person.gender` , `person.birthyear` en `personalEmail.address` .
