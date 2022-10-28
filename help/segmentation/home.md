---
keywords: Experience Platform;huis;populaire onderwerpen;segmentatie;Segmentatie;segmentservice;segment;Segment;Segmenten;segmenten
solution: Experience Platform
title: Overzicht van segmentatieservice
topic-legacy: overview
description: Leer over de Dienst van de Segmentatie van Adobe Experience Platform en de rol het in het ecosysteem van het Platform speelt.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 0%

---

# [!DNL Segmentation Service]-overzicht

Adobe Experience Platform [!DNL Segmentation Service] verstrekt een gebruikersinterface en RESTful API die u toestaat om segmenten te bouwen en publiek van uw te produceren [!DNL Real-time Customer Profile] gegevens. Deze segmenten worden centraal geconfigureerd en onderhouden op [!DNL Platform]en gemakkelijk toegankelijk zijn door elke Adobe-oplossing.

Dit document biedt een overzicht van [!DNL Segmentation Service] en de rol die het speelt in Adobe Experience Platform.

## Aan de slag met [!DNL Segmentation Service]

Het is belangrijk dat u de volgende belangrijke termen kent die in dit document worden gebruikt:

- **Segmentering**: Het verdelen van een grote groep individuen (zoals klanten, vooruitzichten, gebruikers, of organisaties) in kleinere groepen die gelijkaardige eigenschappen delen en op gelijkaardige wijze aan marketing strategieën zullen antwoorden.
- **Segmentdefinitie**: De regelreeks die wordt gebruikt om zeer belangrijke kenmerken of gedrag van een doelpubliek te beschrijven. Zodra geconceptualiseerd, worden de regels die in een segmentdefinitie worden geschetst gebruikt om kwalificerende publieksleden voor een segment te bepalen.
- **Publiek**: De resulterende set profielen die voldoen aan de criteria van een segmentdefinitie.

## Hoe segmentatie werkt

De segmentatie is het proces om specifieke attributen of gedrag te bepalen die door een ondergroep van profielen van uw profielopslag worden gedeeld om een verhandelbare groep mensen van uw klantenbasis te onderscheiden. In een e-mailcampagne met de naam &quot;Hebt u vergeten uw gulders te kopen?&quot; wilt u bijvoorbeeld een publiek van alle gebruikers die in de afgelopen 30 dagen naar schoenen hebben gezocht, maar die geen aankoop hebben gedaan.

Zodra een segment conceptueel is gedefinieerd, wordt het ingebouwd [!DNL Experience Platform]. Doorgaans worden segmenten samengesteld door de marketeter of publieksspecialist, maar sommige organisaties geven de voorkeur aan het maken ervan door hun marketingafdeling, in samenwerking met hun gegevensanalisten. Bij het bekijken van de gegevens die worden verzonden naar [!DNL Platform]De gegevensanalist stelt de segmentdefinitie samen door te selecteren welke velden en waarden worden gebruikt om de regels of voorwaarden van het segment op te bouwen. Dit wordt gedaan gebruikend of UI of API.

## Segmenten maken

Of ze zijn gemaakt met de API of met de [!DNL Segment Builder], segmenten worden uiteindelijk gedefinieerd met [!DNL Profile Query Language] (PQL). Dit is waar de conceptuele segmentdefinitie in de gebouwde taal wordt beschreven om profielen terug te winnen die aan de criteria voldoen. Zie voor meer informatie de [PQL-overzicht](./pql/overview.md).

Leren hoe u segmenten kunt maken en gebruiken in het dialoogvenster [!DNL Segment Builder] (de UI-implementatie van [!DNL Segmentation Service]), zie de [Handleiding Segment Builder](./ui/overview.md).

