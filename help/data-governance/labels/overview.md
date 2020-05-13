---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van labels voor gegevensgebruik
topic: labels
translation-type: tm+mt
source-git-commit: 4b6b9ca5ae7861f8e8b974550be14fbce6efdcf1
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Overzicht van labels voor gegevensgebruik

De Etikettering en de Handhaving van het Gebruik van gegevens (DULE) is het belangrijkste mechanisme van het Beleid van de Gegevens van het Platform van de Ervaring van Adobe. De eigenschappen DULE laten u toe om de etiketten van het gegevensgebruik op datasets en gebieden toe te passen, die elk volgens het verwante beleid van het gegevensgebruik categoriseren.

Dit document biedt een overzicht van labels voor gegevensgebruik (ook wel DULE-labels genoemd) in het Experience Platform. Voordat u deze handleiding leest, raadpleegt u het overzicht [van](../home.md) gegevensbeheer voor een robuustere inleiding op het DULE-kader.

## Werken met labels voor gegevensgebruik

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het in het Platform van de Ervaring wordt opgenomen, of zodra de gegevens voor gebruik in Platform beschikbaar worden.

De etiketten van het gebruik van gegevens die op het datasetniveau worden toegepast worden verspreid aan alle gebieden binnen de dataset. De etiketten kunnen ook direct op individuele gebieden (kolomkopballen) in een dataset, zonder propagatie worden toegepast.

Zie de handleiding over [ondersteunde labels](reference.md)voor gegevensgebruik voor meer informatie over beschikbare labels voor gegevensgebruik in het Experience Platform en het beleid dat deze vertegenwoordigen.

## Labelovererving voor publiekssegmenten

Alle publiekssegmenten die door de Segmentatieservice [van het Platform van de Ervaring van](../../segmentation/home.md) Adobe worden gecreeerd erven de gebruiksetiketten van hun overeenkomstige datasets. Dit staat toepassingen toe die bovenop het Platform van de Ervaring (zoals het Platform van de Gegevens van de Klant in real time) worden gebouwd om de automatische handhaving van het gegevensgebruiksbeleid te verstrekken wanneer het activeren van segmenten aan bestemmingen.

Naast het erven van dataset-vlakke etiketten, erven de segmenten alle gebied-vlakke etiketten van hun bijbehorende datasets door gebrek. Afhankelijk van de manier waarop uw op platform-gebaseerde toepassing segmenten gebruikt, kunt u potentieel specificeren welke gebieden worden gebruikt, daardoor verhinderend het segment etiketten van uitgesloten gebieden erven.

Voor meer informatie over hoe de automatische handhaving in Echt - tijd CDP werkt, zie het overzicht [van het Beheer van Gegevens](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)In real time CDP.

## Volgende stappen

Nu u de etiketten van het gegevensgebruik bent geïntroduceerd, kunt u de [gebruikersgids](user-guide.md) blijven lezen om te leren hoe te om etiketten in de UI van het Platform van de Ervaring te beheren. Voor stappen op hoe te om etiketten te beheren die APIs gebruiken, zie de aangewezen sectie in de de ontwikkelaarsgids [van de Dienst van de](../../catalog/api/labels.md)Catalogus.