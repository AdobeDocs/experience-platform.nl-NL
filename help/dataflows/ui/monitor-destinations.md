---
keywords: Experience Platform;thuis;populaire onderwerpen;monitorrekeningen;monitordataflows;dataflows;bestemmingen
description: Met doelen kunt u uw gegevens activeren van Adobe Experience Platform naar talloze externe partners. Dit leerprogramma verstrekt instructies op hoe u dataflows voor uw bestemmingen kunt controleren gebruikend het gebruikersinterface van het Experience Platform.
solution: Experience Platform
title: Gegevensstromen van de monitor voor Doelen in UI
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 029e990f5b30713ceea5da80ace8002368ac5652
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 0%

---

# Dataflows voor doelen in de UI controleren

Met doelen kunt u uw gegevens activeren van Adobe Experience Platform naar talloze externe partners. Platform maakt het proces om de stroom van gegevens aan uw bestemmingen gemakkelijker te volgen door transparantie van gegevensstromen te verstrekken.

Het controledashboard voorziet u van een visuele vertegenwoordiging van de reis van een gegevensstroom, met inbegrip van de bestemming de gegevens worden geactiveerd aan. Dit leerprogramma verstrekt instructies op hoe u of dataflows direct in de bestemmingswerkruimte kunt controleren of het controledashboard gebruiken om dataflows voor uw bestemmingen te controleren gebruikend het gebruikersinterface van het Experience Platform.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [Gegevensstroom](../home.md): Dataflows zijn een voorstelling van gegevenstaken die gegevens over het Platform verplaatsen. Dataflows worden geconfigureerd op verschillende services, waardoor gegevens van bronconnectors naar doelgegevenssets, naar [!DNL Identity] en [!DNL Profile] en naar [!DNL Destinations] worden verplaatst.
   - [Dataflow wordt uitgevoerd](../../sources/notifications.md): De looppas van Dataflow is de terugkomende geplande banen die op de frequentieconfiguratie van geselecteerde dataflows worden gebaseerd.
