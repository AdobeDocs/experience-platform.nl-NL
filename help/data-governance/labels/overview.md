---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van labels voor gegevensgebruik
topic: labels
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---


# Overzicht van labels voor gegevensgebruik

De Etikettering en de Handhaving van het Gebruik van gegevens (DULE) is het belangrijkste mechanisme van Adobe Experience Platform [!DNL Data Governance]. De eigenschappen DULE laten u toe om de etiketten van het gegevensgebruik op datasets en gebieden toe te passen, die elk volgens het verwante beleid van het gegevensgebruik categoriseren.

Dit document biedt een overzicht van labels voor gegevensgebruik in [!DNL Experience Platform]. Dit wordt ook wel DULE-labels genoemd. Voordat u deze handleiding leest, raadpleegt u het overzicht [van](../home.md) gegevensbeheer voor een robuustere inleiding op het DULE-kader.

## Werken met labels voor gegevensgebruik

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het in wordt opgenomen [!DNL Experience Platform], of zodra de gegevens voor gebruik in [!DNL Platform].

De etiketten van het gebruik van gegevens die op het datasetniveau worden toegepast worden verspreid aan alle gebieden binnen de dataset. De etiketten kunnen ook direct op individuele gebieden (kolomkopballen) in een dataset, zonder propagatie worden toegepast.

[!DNL Platform] biedt verschillende &#39;core&#39; labels voor gegevensgebruik buiten de box, die een groot aantal gemeenschappelijke beperkingen bestrijken die van toepassing zijn op gegevensbeheer. Zie de handleiding over [kernlabels](reference.md)voor meer informatie over deze labels en het gebruiksbeleid dat ze vertegenwoordigen.

Naast de labels die door Adobe worden geleverd, kunt u ook uw eigen aangepaste labels definiëren. Raadpleeg de gebruikershandleiding bij de labels voor [gegevensgebruik voor informatie over hoe u dit in de gebruikersinterface kunt doen](./user-guide.md). Raadpleeg de API-handleiding [voor labels voor](./api.md)gegevensgebruik voor informatie over hoe u dit kunt doen met API-aanroepen.

## Labelovererving voor publiekssegmenten

Alle publiekssegmenten die door de Dienst [van de Segmentatie van het](../../segmentation/home.md) Adobe Experience Platform worden gecreeerd erven de gebruiksetiketten van hun overeenkomstige datasets. Dit staat toepassingen toe die bovenop [!DNL Experience Platform] (zoals [!DNL Real-time Customer Data Platform]) worden gebouwd om de automatische handhaving van het gegevensgebruiksbeleid te verstrekken wanneer het activeren van segmenten aan bestemmingen.

Naast het erven van dataset-vlakke etiketten, erven de segmenten alle gebied-vlakke etiketten van hun bijbehorende datasets door gebrek. Afhankelijk van de manier waarop uw [!DNL Platform]gebaseerde toepassing segmenten gebruikt, kunt u mogelijk opgeven welke velden worden gebruikt, zodat het segment geen labels van uitgesloten velden kan overnemen.

Voor meer informatie over hoe de automatische handhaving in Echt - tijd CDP werkt, zie het overzicht [van het Beleid van Gegevens van](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)Adobe in real time CDP.

### Overerving van de Controles van de Uitvoer van Gegevens van de Adobe Audience Manager

[!DNL Experience Platform] heeft de capaciteit om segmenten met Adobe Audience Manager te delen. Om het even welke Controles van de Uitvoer van Gegevens die op de segmenten van de Audience Manager zijn toegepast worden vertaald in gelijkwaardige etiketten en marketing acties die door [!DNL Experience Platform][!DNL Data Governance]. worden erkend.

Voor een verwijzing op hoe de specifieke Controles van de Uitvoer van Gegevens aan de etiketten van het gegevensgebruik in in kaart brengen, gelieve te verwijzen naar de documentatie [!DNL Platform]van de [](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)Audience Manager.


## Volgende stappen

Nu u de etiketten van het gegevensgebruik bent geïntroduceerd, kunt u de [gebruikersgids](user-guide.md) blijven lezen om te leren hoe te om etiketten in [!DNL Experience Platform] UI te beheren. Zie de handleiding voor [](./api.md)gebruikslabels voor informatie over het beheren van labels met behulp van API&#39;s.