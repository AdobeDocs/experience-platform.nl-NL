---
keywords: Experience Platform;thuis;populaire onderwerpen;de redacteur van de vraag;de vraagredacteur;de dienst van de vraag;de vraagdienst;
solution: Experience Platform
title: UI-gids voor zoekprogramma
description: De redacteur van de Vraag is een interactief hulpmiddel dat door de Dienst van de Vraag van Adobe Experience Platform wordt verstrekt, die u toestaat om, vragen voor klantenervaringsgegevens binnen het gebruikersinterface van het Experience Platform te schrijven te bevestigen en in werking te stellen. De Redacteur van de vraag steunt het ontwikkelen van vragen voor analyse en gegevensexploratie, en staat u toe om interactieve vragen voor ontwikkelingsdoeleinden evenals niet-interactieve vragen in werking te stellen om datasets in Experience Platform te bevolken.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: ff4b528a0456f46d8c99e5921cfc99b197956ba6
workflow-type: tm+mt
source-wordcount: '1626'
ht-degree: 0%

---

# [!DNL Query Editor] UI-hulplijn

[!DNL Query Editor] is een interactief hulpmiddel dat door Adobe Experience Platform wordt verstrekt [!DNL Query Service], die u toestaat schrijven, bevestigen, en vragen voor de gegevens van de klantenervaring binnen [!DNL Experience Platform] gebruikersinterface. [!DNL Query Editor] steunt het ontwikkelen van vragen voor analyse en gegevensonderzoek, en staat u toe om interactieve vragen voor ontwikkelingsdoeleinden evenals niet-interactieve vragen in werking te stellen om datasets in te vullen [!DNL Experience Platform].

Voor meer informatie over de concepten en kenmerken van [!DNL Query Service], zie de [Overzicht van Query Service](../home.md). Om meer over te leren hoe te om het gebruikersinterface van de Dienst van de Vraag te navigeren [!DNL Platform], zie de [Overzicht van Query Service](./overview.md).

## Aan de slag {#getting-started}

[!DNL Query Editor] verstrekt flexibele uitvoering van vragen door met te verbinden [!DNL Query Service]en query&#39;s worden alleen uitgevoerd als deze verbinding actief is.

### Verbinding maken met [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] duurt een paar seconden om te initialiseren en verbinding te maken met [!DNL Query Service] wanneer het wordt geopend. De console vertelt u wanneer het wordt aangesloten, zoals hieronder getoond. Als u probeert om een vraag in werking te stellen alvorens de redacteur heeft verbonden, vertraagt het uitvoering tot de verbinding volledig is.

![De consoleoutput van de Redacteur van de Vraag op aanvankelijke verbinding.](../images/ui/query-editor/connect.png)

### Hoe de vragen van in werking worden gesteld [!DNL Query Editor] {#run-a-query}

Zoekopdrachten uitgevoerd vanuit [!DNL Query Editor] interactief uitvoeren. Dit betekent dat als u de browser sluit of wegnavigeert, de query wordt geannuleerd. Dit is ook waar voor vragen die worden gemaakt om datasets van vraagoutput te produceren.

## Query schrijven met [!DNL Query Editor] {#query-authoring}

Gebruiken [!DNL Query Editor], kunt u schrijven, uitvoeren, en sparen vragen voor de gegevens van de klantenervaring. Alle query&#39;s uitgevoerd of opgeslagen in [!DNL Query Editor] zijn beschikbaar voor alle gebruikers in uw organisatie die toegang hebben tot [!DNL Query Service].

### Toegang tot het [!DNL Query Editor] {#accessing-query-editor}

In de [!DNL Experience Platform] UI, selecteer **[!UICONTROL Queries]** in het navigatiemenu links om het dialoogvenster [!DNL Query Service] werkruimte. Selecteer vervolgens **[!UICONTROL Create Query]** rechtsboven in het scherm om query&#39;s te schrijven. Deze koppeling is beschikbaar op alle pagina&#39;s in het dialoogvenster [!DNL Query Service] werkruimte.

![Het tabblad Overzicht van de werkruimte Vragen met de markering Query maken.](../images/ui/query-editor/create-query.png)

