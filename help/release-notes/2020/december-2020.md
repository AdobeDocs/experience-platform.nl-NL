---
title: Opmerkingen bij de release van Adobe Experience Platform, december 2020
description: In de release van december 2020 staat een opmerking voor Adobe Experience Platform.
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 11%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum:donderdag 9 december 2020**

Nieuwe functies in Adobe Experience Platform:

- [[!DNL Dataflows]](#dataflows)

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

Dataflows zijn een voorstelling van gegevenstaken die gegevens over Experience Platform verplaatsen. Deze dataflows worden gevormd over de verschillende diensten, die gegevens van bronschakelaars aan doeldatasets, aan de Dienst van de Identiteit en van het Profiel, en aan bestemmingen helpen verplaatsen.

**Zeer belangrijke eigenschap**

| Functie | Beschrijving |
| ------- | ----------- |
| Transparantie voor gegevensstromen | U kunt gegevensstromen voor bronnen en bestemmingen controleren. Voor meer informatie, te lezen gelieve het [ leerprogramma op controlebronnen ](../../dataflows/ui/monitor-sources.md) of [ leerprogramma op controlebestemmingen ](../../dataflows/ui/monitor-destinations.md). |

Om meer over gegevensstromen te leren, te lezen gelieve [ dataflows overzicht ](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace maakt gebruik van machinaal leren en kunstmatige intelligentie om inzichten te creëren op basis van uw gegevens. Met Data Science Workspace, dat in Adobe Experience Platform is geïntegreerd, kunt u voorspellingen maken met behulp van uw inhoud en gegevenselementen voor alle Adobe-oplossingen.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| --- | ---|
| Toevoeging Adobe Experience Platform Intelligence-pakket | Het Adobe Experience Platform Intelligence-pakket addon is een Data Science Workspace-upgrade die extra belangrijke functies zoals: <li> Door de gebruikersinterface gestuurde modelexperimenten en -evaluaties.</li><li> Mogelijkheid om modellen te implementeren en te exploiteren met geplande training en het afleiden van taken.</li><li> Ondersteuning voor diep leren in Tensorflow-modellen (GPU Compute).</li><li> Op park-gebaseerde verdeelde computer om te trainen en tegen grote datasets (10MM + rijen) te scoren.</li><li>En meer</li> |

Om meer over het pakket van de Intelligentie van Adobe Experience Platform te leren addon, te zien gelieve de documentatie over {de toegang en de eigenschappen van Workspace van de Wetenschap van 0} Gegevens ](../../data-science-workspace/access-features-dsw.md).[

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Experience Platform] -services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudgebaseerde opslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Account- en verbindingsgegevens voor streamingbronnen bijwerken | U kunt de namen, beschrijvingen en referenties van bestaande streamingverbindingen nu bijwerken met de API van [!DNL Flow Service] en de gebruikersinterface. Voor meer informatie, zie het leerprogramma bij [ het bijwerken verbindingen gebruikend API ](../../sources/tutorials/api/update.md) en [ het uitgeven rekeningsdetails gebruikend UI ](../../sources/tutorials/ui/monitor.md). |
| Gegevensstromen verwijderen | Streaming-gegevensstromen die fouten bevatten of onnodig zijn geworden, kunnen nu worden verwijderd met de API van [!DNL Flow Service] en de gebruikersinterface. Voor meer informatie, zie het leerprogramma bij [ het schrappen dataflows gebruikend API ](../../sources/tutorials/api/delete-dataflows.md) en [ het schrappen dataflows gebruikend UI ](../../sources/tutorials/ui/delete.md). |

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
