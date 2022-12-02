---
keywords: Experience Platform;gebruikersinterface;UI;dashboards;dashboard;profielen;segmenten;bestemmingen;vergunningsgebruik;widgets;metriek;
title: Aangepaste widgets maken voor dashboards
description: Deze handleiding bevat stapsgewijze instructies voor het maken van aangepaste widgets voor gebruik in Adobe Experience Platform-dashboards.
exl-id: 0168ab1e-0b7d-4faf-852e-7208a2b09a04
source-git-commit: 386d805eadf335b95b6eac92c7663fcee17b4b2d
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---

# Aangepaste widgets maken voor dashboards

In Adobe Experience Platform kunt u de gegevens van uw organisatie bekijken en ermee communiceren met behulp van meerdere dashboards. U kunt bepaalde dashboards ook bijwerken door nieuwe widgets aan uw dashboardmening toe te voegen. Naast de standaardwidgets die door Adobe worden geboden, kunt u ook aangepaste widgets maken en deze delen in uw organisatie.

Deze handleiding bevat stapsgewijze instructies voor het maken en toevoegen van aangepaste widgets aan de [!UICONTROL Profiles], [!UICONTROL Segments], en [!UICONTROL Destinations] dashboards in Platform UI.

Raadpleeg de handleiding voor meer informatie over standaardwidgets [standaardwidgets toevoegen aan uw dashboards](standard-widgets.md).

>[!NOTE]
>
>De widgets die worden weergegeven in het dialoogvenster [!UICONTROL License usage] het dashboard kan niet worden aangepast. Voor meer informatie over dit unieke dashboard leest u de [dashboarddocumentatie voor licentiegebruik](../guides/license-usage.md).

## Widget-bibliotheek {#widget-library}

Deze gids vereist toegang tot [!UICONTROL Widget library] in Experience Platform. Als u meer wilt weten over de widgetbibliotheek en hoe u deze kunt openen in de gebruikersinterface, leest u eerst de [Overzicht van widgetbibliotheek](widget-library.md).

## Aan de slag met aangepaste widgets

In de widgetbibliotheek **[!UICONTROL Custom]** kunt u widgets maken en deze delen met andere gebruikers in uw organisatie om de weergave van uw dashboards aan te passen.

>[!IMPORTANT]
>
>Uw organisatie kan maximaal 20 aangepaste widgets maken in de widgetbibliotheek.

Selecteer **[!UICONTROL Custom]** gebruiken om aangepaste widgets te maken of om aangepaste widgets weer te geven die uw organisatie al heeft gemaakt.

![De werkruimte van de widgetbibliotheek met het tabblad Aangepast gemarkeerd.](../images/customization/custom-widgets.png)

## Een aangepaste widget maken

Als u een aangepaste widget wilt maken, selecteert u **[!UICONTROL Create widget]** in de rechterbovenhoek van de widgetbibliotheek of, als dit de eerste aangepaste widget van uw organisatie is, selecteert u **[!UICONTROL Create]** in het midden van de widgetbibliotheek.

![Het tabblad Aangepast van de werkruimte van de widgetbibliotheek met de optie Maken gemarkeerd.](../images/customization/create-widget.png)

In de **[!UICONTROL Create widget]** geeft u een titel en een beschrijving voor de nieuwe widget op en kiest u het kenmerk dat de widget moet weergeven.

>[!NOTE]
>
>De lijst van beschikbare attributen hangt van het schema af dat voor uw organisatie is gevormd. Voor meer informatie over kenmerkselectie en schemaconfiguratie leest u de hulplijn op [het bewerken van het schema om aangepaste widgets te maken](edit-schema.md).

Als u een kenmerk wilt kiezen, selecteert u het keuzerondje naast het kenmerk dat u wilt toevoegen.

>[!NOTE]
>
>Per widget kan slechts één kenmerk worden geselecteerd en per kenmerk kan slechts één widget worden gemaakt. Als er al een widget is gemaakt voor een kenmerk, wordt het kenmerk grijs weergegeven.

![Het dialoogvenster Widget maken.](../images/customization/create-widget-dialog.png)

## Selecteer een visualisatie

Nadat u een kenmerk hebt geselecteerd, wordt een voorvertoning van de nieuwe widget weergegeven in het dialoogvenster. Kunstmatige intelligentie wordt gebruikt om automatisch een visualisatie te selecteren die de attributengegevens het best past, en om extra visualisatieopties te verstrekken die u manueel kunt selecteren.

