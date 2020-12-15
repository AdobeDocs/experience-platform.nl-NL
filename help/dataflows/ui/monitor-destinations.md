---
keywords: Experience Platform;home;popular topics;monitor accounts;monitor dataflows;dataflows;destinations
description: Met doelen kunt u uw gegevens activeren van Adobe Experience Platform naar talloze externe partners. Dit leerprogramma verstrekt instructies op hoe u dataflows voor uw bestemmingen kunt controleren gebruikend het gebruikersinterface van het Experience Platform.
solution: Experience Platform
title: Dataflows bewaken
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 12a6682b6e28e656899aee5c38d3bb4a84bcdd2f
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Dataflows voor doelen in de UI controleren

Met doelen kunt u uw gegevens activeren van Adobe Experience Platform naar talloze externe partners. Dit leerprogramma verstrekt instructies op hoe u dataflows voor uw bestemmingen kunt controleren gebruikend het gebruikersinterface van het Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [Doelen](../../destinations/home.md): Doelen zijn voorgebouwde integraties met veelgebruikte toepassingen die het mogelijk maken om gegevens van Platform naadloos te activeren voor kanaalmarketingcampagnes, e-mailcampagnes, gerichte reclame en vele andere gebruiksgevallen.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Dataflows bewaken

Navigeer in de werkruimte **[!UICONTROL Doelen]** in de interface van het Platform naar het tabblad **[!UICONTROL Bladeren]** en selecteer de naam van een bestemming die u wilt weergeven.

![](../assets/ui/monitor-destinations/select-destination.png)

Er wordt een lijst met bestaande gegevensstromen weergegeven. Op deze pagina vindt u een lijst met zichtbare gegevensstromen, waaronder informatie over het doel, de gebruikersnaam, het aantal gegevensstromen en de status.

Zie de volgende tabel voor meer informatie over statussen:

| Status | Beschrijving |
| ------ | ----------- |
| Ingeschakeld | De `Enabled` status wijst erop dat een dataflow actief is en gegevens volgens het programma opneemt het werd verstrekt. |
| Uitgeschakeld | De `Disabled` status geeft aan dat een gegevensstroom inactief is en geen gegevens opneemt. |
| Verwerking | De `Processing` status geeft aan dat een gegevensstroom nog niet actief is. Deze status wordt vaak direct na het maken van een nieuwe gegevensstroom aangetroffen. |
| Fout | De `Error` status geeft aan dat het activeringsproces van een gegevensstroom is onderbroken. |

## [!UICONTROL Dataflow-uitvoering]

Het [!UICONTROL Dataflow looppas] lusje verstrekt metrische gegevens over uw dataflow looppas aan partijbestemmingen. Er wordt een lijst weergegeven met afzonderlijke uitvoeringen en de bijbehorende maatstaven, samen met de volgende totalen voor profielrecords:

- **[!UICONTROL Profielrecords geactiveerd]**: Het totale aantal profielrecords dat voor activering is gemaakt of bijgewerkt.
- **[!UICONTROL Profielrecords overgeslagen]**:  Het totale aantal profielrecords dat voor activering wordt overgeslagen op basis van het profiel, wordt afgesloten of ontbrekende kenmerken.

![](../assets/ui/monitor-destinations/dataflow-runs.png)

>[!NOTE]
>
>De looppas van Dataflow wordt geproduceerd gebaseerd op de planningsfrequentie van bestemmingsdataflow. Een afzonderlijke dataflow looppas wordt gemaakt voor elk samenvoegbeleid dat op een segment wordt toegepast.

Om de details van een bepaalde dataflow looppas te bekijken, selecteer de begintijd van de looppas van de lijst. De detailpagina voor een dataflow-run bevat aanvullende informatie zoals de grootte van de verwerkte gegevens en een lijst met eventuele fouten die zijn opgetreden met details voor de diagnose van fouten.

![](../assets/ui/monitor-destinations/dataflow.png)