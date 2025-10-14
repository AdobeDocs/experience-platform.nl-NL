---
keywords: Experience Platform;developer guide;Data Science Workspace;populaire onderwerpen;Real-time machine learning;
solution: Experience Platform
title: Aan de slag met het leren van machines in real time
description: In het volgende document worden de stappen beschreven die nodig zijn om een real-time model voor machinetolken in Adobe Experience Platform te maken.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# Aan de slag met Real-Time Machine Learning (Alpha)

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

>[!IMPORTANT]
>
>Het leren van de machine in real time is niet beschikbaar aan alle gebruikers nog. Deze functie bevindt zich in alfa en wordt nog steeds getest. Dit document kan worden gewijzigd.

Als u Real-Time Machine Learning wilt gebruiken, hebt u toegang nodig tot een organisatie die is ingericht voor Adobe Experience Platform en [!DNL Data Science Workspace] . Bovendien, moet u een volledige dataset voor gebruik in opleiding en het scoren hebben.

De gidsen voor het Leren van de machine in real time vereisen een werkend begrip van Python 3, [&#x200B; Jupyter Blocbooks &#x200B;](../jupyterlab/overview.md), gegevenswetenschap, en machine het leren.

**Zeer belangrijke Termen:**

- **DSL:** Specifieke Taal van het Domein.
- **Edge:** Echte machine het Leren van de machine het scoren van de dienst kan op de clusters van Edge dichter aan uw activeringen en toepassingen worden in werking gesteld.
- **Hub:** huidige alpha stelt de Echte machine in werking die de dienst scoring op de Hub van Adobe Experience Platform leert terwijl Edge Network in ontwikkeling is.
- **Knoop:** Een Knoop is de fundamentele eenheid waarvan de grafieken worden gevormd. Elke knoop voert een specifieke taak uit en zij kunnen samen gebruikend verbindingen worden geketend om een grafiek te vormen die een pijpleiding van XML vertegenwoordigt. De taak die door een knoop wordt uitgevoerd vertegenwoordigt een verrichting op inputgegevens zoals een transformatie van gegevens of schema, of een machine het leren conclusie. Het knooppunt geeft de getransformeerde of afgeleide waarde uit aan de volgende node(s).

## Datasets in Adobe Experience Platform

Om te beginnen het Leren van de Machine in real time te gebruiken, moet u toegang tot een dataset hebben. U kunt een externe gegevensset gebruiken en uploaden naar uw [!DNL JupyterLab] -omgeving of een nieuwe gegevensset maken in Experience Platform als u dat nog niet hebt gedaan.

>[!NOTE]
>
>Als u reeds een dataset hebt u wenst om te gebruiken, kunt u aan [&#x200B; Volgende stappen &#x200B;](#next-steps) overslaan.

### Een externe gegevensset gebruiken

Meer leren over het gebruiken van een externe dataset zoals het uploaden van gegevens aan uw [!DNL JupyterLab] milieu, bezoek het leerprogramma op [&#x200B; het analyseren van uw gegevens gebruikend laptops &#x200B;](../jupyterlab/analyze-your-data.md#external-data).

### Een nieuwe gegevensset maken

Om een nieuwe dataset voor gebruik in het Leren van de machine in real time tot stand te brengen, hebt u een gegeven-schema voor uw dataset nodig. Vervolgens moet u gegevens invoeren met het schema dat u hebt gemaakt. Gebruik de volgende zelfstudies om een gegevensset voor [!DNL Experience Platform] te maken en te vullen:

- [Een gegevensset maken en vullen met de API](../../catalog/datasets/create.md)
- [Creeer en bevolk een dataset in UI](../../ingestion/tutorials/ingest-batch-data.md)

## Volgende stappen {#next-steps}

Zodra u uw gegevens voor het Leren van de Machine in real time hebt voorbereid, begin door de [&#x200B; Echt - tijd machine te volgen die notitieboekjectgebruikershandleiding &#x200B;](./rtml-authoring-notebook.md) leren hoe te om een model ONNX tot stand te brengen en te uploaden aan de het leren modelopslag in real time van de Machine.
