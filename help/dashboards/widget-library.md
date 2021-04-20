---
keywords: Experience Platform;gebruikersinterface;UI;dashboards;dashboard;profielen;segmenten;bestemmingen;vergunningsgebruik
title: Widget-widget-bibliotheek gebruiken om dashboardwidgets toe te voegen en te maken
description: 'Deze handleiding bevat stapsgewijze instructies voor het toevoegen van standaardwidgets en het maken van aangepaste widgets voor het visualiseren van dashboardgegevens in Adobe Experience Platform. '
topic: guide
translation-type: tm+mt
source-git-commit: 27444a0106eacbd69149168d7439773ebbb26119
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 0%

---


# (bèta) Widgetbibliotheek {#widget-library}

>[!IMPORTANT]
>
>De dashboardfunctionaliteit bevindt zich momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

In de Adobe Experience Platform-gebruikersinterface kunt u de gegevens van uw organisatie bekijken en ermee werken met meerdere dashboards. U kunt een aantal van deze dashboards ook bijwerken door nieuwe widgets aan uw dashboardmening toe te voegen. Naast de standaardwidgets die door Adobe worden geboden, kunt u aangepaste widgets maken en deze delen in uw organisatie.

Deze handleiding bevat stapsgewijze instructies voor het toevoegen van standaardwidgets en het maken van aangepaste widgets om de informatie aan te passen die wordt weergegeven in de [!UICONTROL Profielen] en [!UICONTROL Segmenten] dashboards in de interface van het Platform.

Voor informatie over hoe u de locatie en grootte van widgets in de [!UICONTROL Profielen], [!UICONTROL Doelen] en [!UICONTROL Segmenten] dashboards kunt wijzigen, raadpleegt u de [handleiding voor het wijzigen van dashboards](modify.md).

>[!NOTE]
>
>De widgets die worden weergegeven in het [!UICONTROL Licentiegebruik]-dashboard kunnen niet worden aangepast. Lees voor meer informatie over dit unieke dashboard de [licentiegebruiksdashboarddocumentatie](guides/license-usage.md).

## De widgetbibliotheek openen

Vanuit elk dashboard (bijvoorbeeld het dashboard Profielen) kunt u **[!UICONTROL Het dashboard wijzigen]** gevolgd door **[!UICONTROL Widgetbibliotheek]** selecteren om de widgetbibliotheek te openen.

>[!NOTE]
>
>De [!UICONTROL Widget-bibliotheek]-knop verschijnt slechts eenmaal [!UICONTROL Het dashboard wijzigen] is geselecteerd.

![](images/customization/modify-dashboard.png)

![](images/customization/widget-library-button.png)

De [!UICONTROL Widget-bibliotheek] bevat twee tabbladen: [!UICONTROL Standaard] en [!UICONTROL Aangepast].

