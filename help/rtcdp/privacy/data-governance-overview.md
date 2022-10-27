---
keywords: gegevensbeheer rtcdp;rtcdp gegevensbeheer;beheer van realtime klantgegevensprofiel
title: Overzicht van gegevensbeheer
description: Met gegevensbeheer kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd.
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 1%

---

# Beheer van gegevens in Real-Time CDP

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP) brengt gegevens van meerdere bedrijfssystemen samen, waardoor marketers hun klanten beter kunnen identificeren, begrijpen en betrekken. Deze gegevens zijn mogelijk onderworpen aan gebruiksbeperkingen die zijn gedefinieerd door uw organisatie of wettelijke voorschriften. Daarom is het belangrijk dat Real-Time CDP zich houdt aan het gebruiksbeleid bij het verwerken van uw gegevens.

Met Adobe Experience Platform Data Governance kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een sleutelrol binnen Real-Time CDP, toestaand u om gebruiksbeleid te bepalen, uw gegevens te categoriseren die op dat beleid worden gebaseerd, en beleidsschendingen te controleren wanneer het uitvoeren van bepaalde marketing acties.

Real-Time CDP is gebouwd op Adobe Experience Platform en daarom wordt het grootste deel van de mogelijkheden voor gegevensbeheer opgenomen in de [!DNL Experience Platform] documentatie. Dit document is bedoeld als aanvulling op het [Overzicht van gegevensbeheer](../../data-governance/home.md) for [!DNL Experience Platform]en geeft een overzicht van de bestuursfuncties die beschikbaar zijn in Real-Time CDP. De volgende onderwerpen worden behandeld:

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

Om gegevensgebruikslabels effectief gegevensnaleving te steunen, moet het beleid van het gegevensgebruik worden bepaald en worden toegelaten. Beleid voor gegevensgebruik is regels die het soort marketingacties beschrijven dat u mag uitvoeren op gegevens in Real-Time CDP of waarvan u een beperking hebt ingesteld. Zie de sectie &quot;Beleid voor gegevensgebruik&quot; in de [!DNL Experience Platform] [Overzicht van gegevensbeheer](../../data-governance/home.md) voor meer informatie .

Adobe Experience Platform biedt verschillende basisbeleidsregels voor veelvoorkomende gebruiksgevallen voor de ervaring van klanten. Dit beleid kan in UI worden bekeken door aan **[!UICONTROL Policies]** werkruimte en het selecteren van de **[!UICONTROL Browse]** tab. Zie de [beleidsgebruikershandleiding](../../data-governance/policies/user-guide.md) in de [!DNL Experience Platform] documentatie voor meer gedetailleerde stappen over het werken met beleid in UI, met inbegrip van hoe te om uw eigen douanebeleid te maken.

## Compatibiliteit met gegevensgebruik afdwingen {#enforce}

Zodra de gegevens worden geëtiketteerd en het gebruiksbeleid wordt bepaald, kunt u de naleving van het gegevensgebruik met beleid afdwingen. Wanneer het activeren van publiekssegmenten aan bestemmingen in Real-Time CDP, dwingt het Beleid van Gegevens automatisch gebruiksbeleid af als om het even welke schendingen voorkomen.

Document weergeven op [automatische beleidshandhaving](../../data-governance/enforcement/auto-enforcement.md) voor meer informatie .

## Volgende stappen

Nu u de belangrijkste functies voor gegevensbeheer op Real-Time CDP hebt geïntroduceerd en leert u hoe [!DNL Experience Platform] zij kunnen [documentatie voor gegevensbeheer op Adobe Experience Platform](../../data-governance/home.md). De documentatie verstrekt overzichten van essentiële concepten van het Beleid van Gegevens, evenals geleidelijke werkschema&#39;s voor het beheren van de etiketten en het beleid van het gegevensgebruik.

De volgende video biedt een overzicht van het beheer van gegevens in Real-Time CDP, inclusief het gebruik van marketinggevallen voor bestemmingen en voorbeeldworkflows voor verschillende scenario&#39;s:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
