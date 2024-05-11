---
title: Query Pro-modus
description: Leer hoe u SQL-query's gebruikt in de gebruikersinterface van Adobe Experience Platform om grafieken te maken voor uw aangepaste dashboards.
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---

# Query Pro-modus {#query-pro-mode}

De modus Query Pro is een op SQL-editors gebaseerde workflow die u begeleidt bij het genereren van inzichten met aangepaste SQL-query&#39;s in de gebruikersinterface van Adobe Experience Platform. Voordat u inzichten kunt genereren met aangepaste SQL-query&#39;s, moet u eerst [een dashboard maken](./overview.md#create-custom-dashboard).

## SQL samenstellen {#compose-sql}

Als u ervoor hebt gekozen een dashboard te maken met de modus query pro, wordt de opdracht **[!UICONTROL Enter SQL]** wordt weergegeven. Selecteer een gegevensbestand (gegevensmodel van inzichten) aan vraag van het drop-down menu, en input een geschikte vraag voor uw dataset in de vraag pro redacteur.

>[!NOTE]
>
>De modus Query Pro is alleen beschikbaar voor gebruikers die de Data Distiller SKU hebben aangeschaft. De [[!UICONTROL Guided design mode]](../../user-defined-dashboards.md) is beschikbaar voor alle gebruikers om inzichten van een bestaand gegevensmodel tot stand te brengen.

