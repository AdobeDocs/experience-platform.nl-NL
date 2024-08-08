---
keywords: Experience Platform;home;populaire onderwerpen;analyse;mixpanel
solution: Experience Platform
title: Een gegevensstroom maken met een Source Analytics in de gebruikersinterface
description: Deze zelfstudie bevat stappen voor het maken van een gegevensstroom voor een analysebron met behulp van de interface van het platform.
exl-id: 108a69e5-d7d9-4ca1-a364-38ea54aa74ff
source-git-commit: d048109141168b33795753c4706dac64cdf29ca5
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 0%

---

# Een gegevensstroom maken met een analysebron in de gebruikersinterface

Een dataflow is een geplande taak die gegevens van een bron aan een dataset in Adobe Experience Platform terugwint en opneemt. Deze zelfstudie bevat stappen voor het maken van een gegevensstroom voor een analysebron met behulp van de interface van het platform.

>[!NOTE]
>
>Als u een gegevensstroom wilt maken, moet u al over een geverifieerd account bij de [!DNL Mixpanel] -bron beschikken. Zie het leerprogramma op [ creërend a  [!DNL Mixpanel]  bronverbinding in UI ](../../ui/create/analytics/mixpanel.md) voor meer informatie.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende componenten van Platform:

* [ Bronnen ](../../../home.md): Het platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [[!DNL Data Prep]](../../../../data-prep/home.md): staat gegevensengineers toe om gegevens in kaart te brengen, om te zetten en te bevestigen aan en van het Model van de Gegevens van de Ervaring (XDM).

<!-- ## Add data

After creating your analytics source account, the **[!UICONTROL Add data]** step appears, providing an interface for you to explore your analytics account's table hierarchy.

* The left half of the interface is a browser, displaying a list of data tables contained in your account. The interface also includes a search option that allows you to quickly identify the source data you intend to use.
* The right half of the interface is a preview panel, allowing you to preview up to 100 rows of data.

>[!NOTE]
>
>The search source data option is available to all table-based sources excluding the Adobe Analytics, [!DNL Amazon Kinesis], and [!DNL Azure Event Hubs].

Once you find the source data, select the table, then select **[!UICONTROL Next]**.

![select-data](../../../images/tutorials/dataflow/table-based/select-data.png) -->

## Gegevens over gegevensstroom opgeven

Met de pagina [!UICONTROL Dataflow detail] kunt u selecteren of u een bestaande gegevensset of een nieuwe gegevensset wilt gebruiken. Tijdens dit proces kunt u ook instellingen configureren voor [!UICONTROL Profile dataset] , [!UICONTROL Error diagnostics] , [!UICONTROL Partial ingestion] en [!UICONTROL Alerts] .

![ dataflow-detail ](../../../images/tutorials/dataflow/table-based/dataflow-detail.png)

### Een bestaande gegevensset gebruiken

Selecteer **[!UICONTROL Existing dataset]** als u gegevens in een bestaande gegevensset wilt opnemen. U kunt of een bestaande dataset terugwinnen gebruikend de [!UICONTROL Advanced search] optie of door door de lijst van bestaande datasets in het dropdown menu te scrollen. Zodra u een dataset hebt geselecteerd, verstrek een naam en een beschrijving voor uw gegevensstroom.

![ bestaand-dataset ](../../../images/tutorials/dataflow/table-based/existing-dataset.png)

### Een nieuwe gegevensset gebruiken

Om in een nieuwe dataset in te gaan, selecteer **[!UICONTROL New dataset]** en verstrek dan een naam van de outputdataset en een facultatieve beschrijving. Selecteer vervolgens het schema dat u wilt toewijzen met de optie [!UICONTROL Advanced search] of door door de lijst met bestaande schema&#39;s in het vervolgkeuzemenu te bladeren. Nadat u een schema hebt geselecteerd, geeft u een naam en een beschrijving voor de gegevensstroom op.

![ nieuw-dataset ](../../../images/tutorials/dataflow/table-based/new-dataset.png)

### [!DNL Profile] en foutdiagnostiek inschakelen