### Bezig met schrijven van query&#39;s {#writing-queries}

[!UICONTROL Query Editor] is georganiseerd om het schrijven van vragen zo gemakkelijk mogelijk te maken. In de onderstaande schermafbeelding ziet u hoe de editor in de gebruikersinterface wordt weergegeven, met het veld voor SQL-invoer en **Afspelen** gemarkeerd.

![De Redacteur van de Vraag met het SQL inputgebied en Spel benadrukt.](../images/ui/query-editor/editor.png)

Om uw ontwikkelingstijd te minimaliseren, adviseert men dat u uw vragen met grenzen op de teruggekeerde rijen ontwikkelt. Bijvoorbeeld, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Nadat u hebt gecontroleerd dat uw vraag de verwachte output veroorzaakt, verwijder de grenzen en stel de vraag met in werking `CREATE TABLE tablename AS SELECT` om een dataset met de output te produceren.

### Schrijfgereedschappen in [!DNL Query Editor] {#writing-tools}

- **Automatische syntaxismarkering:** Maakt het lezen en ordenen van SQL gemakkelijker.

![Een SQL-instructie in de Query Editor die de syntaxiskleurmarkering aangeeft.](../images/ui/query-editor/syntax-highlight.png)

- **SQL trefwoord automatisch aanvullen:** Begin uw vraag te typen dan de pijlsleutels te gebruiken om aan de gewenste termijn te navigeren en te drukken **Enter**.

![Een paar tekens van SQL met het automatische volledige vervolgkeuzemenu dat opties van de Redacteur van de Vraag verstrekt.](../images/ui/query-editor/syntax-auto.png)

- **Tabel en veld automatisch aanvullen:** Typ de tabelnaam die u wilt gebruiken `SELECT` van, dan gebruik de pijlsleutels om aan de lijst te navigeren u zoekt, en drukt **Enter**. Als een tabel eenmaal is geselecteerd, worden de velden in die tabel automatisch herkend.

![De invoer van de Redacteur van de Vraag die drop-down lijstnaamsuggesties toont.](../images/ui/query-editor/tables-auto.png)

### Configuratieschakeloptie voor UI automatisch aanvullen {#auto-complete}

De [!DNL Query Editor] stelt automatisch potentiële SQL sleutelwoorden samen met lijst of kolomdetails voor de vraag voor aangezien u het schrijft. De functie voor automatisch aanvullen is standaard ingeschakeld en kan op elk gewenst moment worden uitgeschakeld of ingeschakeld door de optie [!UICONTROL Syntax auto-complete] knevel aan het hoogste recht van de Redacteur van de Vraag.

De auto-volledige configuratie het plaatsen is per gebruiker en voor de opeenvolgende logins voor die gebruiker herinnerd.

![De Redacteur van de vraag met de syntaxis auto-volledige knevel benadrukt.](../images/ui/query-editor/auto-complete-toggle.png)

Als u deze functie uitschakelt, worden meerdere metagegevensopdrachten niet verwerkt en worden aanbevelingen gedaan die de snelheid van de auteur bij het bewerken van query&#39;s ten goede komen.

Wanneer u de schakeloptie gebruikt om de functie voor automatisch aanvullen in te schakelen, worden aanbevolen suggesties voor tabel- en kolomnamen en SQL-trefwoorden na een korte pauze beschikbaar. Een succesbericht in de console onder de Redacteur van de Vraag wijst op de eigenschap actief is.

Als u de functie voor automatisch aanvullen uitschakelt, wordt de functie pas van kracht nadat u een pagina hebt vernieuwd. Er wordt een bevestigingsvenster weergegeven met drie opties wanneer u het dialoogvenster [!UICONTROL Syntax auto-complete] schakelen:

- [!UICONTROL Cancel]
- [!UICONTROL Save changes and refresh]
- [!UICONTROL Refresh without saving changes]

>[!IMPORTANT]
>
>Als u een query schrijft of bewerkt wanneer u deze functie uitschakelt, moet u eventuele wijzigingen in de query opslaan voordat u de pagina vernieuwt, anders gaat alle voortgang verloren.

