---
solution: Experience Platform
title: Overzicht van segmentatieservice
description: Leer over de Dienst van de Segmentatie van Adobe Experience Platform en de rol het in het ecosysteem van het Platform speelt.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '1627'
ht-degree: 0%

---

# [!DNL Segmentation Service]-overzicht

Adobe Experience Platform [!DNL Segmentation Service] verstrekt een gebruikersinterface en RESTful API die u toestaat om publiek door segmentdefinities of andere bronnen van uw te creëren [!DNL Real-Time Customer Profile] gegevens. Deze doelgroepen worden centraal geconfigureerd en onderhouden op [!DNL Platform]en gemakkelijk toegankelijk zijn via een Adobe-oplossing.

Dit document biedt een overzicht van [!DNL Segmentation Service] en de rol die het speelt in Adobe Experience Platform.

## Aan de slag met [!DNL Segmentation Service]

U moet de volgende belangrijke termen begrijpen die in dit document worden gebruikt:

- **Segmentering**: Het verdelen van een grote groep individuen (zoals klanten, vooruitzichten, gebruikers, of organisaties) in kleinere groepen die gelijkaardige eigenschappen delen en op gelijkaardige wijze aan marketing strategieën zullen antwoorden.
- **Publiek**: Een verzameling personen die vergelijkbare gedragingen en/of kenmerken delen. Deze verzameling personen kan worden gegenereerd door Adobe Experience Platform met behulp van segmentdefinities (publiek dat door het platform wordt gegenereerd) of op basis van externe bronnen (publiek dat extern wordt gegenereerd).
- **Segmentdefinitie**: De regelreeks Adobe Experience Platform gebruikt om zeer belangrijke kenmerken of gedrag van een doelpubliek te beschrijven.

## Hoe segmentatie werkt

De segmentatie is het proces om specifieke attributen of gedrag te bepalen die door een ondergroep van profielen van uw profielopslag worden gedeeld om een verhandelbare groep mensen van uw klantenbasis te onderscheiden. In een e-mailcampagne met de naam &quot;Hebt u vergeten uw gulders te kopen?&quot; wilt u bijvoorbeeld een publiek van alle gebruikers die in de afgelopen 30 dagen naar schoenen hebben gezocht, maar die geen aankoop hebben gedaan.

Zodra een publiek conceptueel is gedefinieerd, wordt het ingebouwd [!DNL Experience Platform]. Doorgaans worden soorten publiek opgebouwd door de marketeter of publieksspecialist, hoewel sommige organisaties de voorkeur geven aan het maken ervan door hun marketingafdeling, in samenwerking met hun gegevensanalisten. Bij het bekijken van de gegevens die worden verzonden naar [!DNL Platform], kan de gegevensanalist het publiek op twee manieren tot stand brengen - of door een segmentdefinitie te creëren door te selecteren welke gebieden en waarden zullen worden gebruikt om de regels of de voorwaarden van het publiek te bouwen, of door een publiek samen te stellen gebruikend de Samenstelling van de Publiek.

## Soorten publiek maken

Op Adobe Experience Platform kunnen soorten publiek op twee verschillende manieren tot stand worden gebracht: rechtstreeks samengesteld als publiek of door middel van op platform gebaseerde segmentdefinities.

### Samenstelling publiek

Wanneer u een publiek rechtstreeks samenstelt op Platform, kunt u de Samenstelling van het publiek gebruiken. Als u wilt leren hoe u Audience Composition kunt gebruiken om een publiek te maken, leest u de [Hulplijn Audience Composition](./ui/audience-composition.md) voor meer informatie .

### Segmentdefinities

Of ze zijn gemaakt met de API of met de [!DNL Segment Builder]segmentdefinities worden uiteindelijk gedefinieerd met [!DNL Profile Query Language] (PQL). Dit is waar de conceptuele segmentdefinitie in de gebouwde taal wordt beschreven om profielen terug te winnen die aan de criteria voldoen. Zie de klasse [PQL-overzicht](./pql/overview.md).

