---
title: Maak een Merkury Enterprise Identity Resolution Source Connection en Dataflow in de gebruikersinterface
description: Leer hoe u een Merkury Enterprise Identity Resolution-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
last-substantial-update: 2023-12=12
badge: Beta
source-git-commit: d862a53c7a8880e86648c05cf94e37e1a1779c9e
workflow-type: tm+mt
source-wordcount: '1944'
ht-degree: 0%

---

# Een [!DNL Merkury Enterprise Identity Resolution] bronverbinding en gegevensstroom in de gebruikersinterface

>[!NOTE]
>
>De [!DNL Merkury Enterprise Identity Resolution] De bron is in bèta. Lees de [overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Deze zelfstudie bevat stappen om een [!DNL Merkury Enterprise Identity Resolution] bronverbinding en gegevensstroom via de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

### Vereiste referenties verzamelen

Om tot uw emmer op Experience Platform toegang te hebben, moet u geldige waarden voor de volgende geloofsbrieven verstrekken:

| Credentials | Beschrijving |
| --- | --- |
| Toegangstoets | De toegangs belangrijkste identiteitskaart voor uw emmer. U kunt deze waarde ophalen uit uw [!DNL Merkury] team. |
| Geheime sleutel | De geheime sleutel-id voor uw emmer. U kunt deze waarde ophalen uit uw [!DNL Merkury] team. |
| Naam van emmertje | Dit is uw Merkury bucket waar de dossiers zullen worden gedeeld. U kunt deze waarde ophalen uit uw [!DNL Merkury] team. |

Meer informatie over instellen voor [!DNL Merkury] en andere voorwaarden, lees de [[!DNL Merkury] bronoverzicht](../../../../connectors/data-partners/merkury.md).

## Maak verbinding met uw Merkury-account

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de **[!UICONTROL Data partners]** categorie, selecteert u **[!UICONTROL Merkury]** en selecteer vervolgens **[!UICONTROL Set up]**.

![De broncatalogus met de geselecteerde Merkury-bron.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/catalog.png)

De **[!UICONTROL Connect to Merkury]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Een nieuwe account maken

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New account]**. Geef op het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Merkury] referenties. Selecteer **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![De nieuwe accountinterface voor Merkury.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/new-account.png)

### Een bestaande account gebruiken

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en selecteert u vervolgens de [!DNL Merkury] account dat u wilt gebruiken. Selecteren **[!UICONTROL Next]** om verder te gaan.

![The existing account interface for Merkury.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/existing-account.png)

>[!BEGINSHADEBOX]

**Ondersteunde bestandsindelingen**

U kunt de volgende bestandsindelingen invoeren met de opdracht [!DNL Merkury] bron:

