---
title: Aangepaste dashboards
description: Leer hoe u aangepaste dashboards kunt maken en beheren waar u op maat gemaakte widgets kunt maken, toevoegen en bewerken om belangrijke metriek zichtbaar te maken.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 0%

---

# Aangepaste dashboards

Gebruik Adobe Experience Platform-dashboards om inzichten te versnellen en visualisatie aan te passen via de functie Dashboards. Met deze functie kunt u aangepaste dashboards maken en beheren waar u op maat gemaakte widgets kunt maken, toevoegen en bewerken om belangrijke metriek die relevant is voor uw organisatie te visualiseren.


<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Een aangepast dashboard maken

Als u eerst een aangepast dashboard wilt maken, navigeert u naar het dashboardoverzicht. Selecteer **[!UICONTROL Dashboards]** in de linkernavigatie van de gebruikersinterface van het platform gevolgd door **[!UICONTROL Create dashboard]** .

![ de dashboardinventaris met Dashboards in de linkernavigatie en &quot;Create dashboard&quot;benadrukte.](./images/user-defined-dashboards/create-dashboard.png)

Voordat u een aangepast dashboard toevoegt, is de dashboardvoorraad leeg en wordt &#39;&#39;Geen dashboards gevonden&#39;&#39; weergegeven. bericht. Nadat u de dashboards hebt gemaakt, worden al uw dashboards weergegeven in de dashboardvoorraad.

<!-- >[!NOTE]
>
>To edit an existing dashboard, select the dashboard name from the inventory list followed by the pencil icon (![A pencil icon.](/help/images/icons/edit.png))
>![A custom inventory listed in the dashboard inventory.](./images/user-defined-dashboards/dashbaord-inventory.png "A custom inventory listed in the dashboard inventory."){width="100" zoomable="yes"} -->

Het dialoogvenster [!UICONTROL Create dashboard] wordt weergegeven. Voer een beschrijvende, mensvriendelijke naam in voor de verzameling widgets die u wilt maken en selecteer **[!UICONTROL Save]** .

![ de Create dashboarddialoog.](./images/user-defined-dashboards/create-dashboard-dialog.png)

Gebruikers die de Data Distiller SKU hebben aangeschaft, kunnen aangepaste SQL-query&#39;s gebruiken om hun inzichten te maken. Zie de [ Aanpasbare gids van de verwezenlijking van het Inzicht ](./data-distiller/customizable-insights/overview.md) voor instructies op dit werkschema.

Het nieuwe lege dashboard wordt met de door u gekozen naam weergegeven in de linkerbovenhoek van de weergave.

## Een widget maken {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Maximum aantal widgets"
>abstract="De Dashboard-service ondersteunt maximaal tien widgets. Nadat u tien widgets aan het dashboard hebt toegevoegd, is de optie [!UICONTROL Add new widget] uitgeschakeld en wordt deze grijs weergegeven."

Selecteer in de nieuwe dashboardweergave **[!UICONTROL Add new widget]** om het maken van de widget te starten.

>[!IMPORTANT]
>
>Elk dashboard ondersteunt maximaal tien widgets. Nadat u tien widgets aan het dashboard hebt toegevoegd, is de optie [!UICONTROL Add new widget] uitgeschakeld en wordt deze grijs weergegeven.

![ het nieuwe lege dashboard met Add nieuwe benadrukte widget.](./images/user-defined-dashboards/add-new-widget.png)

### Widget-composer

De werkruimte van de widgetcomposer wordt weergegeven. Selecteer vervolgens **[!UICONTROL Select data]** om het gegevensmodel te kiezen waaruit u kenmerken aan uw widgets wilt toevoegen.

![ de werkruimte van widgetcomposer.](./images/user-defined-dashboards/widget-composer.png)

#### Gegevensmodel selecteren {#select-data-model}

Het dialoogvenster [!UICONTROL Select data model] wordt weergegeven. Selecteer een gegevensmodel in de linkerkolom om een voorvertoningslijst van alle beschikbare lijsten te tonen. Het vooraf geconfigureerde gegevensmodel voor Real-time Customer Data Platform krijgt de naam [!UICONTROL CDPInsights] .

