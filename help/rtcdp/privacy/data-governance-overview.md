---
keywords: gegevensbeheer rtcdp;rtcdp gegevensbeheer;beheer van realtime klantgegevensprofiel
title: Overzicht van gegevensbeheer
seo-title: Data Governance in Real-time Customer Data Platform
description: 'Met gegevensbeheer kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. '
seo-description: Data Governance allows you to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data use.
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Gegevensbeheer in real time CDP

[!DNL Real-time Customer Data Platform] (CDP in real time) brengt gegevens van veelvoudige ondernemingssystemen samen, die marketers toestaan om, hun klanten beter te identificeren te begrijpen en te betrekken. Deze gegevens zijn mogelijk onderworpen aan gebruiksbeperkingen die zijn gedefinieerd door uw organisatie of wettelijke voorschriften. Daarom is het belangrijk om ervoor te zorgen dat CDP in real time met gebruiksbeleid wanneer het behandelen van uw gegevens compatibel is.

Met Adobe Experience Platform Data Governance kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een zeer belangrijke rol binnen CDP In real time, toestaand u om gebruiksbeleid te bepalen, uw gegevens te categoriseren die op dat beleid worden gebaseerd, en beleidsschendingen te controleren wanneer het uitvoeren van bepaalde marketing acties.

CDP in real time wordt voortgebouwd bovenop Adobe Experience Platform, en daarom worden de meeste mogelijkheden van het Beleid van Gegevens behandeld in [!DNL Experience Platform] documentatie. Dit document is bedoeld als aanvulling op het [Overzicht van gegevensbeheer](../../data-governance/home.md) for [!DNL Experience Platform], en schetst de eigenschappen van het Bestuur die in Echt - tijd CDP beschikbaar zijn. De volgende onderwerpen worden behandeld:

* [Gebruikslabels toepassen op uw gegevens](#labels)
* [Beleid voor gegevensgebruik beheren](#policies)
* [Compatibiliteit met gegevensgebruik afdwingen](#enforce)

## Gebruikslabels toepassen op uw gegevens {#labels}

Met gegevensbeheer kunt u gebruikslabels op uw gegevens toepassen, op het niveau van de gegevensset of op het niveau van de gegevensset-velden. Met labels voor gegevensgebruik kunt u gegevens indelen op basis van het gebruiksbeleid dat op die gegevens van toepassing is.

Voor gedetailleerde informatie over het werken met labels voor gegevensgebruik raadpleegt u de [gebruikershandleiding voor gegevensgebruikslabels](../../data-governance/labels/overview.md) voor Adobe Experience Platform.

## Marketing-acties voor doelen configureren {#destinations}

U kunt beperkingen voor het gegevensgebruik op een bestemming instellen door marketingacties (ook wel marketinggebruiksgevallen genoemd) voor die bestemming te definiëren. Een marketingactie voor een doel geeft de intentie aan van de gegevens die naar die bestemming worden geëxporteerd.

>[!NOTE]
>
>Voor meer informatie over marketingacties en het gebruik ervan in het beleid voor gegevensgebruik raadpleegt u de [overzicht van beleidsregels voor gegevensgebruik](../../data-governance/policies/overview.md) in de [!DNL Experience Platform] documentatie.

Het bepalen van marketing acties op bestemmingen staat u toe om ervoor te zorgen dat om het even welke profielen of segmenten die naar die bestemmingen worden verzonden volgzaam met het beleid van het gegevensgebruik zijn. Daarom zou u aangewezen marketing acties aan uw bestemmingen moeten toevoegen die op de behoeften van uw organisatie worden gebaseerd om beleidsbeperkingen op activering af te dwingen.

Marketingacties kunnen alleen worden geselecteerd wanneer u een bestemming voor het eerst instelt. Afhankelijk van het type van bestemming u met werkt, zal de kans om marketing acties te vormen op verschillende punten in het opstellingswerkschema verschijnen. Zie de [documentatie voor doelen](../destinations/overview.md) voor stappen op hoe te om uw bijzondere bestemming te vormen.

## Beleid voor gegevensgebruik beheren {#policies}

Om gegevensgebruikslabels effectief gegevensnaleving te steunen, moet het beleid van het gegevensgebruik worden bepaald en worden toegelaten. Het beleid van het gebruik van gegevens is regels die de soorten marketing acties beschrijven die u aan, of beperkt van, op gegevens binnen CDP in real time mag uitvoeren. Zie de sectie &quot;Beleid voor gegevensgebruik&quot; in de [!DNL Experience Platform] [Overzicht van gegevensbeheer](../../data-governance/home.md) voor meer informatie .

Adobe Experience Platform biedt verschillende basisbeleidsregels voor veelvoorkomende gebruiksgevallen voor de ervaring van klanten. Dit beleid kan in UI worden bekeken door aan **[!UICONTROL Policies]** werkruimte en het selecteren van de **[!UICONTROL Browse]** tab. Zie de [beleidsgebruikershandleiding](../../data-governance/policies/user-guide.md) in de [!DNL Experience Platform] documentatie voor meer gedetailleerde stappen over het werken met beleid in UI, met inbegrip van hoe te om uw eigen douanebeleid te maken.

## Compatibiliteit met gegevensgebruik afdwingen {#enforce}

Zodra de gegevens worden geëtiketteerd en het gebruiksbeleid wordt bepaald, kunt u de naleving van het gegevensgebruik met beleid afdwingen. Wanneer het activeren van publiekssegmenten aan bestemmingen in Echt - tijd CDP, dwingt het Beleid van Gegevens automatisch gebruiksbeleid af als om het even welke schendingen voorkomen.

Document weergeven op [automatische beleidshandhaving](../../data-governance/enforcement/auto-enforcement.md) voor meer informatie .

## Volgende stappen

Nu u aan de belangrijkste eigenschappen van het Beleid van Gegevens op Real-time CDP en hoe bent geïntroduceerd [!DNL Experience Platform] zij kunnen [documentatie voor gegevensbeheer op Adobe Experience Platform](../../data-governance/home.md). De documentatie verstrekt overzichten van essentiële concepten van het Beleid van Gegevens, evenals geleidelijke werkschema&#39;s voor het beheren van de etiketten en het beleid van het gegevensgebruik.

De volgende video verstrekt een overzicht van de Governance van Gegevens in Echt - tijd CDP, met inbegrip van het gebruik van marketing gebruiksgevallen op bestemmingen en voorbeeldwerkschema&#39;s voor verschillende scenario&#39;s:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
