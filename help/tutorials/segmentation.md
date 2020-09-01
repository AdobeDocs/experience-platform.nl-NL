---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zelfstudies voor segmentatie
topic: tutorial
description: Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful API waarmee u segmenten kunt samenstellen en doelgroepen kunt genereren op basis van uw gegevens in het realtime-klantprofiel. Deze segmenten worden centraal gevormd en gehandhaafd op Platform, en gemakkelijk toegankelijk door om het even welke oplossing van Adobe.
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# Zelfstudies voor segmentatie

Adobe Experience Platform [!DNL Segmentation Service] biedt een gebruikersinterface en RESTful-API waarmee u segmenten kunt samenstellen en doelgroepen kunt genereren op basis van uw [!DNL Real-time Customer Profile] gegevens. Deze segmenten worden centraal gevormd en gehandhaafd [!DNL Platform], en gemakkelijk toegankelijk door om het even welke oplossing van Adobe. Meer over segmentatie leren, begin door het overzicht [van de Dienst van de](../segmentation/home.md)Segmentatie te lezen.

## Een segmentdefinitie maken

Een segmentdefinitie is de regel die wordt gebruikt om zeer belangrijke kenmerken of gedrag van een doelpubliek te beschrijven. Zodra geconceptualiseerd, worden de regels die in een segmentdefinitie worden geschetst gebruikt om kwalificerende publieksleden voor een segment te bepalen. Het ontwikkelen, testen, voorvertonen en opslaan van een segmentdefinitie kan worden uitgevoerd met de [!DNL Platform] gebruikersinterface of API&#39;s. Om een segmentdefinitie tot stand te brengen, volg het [creëren van een segment API leerprogramma](../segmentation/tutorials/create-a-segment.md) of de gebruikersgids [van de Bouwer van het](../segmentation/ui/overview.md)Segment UI.

## Evalueer een segment en toegangsresultaten

Zodra u hebt ontwikkeld, getest, en uw segmentdefinitie bewaard, kunt u het segment door of geplande evaluatie of op bestelling evaluatie dan evalueren. De geplande evaluatie (die ook als &quot;geplande segmentatie&quot;wordt bekend) staat u toe om een terugkomende planning voor het runnen van een uitvoerbaan in een specifieke tijd tot stand te brengen, terwijl de evaluatie op bestelling het creëren van een segmentbaan impliceert om het publiek onmiddellijk te bouwen. Meer leren, bezoek het leerprogramma voor het [evalueren van en de toegang tot van segmentresultaten](../segmentation/tutorials/evaluate-a-segment.md).

## Segmentgegevens exporteren

Voor het exporteren van segmenten met [!DNL Profile] gegevens moet eerst een gegevensset worden [gemaakt waarin de gegevens worden geëxporteerd](../segmentation/tutorials/create-dataset-export-segment.md)en vervolgens een nieuwe exporttaak worden gestart. De stappen voor het produceren van een uitvoerbaan kunnen in het leerprogramma bij het [evalueren van een segment](../segmentation/tutorials/evaluate-a-segment.md)worden gevonden.

## Samenvoegingsbeleid configureren

Met Adobe Experience Platform kunt u gegevens uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Wanneer het brengen van deze gegevens samen, zijn het fusiebeleid de regels die [!DNL Platform] gebruiken om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen. Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Om met samenvoegbeleid in [!DNL Platform] UI te werken, bezoek de de gebruikersgids [van het](../profile/ui/merge-policies.md)fusiebeleid. Zie de ontwikkelaarsgids voor [!DNL Real-time Customer Profile] [samenvoegbeleidsregels als u met de](../profile/api/merge-policies.md)API werkt met samenvoegingsbeleid.

## Compatibiliteit met gegevensgebruik voor segmenten afdwingen

De segmenten die voor gebruik in worden toegelaten [!DNL Real-time Customer Profile] bevatten een identiteitskaart van het fusiebeleid binnen hun segmentdefinitie. Dit samenvoegbeleid bevat informatie over welke datasets in het segment moeten worden omvat, die beurtelings om het even welke toepasselijke etiketten van het gegevensgebruik bevatten. Voor specifieke stappen die het afdwingen van de naleving van het gegevensgebruik voor een publiekssegment, gelieve te volgen de de handhavingszelfstudie van het [gegevensgebruik voor segmenten](../segmentation/tutorials/governance.md).

## Streaming segmentering

Streaming segmentatie is de mogelijkheid om een klant direct te evalueren zodra een gebeurtenis in een bepaalde segmentgroep komt. Met dit vermogen, kunnen de meeste segmentregels nu worden geëvalueerd aangezien de gegevens in Adobe Experience Platform worden overgegaan, betekenend zal het segmentlidmaatschap bijgewerkt zonder geplande segmentatietaken in werking te stellen worden gehouden. Ga voor meer informatie naar het [streamingsegmentatieoverzicht](../segmentation/api/streaming-segmentation.md).

## Segmentatie van meerdere entiteiten

De segmentatie van meerdere entiteiten is de capaciteit om [!DNL Profile] gegevens met extra gegevens uit te breiden die op producten, opslag, of andere niet-profielklassen worden gebaseerd. Zodra verbonden, worden de gegevens van extra klassen beschikbaar alsof zij aan het [!DNL Profile] schema inheems waren. Zie de segmentatiedocumentatie [over](../segmentation/multi-entity-segmentation.md)meerdere entiteiten voor meer informatie over verplaatsen.