Selecteer vervolgens de schakeloptie **[!UICONTROL Profile dataset]** om de gegevensset in te schakelen voor [!DNL Profile] . Hierdoor kunt u een holistische weergave maken van de kenmerken en het gedrag van een entiteit. Gegevens van alle gegevenssets waarvoor [!DNL Profile] is ingeschakeld, worden opgenomen in [!DNL Profile] en wijzigingen worden toegepast wanneer u de gegevensstroom opslaat.

In [!UICONTROL Error diagnostics] kunnen gedetailleerde foutberichten worden gegenereerd voor onjuiste records in de gegevensstroom, terwijl u in [!UICONTROL Partial ingestion] gegevens met fouten kunt invoeren tot een bepaalde drempel die u handmatig definieert. Zie het [ gedeeltelijke overzicht van partijingestie ](../../../../ingestion/batch-ingestion/partial.md) voor meer informatie.

![ profiel-en-fouten ](../../../images/tutorials/dataflow/table-based/profile-and-errors.png)

### Waarschuwingen inschakelen

U kunt waarschuwingen inschakelen om meldingen te ontvangen over de status van uw gegevensstroom. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bronalarm gebruikend UI ](../alerts.md).

Wanneer u klaar bent met het opgeven van details voor de gegevensstroom, selecteert u **[!UICONTROL Next]** .

![ alarm ](../../../images/tutorials/dataflow/table-based/alerts.png)

## Gegevensvelden toewijzen aan een XDM-schema

>[!IMPORTANT]
>
>U kunt geen dynamische sleutel-paar waarden als voorwerp van [!DNL OneTrust] aan Platform in kaart brengen en moet die sleutels in het doelschema specificeren om uw gegevens tijdens opname in kaart te brengen.

De stap [!UICONTROL Mapping] verschijnt, die u van een interface voorziet om de brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie de [ gids UI van de Prep van Gegevens ](../../../../data-prep/ui/mapping.md).

Selecteer **[!UICONTROL Next]** wanneer de brongegevens correct zijn toegewezen.

![ afbeelding ](../../../images/tutorials/dataflow/table-based/mapping.png)

## Planninguitvoering

De stap [!UICONTROL Scheduling] verschijnt, die u toestaat om een innameprogramma te vormen om de geselecteerde brongegevens automatisch in te nemen gebruikend de gevormde afbeeldingen. De planning wordt standaard ingesteld op `Once` . Als u de innamefrequentie wilt aanpassen, selecteert u **[!UICONTROL Frequency]** en vervolgens een optie in het vervolgkeuzemenu.

>[!TIP]
>
>Interval en backfill zijn niet zichtbaar tijdens een eenmalige opname.

![ het plannen ](../../../images/tutorials/dataflow/table-based/scheduling.png)

Als u de innamefrequentie instelt op `Minute` , `Hour` , `Day` of `Week` , moet u een interval instellen om een bepaald tijdkader tussen elke inname te maken. Als de innamefrequentie bijvoorbeeld is ingesteld op `Day` en als het interval is ingesteld op `15` , worden gegevens elke 15 dagen opgenomen.

Tijdens deze stap, kunt u **backfill** ook toelaten en een kolom voor de stijgende opname van gegevens bepalen. Backfill wordt gebruikt om historische gegevens in te voeren, terwijl in de kolom die u voor incrementele inname definieert, nieuwe gegevens kunnen worden onderscheiden van bestaande gegevens.

Zie de lijst hieronder voor meer informatie over het plannen van configuraties.