>[!TIP]
>
>Selecteer het informatiepictogram (![ een informatiepictogram.](/help/images/icons/info.png)) om de volledige naam van het gegevensmodel weer te geven als het te lang is om in de gegevensrails weer te geven.

![ de Uitgezochte gegevensdialoog.](./images/user-defined-dashboards/select-data-model-dialog.png)

De voorvertoningslijst bevat informatie over de tabellen in het gegevensmodel. De onderstaande tabel bevat een beschrijving van de kolomvelden en de mogelijke waarden ervan.

| Kolomveld | Beschrijving |
|---|---|
| [!UICONTROL Title] | De naam van de tabel. |
| [!UICONTROL Table type] | Het type tabel. Mogelijke typen zijn: `fact` , `dimension` en `none` . |
| [!UICONTROL Records] | Het aantal records dat aan de gekozen tabel is gekoppeld. |
| [!UICONTROL Lookups] | Het aantal tabellen dat is gekoppeld aan de gekozen tabel. |
| [!UICONTROL Attributes] | Het aantal kenmerken voor de gekozen tabel. |

Selecteer **[!UICONTROL Next]** om uw keuze van gegevensmodel te bevestigen. In de volgende weergave wordt een lijst weergegeven met de beschikbare tabellen in de linkertrack. Selecteer een tabel voor een uitgebreide uitsplitsing van de gegevens in de geselecteerde tabel.

### Widget vullen {#populate-widget}

Het deelvenster [!UICONTROL Preview] bevat tabbladen voor [!UICONTROL Sample records] en [!UICONTROL Attributes] . Het tabblad [!UICONTROL Sample records] bevat een subset van de records van de geselecteerde tabel in een tabelweergave. Het tabblad [!UICONTROL Attributes] bevat de kenmerknaam, het gegevenstype en de brontabel voor elk kenmerk dat aan de geselecteerde tabel is gekoppeld.

Selecteer een tabel in de lijst in de linkertrack om gegevens voor de widget op te geven en selecteer **[!UICONTROL Select]** om terug te keren naar de widgetcomposer.

![ de uitgezochte dialoog van gegevens met uitgezocht benadrukte.](./images/user-defined-dashboards/select-a-table.png)

De widgetcomposer is nu gevuld met gegevens uit de door u gekozen tabel.

Het gegevensmodel en de geselecteerde tabel worden boven aan de linkertrack weergegeven. De kenmerken die beschikbaar zijn om de widget te maken, worden in de kolom [!UICONTROL Attributes] weergegeven. U kunt de onderzoeksbar gebruiken om attributen te zoeken in plaats van het scrollen van de lijst, of het gekozen gegevensmodel te veranderen door het potloodpictogram (![ pictogram van het Potlood te selecteren.](/help/images/icons/edit.png) ) in de linkerspoorstaaf.

![ widget van A bevolkt met gegevens binnen widgetcomposer.](./images/user-defined-dashboards/populated-widget-composer.png)

#### Kenmerken toevoegen en filteren {#add-and-filter-attributes}

Selecteer het add pictogram (![ en voeg pictogram toe.](/help/images/icons/add-circle.png) ) naast een kenmerknaam om een kenmerk aan uw widget toe te voegen. In het vervolgkeuzemenu dat wordt weergegeven, kunt u een kenmerk toevoegen als de X-as, de Y-as, een kleur of een filter voor de widget. Met het kenmerk [!UICONTROL Color] kunt u de resultaten van de markeringen op de X- en Y-as onderscheiden op basis van kleur. Dit wordt gedaan door de resultaten in verschillende kleuren te verdelen die op hun samenstelling van een derde attribuut worden gebaseerd.

>[!TIP]
>
>Als u de regeling van de as van X en van Y wilt omdraaien, selecteer omhoog en benedenpijlpictogram (![ omhoog en benedenpijlpictogram.](/help/images/icons/switch.png)) om de rangschikking te wijzigen.