Afhankelijk van het kenmerk raadt de AI verschillende visualisatieopties aan. De volledige lijst met visualisaties bevat:

* Horizontaal staafdiagram: Horizontale lijnen worden gebruikt om waarden te vertegenwoordigen.
* Verticaal staafdiagram: Verticale lijnen worden gebruikt om waarden te vertegenwoordigen.
* Donut-grafiek: Net als bij een cirkeldiagram worden waarden weergegeven als delen of delen van een geheel.
* Spreiding: Hiermee geeft u een horizontale en verticale as op om waarden aan te geven.
* Lijndiagram: Waarden worden op één regel weergegeven om wijzigingen gedurende een bepaalde periode weer te geven.
* Nummerkaart: Geeft een samenvattingsnummer weer dat een enkele sleutelwaarde vertegenwoordigt.
* Gegevenstabel: Waarden worden als rijen in een tabel weergegeven.

>[!NOTE]
>
>De enige metrische waarde die momenteel voor alle kenmerken wordt ondersteund, is het aantal profielen.
>
>De gegevens in de voorbeeldwidget dienen alleen ter illustratie. In de voorvertoning worden geen feitelijke gegevens van uw organisatie weergegeven.

Om uw nieuwe widget op te slaan en terug te keren naar de [!UICONTROL Custom] tab, selecteert u **[!UICONTROL Create]**.

![Het dialoogvenster Widget maken met de visualisatieopties en de optie Gemarkeerd maken.](../images/customization/create-widget-select-attribute.png)

Uw nieuwe widget kan nu aan een dashboard worden toegevoegd door de widget te kiezen in de bibliotheek en **[!UICONTROL Add widget]**.

![Het tabblad Aangepast van de werkruimte van de widgetbibliotheek met de nieuwe widget en de Add-widget gemarkeerd.](../images/customization/custom-widgets-new.png)

## Een aangepaste widget verbergen

Nadat een widget aan de bibliotheek is toegevoegd, kan deze worden verborgen door de ellipsen te selecteren (`...`) op de widget-kaart en selecteer vervolgens **[!UICONTROL Hide widget]**. U kunt de widget ook voorvertonen en bewerken vanuit dezelfde vervolgkeuzelijst.

Selecteer **[!UICONTROL Show hidden widgets]** in de rechterbovenhoek van de widgetbibliotheek.

>[!WARNING]
>
>Als u een widget verbergt in de bibliotheek, wordt de widget niet verwijderd uit de dashboards van individuele gebruikers. Als een widget niet meer in uw organisatie moet worden gebruikt, moet u dit rechtstreeks doorgeven aan alle gebruikers van het Platform, omdat zij de widget uit hun dashboards moeten verwijderen.

![Het tabblad Aangepast van de werkruimte van de widgetbibliotheek met de opties in het vervolgkeuzemenu van de widget en de optie Verborgen widgets tonen.](../images/customization/hide-widget.png)

## Een aangepaste widget bewerken

U kunt aangepaste widgets in de widgetbibliotheek bewerken door de ellipsen te selecteren (`...`) op de widget-kaart en selecteer vervolgens **[!UICONTROL Edit]** in het vervolgkeuzemenu.

![De opties in het vervolgkeuzemenu van de widget met de ovalen en Bewerken gemarkeerd.](../images/customization/custom-widget-edit.png)

Op de **[!UICONTROL Edit widget]** kunt u de titel en beschrijving van de widget bewerken en een voorvertoning weergeven en verschillende visualisaties selecteren. Selecteer **[!UICONTROL Save]** om uw wijzigingen op te slaan en terug te keren naar het tabblad Aangepaste widgets.

>[!WARNING]
>
>Als u een widget in de bibliotheek bewerkt, wordt de widget niet voor individuele gebruikers bijgewerkt. Als een widget is bijgewerkt, dient u dit rechtstreeks door te geven aan alle gebruikers van het Platform, aangezien zij de verouderde widget uit hun dashboards moeten verwijderen en vervolgens de bijgewerkte widget uit de widgetbibliotheek moeten selecteren en toevoegen.

![Het dialoogvenster Widget bewerken.](../images/customization/edit-widget.png)

## Volgende stappen

Nadat u dit document hebt gelezen, hebt u toegang tot de widgetbibliotheek en kunt u deze gebruiken om aangepaste widgets voor uw organisatie te maken en toe te voegen. Als u de grootte en locatie wilt wijzigen van widgets die in het dashboard worden weergegeven, raadpleegt u de [hulplijn voor dashboards wijzigen](modify.md).
