---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Aan de slag met het leren van realtime machines
topic: Getting started
translation-type: tm+mt
source-git-commit: c9e6eb41e51ad17ad11b9a669ca5e4cf6c899f8b
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---


# Aan de slag met het leren van machines in real time

>[!IMPORTANT]
>Het leren van de machine in real time is niet beschikbaar aan alle gebruikers nog. Deze functie bevindt zich in alfa en wordt nog steeds getest. Dit document kan worden gewijzigd.

Als u Real-Time Machine Learning wilt gebruiken, hebt u toegang nodig tot een organisatie die beschikt over Adobe Experience Platform en Data Science Workspace. Bovendien, moet u een dataset in Platform hebben.

De handleidingen voor Real-time Machine Learning vereisen een goed begrip van Python 3, [Jupyter notebooks](../jupyterlab/overview.md), gegevenswetenschap en het leren van machines.

## Gegevensbestanden in het Adobe Experience Platform

Als u wilt beginnen met het gebruik van Real-time Machine Learning, moet u een gevulde dataset hebben binnen het Experience Platform. U hebt de optie om een externe dataset te gebruiken en het te uploaden aan uw milieu JupyterLab of een nieuwe dataset binnen Platform tot stand te brengen als u dit niet reeds hebt gedaan.

>[!NOTE]
>Als u reeds een dataset hebt u wenst om te gebruiken, kunt u de volgende twee stappen overslaan.

### Een externe gegevensset gebruiken

Ga voor meer informatie over het gebruik van een externe gegevensset, zoals het uploaden van gegevens naar uw JupyterLab-omgeving, naar de zelfstudie over het [analyseren van gegevens met behulp van laptops](../jupyterlab/analyze-your-data.md#external-data).

### Een nieuwe gegevensset maken

Om een nieuwe dataset voor gebruik in het Leren van de machine in real time tot stand te brengen, hebt u een gegeven-schema voor uw dataset nodig. Vervolgens moet u gegevens invoeren met het schema dat u hebt gemaakt. Gebruik de volgende zelfstudies om een dataset voor Platform te maken en te vullen:

- [Een gegevensset maken en vullen met de API](../../catalog/datasets/create.md)
- [Creeer en bevolk een dataset in UI](../../ingestion/tutorials/ingest-batch-data.md)

## Git en docker

Als u een model wilt trainen met behulp van de Data Science Workplace recept-workflow, zijn Git en Docker vereist.

>[!NOTE]
>U hoeft Git en Docker niet te downloaden als u een model wilt trainen met een Python-laptop of als u uw eigen ONNX-model gebruikt.

- [Installatiegids](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Installatiehandleiding voor dokken](https://docs.docker.com/get-docker/)

## Volgende stappen

Zodra u uw gegevens voor het Leren van de Machine in real time hebt voorbereid, begin door de zelfstudie over [opleiding een model](./training-ml-model.md) te volgen om te leren om een model te creëren en te uploaden ONNX aan de het leren van de machine in real time modelopslag te creëren en.

