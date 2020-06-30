---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van labels voor gegevensgebruik
topic: labels
translation-type: tm+mt
source-git-commit: d4964231ee957349f666eaf6b0f5729d19c408de
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Overzicht van labels voor gegevensgebruik

De Etikettering en de Handhaving van het Gebruik van gegevens (DULE) is het belangrijkste mechanisme van het Beheer van Gegevens van de Adobe Experience Platform. De eigenschappen DULE laten u toe om de etiketten van het gegevensgebruik op datasets en gebieden toe te passen, die elk volgens het verwante beleid van het gegevensgebruik categoriseren.

Dit document biedt een overzicht van labels voor gegevensgebruik in [!DNL Experience Platform]. Dit wordt ook wel DULE-labels genoemd. Voordat u deze handleiding leest, raadpleegt u het overzicht [van](../home.md) gegevensbeheer voor een robuustere inleiding op het DULE-kader.

## Werken met labels voor gegevensgebruik

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het in wordt opgenomen [!DNL Experience Platform], of zodra de gegevens voor gebruik in [!DNL Platform].

De etiketten van het gebruik van gegevens die op het datasetniveau worden toegepast worden verspreid aan alle gebieden binnen de dataset. De etiketten kunnen ook direct op individuele gebieden (kolomkopballen) in een dataset, zonder propagatie worden toegepast.

Zie de handleiding over [!DNL Experience Platform] ondersteunde labels voor [gegevensgebruik voor meer informatie over beschikbare labels voor gegevensgebruik in](reference.md)en het gebruiksbeleid dat ze vertegenwoordigen.

## Labelovererving voor publiekssegmenten

Alle publiekssegmenten die door de Dienst [van de Segmentatie van het](../../segmentation/home.md) Adobe Experience Platform worden gecreeerd erven de gebruiksetiketten van hun overeenkomstige datasets. Dit staat toepassingen toe die bovenop [!DNL Experience Platform] (zoals [!DNL Real-time Customer Data Platform]) worden gebouwd om de automatische handhaving van het gegevensgebruiksbeleid te verstrekken wanneer het activeren van segmenten aan bestemmingen.

Naast het erven van dataset-vlakke etiketten, erven de segmenten alle gebied-vlakke etiketten van hun bijbehorende datasets door gebrek. Afhankelijk van de manier waarop uw [!DNL Platform]gebaseerde toepassing segmenten gebruikt, kunt u mogelijk opgeven welke velden worden gebruikt, zodat het segment geen labels van uitgesloten velden kan overnemen.

Voor meer informatie over hoe de automatische handhaving in Echt - tijd CDP werkt, zie het overzicht [van het Beleid van Gegevens van](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)Adobe in real time CDP.

<!-- (Add after DEC mapping reference is added to AAM docs to link out to)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent labels and marketing actions recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to data usage labels in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Volgende stappen

Nu u de etiketten van het gegevensgebruik bent geïntroduceerd, kunt u de [gebruikersgids](user-guide.md) blijven lezen om te leren hoe te om etiketten in [!DNL Experience Platform] UI te beheren. Voor stappen op hoe te om etiketten te beheren die APIs gebruiken, zie de aangewezen sectie in de de ontwikkelaarsgids [van de Dienst van de](../../catalog/api/labels.md)Catalogus.