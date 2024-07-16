---
keywords: Experience Platform;gebruikersinterface;UI;dashboards;dashboard;profielen;segmenten;bestemmingen;vergunningsgebruik
title: Schema bewerken om aangepaste dashboardwidgets te maken
description: Deze handleiding bevat stapsgewijze instructies voor het selecteren van kenmerken en het configureren van het schema van uw organisatie om aangepaste widgets voor Adobe Experience Platform-dashboards te maken.
exl-id: a744eb24-5ba7-4971-9183-3f891e807863
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Schema bewerken om aangepaste widgets te maken

Als u aangepaste widgets voor Adobe Experience Platform-dashboards wilt maken, moet u eerst de kenmerken van het realtime-klantprofiel identificeren waarop de widgets worden gebaseerd.

Deze handleiding bevat stapsgewijze instructies voor het bewerken van het schema van uw organisatie door kenmerken te selecteren om aangepaste dashboardwidgets te maken.

Zodra de attributen zijn geselecteerd en het schema is gevormd, kunt u met de stappen voor [ te werk gaan creërend douane widgets voor uw dashboards ](custom-widgets.md).

>[!NOTE]
>
>Gebruikers moeten de machtiging &quot;Standaarddashboards beheren&quot; hebben om het schema te kunnen bewerken. Voor stappen bij het verlenen van toegangstoestemmingen voor dashboards, gelieve te verwijzen naar de [ gids van de toestemmingen van het dashboard ](../permissions.md).

## Widget-bibliotheek {#widget-library}

Voor deze handleiding is toegang tot [!UICONTROL Widget library] in het Experience Platform vereist. Meer over de widgetbibliotheek leren, en hoe te om tot het binnen UI toegang te hebben, gelieve te beginnen door het [ overzicht van de widgetbibliotheek te lezen ](widget-library.md).

## Schema bewerken

In de widgetbibliotheek kunt u op het tabblad **[!UICONTROL Custom]** widgets maken en deze delen met andere gebruikers in uw organisatie om de weergave van uw dashboards aan te passen.

Voordat u aangepaste widgets kunt maken, moeten de kenmerken van het realtime-klantprofiel zijn geselecteerd om ervoor te zorgen dat de gegevens worden opgenomen als onderdeel van de dagelijkse momentopname.

>[!IMPORTANT]
>
>Uw organisatie kan maximaal 20 kenmerken selecteren.

Als uw organisatie geen profielkenmerken heeft geselecteerd, begint u met het selecteren van **[!UICONTROL Configure]** in het midden van het scherm.

![ het lusje van de Douane van de werkruimte van de widgetbibliotheek met vormen benadrukt.](../images/customization/configure-schema.png)

Wanneer ten minste één aangepast kenmerk is gemaakt, selecteert u **[!UICONTROL Edit schema]** om de geselecteerde kenmerken weer te geven en meer toe te voegen.

![ het lusje van de Douane van de widgetbibliotheekwerkruimte met Edit benadrukt schema.](../images/customization/edit-schema.png)

## Een kenmerk selecteren

Als u een kenmerk in het dialoogvenster **[!UICONTROL Select union schema field]** wilt selecteren, navigeert u naar het kenmerk in het samenvoegingsschema (of gebruikt u de zoekopdracht) en schakelt u het selectievakje naast het kenmerk in. Als u het selectievakje inschakelt, wordt het kenmerk ook toegevoegd aan de lijst **[!UICONTROL Selected Attributes]** aan de rechterkant van het dialoogvenster.

>[!NOTE]
>
>Een kenmerk is alleen zichtbaar voor selectie als het een van de volgende kenmerken is: String, Date, Date-Time, Boolean, Short, Long, Integer of Byte. De gegevenstypen Map en Double worden niet ondersteund en worden grijs weergegeven zodat ze niet kunnen worden geselecteerd.

Nadat u de kenmerken hebt gekozen die u wilt toevoegen, selecteert u **[!UICONTROL Save]** om uw kenmerken op te slaan en terug te keren naar het tabblad Aangepaste widgets.

>[!WARNING]
>Nieuw geselecteerde kenmerken worden beschikbaar na de volgende dagelijkse momentopname wanneer de gegevens worden vernieuwd.

![ de dialoog om schemakenmerken met benadrukte attributen te selecteren en te bewaren.](../images/customization/select-attribute.png)

## Volgende stappen

Na het lezen van deze gids kunt u aan de widgetbibliotheek navigeren en de attributen van het Profiel van de Klant selecteren in real time om uw schema te vormen. Met de geselecteerde attributen van het Profiel, kunt u [ beginnen creërend douanewidgets voor uw dashboards ](custom-widgets.md).
