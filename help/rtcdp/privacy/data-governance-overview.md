---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance
title: Overzicht van gegevensbeheer
seo-title: Gegevensbeheer in Real-time Customer Data Platform
description: 'Met gegevensbeheer kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. '
seo-description: 'Met gegevensbeheer kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. '
translation-type: tm+mt
source-git-commit: 259c26a9d3b6ef397acd552e255f68ecb25b2dd1
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 0%

---


# [!DNL Data Governance] in Real-time CDP

[!DNL Real-time Customer Data Platform] (CDP in real time) brengt gegevens van veelvoudige ondernemingssystemen samen, toestaand marketers om, hun klanten beter te identificeren te begrijpen en in dienst te nemen. Deze gegevens zijn mogelijk onderworpen aan gebruiksbeperkingen die zijn gedefinieerd door uw organisatie of wettelijke voorschriften. Daarom is het belangrijk om ervoor te zorgen dat CDP in real time met gebruiksbeleid wanneer het behandelen van uw gegevens compatibel is.

Met Adobe Experience Platform [!DNL Data Governance] kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een zeer belangrijke rol binnen CDP In real time, toestaand u om gebruiksbeleid te bepalen, uw gegevens te categoriseren die op dat beleid worden gebaseerd, en beleidsschendingen te controleren wanneer het uitvoeren van bepaalde marketing acties.

CDP in real time wordt gebouwd bovenop Adobe Experience Platform, en daarom wordt de meerderheid van [!DNL Data Governance] mogelijkheden behandeld in de [!DNL Experience Platform] documentatie. Dit document is bedoeld als aanvulling op het overzicht [van](../../data-governance/home.md) gegevensbeheer voor [!DNL Experience Platform], en schetst de bestuurskenmerken die beschikbaar zijn in real time CDP. De volgende onderwerpen worden behandeld:

