---
title: De einddatum van gegevensset-exportgegevens bijwerken (actie vereist op 1 mei 2025)
type: Tutorial
hide: true
hidefromtoc: true
description: Leer hoe te om de einddatum voor dataset de uitvoerdataflows met een huidige einddatum van 1 Mei, 2025 bij te werken.
source-git-commit: aeabbb56002f8640b79ff3a7e3dc532d01ebbadf
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# De einddatum van gegevensset-exportgegevens bijwerken (actie vereist op 1 mei 2025)

>[!IMPORTANT]
>
>De actiepunten op deze pagina zijn van toepassing als uw organisatie gegevensset uitvoergegevens vóór de release van september 2024 van Experience Platform instelt.

## Wat gebeurt er?

[ September 2024 versie van Experience Platform ](/help/release-notes/latest/latest.md#destinations) introduceerde de optie om een `endTime` datum voor de gegevensstroom van de uitvoerdataset te plaatsen. Adobe heeft ook een standaardeinddatum van 1 Mei, 2025, voor alle gegevens van de datasetuitvoer gecreeerd *vóór de versie van september 2024* geïntroduceerd. Deze gegevensstromen tonen momenteel een bericht gelijkend op hieronder getoond.

![ bericht UI over de behoefte om de einddatum van de dataflow van de uitvoerdataset bij te werken.](/help/destinations/assets/ui/export-datasets/update-end-date.png)

**het punt van de Actie**: Voor om het even welk van deze dataflows, moet u de einddatum manueel bijwerken alvorens het verloopt; anders, zal uw uitvoer ophouden. Gebruik de gebruikersinterface van Experience Platform om te bepalen welke gegevensstromen op 1 mei 2025 worden geplaatst te stoppen.

## Waarom word ik op de hoogte gesteld?

Uw organisatie is geïdentificeerd als hebbend actieve gegevensreeks de uitvoerdataflows met een einddatum van 1 Mei, 2025.

## De gebruikersinterface gebruiken om de einddatum bij te werken

Gebruik de gebruikersinterface van Experience Platform om gegevensstromen met een einddatum van 1 mei 2025 te identificeren, en hen bij te werken aan een toekomstige datum.

### Zoek de gegevensstromen die moeten worden bijgewerkt

Navigeer aan **Doelen > doorbladeren** en zoek het gegevenstype **Datasets** in de **kolom van het Type van Gegevens**, zoals hieronder getoond. Selecteer de gewenste gegevensstromen om hen te inspecteren.

![ de uitvoerdataflows van de Dataset die in het Browse lusje worden benadrukt.](/help/destinations/assets/ui/export-datasets/view-dataset-dataflows.png)

### De einddatum van de gegevensstromen bijwerken

De einddatum van gegevensstromen bijwerken:

1. In de dataflows die u voor inspectie in de vorige stap hebt geselecteerd, uitgezochte **datasets van de Uitvoer**.
   ![ de controle van de datasets van de Uitvoer die in Browse tabel wordt benadrukt.](/help/destinations/assets/ui/export-datasets/export-datasets-control-highlighted.png)
2. In het werkschema, ga aan de **Plannende** stap te werk en selecteer **uitgeef programma**.
   ![ geeft programmacontrole uit die in de Plannende stap wordt benadrukt.](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlighted.png)
3. Kies een gewenste einddatum na 1 Mei, 2025 en selecteer **sparen**.
   ![ Uitgezochte controle van de einddatum die in de Plannende stap wordt benadrukt.](/help/destinations/assets/ui/export-datasets/select-end-date.png)
4. Ga naar het einde van de workflow en sla uw updates op.

Voor uitgebreide informatie over de het plannen stap, lees het [ leerprogramma van de de uitvoerdatasets UI ](/help/destinations/api/export-datasets.md#scheduling).

## De API gebruiken om de einddatum bij te werken

### Zoek de gegevensstromen die moeten worden bijgewerkt

### De einddatum van de gegevensstromen bijwerken
