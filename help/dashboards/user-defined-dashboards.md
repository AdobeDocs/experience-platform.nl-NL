---
title: Door gebruiker gedefinieerde dashboards
description: Leer hoe u aangepaste dashboards kunt maken en beheren waar u op maat gemaakte widgets kunt maken, toevoegen en bewerken om belangrijke metriek zichtbaar te maken.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: 8e5df8b3e38197520c6e15f7c6639c62527c086e
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%

---

# Door gebruiker gedefinieerde dashboards

Met Adobe Experience Platform-dashboards kunt u snel inzicht krijgen en de visualisatie aanpassen via de door de gebruiker gedefinieerde dashboards-functie. Met deze functie kunt u aangepaste dashboards maken en beheren waar u op maat gemaakte widgets kunt maken, toevoegen en bewerken om belangrijke metrische gegevens die relevant zijn voor uw organisatie te visualiseren.

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Aangepaste dashboards maken

Als u eerst een aangepast dashboard wilt maken, navigeert u naar het dashboardoverzicht. Selecteren **[!UICONTROL Dashboards]** van de linkernavigatie van het Platform UI gevolgd door **[!UICONTROL Create dashboard]**.

![Het dashboardoverzicht met dashboards in de linkernavigatie en &quot;creëren dashboard&quot;benadrukte.](./images/user-defined-dashboards/create-dashboard.png)

Voordat u een aangepast dashboard toevoegt, is de dashboardvoorraad leeg en wordt &#39;&#39;Geen dashboards gevonden&#39;&#39; weergegeven. bericht. Zodra u hebt gemaakt, worden alle door de gebruiker gedefinieerde dashboards vermeld in de dashboardvoorraad.

De [!UICONTROL Create dashboard] wordt weergegeven. Voer een beschrijvende naam in voor de verzameling widgets die u wilt maken en selecteer **[!UICONTROL Save]**.

![Het dialoogvenster Het dashboard maken.](./images/user-defined-dashboards/create-dashboard-dialog.png)

Het nieuwe lege dashboard wordt met de door u gekozen naam weergegeven in de linkerbovenhoek van de weergave.

## Een widget maken {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Maximum aantal widgets"
>abstract="Door de gebruiker gedefinieerde dashboards ondersteunen maximaal tien widgets. Nadat u tien widgets aan uw dashboard hebt toegevoegd, [!UICONTROL Add new widget] is uitgeschakeld en wordt grijs weergegeven."

Selecteer in de nieuwe dashboardweergave de optie **[!UICONTROL Add new widget]** om het maken van de widget te starten.

>[!IMPORTANT]
>
>Door de gebruiker gedefinieerde dashboards ondersteunen maximaal tien widgets. Nadat u tien widgets aan uw dashboard hebt toegevoegd, [!UICONTROL Add new widget] is uitgeschakeld en wordt grijs weergegeven.

![Het nieuwe lege dashboard met de markering Nieuwe widget toevoegen.](./images/user-defined-dashboards/add-new-widget.png)

### Widget-composer

De werkruimte van de widgetcomposer wordt weergegeven. Selecteer vervolgens **[!UICONTROL Select data]** om het gegevensmodel te kiezen waaruit u kenmerken aan uw widgets wilt toevoegen.

![De werkruimte van de widgetcomposer.](./images/user-defined-dashboards/widget-composer.png)

De [!UICONTROL Select data] wordt weergegeven. Selecteer een gegevensmodel in de linkerkolom om een voorvertoningslijst van alle beschikbare lijsten te tonen.

>[!NOTE]
>
>Door de gebruiker gedefinieerde dashboards ondersteunen momenteel alleen het model met profielgegevens. Meer opties worden ondersteund.

![Het dialoogvenster Gegevens selecteren.](./images/user-defined-dashboards/select-data-dialog.png)

De voorvertoningslijst bevat informatie over de tabellen in het gegevensmodel. De onderstaande tabel bevat een beschrijving van de kolomvelden en de mogelijke waarden ervan.

| Kolomveld | Beschrijving |
|---|---|
| [!UICONTROL Title] | De naam van de tabel. |
| [!UICONTROL Table type] | Het type tabel. Mogelijke typen zijn: `fact`, `dimension`, en `none`. |
| [!UICONTROL Lookups] | Het aantal tabellen dat is gekoppeld aan de gekozen tabel. |

Selecteren **[!UICONTROL Next]** om uw keuze van het gegevensmodel te bevestigen. In de volgende weergave wordt een lijst weergegeven met de beschikbare tabellen in de linkertrack. Selecteer een tabel voor een uitgebreide uitsplitsing van de gegevens in de geselecteerde tabel.

