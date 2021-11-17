---
keywords: Experience Platform;home;populaire onderwerpen;dataflow;DataFlow
solution: Experience Platform
title: Een DataFlow configureren voor een Cloud Storage Batch-connector in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Een dataflow is een geplande taak die gegevens van een bron aan een dataset van de Platform terugwint en opneemt. Deze zelfstudie bevat stappen voor het configureren van een nieuwe gegevensstroom met uw cloud storage account.
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
source-git-commit: 10f04044e970158131677e0c630edf761d4577bd
workflow-type: tm+mt
source-wordcount: '1969'
ht-degree: 0%

---

# Een gegevensstroom configureren voor een batch-verbinding voor cloudopslag in de gebruikersinterface

Een dataflow is een geplande taak die gegevens van een bron aan een bron terugwint en opneemt [!DNL Platform] dataset. Deze zelfstudie bevat stappen voor het configureren van een nieuwe gegevensstroom met uw cloud storage account.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Daarnaast vereist deze zelfstudie dat u beschikt over een gevestigde account voor cloudopslag. Een lijst met zelfstudies voor het maken van verschillende cloudopslagaccounts in de gebruikersinterface vindt u in het dialoogvenster [overzicht van bronconnectors](../../../../home.md).

### Ondersteunde bestandsindelingen

[!DNL Experience Platform] ondersteunt de volgende bestandsindelingen die door externe opslagmedia moeten worden ingevoerd:

