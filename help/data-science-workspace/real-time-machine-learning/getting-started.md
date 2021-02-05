---
keywords: Experience Platform;ontwikkelaarsgids;de Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen;In real time machine het leren;
solution: Experience Platform
title: Aan de slag met het leren van machines in real time
topic: Getting started
description: In het volgende document worden de stappen beschreven die nodig zijn om een real-time model voor machinetolken in Adobe Experience Platform te maken.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Aan de slag met Real-Time Machine Learning (Alpha)

>[!IMPORTANT]
>
>Het leren van de machine in real time is niet beschikbaar aan alle gebruikers nog. Deze functie bevindt zich in alfa en wordt nog steeds getest. Dit document kan worden gewijzigd.

Als u Real-Time Machine Learning wilt gebruiken, hebt u toegang nodig tot een organisatie die is ingericht met Adobe Experience Platform en [!DNL Data Science Workspace]. Bovendien, moet u een volledige dataset voor gebruik in opleiding en het scoren hebben.

De gidsen voor het Leren van de machine in real time vereisen een werkend begrip van Python 3, [Jupyter Notitieboekjes](../jupyterlab/overview.md), gegevenswetenschap, en machine het leren.

**Belangrijkste voorwaarden:**

- **DSL:** Domeinspecifieke taal.
- **Edge:** Real-Time Machine Learning-scoring kan in Edge-clusters worden uitgevoerd, dichter bij uw activeringen en toepassingen.
- **Hub:** De huidige alpha stelt de Echte machine in werking die de dienst van het het scoren op de Hub van Adobe Experience Platform leert terwijl het Netwerk van de Rand van de Ervaring in ontwikkeling is.
- **Knooppunt:** Een knooppunt is de basiseenheid waarvan grafieken worden gevormd. Elke knoop voert een specifieke taak uit en zij kunnen samen gebruikend verbindingen worden geketend om een grafiek te vormen die een pijpleiding van XML vertegenwoordigt. De taak die door een knoop wordt uitgevoerd vertegenwoordigt een verrichting op inputgegevens zoals een transformatie van gegevens of schema, of een machine het leren conclusie. Het knooppunt geeft de getransformeerde of afgeleide waarde uit aan de volgende node(s).

## Datasets in Adobe Experience Platform

Om te beginnen het Leren van de Machine in real time te gebruiken, moet u toegang tot een dataset hebben. U hebt de optie om een externe dataset te gebruiken en het te uploaden aan uw [!DNL JupyterLab] milieu of een nieuwe dataset binnen Platform tot stand te brengen als u dit niet reeds hebt gedaan.

>[!NOTE]
>
>Als u reeds een dataset hebt u wenst te gebruiken, kunt u aan [Volgende stappen ](#next-steps) overslaan.

### Een externe gegevensset gebruiken

Meer informatie over het gebruik van een externe dataset, zoals het uploaden van gegevens naar uw [!DNL JupyterLab]-omgeving, vindt u in de zelfstudie over [het analyseren van gegevens met behulp van laptops](../jupyterlab/analyze-your-data.md#external-data).

### Een nieuwe gegevensset maken

Om een nieuwe dataset voor gebruik in het Leren van de machine in real time tot stand te brengen, hebt u een gegeven-schema voor uw dataset nodig. Vervolgens moet u gegevens invoeren met het schema dat u hebt gemaakt. Gebruik de volgende zelfstudies om een dataset voor [!DNL Platform] te creëren en te bevolken:

- [Een gegevensset maken en vullen met de API](../../catalog/datasets/create.md)
- [Creeer en bevolk een dataset in UI](../../ingestion/tutorials/ingest-batch-data.md)

## Volgende stappen {#next-steps}

Zodra u uw gegevens voor het Leren van de Machine in real time hebt voorbereid, begin door [de Notitiegebruikershandleiding van de Notitieboekje ](./rtml-authoring-notebook.md) te volgen in real time van de Machine het Leren notitieboekje&lt;a1 te leren en een model te uploaden ONNX aan de het modelopslag van het Leren in real time van de Machine.