| Configuratie plannen | Beschrijving |
| --- | --- |
| Frequentie | Vorm frequentie om erop te wijzen hoe vaak dataflow zou moeten lopen. U kunt de frequentie instellen op: <ul><li>**Eenmaal**: Plaats uw frequentie aan `once` om eenmalig te creëren. Configuraties voor interval en backfill zijn niet beschikbaar wanneer u een eenmalige gegevensstroom maakt. Standaard wordt de planningsfrequentie ingesteld op één keer.</li><li>**Minuut**: Plaats uw frequentie aan `minute` om uw gegevensstroom te plannen om gegevens op een per-minieme basis in te voeren.</li><li>**Uur**: Plaats uw frequentie aan `hour` om uw gegevensstroom te plannen om gegevens op een per-uurbasis in te voeren.</li><li>**Dag**: Plaats uw frequentie aan `day` om uw gegevensstroom te plannen om gegevens op een per-dagbasis in te voeren.</li><li>**Week**: Plaats uw frequentie aan `week` om uw gegevensstroom te plannen om gegevens op een per-weekbasis in te voeren.</li></ul> |
| Interval | Zodra u een frequentie selecteert, kunt u het interval dat dan vormen om het tijdkader tussen elke opname te vestigen. Bijvoorbeeld, als u uw frequentie aan dag plaatst en het interval aan 15 vormt, dan zal uw dataflow om de 15 dagen lopen. U kunt het interval niet instellen op nul. De minimaal toegestane intervalwaarde voor elke frequentie is als volgt:<ul><li>**Eenmaal**: n/a</li><li>**Minuut**: 15</li><li>**Uur**: 1</li><li>**Dag**: 1</li><li>**Week**: 1</li></ul> |
| Begintijd | Het tijdstempel voor de geprojecteerde run, weergegeven in UTC-tijdzone. |
| Achtergrond | Met Backfill wordt bepaald welke gegevens in eerste instantie worden ingevoerd. Als backfill is ingeschakeld, worden alle huidige bestanden in het opgegeven pad tijdens de eerste geplande inname opgenomen. Als terugvullen is uitgeschakeld, worden alleen de bestanden opgenomen die tussen de eerste opname en de begintijd worden geladen. Bestanden die vóór de begintijd zijn geladen, worden niet opgenomen. |
| Incrementele gegevens laden met | Een optie met een gefilterde reeks gebieden van het bronschema van type, datum, of tijd. Het veld waarvoor u **[!UICONTROL Load incremental data by]** selecteert, moet zijn datum-tijdwaarden in UTC-tijdzone hebben om de incrementele gegevens correct te laden. Alle op lijst-gebaseerde partijbronnen kiezen stijgende gegevens door een waarde van de de tijdstempeltijd van de deltakolom met de overeenkomstige tijd van het venster UTC van de stroomlooppas te vergelijken, en dan het kopiëren van de gegevens van de bron, als om het even welke nieuwe gegevens binnen het tijdvenster UTC wordt gevonden. |

![ backfill ](../../../images/tutorials/dataflow/table-based/backfill.png)

## Controleer uw gegevensstroom

De stap **[!UICONTROL Review]** wordt weergegeven, zodat u de nieuwe gegevensstroom kunt bekijken voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: geeft het brontype, het relevante pad van het gekozen bronbestand en de hoeveelheid kolommen in dat bronbestand weer.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt aan.
* **[!UICONTROL Scheduling]**: geeft de actieve periode, frequentie en interval van het innameschema weer.

Nadat u de gegevensstroom hebt gereviseerd, selecteert u **[!UICONTROL Finish]** en laat u enige tijd over om de gegevensstroom te maken.

![ overzicht ](../../../images/tutorials/dataflow/table-based/review.png)

## Uw gegevensstroom controleren

Zodra uw gegevensstroom is gecreeerd, kunt u de gegevens controleren die door het worden opgenomen om informatie over innamepercentages, succes, en fouten te zien. Voor meer informatie over hoe te om dataflow te controleren, zie het leerprogramma op [ controlerekeningen en dataflows in UI ](../monitor.md).

## Uw gegevensstroom verwijderen

U kunt gegevensstromen verwijderen die niet meer nodig zijn of die onjuist zijn gemaakt met de functie **[!UICONTROL Delete]** die beschikbaar is in de **[!UICONTROL Dataflows]** -werkruimte. Voor meer informatie over hoe te om dataflows te schrappen, zie het leerprogramma bij [ het schrappen van dataflows in UI ](../delete.md).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een gegevensstroom gemaakt om gegevens van uw analysebron naar Platform te brengen. Binnenkomende gegevens kunnen nu worden gebruikt door [!DNL Platform] -services, zoals [!DNL Real-Time Customer Profile] en [!DNL Data Science Workspace] . Raadpleeg de volgende documenten voor meer informatie:

* [[!DNL Real-Time Customer Profile]-overzicht](../../../../profile/home.md)
* [[!DNL Data Science Workspace]-overzicht](../../../../data-science-workspace/home.md)


>[!WARNING]
>
> De interface van het Platform die in de volgende video wordt getoond is verouderd. Raadpleeg de bovenstaande documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)
