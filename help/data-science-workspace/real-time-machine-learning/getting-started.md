---
keywords: Experience Platform;ontwikkelaarsgids;de Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen;In real time machine het leren;
solution: Experience Platform
title: Aan de slag met het leren van machines in real time
description: In het volgende document worden de stappen beschreven die nodig zijn om een real-time model voor machinetolken in Adobe Experience Platform te maken.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Aan de slag met Real-Time Machine Learning (Alpha)

>[!IMPORTANT]
>
>Het leren van de machine in real time is niet beschikbaar aan alle gebruikers nog. Deze functie bevindt zich in alfa en wordt nog steeds getest. Dit document kan worden gewijzigd.

Als u Real-Time Machine Learning wilt gebruiken, hebt u toegang nodig tot een organisatie die is ingericht voor Adobe Experience Platform en [!DNL Data Science Workspace]. Bovendien, moet u een volledige dataset voor gebruik in opleiding en het scoren hebben.

De gidsen voor het Leren van de machine in real time vereisen een werkend begrip van Python 3, [Jupyter-laptops](../jupyterlab/overview.md), gegevenswetenschap en machinaal leren.

**Belangrijkste voorwaarden:**

- **DSL:** Domeinspecifieke taal.
- **Rand:** In real time de functie van de het het Leren van de machine van de machine kan op de clusters van Edge dichter aan uw activiteiten en toepassingen worden in werking gesteld.
- **Hub:** De huidige alpha stelt de Echte het Leren van de machine het Leren van de Echte - tijd in werking de dienst op de Hub van Adobe Experience Platform terwijl het Netwerk van de Rand in ontwikkeling is.
- **Knooppunt:** Een knooppunt is de basiseenheid waarvan grafieken worden gevormd. Elke knoop voert een specifieke taak uit en zij kunnen samen gebruikend verbindingen worden geketend om een grafiek te vormen die een pijpleiding van XML vertegenwoordigt. De taak die door een knoop wordt uitgevoerd vertegenwoordigt een verrichting op inputgegevens zoals een transformatie van gegevens of schema, of een machine het leren conclusie. Het knooppunt geeft de getransformeerde of afgeleide waarde uit aan de volgende node(s).

## Datasets in Adobe Experience Platform

Om te beginnen het Leren van de Machine in real time te gebruiken, moet u toegang tot een dataset hebben. U hebt de optie om een externe dataset te gebruiken en het te uploaden aan uw [!DNL JupyterLab] milieu of creeer een nieuwe dataset binnen Platform als u dit nog niet hebt gedaan.

>[!NOTE]
>
>Als u reeds een dataset hebt u wenst te gebruiken, kunt u overslaan aan [Volgende stappen](#next-steps).

### Een externe gegevensset gebruiken

Meer informatie over het gebruiken van een externe dataset zoals het uploaden van gegevens aan uw [!DNL JupyterLab] omgeving, bezoek de zelfstudie op [uw gegevens analyseren met behulp van notebooks](../jupyterlab/analyze-your-data.md#external-data).

### Een nieuwe gegevensset maken

Om een nieuwe dataset voor gebruik in het Leren van de machine in real time tot stand te brengen, hebt u een gegeven-schema voor uw dataset nodig. Vervolgens moet u gegevens invoeren met het schema dat u hebt gemaakt. Gebruik de volgende zelfstudies om een dataset te creëren en te bevolken voor [!DNL Platform]:

- [Een gegevensset maken en vullen met de API](../../catalog/datasets/create.md)
- [Creeer en bevolk een dataset in UI](../../ingestion/tutorials/ingest-batch-data.md)

## Volgende stappen {#next-steps}

Nadat u uw gegevens hebt voorbereid voor Real-time Machine Learning, begint u met het volgen van de [Gebruikershandleiding voor laptop in realtime leren van machines](./rtml-authoring-notebook.md) leren om een model te creëren en te uploaden ONNX aan de Echte - tijd machine het Leren modelopslag.
