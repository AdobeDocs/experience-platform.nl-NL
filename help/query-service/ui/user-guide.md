---
keywords: Experience Platform;home;popular topics;Query editor;query editor;Query service;query service;
solution: Experience Platform
title: Gebruikershandleiding voor de Query Editor
topic: query editor
description: De Redacteur van de vraag is een interactief hulpmiddel dat door de Dienst van de Vraag van Adobe Experience Platform wordt verstrekt, die u toestaat om, vragen voor klantenervaringsgegevens te schrijven te bevestigen en in werking te stellen binnen het gebruikersinterface van het Experience Platform. De Redacteur van de vraag steunt het ontwikkelen van vragen voor analyse en gegevensexploratie, en staat u toe om interactieve vragen voor ontwikkelingsdoeleinden evenals niet-interactieve vragen in werking te stellen om datasets in Experience Platform te bevolken.
translation-type: tm+mt
source-git-commit: f35443046a3d2bc5101d0fa2a58d07f4b6a31151
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 1%

---


# [!DNL Query Editor] gebruikershandleiding

[!DNL Query Editor] is een interactief hulpmiddel dat door Adobe Experience Platform wordt verstrekt  [!DNL Query Service], dat u toestaat om, vragen voor klantenervaringsgegevens binnen het  [!DNL Experience Platform] gebruikersinterface te schrijven te bevestigen en in werking te stellen. [!DNL Query Editor] ondersteunt het ontwikkelen van query&#39;s voor analyse en gegevensexploratie, en staat u toe om interactieve query&#39;s voor ontwikkelingsdoeleinden en niet-interactieve query&#39;s uit te voeren om datasets in te vullen  [!DNL Experience Platform].

Voor meer informatie over de concepten en de eigenschappen van [!DNL Query Service], zie [Overzicht van de Dienst van de Vraag][query-service-overview]. Meer over hoe te om het gebruikersinterface van de Dienst van de Vraag op [!DNL Platform] te navigeren, zie [overzicht UI van de Dienst van de Vraag][query-service-ui].

## Aan de slag

[!DNL Query Editor] verstrekt flexibele uitvoering van vragen door met te verbinden,  [!DNL Query Service]en de vragen zullen slechts lopen terwijl deze verbinding actief is.

### Verbinding maken met [!DNL Query Service]

[!DNL Query Editor] Het duurt een paar seconden om te initialiseren en verbinding te maken  [!DNL Query Service] wanneer het wordt geopend. De console vertelt u wanneer het wordt verbonden, zoals hieronder getoond. Als u probeert om een vraag in werking te stellen alvorens de redacteur heeft verbonden, vertraagt het uitvoering tot de verbinding volledig is.

![Image](../images/queries/query-editor-overview/initializing-connection.png)

### Hoe de vragen van [!DNL Query Editor] in werking worden gesteld

De vragen die van [!DNL Query Editor] worden uitgevoerd interactief. Dit betekent dat als u de browser sluit of wegnavigeert, de query wordt geannuleerd. Dit is ook waar voor vragen die worden gemaakt om datasets van vraagoutput te produceren.

## Ontwerpend van de vraag gebruikend [!DNL Query Editor]

Met [!DNL Query Editor] kunt u query&#39;s schrijven, uitvoeren en opslaan voor gegevens van de klantenervaring. Alle query&#39;s die worden uitgevoerd in [!DNL Query Editor] of worden opgeslagen, zijn beschikbaar voor alle gebruikers in uw organisatie met toegang tot [!DNL Query Service].

### Toegang tot het [!DNL Query Editor]

