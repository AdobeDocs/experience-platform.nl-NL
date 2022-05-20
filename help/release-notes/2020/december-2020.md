---
title: Opmerkingen bij de release van Adobe Experience Platform, december 2020
description: In de release van december 2020 staat Adobe Experience Platform vermeld.
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 9 december 2020**

Nieuwe functies in Adobe Experience Platform:

- [[!DNL Dataflows]](#dataflows)

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

Dataflows zijn een voorstelling van gegevenstaken die gegevens over het Platform verplaatsen. Deze dataflows worden gevormd over de verschillende diensten, die gegevens van bronschakelaars aan doeldatasets, aan de Dienst van de Identiteit en van het Profiel, en aan bestemmingen helpen verplaatsen.

**Sleutelfunctie**

| Functie | Beschrijving |
| ------- | ----------- |
| Transparantie voor gegevensstromen | U kunt gegevensstromen voor bronnen en bestemmingen controleren. Lees voor meer informatie de [zelfstudie over bronnen controleren](../../dataflows/ui/monitor-sources.md) of de [zelfstudie over bestemmingen controleren](../../dataflows/ui/monitor-destinations.md). |

Lees voor meer informatie over gegevensstromen de [gegevensstroomoverzicht](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

De Werkruimte van de Wetenschap van Gegevens gebruikt machine het leren en kunstmatige intelligentie om inzichten van uw gegevens tot stand te brengen. De Data Science Workspace is geïntegreerd in Adobe Experience Platform en helpt u om voorspellingen te maken met behulp van uw inhoud en gegevenselementen voor verschillende Adobe-oplossingen.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| --- | ---|
| Toevoeging Adobe Experience Platform Intelligence-pakket | Het Adobe Experience Platform Intelligence-pakket addon is een Data Science Workspace-upgrade die extra belangrijke functies zoals: <li> Door de gebruikersinterface gestuurde modelexperimenten en -evaluaties.</li><li> Mogelijkheid om modellen te implementeren en te exploiteren met geplande training en het afleiden van taken.</li><li> Ondersteuning voor diep leren in Tensorflow-modellen (GPU Compute).</li><li> Op park-gebaseerde verdeelde computer om te trainen en tegen grote datasets (10MM + rijen) te scoren.</li><li>En meer</li> |

Voor meer informatie over het addon Adobe Experience Platform Intelligence-pakket raadpleegt u de documentatie over [Toegang tot en functies van Data Science Workspace](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] diensten. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Account- en verbindingsgegevens voor streamingbronnen bijwerken | U kunt de namen, beschrijvingen en referenties van bestaande streamingverbindingen nu bijwerken met de opdracht [!DNL Flow Service] API en UI. Raadpleeg de zelfstudie voor meer informatie [bijwerken, verbindingen met de API](../../sources/tutorials/api/update.md) en [accountgegevens bewerken met de gebruikersinterface](../../sources/tutorials/ui/monitor.md). |
| Gegevensstromen verwijderen | Streaming-gegevensstromen die fouten bevatten of overbodig zijn geworden, kunnen nu worden verwijderd met de opdracht [!DNL Flow Service] API en UI. Raadpleeg de zelfstudie voor meer informatie [verwijderen, gegevensstromen met behulp van de API](../../sources/tutorials/api/delete-dataflows.md) en [het schrappen van gegevensstromen gebruikend UI](../../sources/tutorials/ui/delete.md). |

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
