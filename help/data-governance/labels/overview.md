---
keywords: Experience Platform;home;popular topics;data governance;data usage label api;policy service api;data usage labels overview
solution: Experience Platform
title: Overzicht van labels voor gegevensgebruik
topic: labels
description: Met Adobe Experience Platform Data Governance kunt u gegevensgebruikslabels toepassen op gegevenssets en velden, waarbij elk veld wordt ingedeeld volgens het beleid voor het gebruik van verwante gegevens. Dit document biedt een overzicht van labels voor gegevensgebruik in Experience Platform.
translation-type: tm+mt
source-git-commit: e680191d495e4c33baa8242d40a15b9124eec8cd
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---


# Overzicht van labels voor gegevensgebruik

Met Adobe Experience Platform [!DNL Data Governance] kunt u labels voor gegevensgebruik toepassen op gegevenssets en velden, waarbij elke tag wordt ingedeeld op basis van het beleid voor het gegevensgebruik.

Dit document biedt een overzicht van labels voor gegevensgebruik in [!DNL Experience Platform]. Voordat u deze handleiding leest, raadpleegt u het [Overzicht gegevensbeheer](../home.md) voor een robuustere inleiding op het gegevensbeheerkader.

## Werken met labels voor gegevensgebruik

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken moedigen etiketteringsgegevens aan zodra het in [!DNL Experience Platform] wordt opgenomen, of zodra de gegevens voor gebruik in [!DNL Platform] beschikbaar worden.

De etiketten van het gebruik van gegevens die op het datasetniveau worden toegepast worden verspreid aan alle gebieden binnen de dataset. De etiketten kunnen ook direct op individuele gebieden (kolomkopballen) in een dataset, zonder propagatie worden toegepast.

[!DNL Platform] biedt verschillende &#39;core&#39; labels voor gegevensgebruik buiten de box, die een groot aantal gemeenschappelijke beperkingen bestrijken die van toepassing zijn op gegevensbeheer. Voor meer informatie over deze etiketten en het gebruiksbeleid zij vertegenwoordigen, zie de gids op [de etiketten van het kerngegevensgebruik](reference.md).

Naast de labels die door Adobe worden verschaft, kunt u ook uw eigen aangepaste labels voor uw organisatie definiëren. Zie de sectie over [het beheren van labels](#manage-labels) voor meer informatie.

## Labelovererving voor publiekssegmenten

Alle publiekssegmenten die door [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) worden gecreeerd erven de gebruiksetiketten van hun overeenkomstige datasets. Dit staat Experience Platform toe om de automatische handhaving van het gegevensgebruiksbeleid te verstrekken wanneer het activeren van segmenten aan bestemmingen.

Naast het erven van dataset-vlakke etiketten, erven de segmenten alle gebied-vlakke etiketten van hun bijbehorende datasets door gebrek. Daarom kunt u gemakkelijker identificeren welke attributen van uw segmenten zouden moeten worden uitgesloten en hen verhinderen etiketten van uitgesloten gebieden over te nemen.

Voor meer informatie over hoe de automatische handhaving in Platform werkt, zie het overzicht op [automatische beleidshandhaving](../enforcement/auto-enforcement.md).

### Overerving van Adobe Audience Manager Data Export Controls

[!DNL Experience Platform] kan segmenten delen met Adobe Audience Manager. Om het even welke Controles van de Uitvoer van Gegevens die op de segmenten van de Audience Manager zijn toegepast worden vertaald in gelijkwaardige etiketten en marketing acties die door [!DNL Experience Platform] [!DNL Data Governance] worden erkend.

Voor een verwijzing op hoe de specifieke Controles van de Uitvoer van Gegevens aan de etiketten van het gegevensgebruik in [!DNL Platform] in kaart brengen, gelieve te verwijzen naar [de documentatie van de Audience Manager](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Labels voor gegevensgebruik beheren in [!DNL Experience Platform] {#manage-labels}

U kunt labels voor gegevensgebruik beheren met behulp van [!DNL Experience Platform] API&#39;s of de gebruikersinterface. Raadpleeg de onderstaande subsecties voor meer informatie over elke subsectie.

### De gebruikersinterface gebruiken

Met de **[!UICONTROL beleidsregels]**-werkruimte in de [!DNL Experience Platform]-gebruikersinterface kunt u kern- en aangepaste labels voor uw organisatie weergeven en beheren. Met de werkruimte **[!DNL Datasets]** kunt u labels toepassen op gegevenssets en velden. Raadpleeg voor meer informatie de [handleiding voor labelgebruikers](user-guide.md).

### API&#39;s gebruiken

Met het `/labels`-eindpunt in de [Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) kunt u gegevensgebruikslabels programmatisch beheren, inclusief het maken van aangepaste labels. Verwijs naar [etiketeindpuntgids](../api/labels.md) voor meer informatie.

De [Dataset Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) wordt gebruikt om labels voor gegevensset en velden te beheren. Zie de gids op [het beheren van datasetetiketten](./dataset-api.md) voor meer informatie.

## Volgende stappen

Dit document bevatte een inleiding op de labels voor gegevensgebruik en hun rol binnen het kader voor gegevensbeheer. Raadpleeg de documentatie bij deze handleiding voor meer informatie over het beheren van labels in [!DNL Experience Platform].