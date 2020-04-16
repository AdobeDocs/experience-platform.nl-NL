---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Accounts en gegevenssetstromen bewaken
topic: overview
translation-type: tm+mt
source-git-commit: fc0a406bdea7b31e046d02427805a9deba557e93

---


# Accounts en gegevenssetstromen bewaken

De bronschakelaars in het Platform van de Ervaring van Adobe verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Dit leerprogramma verstrekt stappen voor het bekijken van bestaande rekeningen en datasetstromen van de werkruimte van *Bronnen* .

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

- [XDM-systeem](../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   - [Basisbeginselen van de schemacompositie](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [Klantprofiel](../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## Accounts controleren

Meld u aan bij <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer vervolgens **Bronnen** in de linkernavigatiebalk voor toegang tot de werkruimte *Bronnen* . Het scherm van de *Catalogus* toont een verscheidenheid van bronnen waarvoor u de stromen van de rekeningsdataset kunt tot stand brengen met. Elke bron toont het aantal bestaande rekeningen en datasetstromen verbonden aan hen.

Selecteer *Accounts* in de bovenste koptekst om bestaande accounts weer te geven.

![catalogus](../../images/tutorials/monitor/catalog.png)

De pagina&#39;s *Accounts* worden weergegeven. Op deze pagina vindt u een lijst met te bekijken accounts, waaronder informatie over de bron, gebruikersnaam, het aantal gegevenssetstromen en de aanmaakdatum.

Selecteer het pictogram linksboven om het sorteervenster te openen.

![rekeningen](../../images/tutorials/monitor/accounts-list.png)

Via het sorteervenster hebt u toegang tot accounts vanuit een specifieke bron. Selecteer de bron waarmee u wilt werken en selecteer het account in de lijst aan de rechterkant.

![accounts selecteren](../../images/tutorials/monitor/accounts-sort.png)

Van de pagina van *Rekeningen* , kunt u een lijst van bestaande datasetstromen bekijken verbonden aan de rekening u toegang had tot. Selecteer de datasetstroom u wenst om te bekijken.

![accountpagina](../../images/tutorials/monitor/dataset-flows.png)

Het scherm *Dataset flow activity* wordt weergegeven. Op deze pagina wordt de snelheid van berichten weergegeven die in de vorm van een grafiek worden gebruikt.

![dataset-flow-activity](../../images/tutorials/monitor/dataset-flows-activity.png)

## Gegevensstromen controleren

Datasetstromen zijn rechtstreeks vanuit de *Cataloguspagina* toegankelijk zonder *accounts* weer te geven. Selecteer *Datasetstromen* in de bovenste koptekst om een lijst met bestaande gegevenssetstromen weer te geven.

![gegevenssetstromen](../../images/tutorials/monitor/dataset-flows-list.png)

Net als bij accounts kunt u de lijst met gegevenssetstromen sorteren met het sorteerpictogram linksboven. Selecteer de bron u wenst om de datasetstroom van de lijst op het recht te bekijken en te selecteren.

![select-dataset-flows](../../images/tutorials/monitor/dataset-flows-sort.png)

Het scherm *Dataset flow activity* wordt weergegeven. Op deze pagina wordt de snelheid van berichten weergegeven die in de vorm van een grafiek worden gebruikt.

![dataset-flow-activity](../../images/tutorials/monitor/dataset-flows-activity.png)

Voor meer informatie over het controleren van datasets en ingestie, verwijs naar het leerprogramma bij het [controleren van het stromen gegevens](../../../ingestion/quality/monitor-data-flows.md).

## Volgende stappen

Door dit leerprogramma te volgen, hebt u met succes bestaande rekeningen en datasetstromen van de *Bronwerkruimte* betreden. De inkomende gegevens kunnen nu door de stroomafwaartse diensten van het Platform zoals het Profiel van de Klant in real time en de Werkruimte van de Wetenschap van Gegevens worden gebruikt. Raadpleeg de volgende documenten voor meer informatie:

- [Overzicht van het realtime klantprofiel](../../../profile/home.md)
- [Overzicht van de Data Science Workspace](../../../data-science-workspace/home.md)