---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zelfstudies voor segmentatie
topic: tutorial
translation-type: tm+mt
source-git-commit: b0ef50e25c27aba121bb01c602867953eb2a5f7e
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---


# Zelfstudies voor segmentatie

De Dienst van de Segmentatie van het Adobe Experience Platform verstrekt een gebruikersinterface en RESTful API die u toestaat om segmenten te bouwen en publiek van uw gegevens van het Profiel van de Klant in real time te produceren. Deze segmenten worden centraal geconfigureerd en onderhouden op het Platform en zijn gemakkelijk toegankelijk voor elke Adobe-oplossing. Meer over segmentatie leren, begin door het overzicht [van de Dienst van de](../segmentation/home.md)Segmentatie te lezen.

## Een segmentdefinitie maken

Een segmentdefinitie is de regel die wordt gebruikt om zeer belangrijke kenmerken of gedrag van een doelpubliek te beschrijven. Zodra geconceptualiseerd, worden de regels die in een segmentdefinitie worden geschetst gebruikt om kwalificerende publieksleden voor een segment te bepalen. Het ontwikkelen, het testen, het previewing, en het bewaren van een segmentdefinitie kunnen worden gedaan gebruikend de gebruikersinterface of APIs van het Platform. Om een segmentdefinitie tot stand te brengen, volg het [creëren van een segment API leerprogramma](../segmentation/tutorials/create-a-segment.md) of de gebruikersgids [van de Bouwer van het](../segmentation/ui/overview.md)Segment UI.

## Evalueer een segment en toegangsresultaten

Zodra u hebt ontwikkeld, getest, en uw segmentdefinitie bewaard, kunt u het segment door of geplande evaluatie of op bestelling evaluatie dan evalueren. De geplande evaluatie (die ook als &quot;geplande segmentatie&quot;wordt bekend) staat u toe om een terugkomende planning voor het runnen van een uitvoerbaan in een specifieke tijd tot stand te brengen, terwijl de evaluatie op bestelling het creëren van een segmentbaan impliceert om het publiek onmiddellijk te bouwen. Meer leren, bezoek het leerprogramma voor het [evalueren van en de toegang tot van segmentresultaten](../segmentation/tutorials/evaluate-a-segment.md).

## Segmentgegevens exporteren

Wanneer u segmenten met profielgegevens exporteert, moet u eerst een gegevensset [maken waarin de gegevens worden geëxporteerd](../segmentation/tutorials/create-dataset-export-segment.md)en vervolgens een nieuwe exporttaak starten. De stappen voor het genereren van een exporttaak vindt u in de zelfstudie over de [exportAPI](../segmentation/tutorials/export-data.md).

## Samenvoegingsbeleid configureren

Met Adobe Experience Platform kunt u gegevens uit meerdere bronnen samenbrengen en combineren om een volledige weergave van elk van uw individuele klanten te bekijken. Wanneer het brengen van deze gegevens samen, is het fusiebeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen. Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Ga naar de gebruikershandleiding [voor](../profile/ui/merge-policies.md)samenvoegbeleid om samen te werken met samenvoegingsbeleid in de gebruikersinterface van het Platform. Om met samenvoegbeleid te werken gebruikend Real-time API van het Profiel van de Klant, zie de de ontwikkelaarsgids [van het](../profile/api/merge-policies.md)fusiebeleid.

## Compatibiliteit met gegevensgebruik voor segmenten afdwingen

De segmenten die voor gebruik in het Profiel van de Klant in real time worden toegelaten bevatten een identiteitskaart van het fusiebeleid binnen hun segmentdefinitie. Dit samenvoegbeleid bevat informatie over welke datasets in het segment moeten worden omvat, die beurtelings om het even welke toepasselijke etiketten van het gegevensgebruik bevatten. Voor specifieke stappen die het afdwingen van de naleving van het gegevensgebruik voor een publiekssegment, gelieve te volgen de de handhavingszelfstudie van het [gegevensgebruik voor segmenten](../segmentation/tutorials/governance.md).

## Streaming segmentering

Streaming segmentatie is de mogelijkheid om een klant direct te evalueren zodra een gebeurtenis in een bepaalde segmentgroep komt. Met dit vermogen, kunnen de meeste segmentregels nu worden geëvalueerd aangezien de gegevens in Adobe Experience Platform worden overgegaan, betekenend zal het segmentlidmaatschap bijgewerkt zonder geplande segmentatietaken in werking te stellen worden gehouden. Ga voor meer informatie naar het [streamingsegmentatieoverzicht](../segmentation/api/streaming-segmentation.md).

## Segmentatie van meerdere entiteiten

De segmentatie van meerdere entiteiten is de capaciteit om de gegevens van het Profiel met extra gegevens uit te breiden die op producten, opslag, of andere niet-profielklassen worden gebaseerd. Zodra verbonden, worden de gegevens van extra klassen beschikbaar alsof zij aan het schema van het Profiel inheems waren. Zie de segmentatiedocumentatie [over](../segmentation/multi-entity-segmentation.md)meerdere entiteiten voor meer informatie over verplaatsen.