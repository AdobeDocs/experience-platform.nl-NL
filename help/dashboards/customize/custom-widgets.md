---
keywords: Experience Platform;gebruikersinterface;UI;dashboards;dashboard;profielen;segmenten;bestemmingen;vergunningsgebruik;widgets;metriek;
title: Aangepaste widgets maken voor dashboards
description: 'Deze handleiding bevat stapsgewijze instructies voor het maken van aangepaste widgets voor gebruik in Adobe Experience Platform-dashboards. '
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---


# Aangepaste widgets maken voor dashboards

In Adobe Experience Platform kunt u de gegevens van uw organisatie bekijken en ermee communiceren met behulp van meerdere dashboards. U kunt bepaalde dashboards ook bijwerken door nieuwe widgets aan uw dashboardmening toe te voegen. Naast de standaardwidgets die door Adobe worden geboden, kunt u ook aangepaste widgets maken en deze delen in uw organisatie.

Deze handleiding bevat stapsgewijze instructies voor het maken en toevoegen van aangepaste widgets aan de [!UICONTROL Profiles]-, [!UICONTROL Segments]- en [!UICONTROL Destinations]-dashboards in de gebruikersinterface van het Platform.

Raadpleeg de handleiding bij [standaardwidgets toevoegen aan uw dashboards](standard-widgets.md) voor meer informatie over standaardwidgets.

>[!NOTE]
>
>De widgets die worden weergegeven in het dashboard [!UICONTROL License usage] kunnen niet worden aangepast. Lees voor meer informatie over dit unieke dashboard de [licentiegebruiksdashboarddocumentatie](../guides/license-usage.md).

## Widget-bibliotheek {#widget-library}

Deze gids vereist toegang tot [!UICONTROL Widget library] binnen Experience Platform. Als u meer wilt weten over de widgetbibliotheek en hoe u deze kunt openen binnen de gebruikersinterface, leest u eerst het [overzicht van de widgetbibliotheek](widget-library.md).

## Aan de slag met aangepaste widgets

In de widgetbibliotheek kunt u op het tabblad **[!UICONTROL Custom]** widgets maken en deze delen met andere gebruikers in uw organisatie om de weergave van uw dashboards aan te passen.

>[!IMPORTANT]
>
>Uw organisatie kan maximaal 20 aangepaste widgets maken in de widgetbibliotheek.

Selecteer het tabblad **[!UICONTROL Custom]** om aangepaste widgets te maken of om aangepaste widgets weer te geven die uw organisatie al heeft gemaakt.

![](../images/customization/custom-widgets.png)

## Een aangepaste widget maken

Als u een aangepaste widget wilt maken, selecteert u **[!UICONTROL Create widget]** in de rechterbovenhoek van de widgetbibliotheek of selecteert u **[!UICONTROL Create]** in het midden van de widgetbibliotheek als dit de eerste aangepaste widget van uw organisatie is.

![](../images/customization/create-widget.png)

Geef in het dialoogvenster **[!UICONTROL Create widget]** een titel en beschrijving op voor de nieuwe widget en kies het kenmerk dat u de widget wilt weergeven.

>[!NOTE]
>
>De lijst van beschikbare attributen hangt van het schema af dat voor uw organisatie is gevormd. Lees de handleiding over [het bewerken van het schema om aangepaste widgets te maken](edit-schema.md) voor meer informatie over kenmerkselectie en schemaconfiguratie.

Als u een kenmerk wilt kiezen, selecteert u het keuzerondje naast het kenmerk dat u wilt toevoegen.

>[!NOTE]
>
>Per widget kan slechts één kenmerk worden geselecteerd en per kenmerk kan slechts één widget worden gemaakt. Als er al een widget is gemaakt voor een kenmerk, wordt het kenmerk grijs weergegeven.

![](../images/customization/create-widget-dialog.png)

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

Als u de nieuwe widget wilt opslaan en wilt terugkeren naar het tabblad [!UICONTROL Custom], selecteert u **[!UICONTROL Create]**.

![](../images/customization/create-widget-select-attribute.png)

Uw nieuwe widget kan nu aan een dashboard worden toegevoegd door de widget in de bibliotheek te kiezen en **[!UICONTROL Add widget]** te selecteren.

![](../images/customization/custom-widgets-new.png)

## Een aangepaste widget verbergen

Nadat een widget aan de bibliotheek is toegevoegd, kan het worden verborgen door de ellipsen (`...`) op de widgetkaart te selecteren en dan **[!UICONTROL Hide widget]** te selecteren. U kunt de widget ook voorvertonen en bewerken vanuit dezelfde vervolgkeuzelijst.

Als u verborgen widgets wilt weergeven, selecteert u **[!UICONTROL Show hidden widgets]** in de rechterbovenhoek van de widgetbibliotheek.

>[!WARNING]
>
>Als u een widget verbergt in de bibliotheek, wordt de widget niet verwijderd uit de dashboards van individuele gebruikers. Als een widget niet meer in uw organisatie moet worden gebruikt, moet u dit rechtstreeks doorgeven aan alle gebruikers van het Platform, omdat zij de widget uit hun dashboards moeten verwijderen.

![](../images/customization/hide-widget.png)

## Een aangepaste widget bewerken

U kunt aangepaste widgets in de widgetbibliotheek bewerken door de ellipsen (`...`) op de widgetkaart te selecteren en vervolgens **[!UICONTROL Edit]** te selecteren in het vervolgkeuzemenu.

![](../images/customization/custom-widget-edit.png)

In het dialoogvenster **[!UICONTROL Edit widget]** kunt u de titel en beschrijving van de widget bewerken en een voorvertoning weergeven en verschillende visualisaties selecteren. Nadat u de gewenste wijzigingen hebt aangebracht, selecteert u **[!UICONTROL Save]** om de wijzigingen op te slaan en terug te keren naar het tabblad Aangepaste widgets.

>[!WARNING]
>
>Als u een widget in de bibliotheek bewerkt, wordt de widget niet voor individuele gebruikers bijgewerkt. Als een widget is bijgewerkt, dient u dit rechtstreeks door te geven aan alle gebruikers van het Platform, aangezien zij de verouderde widget uit hun dashboards moeten verwijderen en vervolgens de bijgewerkte widget uit de widgetbibliotheek moeten selecteren en toevoegen.

![](../images/customization/edit-widget.png)

## Volgende stappen

Nadat u dit document hebt gelezen, hebt u toegang tot de widgetbibliotheek en kunt u deze gebruiken om aangepaste widgets voor uw organisatie te maken en toe te voegen. Als u de grootte en locatie wilt wijzigen van widgets die in het dashboard worden weergegeven, raadpleegt u de [handleiding voor het wijzigen van dashboards](modify.md).
