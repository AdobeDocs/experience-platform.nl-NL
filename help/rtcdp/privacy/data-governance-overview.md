---
keywords: gegevensbeheer rtcdp;rtcdp gegevensbeheer;beheer van realtime klantgegevensprofiel
title: Overzicht van gegevensbeheer
description: Met gegevensbeheer kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd.
feature: Get Started, Data Governance
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---

# Beheer van gegevens in Real-Time CDP

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP) brengt gegevens van meerdere bedrijfssystemen samen, zodat marketers hun klanten beter kunnen identificeren, begrijpen en betrekken. Deze gegevens zijn mogelijk onderworpen aan gebruiksbeperkingen die zijn gedefinieerd door uw organisatie of wettelijke voorschriften. Daarom is het belangrijk dat Real-Time CDP zich houdt aan het gebruiksbeleid bij het verwerken van uw gegevens.

Met Adobe Experience Platform Data Governance kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. Het speelt een sleutelrol binnen Real-Time CDP, toestaand u om gebruiksbeleid te bepalen, uw gegevens te categoriseren die op dat beleid worden gebaseerd, en beleidsschendingen te controleren wanneer het uitvoeren van bepaalde marketing acties.

Real-Time CDP is gebouwd boven op Adobe Experience Platform en daarom worden de meeste functies voor gegevensbeheer besproken in de documentatie van [!DNL Experience Platform] . Dit document is bedoeld om het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](../../data-governance/home.md) voor [!DNL Experience Platform] aan te vullen, en schetst de eigenschappen van het Bestuur die in Real-Time CDP beschikbaar zijn. De volgende onderwerpen worden behandeld:

* [Gebruikslabels toepassen op uw gegevens](#labels)
* [Beleid voor gegevensgebruik beheren](#policies)
* [Compatibiliteit met gegevensgebruik afdwingen](#enforce)

## Gebruikslabels toepassen op uw gegevens {#labels}

Met gegevensbeheer kunt u gebruikslabels op uw gegevens toepassen, op het niveau van de gegevensset of op het niveau van de gegevensset-velden. Met labels voor gegevensgebruik kunt u gegevens indelen op basis van het gebruiksbeleid dat op die gegevens van toepassing is.

Voor gedetailleerde informatie bij het werken met de etiketten van het gegevensgebruik, zie de [&#x200B; gebruikersgids van de de etiketten van het gegevensgebruik &#x200B;](../../data-governance/labels/overview.md) voor Adobe Experience Platform.

## Marketing-acties voor doelen configureren {#destinations}

U kunt beperkingen voor het gegevensgebruik op een bestemming instellen door marketingacties (ook wel marketinggebruiksgevallen genoemd) voor die bestemming te definiëren. Een marketingactie voor een doel geeft de intentie aan van de gegevens die naar die bestemming worden geëxporteerd.

>[!NOTE]
>
>Voor meer informatie over marketing acties en hun gebruik in het beleid van het gegevensgebruik, zie het [&#x200B; overzicht van het beleid van het gegevensgebruik &#x200B;](../../data-governance/policies/overview.md) in de [!DNL Experience Platform] documentatie.

Door marketingacties op doelen te definiëren, kunt u ervoor zorgen dat profielen of doelgroepen die naar die doelen worden verzonden, voldoen aan het beleid voor gegevensgebruik. Daarom zou u aangewezen marketing acties aan uw bestemmingen moeten toevoegen die op de behoeften van uw organisatie worden gebaseerd om beleidsbeperkingen op activering af te dwingen.

Marketingacties kunnen alleen worden geselecteerd wanneer u een bestemming voor het eerst instelt. Afhankelijk van het type van bestemming u met werkt, zal de kans om marketing acties te vormen op verschillende punten in het opstellingswerkschema verschijnen. Zie de [&#x200B; documentatie van bestemmingen &#x200B;](../destinations/overview.md) voor stappen op hoe te om uw bijzondere bestemming te vormen.

## Beleid voor gegevensgebruik beheren {#policies}

Om gegevensgebruikslabels effectief gegevensnaleving te steunen, moet het beleid van het gegevensgebruik worden bepaald en worden toegelaten. Beleid voor gegevensgebruik is regels die het soort marketingacties beschrijven dat u mag uitvoeren op gegevens in Real-Time CDP of waarvan u een beperking hebt ingesteld. Zie de sectie van het &quot;het gebruiksbeleid van Gegevens&quot;in het [!DNL Experience Platform] [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](../../data-governance/home.md) voor meer informatie.

Adobe Experience Platform biedt verschillende basisbeleidsregels voor veelvoorkomende gebruiksgevallen voor de ervaring van klanten. Dit beleid kan in UI worden bekeken door aan de **[!UICONTROL Policies]** werkruimte te navigeren en het **[!UICONTROL Browse]** lusje te selecteren. Zie de [&#x200B; gids van de beleidsgebruiker &#x200B;](../../data-governance/policies/user-guide.md) in de [!DNL Experience Platform] documentatie voor meer gedetailleerde stappen bij het werken met beleid in UI, met inbegrip van hoe te om uw eigen douanebeleid te maken.

## Compatibiliteit met gegevensgebruik afdwingen {#enforce}

Zodra de gegevens worden geëtiketteerd en het gebruiksbeleid wordt bepaald, kunt u de naleving van het gegevensgebruik met beleid afdwingen. Wanneer het activeren van publiek aan bestemmingen in Real-Time CDP, dwingt het Beleid van Gegevens automatisch gebruiksbeleid af als om het even welke schendingen voorkomen.

Zie het document op [&#x200B; automatische beleidshandhaving &#x200B;](../../data-governance/enforcement/auto-enforcement.md) voor meer informatie.

## Volgende stappen

Nu u aan de belangrijkste eigenschappen van het Beleid van Gegevens op Real-Time CDP bent geïntroduceerd en hoe [!DNL Experience Platform] hen toelaat, gelieve te blijven aan de [&#x200B; documentatie voor het Bestuur van Gegevens op Adobe Experience Platform &#x200B;](../../data-governance/home.md). De documentatie verstrekt overzichten van essentiële concepten van het Beleid van Gegevens, evenals geleidelijke werkschema&#39;s voor het beheren van de etiketten en het beleid van het gegevensgebruik.

De volgende video biedt een overzicht van het beheer van gegevens in Real-Time CDP, inclusief het gebruik van marketinggevallen voor bestemmingen en voorbeeldworkflows voor verschillende scenario&#39;s:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