- [Doelen](../../destinations/home.md): Doelen zijn voorgebouwde integraties met veelgebruikte toepassingen die het mogelijk maken om gegevens van Platform naadloos te activeren voor kanaalmarketingcampagnes, e-mailcampagnes, gerichte reclame en vele andere gebruiksgevallen.
- [Sandboxen](../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Gegevens controleren in de werkruimte Doelen

Navigeer in de **[!UICONTROL Destinations]** werkruimte in de interface van het Platform naar het tabblad **[!UICONTROL Browse]** en selecteer de naam van een doel dat u wilt weergeven.

![](../assets/ui/monitor-destinations/select-destination.png)

Er wordt een lijst met bestaande gegevensstromen weergegeven. Op deze pagina vindt u een lijst met zichtbare gegevensstromen, waaronder informatie over het doel, de gebruikersnaam, het aantal gegevensstromen en de status.

Zie de volgende tabel voor meer informatie over statussen:

| Status | Beschrijving |
| ------ | ----------- |
| Ingeschakeld | De status `Enabled` wijst erop dat een dataflow actief is en gegevens volgens het programma opneemt het werd verstrekt. |
| Uitgeschakeld | De status `Disabled` geeft aan dat een gegevensstroom inactief is en geen gegevens opneemt. |
| Verwerking | De status `Processing` geeft aan dat een gegevensstroom nog niet actief is. Deze status wordt vaak direct na het maken van een nieuwe gegevensstroom aangetroffen. |
| Fout | De status `Error` geeft aan dat het activeringsproces van een gegevensstroom is onderbroken. |

### Dataflow wordt uitgevoerd voor streamingdoelen

Voor het stromen bestemmingen, verstrekt het [!UICONTROL Dataflow runs] lusje een uurupdate voor metrische gegevens over uw dataflow looppas. De meest prominente statistieken met het label zijn voor identiteiten.

De identiteiten vertegenwoordigen de verschillende facetten van een profiel. Als een profiel bijvoorbeeld zowel een telefoonnummer als een e-mailadres bevat, heeft dat profiel twee identiteiten.

Er wordt een lijst met afzonderlijke reeksen en de bijbehorende maatstaven weergegeven, samen met de volgende totalen voor identiteiten:

- **[!UICONTROL Identities activated]**: The total count of profile identities that were created or updated for activation.
- **[!UICONTROL Identities excluded]**: Het totale aantal profielidentiteiten dat voor activering wordt overgeslagen op basis van ontbrekende kenmerken en schending van de toestemming.
- **[!UICONTROL Identities failed]**: Het totale aantal profielidentiteiten dat niet aan de bestemming wegens fouten wordt geactiveerd.

![](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Elke individuele dataflow run toont de volgende details:

- **[!UICONTROL Dataflow run start]**: De tijd dat dataflow begon bij.
- **[!UICONTROL Processing time]**: De hoeveelheid tijd die het voor dataflow aan proces nam.
- **[!UICONTROL Profiles received]**: Het totale aantal profielen dat is ontvangen in de gegevensstroom.
- **[!UICONTROL Identities activated]**: Het totale aantal profielidentiteiten dat met succes aan de geselecteerde bestemming werd geactiveerd.
- **[!UICONTROL Identities excluded]**: Het totale aantal profiel-id&#39;s dat is uitgesloten voor activering op basis van ontbrekende kenmerken en schending van de toestemming.
- **[!UICONTROL Identities failed]** Het totale aantal profielidentiteiten dat niet aan de bestemming wegens fouten wordt geactiveerd.
- **[!UICONTROL Activation rate]**: Het percentage ontvangen identiteiten dat is geactiveerd of overgeslagen. De volgende formule laat zien hoe deze waarde wordt berekend:
   ![](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Status]**: Vertegenwoordigt de staat de dataflow is in: of  [!UICONTROL Completed] of  [!UICONTROL Processing]. [!UICONTROL Completed] betekent dat alle identiteiten voor de overeenkomstige dataflow run binnen de periode van één uur werden opgenomen. [!UICONTROL Processing] betekent dat de dataflow run nog niet is voltooid.

Om de details van een bepaalde dataflow looppas te bekijken, selecteer de begintijd van de looppas van de lijst.

De detailpagina voor een dataflow-run bevat aanvullende informatie zoals het aantal ontvangen profielen, het aantal geactiveerde identiteiten, het aantal mislukte identiteiten en het aantal uitgesloten identiteiten.

![](../assets/ui/monitor-destinations/dataflow-details-stream.png)

Op de detailpagina wordt ook een lijst met mislukte identiteiten en identiteiten weergegeven die zijn uitgesloten. De informatie voor zowel de mislukte als uitgesloten identiteiten wordt getoond, met inbegrip van de foutencode, het aantal van de identiteit, en beschrijving. Standaard worden in de lijst de mislukte identiteiten weergegeven. Als u overgeslagen identiteiten wilt weergeven, selecteert u de schakeloptie **[!UICONTROL Identities excluded]**.

![](../assets/ui/monitor-destinations/dataflow-records-stream.png)

### Dataflow wordt uitgevoerd voor batchdoelen

Voor batchbestemmingen, verstrekt het [!UICONTROL Dataflow runs] lusje metrische gegevens over uw dataflow looppas. Er wordt een lijst met afzonderlijke reeksen en de bijbehorende maatstaven weergegeven, samen met de volgende totalen voor identiteiten:

- **[!UICONTROL Identities activated]**: Het aantal afzonderlijke profiel-id&#39;s dat is geactiveerd voor het geselecteerde doel.
- **[!UICONTROL Identities excluded]**: Het aantal individuele profielidentiteiten die zijn uitgesloten voor activering voor de geselecteerde bestemming, op basis van ontbrekende kenmerken en schending van de toestemming.

![](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Elke individuele dataflow run toont de volgende details:

- **[!UICONTROL Dataflow run start]**: De tijd dat dataflow begon bij.
- **[!UICONTROL Processing time]**: De hoeveelheid tijd het voor dataflow nam om te worden verwerkt.
- **[!UICONTROL Profiles received]**: Het totale aantal profielen dat is ontvangen in de gegevensstroom. Deze waarde wordt elke 60 minuten bijgewerkt.
- **[!UICONTROL Identities activated]**: Het totale aantal profielidentiteiten dat met succes aan de geselecteerde bestemming werd geactiveerd.
- **[!UICONTROL Identities excluded]**: Het totale aantal profiel-id&#39;s dat is uitgesloten voor activering op basis van ontbrekende kenmerken en schending van de toestemming.
- **[!UICONTROL Status]**: Geeft de status aan waarin de gegevensstroom zich bevindt. Dit kan een van drie staten zijn: [!UICONTROL Success], [!UICONTROL Failed] en [!UICONTROL Processing]. [!UICONTROL Success] betekent dat de gegevensstroom actief is en gegevens volgens zijn verstrekt programma opneemt. [!UICONTROL Failed] betekent dat de activering van gegevens is opgeschort als gevolg van fouten. [!UICONTROL Processing] betekent dat de gegevensstroom nog niet actief is en over het algemeen wordt ontmoet wanneer een nieuwe gegevensstroom wordt gecreeerd.

Om details van een specifieke dataflow looppas te bekijken, selecteer de begintijd van de looppas van de lijst.

>[!NOTE]
>
>De looppas van Dataflow wordt geproduceerd gebaseerd op de planningsfrequentie van bestemmingsdataflow. Een afzonderlijke dataflow looppas wordt gemaakt voor elk samenvoegbeleid dat op een segment wordt toegepast.

De detailspagina voor een dataflow, naast de details die op de dataflows lijst worden getoond, toont specifiekere informatie over dataflow:

- **[!UICONTROL Size of data]**: De grootte van de gegevensstroom die wordt opgenomen.
- **[!UICONTROL Total files]**: Het totale aantal bestanden dat in de gegevensstroom wordt opgenomen.
- **[!UICONTROL Last updated]**: De tijd de dataflow looppas werd laatst bijgewerkt.

![](../assets/ui/monitor-destinations/dataflow-batch.png)

Op de detailpagina wordt ook een lijst met mislukte identiteiten en identiteiten weergegeven die zijn uitgesloten. Er wordt informatie voor zowel de mislukte als de uitgesloten identiteiten weergegeven, inclusief de foutcode en beschrijving. Standaard worden in de lijst de mislukte identiteiten weergegeven. Als u uitgesloten identiteiten wilt weergeven, selecteert u de schakeloptie **[!UICONTROL Identities excluded]**.

![](../assets/ui/monitor-destinations/dataflow-records-batch.png)

## Het dashboard Bestemmingen controleren

Als u het [!UICONTROL Monitoring]-dashboard wilt openen, selecteert u **[!UICONTROL Monitoring]** (![bewakingspictogram](../assets/ui/monitor-destinations/monitoring-icon.png)
) in de linkernavigatie. Selecteer [!UICONTROL Destinations] eenmaal op de pagina [!UICONTROL Monitoring]. Het dashboard [!UICONTROL Monitoring] bevat metriek en informatie over de banen van de bestemmingslooppas.

In het midden van het dashboard bevindt zich het deelvenster Activering, dat maatstaven en grafieken bevat die gegevens weergeven over de activeringsfrequentie van de gegevens die naar doelen worden geëxporteerd.

![](../assets/ui/monitor-destinations/dashboard-graph.png)


Standaard bevatten de weergegeven gegevens de activeringssnelheden van de laatste 24 uur. Selecteer **[!UICONTROL Last 24 hours]** om het tijdkader van getoonde verslagen aan te passen. Beschikbare opties zijn **[!UICONTROL Last 24 hours]**, **[!UICONTROL Last 7 days]** en **[!UICONTROL Last 30 days]**. U kunt ook de datums in het pop-upvenster Kalender selecteren dat wordt weergegeven. Als u datums hebt geselecteerd, selecteert u **[!UICONTROL Apply]** om het tijdkader van de weergegeven informatie aan te passen.

>[!NOTE]
>
>De volgende schermafbeelding toont de activeringsfrequentie voor de laatste 30 dagen in plaats van de laatste 24 uur. U kunt het tijdkader aanpassen door **[!UICONTROL Last 30 days]** te selecteren.

![](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

De grafiek wordt standaard weergegeven en u kunt deze uitschakelen om de onderstaande lijst met doelen uit te vouwen. Selecteer **[!UICONTROL Metrics and graphs]** knevel om de grafieken onbruikbaar te maken.

In het deelvenster **[!UICONTROL Activation]** wordt een lijst weergegeven met doelen die ten minste één bestaande account bevatten. Deze lijst bevat ook informatie over de ontvangen profielen, profielrecords die zijn geactiveerd, profielrecords die zijn mislukt, profielrecords die zijn overgeslagen, totaal mislukte gegevensstromen en de datum die voor deze doelen het laatst is bijgewerkt.

![](../assets/ui/monitor-destinations/dashboard-destinations.png)

U kunt uw lijst van bestemmingen ook filtreren om slechts de geselecteerde categorie van bestemmingen te tonen. Selecteer **[!UICONTROL My destinations]** dropdown, en selecteer het bestemmingstype u wilt filtreren aan.

![](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

Bovendien kunt u een bestemming in de onderzoeksbar ingaan om aan één enkele bestemming te isoleren. Als u de dataflows van de bestemming wilt zien kunt u het filter ![filter](../assets/ui/monitor-destinations/filter.png) naast het selecteren om een lijst van zijn actieve dataflows te zien.

![](../assets/ui/monitor-destinations/filtered-destinations.png)

Als u alle bestaande gegevensstromen over alle bestemmingen wilt bekijken, uitgezocht **[!UICONTROL Dataflows]**.

Er wordt een lijst met gegevensstromen weergegeven, gegroepeerd per bestemming. U kunt extra details voor een specifieke dataflow zien door de bestemming te vinden u wilt controleren, het filter ![filter ](../assets/ui/monitor-destinations/filter.png) naast het selecteren, en dan het filter ![filter ](../assets/ui/monitor-destinations/filter.png) naast dataflow selecteren u meer informatie over wilt.

![](../assets/ui/monitor-destinations/dashboard-dataflows.png)


De pagina met gegevensstroomuitvoering bevat informatie over de gegevensstroomuitvoering, zoals de begintijd van de gegevensstroom, de verwerkingstijd, ontvangen profielen, geactiveerde identiteiten, uitgesloten identiteiten, mislukte identiteiten, activeringsfrequentie en status. Om meer details over een specifieke dataflow looppas te zien, selecteer het filter ![filter](../assets/ui/monitor-destinations/filter.png) naast de dataflow loopingstijd.

![](../assets/ui/monitor-destinations/dashboard-dataflows-filter.png)

De dataflows detailpagina, naast de details die op de dataflows lijst worden getoond, toont specifiekere informatie over dataflow:

- **[!UICONTROL Dataflow run ID]**: De id van de gegevensstroom.
- **[!UICONTROL IMS org ID]**: De IMS-organisatie waartoe de gegevensstroom behoort.
- **[!UICONTROL Last updated]**: De tijd de dataflow looppas werd laatst bijgewerkt.

Op de detailpagina wordt ook een lijst met mislukte identiteiten en identiteiten weergegeven die zijn uitgesloten. De informatie voor zowel de mislukte als uitgesloten identiteiten wordt getoond, met inbegrip van de foutencode, het aantal van de identiteit, en beschrijving. Standaard worden in de lijst de mislukte identiteiten weergegeven. Als u overgeslagen identiteiten wilt weergeven, selecteert u de schakeloptie **[!UICONTROL Identities excluded]**.

![](../assets/ui/monitor-destinations/identities-excluded.png)

## Volgende stappen

Door deze gids te volgen, weet u nu hoe te om dataflows voor zowel partij als het stromen bestemmingen, met inbegrip van alle relevante informatie zoals verwerkingstijd, activeringstarief, en status te controleren. Lees voor meer informatie over gegevensstromen in Platform [dataflows overview](../home.md). Lees voor meer informatie over doelen het [overzicht van doelen](../../destinations/home.md).