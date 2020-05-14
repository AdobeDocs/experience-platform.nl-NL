---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Aan de slag met het leren van machines in real time
topic: Getting started
translation-type: tm+mt
source-git-commit: dc63ad0c0764355aed267eccd1bcc4965b04dba4
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# Aan de slag met Real-Time Machine Learning (Alpha)

>[!IMPORTANT]
>Het leren van de machine in real time is niet beschikbaar aan alle gebruikers nog. Deze functie bevindt zich in alfa en wordt nog steeds getest. Dit document kan worden gewijzigd.

Als u Real-Time Machine Learning wilt gebruiken, hebt u toegang nodig tot een organisatie die beschikt over Adobe Experience Platform en Data Science Workspace. Bovendien, moet u een volledige dataset voor gebruik in opleiding en het scoren hebben.

De handleidingen voor Real-time Machine Learning vereisen een goed begrip van Python 3, [Jupyter notebooks](../jupyterlab/overview.md), gegevenswetenschap en machinaal leren.

Belangrijkste voorwaarden:

- **DSL:** Domeinspecifieke taal.
- **Rand:** In real time de functie van de het het Leren van de machine van de machine kan op de clusters van Edge dichter aan uw activiteiten en toepassingen worden in werking gesteld.
- **Hub:** De huidige alpha stelt de Echte het Leren van de machine het Leren van de Echte in werking het scoren dienst op de Hub van het Platform van de Ervaring van Adobe terwijl het Netwerk van de Rand van de Ervaring in ontwikkeling is.
- **Knooppunt:** Een knooppunt is de basiseenheid waarvan grafieken worden gevormd. Elke knoop voert een specifieke taak uit en zij kunnen samen gebruikend verbindingen worden geketend om een grafiek te vormen die een pijpleiding van XML vertegenwoordigt. De taak die door een knoop wordt uitgevoerd vertegenwoordigt een verrichting op inputgegevens zoals een transformatie van gegevens of schema, of een machine het leren conclusie. Het knooppunt geeft de getransformeerde of afgeleide waarde uit aan de volgende node(s).

## Gegevensbestanden in het Adobe Experience Platform

Om te beginnen het Leren van de Machine in real time te gebruiken, moet u toegang tot een dataset hebben. U hebt de optie om een externe dataset te gebruiken en het te uploaden aan uw milieu JupyterLab of een nieuwe dataset binnen Platform tot stand te brengen als u dit niet reeds hebt gedaan.

>[!NOTE]
>Als u reeds een dataset hebt u wenst om te gebruiken, kunt u aan [Volgende stappen](#next-steps)overslaan.

### Een externe gegevensset gebruiken

Ga voor meer informatie over het gebruik van een externe gegevensset, zoals het uploaden van gegevens naar uw JupyterLab-omgeving, naar de zelfstudie over het [analyseren van gegevens met behulp van laptops](../jupyterlab/analyze-your-data.md#external-data).

### Een nieuwe gegevensset maken

Om een nieuwe dataset voor gebruik in het Leren van de machine in real time tot stand te brengen, hebt u een gegeven-schema voor uw dataset nodig. Vervolgens moet u gegevens invoeren met het schema dat u hebt gemaakt. Gebruik de volgende zelfstudies om een dataset voor Platform te maken en te vullen:

- [Een gegevensset maken en vullen met de API](../../catalog/datasets/create.md)
- [Creeer en bevolk een dataset in UI](../../ingestion/tutorials/ingest-batch-data.md)

## Volgende stappen {#next-steps}

Zodra u uw gegevens voor het Leren van de Machines in real time hebt voorbereid, begin door de [Echt - tijdGebruiker van de Notitieboekjes](./rtml-authoring-notebook.md) van de Machine te volgen om te leren hoe te om een model ONNX tot stand te brengen en te uploaden aan de Real-time modelopslag van het Leren van de Machine.

