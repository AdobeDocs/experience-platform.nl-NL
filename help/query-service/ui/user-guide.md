---
keywords: Experience Platform;home;popular topics;Query editor;query editor
solution: Experience Platform
title: Gebruikershandleiding voor de Query Editor
topic: query editor
description: De Redacteur van de vraag is een interactief hulpmiddel dat door de Dienst van de Vraag van Adobe Experience Platform wordt verstrekt, die u toestaat om, vragen voor klantenervaringsgegevens te schrijven te bevestigen en in werking te stellen binnen het gebruikersinterface van het Experience Platform. De Redacteur van de vraag steunt het ontwikkelen van vragen voor analyse en gegevensexploratie, en staat u toe om interactieve vragen voor ontwikkelingsdoeleinden evenals niet-interactieve vragen in werking te stellen om datasets in Experience Platform te bevolken.
translation-type: tm+mt
source-git-commit: 3376d6cace9ab196f457e2bf7b84cde06693103c
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 1%

---


# [!DNL Query Editor] gebruikershandleiding

[!DNL Query Editor] is een interactief hulpmiddel dat door Adobe Experience Platform wordt verstrekt [!DNL Query Service], dat u toestaat om, vragen voor de gegevens van de klantenervaring binnen het [!DNL Experience Platform] gebruikersinterface te schrijven te bevestigen en in werking te stellen. [!DNL Query Editor] ondersteunt het ontwikkelen van query&#39;s voor analyse en gegevensexploratie, en staat u toe om interactieve query&#39;s voor ontwikkelingsdoeleinden en niet-interactieve query&#39;s uit te voeren om datasets in te vullen [!DNL Experience Platform].

Voor meer informatie over de concepten en de eigenschappen van [!DNL Query Service], zie het overzicht [van de Dienst van de][query-service-overview]Vraag. Meer over hoe te om het gebruikersinterface van de Dienst van de Vraag te navigeren [!DNL Platform], zie het overzicht [UI van de Dienst van de][query-service-ui]Vraag.

## Aan de slag

[!DNL Query Editor] verstrekt flexibele uitvoering van vragen door met te verbinden, [!DNL Query Service]en de vragen zullen slechts lopen terwijl deze verbinding actief is.

### Verbinding maken met [!DNL Query Service]

[!DNL Query Editor] Het duurt een paar seconden om te initialiseren en verbinding te maken [!DNL Query Service] wanneer het wordt geopend. De console vertelt u wanneer het wordt verbonden, zoals hieronder getoond. Als u probeert om een vraag in werking te stellen alvorens de redacteur heeft verbonden, vertraagt het uitvoering tot de verbinding volledig is.

![Image](../images/queries/query-editor-overview/initializing-connection.png)

### Hoe de vragen van in werking worden gesteld [!DNL Query Editor]

De vragen die van looppas interactively worden uitgevoerd. [!DNL Query Editor] Dit betekent dat als u de browser sluit of wegnavigeert, de query wordt geannuleerd. Dit is ook waar voor vragen die worden gemaakt om datasets van vraagoutput te produceren.

## Query schrijven met [!DNL Query Editor]

Gebruikend [!DNL Query Editor], kunt u schrijven, uitvoeren en sparen vragen voor de gegevens van de klantenervaring. Alle query&#39;s die worden uitgevoerd in [!DNL Query Editor]of opgeslagen, zijn beschikbaar voor alle gebruikers in uw organisatie die toegang hebben tot [!DNL Query Service].

### Toegang tot [!DNL Query Editor]

Klik in de [!DNL Experience Platform] gebruikersinterface op **[!UICONTROL Vragen]** in het navigatiemenu links om de [!DNL Query Service] werkruimte te openen. Klik vervolgens **[!UICONTROL op Query]** maken rechtsboven in het scherm om query&#39;s te schrijven. Deze koppeling is beschikbaar op alle pagina&#39;s in de [!DNL Query Service] werkruimte.

![Image](../images/queries/query-editor-overview/create-query.png)

### Bezig met schrijven van query&#39;s

[!UICONTROL De redacteur] van de vraag wordt georganiseerd om het schrijven vragen zo gemakkelijk mogelijk te maken. In de onderstaande schermafbeelding ziet u hoe de editor in de gebruikersinterface wordt weergegeven, met de knop **Afspelen** en het veld SQL-item gemarkeerd.

![Image](../images/queries/query-editor-overview/editor.png)

Om uw ontwikkelingstijd te minimaliseren, adviseert men dat u uw vragen met grenzen op de teruggekeerde rijen ontwikkelt. Bijvoorbeeld, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Nadat u hebt geverifieerd dat uw vraag de verwachte output veroorzaakt, verwijder de grenzen en stel de vraag met in werking `CREATE TABLE tablename AS SELECT` om een dataset met de output te produceren.

### Schrijfgereedschappen in [!DNL Query Editor]

- **Automatische syntaxismarkering:** Maakt het lezen en ordenen van SQL gemakkelijker.

![Image](../images/queries/query-editor-overview/syntax-highlight.png)

- **SQL-trefwoord automatisch aanvullen:** Begin het typen van uw vraag dan de pijlsleutels te gebruiken om aan de gewenste termijn te navigeren en **binnengaan** te drukken.

![Image](../images/queries/query-editor-overview/syntax-auto.png)

- **Tabel en veld automatisch aanvullen:** Typ de tabelnaam die u wilt `SELECT` gebruiken en navigeer naar de gewenste tabel met de pijltoetsen. Druk op **Enter**. Als een tabel eenmaal is geselecteerd, worden de velden in die tabel automatisch herkend.

![Image](../images/queries/query-editor-overview/tables-auto.png)

### Foutdetectie