* Door scheidingstekens gescheiden waarden (DSV): Elke waarde van één teken kan worden gebruikt als scheidingsteken voor gegevensbestanden met DSV-indeling.
* [!DNL JavaScript Object Notation] (JSON): Gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
* [!DNL Apache Parquet]: Gegevensbestanden met parketindeling moeten XDM-compatibel zijn.
* Gecomprimeerde bestanden: JSON- en gescheiden bestanden kunnen als volgt worden gecomprimeerd: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`, en `tar`.

## Gegevens selecteren

Nadat u uw account voor cloudopslag hebt gemaakt, kunt u **[!UICONTROL Select data]** wordt weergegeven met een interface waarmee u de hiërarchie van uw cloudopslagbestanden kunt verkennen.

* Het linkergedeelte van de interface is een directorybrowser waarin uw bestanden en mappen voor cloudopslag worden weergegeven.
* In het rechtergedeelte van de interface kunt u maximaal 100 rijen gegevens uit een compatibel bestand voorvertonen.

![interface](../../../../images/tutorials/dataflow/cloud-storage/batch/interface.png)

Als u een map in de lijst selecteert, kunt u de mappenhiërarchie doorlopen in diepere mappen. U kunt één map selecteren om alle bestanden in de map recursief in te voeren. Wanneer u een volledige map opgeeft, moet u ervoor zorgen dat alle bestanden in de map hetzelfde schema hebben.

Als u een compatibel bestand of een compatibele map hebt geselecteerd, selecteert u de desbetreffende gegevensindeling in het menu [!UICONTROL Select data format] vervolgkeuzemenu.

In de volgende tabel wordt de juiste gegevensindeling voor de ondersteunde bestandstypen weergegeven:

| Bestandstype | Gegevensindeling |
| --- | --- |
| CSV | [!UICONTROL Delimited] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL XDM Parquet] |

Selecteren **[!UICONTROL JSON]** en wacht een paar seconden totdat de voorvertoningsinterface wordt gevuld.

![select-data](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

>[!NOTE]
>
>In tegenstelling tot de bestandstypen Gescheiden door scheidingstekens en JSON, zijn bestanden met de indeling Parquet niet beschikbaar voor voorvertoning.

Met de voorvertoningsinterface kunt u de inhoud en structuur van een bestand controleren. Standaard wordt in de voorvertoningsinterface het eerste bestand weergegeven in de map die u hebt geselecteerd.

Als u een voorvertoning van een ander bestand wilt weergeven, selecteert u het voorvertoningspictogram naast de naam van het bestand dat u wilt inspecteren.

![standaardvoorvertoning](../../../../images/tutorials/dataflow/cloud-storage/batch/default-preview.png)

Als u de inhoud en structuur van de bestanden in uw map hebt geïnspecteerd, selecteert u **[!UICONTROL Next]** om alle bestanden in de map recursief in te voeren.

![select-folder](../../../../images/tutorials/dataflow/cloud-storage/batch/select-folder.png)

Als u liever een specifiek bestand wilt selecteren, selecteert u het bestand dat u wilt insluiten en selecteert u **[!UICONTROL Next]**.

![bestand selecteren](../../../../images/tutorials/dataflow/cloud-storage/batch/select-file.png)

### Een aangepast scheidingsteken instellen voor gescheiden bestanden

U kunt een aangepast scheidingsteken instellen bij het invoegen van gescheiden bestanden. Selecteer **[!UICONTROL Delimiter]** en selecteert u vervolgens een scheidingsteken in het vervolgkeuzemenu. In het menu worden de meest gebruikte opties voor scheidingstekens weergegeven, waaronder een komma (`,`), een tab (`\t`) en een pijp (`|`). Als u liever een aangepast scheidingsteken gebruikt, selecteert u **[!UICONTROL Custom]** en voert u in de pop-upinvoerbalk een scheidingsteken voor één teken naar keuze in.

Als u de gegevensindeling hebt geselecteerd en het scheidingsteken hebt ingesteld, selecteert u **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/delimiter.png)

### Gecomprimeerde bestanden samenvoegen

U kunt gecomprimeerde JSON- of gescheiden bestanden opnemen door het compressietype ervan op te geven.

In de [!UICONTROL Select data] Selecteer een gecomprimeerd bestand voor inname en selecteer vervolgens het juiste bestandstype en of het al dan niet compatibel is met XDM. Selecteer vervolgens **[!UICONTROL Compression type]** en selecteert u vervolgens het juiste gecomprimeerde bestandstype voor de brongegevens.

Selecteer een gecomprimeerd bestandstype **[!UICONTROL Next]** om verder te gaan.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/compressed-files.png)

## Gegevensvelden toewijzen aan een XDM-schema

De **[!UICONTROL Mapping]** stap wordt weergegeven en biedt een interactieve interface voor het toewijzen van de brongegevens aan een [!DNL Platform] dataset. De brondossiers die in Parquet worden geformatteerd moeten XDM volgzaam zijn en vereisen u niet om de afbeelding manueel te vormen, terwijl de Csv- dossiers u vereisen om de afbeelding uitdrukkelijk te vormen, maar u toe te staan om te kiezen welke brongegevensgebieden aan kaart te brengen. Voor JSON-bestanden is geen handmatige configuratie vereist als deze zijn gemarkeerd als XDM-klacht. Nochtans, als het niet duidelijk als volgzaam XDM is, zal het u vereisen om de afbeelding uitdrukkelijk te vormen.

Kies een dataset voor binnenkomende gegevens waarin moeten worden opgenomen. U kunt of een bestaande dataset gebruiken of nieuwe creëren.

**Een bestaande gegevensset gebruiken**

Om gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Existing dataset]** selecteert u vervolgens het pictogram voor de gegevensset.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

De **[!UICONTROL Select dataset]** wordt weergegeven. Zoek de dataset u wenst te gebruiken, het te selecteren, dan klik **[!UICONTROL Continue]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-dataset.png)

**Een nieuwe gegevensset gebruiken**

Om gegevens in een nieuwe dataset in te voeren, selecteer **[!UICONTROL New dataset]** en voert een naam en een beschrijving voor de gegevensset in de opgegeven velden in. Als u een schema wilt toevoegen, kunt u een bestaande schemanaam invoeren in het dialoogvenster **[!UICONTROL Select schema]** in. U kunt ook de **[!UICONTROL Schema advanced search]** naar een geschikt schema zoeken.

Tijdens deze stap, kunt u uw dataset voor toelaten [!DNL Real-time Customer Profile] en een holistische weergave te maken van de kenmerken en gedragingen van een entiteit. Gegevens van alle ingeschakelde gegevenssets worden opgenomen in [!DNL Profile] en wijzigingen worden toegepast wanneer u de gegevensstroom opslaat.

Schakelen tussen **[!UICONTROL Profile dataset]** knoop om uw doeldataset voor toe te laten [!DNL Profile].

![](../../../../images/tutorials/dataflow/cloud-storage/batch/new-dataset.png)

De **[!UICONTROL Select schema]** wordt weergegeven. Selecteer het schema u op de nieuwe dataset wilt toepassen, dan selecteren **[!UICONTROL Done]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor meer informatie over mapperfuncties en berekende velden raadpleegt u de [Handleiding voor functies Data Prep](../../../../../data-prep/functions.md) of de [hulplijn voor berekende velden](../../../../../data-prep/calculated-fields.md).

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

Voor JSON-bestanden kunt u, naast het rechtstreeks toewijzen van velden aan andere velden, objecten rechtstreeks toewijzen aan andere objecten en arrays aan andere arrays. U kunt ook complexe gegevenstypen voorvertonen en toewijzen, zoals arrays in JSON-bestanden, met behulp van een bronconnector voor cloudopslag.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/source-field-json.png)

![](../../../../images/tutorials/dataflow/cloud-storage/batch/target-field-json.png)

Houd er rekening mee dat u geen toewijzingen kunt maken voor verschillende typen. U kunt een object bijvoorbeeld niet toewijzen aan een array of een veld aan een object.

>[!TIP]
>
>Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen.

Selecteren **[!UICONTROL Preview data]** om afbeeldingsresultaten van maximaal 100 rijen steekproefgegevens van de geselecteerde dataset te zien.

Tijdens de voorvertoning krijgt de identiteitskolom de prioriteit als het eerste veld, omdat dit de belangrijkste informatie is die nodig is voor het valideren van toewijzingsresultaten.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping-preview.png)

Selecteer **[!UICONTROL Close]**.

## Planninguitvoering

De **[!UICONTROL Scheduling]** de stap verschijnt, toestaand u om een innameprogramma te vormen om de geselecteerde brongegevens automatisch in te nemen gebruikend de gevormde afbeeldingen. De volgende lijst schetst de verschillende configureerbare gebieden voor het plannen:

| Veld | Beschrijving |
| --- | --- |
| Frequentie | Selecteerbare frequenties omvatten `Once`, `Minute`, `Hour`, `Day`, en `Week`. |
| Interval | Een geheel getal dat het interval voor de geselecteerde frequentie instelt. |
| Begintijd | Een UTC-tijdstempel die aangeeft wanneer de eerste opname wordt uitgevoerd. |
| Achtergrond | Een booleaanse waarde die bepaalt welke gegevens eerst worden ingevoerd. Indien **[!UICONTROL Backfill]** is ingeschakeld, worden alle huidige bestanden in het opgegeven pad tijdens de eerste geplande opname opgenomen. Indien **[!UICONTROL Backfill]** is uitgeschakeld, worden alleen de bestanden opgenomen die tussen de eerste opname en de begintijd worden geladen. Bestanden die vóór de begintijd zijn geladen, worden niet opgenomen. |

Dataflows worden ontworpen om gegevens automatisch in te voeren op een geplande basis. Begin door de innamefrequentie te selecteren. Daarna, plaats het interval om de periode tussen twee stroomlooppas aan te wijzen. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul en moet worden ingesteld op groter dan of gelijk aan 15.

Als u de begintijd voor inname wilt instellen, past u de datum en tijd aan die worden weergegeven in het vak Begintijd. U kunt ook het kalenderpictogram selecteren om de begintijdwaarde te bewerken. De begintijd moet groter zijn dan of gelijk zijn aan de huidige tijd in UTC.

Geef waarden op voor het schema en selecteer **[!UICONTROL Next]**.

>[!NOTE]
>
>Voor batch-opname selecteert elke volgende gegevensstroom bestanden die van uw bron moeten worden ingepakt op basis van hun **laatst gewijzigd** tijdstempel. Dit betekent dat de partijgegevens uitgezochte dossiers van de bron die of nieuw zijn of sinds de laatste dataflow looppas zijn gewijzigd.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-interval-on.png)

### Eenmalige gegevensstroom voor inname instellen

Als u eenmalige invoer wilt instellen, selecteert u de pijl-omlaag voor de frequentie en selecteert u **[!UICONTROL Once]**. U kunt bewerkingen blijven uitvoeren op een gegevensstroom die is ingesteld voor eenmalig opnemen van de frequentie, zolang de begintijd in de toekomst behouden blijft. Zodra de begintijd is verstreken, kan de eenmalig frequentiewaarde niet meer worden bewerkt. **[!UICONTROL Interval]** en **[!UICONTROL Backfill]** zijn niet zichtbaar wanneer u een eenmalige gegevensstroom instelt.

>[!IMPORTANT]
>
>Het wordt ten zeerste aanbevolen om uw gegevensstroom voor eenmalige inname te plannen wanneer u de [FTP-aansluiting](../../../../connectors/cloud-storage/ftp.md).

Als u de juiste waarden voor het schema hebt opgegeven, selecteert u **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-once.png)

## Gegevens over gegevensstroom opgeven

De **[!UICONTROL Dataflow detail]** wordt weergegeven, zodat u een naam kunt geven en een korte beschrijving kunt geven van uw nieuwe gegevensstroom.

Tijdens dit proces kunt u ook **[!UICONTROL Partial ingestion]** en **[!UICONTROL Error diagnostics]**. Inschakelen **[!UICONTROL Partial ingestion]** biedt de mogelijkheid om gegevens met fouten in te voeren tot een bepaalde drempel die u kunt instellen. Inschakelen **[!UICONTROL Error diagnostics]** bevat details over onjuiste gegevens die afzonderlijk in een batch worden opgeslagen. Zie voor meer informatie de [gedeeltelijke batch-opname, overzicht](../../../../../ingestion/batch-ingestion/partial.md).

Geef waarden op voor de gegevensstroom en selecteer **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/dataflow-detail.png)

## Controleer uw gegevensstroom

De **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Toont het brontype, de relevante weg van het gekozen brondossier, en de hoeveelheid kolommen binnen dat brondossier.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset zich aan houdt.
* **[!UICONTROL Scheduling]**: Toont de actieve periode, de frequentie, en het interval van het innameprogramma.

Nadat u de gegevensstroom hebt gecontroleerd, klikt u op **[!UICONTROL Finish]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamepercentages, succes, en fouten te zien. Voor meer informatie over hoe te om dataflow te controleren, zie de zelfstudie op [het controleren van rekeningen en gegevensstromen in UI](../../monitor.md).

## Uw gegevensstroom verwijderen

U kunt gegevensstromen schrappen die niet meer noodzakelijk of verkeerd gecreeerd gebruikend zijn **[!UICONTROL Delete]** functie beschikbaar in de **[!UICONTROL Dataflows]** werkruimte. Raadpleeg de zelfstudie voor meer informatie over het verwijderen van gegevensstromen [verwijderen, gegevensstromen in de gebruikersinterface](../../delete.md).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes een dataflow gemaakt om gegevens van een externe wolkenopslag in te brengen, en hebt u inzicht gekregen in de controle van datasets. Als u meer wilt weten over het maken van gegevensstromen, kunt u uw studie aanvullen door de onderstaande video te bekijken. Bovendien kunnen inkomende gegevens nu worden gebruikt door downstreamgebruikers [!DNL Platform] diensten zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

* [[!DNL Real-time Customer Profile] - overzicht](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] - overzicht](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> De [!DNL Platform] De interface die in de volgende video wordt weergegeven, is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Aanhangsel

De volgende secties verstrekken extra informatie voor het werken met bronschakelaars.

### Een gegevensstroom uitschakelen

Wanneer een gegevensstroom wordt gecreeerd, wordt het onmiddellijk actief en neemt gegevens volgens het programma op het werd gegeven. U kunt een actieve gegevensstroom op elk ogenblik onbruikbaar maken door de instructies hieronder te volgen.

Binnen de **[!UICONTROL Sources]** werkruimte, klikt u op de knop **[!UICONTROL Browse]** tab. Klik vervolgens op de naam van de account die is gekoppeld aan de actieve gegevensstroom die u wilt uitschakelen.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

De **[!UICONTROL Source activity]** wordt weergegeven. Selecteer de actieve gegevensstroom in de lijst om zijn te openen **[!UICONTROL Properties]** aan de rechterkant van het scherm, dat een **[!UICONTROL Enabled]** schakelknop. Klik op de schakeloptie om de gegevensstroom uit te schakelen. Dezelfde schakeloptie kan worden gebruikt om een gegevensstroom opnieuw in te schakelen nadat deze is uitgeschakeld.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### Inkomende gegevens activeren voor [!DNL Profile] bevolking

De binnenkomende gegevens van uw bronschakelaar kunnen aan het verrijken en het bevolken van uw [!DNL Real-time Customer Profile] gegevens. Voor meer informatie over het vullen van uw [!DNL Real-time Customer Profile] gegevens, raadpleeg de zelfstudie over [Profielpopulatie](../../profile.md).