Leren hoe u segmenten kunt maken en gebruiken in het dialoogvenster [!DNL Segment Builder] (de UI-implementatie van [!DNL Segmentation Service]), zie de [Handleiding Segment Builder](./ui/overview.md).

Raadpleeg de zelfstudie voor informatie over het samenstellen van segmentdefinities met behulp van de API [segmentdefinities maken met de API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Als een schema wordt uitgebreid, moeten alle toekomstige uploads nieuwe toegevoegde gebieden dienovereenkomstig bijwerken. Voor meer informatie over aanpassen [!DNL Experience Data Model] (XDM), ga naar [Zelfstudie Schema-editor](../xdm/tutorials/create-schema-ui.md).
>
>Bovendien, als een de vervalwaarde van de Gebeurtenis van de Ervaring op de dataset wordt toegelaten, zou dit het lidmaatschap van de gecreeerde segmentdefinitie kunnen beïnvloeden. Lees de handleiding op [Verlopen van gebeurtenissen beleven](../profile/event-expirations.md) voor meer informatie over hoe deze eigenschap segmentatie kan beïnvloeden.

## Soorten publiek evalueren {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Evaluatiemethoden"
>abstract="Het platform biedt momenteel ondersteuning voor drie methoden om het publiek te evalueren: streamingsegmentatie, batchsegmentatie en randsegmentatie."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Streaming evaluatie"
>abstract="Streaming segmentatie is een doorlopend proces voor gegevensselectie dat uw publiek bijwerkt als reactie op gebruikersactiviteit."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html" text="Evalueer gebeurtenissen in bijna real time met het stromen segmentatie"

Het platform biedt momenteel ondersteuning voor drie methoden om het publiek te evalueren: streamingsegmentatie, batchsegmentatie en randsegmentatie.

### Streaming segmentering {#streaming}

Streaming segmentatie is een doorlopend proces voor gegevensselectie dat uw publiek bijwerkt als reactie op gebruikersactiviteit. Zodra een publiek is gebouwd en opgeslagen, wordt de segmentdefinitie toegepast op inkomende gegevens aan [!DNL Real-Time Customer Profile]. Toevoegingen en verwijderingen voor het publiek worden regelmatig verwerkt, zodat het doelpubliek relevant blijft.

Voor meer informatie over streamingsegmentatie leest u de [documentatie over streamingsegmentatie](./api/streaming-segmentation.md).

### Batchsegmentatie {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Batchevaluatie"
>abstract="Als alternatief voor een lopend proces van de gegevensselectie, verplaatst de partijsegmentatie alle profielgegevens in één keer door segmentdefinities om het overeenkomstige publiek te veroorzaken. Nadat u het publiek hebt gemaakt, wordt het opgeslagen en opgeslagen zodat u het voor gebruik kunt exporteren."

Als alternatief voor een lopend proces van de gegevensselectie, verplaatst de partijsegmentatie alle profielgegevens in één keer door segmentdefinities om het overeenkomstige publiek te veroorzaken. Nadat het publiek is gemaakt, wordt het opgeslagen en opgeslagen zodat u het voor gebruik kunt exporteren.

Het batchpubliek wordt automatisch elke 24 uur geëvalueerd. Als u een partijpubliek op bestelling wilt evalueren, kunt u een segmentbaan gebruiken. Lees voor meer informatie over segmenttaken de [segmenttaakdocumentatie](./api/segment-jobs.md).

### Randsegmentatie {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Edge-evaluatie"
>abstract="De segmentatie van de rand is de capaciteit om segmenten in Platform op het Netwerk van de Rand onmiddellijk te evalueren, toelatend de kwesties van het de verpersoonlijkingsgebruik van zelfde-pagina en volgende-pagina."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html" text="Edge segmentation UI-hulplijn"

De segmentatie van de rand is de capaciteit om segmenten in Platform onmiddellijk te evalueren [op het Edge-netwerk](../edge/home.md)en maakt het gebruik van hoofdletters en kleine letters mogelijk voor het aanpassen van pagina&#39;s.

Voor meer informatie over randsegmentatie leest u de optie [API-documentatie](./api/edge-segmentation.md) of de [UI-documentatie](./ui/edge-segmentation.md).

## Toegang tot segmenteringsresultaten

Als u wilt leren hoe u toegang krijgt tot een geëxporteerd publiek, raadpleegt u de [zelfstudie segmentdefinitiebeoordeling](./tutorials/evaluate-a-segment.md).

## Metagegevens voor segmentdefinitie

Metagegevens voor segmentdefinitie vergemakkelijken indexering als een van uw doelgroepen opnieuw moet worden gebruikt en/of moet worden gecombineerd.

Een segmentdefinitie samenstellen (via de API of [!DNL Segment Builder]) vereist dat u een naam definieert en beleid voor samenvoegen.

### Segmentdefinitienamen

Wanneer u een nieuwe segmentdefinitie maakt, moet u een naam opgeven. De segmentdefinitienaam wordt gebruikt om een bepaalde segmentdefinitie onder de inzameling te identificeren die door wordt gebouwd [!DNL Segmentation Service]. Segmentdefinitienamen moeten daarom beschrijvend, beknopt en uniek zijn.

>[!NOTE]
>
>Wanneer het plannen van een segmentdefinitie, herinner dat de segmentdefinities van, en gecombineerd met, een andere segmentdefinitie kunnen worden van verwijzingen voorzien. Wanneer het selecteren van een naam, overweeg de mogelijkheid dat uw segmentdefinitie herbruikbare gedeelten kan bevatten.

### Beleid samenvoegen

Beleid voor samenvoegen is regels die worden gebruikt door [!DNL Profile] om te bepalen hoe de gegevens in een verenigde mening onder bepaalde voorwaarden voorrang zullen krijgen en worden gecombineerd.

Als er geen samenvoegingsbeleid is gedefinieerd, wordt de standaardwaarde [!DNL Platform] samenvoegbeleid wordt gebruikt. Als u liever een samenvoegingsbeleid wilt gebruiken dat specifiek is voor uw organisatie, kunt u uw eigen beleid maken en dit markeren als de standaardinstelling van uw organisatie.

Meer informatie over het samenvoegbeleid vindt u in het gedeelte [handleiding voor samenvoegbeleid](../profile/api/merge-policies.md).

>[!NOTE]
>
>De schatting van de omvang van het publiek is gebaseerd op het standaardbeleid voor het samenvoegen van profielen van de organisatie.

### Metagegevens andere segmentdefinitie

Naast naam- en samenvoegbeleid, [!DNL Segment Builder] biedt u een extra gebied van beschrijvingsmeta-gegevens aan waar u het doel van uw segmentdefinitie kunt samenvatten.

## Geavanceerde segmentatiefuncties

Segmentdefinities kunnen worden geconfigureerd om voortdurend een publiek te genereren door [streaming data-invoer](../ingestion/streaming-ingestion/overview.md) met een van de volgende geavanceerde segmentatiefuncties:
- [Opeenvolgende segmentatie](#sequential)
- [Dynamische segmentatie](#dynamic)
- [Segmentatie van meerdere entiteiten](#multi-entity)

Deze geavanceerde functies worden in de volgende secties nader besproken.

### Opeenvolgende segmentatie {#sequential}

Een standaardreis van de gebruiker is sequentieel van aard. Met Adobe Experience Platform kunt u een geordende reeks doelgroepen definiëren die deze reis weerspiegelen. Daarom kunt u sequenties van gebeurtenissen vastleggen zoals deze zich voordoen. U kunt gebeurtenissen in de gewenste volgorde rangschikken met de tijdlijn van de visuele gebeurtenis in het dialoogvenster [!DNL Segment Builder].

Een voorbeeld van een klantenreis die opeenvolgende segmentatie zou vereisen zou productmening > product toevoegen > controle > Geen aankoop zijn.

### Dynamische segmentatie {#dynamic}

Dynamische segmentatie lost de scalability problemen op die markten traditioneel worden geconfronteerd wanneer het opbouwen van publiek voor marketing campagnes.

In tegenstelling tot statische segmentatie die u vereist om elk mogelijk gebruiksgeval uitdrukkelijk en herhaaldelijk te vangen, gebruikt de dynamische segmentatie variabelen om de regellogica te bouwen en dynamisch verhoudingen uit te drukken.

Om de waarde van deze geavanceerde segmenteringseigenschap te illustreren, overweeg een gegevensarchitect die met een telleraar samenwerkt om klanten te identificeren die aankopen buiten hun huisstaat maakten.

De statische segmentatie vereist u om individuele segmenten met een uniek attribuut van de huisstaat te bepalen, alvorens voor aankoopgebeurtenissen te filtreren die niet de huisstaat evenaren. Een expliciete segmentdefinitie van dit type zou &quot;Ik zoek mensen van Utah waar de staat van hun aankoop niet Utah is&quot;lezen. Als u een publiek wilt maken met deze methode, moet u één segmentdefinitie definiëren voor elke staat in de VS, voor in totaal 50 segmenten.

Als resultaat van de verschillende combinaties van de segmentdefinitie die onvermijdelijk voorkomen aangezien u schrapt, wordt het handproces dat voor statische segmentatie wordt vereist meer tijdrovend, verminderend uw algemene efficiency.

Door een variabele toe te wijzen aan het attribuut van de koopstaat, vereenvoudigt uw dynamische segmentdefinitie om &quot;me een aankoop te vinden waar de staat van die aankoop niet gelijk aan de huisstaat van de klant is&quot;. Zo kunt u vervolgens 50 statische segmenten verenigen in één dynamische segmentdefinitie.

### Segmentatie van meerdere entiteiten {#multi-entity}

Met de geavanceerde functie voor segmentatie van meerdere entiteiten kunt u [!DNL Real-Time Customer Profile] gegevens met aanvullende gegevens op basis van producten, opslagruimten of andere niet-natuurlijke personen, ook wel &quot;dimensie-entiteiten&quot; genoemd. Dientengevolge, [!DNL Segmentation Service] heeft tijdens de segmentdefinitie toegang tot aanvullende velden alsof deze native zijn voor de [!DNL Profile] gegevensopslag. De segmentatie van meerdere entiteiten verstrekt flexibiliteit wanneer het identificeren van publiek dat op gegevens wordt gebaseerd relevant voor uw unieke bedrijfsbehoeften. Raadpleeg de klasse [segmentatiegids voor meerdere entiteiten](multi-entity-segmentation.md).

## [!DNL Segmentation Service] gegevenstypen

[!DNL Segmentation Service] ondersteunt diverse primitieve en complexe gegevenstypen. Gedetailleerde informatie, waaronder een lijst met ondersteunde gegevenstypen, kunt u vinden in de [supported data types guide](./data-types.md).

## Volgende stappen

[!DNL Segmentation Service] biedt een geconsolideerde workflow om publiek te maken van [!DNL Real-Time Customer Profile] gegevens.

Voor meer informatie bij het gebruiken van de Dienst UI van de Segmentatie, gelieve te lezen [Overzicht van de gebruikersinterface van Segmentatieservice](./ui/overview.md).

Als u wilt leren hoe u een publiek kunt samenstellen in de gebruikersinterface, leest u de [Hulplijn Audience Composition](./ui/audience-composition.md). Leer hoe te om segmentdefinities in UI te bepalen, zie [Handleiding Segment Builder](./ui/overview.md). Raadpleeg de zelfstudie voor informatie over het samenstellen van segmentdefinities met behulp van de API [segmentdefinities maken met de API](./tutorials/create-a-segment.md).
