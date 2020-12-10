---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform 9 december 2020
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
translation-type: tm+mt
source-git-commit: ae353e6dda3f92647c32ee8e731be5785d24e5cb
workflow-type: tm+mt
source-wordcount: '426'
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
| Transparantie voor gegevensstromen | U kunt gegevensstromen voor bronnen en bestemmingen controleren. Lees voor meer informatie de [zelfstudie over monitoringbronnen](../../dataflows/ui/monitor-sources.md) of de [zelfstudie over het controleren van bestemmingen](../../dataflows/ui/monitor-destinations.md). |

Lees het [dataflows-overzicht](../../dataflows/home.md)voor meer informatie over gegevensstromen.

## [!DNL Data Science Workspace] {#dsw}

De Werkruimte van de Wetenschap van Gegevens gebruikt machine het leren en kunstmatige intelligentie om inzichten van uw gegevens tot stand te brengen. De Data Science Workspace is geïntegreerd in Adobe Experience Platform en helpt u om voorspellingen te maken met behulp van uw inhoud en gegevenselementen voor verschillende Adobe-oplossingen.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| --- | ---|
| Toevoeging Adobe Experience Platform Intelligence-pakket | Het Adobe Experience Platform Intelligence-pakket addon is een Data Science Workspace-upgrade die extra belangrijke functies zoals: <li> Door de gebruikersinterface gestuurde modelexperimenten en -evaluaties.</li><li> Mogelijkheid om modellen te implementeren en te exploiteren met geplande training en het afleiden van taken.</li><li> Ondersteuning voor diep leren in Tensorflow-modellen (GPU Compute).</li><li> Op park-gebaseerde verdeelde computer om te trainen en tegen grote datasets (10MM + rijen) te scoren.</li><li>En meer</li> |

Raadpleeg de documentatie over de toegang tot en de functies [](../../data-science-workspace/access-features-dsw.md)van de Data Science Workspace voor meer informatie over het Adobe Experience Platform Intelligence-pakket.

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Account- en verbindingsgegevens voor streamingbronnen bijwerken | U kunt de namen, beschrijvingen en referenties van bestaande streamingverbindingen nu bijwerken met behulp van de API en de [!DNL Flow Service] UI. Zie de zelfstudie over het [bijwerken van verbindingen met de API](../../sources/tutorials/api/update.md) en het [bewerken van accountgegevens met de gebruikersinterface](../../sources/tutorials/ui/monitor.md)voor meer informatie. |
| Gegevensstromen verwijderen | Streaming-gegevensstromen die fouten bevatten of onnodig zijn geworden, kunnen nu worden verwijderd met de API en de interface [!DNL Flow Service] . Zie de zelfstudie over het [verwijderen van gegevensstromen met de API](../../sources/tutorials/api/delete-dataflows.md) en het [verwijderen van gegevensstromen met de UI](../../sources/tutorials/ui/delete.md)voor meer informatie. |

Zie het [bronoverzicht](../../sources/home.md)voor meer informatie over bronnen.


