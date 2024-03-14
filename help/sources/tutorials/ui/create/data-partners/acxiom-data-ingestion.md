---
title: Acxiale gegevensinname
description: Gebruik de Opname van Gegevens van Acxiom om gegevens van Acxiom in Real-Time CDP in te voeren en verrijkt first-party profielen. Gebruik uw door Acxiom verrijkte first-party profielen om het publiek te verbeteren en over marketing kanalen te activeren.
last-substantial-update: 2024-03-19T00:00:00Z
badge: Beta
source-git-commit: 9916e882e5ef31d14dc3df0f24275995c0b6d5ca
workflow-type: tm+mt
source-wordcount: '1767'
ht-degree: 0%

---

# Een [!DNL Acxiom Data Ingestion] bronverbinding en gegevensstroom in de gebruikersinterface

>[!NOTE]
>
>De [!DNL Acxiom Data Ingestion] De bron is in bèta. Lees de [voorwaarden](../../../../home.md#terms-and-conditions) in het overzicht van bronnen voor meer informatie over het gebruik van bronnen met een bètalabel.

Gebruik de [!DNL Acxiom Data Ingestion] bron voor invoer [!DNL Acxiom] gegevens naar Real-time Customer Data Platform en verrijken profielen van eerste partijen. Vervolgens kunt u uw [!DNL Acxiom]- verrijkte first-party profielen om publiek te verbeteren en over marketing kanalen te activeren.

Lees deze zelfstudie om te leren hoe u een [!DNL Acxiom Data Ingestion] bronverbinding en gegevensstroom via de Adobe Experience Platform-gebruikersinterface. De [!DNL Acxiom Data Ingestion] bron wordt gebruikt om reactie van terug te winnen en in kaart te brengen [!DNL Acxiom] verbeteringsdienst die Amazon S3 als dalingspunt gebruikt.

## Vereisten {#prerequisites}

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

### Vereiste referenties verzamelen

Om tot uw emmer op Experience Platform toegang te hebben, moet u geldige waarden voor de volgende geloofsbrieven verstrekken:

| Credentials | Beschrijving |
| --- | --- |
| [!DNL Acxiom] verificatiesleutel | De verificatiesleutel. U kunt deze waarde ophalen uit het dialoogvenster [!DNL Acxiom] team. |
| [!DNL Amazon S3] toegangstoets | De toegangs belangrijkste identiteitskaart voor uw emmer. U kunt deze waarde ophalen uit het dialoogvenster [!DNL Acxiom] team. |
| [!DNL Amazon S3] geheime sleutel | De geheime sleutel-id voor uw emmer. U kunt deze waarde ophalen uit het dialoogvenster [!DNL Acxiom] team. |
| Naam van emmertje | Dit is uw emmertje waar de dossiers zullen worden gedeeld. U kunt deze waarde ophalen uit het dialoogvenster [!DNL Acxiom] team. |

>[!IMPORTANT]
>
>U moet beide hebben **[!UICONTROL View Sources]** en **[!UICONTROL Manage Sources]** machtigingen die zijn ingeschakeld voor uw account om verbinding te maken met uw [!DNL Acxiom] aan Experience Platform. Neem contact op met de productbeheerder om de benodigde machtigingen te verkrijgen. Lees voor meer informatie de [gebruikershandleiding voor toegangsbeheer](../../../../../access-control/ui/overview.md).

## Verbind uw [!DNL Acxiom] account

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de **[!UICONTROL Data & Identity Partners]** categorie, selecteert u **[!UICONTROL Acxiom Data Ingestion]** en selecteer vervolgens **[!UICONTROL Set up]**.

>[!TIP]
>
>Een bronkaart die **[!UICONTROL Add data]** betekent dat de bron al een geverifieerde account heeft. Aan de andere kant een bronkaart die **[!UICONTROL Set up]** betekent dat u gebruikersgegevens moet opgeven en een nieuw account moet maken om die bron te kunnen gebruiken.

![De broncatalogus met de geselecteerde Acxiom-bron.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-catalog.png)

### Een nieuwe account maken

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New account]**. Geef op het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Acxiom] referenties. Selecteer **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![De nieuwe accountinterface van de workflow voor bronnen.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-new-account.png)

