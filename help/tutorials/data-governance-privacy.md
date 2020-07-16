---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zelfstudies over gegevensbeheer en privacy
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# [!DNL Data Governance] en [!DNL Privacy] zelfstudies

[!DNL Data Usage Labeling and Enforcement] (DULE) is het kernmechanisme van Adobe Experience Platform [!DNL Data Governanc]e. De eigenschappen DULE laten u toe om de etiketten van het gegevensgebruik op datasets en gebieden toe te passen, die elk volgens het verwante beleid van het gegevensgebruik categoriseren. Voordat u aan de slag gaat met labels, raadpleegt u het overzicht [van](../data-governance/home.md) gegevensbeheer voor een robuustere inleiding op het DULE-framework binnen [!DNL Platform].

Adobe Experience Platform [!DNL Privacy Service] verstrekt een RESTful API en gebruikersinterface die u toestaan om privacy en nalevingsverzoeken over diverse oplossingen te coördineren. Als u meer informatie wilt, leest u eerst het overzicht [van de](../privacy-service/home.md)Privacy Service.

## Labels voor gegevensgebruik toevoegen

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het in wordt opgenomen [!DNL Experience Platform], of zodra de gegevens voor gebruik in [!DNL Platform]. De etiketten van het gebruik van gegevens die op het datasetniveau worden toegepast worden verspreid aan alle gebieden binnen de dataset. De etiketten kunnen ook direct op individuele gebieden (kolomkopballen) in een dataset, zonder propagatie worden toegepast. Ga naar het overzicht [van de labels voor](../data-governance/labels/overview.md)gegevensgebruik voor informatie over het toepassen van labels voor gegevensgebruik.

## Beleid voor gegevensgebruik maken

DULE [!DNL Policy Service] API staat u toe om DULE beleid tot stand te brengen en te beheren om te bepalen welke marketing acties tegen gegevens kunnen worden genomen die bepaalde etiketten DULE bevatten. Lees eerst het overzicht [van het beleid voor](../data-governance/policies/overview.md)gegevensgebruik.

## Beleid voor gegevensgebruik afdwingen

Zodra u de etiketten van de Etikettering en van het Gebruik van Gegevens (DULE) voor uw gegevens hebt gecreeerd, en DULE beleid voor marketing acties tegen die etiketten hebt gecreeerd, kunt u DULE [!DNL Policy Service] API gebruiken om te evalueren of een marketing actie die op een dataset, of een willekeurige groep etiketten van DULE wordt uitgevoerd, een beleidsschending vormt. Vervolgens kunt u uw eigen interne protocollen instellen om beleidsovertredingen af te handelen op basis van de API-reactie. Ga om aan de slag te gaan naar het overzicht [van de](../data-governance/enforcement/overview.md)beleidshandhaving.

## Compatibiliteit met gegevensgebruik afdwingen voor een publiekssegment

De segmenten die voor gebruik in worden toegelaten [!DNL Real-time Customer Profile] bevatten een identiteitskaart van het fusiebeleid binnen hun segmentdefinitie. Dit samenvoegbeleid bevat informatie over welke datasets in het segment moeten worden omvat, die beurtelings om het even welke toepasselijke etiketten van het gegevensgebruik bevatten. Voor specifieke stappen die het afdwingen van de naleving van het gegevensgebruik voor een publiekssegment, gelieve te volgen de de handhavingszelfstudie van het [gegevensgebruik voor segmenten](../segmentation/tutorials/governance.md).

## Get started with [!DNL Privacy Service]

[!DNL Privacy Service] biedt een RESTful-API en -gebruikersinterface waarmee u de persoonlijke gegevens van uw betrokkenen (klanten) kunt beheren in alle Adobe Experience Cloud-toepassingen. [!DNL Privacy Service] voorziet ook een centraal controle en registrerenmechanisme dat u toestaat om tot de status en de resultaten van banen toegang te hebben die [!DNL Experience Cloud] toepassingen impliceren. Voor instructies die tonen hoe te om [!DNL Privacy Service] banen tot stand te brengen en te controleren, volg de stappen die in de de ontwikkelaarsgids [van de](../privacy-service/api/getting-started.md) Privacy Service of de [gebruikershandleiding](../privacy-service/ui/overview.md)van de Privacy Service worden verstrekt.