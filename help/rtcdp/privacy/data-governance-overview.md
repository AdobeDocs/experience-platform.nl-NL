---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance
title: Overzicht van gegevensbeheer
seo-title: Gegevensbeheer in Real-time Customer Data Platform
description: 'Met gegevensbeheer kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. '
seo-description: 'Met gegevensbeheer kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. '
translation-type: tm+mt
source-git-commit: e680191d495e4c33baa8242d40a15b9124eec8cd
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---


# [!DNL Data Governance] in Real-time CDP

[!DNL Real-time Customer Data Platform] (CDP in real time) brengt gegevens van veelvoudige ondernemingssystemen samen, toestaand marketers om, hun klanten beter te identificeren te begrijpen en in dienst te nemen. Deze gegevens zijn mogelijk onderworpen aan gebruiksbeperkingen die zijn gedefinieerd door uw organisatie of wettelijke voorschriften. Daarom is het belangrijk om ervoor te zorgen dat CDP in real time met gebruiksbeleid wanneer het behandelen van uw gegevens compatibel is.

Met Adobe Experience Platform [!DNL Data Governance] kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een zeer belangrijke rol binnen CDP In real time, toestaand u om gebruiksbeleid te bepalen, uw gegevens te categoriseren die op dat beleid worden gebaseerd, en beleidsschendingen te controleren wanneer het uitvoeren van bepaalde marketing acties.

CDP in real time wordt gebouwd bovenop Adobe Experience Platform, en daarom worden de meerderheid van [!DNL Data Governance] mogelijkheden behandeld in de [!DNL Experience Platform] documentatie. Dit document is bedoeld als aanvulling op het [Data Governance-overzicht](../../data-governance/home.md) voor [!DNL Experience Platform], en schetst de eigenschappen van de Governance die in real time CDP beschikbaar zijn. De volgende onderwerpen worden behandeld:

* [Gebruikslabels toepassen op uw gegevens](#labels)
* [Beleid voor gegevensgebruik beheren](#policies)
* [Compatibiliteit met gegevensgebruik afdwingen](#enforce)

## Gebruikslabels toepassen op uw gegevens {#labels}

[!DNL Data Governance] staat u toe om gebruiksetiketten op uw gegevens, of op de dataset of dataset-gebied niveau toe te passen. Met labels voor gegevensgebruik kunt u gegevens indelen op basis van het gebruiksbeleid dat op die gegevens van toepassing is.

Raadpleeg [de gebruikershandleiding ](../../data-governance/labels/overview.md) voor gegevensgebruikslabels voor meer informatie over het werken met labels voor gegevensgebruik voor Adobe Experience Platform.

## Gebruiksgevallen voor marketingdoeleinden configureren voor doelen {#destinations}

U kunt beperkingen voor het gegevensgebruik op een bestemming instellen door gevallen van marketinggebruik (ook wel marketingacties genoemd) voor die bestemming te definiëren. Een marketinggeval voor een bestemming geeft de intentie aan van de gegevens die naar die bestemming worden geëxporteerd.

>[!NOTE]
>
>Zie [Overzicht van beleidsregels voor gegevensgebruik](../../data-governance/policies/overview.md) in de [!DNL Experience Platform]-documentatie voor meer informatie over marketingacties en het gebruik ervan in beleidsregels voor gegevensgebruik.

Het bepalen van marketing gebruiksgevallen op bestemmingen staat u toe om ervoor te zorgen dat om het even welke profielen of segmenten die naar die bestemmingen worden verzonden volgzaam met het beleid van het gegevensgebruik zijn. Daarom zou u aangewezen gevallen van het marketinggebruik aan uw bestemmingen moeten toevoegen die op de behoeften van uw organisatie worden gebaseerd om beleidsbeperkingen op activering af te dwingen.

Gebruiksscenario&#39;s voor marketingdoeleinden kunnen alleen worden geselecteerd wanneer u een bestemming voor het eerst instelt. Afhankelijk van het type van bestemming u met werkt, zal de kans om de gevallen van het marketinggebruik te vormen op verschillende punten in het opstellingswerkschema verschijnen. Zie [doeldocumentatie](../destinations/overview.md) voor stappen op hoe te om uw bepaalde bestemming te vormen.

## Beleid voor gegevensgebruik beheren {#policies}

Om gegevensgebruikslabels effectief gegevensnaleving te steunen, moet het beleid van het gegevensgebruik worden bepaald en worden toegelaten. Het beleid van het gebruik van gegevens is regels die de soorten marketing acties beschrijven die u aan, of beperkt van, op gegevens binnen CDP in real time mag uitvoeren. Zie de sectie &quot;Beleid voor gegevensgebruik&quot; in [!DNL Experience Platform] [Overzicht van gegevensbeheer](../../data-governance/home.md) voor meer informatie.

Adobe Experience Platform biedt verschillende basisbeleidsregels voor veelvoorkomende gebruiksgevallen voor de ervaring van klanten. Dit beleid kan in UI worden bekeken door aan **[!UICONTROL Beleid]** werkruimte te navigeren en **[!UICONTROL Browse]** tabel te selecteren. Zie [beleidsgebruikershandleiding](../../data-governance/policies/user-guide.md) in de [!DNL Experience Platform] documentatie voor meer gedetailleerde stappen bij het werken met beleid in UI, met inbegrip van hoe te om uw eigen douanebeleid te maken.

## Naleving van gegevensgebruik afdwingen {#enforce}

Zodra de gegevens worden geëtiketteerd en het gebruiksbeleid wordt bepaald, kunt u de naleving van het gegevensgebruik met beleid afdwingen. Wanneer het activeren van publiekssegmenten aan bestemmingen in Echt - tijd CDP, [!DNL Data Governance] handhaaft automatisch gebruiksbeleid als om het even welke schendingen voorkomen.

Zie het document over [automatische beleidshandhaving](../../data-governance/enforcement/auto-enforcement.md) voor meer informatie.

## Volgende stappen

Nu u aan de zeer belangrijke eigenschappen [!DNL Data Governance] op CDP in real time en hoe [!DNL Experience Platform] hen toelaat, gelieve aan de [documentatie voor het Bestuur van Gegevens op Adobe Experience Platform](../../data-governance/home.md) verder te gaan. De documentatie verstrekt overzichten van essentiële concepten [!DNL Data Governance], evenals geleidelijke werkschema&#39;s voor het beheren van de etiketten en het beleid van het gegevensgebruik.

De volgende video verstrekt een overzicht van [!DNL Data Governance] in Echt - tijd CDP, met inbegrip van het gebruik van marketing gebruiksgevallen op bestemmingen en voorbeeldwerkschema&#39;s voor verschillende scenario&#39;s:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)