* [Gebruikslabels toepassen op uw gegevens](#labels)
* [Beleid voor gegevensgebruik beheren](#policies)
* [Compatibiliteit met gegevensgebruik afdwingen](#enforce-data-usage-compliance)

## Gebruikslabels toepassen op uw gegevens {#labels}

[!DNL Data Governance] staat u toe om gebruiksetiketten op uw gegevens, of op de dataset of dataset-gebied niveau toe te passen. Met labels voor gegevensgebruik kunt u gegevens indelen op basis van het gebruiksbeleid dat op die gegevens van toepassing is.

Zie de gebruikershandleiding bij [de labels voor](../../data-governance/labels/overview.md) gegevensgebruikslabels voor Adobe Experience Platform voor gedetailleerde informatie over het werken met labels voor gegevensgebruik.

## Gebruiksgevallen voor marketingdoeleinden configureren voor doelen {#destinations}

U kunt beperkingen voor het gegevensgebruik op een bestemming instellen door gevallen van marketinggebruik (ook wel marketingacties genoemd) voor die bestemming te definiëren. Een marketinggeval voor een bestemming geeft de intentie aan van de gegevens die naar die bestemming worden geëxporteerd.

>[!NOTE]
>
>Zie het overzicht [van beleidsregels voor](../../data-governance/policies/overview.md) gegevensgebruik in de [!DNL Experience Platform] documentatie voor meer informatie over marketingacties en het gebruik ervan in het beleid voor gegevensgebruik.

Het bepalen van marketing gebruiksgevallen op bestemmingen staat u toe om ervoor te zorgen dat om het even welke profielen of segmenten die naar die bestemmingen worden verzonden volgzaam met het beleid van het gegevensgebruik zijn. Daarom zou u aangewezen gevallen van het marketinggebruik aan uw bestemmingen moeten toevoegen die op de behoeften van uw organisatie worden gebaseerd om beleidsbeperkingen op activering af te dwingen.

Gebruiksscenario&#39;s voor marketingdoeleinden kunnen alleen worden geselecteerd wanneer u een bestemming voor het eerst instelt. Afhankelijk van het type van bestemming u met werkt, zal de kans om de gevallen van het marketinggebruik te vormen op verschillende punten in het opstellingswerkschema verschijnen. Zie de [bestemmingsdocumentatie](../destinations/destinations-overview.md) voor stappen op hoe te om uw bijzondere bestemming te vormen.


## Beleid voor gegevensgebruik beheren {#policies}

Om gegevensgebruikslabels effectief gegevensnaleving te steunen, moet het beleid van het gegevensgebruik worden bepaald en worden toegelaten. Het beleid van het gebruik van gegevens is regels die de soorten marketing acties beschrijven die u aan, of beperkt van, op gegevens binnen CDP in real time mag uitvoeren. Zie de sectie &quot;Beleid voor gegevensgebruik&quot; in het overzicht [!DNL Experience Platform] van [](../../data-governance/home.md) gegevensbeheer voor meer informatie.

Adobe Experience Platform biedt verschillende basisbeleidsregels voor veelvoorkomende gebruiksgevallen voor de ervaring van klanten. Dit beleid kan in UI worden bekeken door aan de werkruimte van **[!UICONTROL Beleid]** te navigeren en het **[!UICONTROL Browse]** lusje te selecteren. Zie de gids [van de](../../data-governance/policies/user-guide.md) beleidsgebruiker in de [!DNL Experience Platform] documentatie voor meer gedetailleerde stappen bij het werken met beleid in UI, met inbegrip van hoe te om uw eigen douanebeleid te maken.

## Compatibiliteit met gegevensgebruik afdwingen {#enforce-data-usage-compliance}

Zodra de gegevens worden geëtiketteerd en het gebruiksbeleid wordt bepaald, kunt u de naleving van het gegevensgebruik met beleid afdwingen. Wanneer het activeren van publiekssegmenten aan bestemmingen in Echt - tijd CDP, [!DNL Data Governance] dwingt automatisch gebruiksbeleid af als om het even welke schendingen voorkomen.

Het volgende diagram illustreert hoe de beleidshandhaving in de gegevensstroom van segmentactivering wordt geïntegreerd:

![](assets/enforcement-flow.png)

Wanneer een segment voor het eerst wordt geactiveerd, wordt op basis van de volgende factoren [!DNL Policy Service] gecontroleerd op beleidsovertredingen:

* De labels voor gegevensgebruik die worden toegepast op velden en gegevenssets binnen het segment dat moet worden geactiveerd.
* Het marketingdoel van de bestemming.

>[!NOTE]
>
>Als er gegevensgebruikslabels zijn die slechts op bepaalde gebieden binnen een dataset (eerder dan de volledige dataset) zijn toegepast, komt de handhaving van die gebieden-vlakke etiketten op activering slechts onder de volgende voorwaarden voor:
>* De velden worden gebruikt in de segmentdefinitie.
>* De velden worden geconfigureerd als geprojecteerde kenmerken voor de doelbestemming.


### Berichten over beleidsovertredingen {#enforcement}

Als een beleidsovertreding voorkomt in een poging om een segment te activeren (of [bewerkingen uit te voeren op een reeds geactiveerd segment](#policy-enforcement-for-activated-segments)), wordt de handeling voorkomen en wordt een pop-up weergegeven die aangeeft dat een of meer beleidsregels zijn overtreden. Selecteer een beleidsovertreding in de linkerkolom van de pop-up om details voor die schending te tonen.

![](assets/violation-popover.png)

Het tabblad **[!UICONTROL Details]** van de popover geeft de actie aan die de schending heeft veroorzaakt, de reden waarom de schending heeft plaatsgevonden en bevat suggesties voor het mogelijk oplossen van het probleem.

Klik op **[!UICONTROL Gegevenslijn]** om de doelen, segmenten, samenvoegbeleidsregels of gegevenssets bij te houden waarvan de gegevenslabels de schending hebben veroorzaakt.

![](assets/data-lineage.png)

Nadat een schending heeft teweeggebracht, wordt de **[!UICONTROL sparen]** knoop onbruikbaar gemaakt voor de activering tot de aangewezen componenten worden bijgewerkt om aan het beleid van het gegevensgebruik te voldoen.

### Beleidshandhaving voor geactiveerde segmenten {#policy-enforcement-for-activated-segments}

De handhaving van het beleid is nog op segmenten van toepassing nadat zij zijn geactiveerd, beperkt om het even welke veranderingen in een segment of zijn bestemming die in een beleidsschending zouden resulteren. Wegens de talrijke componenten betrokken bij het activeren van segmenten aan bestemmingen, kunnen om het even welke volgende acties potentieel een schending teweegbrengen:

* Labels voor gegevensgebruik bijwerken
* Gegevenssets voor een segment wijzigen
* Het veranderen van segmentpredikaten
* Doelconfiguraties wijzigen

Als een van de bovenstaande acties een schending veroorzaakt, wordt die actie verhinderd worden bewaard en een bericht van de beleidsschending wordt getoond, die ervoor zorgen dat uw geactiveerde segmenten aan het beleid van het gegevensgebruik blijven voldoen wanneer wordt gewijzigd.

## Volgende stappen

Nu u aan de belangrijkste [!DNL Data Governance] eigenschappen op CDP in real time en hoe [!DNL Experience Platform] toelaat bent geïntroduceerd, gelieve aan de [documentatie voor het Beleid van Gegevens op Adobe Experience Platform](../../data-governance/home.md)voort te zetten. De documentatie verstrekt overzichten van essentiële [!DNL Data Governance] concepten, evenals geleidelijke werkschema&#39;s voor het beheren van de etiketten en het beleid van het gegevensgebruik.

De volgende video verstrekt een overzicht van [!DNL Data Governance] in real time CDP, met inbegrip van het gebruik van marketing gebruiks-gevallen op bestemmingen en voorbeeldwerkschema&#39;s voor verschillende scenario&#39;s:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)