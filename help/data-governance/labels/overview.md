---
keywords: Experience Platform;home;popular topics;data governance;data usage label api;policy service api;data usage labels overview
solution: Experience Platform
title: Overzicht van labels voor gegevensgebruik
topic: labels
description: Met Adobe Experience Platform Data Governance kunt u gegevensgebruikslabels toepassen op gegevenssets en velden, waarbij elk veld wordt ingedeeld volgens het beleid voor het gebruik van verwante gegevens. Dit document biedt een overzicht van labels voor gegevensgebruik in Experience Platform.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---


# Overzicht van labels voor gegevensgebruik

Adobe Experience Platform [!DNL Data Governance] staat u toe om de etiketten van het gegevensgebruik op datasets en gebieden toe te passen, die elk volgens het verwante beleid van het gegevensgebruik categoriseren.

Dit document biedt een overzicht van labels voor gegevensgebruik in [!DNL Experience Platform]. Voordat u deze handleiding leest, raadpleegt u het overzicht [van](../home.md) gegevensbeheer voor een robuustere inleiding op het kader voor gegevensbeheer.

## Werken met labels voor gegevensgebruik

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het in wordt opgenomen [!DNL Experience Platform], of zodra de gegevens voor gebruik in [!DNL Platform].

De etiketten van het gebruik van gegevens die op het datasetniveau worden toegepast worden verspreid aan alle gebieden binnen de dataset. De etiketten kunnen ook direct op individuele gebieden (kolomkopballen) in een dataset, zonder propagatie worden toegepast.

[!DNL Platform] biedt verschillende &#39;core&#39; labels voor gegevensgebruik buiten de box, die een groot aantal gemeenschappelijke beperkingen bestrijken die van toepassing zijn op gegevensbeheer. Zie de handleiding over [kernlabels](reference.md)voor meer informatie over deze labels en het gebruiksbeleid dat ze vertegenwoordigen.

Naast de labels die door Adobe worden verschaft, kunt u ook uw eigen aangepaste labels voor uw organisatie definiëren. Zie de sectie over het [beheren van labels](#manage-labels) voor meer informatie.

## Labelovererving voor publiekssegmenten

Alle publiekssegmenten die door de Dienst [van de Segmentatie van](../../segmentation/home.md) Adobe Experience Platform worden gecreeerd erven de gebruiksetiketten van hun overeenkomstige datasets. Dit staat toepassingen toe die bovenop Experience Platform (zoals [!DNL Real-time Customer Data Platform]) worden gebouwd om de automatische handhaving van het gegevensgebruiksbeleid te verstrekken wanneer het activeren van segmenten aan bestemmingen.

Naast het erven van dataset-vlakke etiketten, erven de segmenten alle gebied-vlakke etiketten van hun bijbehorende datasets door gebrek. Afhankelijk van de manier waarop uw [!DNL Platform]gebaseerde toepassing segmenten gebruikt, kunt u mogelijk opgeven welke velden worden gebruikt, zodat het segment geen labels van uitgesloten velden kan overnemen.

Voor meer informatie over hoe de automatische handhaving in Echt - tijd CDP werkt, zie het overzicht over het Beheer van [Gegevens in Echt - tijd CDP](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance).

### Overerving van Adobe Audience Manager Data Export Controls

[!DNL Experience Platform] kan segmenten delen met Adobe Audience Manager. Om het even welke Controles van de Uitvoer van Gegevens die op de segmenten van de Audience Manager zijn toegepast worden vertaald in gelijkwaardige etiketten en marketing acties die door [!DNL Experience Platform][!DNL Data Governance]. worden erkend.

Voor een verwijzing op hoe de specifieke Controles van de Uitvoer van Gegevens aan de etiketten van het gegevensgebruik in in kaart brengen, gelieve te verwijzen naar de documentatie [!DNL Platform]van de [](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)Audience Manager.

## Labels voor gegevensgebruik beheren in [!DNL Experience Platform] {#manage-labels}

U kunt labels voor gegevensgebruik beheren met API&#39; [!DNL Experience Platform] s of de gebruikersinterface. Raadpleeg de onderstaande subsecties voor meer informatie over elke subsectie.

### De gebruikersinterface gebruiken

De werkruimte **[!UICONTROL Beleid]** in [!DNL Experience Platform] UI staat u toe om kern en douanelabels voor uw organisatie te bekijken en te beheren. In de **[!DNL Datasets]** werkruimte kunt u labels toepassen op gegevenssets en velden. Raadpleeg de gebruikershandleiding bij [](user-guide.md)labels voor meer informatie.

### API&#39;s gebruiken

Het `/labels` eindpunt in de [Dienst API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) van het Beleid staat u toe om de etiketten van het gegevensgebruik programmatically te beheren, met inbegrip van het creëren van douanelabels. Raadpleeg de handleiding voor het [eindpunt van labels](../api/labels.md) voor meer informatie.

De [Dataset Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) wordt gebruikt om labels voor dataset en gebieden te beheren. Zie de gids over het [beheren van datasetetiketten](./dataset-api.md) voor meer informatie.

## Volgende stappen

Dit document bevatte een inleiding op de labels voor gegevensgebruik en hun rol binnen het kader voor gegevensbeheer. Raadpleeg de documentatie bij deze handleiding voor meer informatie over het beheren van labels in [!DNL Experience Platform].