| Credentials | Beschrijving |
| --- | --- |
| Accountnaam | De naam van de account. |
| Beschrijving | (Optioneel) Een korte toelichting van het doel van de rekening. |
| [!DNL Acxiom] verificatiesleutel | De [!DNL Acxiom]-geleverde sleutel vereist voor accountgoedkeuring. Dit moet overeenkomen met de juiste waarde voordat een verbinding met de database tot stand kan worden gebracht.  Deze sleutel moet 24 tekens lang zijn en mag alleen bestaan uit: A-Z, a-z en 0-9. |
| S3-toegangstoets | De S3 toegangstoets verwijst naar de Amazon S3 locatie. Dit wordt verstrekt door uw beheerder wanneer de S3 roltoestemmingen worden bepaald. |
| S3, geheime sleutel | De geheime sleutel S3 verwijst naar de plaats van Amazon S3. Dit wordt verstrekt door uw beheerder wanneer de S3 roltoestemmingen worden bepaald. |
| s3SessionToken | (Optioneel) De waarde van het verificatietoken bij verbinding met S3. |
| serviceUrl | (Optioneel) De URL-locatie die moet worden gebruikt wanneer verbinding wordt gemaakt met S3 op een niet-standaardlocatie. |
| Naam van emmertje | (Optioneel) De naam van het S3-emmertje dat is ingesteld op S3 en dat fungeert als beginpad voor gegevensselectie. |
| Mappad | Als submappen in een emmertje worden gebruikt, kunt u ook een pad opgeven als beginpad in de gegevensselectie. |

### Een bestaande account gebruiken

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]**.

Selecteer een account in de lijst om details over dat account weer te geven. Als u een account hebt geselecteerd, selecteert u **[!UICONTROL Next]** om verder te gaan.

![De bestaande accountinterface van de workflow voor bronnen.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-existing-account.png)

## Gegevens selecteren

Selecteer het bestand dat u wilt opnemen in het gewenste emmertje en de gewenste submap. U kunt een voorbeeld van de gegevens weergeven wanneer het scheidingsteken en het compressietype zijn gedefinieerd. Als u het bestand hebt geselecteerd, selecteert u **[!UICONTROL Next]** om verder te gaan.

![De interface voor het selecteren van gegevens en het voorvertonen van bestanden van de workflow voor bronnen.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-preview.png)

>[!NOTE]
>
>Terwijl de bestandstypen JSON en Parquet worden vermeld, bent u niet verplicht of verwacht deze te gebruiken tijdens het [!DNL Acxiom] bronworkflow.

## Gegevensset en gegevens over gegevensstroom opgeven

Daarna, moet u informatie betreffende uw dataset en uw gegevensstroom verstrekken.

### Gegevens over gegevensset

>[!BEGINTABS]

>[!TAB Een nieuwe gegevensset gebruiken]

Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. De gegevens die met succes in Experience Platform worden opgenomen worden voortgeduurd binnen het gegevensmeer als datasets. Als u een nieuwe gegevensset wilt gebruiken, selecteert u **[!UICONTROL New dataset]**.

![De nieuwe datasetinterface.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-new-dataset.png)

| Nieuwe gegevens gegevensset | Beschrijving |
| --- | --- |
| Naam uitvoergegevensset | De naam van de nieuwe dataset. |
| Beschrijving | (Optioneel) Een korte toelichting van het doel van de gegevensset. |
| Schema | Een vervolgkeuzelijst met schema&#39;s die in uw organisatie bestaan. U kunt ook uw eigen schema vóór het proces van de bronconfiguratie maken. Lees voor meer informatie de handleiding op [schema maken in de gebruikersinterface](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Een bestaande gegevensset gebruiken]

