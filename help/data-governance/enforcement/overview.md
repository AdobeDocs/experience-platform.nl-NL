---
keywords: Experience Platform;home;populaire onderwerpen;Beleidshandhaving;Automatische handhaving;API-gebaseerde handhaving;gegevensbeheer
solution: Experience Platform
title: Overzicht van beleidshandhaving
topic: guide
description: Zodra de etiketten van het gegevensgebruik op de datasets van Adobe Experience Platform zijn toegepast, en het beleid van het gegevensgebruik voor marketing acties tegen die etiketten is bepaald, staat de mogelijkheden van het Beleid van Gegevens u toe om dat beleid te handhaven en gegevensverrichtingen te verhinderen die beleidsschendingen vormen. Er zijn twee methodes van beleidshandhaving die door de eigenschappen van het Beleid van Gegevens op Platform, op API-Gebaseerde handhaving en automatische handhaving worden verstrekt.
translation-type: tm+mt
source-git-commit: acc4fa59a4808ed9a32c2aaf664039e0d12dc1d8
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Overzicht van beleidshandhaving

Zodra de etiketten van het gegevensgebruik op [!DNL Platform] datasets zijn toegepast, en het beleid van het gegevensgebruik is bepaald voor marketing acties tegen die etiketten, [!DNL Data Governance] mogelijkheden staat u toe om dat beleid te handhaven en gegevensverrichtingen te verhinderen die beleidsschendingen vormen.

Er zijn twee methodes van beleidshandhaving die door [!DNL Data Governance] eigenschappen op [!DNL Platform] worden verstrekt: Op API gebaseerde handhaving en automatische handhaving.

## Op API gebaseerde handhaving

De [!DNL Policy Service] API verstrekt eindpunten die u toestaan om marketing acties tegen datasets of willekeurige combinaties etiketten van het gegevensgebruik te testen om te controleren als om het even welke beleidsschendingen voorkomen. Op basis van de API-reactie kunt u vervolgens protocollen in uw ervaringstoepassing instellen om op de juiste wijze de naleving van het gegevensgebruiksbeleid af te dwingen.

Zie de zelfstudie over op [API gebaseerde handhaving](./api-enforcement.md) voor stappen over hoe te om beleid te evalueren gebruikend API.

## Automatische handhaving

Het Experience Platform maakt gebruik van gegevenslijn, gegevensclassificatie en mogelijkheden voor beleidsbeheer om beleidsovertredingen automatisch te evalueren en aan te geven. Zie het overzicht op [automatische beleidshandhaving](./auto-enforcement.md) voor meer informatie.