![Het bevestigingsvenster om de functie voor automatisch aanvullen uit te schakelen.](../images/ui/query-editor/confirmation-dialog.png)

Selecteer de gewenste optie om de functie voor automatisch aanvullen uit te schakelen.

### Foutdetectie {#error-detection}

[!DNL Query Editor] valideert automatisch een vraag aangezien u het schrijft, verstrekkend generische SQL bevestiging en specifieke uitvoeringsbevestiging. Als een rode onderstreping onder de query wordt weergegeven (zoals in de onderstaande afbeelding wordt getoond), vertegenwoordigt deze een fout binnen de query.

![De invoer van de Redacteur van de Vraag tonend in rood onderstreepte SQL om op een fout te wijzen.](../images/ui/query-editor/syntax-error-highlight.png)

Wanneer fouten worden ontdekt, kunt u de specifieke foutenmeldingen bekijken door over de SQL code te hangen.

![Een dialoogvenster met een foutbericht.](../images/ui/query-editor/linting-error.png)

### Query-details {#query-details}

Selecteer een opgeslagen sjabloon in het menu [!UICONTROL Templates] om het in de Redacteur van de Vraag te bekijken. Het deelvenster met querydetails bevat meer informatie en gereedschappen voor het beheer van de geselecteerde query.

![De Query-editor met het deelvenster met querydetails gemarkeerd.](../images/ui/query-editor/query-details.png)

Dit paneel staat u toe om een outputdataset direct van UI te produceren, de getoonde vraag te schrappen of te noemen, en een programma aan de vraag toe te voegen.

In dit deelvenster worden ook nuttige metagegevens weergegeven, zoals de laatste keer dat de query werd gewijzigd en de eventuele wijziging. Als u een gegevensset wilt genereren, selecteert u **[!UICONTROL Output Dataset]**. De **[!UICONTROL Output Dataset]** wordt weergegeven. Voer een naam en beschrijving in en selecteer **[!UICONTROL Run Query]**. De nieuwe dataset wordt getoond in **[!UICONTROL Datasets]** op het tabblad [!DNL Query Service] gebruikersinterface op [!DNL Platform].

### Geplande query&#39;s {#scheduled-queries}

De vragen die als malplaatje zijn bewaard kunnen van de Redacteur van de Vraag worden gepland. Dit staat u toe om vraaglooppas te automatiseren die op een douanecadence wordt uitgevoerd. U kunt vragen plannen die op frequentie, datum, en tijd worden gebaseerd, en ook een outputdataset voor uw resultaten kiezen indien vereist. De programma&#39;s van de vraag kunnen ook door UI worden onbruikbaar gemaakt of worden geschrapt.

Planningen worden ingesteld in de Query-editor. Wanneer het gebruiken van de Redacteur van de Vraag, kunt u een programma aan een vraag slechts toevoegen die reeds is gecreeerd, opgeslagen, en looppas. Dit geldt niet voor de [!DNL Query Service] API:

Zie de documentatie van vraagprogramma&#39;s om te leren hoe te [vraagprogramma&#39;s in UI creëren](./query-schedules.md). Als u ook wilt leren hoe u planningen kunt toevoegen met de API, leest u de [de geplande gids van het vraageindpunt](../api/scheduled-queries.md).

Alle geplande query&#39;s worden toegevoegd aan de lijst in de [!UICONTROL Scheduled queries] tab. Van die werkruimte kunt u het statuut van alle geplande vraagbanen door UI controleren. Op de [!UICONTROL Scheduled queries] kunt u belangrijke informatie over uw vraaglooppas vinden en aan alarm intekenen. De beschikbare informatie omvat de status, de planningsdetails, en foutenmeldingen/codes als een looppas ontbreekt. Zie de [Geplande query&#39;s controleren](./monitor-queries.md) voor meer informatie .

### Bezig met opslaan van query&#39;s {#saving-queries}

De [!DNL Query Editor] beschikt over een opslagfunctie waarmee u een query kunt opslaan en er later aan kunt werken. Selecteer **[!UICONTROL Save]** in de rechterbovenhoek van [!DNL Query Editor]. Voordat een query kan worden opgeslagen, moet u een naam opgeven voor de query met de opdracht **[!UICONTROL Query Details]** deelvenster.

