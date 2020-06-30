---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van beleidshandhaving
topic: enforcement
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Overzicht van beleidshandhaving

Zodra de etiketten van het gegevensgebruik op [!DNL Platform] [!DNL Data Governance] datasets zijn toegepast, en het beleid van het gegevensgebruik is bepaald voor marketing acties tegen die etiketten, staan de mogelijkheden u toe om dat beleid te handhaven en gegevensverrichtingen te verhinderen die beleidsschendingen vormen.

Er zijn twee methodes van beleidshandhaving die door [!DNL Data Governance] eigenschappen op worden verstrekt [!DNL Platform]: **Op API gebaseerde handhaving** en **automatische handhaving**.

## Op API gebaseerde handhaving

De [!DNL Policy Service] API verstrekt eindpunten die u toestaan om marketing acties tegen datasets of willekeurige combinaties etiketten van het gegevensgebruik te testen om te controleren of om het even welke beleidsschendingen voorkomen. Op basis van de API-reactie kunt u vervolgens protocollen in uw ervaringstoepassing instellen om op de juiste wijze de naleving van het gegevensgebruiksbeleid af te dwingen.

Zie de zelfstudie over [beleidshandhaving](api-enforcement.md) voor stappen over het evalueren van beleid met behulp van de API.

## Automatische handhaving

Bepaalde toepassingen die bovenop [!DNL Experience Platform] (zoals [!DNL Real-time Customer Data Platform]) worden gebouwd verstrekken automatische handhaving voor het beleid van het gegevensgebruik. Elke toepassing handhaaft zijn eigen methode om beleidsschendingen te onderzoeken en stappen te verstrekken om kwesties op te lossen.

Raadpleeg de documentatie bij de [!DNL Platform]toepassing die u gebruikt voor meer informatie over de automatische handhaving van het gegevensgebruiksbeleid. Voor informatie over automatische beleidshandhaving in Echt - tijd CDP, gelieve te verwijzen naar het overzicht [van het Beheer van Gegevens CDP in](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)real time.