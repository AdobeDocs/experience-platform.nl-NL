---
keywords: Experience Platform;ontwikkelaarshandleiding;Data Science Workspace;populaire onderwerpen;In real time machinaal leren;
solution: Experience Platform
title: Aan de slag met het leren van machines in real time
description: In het volgende document worden de stappen beschreven die zijn vereist om een Real-Time Machine Learning-model in Adobe Experience Platform te maken.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Aan de slag met Real-Time Machine Learning (Alpha)

>[!NOTE]
>
>Data Science Workspace is niet meer verkrijgbaar.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

>[!IMPORTANT]
>
>Het leren van de machine in real time is niet beschikbaar aan alle gebruikers nog. Deze functie bevindt zich in alfa en wordt nog steeds getest. Dit document kan worden gewijzigd.

Als u Real-Time Machine Learning wilt gebruiken, hebt u toegang nodig tot een organisatie die is ingericht voor Adobe Experience Platform en [!DNL Data Science Workspace] . Bovendien, moet u een volledige dataset voor gebruik in opleiding en het scoren hebben.

De gidsen voor het Leren van de machine in real time vereisen een werkend begrip van Python 3, [ Jupyter Blocbooks ](../jupyterlab/overview.md), gegevenswetenschap, en machine het leren.

**Zeer belangrijke Termen:**

- **DSL:** Specifieke Taal van het Domein.
- **Edge:** Echte machine het Leren van de machine het scoren van de dienst kan op de clusters van Edge dichter aan uw activeringen en toepassingen worden in werking gesteld.
- **Hub:** De huidige alpha stelt de Echte het Leren van de Machine in werking die dienst op de Hub van Adobe Experience Platform leert terwijl de Edge Network in ontwikkeling is.
- **Knoop:** Een Knoop is de fundamentele eenheid waarvan de grafieken worden gevormd. Elke knoop voert een specifieke taak uit en zij kunnen samen gebruikend verbindingen worden geketend om een grafiek te vormen die een pijpleiding van XML vertegenwoordigt. De taak die door een knoop wordt uitgevoerd vertegenwoordigt een verrichting op inputgegevens zoals een transformatie van gegevens of schema, of een machine het leren conclusie. Het knooppunt geeft de getransformeerde of afgeleide waarde uit aan de volgende node(s).

## Datasets in Adobe Experience Platform

Om te beginnen het Leren van de Machine in real time te gebruiken, moet u toegang tot een dataset hebben. U hebt de optie om een externe dataset te gebruiken en het te uploaden aan uw [!DNL JupyterLab] milieu of een nieuwe dataset binnen Platform tot stand te brengen als u dit nog niet hebt gedaan.

>[!NOTE]
>
>Als u reeds een dataset hebt u wenst om te gebruiken, kunt u aan [ Volgende stappen ](#next-steps) overslaan.

### Een externe gegevensset gebruiken

Meer leren over het gebruiken van een externe dataset zoals het uploaden van gegevens aan uw [!DNL JupyterLab] milieu, bezoek het leerprogramma op [ het analyseren van uw gegevens gebruikend laptops ](../jupyterlab/analyze-your-data.md#external-data).

### Een nieuwe gegevensset maken

Om een nieuwe dataset voor gebruik in het Leren van de machine in real time tot stand te brengen, hebt u een gegeven-schema voor uw dataset nodig. Vervolgens moet u gegevens opnemen met het schema dat u hebt gemaakt. Gebruik de volgende zelfstudies om een gegevensset voor [!DNL Platform] te maken en te vullen:

- [Een gegevensset maken en invullen in de API](../../catalog/datasets/create.md)
- [Creeer en bevolk een dataset in UI](../../ingestion/tutorials/ingest-batch-data.md)

## Volgende stappen {#next-steps}

Zodra u uw gegevens voor het Leren van de Machine in real time hebt voorbereid, begin door de [ Echt - tijd machine te volgen die notitieboekjectgebruikershandleiding ](./rtml-authoring-notebook.md) leren hoe te om een model ONNX tot stand te brengen en te uploaden aan de het leren modelopslag in real time van de Machine.
