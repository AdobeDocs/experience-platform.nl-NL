---
title: Publiek Veelgestelde vragen
description: Ontdek antwoorden op veelgestelde vragen over het publiek.
source-git-commit: 4dbd20dd3ac596052a3390eb6d3731fac7095c0d
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---


# Veelgestelde vragen

Adobe Experience Platform [!DNL Segmentation Service] verstrekt een gebruikersinterface en RESTful API die u toestaat om publiek door segmentdefinities of andere bronnen van uw tot stand te brengen [!DNL Real-Time Customer Profile] gegevens. Dit publiek wordt centraal gevormd en gehandhaafd op Platform, en gemakkelijk toegankelijk door om het even welke oplossing van Adobe. Hieronder volgt een lijst met veelgestelde vragen over publiek en segmentatie.

## Heb ik toegang tot het Portaal van het Publiek en de Samenstelling van het Publiek?

Poort van publiek en Audience Composition zijn beschikbaar voor alle klanten van Real-Time CDP Premier en Ultimate (B2C, B2B en B2P Editions) en Journey Optimizer Select, Prime, Ultimate Starter en Ultimate.

Op dit moment worden alleen op profielen gebaseerde soorten publiek ondersteund. Ondersteuning voor publiek op basis van account wordt in een latere release toegevoegd.

## Worden extern geproduceerd vooraf gebouwd publiek gesteund met het Portaal van het Publiek?

Ja, extern gegenereerde, vooraf gebouwde doelgroepen worden ondersteund met Poorten publiek. Op dit moment kunt u een extern gegenereerd publiek importeren via een CSV-bestand. In de toekomst kunt u een publiek toevoegen via batch- of streaminggebaseerde bronconnectors.

## Kan ik extern gegenereerde publieksgegevens combineren met een bestaand profiel in Platform?

Ja, het extern gegenereerde publiek wordt samengevoegd met het bestaande profiel in het Platform als de primaire id&#39;s overeenkomen. Het kan 24 uur duren voordat de gegevens met elkaar in overeenstemming zijn. Als profielgegevens nog niet bestaan, wordt een nieuw profiel gemaakt wanneer de gegevens worden ingevoerd.

## Kan ik een extern gegenereerd publiek gebruiken om andere soorten publiek op te bouwen?

Ja, elk extern gegenereerd publiek wordt weergegeven in de publieksinventaris en kan worden gebruikt bij het opbouwen van publiek binnen het [Segment Builder](./ui/segment-builder.md).

## Kan ik extern geüploade kenmerken gebruiken als onderdeel van segmentatie?

Nee, dat kan niet. Profielkenmerken moeten langetermijnkenmerken zijn, terwijl extern gegenereerde publieksgegevens die worden geüpload alleen contextuele gegevens bevatten die aan dat extern gegenereerde publiek zijn gekoppeld.

De extern gegenereerde contextafhankelijke gegevens van het publiek, of verrijkingskenmerken, zijn: **niet** duurzaam, omdat hun levenscyclus aan het geüploade publiek is gebonden. Als gevolg hiervan zijn deze verrijkingskenmerken vanwege hun voorbijgaande aard **niet** beschikbaar voor gebruik in segmentatie.

Wanneer u uw publiek echter toewijst aan batchbestemmingen of op bestanden gebaseerde bestemmingen, kunt u deze extern gegenereerde verrijkingskenmerken gebruiken om uw publiek en verdere downstreamactiveringen te verhogen.