Als u een bestaande gegevensset wilt gebruiken, selecteert u **[!UICONTROL Existing dataset]**.

U kunt **[!UICONTROL Advanced search]** om een venster van alle datasets te bekijken uw organisatie, met inbegrip van hun respectieve details zoals of zij voor opname aan het Profiel van de Klant in real time worden toegelaten.

![De bestaande gegevenssetinterface.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-dataset.png)

>[!ENDTABS]

+++Selecteer voor stappen om de opname van het Profiel, de diagnostiek van de fout, en gedeeltelijke opname toe te laten.

Als uw dataset voor het Profiel van de Klant in real time wordt toegelaten, dan tijdens deze stap, kunt u van een knevel voorzien **[!UICONTROL Profile dataset]** om uw gegevens in te schakelen voor profielopname. U kunt deze stap ook gebruiken om **[!UICONTROL Error diagnostics]** en **[!UICONTROL Partial ingestion]**.

* **[!UICONTROL Error diagnostics]**: Select **[!UICONTROL Error diagnostics]** om de bron op te dragen om foutendiagnostiek te veroorzaken die u wanneer het controleren van uw datasetactiviteit en dataflow status kunt later van verwijzingen voorzien.
* **[!UICONTROL Partial ingestion]**: Gedeeltelijke batch-opname is de mogelijkheid om gegevens met fouten in te voeren, tot een bepaalde configureerbare drempel. Met deze functie kunt u al uw nauwkeurige gegevens in het Experience Platform opnemen, terwijl al uw onjuiste gegevens afzonderlijk worden opgeslagen met informatie over waarom deze niet geldig zijn.

+++

### Gegevens gegevensstroom

Zodra uw dataset wordt gevormd, moet u details op uw gegevensstroom, met inbegrip van een naam, een facultatieve beschrijving, en waakzame configuraties dan verstrekken.

![De interface van de dataflow-detailconfiguraties.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-dataset-details.png)

| Dataflow-configuraties | Beschrijving |
| --- | --- |
| Naam gegevensstroom | De naam van de gegevensstroom.  Standaard wordt hiervoor de naam gebruikt van het bestand dat wordt geïmporteerd. |
| Beschrijving | (Optioneel) Een korte beschrijving van uw gegevensstroom. |
| Waarschuwingen | Experience Platform kan op gebeurtenissen gebaseerde waarschuwingen produceren waarop gebruikers zich kunnen abonneren. Deze opties zijn allemaal een doorlopende gegevensstroom om deze waarschuwingen te activeren.  Lees voor meer informatie de [waarschuwingsoverzicht](../../alerts.md) <ul><li>**Bronnen DataAfter Run Start**: Selecteer deze waarschuwing om een melding te ontvangen wanneer de dataflow-run begint.</li><li>**Bronnen DataAfterFlow voltooid**: Selecteer deze waarschuwing om een melding te ontvangen als de gegevensstroom zonder fouten eindigt.</li><li>**Bronnen DataAfterFlow-fout**: Selecteer deze waarschuwing als u een melding wilt ontvangen als de uitvoering van de gegevensstroom eindigt met fouten.</li></ul> |

## Toewijzing

Gebruik de toewijzingsinterface om uw brongegevens toe te wijzen aan de aangewezen schemagebieden alvorens gegevens aan Experience Platform in te voeren.  Lees voor meer informatie de [toewijzingshulplijn in de gebruikersinterface](../../../../../data-prep/ui/mapping.md)

![De toewijzingsinterface.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-mapping.png)

## Plaats uw gegevensstroomopname

Daarna, gebruik de het plannen interface om het innameprogramma van uw dataflow te bepalen.

![De plannende configuratieinterface.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-scheduling.png)

