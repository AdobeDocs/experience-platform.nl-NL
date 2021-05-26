---
keywords: Experience Platform;thuis;populaire onderwerpen;monitorrekeningen;monitordataflows;dataflows;bestemmingen
description: Met doelen kunt u uw gegevens activeren van Adobe Experience Platform naar talloze externe partners. Dit leerprogramma verstrekt instructies op hoe u dataflows voor uw bestemmingen kunt controleren gebruikend het gebruikersinterface van het Experience Platform.
solution: Experience Platform
title: Gegevensstromen van de monitor voor Doelen in UI
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 1d40ef02bd0bdb48bb999c3308f78824f75e3459
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---

# Dataflows voor doelen in de UI controleren

Met doelen kunt u uw gegevens activeren van Adobe Experience Platform naar talloze externe partners. Dit leerprogramma verstrekt instructies op hoe u dataflows voor uw bestemmingen kunt controleren gebruikend het gebruikersinterface van het Experience Platform.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [Doelen](../../destinations/home.md): Doelen zijn voorgebouwde integraties met veelgebruikte toepassingen die het mogelijk maken om gegevens van Platform naadloos te activeren voor kanaalmarketingcampagnes, e-mailcampagnes, gerichte reclame en vele andere gebruiksgevallen.
- [Sandboxen](../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Dataflows bewaken

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

## Dataflow wordt uitgevoerd voor streamingdoelen

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

## Dataflow wordt uitgevoerd voor batchdoelen

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


## Volgende stappen

Door deze gids te volgen, weet u nu hoe te om dataflows voor zowel partij als het stromen bestemmingen, met inbegrip van alle relevante informatie zoals verwerkingstijd, activeringstarief, en status te controleren. Lees voor meer informatie over gegevensstromen in Platform [dataflows overview](../home.md). Lees voor meer informatie over doelen het [overzicht van doelen](../../destinations/home.md).