>[!NOTE]
>
>Vragen die zijn genoemd en opgeslagen in de Query-editor, zijn beschikbaar als sjablonen in het dashboard Query [!UICONTROL Templates] tab. Zie de [sjabloondocumentatie](./query-templates.md) voor meer informatie .

### Hoe te om vorige vragen te vinden {#previous-queries}

Alle query&#39;s uitgevoerd van [!DNL Query Editor] worden vastgelegd in de logbestandentabel. U kunt de zoekfunctionaliteit in het dialoogvenster **[!UICONTROL Log]** om query-uitvoeringen te zoeken. Opgeslagen query&#39;s worden weergegeven in het dialoogvenster **[!UICONTROL Templates]** tab.

Als een vraag gepland was, toen [!UICONTROL Scheduled Queries] biedt een verbeterde zichtbaarheid via de gebruikersinterface voor die querytaken. Zie de [query-monitoringdocumentatie](./monitor-queries.md) voor meer informatie .

>[!NOTE]
>
>Vragen die niet worden uitgevoerd, worden niet opgeslagen in het logbestand. De query is beschikbaar in [!DNL Query Service], moet het worden uitgevoerd of opgeslagen in [!DNL Query Editor].

## Vragen uitvoeren met de Query Editor {#executing-queries}

Een query uitvoeren in [!DNL Query Editor], kunt u SQL in de redacteur ingaan of een vorige vraag van laden **[!UICONTROL Log]** of **[!UICONTROL Templates]** en selecteert u **Afspelen**. De status van query-uitvoering wordt weergegeven in het dialoogvenster **[!UICONTROL Console]** en de uitvoergegevens worden weergegeven in het dialoogvenster **[!UICONTROL Results]** tab.

### Console {#console}

De console biedt informatie over de status en werking van [!DNL Query Service]. De console toont de verbindingsstatus aan [!DNL Query Service], querybewerkingen die worden uitgevoerd en foutberichten die het resultaat zijn van deze query&#39;s.

![Het tabblad Console van de console van de Query Editor.](../images/ui/query-editor/console.png)

>[!NOTE]
>
>De console toont slechts fouten die uit het uitvoeren van een vraag voortkwamen. Er worden geen fouten met de queryvalidatie weergegeven voordat een query wordt uitgevoerd.

### Zoekresultaten {#query-results}

Nadat een vraag is voltooid, worden de resultaten getoond in **[!UICONTROL Results]** tab, naast de **[!UICONTROL Console]** tab. In deze weergave wordt de tabeluitvoer van uw query weergegeven, met maximaal 100 rijen. In deze weergave kunt u controleren of de query de verwachte uitvoer oplevert. Om een dataset met uw vraag te produceren, verwijder grenzen op teruggekeerde rijen, en stel de vraag met in werking `CREATE TABLE tablename AS SELECT` om een dataset met de output te produceren. Zie de [het produceren van datasetleerprogramma](./create-datasets.md) voor instructies op hoe te om een dataset van vraagresultaten te produceren in [!DNL Query Editor].

![Het lusje van Resultaten van de console van de Redacteur van de Vraag die de resultaten van een vraaglooppas toont.](../images/ui/query-editor/query-results.png)

## Zoekopdrachten uitvoeren met [!DNL Query Service] zelfstudievideo {#query-tutorial-video}

In de volgende video ziet u hoe u query&#39;s uitvoert in de Adobe Experience Platform-interface en in een PSQL-client. Bovendien wordt het gebruik van individuele eigenschappen in een XDM-object, met gebruik van door Adobe gedefinieerde functies en het gebruik van CREATE TABLE AS SELECT (CTAS) aangetoond.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Volgende stappen

Nu weet u welke functies beschikbaar zijn in [!DNL Query Editor] en hoe u door de toepassing kunt navigeren, kunt u uw eigen query&#39;s rechtstreeks ontwerpen in [!DNL Platform]. Voor meer informatie over het runnen van SQL vragen tegen datasets binnen [!DNL Data Lake], zie de handleiding op [uitvoeren, query&#39;s](../best-practices/writing-queries.md).
