---
keywords: Experience Platform;gebruikersinterface;UI;dashboards;dashboard;profielen;segmenten;bestemmingen;vergunningsgebruik
title: Schema bewerken om aangepaste dashboardwidgets te maken
description: 'Deze handleiding bevat stapsgewijze instructies voor het selecteren van kenmerken en het configureren van het schema van uw organisatie om aangepaste widgets voor Adobe Experience Platform-dashboards te maken. '
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Schema bewerken om aangepaste widgets te maken

Als u aangepaste widgets voor Adobe Experience Platform-dashboards wilt maken, moet u eerst de realtime kenmerken van het klantprofiel identificeren waarop de widgets worden gebaseerd.

Deze handleiding bevat stapsgewijze instructies voor het bewerken van het schema van uw organisatie door kenmerken te selecteren om aangepaste dashboardwidgets te maken.

Zodra de attributen zijn geselecteerd en het schema is gevormd, kunt u met de stappen voor [het creëren van douanewidgets voor uw dashboards ](custom-widgets.md) te werk gaan.

>[!NOTE]
>
>Gebruikers moeten de machtiging &quot;Standaarddashboards beheren&quot; hebben om het schema te kunnen bewerken. Raadpleeg de [handleiding voor dashboardmachtigingen](../permissions.md) voor stappen voor het verlenen van toegangsmachtigingen voor dashboards.

## Widget-bibliotheek {#widget-library}

Deze gids vereist toegang tot [!UICONTROL Widget library] binnen Experience Platform. Als u meer wilt weten over de widgetbibliotheek en hoe u deze kunt openen binnen de gebruikersinterface, leest u eerst het [overzicht van de widgetbibliotheek](widget-library.md).

## Schema bewerken

In de widgetbibliotheek kunt u op het tabblad **[!UICONTROL Custom]** widgets maken en deze delen met andere gebruikers in uw organisatie om de weergave van uw dashboards aan te passen.

Voordat u aangepaste widgets kunt maken, moeten de kenmerken van het profiel van de klant in realtime worden geselecteerd om ervoor te zorgen dat de gegevens worden opgenomen als onderdeel van de dagelijkse momentopname.

>[!IMPORTANT]
>
>Uw organisatie kan maximaal 20 kenmerken selecteren.

Als uw organisatie geen profielkenmerken heeft geselecteerd, begint u met het selecteren van **[!UICONTROL Edit schema]** in de rechterbovenhoek van de widgetbibliotheek.

Wanneer ten minste één aangepast kenmerk is gemaakt, selecteert u **[!UICONTROL Edit schema]** om de geselecteerde kenmerken weer te geven en meer toe te voegen.

![](../images/customization/edit-schema.png)

## Een kenmerk selecteren

Als u een kenmerk in het dialoogvenster **[!UICONTROL Select union schema field]** wilt selecteren, navigeert u naar het kenmerk in het samenvoegingsschema (of gebruikt u de zoekopdracht) en schakelt u het selectievakje naast het kenmerk in. Als u het selectievakje inschakelt, wordt het kenmerk ook toegevoegd aan de lijst **[!UICONTROL Selected Attributes]** rechts in het dialoogvenster.

>[!NOTE]
>
>Een kenmerk kan alleen zichtbaar zijn voor selectie als het een van de volgende kenmerken is: Tekenreeks, datum, datum en tijd, Boolean, kort, lang, geheel getal of byte. De gegevenstypen Map en Double worden niet ondersteund en worden grijs weergegeven zodat ze niet kunnen worden geselecteerd.

Nadat u de kenmerken hebt gekozen die u wilt toevoegen, selecteert u **[!UICONTROL Save]** om uw kenmerken op te slaan en terug te keren naar het tabblad Aangepaste widgets.

>[!WARNING]
>Nieuw geselecteerde kenmerken worden beschikbaar na de volgende dagelijkse momentopname wanneer de gegevens worden vernieuwd.

![](../images/customization/select-attribute.png)

## Volgende stappen

Na het lezen van deze gids kunt u aan de widgetbibliotheek navigeren en de attributen van het Profiel van de Klant in real time selecteren om uw schema te vormen. Als Profielkenmerken zijn geselecteerd, kunt u [aangepaste widgets maken voor uw dashboards](custom-widgets.md).