[!DNL Query Editor] valideert automatisch een vraag aangezien u het schrijft, verstrekkend generische SQL bevestiging en specifieke uitvoeringsbevestiging. Als een rode onderstreping onder de query wordt weergegeven (zoals in de onderstaande afbeelding wordt getoond), vertegenwoordigt deze een fout binnen de query.

![Image](../images/queries/query-editor-overview/syntax-error-highlight.png)

Wanneer fouten worden ontdekt, kunt u de specifieke foutenmeldingen bekijken door over de SQL code te hangen.

![Image](../images/queries/query-editor-overview/linting-error.png)

### Query-details

Terwijl u een query bekijkt in [!DNL Query Editor], bevat het deelvenster *[!UICONTROL Query-details]* gereedschappen voor het beheer van de geselecteerde query.

![Image](../images/queries/query-editor-overview/query-details.png)

In dit deelvenster kunt u rechtstreeks vanuit de gebruikersinterface een uitvoergegevensset genereren, de weergegeven query verwijderen of een naam geven en de SQL-code in een gemakkelijk te kopiëren indeling weergeven op het tabblad *[!UICONTROL SQL-query]* . In dit deelvenster worden ook nuttige metagegevens weergegeven, zoals de laatste keer dat de query werd gewijzigd en de eventuele wijziging. Als u een gegevensset wilt genereren, klikt u op Gegevensset **[!UICONTROL Uitvoer]**. Het dialoogvenster *[!UICONTROL Uitvoergegevensset]* wordt geopend. Voer een naam en beschrijving in en klik vervolgens op **[!UICONTROL Query]** uitvoeren. De nieuwe dataset wordt getoond in het lusje van *[!UICONTROL Datasets]* op het [!DNL Query Service] gebruikersinterface op [!DNL Platform].

### Bezig met opslaan van query&#39;s

[!DNL Query Editor] beschikt over een opslagfunctie waarmee u een query kunt opslaan en er later aan kunt werken. Als u een query wilt opslaan, klikt u op **[!UICONTROL Opslaan]** in de rechterbovenhoek van [!DNL Query Editor]. Voordat een query kan worden opgeslagen, moet u een naam opgeven voor de query via het deelvenster *[!UICONTROL Query-details]* .

### Hoe te om vorige vragen te vinden

Alle query&#39;s die vanuit [!DNL Query Editor] worden uitgevoerd, worden vastgelegd in de logbestandentabel. U kunt de zoekfunctionaliteit op het tabblad *[!UICONTROL Logboek]* gebruiken om query-uitvoeringen te zoeken. Opgeslagen query&#39;s worden weergegeven op het tabblad *[!UICONTROL Bladeren]* .

Zie het overzicht [van de Dienst van de][query-service-ui] Vraag UI voor meer informatie.

>[!NOTE]
>
>Vragen die niet worden uitgevoerd, worden niet opgeslagen in het logbestand. De query is alleen beschikbaar in [!DNL Query Service]als deze wordt uitgevoerd of opgeslagen in [!DNL Query Editor].

## Vragen uitvoeren met de Query Editor

Als u een query wilt uitvoeren in, [!DNL Query Editor]kunt u SQL invoeren in de editor of een vorige query laden via het tabblad *Logboek* of *[!UICONTROL Bladeren]* en op **Afspelen** klikken. De status van de vraaguitvoering wordt getoond op het lusje van de *[!UICONTROL Console]* hieronder, en de outputgegevens worden getoond op het lusje van *[!UICONTROL Resultaten]* .

### Console

De console verstrekt informatie over de status en de verrichting van [!DNL Query Service]. De console toont de verbindingsstatus aan [!DNL Query Service], vraagverrichtingen die, en om het even welke foutenmeldingen worden uitgevoerd die uit die vragen voortvloeien.

![Image](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>De console toont slechts fouten die uit het uitvoeren van een vraag voortkwamen. Er worden geen fouten met de queryvalidatie weergegeven voordat een query wordt uitgevoerd.

### Zoekresultaten

Nadat een query is voltooid, worden de resultaten weergegeven op het tabblad *[!UICONTROL Resultaten]* , naast het tabblad *[!UICONTROL Console]* . In deze weergave wordt de tabeluitvoer van uw query weergegeven, met maximaal 100 rijen. In deze weergave kunt u controleren of de query de verwachte uitvoer oplevert. Om een dataset met uw vraag te produceren, verwijder grenzen op teruggekeerde rijen, en stel de vraag met in werking `CREATE TABLE tablename AS SELECT` om een dataset met de output te produceren. Zie het [produceren datasetleerprogramma][query-service-create-datasets] voor instructies op hoe te om een dataset van vraagresultaten in te produceren [!DNL Query Editor].

![Image](../images/queries/query-editor-overview/query-results.png)

## Zoekopdrachten uitvoeren met [!DNL Query Service] zelfstudievideo

In de volgende video ziet u hoe u query&#39;s uitvoert in de Adobe Experience Platform-interface en in een PSQL-client. Bovendien wordt het gebruik van individuele eigenschappen in een XDM-object, met gebruik van door Adobe gedefinieerde functies en het gebruik van CREATE TABLE AS SELECT (CTAS) aangetoond.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Volgende stappen

Nu u weet welke functies beschikbaar zijn in [!DNL Query Editor] en hoe u door de toepassing kunt navigeren, kunt u uw eigen query&#39;s rechtstreeks schrijven [!DNL Platform]. Voor meer informatie over het runnen van SQL vragen tegen datasets binnen [!DNL Data Lake], zie de gids bij het [runnen van vragen][query-service-running-queries]. Zie de [voorbeeldquery][query-service-sample-queries]&#39;s voor voorbeeld-SQL-query&#39;s voor het werken met Adobe Analytics- en Adobe Target-gegevens.

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