| Configuratie plannen | Beschrijving |
| --- | --- |
| Frequentie | Vorm frequentie om erop te wijzen hoe vaak dataflow zou moeten lopen. U kunt de frequentie instellen op: <ul><li>**Eenmaal**: Stel de frequentie in op `once` een eenmalige opname maken. Configuraties voor interval en backfill zijn niet beschikbaar wanneer u een eenmalige gegevensstroom maakt. Standaard wordt de planningsfrequentie ingesteld op één keer.</li><li>**Minute**: Stel de frequentie in op `minute` om uw gegevensstroom te plannen om gegevens per minuut in te voeren.</li><li>**Uur**:Stel de frequentie in op `hour` om uw gegevensstroom te plannen om gegevens op een per-uurbasis in te voeren.</li><li>**Dag**: Stel de frequentie in op `day` om uw gegevensstroom te plannen om gegevens per dag in te voeren.</li><li>**Week**: Stel de frequentie in op `week` om uw gegevensstroom te plannen om gegevens per week in te voeren.</li></ul> |
| Interval | Zodra u een frequentie selecteert, kunt u het interval dat dan vormen om het tijdkader tussen elke opname te vestigen. Bijvoorbeeld, als u uw frequentie aan dag plaatst en het interval aan 15 vormt, dan zal uw dataflow om de 15 dagen lopen. **Opmerking**: U kunt interval niet instellen op nul. |
| Begintijd | Het tijdstempel voor de geprojecteerde run, weergegeven in UTC-tijdzone. |
| Achtergrond | Met Backfill wordt bepaald welke gegevens in eerste instantie worden ingevoerd. Als backfill is ingeschakeld, worden alle huidige bestanden in het opgegeven pad tijdens de eerste geplande inname opgenomen. Als terugvullen is uitgeschakeld, worden alleen de bestanden opgenomen die tussen de eerste opname en de begintijd worden geladen. Bestanden die vóór de begintijd zijn geladen, worden niet opgenomen. |

## Controleer uw gegevensstroom

Gebruik de overzichtspagina voor een samenvatting van uw gegevensstroom voorafgaand aan opname. De details worden gegroepeerd in de volgende categorieën:

* **Verbinding** - Geeft het brontype, het relevante pad van het gekozen bronbestand en het aantal kolommen in dat bronbestand weer.
* **Gegevensset- en kaartvelden toewijzen** - Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt.
* **Planning** - Geeft aan dat de actieve periode, frequentie en interval van het innameschema
Nadat u de gegevensstroom hebt gereviseerd, klikt u op Voltooien en wacht u enige tijd tot de gegevensstroom is gemaakt.

![De pagina Review.](../../../../images/tutorials/create/acxiom-data-enhancement-import/image-source-review.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een gegevensstroom gemaakt om batchgegevens van uw [!DNL Acxiom] bron naar Experience Platform. Voor extra bronnen raadpleegt u de documentatie die hieronder wordt beschreven.

### Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamesnelheden, succes, en fouten te bekijken. Voor meer informatie over hoe te om dataflow te controleren, bezoek de zelfstudie op [het controleren van rekeningen en gegevensstromen in UI](../../../../../dataflows/ui/monitor-sources.md).

### Uw gegevensstroom bijwerken

Ga naar de zelfstudie voor het bijwerken van configuraties voor uw dataflows die plannen, toewijzingen en algemene informatie plannen [het bijwerken van bronnen dataflows in UI](../../update-dataflows.md).

### Uw gegevensstroom verwijderen

U kunt gegevensstromen schrappen die niet meer noodzakelijk of verkeerd gecreeerd gebruikend zijn **[!UICONTROL Delete]** functie beschikbaar in de **[!UICONTROL Dataflows]** werkruimte. Ga voor meer informatie over het verwijderen van gegevensstromen naar de zelfstudie op [gegevens verwijderen in de gebruikersinterface](../../delete.md).

## Aanvullende bronnen {#additional-resources}

Lees voor meer informatie de [[!DNL Acxiom] InfoBase](https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf).
