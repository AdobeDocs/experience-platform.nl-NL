---
title: Overzicht van gegevensbeheer
seo-title: Gegevensbeheer in het Real-Time Customer Data Platform
description: 'Met gegevensbeheer kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. '
seo-description: 'Met gegevensbeheer kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. '
translation-type: tm+mt
source-git-commit: e21cf6794e6c9ee522482cd9ccb95d66b06d330a

---


# Gegevensbeheer in real time CDP

Het Real-time Platform van de Gegevens van de Klant (CDP in real time) brengt gegevens van veelvoudige ondernemingssystemen samen, die marketers toestaan om, hun klanten beter te identificeren te begrijpen en te betrekken. Deze gegevens zijn mogelijk onderworpen aan gebruiksbeperkingen die zijn gedefinieerd door uw organisatie of wettelijke voorschriften. Daarom is het belangrijk om ervoor te zorgen dat CDP in real time met gebruiksbeleid wanneer het behandelen van uw gegevens compatibel is.

Met de gegevensbeheer van het Adobe Experience Platform kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een zeer belangrijke rol binnen CDP In real time, toestaand u om gebruiksbeleid te bepalen, uw gegevens te categoriseren die op dat beleid worden gebaseerd, en beleidsschendingen te controleren wanneer het uitvoeren van bepaalde marketing acties.

CDP in real time wordt voortgebouwd bovenop het Platform van de Ervaring van Adobe, en daarom worden de meeste mogelijkheden van het Beleid van Gegevens behandeld in de documentatie van het Platform van de Ervaring. Dit document is bedoeld als aanvulling op het overzicht [van](../../data-governance/home.md) gegevensbeheer voor het ervaringsplatform en geeft een overzicht van de bestuurskenmerken die beschikbaar zijn in real-time CDP. De volgende onderwerpen worden behandeld:

* [Gebruikslabels toepassen op uw gegevens](#labels)
* [Beleid voor gegevensgebruik beheren](#policies)
* [Compatibiliteit met gegevensgebruik afdwingen](#enforcement)

## Gebruikslabels toepassen op uw gegevens {#labels}

Met gegevensbeheer kunt u gebruikslabels op uw gegevens toepassen, op het niveau van de gegevensset of op het niveau van de gegevensset-velden. Met labels voor gegevensgebruik kunt u gegevens indelen op basis van het gebruiksbeleid dat op die gegevens van toepassing is.

Raadpleeg de gebruikershandleiding bij [de labels voor](../../data-governance/labels/overview.md) gegevensgebruikslabels voor het Adobe Experience Platform voor meer informatie over het werken met labels voor gegevensgebruik.

## Beperkingen voor doelen instellen

U kunt beperkingen voor het gegevensgebruik op een bestemming instellen door marketinggevallen voor die bestemming te definiëren. Het bepalen van gebruiksgevallen voor bestemmingen staat u toe om op de schendingen van het gebruiksbeleid te controleren en ervoor te zorgen dat om het even welke profielen of segmenten die naar die bestemming worden verzonden met de regels van het Beheer van Gegevens compatibel zijn.

Gebruiksgevallen voor marketing kunnen worden gedefinieerd tijdens de fase _Setup_ voor de workflow _Doel_ bewerken. Zie de doeldocumentatie voor meer informatie.


## Beleid voor gegevensgebruik beheren {#policies}

Om gegevensgebruikslabels effectief gegevensnaleving te steunen, moet het beleid van het gegevensgebruik worden bepaald en worden toegelaten. Het beleid van het gebruik van gegevens is regels die de soorten marketing acties beschrijven die u aan, of beperkt van, op gegevens binnen CDP in real time mag uitvoeren. Zie het gedeelte Beleid voor gegevensgebruik in het overzicht [Data Governance-](../../data-governance/home.md) gegevens van het ervaringsplatform voor meer informatie.

Het Adobe Experience Platform biedt verschillende **basisbeleidsregels** voor veelvoorkomende gebruikssituaties voor klanten. Dit beleid kan worden bekeken door een verzoek aan de [DULE Dienst API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)van het Beleid, zoals aangetoond in de &quot;Lijst alle beleidsgebieden&quot;sectie in de [de ontwikkelaarsgids](../../data-governance/policies/overview.md)van de Dienst van het Beleid te doen. U kunt ook uw eigen **aangepaste beleid** maken om aangepaste gebruiksbeperkingen te modelleren, zoals in de sectie &quot;Een beleid maken&quot; in de handleiding voor ontwikkelaars wordt getoond.

## (bèta) Naleving van gegevensgebruik afdwingen {#enforce-data-usage-compliance}

>[!IMPORTANT]
>Deze functie is momenteel in bèta beschikbaar en niet voor alle gebruikers. Deze functie kan op verzoek worden ingeschakeld. De documentatie en de functionaliteit kunnen worden gewijzigd.

Zodra de gegevens worden geëtiketteerd en het gebruiksbeleid wordt bepaald, kunt u de naleving van het gegevensgebruik met beleid afdwingen. Wanneer het activeren van publiekssegmenten aan bestemmingen in Echt - tijd CDP, dwingt het Beleid van Gegevens automatisch gebruiksbeleid af als om het even welke schendingen voorkomen.

Het volgende diagram illustreert hoe de beleidshandhaving in de gegevensstroom van segmentactivering wordt geïntegreerd:

![](assets/enforcement-flow.png)

Wanneer een segment eerst wordt geactiveerd, controleert de Dienst van het Beleid DULE beleidsschendingen die op de volgende factoren worden gebaseerd:

* De labels voor gegevensgebruik die worden toegepast op velden en gegevenssets binnen het segment dat moet worden geactiveerd.
* Het marketingdoel van de bestemming.

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

Nu u bent geïntroduceerd in de belangrijkste functies voor gegevensbeheer op CDP in real-time en hoe het Experience Platform deze functies inschakelt, gaat u verder met de [documentatie voor gegevensbeheer op het Adobe Experience Platform](../../data-governance/home.md). De documentatie verstrekt overzichten van essentiële concepten van het Beleid van Gegevens, evenals geleidelijke werkschema&#39;s voor het beheren van de etiketten en het beleid van het gegevensgebruik.