Raadpleeg de zelfstudie voor informatie over het samenstellen van segmentdefinities met behulp van de API [publiekssegmenten maken met behulp van de API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Als een schema wordt uitgebreid, moeten alle toekomstige uploads nieuwe toegevoegde gebieden dienovereenkomstig bijwerken. Voor meer informatie over aanpassen [!DNL Experience Data Model] (XDM), ga naar [Zelfstudie Schema Editor](../xdm/tutorials/create-schema-ui.md).
>
>Bovendien, als een waarde van de Vervaldatum van de Gebeurtenis van de Ervaring op de dataset wordt toegelaten, zou dit het lidmaatschap van het gecreeerde segment kunnen beïnvloeden. Lees de handleiding op [Verlopen van gebeurtenissen beleven](../profile/event-expirations.md) voor meer informatie over hoe deze eigenschap segmentatie kan beïnvloeden.

## Segmenten evalueren {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Evaluatiemethoden"
>abstract="Platform ondersteunt momenteel drie methoden voor het evalueren van segmenten: streamingsegmentatie, batchsegmentatie en randsegmentatie."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Streaming evaluatie"
>abstract="Streaming segmentatie is een doorlopend proces voor gegevensselectie dat uw segmenten bijwerkt als reactie op gebruikersactiviteit."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html" text="Evalueer gebeurtenissen in bijna real time met het stromen segmentatie"

Platform ondersteunt momenteel drie methoden voor het evalueren van segmenten: streamingsegmentatie, batchsegmentatie en randsegmentatie.

### Streaming segmentering {#streaming}

Streaming segmentatie is een doorlopend proces voor gegevensselectie dat uw segmenten bijwerkt als reactie op gebruikersactiviteit. Zodra een segment is gebouwd en bewaard, wordt de segmentdefinitie toegepast op inkomende gegevens aan [!DNL Real-time Customer Profile]. Segmenttoevoegingen en verwijderingen worden regelmatig verwerkt, zodat het doelpubliek relevant blijft.

Lees voor meer informatie over streamingsegmentatie de [documentatie over streamingsegmentatie](./api/streaming-segmentation.md).

### Batchsegmentatie {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Batchevaluatie"
>abstract="Als alternatief voor een lopend proces van de gegevensselectie, verplaatst de partijsegmentatie alle profielgegevens in één keer door segmentdefinities om het overeenkomstige publiek te veroorzaken. Nadat u het segment hebt gemaakt, wordt het opgeslagen en opgeslagen zodat u het voor gebruik kunt exporteren."

Als alternatief voor een lopend proces van de gegevensselectie, verplaatst de partijsegmentatie alle profielgegevens in één keer door segmentdefinities om het overeenkomstige publiek te veroorzaken. Zodra gecreeerd, wordt dit segment bewaard en opgeslagen zodat u het voor gebruik kunt uitvoeren.

Batchsegmenten worden automatisch elke 24 uur geëvalueerd. Als u een partijsegment op bestelling wilt evalueren, kunt u een segmentbaan gebruiken. Lees voor meer informatie over segmenttaken de [segmenttaakdocumentatie](./api/segment-jobs.md).

### Randsegmentatie {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Edge-evaluatie"
>abstract="De segmentatie van de rand is de capaciteit om segmenten in Platform onmiddellijk op de Rand van de Ervaring te evalueren, toelatend de kwesties van het de verpersoonlijkingsgebruik van de zelfde pagina en van de volgende pagina."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html" text="Edge segmentation UI-hulplijn"

De segmentatie van de rand is de capaciteit om segmenten in Platform onmiddellijk te evalueren [over Experience Edge](../edge/home.md)en maakt het gebruik van hoofdletters en kleine letters mogelijk.

Voor meer informatie over randsegmentatie leest u de optie [API-documentatie](./api/edge-segmentation.md) of de [UI-documentatie](./ui/edge-segmentation.md).

## Toegang tot segmenteringsresultaten

Als u wilt leren hoe u toegang kunt krijgen tot een geëxporteerd segment, raadpleegt u de [zelfstudie segmentbeoordeling](./tutorials/evaluate-a-segment.md).

## Metagegevens segment

Metagegevens van segmenten maken het indexeren mogelijk als een van uw segmenten opnieuw moet worden gebruikt en/of moet worden gecombineerd.

De segmenten samenstellen (via de API of [!DNL Segment Builder]) vereist dat u een segmentnaam definieert en beleid voor samenvoegen.

### Segmentnamen

Wanneer u een nieuw segment maakt, moet u een segmentnaam opgeven. De segmentnaam wordt gebruikt om een bepaald segment onder de inzameling te identificeren die door wordt gebouwd [!DNL Segmentation Service]. Segmentnamen moeten daarom beschrijvend, beknopt en uniek zijn.

>[!NOTE]
>
>Wanneer het plannen van een segment, herinner dat de segmenten van, en gecombineerd met, een ander segment kunnen worden van verwijzingen voorzien. Houd er bij het selecteren van een naam rekening mee dat uw segment herbruikbare gedeelten kan bevatten.

### Beleid samenvoegen

Beleid voor samenvoegen is regels die worden gebruikt door [!DNL Profile] om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en in een verenigde mening onder bepaalde voorwaarden zullen worden gecombineerd.
Als er geen samenvoegingsbeleid is gedefinieerd, wordt de standaardwaarde [!DNL Platform] samenvoegbeleid wordt gebruikt. Als u liever een samenvoegingsbeleid wilt gebruiken dat specifiek is voor uw organisatie, kunt u uw eigen beleid maken en dit markeren als de standaardinstelling van uw organisatie.

Meer informatie over het samenvoegbeleid vindt u in het gedeelte [handleiding voor samenvoegbeleid](../profile/api/merge-policies.md).

>[!NOTE]
>
>De schatting van de omvang van het publiek is gebaseerd op het standaardbeleid voor het samenvoegen van profielen van de organisatie.

### Andere segmentmetagegevens

Naast segmentnaam en samenvoegbeleid, [!DNL Segment Builder] biedt u een extra de meta-gegevensgebied van de &quot;segmentbeschrijving&quot;waar u het doel van uw segmentdefinitie kunt samenvatten.

## Geavanceerde segmentatiefuncties

De segmenten kunnen worden gevormd om voortdurend een publiek te produceren door te combineren [streaming data-invoer](../ingestion/streaming-ingestion/overview.md) met een van de volgende geavanceerde segmentatiefuncties:
- [Opeenvolgende segmentatie](#sequential)
- [Dynamische segmentatie](#dynamic)
- [Segmentatie van meerdere entiteiten](#multi-entity)

Deze geavanceerde functies worden in de volgende secties nader besproken.

## Opeenvolgende segmentatie {#sequential}

Een standaardreis van de gebruiker is sequentieel van aard. Met Adobe Experience Platform kunt u een geordende reeks segmenten definiëren die deze reis weerspiegelen. Daarom kunt u sequenties van gebeurtenissen vastleggen zoals deze zich voordoen. U kunt gebeurtenissen in de gewenste volgorde rangschikken met de tijdlijn van de visuele gebeurtenis in het dialoogvenster [!DNL Segment Builder].

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

Met de geavanceerde functie voor segmentatie van meerdere entiteiten kunt u [!DNL Real-time Customer Profile] gegevens met aanvullende gegevens op basis van producten, opslagruimten of andere niet-natuurlijke personen, ook wel &quot;dimensie-entiteiten&quot; genoemd. Dientengevolge [!DNL Segmentation Service] heeft tijdens de segmentdefinitie toegang tot aanvullende velden alsof deze native zijn voor de [!DNL Profile] gegevensopslag. De segmentatie van meerdere entiteiten verstrekt flexibiliteit wanneer het identificeren van publiek dat op gegevens wordt gebaseerd relevant voor uw unieke bedrijfsbehoeften. Raadpleeg voor meer informatie, zoals gebruiksgevallen en workflows, de [segmentatiegids voor meerdere entiteiten](multi-entity-segmentation.md).

## [!DNL Segmentation Service] gegevenstypen

[!DNL Segmentation Service] ondersteunt diverse primitieve en complexe gegevenstypen. Gedetailleerde informatie, waaronder een lijst met ondersteunde gegevenstypen, kunt u vinden in de [supported data types guide](./data-types.md).

## Volgende stappen

[!DNL Segmentation Service] biedt een geconsolideerde workflow voor het samenstellen van segmenten van [!DNL Real-time Customer Profile] gegevens. Samenvattend:

- [!DNL Segmentation] Dit is het proces waarbij u een subset van profielen definieert vanuit het profielarchief, zodat u gedrag of kenmerken van een gewenste verhandelbare groep kunt karakteriseren. [!DNL Segmentation Service] maakt dit proces mogelijk.
- Wanneer het plannen van een segment, houd in mening dat een segment van, en gecombineerd met, een ander segment kan worden van verwijzingen voorzien.
- Een segment kan van regels worden gebouwd die op profielgegevens, verwante tijdreeksgegevens, of allebei worden gebaseerd.
- Segmenten kunnen op aanvraag of continu worden geëvalueerd. Wanneer geëvalueerd op bestelling, worden alle profielgegevens overgegaan door de segmentdefinities in één keer. Bij continue evaluatie worden de gegevens door segmentdefinities gestreamd terwijl deze worden ingevoerd [!DNL Platform].

Als u wilt leren hoe u segmenten in de gebruikersinterface definieert, raadpleegt u de [Handleiding Segment Builder](./ui/overview.md). Raadpleeg de zelfstudie voor informatie over het samenstellen van segmentdefinities met behulp van de API [segmenten maken met de API](./tutorials/create-a-segment.md).