* Het tabblad **[!UICONTROL Standaard]** bevat widgets die door Adobe zijn gemaakt en waarmee u het dashboard kunt bijwerken met behulp van deze standaardmeetwaarden. Zie de sectie [standaardwidgets](#standard-widgets) in deze handleiding voor meer informatie over het toevoegen van standaardwidgets aan het dashboard.
* Met het tabblad **[!UICONTROL Aangepast]** kunt u widgets maken en delen binnen uw organisatie. Raadpleeg de sectie [Aangepaste widgets](#custom-widgets) in deze handleiding voor volledige stappen voor het maken van uw eigen widgets.

![](images/customization/widget-library.png)

## Standaardwidgets {#standard-widgets}

Het tabblad **[!UICONTROL Standaard]** bevat widgets die door Adobe zijn gemaakt, en die zijn onderverdeeld in categorieën. Als u een categorie selecteert, worden de beschikbare widgets voor dat dashboard weergegeven. Elke widget wordt weergegeven als een kaart met de titel, beschrijving en een voorbeeldvisualisatie van de metrische code.

>[!NOTE]
>
>Widgets kunnen alleen worden toegevoegd aan het dashboard dat overeenkomt met de geselecteerde categorie. U kunt bijvoorbeeld alleen widgets uit de categorie [!UICONTROL Profielen] toevoegen aan het dashboard [!UICONTROL Profielen].

![](images/customization/standard-widgets.png)

Als u een standaardwidget wilt kiezen die u aan het dashboard wilt toevoegen, markeert u de widget en schakelt u het selectievakje voor de widget in. Als er ten minste één widget is geselecteerd, wordt de knop **[!UICONTROL Widget toevoegen]** belicht.

>[!NOTE]
>
>De teller in de hoger-juiste hoek van de widgetbibliotheek toont het totale aantal geselecteerde widgets.

Selecteer **[!UICONTROL Widget toevoegen]** om geselecteerde widgets aan uw dashboard toe te voegen.

![](images/customization/add-widget.png)

## Aangepaste widgets {#custom-widgets}

>[!IMPORTANT]
>
>Uw organisatie kan maximaal 20 aangepaste widgets maken in de widgetbibliotheek.

Als u de weergave van dashboards in het Experience Platform verder wilt aanpassen, kunt u widgets maken en deze delen met andere gebruikers in uw organisatie. Selecteer in de widgetbibliotheek het tabblad **[!UICONTROL Aangepast]** om aangepaste widgets te maken. Op het tabblad [!UICONTROL Aangepast] zijn alle widgets die door uw organisatie zijn gemaakt zichtbaar. In dit voorbeeld zijn nog geen aangepaste widgets gemaakt.

![](images/customization/custom-widgets.png)

### Kenmerken selecteren

Als u aangepaste widgets wilt maken, moeten de kenmerken van het realtime-klantprofiel worden geïdentificeerd om ervoor te zorgen dat de gegevens worden opgenomen als onderdeel van de dagelijkse momentopname. Als uw organisatie geen Profielkenmerken heeft geselecteerd, wordt de knop [!UICONTROL Schema configureren] in de rechterbovenhoek van de widgetbibliotheek weergegeven.

Wanneer ten minste één aangepast kenmerk is geselecteerd, wordt de knop [!UICONTROL Schema bewerken] in de rechterbovenhoek van de widgetbibliotheek weergegeven. Selecteer **[!UICONTROL Schema bewerken]** om het dialoogvenster **[!UICONTROL Unieschemaveld]** te openen om de geselecteerde kenmerken weer te geven en meer kenmerken toe te voegen.

>[!IMPORTANT]
>
>Een organisatie kan maximaal 20 kenmerken selecteren.

![](images/customization/edit-schema.png)

Als u een kenmerk wilt selecteren, navigeert u naar het kenmerk in het samenvoegingsschema (of gebruikt u de zoekfunctie) en schakelt u het selectievakje naast het kenmerk in. Als u het selectievakje inschakelt, wordt het kenmerk ook toegevoegd aan de lijst **[!UICONTROL Geselecteerde kenmerken]** rechts in het dialoogvenster.

>[!NOTE]
>
>Een kenmerk kan alleen zichtbaar zijn voor selectie als het een van de volgende kenmerken is: Tekenreeks, datum, datum en tijd, Boolean, kort, lang, geheel getal of byte. De gegevenstypen Map en Double worden niet ondersteund en worden grijs weergegeven zodat ze niet kunnen worden geselecteerd.

Nadat u de kenmerken hebt gekozen die u wilt toevoegen, selecteert u **[!UICONTROL Opslaan]** om uw kenmerken op te slaan en terug te keren naar het tabblad Aangepaste widgets.

Nieuw geselecteerde kenmerken zijn beschikbaar na de dagelijkse momentopname wanneer de gegevens worden vernieuwd.

![](images/customization/select-attribute.png)

### Een aangepaste widget maken

Als u een aangepaste widget wilt maken, selecteert u **[!UICONTROL Maken]** in het midden van de widgetbibliotheek of selecteert u **[!UICONTROL Widget maken]** in de rechterbovenhoek van de widgetbibliotheek als er al aangepaste widgets zijn gemaakt.

![](images/customization/create-widget.png)

In het dialoogvenster **[!UICONTROL Widget maken]** kunt u een titel en een beschrijving voor de nieuwe widget opgeven en het kenmerk kiezen dat de widget moet weergeven. Als u een kenmerk wilt kiezen, selecteert u het keuzerondje naast het kenmerk dat u wilt toevoegen.

>[!NOTE]
>
>Per widget kan slechts één kenmerk worden geselecteerd. Als er al een widget is gemaakt voor een kenmerk, wordt het kenmerk grijs weergegeven.

![](images/customization/create-widget-dialog.png)

Er wordt een voorvertoning van de nieuwe widget weergegeven in het dialoogvenster en er wordt een horizontale staafgrafiek met mokgegevens weergegeven.

>[!NOTE]
>
>De enige metrische waarde die momenteel voor alle kenmerken wordt ondersteund, is het aantal profielen en de enige visualisatie die momenteel wordt ondersteund voor aangepaste widgets is een horizontale staafgrafiek.
>
>De gegevens in de voorbeeldwidget dienen alleen ter illustratie. In de voorvertoning worden geen feitelijke gegevens van uw organisatie weergegeven.

![](images/customization/create-widget-select-attribute.png)

Als u de nieuwe widget wilt opslaan en wilt terugkeren naar het tabblad [!UICONTROL Aangepast], selecteert u **[!UICONTROL Maken]**. Uw nieuwe widget kan nu aan een dashboard worden toegevoegd door de widget in de bibliotheek te kiezen en **[!UICONTROL Widget toevoegen]** te selecteren.

### Een aangepaste widget archiveren

Nadat een widget aan de bibliotheek is toegevoegd, kan deze worden gearchiveerd met de knop **[!UICONTROL Archiveren]**. U kunt de widget ook bewerken om de titel- of beschrijvingsvelden bij te werken.

## Volgende stappen

Nadat u dit document hebt gelezen, hebt u nu toegang tot [!UICONTROL Widget-bibliotheek] en kunt u deze gebruiken om widgets aan een dashboard toe te voegen of aangepaste widgets voor uw organisatie te maken. Als u de grootte en locatie van widgets in het dashboard wilt wijzigen, raadpleegt u de [handleiding voor het wijzigen van dashboards](modify.md).