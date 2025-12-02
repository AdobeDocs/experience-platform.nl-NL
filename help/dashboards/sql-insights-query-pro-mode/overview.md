---
title: SQL-inzichten voor uitgebreide toepassingsrapportage
description: Leer hoe u SQL-query's kunt gebruiken om inzichten voor uw aangepaste dashboards te genereren.
exl-id: c60a9218-4ac0-4638-833b-bdbded36ddf5
source-git-commit: 9f4ce2a3a8af72342683c859caa270662b161b7d
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 0%

---

# SQL Insights voor uitgebreide apprapportage

Gebruik aangepaste SQL-query&#39;s om inzichten effectief te extraheren uit verschillende gestructureerde datasets. De technische mensen kunnen vraag pro wijze gebruiken om complexe analyse met SQL uit te voeren en dan deze analyse met niet-technische gebruikers door grafieken op uw douanedashboard te delen of hen in Csv- dossiers uit te voeren. Deze methode voor het maken van insight is zeer geschikt voor tabellen met duidelijke relaties en maakt een grotere mate van aanpassing mogelijk binnen uw inzichten en filters die geschikt zijn voor nichemoepassingen.

>[!IMPORTANT]
>
>De vraag pro wijze is slechts beschikbaar aan gebruikers die [&#x200B; Gegevens Distiller SKU &#x200B;](../../query-service/data-distiller/overview.md) hebben gekocht.

Als u inzichten wilt genereren op basis van SQL, moet u eerst een dashboard maken.

## Een aangepast dashboard maken {#create-custom-dashboard}

Als u een aangepast dashboard wilt maken, selecteert u **[!UICONTROL Dashboards]** in het navigatievenster aan de linkerkant om de werkruimte Dashboards te openen. Selecteer vervolgens **[!UICONTROL Create dashboard]** .

![&#x200B; de inventaris van het dashboard met Create benadrukte dashboard.](../images/sql-insights-query-pro-mode/create-dashboard.png)

Het dialoogvenster **[!UICONTROL Create dashboard]** wordt weergegeven. Er zijn twee opties waaruit u de methode voor het maken van het dashboard kunt kiezen. Om uw inzichten tot stand te brengen kunt u of een bestaand gegevensmodel met [[!UICONTROL Guided design mode]](../standard-dashboards.md) of uw eigen SQL met [!UICONTROL Query pro mode] gebruiken.

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

Het gebruik van een bestaand gegevensmodel biedt de voordelen van een gestructureerd, efficiënt en schaalbaar framework dat is afgestemd op uw specifieke bedrijfsbehoeften. Leren hoe te om [&#x200B; inzichten van een bestaand gegevensmodel &#x200B;](../standard-dashboards.md#create-widget) tot stand te brengen, verwijs naar de gids van het douanedashboard.

De inzichten die van SQL vragen worden geproduceerd bieden veel grotere flexibiliteit en aanpassing aan. De technische mensen kunnen vraag pro wijze gebruiken om complexe analyse op SQL uit te voeren en dan deze analyse met niet-technische gebruikers door dit dashboardvermogen te delen. Selecteer **[!UICONTROL Query pro mode]** gevolgd door **[!UICONTROL Save]** .

>[!NOTE]
>
>Als u eenmaal een selectie hebt gemaakt, kunt u deze selectie in het dashboard niet meer wijzigen. In plaats daarvan moet u een nieuw dashboard maken met een andere methode voor het maken van het dashboard.

![&#x200B; de [!UICONTROL Create dashboard] dialoog met Vraag pro wijze en sparen benadrukte.](../images/sql-insights-query-pro-mode/query-pro-mode.png)

## Overzicht van de modus Query Pro {#query-pro-mode}

De modus Query Pro is een op SQL-editors gebaseerde workflow die u begeleidt bij het genereren van inzichten met aangepaste SQL-query&#39;s in de gebruikersinterface van Adobe Experience Platform. Voordat u inzichten kunt genereren met aangepaste SQL-query&#39;s, moet u eerst een dashboard maken.

## SQL samenstellen {#compose-sql}

Nadat u hebt opgegeven dat u een dashboard met de modus Query Pro wilt maken, wordt het dialoogvenster **[!UICONTROL Enter SQL]** weergegeven. Selecteer een gegevensbestand (gegevensmodel van inzichten) aan vraag van het drop-down menu, en input een geschikte vraag voor uw dataset in de vraag pro redacteur.

>[!NOTE]
>
>De modus Query Pro is alleen beschikbaar voor gebruikers die de Data Distiller SKU hebben aangeschaft. [[!UICONTROL Guided design mode]](../standard-dashboards.md) is beschikbaar voor alle gebruikers om inzichten van een bestaand gegevensmodel tot stand te brengen.

Zie de [&#x200B; gebruikersgids van de Redacteur van de Vraag &#x200B;](../../query-service/ui/user-guide.md#query-authoring) voor informatie over zijn elementen UI.

![&#x200B; De [!UICONTROL Enter SQL] dialoog met het Datumet dropdown menu en in werking gestelde pictogram benadrukte, heeft de dialoog een bevolkte SQL vraag en de getoonde vraagparameters tabel.](../images/sql-insights-query-pro-mode/enter-sql-database-dropdown.png)

### Query-parameters {#query-parameters}

Om [&#x200B; globale &#x200B;](./filters/global-filter.md) of [&#x200B; datumfilters &#x200B;](./filters/date-filter.md) te omvatten uw vraag **moet** de parameters van de gebruiksvraag. Wanneer het samenstellen van uw verklaring op vraag pro wijze, moet u steekproefwaarden verstrekken als uw vraag vraagparameters gebruikt. Met de voorbeeldwaarden kunt u de SQL-instructie uitvoeren en het diagram samenstellen. De voorbeeldwaarden die u opgeeft bij het samenstellen van de instructie, worden vervangen door de werkelijke waarden die u tijdens runtime voor de datum of het algemene filter selecteert.

>[!IMPORTANT]
>
>Als u een algemeen filter wilt gebruiken, moet u een vraagparameter in uw SQL plaatsen en dan die vraagparameter verbinden met het globale filter in widgetcomposer. In de onderstaande schermafbeelding wordt `CONSENT_VALUE_FILTER` in de SQL gebruikt als een queryparameter voor een algemeen filter. Zie de [&#x200B; globale filterdocumentatie &#x200B;](./filters/global-filter.md#enable-global-filter) voor meer informatie over hoe te om dit te doen.

Om uw vraag uit te voeren, selecteer het looppaspictogram (![&#x200B; het looppaspictogram.](/help/images/icons/play.png)). De Redacteur van de Vraag toont de resultaten tabel. Selecteer vervolgens **[!UICONTROL Select]** om uw configuratie te bevestigen en de widgetcomposer te openen.

>[!TIP]
>
>Als uw vraag vraagparameters gebruikt, stel de vraag eens in werking om alle gebruikte sleutels van de vraagparameter vooraf in te vullen. De query zal mislukken, maar de gebruikersinterface geeft automatisch het tabblad Query-parameters weer en geeft alle opgenomen toetsen weer. Voeg de juiste waarden voor de toetsen toe.

![&#x200B; het [!UICONTROL Enter SQL] dialoog met SQL input, het getoonde resultatenlusje, en Uitgezochte benadrukte.](../images/sql-insights-query-pro-mode/enter-sql-select.png)

## Widget vullen {#populate-widget}

De widgetcomposer wordt nu gevuld met de kolommen van de uitgevoerde SQL. Het type dashboard wordt linksboven aangegeven, in dit geval [!UICONTROL Manual SQL Entry] . Selecteer het potloodpictogram (![&#x200B; het potloodpictogram van A.](/help/images/icons/edit.png) ) om de SQL op elk gewenst moment te bewerken.

>[!TIP]
>
>De beschikbare kenmerken zijn kolommen die zijn opgehaald uit de uitgevoerde SQL.

Als u een widget wilt maken, gebruikt u de kenmerken in de kolom [!UICONTROL Attributes] . Met de zoekbalk kunt u naar kenmerken zoeken of door de lijst bladeren.

![&#x200B; Widget composer met de creatiemethode en kenmerkenkolom benadrukte.](../images/sql-insights-query-pro-mode/creation-method-and-attribute-column.png)

### Kenmerken toevoegen {#add-attributes}

Om een attribuut aan uw widget toe te voegen, selecteer het plusteken (![&#x200B; A plus pictogram.](/help/images/icons/add-circle.png) ) naast een kenmerknaam. In het vervolgkeuzemenu dat wordt weergegeven, kunt u een kenmerk aan het diagram toevoegen op basis van de opties die door de SQL worden bepaald. Verschillende diagramtypen hebben verschillende opties, zoals een vervolgkeuzelijst op de X- en Y-as.

In dit voorbeeld van het donutdiagram zijn de opties grootte en kleur. Kleuren worden verdeeld in de resultaten van het donutdiagram en de grootte is de werkelijk gebruikte metrische waarde. Voeg een attribuut aan het [!UICONTROL Color] gebied toe om de resultaten in verschillende kleuren te verdelen die op hun samenstelling van dat attribuut worden gebaseerd.

>[!TIP]
>
>Selecteer omhoog en benedenpijlpictogram (![&#x200B; het omhoog en benedenpijlpictogram.](/help/images/icons/switch.png)) om de rangschikking van de X- en Y-as op staaf- of lijngrafieken te wijzigen.

![&#x200B; Widget composer met toe:voegen-pictogram dropdown en schakelaar gemarkeerde pijlen.](../images/sql-insights-query-pro-mode/add-icon-and-switch-arrows.png)

Als u het type grafiek of grafiek van de widget wilt wijzigen, selecteert u een van de beschikbare opties in het vervolgkeuzemenu [!UICONTROL Marks] . De opties zijn [!UICONTROL Line] , [!UICONTROL Donut] , [!UICONTROL Big number] en [!UICONTROL Bar] . Als deze optie is geselecteerd, wordt een voorvertoning van de huidige instellingen van de widget gegenereerd.

![&#x200B; Widget composer met de benadrukte widgetvoorproef.](../images/sql-insights-query-pro-mode/widget-preview.png)

## Geavanceerde tabelkenmerken {#advanced-attributes}

Als u automatische sorteermogelijkheden wilt toepassen op een of alle kolommen in de tabellen, selecteert u **[!UICONTROL Edit]** om het hele dashboard te bewerken.

![&#x200B; A douanedashboard met Edit benadrukte.](../images/sql-insights-query-pro-mode/advanced-edit-dashboard.png)

Selecteer de ellips (`...`) in het lijstdiagram waar u kolomsortering wilt toevoegen, dan uitgezocht **[!UICONTROL Edit]**.

![&#x200B; een lijst die van A het ellips menu met uitgezocht geeft toont.](../images/sql-insights-query-pro-mode/advanced-table-edit.png)

Schakel de selectievakjes **[!UICONTROL Sortable]** in om het sorteren voor elke kolom in te schakelen.

![&#x200B; uitgeven de Lijst pagina met sorteerbare benadrukte controledozen.](../images/sql-insights-query-pro-mode/advanced-table-sortable.png)

Selecteer het eigenschappen pictogram (![&#x200B; het eigenschappen pictogram.](/help/images/icons/properties.png) ) in de rechterrail om het deelvenster [!UICONTROL Properties] te openen. Selecteer in het deelvenster **[!UICONTROL Properties]** de kolom met de vervolgkeuzelijst **[!UICONTROL Default sort]** en selecteer vervolgens de kolom met de vervolgkeuzelijst **[!UICONTROL Sort direction]** . Selecteer ten slotte **[!UICONTROL Save and close]** .

![&#x200B; Widget composer met het bezitspictogram, standaardsoort, sorteerrichting, sparen en dicht benadrukte.](../images/sql-insights-query-pro-mode/advanced-table-properties.png)

Meer leren over het gebruiken van de soort, het resizing van kolommen, en pagineringseigenschappen, verwijs naar [&#x200B; Mening meer &#x200B;](./view-more.md).

## Eigenschappen van Widget {#properties}

Selecteer het eigenschappen pictogram (![&#x200B; het eigenschappen pictogram.](/help/images/icons/properties.png) ) in de rechterrail om het deelvenster Eigenschappen te openen. Typ in het deelvenster [!UICONTROL Properties] een naam voor de widget in het tekstveld **[!UICONTROL Widget title]** . U kunt ook de naam wijzigen van verschillende aspecten van uw diagram.

>[!NOTE]
>
>Welke specifieke velden beschikbaar zijn in de zijbalk Eigenschappen, is afhankelijk van het diagramtype dat u bewerkt.

![&#x200B; Widget composer met het eigenschappen pictogram en benadrukt gebied van de titel van Widget.](../images/sql-insights-query-pro-mode/widget-properties-title-text.png)

## Uw widget opslaan {#save-widget}

Als u de widget opslaat in de widgetcomposer, wordt de widget lokaal op het dashboard opgeslagen. Selecteer **[!UICONTROL Save]** als u uw werk wilt opslaan en later wilt hervatten. Een tikpictogram onder de widgetnaam geeft aan dat de widget is opgeslagen. Als u tevreden bent met de widget, selecteert u **[!UICONTROL Save and close]** om de widget beschikbaar te maken voor alle andere gebruikers die toegang hebben tot het dashboard. Selecteer Annuleren om uw werk te verlaten en terug te keren naar het aangepaste dashboard.

![&#x200B; Widget composer met sparen, Opgeslagen Widget, en sparen en dicht benadrukte.](../images/sql-insights-query-pro-mode/insight-saved.png)

## Uw dashboard en grafieken bewerken {#edit}

Selecteer **[!UICONTROL Edit]** om het hele dashboard of een van uw inzichten te bewerken. In de bewerkingsmodus kunt u widgets vergroten of verkleinen, uw SQL bewerken of algemene en tijdelijke filters maken en toepassen. Deze filters beperken de gegevens die in uw dashboardwidgets worden weergegeven. Dit is een handige manier om uw inzichten voor verschillende gebruiksgevallen snel bij te werken en af te stemmen.

![&#x200B; A douanedashboard met Edit benadrukte.](../images/sql-insights-query-pro-mode/edit-dashboard.png)

Selecteer **[!UICONTROL Add filter]** om een [[!UICONTROL Date filter]](#create-date-filter) of een [[!UICONTROL Global filter]](#create-global-filter) -element te maken. Zodra gecreeerd, zijn alle globale en datumfilters beschikbaar van [&#x200B; het filterpictogram &#x200B;](#select-global-filter) (![&#x200B; het filterpictogram van A.](/help/images/icons/filter.png) ) van het dashboard.

![&#x200B; A douanedashboard met Add benadrukt het drop-down menu van de filter.](../images/sql-insights-query-pro-mode/add-filter.png)

## Insight bewerken, dupliceren of verwijderen

Zie de gids van het dashboard van de Douane voor instructies op hoe te [&#x200B; uitgeven, dupliceren, of schrappen een bestaande widget &#x200B;](../standard-dashboards.md#duplicate).

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu hoe u SQL-query&#39;s kunt schrijven in de gebruikersinterface van Adobe Experience Platform om grafieken te genereren voor uw aangepaste dashboards. Daarna, zou u moeten leren hoe te om uw gegevens verder te verrijken door [&#x200B; een datumfilter &#x200B;](./filters/date-filter.md) te creëren, of [&#x200B; creërend een globale filter &#x200B;](./filters/global-filter.md).

U kunt meer over andere Aangepaste eigenschappen van Inzichten met inbegrip van [&#x200B; ook leren de verschillende het bekijken opties voor u SQL analyseerde gegevens &#x200B;](./view-more.md) of hoe te [&#x200B; om SQL achter uw douaneinzichten &#x200B;](./view-sql.md) te bekijken.
