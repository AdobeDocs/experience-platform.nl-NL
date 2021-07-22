---
keywords: Experience Platform;gebruikersinterface;UI;dashboards;dashboard;profielen;segmenten;bestemmingen;vergunningsgebruik;widgets;metriek;
title: Aangepaste widgets maken voor dashboards
description: 'Deze handleiding bevat stapsgewijze instructies voor het maken van aangepaste widgets voor gebruik in Adobe Experience Platform-dashboards. '
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
source-git-commit: a07eb2baec48ad514ff0afc0548f53baf34da561
workflow-type: tm+mt
source-wordcount: '570'
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

Als u een aangepaste widget wilt maken, selecteert u **[!UICONTROL Create]** in het midden van de widgetbibliotheek. Als er al aangepaste widgets zijn gemaakt, selecteert u **[!UICONTROL Create widget]** in de rechterbovenhoek van de widgetbibliotheek.

![](../images/customization/create-widget.png)

In het dialoogvenster **[!UICONTROL Create widget]** kunt u een titel en beschrijving opgeven voor de nieuwe widget en het kenmerk kiezen dat u de widget wilt weergeven.

>[!NOTE]
>
>De lijst van beschikbare attributen hangt van het schema af dat voor uw organisatie is gevormd. Lees de handleiding over [het bewerken van het schema om aangepaste widgets te maken](edit-schema.md) voor meer informatie over kenmerkselectie en schemaconfiguratie.

Als u een kenmerk wilt kiezen, selecteert u het keuzerondje naast het kenmerk dat u wilt toevoegen.

>[!NOTE]
>
>Per widget kan slechts één kenmerk worden geselecteerd en per kenmerk kan slechts één widget worden gemaakt. Als er al een widget is gemaakt voor een kenmerk, wordt het kenmerk grijs weergegeven.

![](../images/customization/create-widget-dialog.png)

## Aangepaste widget voorvertonen

Er wordt een voorvertoning van de nieuwe widget weergegeven in het dialoogvenster en er wordt een horizontale staafgrafiek met mokgegevens weergegeven.

>[!NOTE]
>
>De enige metrische waarde die momenteel voor alle kenmerken wordt ondersteund, is het aantal profielen en de enige visualisatie die momenteel wordt ondersteund voor aangepaste widgets is een horizontale staafgrafiek.
>
>De gegevens in de voorbeeldwidget dienen alleen ter illustratie. In de voorvertoning worden geen feitelijke gegevens van uw organisatie weergegeven.

![](../images/customization/create-widget-select-attribute.png)

Als u de nieuwe widget wilt opslaan en wilt terugkeren naar het tabblad [!UICONTROL Custom], selecteert u **[!UICONTROL Create]**. Uw nieuwe widget kan nu aan een dashboard worden toegevoegd door de widget in de bibliotheek te kiezen en **[!UICONTROL Add widget]** te selecteren.

## Een aangepaste widget archiveren

Nadat een widget aan de bibliotheek is toegevoegd, kan het worden gearchiveerd gebruikend **[!UICONTROL Archive]** knoop. U kunt de widget ook bewerken om de titel- of beschrijvingsvelden bij te werken.

## Volgende stappen

Nadat u dit document hebt gelezen, hebt u toegang tot de widgetbibliotheek en kunt u deze gebruiken om aangepaste widgets voor uw organisatie te maken en toe te voegen. Als u de grootte en locatie wilt wijzigen van widgets die in het dashboard worden weergegeven, raadpleegt u de [handleiding voor het wijzigen van dashboards](modify.md).
