---
title: Overzicht van gegevensbeheer
seo-title: Gegevensbeheer in Real-time Customer Data Platform
description: 'Met gegevensbeheer kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. '
seo-description: 'Met gegevensbeheer kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. '
translation-type: tm+mt
source-git-commit: c81723d00f6b0a9338c8dd3be8c79385677b4e93
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---


# Gegevensbeheer in real time CDP

Het Platform van Gegevens van de Klant in real time (in real time CDP) brengt gegevens van veelvoudige ondernemingssystemen samen, toestaand marketers om, hun klanten beter te identificeren te begrijpen en te betrekken. Deze gegevens zijn mogelijk onderworpen aan gebruiksbeperkingen die zijn gedefinieerd door uw organisatie of wettelijke voorschriften. Daarom is het belangrijk om ervoor te zorgen dat CDP in real time met gebruiksbeleid wanneer het behandelen van uw gegevens compatibel is.

Met gegevensbeheer voor Adobe Experience Platforms kunt u klantgegevens beheren en ervoor zorgen dat de voorschriften, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een zeer belangrijke rol binnen CDP In real time, toestaand u om gebruiksbeleid te bepalen, uw gegevens te categoriseren die op dat beleid worden gebaseerd, en beleidsschendingen te controleren wanneer het uitvoeren van bepaalde marketing acties.

CDP in real time wordt voortgebouwd bovenop Adobe Experience Platform, en daarom wordt de meerderheid van de mogelijkheden van het Beleid van Gegevens behandeld in de documentatie van het Experience Platform. Dit document is bedoeld als aanvulling op het overzicht [van](../../data-governance/home.md) gegevensbeheer voor Experience Platform en geeft een overzicht van de bestuurskenmerken die beschikbaar zijn in real time CDP. De volgende onderwerpen worden behandeld:

* [Gebruikslabels toepassen op uw gegevens](#labels)
* [Beleid voor gegevensgebruik beheren](#policies)
* [Compatibiliteit met gegevensgebruik afdwingen](#enforcement)

## Gebruikslabels toepassen op uw gegevens {#labels}

Met gegevensbeheer kunt u gebruikslabels op uw gegevens toepassen, op het niveau van de gegevensset of op het niveau van de gegevensset-velden. Met labels voor gegevensgebruik kunt u gegevens indelen op basis van het gebruiksbeleid dat op die gegevens van toepassing is.

Zie de gebruikershandleiding [voor](../../data-governance/labels/overview.md) gegevensgebruikslabels voor Adobe Experience Platform voor gedetailleerde informatie over het werken met labels voor gegevensgebruik.

## Gebruiksgevallen voor marketingdoeleinden configureren voor doelen {#destinations}

U kunt beperkingen voor het gegevensgebruik op een bestemming instellen door gevallen van marketinggebruik (ook wel marketingacties genoemd) voor die bestemming te definiëren. Een marketinggeval voor een bestemming geeft de intentie aan van de gegevens die naar die bestemming worden geëxporteerd.

>[!NOTE] Raadpleeg het overzicht [van het beleid voor](../../data-governance/policies/overview.md) gegevensgebruik in de documentatie bij het Experience Platform voor meer informatie over marketingacties en het gebruik ervan in het beleid voor gegevensgebruik.

Het bepalen van marketing gebruiksgevallen op bestemmingen staat u toe om ervoor te zorgen dat om het even welke profielen of segmenten die naar die bestemmingen worden verzonden volgzaam met het beleid van het gegevensgebruik zijn. Daarom zou u aangewezen gevallen van het marketinggebruik aan uw bestemmingen moeten toevoegen die op de behoeften van uw organisatie worden gebaseerd om beleidsbeperkingen op activering af te dwingen.

Gebruiksscenario&#39;s voor marketingdoeleinden kunnen alleen worden geselecteerd wanneer u een bestemming voor het eerst instelt. Afhankelijk van het type van bestemming u met werkt, zal de kans om de gevallen van het marketinggebruik te vormen op verschillende punten in het opstellingswerkschema verschijnen. Zie de [bestemmingsdocumentatie](../destinations/destinations-overview.md) voor stappen op hoe te om uw bijzondere bestemming te vormen.


## Beleid voor gegevensgebruik beheren {#policies}

Om gegevensgebruikslabels effectief gegevensnaleving te steunen, moet het beleid van het gegevensgebruik worden bepaald en worden toegelaten. Het beleid van het gebruik van gegevens is regels die de soorten marketing acties beschrijven die u aan, of beperkt van, op gegevens binnen CDP in real time mag uitvoeren. Zie de sectie &quot;Beleid van het Gebruik van Gegevens&quot;in het overzicht [van de](../../data-governance/home.md) Gegevensbeheer van het Experience Platform voor meer informatie.

Het Adobe Experience Platform verstrekt verscheidene **kernbeleid** voor de gemeenschappelijke gebruiksgevallen van de klantenervaring. Dit beleid kan in UI worden bekeken door aan de werkruimte van **[!UICONTROL Beleid]** te navigeren en het **[!UICONTROL Browse]** lusje te selecteren. Zie de gids [van de](../../data-governance/policies/user-guide.md) beleidsgebruiker in de documentatie van het Experience Platform voor meer gedetailleerde stappen bij het werken met beleid in UI, met inbegrip van hoe te om uw eigen douanebeleid te maken.

## (bèta) Naleving van gegevensgebruik afdwingen {#enforce-data-usage-compliance}

>[!IMPORTANT]
>Deze functie is momenteel in bèta beschikbaar en niet voor alle gebruikers. Deze functie kan op verzoek worden ingeschakeld. De documentatie en de functionaliteit kunnen worden gewijzigd.

Zodra de gegevens worden geëtiketteerd en het gebruiksbeleid wordt bepaald, kunt u de naleving van het gegevensgebruik met beleid afdwingen. Wanneer het activeren van publiekssegmenten aan bestemmingen in Echt - tijd CDP, dwingt het Beleid van Gegevens automatisch gebruiksbeleid af als om het even welke schendingen voorkomen.

Het volgende diagram illustreert hoe de beleidshandhaving in de gegevensstroom van segmentactivering wordt geïntegreerd:

![](assets/enforcement-flow.png)

Wanneer een segment eerst wordt geactiveerd, controleert de Dienst van het Beleid DULE beleidsschendingen die op de volgende factoren worden gebaseerd:

* De labels voor gegevensgebruik die worden toegepast op velden en gegevenssets binnen het segment dat moet worden geactiveerd.
* Het marketingdoel van de bestemming.

>[!NOTE] Als er gegevensgebruikslabels zijn die slechts op bepaalde gebieden binnen een dataset (eerder dan de volledige dataset) zijn toegepast, komt de handhaving van die gebieden-vlakke etiketten op activering slechts onder de volgende voorwaarden voor:
>* De velden worden gebruikt in de segmentdefinitie.
>* De velden worden geconfigureerd als geprojecteerde kenmerken voor de doelbestemming.


### Berichten over beleidsovertredingen {#enforcement}

Als een beleidsovertreding voorkomt in een poging om een segment te activeren (of [bewerkingen uit te voeren op een reeds geactiveerd segment](#policy-enforcement-for-activated-segments)), wordt de handeling voorkomen en wordt een pop-up weergegeven die aangeeft dat een of meer beleidsregels zijn overtreden. Selecteer een beleidsovertreding in de linkerkolom van de pop-up om details voor die schending te tonen.

![](assets/violation-popover.png)

Het tabblad *Details* van de popover geeft de actie aan die de schending heeft veroorzaakt, de reden waarom de schending heeft plaatsgevonden en bevat suggesties voor het mogelijk oplossen van het probleem.

Klik op **Gegevenslijn** om de doelen, segmenten, samenvoegbeleidsregels of gegevenssets bij te houden waarvan de gegevenslabels de schending hebben veroorzaakt.

![](assets/data-lineage.png)

Nadat een schending heeft teweeggebracht, wordt de **sparen** knoop onbruikbaar gemaakt voor de activering tot de aangewezen componenten worden bijgewerkt om aan het beleid van het gegevensgebruik te voldoen.

### Beleidshandhaving voor geactiveerde segmenten {#policy-enforcement-for-activated-segments}

De handhaving van het beleid is nog op segmenten van toepassing nadat zij zijn geactiveerd, beperkt om het even welke veranderingen in een segment of zijn bestemming die in een beleidsschending zouden resulteren. Wegens de talrijke componenten betrokken bij het activeren van segmenten aan bestemmingen, kunnen om het even welke volgende acties potentieel een schending teweegbrengen:

* Labels voor gegevensgebruik bijwerken
* Gegevenssets voor een segment wijzigen
* Het veranderen van segmentpredikaten
* Doelconfiguraties wijzigen

Als een van de bovenstaande acties een schending veroorzaakt, wordt die actie verhinderd worden bewaard en een bericht van de beleidsschending wordt getoond, die ervoor zorgen dat uw geactiveerde segmenten aan het beleid van het gegevensgebruik blijven voldoen wanneer wordt gewijzigd.

## Volgende stappen

Nu u aan de belangrijkste eigenschappen van het Beleid van Gegevens op CDP in real time en hoe het Experience Platform hen toelaat bent geïntroduceerd, gelieve aan de [documentatie voor het Beleid van Gegevens over Adobe Experience Platform](../../data-governance/home.md)verder te gaan. De documentatie verstrekt overzichten van essentiële concepten van het Beleid van Gegevens, evenals geleidelijke werkschema&#39;s voor het beheren van de etiketten en het beleid van het gegevensgebruik.

De volgende video verstrekt een overzicht van de Governance van Gegevens in Echt - tijd CDP, met inbegrip van het gebruik van marketing gebruiksgevallen op bestemmingen en voorbeeldwerkschema&#39;s voor verschillende scenario&#39;s:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)