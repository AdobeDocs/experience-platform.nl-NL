---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zelfstudies over gegevensbeheer en privacy
topic: tutorial
type: Tutorial
description: Dit document biedt een overzicht van de verschillende beschikbare zelfstudies met betrekking tot Adobe Experience Platform Data Governance en Adobe Experience Platform Privacy Service.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---


# [!DNL Data Governance] en [!DNL Privacy] Tutorials

Met Adobe Experience Platform Data Governance kunt u gegevensgebruikslabels toepassen op gegevenssets en velden, waarbij elke code wordt ingedeeld op basis van het beleid voor het gebruik van verwante gegevens, en kunt u overtredingen van het beleid beoordelen wanneer bepaalde handelingen op die gegevenssets en/of velden worden uitgevoerd. Voordat u aan de slag gaat met de zelfstudies die in dit document worden vermeld, raadpleegt u het [[!DNL Data Governance] overzicht](../data-governance/home.md) voor een robuustere introductie van het framework.

Adobe Experience Platform [!DNL Privacy Service] biedt een RESTful-API en -gebruikersinterface waarmee u privacy- en compatibiliteitsverzoeken op verschillende oplossingen kunt coördineren. Als u meer informatie wilt, leest u eerst het overzicht [van de](../privacy-service/home.md)Privacy Service.

## Labels voor gegevensgebruik toevoegen

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het in wordt opgenomen [!DNL Experience Platform], of zodra de gegevens voor gebruik in [!DNL Platform]. De etiketten van het gebruik van gegevens die op het datasetniveau worden toegepast worden verspreid aan alle gebieden binnen de dataset. De etiketten kunnen ook direct op individuele gebieden (kolomkopballen) in een dataset, zonder propagatie worden toegepast. Ga naar het overzicht [van de labels voor](../data-governance/labels/overview.md)gegevensgebruik voor informatie over het toepassen van labels voor gegevensgebruik.

## Beleid voor gegevensgebruik maken

Met de [!DNL Policy Service] API kunt u beleid voor gegevensgebruik maken en beheren om te bepalen welke marketingacties kunnen worden uitgevoerd tegen gegevens die bepaalde gebruikslabels bevatten. Lees eerst het overzicht [van het beleid voor](../data-governance/policies/overview.md)gegevensgebruik.

## Beleid voor gegevensgebruik afdwingen

Zodra u gebruiksetiketten voor uw gegevens hebt toegevoegd, en beleid voor marketing acties tegen die etiketten gecreeerd, kunt u gebruiken [!DNL Policy Service API] om te evalueren of een marketing actie een beleidsschending wanneer uitgevoerd op een dataset of een willekeurige groep gebruiksetiketten vormt. Vervolgens kunt u uw eigen interne protocollen instellen om beleidsovertredingen af te handelen op basis van de API-reactie. Ga om aan de slag te gaan naar het overzicht [van de](../data-governance/enforcement/overview.md)beleidshandhaving.

## Compatibiliteit met gegevensgebruik afdwingen voor een publiekssegment

De segmenten die voor gebruik in worden toegelaten [!DNL Real-time Customer Profile] bevatten een identiteitskaart van het fusiebeleid binnen hun segmentdefinitie. Dit samenvoegbeleid bevat informatie over welke datasets in het segment moeten worden omvat, die beurtelings om het even welke toepasselijke etiketten van het gegevensgebruik bevatten. Voor specifieke stappen die het afdwingen van de naleving van het gegevensgebruik voor een publiekssegment, gelieve te volgen de de handhavingszelfstudie van het [gegevensgebruik voor segmenten](../segmentation/tutorials/governance.md).

## Aan de slag met [!DNL Privacy Service]

[!DNL Privacy Service] biedt een RESTful-API en -gebruikersinterface waarmee u de persoonlijke gegevens van uw betrokkenen (klanten) in Adobe Experience Cloud-toepassingen kunt beheren. [!DNL Privacy Service] voorziet ook een centraal controle en registrerenmechanisme dat u toestaat om tot de status en de resultaten van banen toegang te hebben die [!DNL Experience Cloud] toepassingen impliceren. Voor instructies die tonen hoe te om [!DNL Privacy Service] banen tot stand te brengen en te controleren, volg de stappen die in de de ontwikkelaarsgids [van de](../privacy-service/api/getting-started.md) Privacy Service of de [gebruikershandleiding](../privacy-service/ui/overview.md)van de Privacy Service worden verstrekt.