---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gegevensstromen controleren en verwijderen
topic: overview
translation-type: tm+mt
source-git-commit: f08ad2c9cc48c08bcdc0e278481992e8789000b5
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---


# Gegevensstromen controleren en verwijderen

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Dit leerprogramma verstrekt stappen voor het bekijken van bestaande rekeningen en gegevensstromen van de *[!UICONTROL werkruimte van Bronnen]* . Dit leerprogramma verstrekt ook stappen voor het schrappen van gegevensstromen van de werkruimte van *[!UICONTROL Bronnen]* .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Adobe Experience Platform:

- [XDM-systeem](../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [Klantprofiel](../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## Accounts controleren

Login aan [Adobe Experience Platform](https://platform.adobe.com) en selecteer dan **[!UICONTROL Bronnen]** van de linkernavigatiebar om tot de werkruimte van *[!UICONTROL Bronnen]* toegang te hebben. In het scherm *[!UICONTROL Catalogus]* worden diverse bronnen weergegeven waarvoor u accounts en gegevensstromen kunt maken. Elke bron toont het aantal bestaande rekeningen en gegevensstromen verbonden aan hen.

Selecteer *[!UICONTROL Accounts]* in de bovenste koptekst om bestaande accounts weer te geven.

![catalogus](../../images/tutorials/monitor/catalog.png)

De pagina&#39;s *[!UICONTROL Accounts]* worden weergegeven. Op deze pagina vindt u een lijst met weer te geven accounts, waaronder informatie over de bron, gebruikersnaam, het aantal gegevensstromen en de aanmaakdatum.

Selecteer het trechter-pictogram linksboven om het sorteervenster te openen.

![rekeningen](../../images/tutorials/monitor/accounts-list.png)

Via het sorteervenster hebt u toegang tot accounts vanuit een specifieke bron. Selecteer de bron waarmee u wilt werken en selecteer het account in de lijst aan de rechterkant.

![accounts selecteren](../../images/tutorials/monitor/accounts-sort.png)

Vanuit de pagina *[!UICONTROL Accounts]* kunt u een lijst weergeven met bestaande gegevensstromen die zijn gekoppeld aan de account die u hebt geopend. Selecteer de gegevensstroom u wenst om te bekijken.

![accountpagina](../../images/tutorials/monitor/dataflows.png)

Het scherm *[!UICONTROL Dataflow-activiteit]* wordt weergegeven. Op deze pagina wordt de snelheid van berichten weergegeven die in de vorm van een grafiek worden gebruikt.

![dataset-flow-activity](../../images/tutorials/monitor/dataflow-activity.png)

## Dataflows bewaken

Dataflows zijn rechtstreeks vanuit de *[!UICONTROL Cataloguspagina]* toegankelijk zonder *[!UICONTROL accounts]* weer te geven. Selecteer *[!UICONTROL Gegevensstromen]* van de hoogste kopbal om een lijst van bestaande gegevensstromen te bekijken.

![catalogusgegevensstromen](../../images/tutorials/monitor/catalog-dataflows.png)

Er wordt een lijst met bestaande gegevensstromen weergegeven. Op deze pagina vindt u een lijst met zichtbare gegevensstromen, waaronder informatie over de bron, gebruikersnaam, het aantal gegevensstromen en de status. Selecteer het trechter-pictogram linksboven om te sorteren.

![dataflows-list](../../images/tutorials/monitor/dataflows-list.png)

Het sorteervenster wordt weergegeven. Selecteer de bron die u wilt openen in het schuifmenu en selecteer de gegevensstroom in de lijst aan de rechterkant.

![sortDataFlow](../../images/tutorials/monitor/dataflows-sort.png)

Het scherm *[!UICONTROL Dataflow-activiteit]* wordt weergegeven. Op deze pagina wordt de snelheid van berichten weergegeven die in de vorm van een grafiek worden gebruikt.

![dataset-flow-activity](../../images/tutorials/monitor/dataflow-activity.png)

Raadpleeg de zelfstudie over het [controleren van streaming dataflows voor meer informatie over het controleren van gegevensstromen](../../../ingestion/quality/monitor-data-flows.md)en het opnemen van gegevens.

## Een gegevensstroom verwijderen

U kunt gegevens verwijderen die onjuist zijn gemaakt of niet meer nodig zijn door het venster met gegevensstromen te openen. Zoek de gegevensstroom die u wilt verwijderen met het pictogram van de sorteertrechter en selecteer de gegevensstroom om het deelvenster **[!UICONTROL Eigenschappen]** te openen.

Als u een gegevensstroom wilt verwijderen, selecteert u **[!UICONTROL Verwijderen]** in de eigenschappen aan de rechterbovenhoek.

![delete-dataflows](../../images/tutorials/monitor/dataflows-sort-delete.png)

Er verschijnt een laatste bevestigingsbericht. Selecteer **[!UICONTROL Verwijderen]** om te bevestigen.

![bevestigen-schrappen](../../images/tutorials/monitor/confirm-delete.png)

Na enkele ogenblikken verschijnt er een groen bevestigingsvak onder aan het scherm om te bevestigen dat het verwijderen is gelukt.

![delete gelukt](../../images/tutorials/monitor/deletion-confirmed.png)

U kunt ook een gegevensstroom verwijderen uit het scherm *[!UICONTROL Accounts]* . Zoek de account die u wilt openen met het pictogram van de sorteertrechter en selecteer de account in de lijst.

![accounts selecteren](../../images/tutorials/monitor/accounts-sort.png)

De pagina *[!UICONTROL Accounts]* wordt weergegeven. Selecteer de gegevensstroom die u wilt verwijderen en selecteer vervolgens **[!UICONTROL Verwijderen]** in het deelvenster Eigenschappen om het proces te voltooien.

![accounts-delete](../../images/tutorials/monitor/accounts-delete.png)

Volg de bovenstaande bevestigingsstappen om het proces te voltooien.

## Volgende stappen

Door dit leerprogramma te volgen, hebt u met succes bestaande rekeningen en gegevensstromen van de *[!UICONTROL werkruimte van Bronnen]* betreden. Inkomende gegevens kunnen nu worden gebruikt door downstreamdiensten [!DNL Platform] zoals [!DNL Real-time Customer Profile] en [!DNL Data Science Workspace]. Raadpleeg de volgende documenten voor meer informatie:

- [Overzicht van het realtime klantprofiel](../../../profile/home.md)
- [Overzicht van de Data Science Workspace](../../../data-science-workspace/home.md)