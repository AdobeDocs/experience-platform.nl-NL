---
title: Een datumfilter maken
description: Leer hoe u uw eigen inzichten op datum kunt filteren.
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# Een datumfilter maken {#create-date-filter}

Om uw inzichten door datum te filtreren, moet u parameters aan uw SQL vragen toevoegen die datumbeperkingen kunnen goedkeuren. Dit wordt gedaan als deel van het bevel van de vraag pro wijze inzicht creatiewerkschema. Zie de [query pro mode documentatie](#query-pro-mode) om te leren hoe u SQL voor uw inzichten ingaat.

Met queryparameters kunt u werken met dynamische gegevens zoals deze fungeren als plaatsaanduidingen voor de waarden die u toevoegt tijdens de uitvoering. Deze plaatsaanduidingswaarden kunnen worden bijgewerkt via de gebruikersinterface en stellen minder technische gebruikers in staat de inzichten bij te werken die op datumbereiken zijn gebaseerd.

Als u niet vertrouwd met vraagparameters bent, zie de documentatie voor [begeleiding op hoe te om geparametereerde vragen uit te voeren](../../../../query-service/ui/parameterized-queries.md).

## Een datumfilter toepassen op het dashboard {#apply-date-filter}

Als u een datumfilter wilt toepassen, selecteert u **[!UICONTROL Add filter]** vervolgens **[!UICONTROL Date Filter]** in het vervolgkeuzemenu van de dashboardweergave.

![Een aangepast dashboard met het filter Toevoegen en het vervolgkeuzemenu gemarkeerd.](../../../images/customizable-insights/add-filter.png)

## SQL bewerken om parameters voor datumquery op te nemen {#include-date-parameters}

Zorg er daarna voor dat uw SQL queryparameters bevat die een datumbereik toestaan. Als u query-parameters nog niet hebt opgenomen in uw SQL, bewerkt u de inzichten om deze parameters op te nemen. Zie de documentatie voor instructies over hoe u kunt [een inzicht bewerken](../query-pro-mode.md#edit).

>[!TIP]
>
>U wordt aangeraden om toe te voegen `$START_DATE` en `$END_DATE` parameters aan uw SQL verklaring in elk van de grafieken die u datumfilters voor wilt toelaten.

>[!NOTE]
>
>Datumfilters bieden geen ondersteuning voor tijdbeperkingen. Het filter is alleen van toepassing op datumbereiken. Dit betekent dat als u meerdere rapporten binnen een periode van 24 uur hebt, u geen onderscheid kunt maken tussen verschillende uren binnen dezelfde dag. Om deze reden, wordt u geadviseerd om de tijdcomponent als datum te werpen.

Als het gegevensmodel of de lijsten u analyseert een tijdcomponent hebben, kunt u uw gegevens groeperen door datum en dan deze datumfilters toepassen.

De voorbeeld-SQL-instructie hieronder laat zien hoe u deze invoegt `$START_DATE` en `$END_DATE` parameters en gebruik `cast` om de tijdcomponent als een datum te plaatsen.

```sql
SELECT Sum(personalization_consent_count) AS Personalization,
       Sum(datacollection_consent_count)  AS Datacollection,
       Sum(datasharing_consent_count)     AS Datasharing
FROM   fact_daily_consent_aggregates f
       INNER JOIN dim_consent_valued
               ON f.consent_value_id = d.consent_value_id
WHERE  f.date BETWEEN Upper(Coalesce(Cast('$START_DATE' AS date), '')) AND Upper
                      (
                             Coalesce(Cast('$END_DATE' AS date), ''))
       AND ( ( Upper(Coalesce($consent_value_filter, '')) IN ( '', 'NULL' ) )
              OR ( f.consent_value_id IN ( $consent_value_filter ) ) )
LIMIT  0; 
```

In de onderstaande schermafbeelding worden de datumbeperkingen gemarkeerd die zijn opgenomen in de SQL-instructie en de sleutelwaardeparen van de queryparameter.

>[!NOTE]
>
>Wanneer het samenstellen van uw verklaring op vraag pro wijze, moet u steekproefwaarden voor elke parameter verstrekken om de SQL verklaring uit te voeren en de grafiek te bouwen. De samplewaarden die u opgeeft wanneer u de instructie samenstelt, worden vervangen door de werkelijke waarden die u selecteert voor het datumfilter (of algemene filter) bij uitvoering.

![De [!UICONTROL Enter SQL] met de datumparameters die in de SQL worden gemarkeerd.](../../../images/customizable-insights/sql-date-parameters.png)

## Datumparameters inschakelen in elk inzicht {#enable-date-parameters}

Als u de juiste parameters hebt opgenomen in de SQL van uw inzichten, `Start_date` en `End_date` variabelen zijn nu beschikbaar als een schakeloptie in de widgetcomposer. Zie de [sectie over populatie van widget query voor modus](#populate-widget) voor informatie over het bewerken van een inzicht.

Selecteer in de widgetcomposer de optie Schakelen om het `Start_date` en `End_date` parameters.

![De widgetcomposer met de toggles Start_date en End_date gemarkeerd.](../../../images/customizable-insights/widget-composer-date-filter-toggles.png)

Selecteer vervolgens de juiste queryparameters in de vervolgkeuzemenu&#39;s.

![De widgetcomposer met het drop-down menu Start_date gemarkeerd.](../../../images/customizable-insights/widget-composer-date-filter-dropdown.png)

Tot slot selecteert u **[!UICONTROL Save and close]** om terug te keren naar het dashboard. Datumfilters zijn nu ingeschakeld voor alle inzichten met begin- en einddatumparameters.

## Het datumfilter gebruiken

Als u een aangepast datumfilter wilt gebruiken, selecteert u het kalenderpictogram en kiest u een begin- en einddatum in de kalender-weergave.

>[!IMPORTANT]
>
>Als u gewoon een datumfilter toevoegt, worden de diagrammen niet gewijzigd. U moet elk van uw inzichten uitgeven om uw gekozen begin en einddatum te omvatten.

![Een aangepast dashboard waarvan de aanroeper van het datumfilter is gemarkeerd.](../../../images/customizable-insights/date-filter.png)

Zodra u een datumbereik van het dashboard hebt geselecteerd, worden de datumfilteropties in de widgetcomposer weergegeven voor inzichten die datumparameters in hun SQL hebben.

>[!NOTE]
>
>Als u een datumbereik op het dashboard selecteert, worden de schakelopties voor datumfilters weergegeven als onderdeel van de workflow voor het maken van inzichten.

## Een datumfilter verwijderen {#delete-date-filter}

Als u het datumfilter wilt verwijderen, selecteert u het pictogram van het verwijderfilter (![Het verwijderfilterpictogram.](../../../images/customizable-insights/delete-filter-icon.png)).

![Een aangepast dashboard met het pictogram voor het verwijderen van filters gemarkeerd.](../../../images/customizable-insights/delete-date-filter.png)
