---
title: Identiteitsoverlappingen van doelgroepen
description: Leer hoe u overlap van doelgroepidentiteiten kunt analyseren met het dashboard Doelgroepsidentiteiten overlapt. Filter doelgroepen, geef beleid voor samenvoegen op en controleer identiteitsrelaties om datagestuurde beslissingen te nemen.
source-git-commit: 90d5f00648a80d735b92c3bdc540f1ad18ff38f5
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---

# Overlap van doelgroepidentiteit

Analyseer identiteitsoverlap voor geselecteerde doelgroepen met het [!UICONTROL Audience Identity Overlaps] -dashboard. U kunt inzichten in gebruiken hoe de verschillende identiteiten binnen een publiek op elkaar betrekking hebben om het stitching strategieën te optimaliseren, overtolligheid te verminderen, en klantensegmenteringsnauwkeurigheid te verbeteren. Ontwikkel effectieve targetingstrategieën en stroomlijn de klantinteracties met een beter inzicht in de overlapping tussen identiteitstypen.

## Doelgroepen filteren {#filter-audiences}

Gebruik aangepaste filters voor gerichte analyse van specifieke doelgroepen en identiteitstypen om ervoor te zorgen dat de gepresenteerde gegevens worden afgestemd op je analysedoelen. Om uw analyse te beginnen, selecteer het filterpictogram (![ het filterpictogram.](../../../images/icons/filter-icon-white.png)).

![ het Verlaten dashboard van de Identiteit van het publiek met het benadrukte filterpictogram.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-filter-icon.png)

Het dialoogvenster **[!UICONTROL Filters]** wordt weergegeven. In deze weergave kiest u de algemene filters om uw doelgroep te configureren, het samenvoegbeleid te bepalen en de identiteiten voor de vergelijking vast te stellen. Selecteer uw instellingen voor analyse in het vervolgkeuzemenu van elke sectie

1. Selecteer een **[!UICONTROL Audience]**: Kies het doelgroepsegment u (bijvoorbeeld, **Canada - Alberta**) wilt analyseren.
2. Specificeer a **[!UICONTROL Merge Policy]**: Bepaal het fusiebeleid dat dicteert hoe de identiteiten over het geselecteerde publiek worden gecombineerd (in het voorbeeldscreenshot, wordt het **Gebaseerde op tijd gebaseerde** beleid geselecteerd).
3. Selecteer een **[!UICONTROL Identity A]** en **[!UICONTROL  Identity B]** ter vergelijking**: kies de twee identiteitstypen die u wilt vergelijken. In het voorbeeld, **Identiteit A** wordt geselecteerd als &quot;crmId&quot; en **Identiteit B** wordt geselecteerd als &quot;e-mail.&quot;
4. **plaats een datumwaaier**: Kies een vooraf bepaalde waaier zoals &quot;vandaag&quot;of plaats manueel de begin en einddata gebruikend de kalendergebieden.

![ de dialoog van Filters op het Dashboard van de Identiteit van het Publiek.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-filters-dialog.png)

>[!TIP]
>
>Als u al uw aangepaste globale filters wilt wissen, selecteert u **[!UICONTROL Clear all]** in het dialoogvenster [!UICONTROL Filters] . Om één enkel filter te verwijderen, selecteer &quot;[!UICONTROL X]&quot;rechts van de filternaam.

Nadat u de filters hebt gekozen, selecteert u **[!UICONTROL Apply]** om het dashboard te vernieuwen.

![ de dialoog van Filters op het Dashboard van de Identiteit van het publiek met Toepassen benadrukte.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-apply-filters.png)

## Beschikbare dashboardinzichten {#available-insights}

Het **dashboard van de Identiteit van de Audience van het publiek overlapt** verstrekt verscheidene visualisaties en gegevens in tabelvorm om u te helpen identiteitsoverlappingen en trends binnen uw publiek begrijpen.

### Identiteitsoverlappingen van doelgroepen {#overlaps-table}

In de tabel **[!UICONTROL Audience Identity Overlaps]** worden op basis van uw geselecteerde filters overlappingen met de identiteit weergegeven. Gebruik deze informatie om de overlapping tussen verschillende identiteitstypen te beoordelen en te begrijpen hoe effectief identiteiten worden opgelost. In de onderstaande tabel wordt elke kolom uitgebreid uitgelegd:

| Kolomnaam | Beschrijving |
|-----------------|-------------------------------|
| **[!UICONTROL Audience Name]** | De naam van het publiek dat wordt geanalyseerd. Deze kolom identificeert welk doelgroepsegment wordt geëvalueerd om ervoor te zorgen dat de inzichten op de voorgenomen doelgroep worden gericht. |
| **[!UICONTROL Identity A]** en **[!UICONTROL Identity B]** | De identiteiten die worden vergeleken (bijvoorbeeld `crmId` en `email` ). Als u weet welke identiteitstypen worden vergeleken, kunt u beter bepalen welke identiteitsresolutiestrategieën bijdragen tot het overlappen van de doelgroep en kunt u deze relaties optimaliseren. |
| **[!UICONTROL Overlap Count]** | Het aantal profielen waarbij beide identiteiten aanwezig zijn. Deze metric geeft inzicht in de mate van identiteitsoverlapping binnen het publiek. Deze informatie is van cruciaal belang om te beoordelen hoe effectief meerdere identiteiten worden opgelost in uniforme profielen, die op hun beurt de strategieën voor doelgerichtheid en personalisatie kunnen verbeteren. |
| **[!UICONTROL Identity A Count]** | Het totale aantal profielen in het geselecteerde publiek dat **Identiteit A** bevat. Gebruik deze informatie om de prevalentie van het primaire identiteitstype binnen het publiek te begrijpen en de rol ervan in de overlappende analyse te beoordelen. |

![ de Lijst van de Overlap van de Identiteit van het publiek op de identiteit van het Publiek overlapt dashboard.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-chart.png)

### Naamuitsplitsing {#identity-breakdown}

Het **[!UICONTROL Identity Breakdown]** -diagram toont de relatieve samenstelling van identiteiten binnen het geselecteerde publiek. De X-as geeft het totale aantal identiteiten in het geselecteerde publiek aan, terwijl de Y-as de doelgroepnaam vertegenwoordigt die wordt geanalyseerd. Gebruik deze visualisatie om de prevalentie van elk identiteitstype te begrijpen en de impact van uw strategie voor identiteitsbeheer te evalueren. Het diagram maakt onderscheid tussen identiteitstypen met behulp van verschillende kleuren, zodat u snel kunt zien hoe identiteiten over uw publiek worden verdeeld.

>[!TIP]
>
>Houd de muisaanwijzer boven de kolommen om de afzonderlijke aantallen profielen voor elk identiteitstype weer te geven.

![ de grafiek van de Onderverdeling van de Identiteit.](../../images/sql-insights-query-pro-mode/templates/identity-breakdown-chart.png)

### Trends in de identiteit van het publiek {#audience-identity-trends}

Het **[!UICONTROL Audience Identity Trends]** -diagram geeft inzicht in hoe het totale aantal identiteiten in de loop der tijd is gewijzigd. De X-as vertegenwoordigt het datumbereik dat wordt geanalyseerd, terwijl de Y-as het totale aantal identiteiten per publiek vertegenwoordigt. Gebruik deze maatstaf om de identiteitsgroei te volgen, de stabiliteit te beoordelen en de effectiviteit van de lopende identiteitsbeheerinspanningen te meten.

>[!TIP]
>
>Houd de muis boven een datum in het diagram om het totale aantal identiteiten voor het publiek op een specifieke datum weer te geven.

![ de grafiek van de Trends van de Identiteit van het publiek.](../../images/sql-insights-query-pro-mode/templates/audience-identity-trends-chart.png)

## Inzichten exporteren {#export-insights}

Na het analyseren van identiteitsoverlappingen, kunt u de gegevens voor off-line analyse of rapportering uitvoeren. Als u uw gegevens wilt exporteren, selecteert u **[!UICONTROL Export]** rechtsboven in de tabel. Het dialoogvenster PDF wordt weergegeven, zodat u de visualiseerde gegevens kunt opslaan als een PDF of kunt afdrukken.

![ het Overlappende dashboard van de Identiteit van het publiek met de Uitvoer benadrukte.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-export.png)

Het **dashboard van de Identiteit van het publiek 0} {overlapt essentiële inzichten in hoe de verschillende identiteiten over uw geselecteerde publiek snijden.** Door gebruik te maken van deze inzichten, kun je identiteitsverstikkende strategieën verfijnen, redundantie verminderen en ervoor zorgen dat je doelgroepsegmentatie nauwkeuriger en effectiever is.

## Volgende stappen

Na het lezen van dit document, hebt u geleerd hoe te om waardevolle inzichten in identiteitsoverlap voor geselecteerde doelgroepen te verkrijgen gebruikend het **dashboard van de Identiteit van het publiek 0} {.** Om je inzicht in doelgroepsegmentatie en identiteitbeheer verder te verbeteren, verken je andere Data Distiller Templates die uitgebreide inzichten bieden. Verwijs naar de [ Trends van het Publiek ](./trends.md), [ Vergelijking van het Publiek ](./comparison.md), en [ Geavanceerde gidsen van de Overlapping van het Publiek ](./overlaps.md) UI om uw het richten en betrokkenheidsstrategieën verder te verbeteren.