Voor meer informatie over deze mogelijkheid leest u de handleiding op [publieksgegevens activeren om exportdoelen voor batchprofielen te maken](../destinations/ui/activate-batch-profile-destinations.md#mapping).

## Kan ik extern gegenereerde publiek activeren naar Adobe Journey Optimizer?

Op dit moment, nee. Deze mogelijkheid zal echter in de nabije toekomst beschikbaar zijn.

## Kan ik een extern gegenereerd publiek verwijderen?

Op dit moment, nee. U kunt dit publiek deactiveren of archiveren. In deze status worden profielen **zal** actief blijven voor gebruik in downstreamtoepassingen. Ondersteuning voor het verwijderen van extern gegenereerde soorten publiek wordt toegevoegd aan een volgende release.

## Hoe zal het Portaal van het Publiek en de Samenstelling van het Publiek met de versie van de Gegevens van de Partner van Real-Time CDP in wisselwerking staan?

Het Portaal van het publiek en de Samenstelling van het Publiek zullen met de Gegevens van de Partner op twee manieren in wisselwerking staan:

1. Als u een partner-verstrekte lijst van het Vooruitzicht gebruikend de klasse en het werkschema van het Profiel van het Vooruitzicht ingaat, zullen de vooruitzichten worden bewaard **apart** vanuit profielen van klanten samenvoegen in de profielservice. Dit betekent dat er lijsten met perspectieven worden opgesteld **niet** verschijnt in of het Portaal van de Poorten van de Publiek of de Samenstelling van de Publiek voor gebruik.
2. Als u partner-Geleverde attributen leveraging om te verrijken **bestaand** first-party profielen, die partner-gegeven-verrijkt publiek **zal** verschijnen in zowel Portaal van het Publiek als Samenstelling van het Publiek voor gebruik.

## Kan ik extern gegenereerd publiek gebruiken in Audience Composition?

Op dit moment, nee. Deze mogelijkheid moet echter in de nabije toekomst beschikbaar zijn.

## Kan ik publiek van de Samenstelling van het Publiek naar alle stroomafwaartse bestemmingen en kanalen verzenden?

Op dit moment, nee. Momenteel, kunt u publiek van de Samenstelling van het Publiek in de Campagnes van Adobe Journey Optimizer en Echte - tijd CDP bestemmingen gebruiken. Adobe Journey Optimizer-reizen worden in een toekomstige release ondersteund.

## Zijn er aanwijzingen voor het aantal composities?

Op dit moment kunt u alleen **10** gepubliceerde samenstellingen per sandbox. Deze guardrail zal naar verwachting in een toekomstige release worden verhoogd.

## Wat zijn de werkstroominstructies voor Audience Composition?

De compositiecomponent die als volgt plaatst volgt een stijve structuur:

1. U **altijd** beginnen met de [!UICONTROL Audience] blokkeren om uw startactiviteit te selecteren. U kunt maximaal **één** [!UICONTROL Audience] blokkeren.
2. U kunt desgewenst een [!UICONTROL Exclude] blok dat volgt op het [!UICONTROL Audience] blokkeren.
3. U kunt desgewenst een [!UICONTROL Enrich] blok dat volgt op het [!UICONTROL Exclude] blokkeren.
4. U kunt desgewenst een [!UICONTROL Rank] of [!UICONTROL Split] blokkeren. U kunt **alleen** hebben één van deze blokken per samenstelling.
5. U **altijd** eindigen met een [!UICONTROL Save] blokkeren om uw publiek op te slaan.

Lees voor meer informatie over het gebruik van Audience Composition de [Handleiding voor compositie van publiek](./ui/audience-composition.md).

## Kan ik een Samenstelling van het Publiek in een andere samenstelling gebruiken?

Nee, publiek gemaakt met Audience Composition **kan** worden gebruikt als input in een andere publiekssamenstelling.

## Hoe werkt splitsen in Audience Composition?

Door het publiek te splitsen kunt u het publiek verder onderbrengen in kleinere groepen. Deze splitsing dwingt de fracties tot wederzijdse exclusiviteit. Dit betekent dat als een record voldoet aan de criteria van meerdere gesplitste paden, de record de opdracht **first** pad van links en **niet** toegewezen aan een van de andere paden.

Lees voor meer informatie over het blok Splitsen de [Handleiding voor compositie van publiek](./ui/audience-composition.md#split).

## Kan ik alle segmentatietypen in het werkschema van de Samenstelling van het Publiek gebruiken?

Ja, alle segmentatietypen ([batchsegmentatie, streamingsegmentatie en randsegmentatie](./home.md#evaluate-segments)) worden ondersteund in de workflow Audience Composition. Aangezien composities momenteel echter maar één keer per dag worden uitgevoerd, zelfs als streaming- of Edge-publiek wordt opgenomen, wordt het resultaat gebaseerd op het lidmaatschap van het publiek op het moment dat de compositie werd uitgevoerd.

## Hoe kan ik het lidmaatschap van een profiel in een publiek bevestigen?

Ga naar de pagina met profieldetails van het profiel dat u wilt bevestigen om het publiekslidmaatschap van een profiel te bevestigen. Selecteren **[!UICONTROL Attributes]**, gevolgd door **[!UICONTROL View JSON]** en u kunt bevestigen dat de `segmentMembership` bevat de id van het publiek.