Zie de [Gebruikershandleiding voor de Query Editor](../../../query-service/ui/user-guide.md#query-authoring) voor informatie over zijn UI-elementen.

![De [!UICONTROL Enter SQL] dialoog met het dataset dropdown menu en looppaspictogram benadrukte, heeft de dialoog een bevolkte SQL vraag en de getoonde vraagparameters tabel.](../../images/customizable-insights/enter-sql-database-dropdown.png)

### Query-parameters {#query-parameters}

Opnemen [globaal](./filters/global-filter.md) of [datumfilters](./filters/date-filter.md) uw query **moet** gebruiken queryparameters. Wanneer het samenstellen van uw verklaring op vraag pro wijze, moet u steekproefwaarden verstrekken als uw vraag vraagparameters gebruikt. Met de voorbeeldwaarden kunt u de SQL-instructie uitvoeren en het diagram samenstellen. De voorbeeldwaarden die u opgeeft bij het samenstellen van de instructie, worden vervangen door de werkelijke waarden die u tijdens runtime voor de datum of het algemene filter selecteert.



>[!IMPORTANT]
>
>Als u een algemeen filter wilt gebruiken, moet u een vraagparameter in uw SQL plaatsen en dan die vraagparameter verbinden met het globale filter in widgetcomposer. In de onderstaande schermafbeelding: `CONSENT_VALUE_FILTER` wordt gebruikt in SQL als vraagparameter voor een globale filter. Zie de [algemene filterdocumentatie](./filters/global-filter.md#enable-global-filter) voor meer informatie over hoe dit te doen.

Selecteer het runpictogram (![Het runpictogram.](../../images/customizable-insights/run-icon.png)). De Redacteur van de Vraag toont de resultaten tabel. Selecteer vervolgens **[!UICONTROL Select]**.

>[!TIP]
>
>Als uw vraag vraagparameters gebruikt, stel de vraag eens in werking om alle gebruikte sleutels van de vraagparameter vooraf in te vullen. De query zal mislukken, maar de gebruikersinterface geeft automatisch het tabblad Query-parameters weer en geeft alle opgenomen toetsen weer. Voeg de juiste waarden voor de toetsen toe.

![De [!UICONTROL Enter SQL] met SQL-invoer, wordt het resultatentabblad weergegeven en Selecteren gemarkeerd.](../../images/customizable-insights/enter-sql-select.png)

## Widget vullen {#populate-widget}

De widgetcomposer wordt nu gevuld met de kolommen van de uitgevoerde SQL. Het type dashboard wordt linksboven aangegeven, in dit geval is [!UICONTROL Manual SQL Entry]. Selecteer het potloodpictogram (![Een potloodpictogram.](../../images/customizable-insights/edit-icon.png)) om de SQL op elk gewenst moment te bewerken.

>[!TIP]
>
>De beschikbare kenmerken zijn kolommen die zijn opgehaald uit de uitgevoerde SQL.

Als u een widget wilt maken, gebruikt u de kenmerken in de [!UICONTROL Attributes] kolom. Met de zoekbalk kunt u naar kenmerken zoeken of door de lijst bladeren.

![De widgetcomposer met de methode creation en kenmerkkolom gemarkeerd.](../../images/customizable-insights/creation-method-and-attribute-column.png)

### Kenmerken toevoegen {#add-attributes}

Als u een kenmerk aan de widget wilt toevoegen, selecteert u het plusteken (![Een plusteken.](../../images/customizable-insights/add-icon.png)) naast een kenmerknaam. In het vervolgkeuzemenu dat wordt weergegeven, kunt u een kenmerk aan het diagram toevoegen op basis van de opties die door de SQL worden bepaald. Verschillende diagramtypen hebben verschillende opties, zoals een vervolgkeuzelijst op de X- en Y-as.

In dit voorbeeld van het donutdiagram zijn de opties grootte en kleur. Kleuren worden verdeeld in de resultaten van het donutdiagram en de grootte is de werkelijk gebruikte metrische waarde. Voeg een attribuut aan toe [!UICONTROL Color] veld waarin de resultaten in verschillende kleuren worden gesplitst op basis van de samenstelling van dat kenmerk.

>[!TIP]
>
>Selecteer het pictogram pijl-omhoog en pijl-omlaag (![Het pictogram pijl-omhoog en pijl-omlaag.](../../images/customizable-insights/switch-axis-icon.png)) om de opstelling van de X- en Y-as op staaf- of lijndiagrammen te schakelen.

![De widgetcomposer met het vervolgkeuzemenu met invoegpictogrammen en de gemarkeerde switchpijlen.](../../images/customizable-insights/add-icon-and-switch-arrows.png)

Als u het type grafiek of grafiek van de widget wilt wijzigen, selecteert u een van de beschikbare opties van het dialoogvenster [!UICONTROL Marks] vervolgkeuzelijst. De opties omvatten [!UICONTROL Line], [!UICONTROL Donut], [!UICONTROL Big number], en [!UICONTROL Bar]. Als deze optie is geselecteerd, wordt een voorvertoning van de huidige instellingen van de widget gegenereerd.

![De widgetcomposer met de voorvertoning van de widget gemarkeerd.](../../images/customizable-insights/widget-preview.png)

## Eigenschappen van Widget {#properties}

Selecteer het pictogram Eigenschappen (![Het pictogram Eigenschappen.](../../images/customizable-insights/properties-icon.png)) in het rechterspoor om het deelvenster Eigenschappen te openen. In de [!UICONTROL Properties] een naam voor de widget in het deelvenster **[!UICONTROL Widget title]** tekstveld. U kunt ook de naam wijzigen van verschillende aspecten van uw diagram.

>[!NOTE]
>
>Welke specifieke velden beschikbaar zijn in de zijbalk Eigenschappen, is afhankelijk van het diagramtype dat u bewerkt.

![De widgetcomposer met het pictogram Eigenschappen en het veld Widgettitel gemarkeerd.](../../images/customizable-insights/widget-properties-title-text.png)

## Uw widget opslaan {#save-widget}

Als u de widget opslaat in de widgetcomposer, wordt de widget lokaal op het dashboard opgeslagen. Als u uw werk wilt opslaan en later wilt hervatten, selecteert u **[!UICONTROL Save]**. Een tikpictogram onder de widgetnaam geeft aan dat de widget is opgeslagen. Als u tevreden bent met de widget, selecteert u **[!UICONTROL Save and close]** om de widget beschikbaar te maken voor alle andere gebruikers die toegang hebben tot het dashboard. Selecteer Annuleren om uw werk te verlaten en terug te keren naar het aangepaste dashboard.

![De widgetcomposer met Opslaan, Widget opgeslagen en Opslaan en sluiten gemarkeerd.](../../images/customizable-insights/insight-saved.png)

## Uw dashboard en grafieken bewerken {#edit}

Selecteren **[!UICONTROL Edit]** om het hele dashboard of een van uw inzichten te bewerken. In de bewerkingsmodus kunt u widgets vergroten of verkleinen, uw SQL bewerken of algemene en tijdelijke filters maken en toepassen. Deze filters beperken de gegevens die in uw dashboardwidgets worden weergegeven. Dit is een handige manier om uw inzichten voor verschillende gebruiksgevallen snel bij te werken en af te stemmen.

![Een aangepast dashboard met de markering Bewerken.](../../images/customizable-insights/edit-dashboard.png)

Selecteren **[!UICONTROL Add filter]** om een [[!UICONTROL Date filter]](#create-date-filter) of [[!UICONTROL Global filter]](#create-global-filter). Na het maken zijn alle algemene en datumfilters beschikbaar vanuit [het filterpictogram](#select-global-filter) (![Een filterpictogram.](../../images/customizable-insights/filter.png)) van uw dashboard.

![Een aangepast dashboard met het Add filtervervolgkeuzemenu gemarkeerd.](../../images/customizable-insights/add-filter.png)

## Een inzicht bewerken, dupliceren of verwijderen

Zie de handleiding Aangepast dashboard voor instructies over hoe u [Een bestaande widget bewerken, dupliceren of verwijderen](../../user-defined-dashboards.md#duplicate).

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu hoe u SQL-query&#39;s kunt schrijven in de gebruikersinterface van Adobe Experience Platform om grafieken te genereren voor uw aangepaste dashboards. Vervolgens leert u hoe u uw gegevens verder kunt verrijken met [een datumfilter maken](./filters/date-filter.md), of [een algemeen filter maken](./filters/global-filter.md).

U kunt ook meer leren over andere aangepaste functies voor Inzichten, zoals [de verschillende weergaveopties voor de door SQL geanalyseerde gegevens](./view-more.md) of hoe [de SQL achter uw aangepaste inzichten weergeven](./view-sql.md).