De [!UICONTROL Preview] deelvenster bevat tabbladen voor [!UICONTROL Sample records] en [!UICONTROL Attributes]. De [!UICONTROL Sample records] bevat een subset van de records uit de geselecteerde tabel in een tabelweergave. De [!UICONTROL Attributes] bevat de kenmerknaam, het gegevenstype en de brontabel voor elk kenmerk dat aan de geselecteerde tabel is gekoppeld.

Selecteer een tabel in de lijst in de linkertrack om gegevens voor de widget op te geven en selecteer **[!UICONTROL Select]** om terug te keren naar de widgetcomposer.

![Het dialoogvenster Gegevens selecteren met de optie gemarkeerd.](./images/user-defined-dashboards/select-a-table.png)

De widgetcomposer is nu gevuld met gegevens uit de door u gekozen tabel.

Het gegevensmodel en de geselecteerde tabel worden boven aan de linkertrack weergegeven. De kenmerken die beschikbaar zijn om de widget te maken, worden in de kolom Kenmerken weergegeven.

![Een widget die is gevuld met gegevens binnen de widgetcomposer.](./images/user-defined-dashboards/populated-widget-composer.png)

>[!TIP]
>
>U kunt het gekozen gegevensmodel wijzigen door het potloodpictogram te selecteren (![Potloodpictogram.](./images/user-defined-dashboards/edit-icon.png)) in het linkerspoor.

Selecteer het pictogram Toevoegen (./images/user-defined-dashboards/add-icon.png) naast een kenmerknaam om een kenmerk aan de X- of Y-as toe te voegen.

![De widgetcomposer met het vervolgkeuzemenu voor het pictogram Toevoegen gemarkeerd om kenmerken aan een widgetas toe te voegen.](./images/user-defined-dashboards/attributes-dropdown.png)

Selecteer vervolgens het type grafiek of grafiek in het menu [!UICONTROL Marks] vervolgkeuzelijst voor het genereren van een voorvertoning van de huidige instellingen van de widget. In de [!UICONTROL Properties] aan de rechterkant van het scherm typt u een naam voor de widget in het deelvenster [!UICONTROL Widget title] tekstveld.

![De widgetcomposer met het tekstveld Markeringen in de vervolgkeuzelijst en de widgettitel gemarkeerd.](./images/user-defined-dashboards/marks-dropdown-widget-title.png)

Wanneer u tevreden bent met uw widget, selecteert u **[!UICONTROL Save]**. Een tikpictogram onder de widgetnaam geeft aan dat de widget is opgeslagen.

>[!NOTE]
>
>Als u de widget opslaat in de widgetcomposer, wordt de widget lokaal op het dashboard opgeslagen. Als u de dashboardeditor verlaat zonder het dashboard op te slaan, wordt de widget niet opgeslagen op het dashboard.

![Bevestiging van opslaan van nieuwe widget.](./images/user-defined-dashboards/save-confirmation.png)

Selecteren **[!UICONTROL Cancel]** om terug te keren naar uw aangepaste dashboard.

![De widgetcomposer met een voorbeeldwidget gemaakt.](./images/user-defined-dashboards/composed-widget.png)

>[!TIP]
>
>Selecteer het instellingspictogram naast de naam van het dashboard om meer informatie over het maken van het dashboard weer te geven. U kunt de naam van het dashboard wijzigen in het dialoogvenster dat verschijnt.

U kunt widgets opnieuw rangschikken en de grootte ervan wijzigen in deze werkruimte. Selecteren **[!UICONTROL Save]** om de naam en de geconfigureerde indeling van het dashboard te behouden.

![Het door de gebruiker gedefinieerde dashboard met een aangepaste widget en de knop Opslaan gemarkeerd.](./images/user-defined-dashboards/user-defined-dashboard.png)

Om ervoor te zorgen dat elke query voor een Real-time Customer Data Platform-inzichten over voldoende bronnen beschikt om efficiënt te worden uitgevoerd, houdt de API het gebruik van bronnen bij door er corrency-sleuven aan elke query toe te wijzen. Het systeem kan tot vier gezamenlijke vragen verwerken, en daarom zijn vier gezamenlijke vraaggroeven beschikbaar op elk bepaald ogenblik. Vragen worden in een wachtrij geplaatst op basis van sleuven voor gelijktijdige uitvoering en wachten vervolgens in de wachtrij totdat voldoende sleuven voor gelijktijdige uitvoering beschikbaar zijn.

## Volgende stappen

Door dit document te lezen hebt u een beter inzicht in hoe u een aangepast dashboard kunt maken en hoe u aangepaste widgets voor dat dashboard kunt maken, bewerken en bijwerken.

Om de beschikbare pre-gevormde metriek en visualisaties voor te ontdekken [profielen](./guides/profiles.md#standard-widgets), [segmenten](./guides/segments.md#standard-widgets), en [bestemmingen](./guides/destinations.md#standard-widgets) dashboards, zie de lijst van standaardwidgets in hun respectieve documentatie.
