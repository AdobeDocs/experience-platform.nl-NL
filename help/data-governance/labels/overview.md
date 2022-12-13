---
keywords: Experience Platform;home;populaire onderwerpen;gegevensbeheer;label api voor gegevensgebruik;beleidservice-api;overzicht van labels voor gegevensgebruik
solution: Experience Platform
title: Overzicht van labels voor gegevensgebruik
topic-legacy: labels
description: Leer hoe labels voor gegevensgebruik worden gebruikt om naleving van gegevensbeheer in Adobe Experience Platform af te dwingen.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 7e4c2ef8089276829604c9d8a8dd20a122b18c7a
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# Overzicht van labels voor gegevensgebruik

Met Adobe Experience Platform kunt u gegevensgebruikslabels toepassen op gegevenssets en velden, waarbij elke tag wordt ingedeeld op basis van verwante [beleid inzake gegevensbeheer](../policies/overview.md) en [toegangsbeheerbeleid](../../access-control/abac/ui/policies.md).

Dit document biedt een overzicht van labels voor gegevensgebruik in [!DNL Experience Platform].

## Werken met labels voor gegevensgebruik

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het beleid dat van toepassing is op die gegevens. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het wordt opgenomen in [!DNL Experience Platform]of zodra gegevens beschikbaar zijn voor gebruik in [!DNL Platform].

De etiketten van het gebruik van gegevens die op het datasetniveau worden toegepast worden verspreid aan alle gebieden binnen de dataset. De etiketten kunnen ook direct op individuele gebieden (kolomkopballen) in een dataset, zonder propagatie worden toegepast.

[!DNL Platform] biedt verschillende &#39;core&#39; labels voor gegevensgebruik buiten de box, die een groot aantal gemeenschappelijke beperkingen bestrijken die van toepassing zijn op gegevensbeheer. Zie de handleiding voor meer informatie over deze labels en het beleid voor governance dat ze vertegenwoordigen [basislabels voor gegevensgebruik](reference.md).

Naast de labels die door Adobe worden verschaft, kunt u ook uw eigen aangepaste labels voor uw organisatie definiëren. Zie de sectie over [beheren, labels](#manage-labels) voor meer informatie .

## Labelovererving voor publiekssegmenten

Alle publiekssegmenten gemaakt door [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) erven de gebruiksetiketten van hun overeenkomstige datasets. Dit staat Experience Platform toe om automatische beleidshandhaving te verstrekken wanneer het activeren van segmenten aan bestemmingen.

Naast het erven van dataset-vlakke etiketten, erven de segmenten alle gebied-vlakke etiketten van hun bijbehorende datasets door gebrek. Daarom kunt u gemakkelijker identificeren welke attributen van uw segmenten zouden moeten worden uitgesloten en hen verhinderen etiketten van uitgesloten gebieden over te nemen.

Zie voor meer informatie over de werking van automatische handhaving in Platform het overzicht over [automatische beleidshandhaving](../enforcement/auto-enforcement.md).

### Overerving van Adobe Audience Manager Data Export Controls

[!DNL Experience Platform] kan segmenten delen met Adobe Audience Manager. Om het even welke Controles van de Uitvoer van Gegevens die op de segmenten van de Audience Manager zijn toegepast worden vertaald in gelijkwaardige etiketten en marketing acties die door worden erkend [!DNL Experience Platform] Gegevensbeheer.

Voor een verwijzing naar hoe de specifieke Controles van de Uitvoer van Gegevens aan de etiketten van het gegevensgebruik in kaart brengen [!DNL Platform], gelieve de [Documentatie Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Labels voor gegevensgebruik beheren in [!DNL Experience Platform] {#manage-labels}

U kunt gegevensgebruikslabels beheren met [!DNL Experience Platform] API&#39;s of de gebruikersinterface. Raadpleeg de onderstaande subsecties voor meer informatie over elke subsectie.

### De gebruikersinterface gebruiken

De **[!UICONTROL Policies]** werkruimte in de [!DNL Experience Platform] UI staat u toe om kern en douanelabels voor uw organisatie te bekijken en te beheren. U kunt de **[!UICONTROL Schemas]** werkruimte naar [labels toepassen op uw XDM-schema&#39;s (Experience Data Model)](../../xdm/tutorials/labels.md)of u kunt de **[!DNL Datasets]** werkruimte naar [labels toepassen op gegevenssets](./user-guide.md) in plaats daarvan.

>[!NOTE]
>
>Het toepassen van labels op gegevenssetniveau wordt alleen ondersteund voor gevallen waarin gegevens worden beheerd. Als u probeert om toegangsbeleid voor de gegevens tot stand te brengen, moet u etiketten op het schema toepassen dat de dataset op gebaseerd is. Zie het overzicht op [attribuut-based toegangsbeheer](../../access-control/abac/overview.md) voor meer informatie .

### API&#39;s gebruiken

De `/labels` in de [Beleidsservice-API](https://www.adobe.io/experience-platform-apis/references/policy-service/) Hiermee kunt u gegevensgebruikslabels programmatisch beheren, inclusief het maken van aangepaste labels. Zie de [eindhulplijn voor labels](../api/labels.md) voor meer informatie .

De [Dataset-service-API](https://www.adobe.io/experience-platform-apis/references/dataset-service/) wordt gebruikt om etiketten voor dataset en gebieden te beheren. Zie de handleiding op [gegevenssetlabels beheren](./dataset-api.md) voor meer informatie .

>[!NOTE]
>
>Het toepassen van labels op gegevenssetniveau wordt alleen ondersteund voor gevallen waarin gegevens worden beheerd. Als u probeert toegangsbeleid voor de gegevens tot stand te brengen, moet u [labels toepassen op het schema](../../xdm/tutorials/labels.md) dat de gegevensset op die gegevens is gebaseerd. Zie het overzicht op [attribuut-based toegangsbeheer](../../access-control/abac/overview.md) voor meer informatie .

## Volgende stappen

Dit document bevatte een inleiding op de labels voor gegevensgebruik en hun rol binnen het kader voor gegevensbeheer. Raadpleeg de documentatie bij deze handleiding voor meer informatie over het beheren van labels in [!DNL Experience Platform].