![ Widget composer met toe:voegen-pictogram benadrukt dropdown.](./images/user-defined-dashboards/attributes-dropdown.png)

Als u het type grafiek of grafiek van de widget wilt wijzigen, selecteert u het vervolgkeuzemenu [!UICONTROL Marks] en kiest u een van de beschikbare opties. U kunt onder andere balken, punten, tikken, lijnen of gebieden kiezen. Als deze optie is geselecteerd, wordt een voorvertoning van de huidige instellingen van de widget gegenereerd.

![ Widget composer met de benadrukte dropdown van Tekens.](./images/user-defined-dashboards/marks-dropdown.png)

Door een kenmerk toe te voegen als filter, kunt u selecteren welke waarden u wilt opnemen in of uitsluiten van de widget. Nadat u een filter hebt toegevoegd uit de lijst met kenmerken, wordt het dialoogvenster [!UICONTROL Filter] weergegeven waarin u waarden kunt selecteren of deselecteren met behulp van het selectievakje.

![ de filterdialoog aan filterwaarden van uw widget.](./images/user-defined-dashboards/filter-dialog.png)

#### Historische gegevens uitfilteren {#filter-historical-data}

Als u historische gegevens wilt filteren uit de inzichten die door de widget zijn gegenereerd, voegt u het kenmerk `date_key` toe als een filter en selecteert u **[!UICONTROL Recent date]** gevolgd door **[!UICONTROL Apply]** . Dit filter zorgt ervoor dat de gegevens die worden gebruikt om inzichten af te leiden uit de meest recente systeemmomentopname worden genomen.

![ de [!UICONTROL Filter: date_key] dialoog met [!UICONTROL Recent date] en [!UICONTROL Apply] benadrukte.](./images/user-defined-dashboards/recent-date.png)

U kunt ook een aangepaste periode maken om de gegevens op te filteren. Selecteer **[!UICONTROL Select dates]** om het dialoogvenster uit te breiden met een lijst met beschikbare datums. Gebruik het selectievakje **[!UICONTROL Select all]** om alle beschikbare opties in of uit te schakelen, of schakel het selectievakje voor elke dag afzonderlijk in. Selecteer ten slotte **[!UICONTROL Apply]** om uw keuzes te bevestigen.

>[!NOTE]
>
>Als het kenmerk `date_key` al als filter is toegevoegd, selecteert u in de vervolgkeuzelijst de ellips gevolgd door **[!UICONTROL Edit]** om de filterperiode te wijzigen.

![ het [!UICONTROL Filter: date_key] dialoogvenster met individuele dag checkboxes zowel gecontroleerd als ongecontroleerd.](./images/user-defined-dashboards/select-dates.png)

### Eigenschappen van Widget

Selecteer het eigenschappen pictogram (![ het eigenschappen pictogram.](/help/images/icons/properties.png) ) in de rechterrail om het deelvenster Eigenschappen te openen. Typ in het deelvenster [!UICONTROL Properties] een naam voor de widget in het tekstveld [!UICONTROL Widget title] .

![ het eigenschappen paneel met het eigenschappen pictogram en het benadrukte gebied van de Titel van Widget.](./images/user-defined-dashboards/properties-panel.png)

Vanuit het deelvenster met widgeigenschappen kunt u verschillende aspecten van uw widget bewerken. U hebt volledige controle om de plaats van widgetlegenda uit te geven. Als u de legenda wilt verplaatsen, selecteert u het vervolgkeuzemenu [!UICONTROL Legend placement] en kiest u de gewenste locatie in de lijst met beschikbare opties. U kunt ook de naam wijzigen van het label dat is gekoppeld aan de legenda en de X- of Y-as door een nieuwe naam in te voeren in respectievelijk het tekstveld [!UICONTROL Legend title] of [!UICONTROL Axis label] .

#### Uw widget opslaan {#save-widget}

