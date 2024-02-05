---
title: Soorten publiek activeren om exportdoelen voor batchprofielen te gebruiken
type: Tutorial
description: Leer hoe u het publiek in Adobe Experience Platform activeert door het naar batchbestemmingen te sturen.
exl-id: 82ca9971-2685-453a-9e45-2001f0337cda
source-git-commit: a66c4397a02da81e4b3304f3bc975f725f8f8d76
workflow-type: tm+mt
source-wordcount: '3636'
ht-degree: 0%

---


# Soorten publiek activeren om exportdoelen voor batchprofielen te gebruiken

>[!IMPORTANT]
> 
> * Om het publiek te activeren en het [toewijzingsstap](#mapping) van de workflow hebt u de **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions).
> * Om het publiek te activeren zonder door [toewijzingsstap](#mapping) van de workflow hebt u de **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions).
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}
> 
> Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

## Overzicht {#overview}

In dit artikel wordt uitgelegd welke workflow wordt vereist om het publiek in Adobe Experience Platform te activeren voor batchbestanddoelen, zoals cloudopslag en marketingdoelen voor e-mail.

## Vereisten {#prerequisites}

Als u een publiek naar een bestemming wilt activeren, moet u [verbonden met een bestemming](./connect-destination.md). Als u dat nog niet hebt gedaan, gaat u naar de [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

## Ondersteunde bestandsindelingen voor export {#supported-file-formats-export}

De volgende bestandsindelingen worden ondersteund bij het exporteren van soorten publiek:

* CSV
* JSON
* Parquet

Houd er rekening mee dat u bij het exporteren van CSV-bestanden flexibeler kunt omgaan met de structuur die u aan geëxporteerde bestanden wilt geven. Meer informatie over [bestandsindelingconfiguratie voor CSV-bestanden](/help/destinations/ui/batch-destinations-file-formatting-options.md#file-configuration).

Selecteer de gewenste bestandsindeling voor het exporteren wanneer [verbinding maken met het doel dat op een bestand is gebaseerd](/help/destinations/ui/connect-destination.md).

## Kies uw bestemming {#select-destination}

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab.

   ![Afbeelding die aangeeft hoe u het tabblad Doelcatalogus kunt openen.](../assets/ui/activate-batch-profile-destinations/catalog-tab.png)

1. Selecteren **[!UICONTROL Activate audiences]** op de kaart die overeenkomt met de bestemming waar u uw publiek wilt activeren, zoals in de onderstaande afbeelding wordt getoond.

   ![Activeer de besturingselementen voor doelgroepen die in de cataloguspagina zijn gemarkeerd.](../assets/ui/activate-batch-profile-destinations/activate-audiences-button.png)

1. Selecteer de doelverbinding die u wilt gebruiken om uw publiek te activeren en selecteer vervolgens **[!UICONTROL Next]**.

   ![Selectievakjes gemarkeerd om een of meerdere doelen te selecteren waarnaar het publiek moet worden geactiveerd.](../assets/ui/activate-batch-profile-destinations/select-destination.png)

1. Naar de volgende sectie gaan [uw publiek selecteren](#select-audiences).

## Uw publiek selecteren {#select-audiences}

Als u het publiek dat u wilt activeren naar het doel wilt selecteren, schakelt u het selectievakje links van de publieksnamen in en selecteert u **[!UICONTROL Next]**.

U kunt kiezen uit meerdere soorten publiek, afhankelijk van de oorsprong:

* **[!UICONTROL Segmentation Service]**: publiek dat binnen Experience Platform door de Dienst van de Segmentatie wordt geproduceerd. Zie de [segmentatiedocumentatie](../../segmentation/ui/overview.md) voor meer informatie .
* **[!UICONTROL Custom upload]**: Soorten publiek dat buiten het Experience Platform is gegenereerd en als CSV-bestanden naar Platform is geüpload. Raadpleeg de documentatie over [een publiek importeren](../../segmentation/ui/overview.md#import-audience).
* Andere soorten soorten publiek, afkomstig van andere oplossingen voor Adobe, zoals [!DNL Audience Manager].

![Selectievakjes worden weergegeven wanneer u een of meer soorten publiek selecteert om te activeren.](../assets/ui/activate-batch-profile-destinations/select-audiences.png)

>[!TIP]
>
>Soorten publiek selecteren afkomstig van **[!UICONTROL Custom uploads]** schakelt automatisch de [Verrijkingskenmerken selecteren](#select-enrichment-attributes) stap.

## Het exporteren van publiek plannen {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_schedule"
>title="Schema"
>abstract="Gebruik het potloodpictogram om het bestandstype (volledige bestanden of incrementele bestanden) en de exportfrequentie in te stellen."

[!DNL Adobe Experience Platform] exporteert gegevens voor e-mailmarketing en cloudopslagdoelen als [verschillende bestandstypen](#supported-file-formats-export). In de **[!UICONTROL Scheduling]** pagina, kunt u het programma en de dossiernamen voor elk publiek vormen u uitvoert. Het is verplicht het schema te configureren, maar het configureren van de bestandsnaam is optioneel.

>[!IMPORTANT]
>
>[!DNL Adobe Experience Platform] Hiermee worden de exportbestanden automatisch gesplitst op 5 miljoen records (rijen) per bestand. Elke rij vertegenwoordigt één profiel.
>
>Namen van gesplitste bestanden worden toegevoegd met een getal dat aangeeft dat het bestand deel uitmaakt van een grotere exportbewerking, als zodanig: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

Selecteer de **[!UICONTROL Create schedule]** controle die aan het publiek beantwoordt dat u naar uw bestemming wilt verzenden.

![Creeer planningscontrole die in de Plannende stap wordt benadrukt.](../assets/ui/activate-batch-profile-destinations/create-schedule-button.png)

### Volledige bestanden exporteren {#export-full-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_exportoptions"
>title="Exportopties voor bestanden"
>abstract="Selecteren **Volledige bestanden exporteren** om een volledige momentopname van alle profielen te exporteren die voor het publiek in aanmerking komen. Selecteren **Incrementele bestanden exporteren** om alleen de profielen te exporteren die voor het publiek in aanmerking zijn gekomen sinds de laatste exportbewerking. <br> Het eerste incrementele exportbestand bevat alle profielen die in aanmerking komen voor het publiek en die fungeren als backfill. Toekomstige incrementele bestanden bevatten alleen de profielen die voor het publiek in aanmerking zijn gekomen sinds de eerste incrementele bestandsexport."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#export-incremental-files" text="Incrementele bestanden exporteren"

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_aftersegmentevaluation"
>title="Activeren na publieksevaluatie"
>abstract="De activering wordt onmiddellijk uitgevoerd nadat de dagelijkse segmentatietaak is voltooid. Zo weet u zeker dat de meest actuele profielen worden geëxporteerd."

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_scheduled"
>title="Geplande activering"
>abstract="De activering wordt uitgevoerd op een vast tijdstip van de dag."

Selecteren **[!UICONTROL Export full files]** om het exporteren van een bestand met een volledige opname van alle profielkwalificaties voor het geselecteerde publiek te activeren.

![Selectie voor het exporteren van volledige bestanden.](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. Gebruik de **[!UICONTROL Frequency]** om de exportfrequentie te selecteren:

   * **[!UICONTROL Once]**: plant een eenmalige, volledige bestandsexport.
   * **[!UICONTROL Daily]**: Plan de volledige bestandsexport eenmaal per dag, elke dag, op het opgegeven tijdstip.

2. Gebruik de **[!UICONTROL Time]** om te selecteren of de uitvoer onmiddellijk na publieksevaluatie of op een geplande basis, op een gespecificeerde tijd zou moeten gebeuren. Wanneer u de **[!UICONTROL Scheduled]** kunt u met de kiezer de tijd van de dag kiezen, in [!DNL UTC] formaat, wanneer het exporteren moet plaatsvinden.

   >[!NOTE]
   >
   >De **[!UICONTROL After segment evaluation]** hieronder beschreven optie is alleen beschikbaar voor het selecteren van bèta-klanten.

   Gebruik de **[!UICONTROL After segment evaluation]** optie om de activeringstaak onmiddellijk uit te voeren nadat de dagelijkse batchsegmentatietaak van het Platform is voltooid. Met deze optie zorgt u ervoor dat de meest actuele profielen naar uw bestemming worden geëxporteerd wanneer de activeringstaak wordt uitgevoerd.

   <!-- Batch segmentation currently runs at {{insert time of day}} and lasts for an average {{x hours}}. Adobe reserves the right to modify this schedule. -->

   ![Afbeelding die de evaluatieoptie Na-segment markeert in de activeringsstroom voor batchbestemmingen.](../assets/ui/activate-batch-profile-destinations/after-segment-evaluation-option.png)
Gebruik de **[!UICONTROL Scheduled]** om de activeringstaak op een vast tijdstip te laten uitvoeren. Met deze optie zorgt u ervoor dat gegevens in het profiel Experience Platform elke dag op hetzelfde tijdstip worden geëxporteerd. De profielen die u exporteert, zijn echter mogelijk niet de meest actuele, afhankelijk van het feit of de batchsegmentatietaak is voltooid voordat de activeringstaak wordt uitgeschakeld.

   ![Afbeelding die de optie Scheduled markeert in de activeringsstroom voor batchbestemmingen en die de tijdkiezer weergeeft.](../assets/ui/activate-batch-profile-destinations/scheduled-option.png)

3. Gebruik de **[!UICONTROL Date]** om de dag of het interval te kiezen waarop het exporteren moet plaatsvinden. Voor dagelijkse exportbewerkingen kunt u het beste uw begin- en einddatum instellen zodat deze aansluiten op de duur van uw campagnes op de downstreamplatforms.

   >[!IMPORTANT]
   >
   > Wanneer u een exportinterval selecteert, wordt de laatste dag van het interval niet in de exportbewerking opgenomen. Als u bijvoorbeeld een interval van 4-11 januari selecteert, wordt het laatste bestand op 10 januari geëxporteerd.

4. Selecteren **[!UICONTROL Create]** om het programma op te slaan.

### Incrementele bestanden exporteren

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_something"
>title="Bestandsnaam configureren"
>abstract="Voor op een bestand gebaseerde doelen wordt een unieke bestandsnaam per publiek gegenereerd. Met de bestandsnaameditor kunt u een unieke bestandsnaam maken en bewerken of de standaardnaam behouden."

Selecteren **[!UICONTROL Export incremental files]** om een exportbewerking te activeren waarbij het eerste bestand een volledige momentopname is van alle profielkwalificaties voor het geselecteerde publiek, en volgende bestanden zijn incrementele profielkwalificaties sinds de vorige exportbewerking.

>[!IMPORTANT]
>
>Het eerste geëxporteerde incrementele bestand bevat alle profielen die in aanmerking komen voor een publiek en die als backfill functioneren.

![Selectie voor het exporteren van incrementele bestanden.](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. Gebruik de **[!UICONTROL Frequency]** om de exportfrequentie te selecteren:

   * **[!UICONTROL Daily]**: plant de incrementele bestandsuitvoer eenmaal per dag, elke dag, op het door u opgegeven tijdstip.
   * **[!UICONTROL Hourly]**: schema incrementele het dossieruitvoer om de 3, 6, 8, of 12 uur.

2. Gebruik de **[!UICONTROL Time]** om de tijd van de dag te kiezen, in [!DNL UTC] formaat, wanneer het exporteren moet plaatsvinden.

3. Gebruik de **[!UICONTROL Date]** om het interval te kiezen waarin het exporteren moet plaatsvinden. De beste manier is om uw begin- en einddatum in te stellen op de duur van uw campagnes op uw downstreamplatforms.

   >[!IMPORTANT]
   >
   >De laatste dag van het interval wordt niet in de uitvoer opgenomen. Als u bijvoorbeeld een interval van 4-11 januari selecteert, wordt het laatste bestand op 10 januari geëxporteerd.

4. Selecteren **[!UICONTROL Create]** om het programma op te slaan.

### Bestandsnamen configureren

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_filename"
>title="Bestandsnaam configureren"
>abstract="Voor op een bestand gebaseerde doelen wordt een unieke bestandsnaam per publiek gegenereerd. Met de bestandsnaameditor kunt u een unieke bestandsnaam maken en bewerken of de standaardnaam behouden."

Voor de meeste bestemmingen, bestaan de standaarddossiernamen uit bestemmingsnaam, publiek-identiteitskaart, en een datum en tijdindicator. U kunt bijvoorbeeld uw geëxporteerde bestandsnamen bewerken om onderscheid te maken tussen verschillende campagnes of om de exporttijd van de gegevens aan de bestanden toe te voegen. Merk op dat sommige bestemmingsontwikkelaars zouden kunnen selecteren om verschillende standaard dossier te hebben toevoegt opties voor hun bestemmingen worden getoond.

Als u een modaal venster wilt openen en de bestandsnamen wilt bewerken, selecteert u het potloodpictogram. Bestandsnamen mogen maximaal 255 tekens bevatten.

>[!NOTE]
>
>In de onderstaande afbeelding ziet u hoe bestandsnamen kunnen worden bewerkt voor [!DNL Amazon S3] bestemmingen maar het proces is identiek voor alle batchbestemmingen (bijvoorbeeld SFTP); [!DNL Azure Blob Storage], of [!DNL Google Cloud Storage]).

![Afbeelding die het potloodpictogram markeert. Hiermee worden bestandsnamen geconfigureerd.](../assets/ui/activate-batch-profile-destinations/configure-name.png)

In de bestandsnaameditor kunt u verschillende componenten selecteren om aan de bestandsnaam toe te voegen.

![Afbeelding met alle beschikbare opties voor de bestandsnaam.](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

De doelnaam en de gebruikers-id kunnen niet uit bestandsnamen worden verwijderd. Naast deze opties kunt u de volgende opties toevoegen:

| Bestandsnaam, optie | Beschrijving |
|---------|----------|
| **[!UICONTROL Audience name]** | De naam van het geëxporteerde publiek. |
| **[!UICONTROL Date and time]** | Selecteer tussen het toevoegen van een `MMDDYYYY_HHMMSS` gebruiken of een UNIX 10-cijferig tijdstempel van de tijd waarop de bestanden worden gegenereerd. Kies een van deze opties als u voor de bestanden een dynamische bestandsnaam wilt genereren bij elke incrementele exportbewerking. |
| **[!UICONTROL Custom text]** | Alle aangepaste tekst die u aan de bestandsnamen wilt toevoegen. |
| **[!UICONTROL Destination ID]** | De id van de doelgegevensstroom die u gebruikt om het publiek te exporteren. |
| **[!UICONTROL Destination name]** | De naam van de bestemmingsgegevensstroom u gebruikt om het publiek uit te voeren. |
| **[!UICONTROL Organization name]** | Uw organisatienaam binnen Experience Platform. |
| **[!UICONTROL Sandbox name]** | De id van de sandbox die u gebruikt om het publiek te exporteren. |

{style="table-layout:auto"}

Selecteren **[!UICONTROL Apply changes]** om uw selectie te bevestigen.

>[!IMPORTANT]
> 
>Als u de optie **[!UICONTROL Date and Time]** de bestandsnamen statisch zijn en het nieuwe geëxporteerde bestand overschrijft het vorige bestand in uw opslaglocatie met elke exportbewerking. Als u een terugkerende importtaak uitvoert vanaf een opslaglocatie naar een e-mailmarketingplatform, is dit de aanbevolen optie.

Nadat u alle soorten publiek hebt geconfigureerd, selecteert u **[!UICONTROL Next]** om door te gaan.

## Toewijzing {#mapping}

In deze stap moet u de profielkenmerken selecteren die u wilt toevoegen aan de bestanden die naar de doelbestemming zijn geëxporteerd. Profielkenmerken en -identiteiten selecteren voor exporteren:

1. In de **[!UICONTROL Mapping]** pagina, selecteert u **[!UICONTROL Add new mapping]**.

   ![Voeg nieuwe gebiedscontrole toe die in het kaartwerkschema wordt benadrukt.](../assets/ui/activate-batch-profile-destinations/add-new-field-mapping.png)

1. Selecteer de pijl rechts van de knop **[!UICONTROL Source field]** vermelding.

   ![Selecteer controle van brongebied die in het kaartwerkschema wordt benadrukt.](../assets/ui/activate-batch-profile-destinations/select-source-field.png)

1. In de **[!UICONTROL Select source field]** pagina, selecteert u de profielkenmerken en -identiteiten die u wilt opnemen in de geëxporteerde bestanden naar de bestemming en kiest u **[!UICONTROL Select]**.

   >[!TIP]
   > 
   >U kunt het zoekveld gebruiken om de selectie te verkleinen, zoals in de onderstaande afbeelding wordt getoond.

   ![Modal venster met profielkenmerken die kunnen worden geëxporteerd naar de bestemming.](../assets/ui/activate-batch-profile-destinations/select-source-field-modal.png)


1. Het veld dat u hebt geselecteerd voor export, wordt nu weergegeven in de toewijzingsweergave. Desgewenst kunt u de naam van de koptekst in het geëxporteerde bestand bewerken. Selecteer hiertoe het pictogram in het doelveld.

   ![Modal venster met profielkenmerken die kunnen worden geëxporteerd naar de bestemming.](../assets/ui/activate-batch-profile-destinations/mapping-step-select-target-field.png)

1. In de **[!UICONTROL Select target field]** pagina, typt u de gewenste naam van de koptekst in het geëxporteerde bestand en kiest u **[!UICONTROL Select]**.

   ![Het modulaire venster dat een typed-binnen vriendschappelijke naam voor een kopbal toont.](../assets/ui/activate-batch-profile-destinations/select-target-field-mapping.png)

1. Het veld dat u hebt geselecteerd voor export, verschijnt nu in de toewijzingsweergave en toont de bewerkte koptekst in het geëxporteerde bestand.

   ![Modal venster met profielkenmerken die kunnen worden geëxporteerd naar de bestemming.](../assets/ui/activate-batch-profile-destinations/select-target-field-updated.png)

1. (Optioneel) U kunt het geëxporteerde veld selecteren als een [verplichte sleutel](#mandatory-keys) of [deduplicatie-sleutel](#deduplication-keys).

   ![Modal venster met profielkenmerken die kunnen worden geëxporteerd naar de bestemming.](../assets/ui/activate-batch-profile-destinations/select-mandatory-deduplication-key.png)

1. Herhaal bovenstaande stappen om meer velden voor exporteren toe te voegen.

### Verplichte kenmerken {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="Verplichte kenmerken"
>abstract="Selecteer de XDM-schemakenmerken die alle geëxporteerde profielen moeten bevatten. Profielen zonder de verplichte sleutel worden niet naar de bestemming geëxporteerd. Als u geen verplichte sleutel selecteert, worden alle gekwalificeerde profielen niet geëxporteerd, ongeacht de kenmerken ervan."

Een verplicht kenmerk is een selectievakje dat door de gebruiker wordt ingeschakeld en dat ervoor zorgt dat alle profielrecords het geselecteerde kenmerk bevatten. Alle geëxporteerde profielen bevatten bijvoorbeeld een e-mailadres. &#x200B;

U kunt kenmerken als verplicht markeren om ervoor te zorgen dat [!DNL Platform] Hiermee worden alleen de profielen geëxporteerd die het specifieke kenmerk bevatten. Het resultaat is dat het kan worden gebruikt als extra filtermethode. Een attribuut als verplicht markeren is **niet** vereist.

Als u geen verplicht kenmerk selecteert, worden alle gekwalificeerde profielen geëxporteerd, ongeacht de kenmerken ervan.

Het wordt aanbevolen een van de kenmerken [unieke id](../../destinations/catalog/email-marketing/overview.md#identity) vanuit uw schema. Zie het gedeelte Identiteit in het dialoogvenster [E-mailmarketingdoelen](../../destinations/catalog/email-marketing/overview.md#identity) documentatie.

### Deduplicatietoetsen {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="Deduplicatietoetsen"
>abstract="U kunt meerdere records van hetzelfde profiel uit de exportbestanden verwijderen door een deduplicatietoets te selecteren. Selecteer één naamruimte of maximaal twee XDM-schemakenmerken als een deduplicatietoets. Als u geen deduplicatietoets selecteert, kan dit leiden tot dubbele profielvermeldingen in de exportbestanden."

Een deduplicatiesleutel is een door de gebruiker gedefinieerde primaire sleutel waarmee de identiteit wordt bepaald waarmee gebruikers hun profielen willen dedupliceren. &#x200B;

Deduplicatietoetsen maken het onmogelijk meerdere records van hetzelfde profiel in één exportbestand te hebben.

Er zijn drie manieren waarop u deduplicatietoetsen kunt gebruiken in [!DNL Platform]:

* Eén naamruimte voor identiteit gebruiken als een [!UICONTROL deduplication key]
* Eén profielkenmerk gebruiken vanuit een [!DNL XDM] profiel als [!UICONTROL deduplication key]
* Een combinatie van twee profielkenmerken van een [!DNL XDM] profiel als samengestelde sleutel

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
        "id": "johndoe_2@example.com"
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
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
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

Uitdeduplicatie door de [!DNL Email] naamruimte, bevat het exportbestand de volgende vermeldingen. Profiel B is het meest recente profiel dat in aanmerking komt voor het publiek. Het is dus de enige profiel dat wordt geëxporteerd.

| E-mail* | PersonalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | John | D |
| johndoe_2@example.com | johndoe@example.com | John | D |

### Gebruiksscenario voor deduplicatie 3: deduplicatie op basis van één profielkenmerk {#deduplication-use-case-3}

Uitdeduplicatie door de `personal Email` -kenmerk, bevat het exportbestand de volgende vermelding. Profiel B is het meest recente profiel dat in aanmerking komt voor het publiek. Het is dus de enige profiel dat wordt geëxporteerd.

| PersonalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | D |


### Gebruiksscenario deduplicatie 4: deduplicatie op basis van twee profielkenmerken {#deduplication-use-case-4}

Veronderstellend deduplicatie door de samengestelde sleutel `personalEmail + lastName`bevat het exportbestand de volgende vermeldingen.

| PersonalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | John |
| johndoe@example.com | Doe | John |

Adobe raadt u aan een naamruimte voor identiteiten te selecteren, zoals een naamruimte [!DNL CRM ID] of e-mailadres als deduplicatietoets, om ervoor te zorgen dat alle profielrecords uniek worden geïdentificeerd.

>[!NOTE]
> 
>Als er labels voor gegevensgebruik zijn toegepast op bepaalde velden in een gegevensset (in plaats van op de gehele gegevensset), wordt de toepassing van die labels op veldniveau bij activering uitgevoerd onder de volgende voorwaarden:
>
>* De velden worden gebruikt in de definitie van het publiek.
>* De velden worden geconfigureerd als geprojecteerde kenmerken voor de doelbestemming.
>
> Als het veld `person.name.firstName` heeft bepaalde etiketten van het gegevensgebruik die met de het op de markt brengen van de bestemming in conflict zijn, zou u een schending van het beleid van het gegevensgebruik in de overzichtsstap worden getoond. Zie voor meer informatie [Beheer van gegevens in Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations).

### [!BADGE Beta]{type=Informative} Arrays exporteren via berekende velden {#export-arrays-calculated-fields}

Selecteer bèta-klanten kunnen arrayobjecten van Experience Platform naar cloudopslagdoelen exporteren. Meer informatie over [exporteren, arrays en berekende velden](/help/destinations/ui/export-arrays-calculated-fields.md) en neem contact op met uw Adobe voor toegang tot de functionaliteit.

### Bekende beperkingen {#known-limitations}

De nieuwe **[!UICONTROL Mapping]** De pagina heeft de volgende bekende beperkingen:

#### Het kenmerk Publiek-lidmaatschap kan niet worden geselecteerd via de toewijzingsworkflow

Vanwege een bekende beperking kun je momenteel de **[!UICONTROL Select field]** toe te voegen venster `segmentMembership.status` naar uw bestand exporteren. In plaats daarvan moet u de waarde handmatig plakken `xdm: segmentMembership.status` in het schemagebied, zoals hieronder getoond.

![De opname van het scherm die de werkruimte van het publiekslidmaatschap in de afbeeldingsstap van het activeringswerkschema toont.](../assets/ui/activate-batch-profile-destinations/segment-membership-mapping-step.gif)

Het exporteren van bestanden kan als volgt variëren, afhankelijk van of `segmentMembership.status` is geselecteerd:
* Als de `segmentMembership.status` veld is geselecteerd, geëxporteerde bestanden bevatten **[!UICONTROL Active]** leden in de eerste volledige momentopname en nieuw **[!UICONTROL Active]** en **[!UICONTROL Expired]** leden in latere incrementele uitvoer.
* Als de `segmentMembership.status` veld is niet geselecteerd, geëxporteerde bestanden bevatten alleen **[!UICONTROL Active]** leden in de eerste volledige momentopname en in de daaropvolgende incrementele uitvoer.

Meer informatie over [exportgedrag profiel voor op bestanden gebaseerde doelen](/help/destinations/how-destinations-work/profile-export-behavior.md#file-based-destinations).

#### Naamruimten kunnen momenteel niet worden geselecteerd voor exporteren

Het selecteren van naamruimten voor exporteren, zoals wordt weergegeven in de onderstaande afbeelding, wordt momenteel niet ondersteund. Als u naamruimten selecteert die u wilt exporteren, wordt een fout weergegeven in het dialoogvenster **[!UICONTROL Review]** stap.

![Niet-ondersteunde toewijzing die identiteitsexport weergeeft.](../assets/ui/activate-batch-profile-destinations/unsupported-identity-mapping.png)

Als tijdelijke oplossing kunt u:
* Gebruik de oude opslagdoelen van de cloud voor de dataflows waar u naamruimten wilt opnemen in de exportbewerkingen
* Upload identiteiten als attributen in Experience Platform, dan voer hen naar uw bestemmingen van de wolkenopslag uit.

## Profielkenmerken selecteren {#select-attributes}

>[!IMPORTANT]
> 
Alle cloudopslagbestemmingen in de catalogus kunnen een verbeterde [[!UICONTROL Mapping] stap](#mapping) die de **[!UICONTROL Select attributes]** in deze sectie beschreven stap.
>
Dit **[!UICONTROL Select attributes]** De stap wordt nog getoond voor Adobe Campaign, Oracle Resys, Oracle Eloqua, en de Marketing Cloud van Salesforce e-mailmarketing bestemmingen.

Voor op profiel gebaseerde bestemmingen, moet u de profielattributen selecteren die u naar de doelbestemming wilt verzenden.

1. In de **[!UICONTROL Select attributes]** pagina, selecteert u **[!UICONTROL Add new field]**.

   ![Afbeelding die de knop Nieuw veld toevoegen markeert.](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

2. Selecteer de pijl rechts van de knop **[!UICONTROL Schema field]** vermelding.

   ![Afbeeldingsmarkering waarmee u een bronveld kunt selecteren.](../assets/ui/activate-batch-profile-destinations/select-source-field.png)

3. In de **[!UICONTROL Select field]** pagina, selecteert u de XDM-kenmerken of naamruimten die u naar het doel wilt verzenden en kiest u **[!UICONTROL Select]**.

   ![Afbeelding waarin de verschillende velden worden weergegeven die beschikbaar zijn als bronvelden.](../assets/ui/activate-batch-profile-destinations/target-field-page.png)

4. Herhaal stap 1 tot en met 3 om meer toewijzingen toe te voegen.

>[!NOTE]
>
Adobe Experience Platform vult uw selectie vooraf in met vier aanbevolen, veelgebruikte kenmerken uit uw schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

![Afbeelding met vooraf ingevulde aanbevolen kenmerken in de toewijzingsstap van de activeringsworkflow voor het publiek.](../assets/ui/activate-batch-profile-destinations/prefilled-fields.png)

>[!IMPORTANT]
>
Vanwege een bekende beperking kun je momenteel de **[!UICONTROL Select field]** toe te voegen venster `segmentMembership.status` naar uw bestand exporteren. In plaats daarvan moet u de waarde handmatig plakken `xdm: segmentMembership.status` in het schemagebied, zoals hieronder getoond.
>
![De opname van het scherm die de werkruimte van het publiekslidmaatschap in de afbeeldingsstap van het activeringswerkschema toont.](..//assets/ui/activate-batch-profile-destinations/segment-membership.gif)

Het exporteren van bestanden kan op de volgende manieren verschillen, afhankelijk van of `segmentMembership.status` is geselecteerd:
* Als de `segmentMembership.status` veld is geselecteerd, geëxporteerde bestanden bevatten **[!UICONTROL Active]** leden in de eerste volledige momentopname en **[!UICONTROL Active]** en **[!UICONTROL Expired]** leden in latere incrementele uitvoer.
* Als de `segmentMembership.status` veld is niet geselecteerd, geëxporteerde bestanden bevatten alleen **[!UICONTROL Active]** leden in de eerste volledige momentopname en in de daaropvolgende incrementele uitvoer.

## Verrijkingskenmerken selecteren {#select-enrichment-attributes}

[!CONTEXTUALHELP]
id="platform_destinations_activate_exclude_enrichment_attributes"
title="Verrijkingskenmerken uitsluiten"
abstract="Schakel deze optie in om de profielen van het geselecteerde aangepaste geüploade publiek naar uw bestemming te exporteren, zonder alle kenmerken ervan uit te sluiten."
additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#select-enrichment-attributes" text="Meer informatie in documentatie"

>[!IMPORTANT]
>
Deze stap wordt alleen weergegeven als u **[!UICONTROL Custom upload]** publiek tijdens de [doelselectie](#select-audiences) stap.

Verrijkingskenmerken komen overeen met het aangepaste geüploade publiek dat in Experience Platform wordt opgenomen als **[!UICONTROL Custom uploads]**. In deze stap kunt u voor elk geselecteerd extern publiek selecteren welke kenmerken u wilt exporteren naar uw doel.

![UI-afbeelding die de selectiestap voor verrijkingskenmerken weergeeft.](../assets/ui/activate-batch-profile-destinations/select-enrichment-attributes-step.png)

Voer de onderstaande stappen uit om verrijkingskenmerken voor elk extern publiek te selecteren:

1. In de **[!UICONTROL Enrichment attributes]** kolom, selecteert u de ![Bewerken, knop](../assets/ui/activate-batch-profile-destinations/edit-button.svg) (Bewerken).
2. Selecteer **[!UICONTROL Add enrichment attribute]**. Er wordt een nieuw leeg schemaveld weergegeven.
   ![UI-afbeelding die het modale scherm weergeeft met de verrijkingskenmerken.](../assets/ui/activate-batch-profile-destinations/add-enrichment-attribute.png)
3. Selecteer de knop rechts van het lege veld om het selectiescherm van het veld te openen.
4. Selecteer de kenmerken die u voor het publiek wilt exporteren.
   ![UI-afbeelding met de lijst met verrijkingskenmerken.](../assets/ui/activate-batch-profile-destinations/select-enrichment-attributes.png)
5. Nadat u alle kenmerken hebt toegevoegd die u wilt exporteren, selecteert u **[!UICONTROL Save and close]**.
6. Herhaal deze stappen voor elk extern publiek.

Als u een extern publiek naar uw doelen wilt activeren zonder een kenmerk te exporteren, schakelt u het **[!UICONTROL Exclude enrichment attributes]** schakelen. Met deze optie exporteert u de profielen van het externe publiek, maar de bijbehorende kenmerken worden niet naar uw bestemming verzonden.

![UI-afbeelding die de schakeloptie Verrijkingskenmerken uitsluiten weergeeft.](../assets/ui/activate-batch-profile-destinations/exclude-enrichment-attributes.png)

Selecteren **[!UICONTROL Next]** om naar [Controleren](#review) stap.

## Controleren {#review}

Op de **[!UICONTROL Review]** , kunt u een overzicht van uw selectie zien. Selecteren **[!UICONTROL Cancel]** om de stroom op te delen, **[!UICONTROL Back]** om uw instellingen te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

![Selectieoverzicht weergegeven in de revisiestap.](../assets/ui/activate-batch-profile-destinations/review.png)

### Goedkeuring van het beleid {#consent-policy-evaluation}

[!CONTEXTUALHELP]
id="platform_governance_policies_viewApplicableConsentPolicies"
title="Toepasselijk toestemmingsbeleid weergeven"
abstract="Als uw organisatie is aangeschaft **Adobe Gezondheidsschild** of **Privacy- en beveiligingsschild van Adobe**, selecteert u **[!UICONTROL View applicable consent policies]** na te gaan welk toestemmingsbeleid wordt toegepast en hoeveel profielen als gevolg daarvan in de activering worden opgenomen. Deze controle is gehandicapt als uw bedrijf geen toegang tot hierboven vermelde SKUs heeft."

Als uw organisatie is aangeschaft **Adobe Gezondheidsschild** of **Privacy- en beveiligingsschild van Adobe**, selecteert u **[!UICONTROL View applicable consent policies]** na te gaan welk toestemmingsbeleid wordt toegepast en hoeveel profielen als gevolg daarvan in de activering worden opgenomen. Meer informatie [goedkeuring beleidsevaluatie](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) voor meer informatie .

### Controle van het gegevensgebruiksbeleid {#data-usage-policy-checks}

In de **[!UICONTROL Review]** stap, controleert het Experience Platform ook om het even welke schendingen van het beleid van het gegevensgebruik. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor publieksactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe u beleidsovertredingen kunt oplossen, leest u informatie over [beleidsovertredingen voor gegevensgebruik](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) in de sectie Documentatie inzake gegevensbeheer.

![Een voorbeeld van een schending van gegevensbeleid dat in de activeringswerkstroom wordt getoond.](../assets/common/data-policy-violation.png)

### Filter publiek {#filter-audiences}

In deze stap kunt u ook de beschikbare filters op de pagina gebruiken om alleen de doelgroepen weer te geven waarvan het schema of de toewijzing is bijgewerkt als onderdeel van deze workflow. U kunt ook schakelen welke tabelkolommen u wilt zien.

![De opname van het scherm die de beschikbare publieksfilters in de overzichtsstap toont.](../assets/ui/activate-batch-profile-destinations/filter-audiences-batch-review.gif)

Als u tevreden bent met de selectie en er zijn geen beleidsovertredingen vastgesteld, selecteert u **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

## Activering van publiek controleren {#verify}

Bij het exporteren van soorten publiek naar cloudopslagbestemmingen maakt Adobe Experience Platform een `.csv`, `.json`, of `.parquet` in de opslaglocatie die u hebt opgegeven. Er wordt een nieuw bestand verwacht dat op uw opslaglocatie wordt gemaakt volgens het schema dat u instelt in de workflow. De standaardbestandsindeling wordt hieronder weergegeven, maar u kunt [de componenten van de bestandsnaam bewerken](#file-names):
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

Als u bijvoorbeeld een dagelijkse exportfrequentie selecteert, kunnen de bestanden die u op drie opeenvolgende dagen ontvangt er als volgt uitzien:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

De aanwezigheid van deze bestanden op de opslaglocatie bevestigt dat de activering is gelukt. Als u wilt weten hoe de geëxporteerde bestanden zijn gestructureerd, kunt u [een voorbeeld van een CSV-bestand downloaden](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). Dit voorbeeldbestand bevat de profielkenmerken `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, en `personalEmail.address`.
