---
keywords: Experience Platform;huis;populaire onderwerpen;segmentatie;Segmentatie;segmentservice;segment;Segment;Segmenten;segmenten
solution: Experience Platform
title: Overzicht van segmentatieservice
topic: overzicht
description: Leer over de Dienst van de Segmentatie van Adobe Experience Platform en de rol het in het ecosysteem van het Platform speelt.
translation-type: tm+mt
source-git-commit: 738256021fb583e7dc14fd33f5df193813a6e0bb
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---


# [!DNL Segmentation Service] - overzicht

Adobe Experience Platform [!DNL Segmentation Service] biedt een gebruikersinterface en RESTful API waarmee u segmenten kunt samenstellen en doelgroepen kunt genereren op basis van uw [!DNL Real-time Customer Profile]-gegevens. Deze segmenten worden centraal gevormd en gehandhaafd op [!DNL Platform], en zijn gemakkelijk toegankelijk door om het even welke oplossing van Adobe.

Dit document biedt een overzicht van [!DNL Segmentation Service] en de rol die het speelt in Adobe Experience Platform.

## Aan de slag met [!DNL Segmentation Service]

Het is belangrijk dat u de volgende belangrijke termen kent die in dit document worden gebruikt:

- **Segmentatie**: Het verdelen van een grote groep individuen (zoals klanten, vooruitzichten, gebruikers, of organisaties) in kleinere groepen die gelijkaardige eigenschappen delen en op gelijkaardige wijze aan marketing strategieën zullen antwoorden.
- **Segmentdefinitie**: De regelreeks die wordt gebruikt om zeer belangrijke kenmerken of gedrag van een doelpubliek te beschrijven. Zodra geconceptualiseerd, worden de regels die in een segmentdefinitie worden geschetst gebruikt om kwalificerende publieksleden voor een segment te bepalen.
- **Publiek**: De resulterende set profielen die voldoen aan de criteria van een segmentdefinitie.

## Hoe segmentatie werkt

De segmentatie is het proces om specifieke attributen of gedrag te bepalen die door een ondergroep van profielen van uw profielopslag worden gedeeld om een verhandelbare groep mensen van uw klantenbasis te onderscheiden. In een e-mailcampagne met de naam &quot;Hebt u vergeten uw gulders te kopen?&quot; wilt u bijvoorbeeld een publiek van alle gebruikers die in de afgelopen 30 dagen naar schoenen hebben gezocht, maar die geen aankoop hebben gedaan.

Zodra een segment conceptueel is bepaald, wordt het gebouwd in [!DNL Experience Platform]. Doorgaans worden segmenten samengesteld door de marketeter of publieksspecialist, maar sommige organisaties geven de voorkeur aan het maken ervan door hun marketingafdeling, in samenwerking met hun gegevensanalisten. Bij het bekijken van de gegevens die naar [!DNL Platform] worden verzonden, stelt de gegevensanalist de segmentdefinitie samen door te selecteren welke gebieden en waarden zullen worden gebruikt om de regels of voorwaarden van het segment te bouwen. Dit wordt gedaan gebruikend of UI of API.

## Segmenten maken

Of ze nu zijn gemaakt met de API of met de [!DNL Segment Builder], segmenten worden uiteindelijk gedefinieerd met [!DNL Profile Query Language] (PQL). Dit is waar de conceptuele segmentdefinitie in de gebouwde taal wordt beschreven om profielen terug te winnen die aan de criteria voldoen. Voor meer informatie, zie [PQL overzicht](./pql/overview.md).

Om te leren om segmenten in [!DNL Segment Builder] (de implementatie UI van [!DNL Segmentation Service]) tot stand te brengen en te gebruiken, zie [de gids van de Bouwer van het Segment](./ui/overview.md).

