---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segment;Segment;Segments;segments
solution: Experience Platform
title: Adobe Experience Platform Segmentation Service
topic: overview
description: Dit document biedt een overzicht van de Segmentatieservice en de rol die deze speelt in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 5dd07bf9afe96be3a4c3f4a4d4e3b23aef4fde70
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 0%

---


# Adobe Experience Platform [!DNL Segmentation Service] overview

Adobe Experience Platform [!DNL Segmentation Service] biedt een gebruikersinterface en RESTful-API waarmee u segmenten kunt samenstellen en doelgroepen kunt genereren op basis van uw [!DNL Real-time Customer Profile] gegevens. Deze segmenten worden centraal gevormd en gehandhaafd [!DNL Platform], en gemakkelijk toegankelijk door om het even welke oplossing van Adobe.

Dit document biedt een overzicht van [!DNL Segmentation Service] en de rol die het speelt in Adobe Experience Platform.

## Getting started with [!DNL Segmentation Service]

Het is belangrijk dat u de volgende belangrijke termen kent die in dit document worden gebruikt:

- **Segmentatie**: Het verdelen van een grote groep individuen (zoals klanten, vooruitzichten, gebruikers, of organisaties) in kleinere groepen die gelijkaardige eigenschappen delen en op gelijkaardige wijze aan marketing strategieën zullen antwoorden.
- **Segmentdefinitie**: De regelreeks die wordt gebruikt om zeer belangrijke kenmerken of gedrag van een doelpubliek te beschrijven. Zodra geconceptualiseerd, worden de regels die in een segmentdefinitie worden geschetst gebruikt om kwalificerende publieksleden voor een segment te bepalen.
- **Publiek**: De resulterende set profielen die voldoen aan de criteria van een segmentdefinitie.

## Hoe segmentatie werkt

De segmentatie is het proces om specifieke attributen of gedrag te bepalen die door een ondergroep van profielen van uw profielopslag worden gedeeld om een verhandelbare groep mensen van uw klantenbasis te onderscheiden. In een e-mailcampagne met de naam &quot;Hebt u vergeten uw gulders te kopen?&quot; wilt u bijvoorbeeld een publiek van alle gebruikers die in de afgelopen 30 dagen naar schoenen hebben gezocht, maar die geen aankoop hebben gedaan.

Zodra een segment conceptueel is gedefinieerd, wordt het ingebouwd [!DNL Experience Platform]. Doorgaans worden segmenten samengesteld door de marketeter of publieksspecialist, maar sommige organisaties geven de voorkeur aan het maken ervan door hun marketingafdeling, in samenwerking met hun gegevensanalisten. Bij het herzien van de gegevens die worden verzonden naar [!DNL Platform], stelt de gegevensanalist de segmentdefinitie samen door te selecteren welke gebieden en waarden zullen worden gebruikt om de regels of voorwaarden van het segment te bouwen. Dit wordt gedaan gebruikend of UI of API.

## Segmenten maken

Of ze nu zijn gemaakt met de API of met de API, segmenten [!DNL Segment Builder]worden uiteindelijk gedefinieerd met [!DNL Profile Query Language] (PQL). Dit is waar de conceptuele segmentdefinitie in de gebouwde taal wordt beschreven om profielen terug te winnen die aan de criteria voldoen. Zie het [PQL-overzicht](./pql/overview.md)voor meer informatie.

Leren om segmenten in te creëren en te gebruiken [!DNL Segment Builder] (de implementatie UI van [!DNL Segmentation Service]), zie de gids [van de Bouwer van het](./ui/overview.md)Segment.