Klik in de gebruikersinterface [!DNL Experience Platform] op **[!UICONTROL Query&#39;s]** in het navigatiemenu links om de werkruimte [!DNL Query Service] te openen. Klik vervolgens op **[!UICONTROL Query maken]** rechtsboven in het scherm om query&#39;s te beginnen schrijven. Deze koppeling is beschikbaar op een van de pagina&#39;s in de werkruimte [!DNL Query Service].

![Afbeelding](../images/queries/query-editor-overview/create-query.png)

### Bezig met schrijven van query&#39;s

[!UICONTROL De ] Editor van de vraag is georganiseerd om het schrijven van vragen zo gemakkelijk mogelijk te maken. De schermafbeelding hieronder laat zien hoe de editor in de UI wordt weergegeven, met de knop **Afspelen** en het veld SQL-item gemarkeerd.

![Afbeelding](../images/queries/query-editor-overview/editor.png)

Om uw ontwikkelingstijd te minimaliseren, adviseert men dat u uw vragen met grenzen op de teruggekeerde rijen ontwikkelt. Bijvoorbeeld, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Nadat u hebt geverifieerd dat uw vraag de verwachte output veroorzaakt, verwijder de grenzen en stel de vraag met `CREATE TABLE tablename AS SELECT` in werking om een dataset met de output te produceren.

### Schrijfgereedschappen in [!DNL Query Editor]

- **Automatische syntaxismarkering:** maakt het lezen en ordenen van SQL eenvoudiger.

![Afbeelding](../images/queries/query-editor-overview/syntax-highlight.png)

- **SQL-sleutelwoord automatisch aanvullen:** typ de query en gebruik vervolgens de pijltoetsen om naar de gewenste term te navigeren en druk op  **Enter**.

![Afbeelding](../images/queries/query-editor-overview/syntax-auto.png)

- **Tabel en veld automatisch aanvullen:** typ de tabelnaam die u wilt  `SELECT` opgeven en navigeer met de pijltoetsen naar de gewenste tabel en druk op  **Enter**. Als een tabel eenmaal is geselecteerd, worden de velden in die tabel automatisch herkend.

![Afbeelding](../images/queries/query-editor-overview/tables-auto.png)

### Foutdetectie

[!DNL Query Editor] valideert automatisch een vraag aangezien u het schrijft, verstrekkend generische SQL bevestiging en specifieke uitvoeringsbevestiging. Als een rode onderstreping onder de query wordt weergegeven (zoals in de onderstaande afbeelding wordt getoond), vertegenwoordigt deze een fout binnen de query.

![Afbeelding](../images/queries/query-editor-overview/syntax-error-highlight.png)

Wanneer fouten worden ontdekt, kunt u de specifieke foutenmeldingen bekijken door over de SQL code te hangen.

![Afbeelding](../images/queries/query-editor-overview/linting-error.png)

### Query-details

Terwijl u een vraag in [!DNL Query Editor] bekijkt, **[!UICONTROL de Details van de Vraag]** verstrekt het paneel hulpmiddelen om de geselecteerde vraag te beheren.

![Afbeelding](../images/queries/query-editor-overview/query-details.png)

Dit paneel staat u toe om een outputdataset van UI direct te produceren, schrapt of noemt de getoonde vraag, en bekijkt de SQL code in een gemakkelijk te kopiëren formaat op **[!UICONTROL SQL Vraag]** tabel. In dit deelvenster worden ook nuttige metagegevens weergegeven, zoals de laatste keer dat de query werd gewijzigd en de eventuele wijziging. Om een dataset te produceren, klik **[!UICONTROL Dataset van de Output]**. Het dialoogvenster **[!UICONTROL Gegevensset uitvoer]** wordt weergegeven. Voer een naam en beschrijving in en klik vervolgens op **[!UICONTROL Query uitvoeren]**. De nieuwe dataset wordt getoond in **[!UICONTROL Datasets]** tabel op [!DNL Query Service] gebruikersinterface op [!DNL Platform].

### Bezig met opslaan van query&#39;s

[!DNL Query Editor] beschikt over een opslagfunctie waarmee u een query kunt opslaan en er later aan kunt werken. Als u een query wilt opslaan, klikt u op **[!UICONTROL Opslaan]** in de rechterbovenhoek van [!DNL Query Editor]. Voordat een query kan worden opgeslagen, moet een naam voor de query worden opgegeven met het deelvenster **[!UICONTROL Query Details]**.

### Hoe te om vorige vragen te vinden

Alle query&#39;s die worden uitgevoerd vanuit [!DNL Query Editor] worden vastgelegd in de logbestandentabel. U kunt de onderzoeksfunctionaliteit op **[!UICONTROL Logboek]** lusje gebruiken om vraaguitvoeringen te vinden. Opgeslagen query&#39;s worden weergegeven op het tabblad **[!UICONTROL Bladeren]**.

Zie [Overzicht van de Dienst UI van de Vraag][query-service-ui] voor meer informatie.

>[!NOTE]
>
>Vragen die niet worden uitgevoerd, worden niet opgeslagen in het logbestand. De query is alleen beschikbaar in [!DNL Query Service] als deze wordt uitgevoerd of opgeslagen in [!DNL Query Editor].

## Vragen uitvoeren met de Query Editor

Als u een query wilt uitvoeren in [!DNL Query Editor], kunt u SQL invoeren in de editor of een vorige query laden via het tabblad **[!UICONTROL Log]** of **[!UICONTROL Browse]** en op **Play** klikken. De status van de vraaguitvoering wordt getoond in **[!UICONTROL Console]** hieronder lusje, en de outputgegevens worden getoond in **[!UICONTROL Results]** tabel.

### Console

De console verstrekt informatie over de status en de verrichting van [!DNL Query Service]. De console toont de verbindingsstatus aan [!DNL Query Service], vraagverrichtingen die, en om het even welke foutenmeldingen worden uitgevoerd die uit die vragen voortvloeien.

![Afbeelding](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>De console toont slechts fouten die uit het uitvoeren van een vraag voortkwamen. Er worden geen fouten met de queryvalidatie weergegeven voordat een query wordt uitgevoerd.

### Zoekresultaten

Nadat een vraag heeft voltooid, worden de resultaten getoond in **[!UICONTROL Resultaten]** lusje, naast **[!UICONTROL Console]** tabel. In deze weergave wordt de tabeluitvoer van uw query weergegeven, met maximaal 100 rijen. In deze weergave kunt u controleren of de query de verwachte uitvoer oplevert. Om een dataset met uw vraag te produceren, verwijder grenzen op teruggekeerde rijen, en stel de vraag met `CREATE TABLE tablename AS SELECT` in werking om een dataset met de output te produceren. Zie [het produceren van datasetleerprogramma][query-service-create-datasets] voor instructies op hoe te om een dataset van vraagresultaten in [!DNL Query Editor] te produceren.

![Afbeelding](../images/queries/query-editor-overview/query-results.png)

## Zoekopdrachten uitvoeren met zelfstudie [!DNL Query Service]

In de volgende video ziet u hoe u query&#39;s uitvoert in de Adobe Experience Platform-interface en in een PSQL-client. Bovendien wordt het gebruik van individuele eigenschappen in een XDM-object, met gebruik van door Adobe gedefinieerde functies en het gebruik van CREATE TABLE AS SELECT (CTAS) aangetoond.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Volgende stappen

Nu u weet welke functies beschikbaar zijn in [!DNL Query Editor] en hoe u door de toepassing kunt navigeren, kunt u uw eigen query&#39;s rechtstreeks schrijven in [!DNL Platform]. Voor meer informatie over het runnen van SQL vragen tegen datasets in [!DNL Data Lake], zie de gids op [lopende query][query-service-running-queries].

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../best-practices/writing-queries.md
[query-service-create-datasets]: ./create-datasets.md
