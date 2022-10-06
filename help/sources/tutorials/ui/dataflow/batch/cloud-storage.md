---
keywords: Experience Platform;home;populaire onderwerpen;dataflow;DataFlow
title: Een gegevensstroom configureren om batchgegevens in te voeren vanuit een Cloud Storage-bron in de gebruikersinterface
description: Deze zelfstudie bevat stappen voor het configureren van een nieuwe gegevensstroom voor het opnemen van batchgegevens uit een bron voor cloudopslag in de gebruikersinterface
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
source-git-commit: 0910de76d817eea7c7c3cb2b988d81268b3e5812
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 0%

---

# Een gegevensstroom configureren om batchgegevens van een bron voor cloudopslag in de gebruikersinterface in te voeren

Deze zelfstudie bevat stappen voor het configureren van een gegevensstroom om batchgegevens van uw cloudopslagbron naar Adobe Experience Platform te verzenden.

## Aan de slag

>[!NOTE]
>
>Als u een gegevensstroom wilt maken om batchgegevens van een cloudopslag te kunnen ophalen, moet u al toegang hebben tot een geverifieerde bron voor cloudopslag. Als u geen toegang hebt, gaat u naar [overzicht van bronnen](../../../../home.md#cloud-storage) voor een lijst met bronnen voor cloudopslag waarmee u een account kunt maken.

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

### Ondersteunde bestandsindelingen

Cloudopslagbronnen voor batchgegevens ondersteunen de volgende bestandsindelingen voor inname:

* Door scheidingstekens gescheiden waarden (DSV): Elke waarde van één teken kan worden gebruikt als scheidingsteken voor gegevensbestanden met DSV-indeling.
* [!DNL JavaScript Object Notation] (JSON): Gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
* [!DNL Apache Parquet]: Gegevensbestanden met parketindeling moeten XDM-compatibel zijn.
* Gecomprimeerde bestanden: JSON- en gescheiden bestanden kunnen als volgt worden gecomprimeerd: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`, en `tar`.

## Gegevens toevoegen

Nadat u uw account voor cloudopslag hebt gemaakt, kunt u **[!UICONTROL Add data]** wordt weergegeven, zodat u een interface hebt waarmee u de hiërarchie van uw cloudopslagbestanden kunt verkennen en de map of het specifieke bestand kunt selecteren dat u naar het Platform wilt brengen.

* Het linkergedeelte van de interface is een mappenbrowser waarin de hiërarchie van de bestanden voor cloudopslag wordt weergegeven.
* In het rechtergedeelte van de interface kunt u maximaal 100 rijen gegevens uit een compatibele map of bestand voorvertonen.

![](../../../../images/tutorials/dataflow/cloud-batch/select-data.png)

Selecteer de hoofdmap voor toegang tot de mappenhiërarchie. Van hieruit kunt u één map selecteren om alle bestanden in de map recursief in te voeren. Wanneer u een volledige map opgeeft, moet u ervoor zorgen dat alle bestanden in die map dezelfde gegevensindeling en hetzelfde schema hebben.

![](../../../../images/tutorials/dataflow/cloud-batch/folder-directory.png)

Nadat u een map hebt geselecteerd, wordt de juiste interface bijgewerkt met een voorvertoning van de inhoud en structuur van het eerste bestand in de geselecteerde map.

![](../../../../images/tutorials/dataflow/cloud-batch/select-folder.png)

Tijdens deze stap kunt u verschillende configuraties voor uw gegevens maken voordat u verdergaat. Eerst selecteert u **[!UICONTROL Data format]** en selecteert u vervolgens de juiste gegevensindeling voor het bestand in het vervolgkeuzemenu dat wordt weergegeven.

In de volgende tabel worden de juiste gegevensindelingen voor de ondersteunde bestandstypen weergegeven:

| Bestandstype | Gegevensindeling |
| --- | --- |
| CSV | [!UICONTROL Delimited] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL XDM Parquet] |

![](../../../../images/tutorials/dataflow/cloud-batch/data-format.png)

### Een kolomscheidingsteken selecteren

Nadat u de gegevensindeling hebt geconfigureerd, kunt u een kolomscheidingsteken instellen bij het invoegen van gescheiden bestanden. Selecteer **[!UICONTROL Delimiter]** en selecteert u vervolgens een scheidingsteken in het vervolgkeuzemenu. In het menu worden de meest gebruikte opties voor scheidingstekens weergegeven, waaronder een komma (`,`), een tab (`\t`) en een pijp (`|`).

![](../../../../images/tutorials/dataflow/cloud-batch/delimiter.png)

Als u liever een aangepast scheidingsteken gebruikt, selecteert u **[!UICONTROL Custom]** en voert u in de pop-upinvoerbalk een scheidingsteken voor één teken naar keuze in.

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

### Gecomprimeerde bestanden samenvoegen

U kunt ook gecomprimeerde JSON- of gescheiden bestanden opnemen door het compressietype ervan op te geven.

In de [!UICONTROL Select data] Selecteer een gecomprimeerd bestand voor inname en selecteer vervolgens het juiste bestandstype en of het al dan niet compatibel is met XDM. Selecteer vervolgens **[!UICONTROL Compression type]** en selecteert u vervolgens het juiste gecomprimeerde bestandstype voor de brongegevens.

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

Als u een specifiek bestand naar een Platform wilt overbrengen, selecteert u een map en selecteert u vervolgens het bestand dat u wilt insluiten. Tijdens deze stap kunt u ook een voorbeeld van de bestandsinhoud van andere bestanden in een bepaalde map bekijken met het voorvertoningspictogram naast een bestandsnaam.

Als u klaar bent, selecteert u **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-batch/select-file.png)

## Gegevens over gegevensstroom opgeven

De [!UICONTROL Dataflow detail] De pagina staat u toe om te selecteren of u een bestaande dataset of een nieuwe dataset wilt gebruiken. Tijdens dit proces kunt u ook uw gegevens configureren om in te voegen in profiel en instellingen inschakelen zoals [!UICONTROL Error diagnostics], [!UICONTROL Partial ingestion], en [!UICONTROL Alerts].

![](../../../../images/tutorials/dataflow/cloud-batch/dataflow-detail.png)

### Een bestaande gegevensset gebruiken

Om gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Existing dataset]**. U kunt of een bestaande dataset terugwinnen gebruikend [!UICONTROL Advanced search] of door door de lijst van bestaande datasets in het dropdown menu te scrollen. Zodra u een dataset hebt geselecteerd, verstrek een naam en een beschrijving voor uw gegevensstroom.

![](../../../../images/tutorials/dataflow/cloud-batch/existing.png)

### Een nieuwe gegevensset gebruiken

Om in een nieuwe dataset in te gaan, selecteer **[!UICONTROL New dataset]** en geef vervolgens een naam voor de uitvoergegevensset en een optionele beschrijving op. Selecteer vervolgens het schema waaraan u wilt toewijzen [!UICONTROL Advanced search] of door door de lijst van bestaande schema&#39;s in het dropdown menu te scrollen. Nadat u een schema hebt geselecteerd, geeft u een naam en een beschrijving voor de gegevensstroom op.

![](../../../../images/tutorials/dataflow/cloud-batch/new.png)

### Profiel- en foutdiagnostiek inschakelen

Selecteer vervolgens de **[!UICONTROL Profile dataset]** Schakel deze optie in om uw gegevensset in te schakelen voor Profiel. Hierdoor kunt u een holistische weergave maken van de kenmerken en het gedrag van een entiteit. De gegevens van alle profiel-toegelaten datasets zullen in Profiel worden omvat en de veranderingen worden toegepast wanneer u sparen uw gegevensstroom.

[!UICONTROL Error diagnostics] laat gedetailleerde foutenmelding generatie voor om het even welke onjuiste verslagen toe die in uw dataflow voorkomen, terwijl [!UICONTROL Partial ingestion] kunt u gegevens met fouten opnemen tot een bepaalde drempel die u handmatig definieert. Zie de [gedeeltelijke batch-opname, overzicht](../../../../../ingestion/batch-ingestion/partial.md) voor meer informatie .

![](../../../../images/tutorials/dataflow/cloud-batch/ingestion-configs.png)

### Waarschuwingen inschakelen

U kunt waarschuwingen inschakelen om meldingen te ontvangen over de status van uw gegevensstroom. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [abonneren op berichten voor bronnen met behulp van de gebruikersinterface](../../alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw gegevensstroom, selecteert u **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-batch/alerts.png)

## Gegevensvelden toewijzen aan een XDM-schema

De [!UICONTROL Mapping] de stap verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie [UI-hulplijn voor gegevensvoorinstelling](../../../../../data-prep/ui/mapping.md).

Als de brongegevens eenmaal zijn toegewezen, selecteert u **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-batch/mapping.png)

## Planninguitvoering

>[!IMPORTANT]
>
>Het wordt ten zeerste aanbevolen om uw gegevensstroom voor eenmalige inname te plannen wanneer u de [FTP-bron](../../../../connectors/cloud-storage/ftp.md).

De [!UICONTROL Scheduling] de stap verschijnt, toestaand u om een innameprogramma te vormen om de geselecteerde brongegevens automatisch in te nemen gebruikend de gevormde afbeeldingen. Standaard is de planning ingesteld op `Once`. Selecteer **[!UICONTROL Frequency]** en selecteert u vervolgens een optie in het vervolgkeuzemenu.

>[!TIP]
>
>Interval en backfill zijn niet zichtbaar tijdens een eenmalige opname.

![plannen](../../../../images/tutorials/dataflow/cloud-batch/scheduling.png)

Als u de innamefrequentie instelt op `Minute`, `Hour`, `Day`, of `Week`dan moet u een interval instellen om een bepaald tijdkader tussen elke opname te bepalen. Bijvoorbeeld een innamefrequentie ingesteld op `Day` en een interval instellen op `15` betekent dat uw gegevensstroom gepland is om gegevens in te voeren om de 15 dagen.

Tijdens deze stap kunt u ook **backfill** en definieert u een kolom voor de incrementele opname van gegevens. Backfill wordt gebruikt om historische gegevens in te voeren, terwijl in de kolom die u voor incrementele inname definieert, nieuwe gegevens kunnen worden onderscheiden van bestaande gegevens.

Zie de lijst hieronder voor meer informatie over het plannen van configuraties.

| Veld | Beschrijving |
| --- | --- |
| Frequentie | De frequentie waarin inname plaatsvindt. Selecteerbare frequenties omvatten `Once`, `Minute`, `Hour`, `Day`, en `Week`. |
| Interval | Een geheel getal dat het interval voor de geselecteerde frequentie instelt. De waarde van het interval moet een geheel getal zijn dat niet gelijk is aan nul en moet worden ingesteld op groter dan of gelijk aan 15. |
| Begintijd | Een UTC-tijdstempel die aangeeft wanneer de eerste opname wordt uitgevoerd. De begintijd moet groter zijn dan of gelijk zijn aan de huidige UTC-tijd. |
| Achtergrond | Een booleaanse waarde die bepaalt welke gegevens eerst worden ingevoerd. Als backfill is ingeschakeld, worden alle huidige bestanden in het opgegeven pad tijdens de eerste geplande inname opgenomen. Als terugvullen is uitgeschakeld, worden alleen de bestanden opgenomen die tussen de eerste opname en de begintijd worden geladen. Bestanden die vóór de begintijd zijn geladen, worden niet opgenomen. |

>[!NOTE]
>
>Voor batch-opname selecteert elke volgende gegevensstroom bestanden die van uw bron moeten worden ingepakt op basis van hun **laatst gewijzigd** tijdstempel. Dit betekent dat de batch-gegevens uitgezocht bestanden van de bron zijn die nieuw zijn of zijn gewijzigd sinds de laatste flowuitvoering. Bovendien moet u ervoor zorgen dat er voldoende tijd is tussen het uploaden van een bestand en een geplande doorloop, omdat bestanden die niet volledig naar uw account voor cloudopslag zijn geüpload voordat de geplande doorlooptijd wordt uitgevoerd, niet kunnen worden opgehaald voor opname.

Als u klaar bent met het configureren van uw innameschema, selecteert u **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-batch/scheduling-configs.png)

## Controleer uw gegevensstroom

De **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Toont het brontype, de relevante weg van het gekozen brondossier, en de hoeveelheid kolommen binnen dat brondossier.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset zich aan houdt.
* **[!UICONTROL Scheduling]**: Toont de actieve periode, de frequentie, en het interval van het innameprogramma.

Nadat u de gegevensstroom hebt gecontroleerd, klikt u op **[!UICONTROL Finish]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

![](../../../../images/tutorials/dataflow/cloud-batch/review.png)


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

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamepercentages, succes, en fouten te bekijken. Voor meer informatie over hoe te om dataflow te controleren, bezoek de zelfstudie op [het controleren van rekeningen en gegevensstromen in UI](../../monitor.md).

## Uw gegevensstroom bijwerken

Ga naar de zelfstudie voor het bijwerken van configuraties voor uw dataflows die plannen, toewijzingen en algemene informatie plannen [het bijwerken van bronnen dataflows in UI](../../update-dataflows.md)

## Uw gegevensstroom verwijderen

U kunt gegevensstromen schrappen die niet meer noodzakelijk of verkeerd gecreeerd gebruikend zijn **[!UICONTROL Delete]** functie beschikbaar in de **[!UICONTROL Dataflows]** werkruimte. Ga voor meer informatie over het verwijderen van gegevensstromen naar de zelfstudie op [verwijderen, gegevensstromen in de gebruikersinterface](../../delete.md).