Als u de widget opslaat in de widgetcomposer, wordt de widget lokaal op het dashboard opgeslagen. Selecteer **[!UICONTROL Save]** als u uw werk wilt opslaan en later wilt hervatten. Een tikpictogram onder de widgetnaam geeft aan dat de widget is opgeslagen. Als u tevreden bent met de widget, selecteert u **[!UICONTROL Save and close]** om de widget beschikbaar te maken voor alle andere gebruikers die toegang hebben tot het dashboard. Selecteer **[!UICONTROL Cancel]** om uw werk te verlaten en terug te keren naar het aangepaste dashboard.

![ Nieuwe widget sparen bevestiging.](./images/user-defined-dashboards/save-confirmation.png)

>[!TIP]
>
>Selecteer het eigenschappen pictogram (![ het eigenschappen pictogram.](/help/images/icons/properties.png) ) naast de naam van het dashboard voor meer informatie over het maken ervan. U kunt de naam van het dashboard wijzigen in het dialoogvenster dat verschijnt.

U kunt widgets opnieuw rangschikken en de grootte ervan wijzigen in deze werkruimte. Selecteer **[!UICONTROL Save]** om de naam en de geconfigureerde indeling van het dashboard te behouden.

![ het user-defined dashboard met een douane widget en sparen benadrukte knoop.](./images/user-defined-dashboards/user-defined-dashboard.png)

Om ervoor te zorgen dat elke vraag voor een Adobe Real-time Customer Data Platform inzichten dashboard genoeg middelen heeft om efficiënt uit te voeren, volgt API middelgebruik door gelijkheidsgroeven aan elke vraag toe te wijzen. Het systeem kan tot vier gezamenlijke vragen verwerken, en daarom zijn vier gezamenlijke vraaggroeven beschikbaar op elk bepaald ogenblik. Vragen worden in een wachtrij geplaatst op basis van sleuven voor gelijktijdige uitvoering en wachten vervolgens in de wachtrij totdat voldoende sleuven voor gelijktijdige uitvoering beschikbaar zijn.

### Een widget bewerken, dupliceren of verwijderen {#duplicate}

Nadat u een widget hebt gemaakt, kunt u volledige widgets uit uw aangepaste dashboard bewerken, dupliceren of verwijderen.

>[!TIP]
>
>Als u wilt schakelen tussen een van uw bestaande aangepaste dashboards, selecteert u Dashboards in de linkernavigatiebalk en selecteert u vervolgens de dashboardnaam in de inventarislijst.

Selecteer het potloodpictogram (![ het potloodpictogram van A.](/help/images/icons/edit.png) ) rechtsboven in het aangepaste dashboard om de bewerkingsmodus te activeren.

![ A douanedashboard met het benadrukte potloodpictogram.](./images/user-defined-dashboards/edit-mode.png)

Selecteer vervolgens de ovalen in de rechterbovenhoek van de widget die u wilt bewerken, kopiëren of verwijderen. Selecteer de gewenste actie in het vervolgkeuzemenu.

![ widget van A in een douane dashboard met de ellipsen en Dubbele benadrukte widget.](./images/user-defined-dashboards/duplicate.png)

>[!NOTE]
>
>Met duplicatie kunt u de kenmerken van een inzicht aanpassen om een unieke widget te maken zonder dat u helemaal opnieuw hoeft te beginnen. Als u een widget dupliceert, wordt deze weergegeven in het aangepaste dashboard. U kunt vervolgens de ovalen van de nieuwe widget selecteren, gevolgd door **[!UICONTROL Edit]** , om uw inzicht aan te passen.

## Volgende stappen en extra bronnen

Door dit document te lezen, hebt u een beter inzicht in hoe u een aangepast dashboard kunt maken en hoe u aangepaste widgets voor dat dashboard kunt maken, bewerken en bijwerken.

Om de beschikbare pre-gevormde metriek en visualisaties voor de [ profielen ](./guides/profiles.md#standard-widgets), [ segmenten ](./guides/audiences.md#standard-widgets), en [ bestemmingen ](./guides/destinations.md#standard-widgets) dashboards te ontdekken, zie de lijst van standaard widgets in hun respectieve documentatie.

Bekijk de volgende video om uw inzicht in dashboards in Experience Platform te versterken:

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
