---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Overzicht van beleidshandhaving
topic: enforcement
description: Zodra de etiketten van het gegevensgebruik op de datasets van Adobe Experience Platform zijn toegepast, en het beleid van het gegevensgebruik voor marketing acties tegen die etiketten is bepaald, staat de mogelijkheden van het Beleid van Gegevens u toe om dat beleid te handhaven en gegevensverrichtingen te verhinderen die beleidsschendingen vormen. Er zijn twee methodes van beleidshandhaving die door de eigenschappen van het Beleid van Gegevens op Platform, op API-Gebaseerde handhaving en automatische handhaving worden verstrekt.
translation-type: tm+mt
source-git-commit: 83f1392ffab3571ebd91325123fbe7095ad59e28
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# Overzicht van beleidshandhaving

Zodra de etiketten van het gegevensgebruik op [!DNL Platform] [!DNL Data Governance] datasets zijn toegepast, en het beleid van het gegevensgebruik is bepaald voor marketing acties tegen die etiketten, staan de mogelijkheden u toe om dat beleid te handhaven en gegevensverrichtingen te verhinderen die beleidsschendingen vormen.

Er zijn twee methodes van beleidshandhaving die door [!DNL Data Governance] eigenschappen op worden verstrekt [!DNL Platform]: Op API gebaseerde handhaving en automatische handhaving.

## Op API gebaseerde handhaving

De [!DNL Policy Service] API verstrekt eindpunten die u toestaan om marketing acties tegen datasets of willekeurige combinaties etiketten van het gegevensgebruik te testen om te controleren of om het even welke beleidsschendingen voorkomen. Op basis van de API-reactie kunt u vervolgens protocollen in uw ervaringstoepassing instellen om op de juiste wijze de naleving van het gegevensgebruiksbeleid af te dwingen.

Zie de zelfstudie over [beleidshandhaving](api-enforcement.md) voor stappen over het evalueren van beleid met behulp van de API.

## Automatische handhaving

Bepaalde toepassingen die bovenop [!DNL Experience Platform] (zoals [!DNL Real-time Customer Data Platform]) worden gebouwd verstrekken automatische handhaving voor het beleid van het gegevensgebruik. Elke toepassing handhaaft zijn eigen methode om beleidsschendingen te onderzoeken en stappen te verstrekken om kwesties op te lossen.

De automatische beleidshandhaving in Realtime CDP hefboomwerkingen gegevenslijn, gegevensclassificatie, en de mogelijkheden van het beleidsbeheer om beleidsschendingen te evalueren en te oppervlakte. Raadpleeg het [Real-time CDP-overzicht](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance) voor gegevensbeheer voor meer informatie.