* DSV (Delimiter-separated-separated values, gescheiden waarden): elke waarde van één teken kan worden gebruikt als scheidingsteken voor gegevensbestanden met DSV-indeling.
* [!DNL JavaScript Object Notation] (JSON): gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
* [!DNL Apache Parquet]: Gegevensbestanden met Parquet-indeling moeten XDM-compatibel zijn.
* Gecomprimeerde bestanden: JSON en bestanden met scheidingstekens kunnen worden gecomprimeerd als: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`, en `tar`.

>[!ENDSHADEBOX]

## Gegevens toevoegen

Nadat u uw [!DNL Merkury] de **[!UICONTROL Add data]** de stap verschijnt, die een interface verstrekken voor u om uw te onderzoeken [!DNL Merkury] bestandshiërarchie en selecteer de map of het specifieke bestand dat u naar het Experience Platform wilt brengen.

* Het linkergedeelte van de interface is een directorybrowser waarin uw [!DNL Merkury] bestandshiërarchie.
* In het rechtergedeelte van de interface kunt u maximaal 100 rijen gegevens uit een compatibele map of bestand voorvertonen.

![Het dossier en de omslagfolder van het bronwerkschema waar u de gegevens kunt selecteren die u wilt opnemen.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/add-data.png)

Selecteer de hoofdmap voor toegang tot de mappenhiërarchie. Van hieruit kunt u één map selecteren om alle bestanden in de map recursief in te voeren. Wanneer u een volledige map opgeeft, moet u ervoor zorgen dat alle bestanden in die map dezelfde gegevensindeling en hetzelfde schema hebben.

Nadat u een map hebt geselecteerd, wordt de juiste interface bijgewerkt met een voorvertoning van de inhoud en structuur van het eerste bestand in de geselecteerde map.

![De gegevens die zijn geselecteerd voor opname en de interface voor voorvertoning van het bestand.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/selected-data.png)


Tijdens deze stap kunt u verschillende configuraties aan uw gegevens toevoegen voordat u verdergaat. Eerst selecteert u **[!UICONTROL Data format]** en selecteert u vervolgens de juiste gegevensindeling voor het bestand in het vervolgkeuzemenu dat wordt weergegeven.

In de volgende tabel worden de juiste gegevensindelingen voor de ondersteunde bestandstypen weergegeven:

| Bestandstype | Gegevensindeling |
| --- | --- |
| CSV | [!UICONTROL Delimited] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL XDM Parquet] |

### Een kolomscheidingsteken selecteren

+++Selecteren om stappen weer te geven voor het instellen van een scheidingsteken

Nadat u de gegevensindeling hebt geconfigureerd, kunt u een kolomscheidingsteken instellen bij het invoegen van gescheiden bestanden. Selecteer de **[!UICONTROL Delimiter]** en selecteert u vervolgens een scheidingsteken in het vervolgkeuzemenu. In het menu worden de meest gebruikte opties voor scheidingstekens weergegeven, waaronder een komma (`,`), een tab (`\t`) en een pijp (`|`).

Als u liever een aangepast scheidingsteken gebruikt, selecteert u **[!UICONTROL Custom]** en voert u in de pop-upinvoerbalk een scheidingsteken voor één teken naar keuze in.

+++

### Gecomprimeerde bestanden samenvoegen

+++ Selecteren om stappen weer te geven voor het opnemen van gecomprimeerde bestanden

U kunt ook gecomprimeerde JSON- of gescheiden bestanden opnemen door het compressietype ervan op te geven.

In de [!UICONTROL Select data] Selecteer een gecomprimeerd bestand voor inname en selecteer vervolgens het juiste bestandstype en of het al dan niet compatibel is met XDM. Selecteer vervolgens **[!UICONTROL Compression type]** en selecteert u vervolgens het juiste gecomprimeerde bestandstype voor de brongegevens.

Als u een specifiek bestand wilt overbrengen naar Platform, selecteert u een map en selecteert u vervolgens het bestand dat u wilt opnemen. Tijdens deze stap kunt u ook een voorbeeld van de bestandsinhoud van andere bestanden in een bepaalde map bekijken met het voorvertoningspictogram naast een bestandsnaam.

Selecteer **[!UICONTROL Next]**.

+++

## Gegevens over gegevensstroom opgeven

De [!UICONTROL Dataflow detail] De pagina staat u toe om te selecteren of u een bestaande dataset of een nieuwe dataset wilt gebruiken. Tijdens dit proces kunt u ook uw gegevens configureren om in te voegen in Profiel en instellingen inschakelen zoals [!UICONTROL Error diagnostics], [!UICONTROL Partial ingestion], en [!UICONTROL Alerts].

### Een bestaande gegevensset gebruiken

Om gegevens in een bestaande dataset in te voeren, selecteer **[!UICONTROL Existing dataset]**. U kunt of een bestaande dataset terugwinnen gebruikend [!UICONTROL Advanced search] of door door de lijst van bestaande datasets in het dropdown menu te scrollen. Zodra u een dataset hebt geselecteerd, verstrek een naam en een beschrijving voor uw gegevensstroom.

![De bestaande gegevenssetinterface.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/existing-dataset.png)

### Een nieuwe gegevensset gebruiken

Om in een nieuwe dataset in te gaan, selecteer **[!UICONTROL New dataset]** en geef vervolgens een naam voor de uitvoergegevensset en een optionele beschrijving op. Selecteer vervolgens het schema waaraan u wilt toewijzen [!UICONTROL Advanced search] of door door de lijst van bestaande schema&#39;s in het dropdown menu te scrollen. Nadat u een schema hebt geselecteerd, geeft u een naam en een beschrijving voor de gegevensstroom op.

![De nieuwe datasetinterface.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/new-dataset.png)

### Profiel- en foutdiagnostiek inschakelen

+++Selecteer om stappen weer te geven om foutdiagnose en profielopname in te schakelen

Selecteer vervolgens de **[!UICONTROL Profile dataset]** Schakel deze optie in om uw gegevensset in te schakelen voor realtime klantprofiel. Hierdoor kunt u een holistische weergave maken van de kenmerken en het gedrag van een entiteit. De gegevens van alle profiel-toegelaten datasets zullen in Profiel worden omvat en de veranderingen worden toegepast wanneer u sparen uw gegevensstroom.

[!UICONTROL Error diagnostics] laat gedetailleerde foutenmelding generatie voor om het even welke onjuiste verslagen toe die in uw dataflow voorkomen, terwijl [!UICONTROL Partial ingestion] kunt u gegevens met fouten opnemen tot een bepaalde drempel die u handmatig definieert. Zie de [gedeeltelijke batch-opname, overzicht](../../../../../ingestion/batch-ingestion/partial.md) voor meer informatie .

+++

### Waarschuwingen inschakelen

+++Selecteren om stappen weer te geven voor het inschakelen van waarschuwingen

U kunt waarschuwingen inschakelen om meldingen te ontvangen over de status van uw gegevensstroom. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op berichten voor bronnen met behulp van de gebruikersinterface](../../alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw gegevensstroom, selecteert u **[!UICONTROL Next]**.

+++

## Gegevensvelden toewijzen aan een XDM-schema

De [!UICONTROL Mapping] de stap verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie [UI-hulplijn voor gegevensvoorinstelling](../../../../../data-prep/ui/mapping.md).

Als de brongegevens zijn toegewezen, selecteert u **[!UICONTROL Next]**.

![De toewijzingsinterface.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/mapping.png)

## Planninguitvoering

De [!UICONTROL Scheduling] de stap verschijnt, toestaand u om een innameprogramma te vormen om de geselecteerde brongegevens automatisch in te nemen gebruikend de gevormde afbeeldingen. Standaard is de planning ingesteld op `Once`. Selecteer **[!UICONTROL Frequency]** en selecteert u vervolgens een optie in het vervolgkeuzemenu.

>[!TIP]
>
>Interval en backfill zijn niet zichtbaar tijdens een eenmalige opname.

![De planningsinterface](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/schedule.png)

Als u de innamefrequentie instelt op `Minute`, `Hour`, `Day`, of `Week`dan moet u een interval instellen om een bepaald tijdkader tussen elke opname te bepalen. Bijvoorbeeld een innamefrequentie ingesteld op `Day` en een interval instellen op `15` betekent dat uw gegevensstroom gepland is om gegevens in te voeren om de 15 dagen.

Tijdens deze stap kunt u ook **backfill** en definieert u een kolom voor de incrementele opname van gegevens. Backfill wordt gebruikt om historische gegevens in te voeren, terwijl in de kolom die u voor incrementele inname definieert, nieuwe gegevens kunnen worden onderscheiden van bestaande gegevens.

Zie de lijst hieronder voor meer informatie over het plannen van configuraties.

| Veld | Beschrijving |
| --- | --- |
| Frequentie | De frequentie waarin inname plaatsvindt. Selecteerbare frequenties omvatten `Once`, `Minute`, `Hour`, `Day`, en `Week`. |
| Interval | Een geheel getal dat het interval voor de geselecteerde frequentie instelt. De waarde van het interval moet een geheel getal anders dan nul zijn en moet worden ingesteld op groter dan of gelijk aan 15. |
| Begintijd | Een UTC-tijdstempel die aangeeft wanneer de eerste opname wordt uitgevoerd. De begintijd moet groter zijn dan of gelijk zijn aan de huidige UTC-tijd. |
| Achtergrond | Een booleaanse waarde die bepaalt welke gegevens eerst worden ingevoerd. Als backfill is ingeschakeld, worden alle huidige bestanden in het opgegeven pad tijdens de eerste geplande inname opgenomen. Als terugvullen is uitgeschakeld, worden alleen de bestanden opgenomen die tussen de eerste opname en de begintijd worden geladen. Bestanden die vóór de begintijd zijn geladen, worden niet opgenomen. |

>[!NOTE]
>
>Voor batch-opname selecteert elke volgende gegevensstroom bestanden die van uw bron moeten worden ingepakt op basis van hun **laatst gewijzigd** tijdstempel. Dit betekent dat de batch-gegevens uitgezocht bestanden van de bron zijn die nieuw zijn of zijn gewijzigd sinds de laatste flowuitvoering. Bovendien moet u ervoor zorgen dat er voldoende tijd is tussen het uploaden van een bestand en een geplande doorloop, omdat bestanden die niet volledig naar uw account voor cloudopslag zijn geüpload voordat de geplande doorlooptijd wordt uitgevoerd, niet kunnen worden opgehaald voor opname.

Als u klaar bent met het configureren van uw innameschema, selecteert u **[!UICONTROL Next]**.

## Controleer uw gegevensstroom

De **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt controleren voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: Hiermee geeft u het brontype, het relevante pad van het gekozen bronbestand en de hoeveelheid kolommen in dat bronbestand weer.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt.
* **[!UICONTROL Scheduling]**: Hiermee geeft u de actieve periode, frequentie en interval van het innameschema weer.

Nadat u de gegevensstroom hebt gecontroleerd, klikt u op **[!UICONTROL Finish]** en laat enige tijd voor de gegevensstroom worden gecreeerd.

![De pagina Review.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/review.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een gegevensstroom gemaakt om batchgegevens van uw [!DNL Merkury] bron naar Experience Platform. Voor extra bronnen raadpleegt u de documentatie die hieronder wordt beschreven.

### Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamesnelheden, succes, en fouten te bekijken. Voor meer informatie over hoe te om dataflow te controleren, bezoek de zelfstudie op [het controleren van rekeningen en gegevensstromen in UI](../../monitor.md).

### Uw gegevensstroom bijwerken

Ga naar de zelfstudie voor het bijwerken van configuraties voor uw dataflows die plannen, toewijzingen en algemene informatie plannen [het bijwerken van bronnen dataflows in UI](../../update-dataflows.md)

### Uw gegevensstroom verwijderen

U kunt gegevensstromen schrappen die niet meer noodzakelijk of verkeerd gecreeerd gebruikend zijn **[!UICONTROL Delete]** functie beschikbaar in de **[!UICONTROL Dataflows]** werkruimte. Ga voor meer informatie over het verwijderen van gegevensstromen naar de zelfstudie op [gegevens verwijderen in de gebruikersinterface](../../delete.md).