Voor informatie over het bouwen van segmentdefinities die API gebruiken, zie de zelfstudie over [het creëren van publiekssegmenten gebruikend API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Als een schema wordt uitgebreid, moeten alle toekomstige uploads nieuwe toegevoegde gebieden dienovereenkomstig bijwerken. Voor meer informatie bij het aanpassen van [!DNL Experience Data Model] (XDM), bezoek [de zelfstudie van de Redacteur van het Schema](../xdm/tutorials/create-schema-ui.md).

## Segmenten evalueren

Platform ondersteunt momenteel twee methoden voor het evalueren van segmenten: streamingsegmentatie en batchsegmentatie.

### Streaming segmentering

Streaming segmentatie is een doorlopend proces voor gegevensselectie dat uw segmenten bijwerkt als reactie op gebruikersactiviteit. Nadat een segment is gemaakt en opgeslagen, wordt de segmentdefinitie toegepast op inkomende gegevens op [!DNL Real-time Customer Profile]. Segmenttoevoegingen en verwijderingen worden regelmatig verwerkt, zodat het doelpubliek relevant blijft.

Lees de [streamingsegmentatiedocumentatie](./api/streaming-segmentation.md) voor meer informatie over streamingsegmentatie.

### Batchsegmentatie

Als alternatief voor een lopend proces van de gegevensselectie, verplaatst de partijsegmentatie alle profielgegevens in één keer door segmentdefinities om het overeenkomstige publiek te veroorzaken. Zodra gecreeerd, wordt dit segment bewaard en opgeslagen zodat u het voor gebruik kunt uitvoeren.

Segmenten die met batchsegmentatie zijn geëvalueerd, worden om de 24 uur geëvalueerd. Nochtans, voor bestaande segmenten, houdt de stijgende segmentatie segmenten geëvalueerd gebruikend batch segmentatie vers voor maximaal een uur. Om het even welke nieuwe of onlangs gewijzigde segmenten zullen moeten wachten tot de volgende volledige baan van de partijsegmentatie is in werking gesteld om uit stijgende segmentatie voordeel te halen.

Leren hoe te om segmenten te evalueren zie [segment evaluatiezelfstudie](./tutorials/evaluate-a-segment.md).

### Randsegmentatie

De segmentatie van de rand is de capaciteit om segmenten in Platform op de rand onmiddellijk te evalueren, toelatend de zelfde pagina en volgende de gebruikscituaties van de paginagrootte.

Voor meer informatie over randsegmentatie leest u de [API-documentatie](./api/edge-segmentation.md) of de [UI-documentatie](./ui/edge-segmentation.md).

## Toegang tot segmenteringsresultaten

Om te leren hoe te om tot een uitgevoerd segment toegang te hebben, zie [segmentevaluatiezelfstudie](./tutorials/evaluate-a-segment.md).

## Metagegevens segment

Metagegevens van segmenten maken het indexeren mogelijk als een van uw segmenten opnieuw moet worden gebruikt en/of moet worden gecombineerd.

Het samenstellen van uw segmenten (door of API of [!DNL Segment Builder]) vereist dat u een segmentnaam en fusiebeleid bepaalt.

### Segmentnamen

Wanneer u een nieuw segment maakt, moet u een segmentnaam opgeven. De segmentnaam wordt gebruikt om een bepaald segment onder de inzameling te identificeren die door [!DNL Segmentation Service] wordt gebouwd. Segmentnamen moeten daarom beschrijvend, beknopt en uniek zijn.

>[!NOTE]
>
>Wanneer het plannen van een segment, herinner dat de segmenten van, en gecombineerd met, een ander segment kunnen worden van verwijzingen voorzien. Houd er bij het selecteren van een naam rekening mee dat uw segment herbruikbare gedeelten kan bevatten.

### Beleid samenvoegen

Het beleid van de fusie is regels die door [!DNL Profile] worden gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en in een verenigde mening onder bepaalde voorwaarden zullen worden gecombineerd.
Als er geen samenvoegingsbeleid is gedefinieerd, wordt het standaardsamenvoegbeleid [!DNL Platform] gebruikt. Als u liever een samenvoegingsbeleid wilt gebruiken dat specifiek is voor uw organisatie, kunt u uw eigen beleid maken en dit markeren als de standaardinstelling van uw organisatie.

Meer informatie over samenvoegingsbeleid kan in [de gids van het samenvoegbeleid](../profile/api/merge-policies.md) worden gevonden.

>[!NOTE]
>
>De schatting van de omvang van het publiek is gebaseerd op het standaardbeleid voor het samenvoegen van profielen van de organisatie.

### Andere segmentmetagegevens

Naast segmentnaam en samenvoegbeleid, [!DNL Segment Builder] biedt u een extra &quot;segmentbeschrijving&quot;meta-gegevensgebied aan waar u het doel van uw segmentdefinitie kunt samenvatten.

## Geavanceerde segmentatiefuncties

De segmenten kunnen worden gevormd om voortdurend een publiek te produceren door [het stromen gegevensopname](../ingestion/streaming-ingestion/overview.md) met om het even welke volgende geavanceerde segmenteringseigenschappen te combineren:
- [Opeenvolgende segmentatie](#sequential)
- [Dynamische segmentatie](#dynamic)
- [Segmentatie van meerdere entiteiten](#multi-entity)

Deze geavanceerde functies worden in de volgende secties nader besproken.

## Opeenvolgende segmentatie {#sequential}

Een standaardreis van de gebruiker is sequentieel van aard. Met Adobe Experience Platform kunt u een geordende reeks segmenten definiëren die deze reis weerspiegelen. Daarom kunt u sequenties van gebeurtenissen vastleggen zoals deze zich voordoen. U kunt gebeurtenissen in de gewenste volgorde rangschikken met de tijdlijn van de visuele gebeurtenis in [!DNL Segment Builder].

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

Met de geavanceerde functie voor segmentatie van meerdere entiteiten kunt u [!DNL Real-time Customer Profile]-gegevens uitbreiden met aanvullende gegevens die zijn gebaseerd op producten, winkels of andere niet-personen, ook wel &#39;dimensie&#39;-entiteiten genoemd. Als gevolg hiervan heeft [!DNL Segmentation Service] tijdens de segmentdefinitie toegang tot extra velden alsof deze native zijn in de [!DNL Profile]-gegevensopslag. De segmentatie van meerdere entiteiten verstrekt flexibiliteit wanneer het identificeren van publiek dat op gegevens wordt gebaseerd relevant voor uw unieke bedrijfsbehoeften. Raadpleeg de [segmentatiehandleiding voor meerdere entiteiten](multi-entity-segmentation.md) voor meer informatie, zoals gebruiksgevallen en workflows.

## [!DNL Segmentation Service] gegevenstypen

[!DNL Segmentation Service] ondersteunt diverse primitieve en complexe gegevenstypen. Gedetailleerde informatie, waaronder een lijst met ondersteunde gegevenstypen, vindt u in de [ondersteunde gids voor gegevenstypen](./data-types.md).

## Volgende stappen

[!DNL Segmentation Service] biedt een geconsolideerde workflow voor het samenstellen van segmenten op basis van  [!DNL Real-time Customer Profile] gegevens. Samenvattend:

- [!DNL Segmentation] Dit is het proces waarbij u een subset van profielen definieert vanuit het profielarchief, zodat u gedrag of kenmerken van een gewenste verhandelbare groep kunt karakteriseren. [!DNL Segmentation Service] maakt dit proces mogelijk.
- Wanneer het plannen van een segment, houd in mening dat een segment van, en gecombineerd met, een ander segment kan worden van verwijzingen voorzien.
- Een segment kan van regels worden gebouwd die op profielgegevens, verwante tijdreeksgegevens, of allebei worden gebaseerd.
- Segmenten kunnen op aanvraag of continu worden geëvalueerd. Wanneer geëvalueerd op bestelling, worden alle profielgegevens overgegaan door de segmentdefinities in één keer. Wanneer voortdurend geëvalueerd, stromen de gegevens door segmentdefinities aangezien het [!DNL Platform] ingaat.

Leren hoe te om segmenten in UI te bepalen, zie [de gids van de Bouwer van het Segment](./ui/overview.md). Zie de zelfstudie over het maken van segmenten met behulp van de API voor informatie over het maken van segmentdefinities met behulp van de API.[](./tutorials/create-a-segment.md)