---
title: Een globaal filter maken
description: Leer hoe u uw gegevensinzichten kunt filteren met een aangepast, globaal toegepast filter.
source-git-commit: b95616263d5a6dd26f7fce61d5d0b33c2d470c46
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# Een algemeen filter maken {#create-global-filter}

Als u een algemeen filter wilt maken, selecteert u eerst **[!UICONTROL Add filter]** vanuit uw dashboardweergave, en vervolgens **[!UICONTROL Global filter]** in het vervolgkeuzemenu.

>[!IMPORTANT]
>
>Zorg ervoor dat u de algemene filters toewijst aan al uw diagrammen. Dit is geen automatisch proces. Als u een algemeen filter wilt gebruiken, moet u een [queryparameter](../../../../query-service/ui/parameterized-queries.md) in de SQL van uw grafiek, [het globale filter inschakelen](#enable-global-filter) in de widgetcomposer, en [een runtimewaarde selecteren](#select-global-filter) voor de parameter in het globale filterdialoogvenster. Zie de vraag pro gids om te leren hoe te om uw SQL uit te geven als u een vraagparameter moet opnemen.

![Een aangepast dashboard met het filter Toevoegen en het vervolgkeuzemenu gemarkeerd.](../../../images/customizable-insights/add-filter.png)

U kunt de inzichten die door uw SQL met aangepaste globale filters worden verstrekt snel veranderen.

De [!UICONTROL Create a global filter] wordt geopend. Het maken van een algemeen filter volgt hetzelfde proces als het maken van inzicht in SQL. Selecteer eerst een database (inzichten-gegevensmodel) waarop u een query wilt uitvoeren, voer vervolgens uw aangepaste SQL in de Query Editor in en selecteer ten slotte het runpictogram (![Een runpictogram.](../../../images/customizable-insights/run-icon.png)).

>[!IMPORTANT]
>
>Wanneer u een algemeen filter maakt, moet u een id en een waarde opnemen. Met de voorbeeldwaarden kunt u de SQL-instructie uitvoeren en het diagram samenstellen. De voorbeeldwaarden die u opgeeft bij het samenstellen van de instructie, worden vervangen door de werkelijke waarden die u tijdens runtime voor de datum of het algemene filter selecteert.

Nadat de query is uitgevoerd, worden de resultaten weergegeven op het tabblad Resultaten. Selecteer **[!UICONTROL Next]**.

![De [!UICONTROL Create a global filter dialog] met het gegevenssetdropdown menu, het looppaspictogram en Volgende benadrukte.](../../../images/customizable-insights/global-filter.png)

In de laatste stap van de algemene workflow voor het maken van filters moet u een label voor het filter toevoegen. Een label toevoegen aan de **[!UICONTROL Filter label]** tekstveld en selecteer een filtertype in het vervolgkeuzemenu.

>[!NOTE]
>
>Alleen de [!UICONTROL Combo box] filtertypeoptie wordt momenteel ondersteund.

Tot slot selecteert u **[!UICONTROL Select]** om terug te keren naar de dashboardweergave.

![De [!UICONTROL Create a global filter dialog] met Selecteren en de tekstinvoer van het label Filter gemarkeerd.](../../../images/customizable-insights/global-filter-label.png)

## Globaal filter inschakelen voor elk inzicht {#enable-global-filter}

>[!TIP]
>
>Schakel de algemene filters in elk diagram dat u maakt in. Op deze manier weet u zeker dat de waarden die u kiest als algemeen filter, in al uw grafieken worden weerspiegeld.

Nadat u het algemene filter voor het dashboard hebt gemaakt, wordt de schakeloptie voor dat algemene filter beschikbaar als onderdeel van de widgetcomposer.

![De widgetcomposer met de globale filterknevel benadrukt.](../../../images/customizable-insights/global-filter-consent.png)

>[!IMPORTANT]
>
>Zorg ervoor dat de algemene filterparameter is opgenomen in de SQL van elk inzicht.

## Een algemeen filter selecteren {#select-global-filter}

Als u het dialoogvenster [!UICONTROL Filters] een lijst met al uw aangepaste filters en selecteer het filterpictogram (![Een filterpictogram.](../../../images/customizable-insights/filter.png)) links op het dashboard. Als u vervolgens de effecten op uw dashboardinzichten wilt toepassen, kiest u een optie in het vervolgkeuzemenu van het algemene filter en selecteert u **[!UICONTROL Apply]**.

![Een aangepast dashboard met het filterdialoogvenster gemarkeerd.](../../../images/customizable-insights/custom-filters.png)