Voor informatie over het bouwen van segmentdefinities die API gebruiken, zie de zelfstudie over het [creëren van publiekssegmenten gebruikend API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Als een schema wordt uitgebreid, moeten alle toekomstige uploads nieuwe toegevoegde gebieden dienovereenkomstig bijwerken. Voor meer informatie bij het aanpassen [!DNL Experience Data Model] (XDM), bezoek het [Zelfstudie](../xdm/tutorials/create-schema-ui.md)van de Redacteur van het Schema.

## Segmenten evalueren

### Streaming segmentering

Streaming segmentatie is een doorlopend proces voor gegevensselectie dat uw segmenten bijwerkt als reactie op gebruikersactiviteit. Zodra een segment is gebouwd en opgeslagen, wordt de segmentdefinitie toegepast op inkomende gegevens aan [!DNL Real-time Customer Profile]. Segmenttoevoegingen en verwijderingen worden regelmatig verwerkt, zodat het doelpubliek relevant blijft.

Lees de documentatie over [](./api/streaming-segmentation.md)streamingsegmentatie voor meer informatie over streamingsegmentatie.

### Batchsegmentatie

Als alternatief voor een lopend proces van de gegevensselectie, verplaatst de partijsegmentatie alle profielgegevens in één keer door segmentdefinities om het overeenkomstige publiek te veroorzaken. Zodra gecreeerd, wordt dit segment bewaard en opgeslagen zodat u het voor gebruik kunt uitvoeren.

Leren hoe te om segmenten te evalueren zie het [vakevaluatieleerprogramma](./tutorials/evaluate-a-segment.md).

## Toegang tot segmenteringsresultaten

Leren hoe te om tot een uitgevoerd segment toegang te hebben, zie het [studiepagina](./tutorials/evaluate-a-segment.md)van de segmentevaluatie.

## Metagegevens segment

Metagegevens van segmenten maken het indexeren mogelijk als een van uw segmenten opnieuw moet worden gebruikt en/of moet worden gecombineerd.

Het samenstellen van uw segmenten (door of API of [!DNL Segment Builder]) vereist dat u een segmentnaam en fusiebeleid bepaalt.

### Segmentnamen

Wanneer u een nieuw segment maakt, moet u een segmentnaam opgeven. De segmentnaam wordt gebruikt om een bepaald segment onder de inzameling te identificeren die door wordt gebouwd [!DNL Segmentation Service]. Segmentnamen moeten daarom beschrijvend, beknopt en uniek zijn.

>[!NOTE]
>
>Wanneer het plannen van een segment, herinner dat de segmenten van, en gecombineerd met, een ander segment kunnen worden van verwijzingen voorzien. Houd er bij het selecteren van een naam rekening mee dat uw segment herbruikbare gedeelten kan bevatten.

### Beleid samenvoegen

Het beleid van de fusie is regels die door worden gebruikt [!DNL Profile] om te bepalen hoe de gegevens aan prioriteit zullen worden gegeven en in een verenigde mening onder bepaalde voorwaarden zullen worden gecombineerd.
Als er geen samenvoegbeleid is gedefinieerd, wordt het standaardsamenvoegbeleid [!DNL Platform] gebruikt. Als u liever een samenvoegingsbeleid wilt gebruiken dat specifiek is voor uw organisatie, kunt u uw eigen beleid maken en dit markeren als de standaardinstelling van uw organisatie.

Meer informatie over samenvoegingsbeleid vindt u in de handleiding voor [samenvoegingsbeleid](../profile/api/merge-policies.md).

>[!NOTE]
>
>De schatting van de omvang van het publiek is gebaseerd op het standaardbeleid voor het samenvoegen van profielen van de organisatie.

### Andere segmentmetagegevens

Naast segmentnaam en samenvoegbeleid, [!DNL Segment Builder] biedt u een extra &quot;segmentbeschrijving&quot;meta-gegevensgebied aan waar u het doel van uw segmentdefinitie kunt samenvatten.

## Geavanceerde segmentatiefuncties

De segmenten kunnen worden gevormd om voortdurend een publiek te produceren door het [stromen gegevensopname](../ingestion/streaming-ingestion/overview.md) met om het even welke volgende geavanceerde segmenteringseigenschappen te combineren:
- [Opeenvolgende segmentatie](#sequential)
- [Dynamische segmentatie](#dynamic)
- [Segmentatie van meerdere entiteiten](#multi-entity)

Deze geavanceerde functies worden in de volgende secties nader besproken.

## Opeenvolgende segmentatie {#sequential}

Een standaardreis van de gebruiker is sequentieel van aard. Met Adobe Experience Platform kunt u een geordende reeks segmenten definiëren die deze reis weerspiegelen en zo sequenties van gebeurtenissen vastleggen zoals deze zich voordoen. U kunt gebeurtenissen in de gewenste volgorde rangschikken met de tijdlijn van de visuele gebeurtenis in de [!DNL Segment Builder]tijdlijn.

Een voorbeeld van een klantenreis die opeenvolgende segmentatie zou vereisen zou productmening > product toevoegen > controle > Geen aankoop zijn.

## Dynamische segmentatie {#dynamic}

De dynamische segmentatie lost de scalability problemen op markten traditioneel wanneer het bouwen van segmenten voor marketing campagnes worden geconfronteerd.

In tegenstelling tot statische segmentatie die u vereist om elk mogelijk gebruiksgeval uitdrukkelijk en herhaaldelijk te vangen, gebruikt de dynamische segmentatie variabelen om de regellogica te bouwen en dynamisch verhoudingen uit te drukken.

### Hoofdlettergebruik: Op zoek naar klanten die buiten hun thuisland aankopen doen

Om de waarde van deze geavanceerde segmenteringseigenschap te illustreren, overweeg een gegevensarchitect die met een telleraar samenwerkt om klanten te identificeren die aankopen buiten hun huisstaat maakten.

**Het probleem**

De statische segmentatie vereist u om individuele segmenten met een uniek attribuut van de huisstaat te bepalen, alvorens voor aankoopgebeurtenissen te filtreren die niet de huisstaat evenaren. Een expliciet segment van dit type zou &quot;Ik zoek mensen uit Utah waar de staat van hun aankoop niet Utah is&quot; lezen. Als u een publiek wilt maken met deze methode, moet u één segment definiëren voor elke staat in de VS, voor in totaal 50 segmenten.

Als gevolg van de verschillende segmentcombinaties die onvermijdelijk optreden wanneer u schaalt, neemt het handmatige proces dat nodig is voor statische segmentatie meer tijd in beslag, waardoor de algehele efficiëntie afneemt.

**De oplossing**

Door een variabele toe te wijzen aan het attribuut van de koopstaat, vereenvoudigt uw dynamisch segment om &quot;me een aankoop te vinden waar de staat van die aankoop niet gelijk aan de huisstaat van de klant is&quot;. Zo kunt u vervolgens 50 statische segmenten verenigen in één dynamisch segment.

## Segmentatie van meerdere entiteiten {#multi-entity}

Met de geavanceerde functie voor segmentatie van meerdere entiteiten hebt u de mogelijkheid om [!DNL Real-time Customer Profile] gegevens uit te breiden met aanvullende gegevens op basis van producten, winkels of andere personen, ook wel &#39;dimensie&#39;-entiteiten genoemd. Dientengevolge, [!DNL Segmentation Service] kan tot extra gebieden tijdens segmentdefinitie toegang hebben alsof zij aan de [!DNL Profile] gegevensopslag inheems waren. De segmentatie van meerdere entiteiten verstrekt flexibiliteit wanneer het identificeren van publiek dat op gegevens wordt gebaseerd relevant voor uw unieke bedrijfsbehoeften. Raadpleeg de segmentatiehandleiding voor [meerdere entiteiten voor meer informatie, zoals gebruiksgevallen en workflows](multi-entity-segmentation.md).

## [!DNL Segmentation Service] gegevenstypen

[!DNL Segmentation Service] ondersteunt diverse primitieve en complexe gegevenstypen. Gedetailleerde informatie, waaronder een lijst met ondersteunde gegevenstypen, vindt u in de [ondersteunde gegevenstypehandleiding](./data-types.md).

## Volgende stappen

[!DNL Segmentation Service] biedt een geconsolideerde workflow voor het samenstellen van segmenten op basis van [!DNL Real-time Customer Profile] gegevens. Samenvattend:

- [!DNL Segmentation] Dit is het proces waarbij u een subset van profielen definieert vanuit het profielarchief, zodat u gedrag of kenmerken van een gewenste verhandelbare groep kunt karakteriseren. [!DNL Segmentation Service] maakt dit proces mogelijk.
- Wanneer het plannen van een segment, houd in mening dat een segment van, en gecombineerd met, een ander segment kan worden van verwijzingen voorzien.
- Een segment kan van regels worden gebouwd die op profielgegevens, verwante tijdreeksgegevens, of allebei worden gebaseerd.
- Segmenten kunnen op aanvraag of continu worden geëvalueerd. Wanneer geëvalueerd op bestelling, worden alle profielgegevens overgegaan door de segmentdefinities in één keer. Wanneer voortdurend geëvalueerd, stromen de gegevens door segmentdefinities aangezien het ingaat [!DNL Platform].

Leer hoe te om segmenten in UI te bepalen, zie de gids [van de Bouwer van het](./ui/overview.md)Segment. Zie de zelfstudie over het [maken van segmenten met de API](./tutorials/create-a-segment.md)voor informatie over het maken van segmentdefinities met de API.