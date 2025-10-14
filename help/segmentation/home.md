---
solution: Experience Platform
title: Overzicht van segmentatieservice
description: Meer informatie over de Adobe Experience Platform Segmentation Service en de rol die deze speelt in het ecosysteem van Experience Platform.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 0a9028beca36b46d6228c0038366bbac5d32603c
workflow-type: tm+mt
source-wordcount: '1679'
ht-degree: 1%

---

# [!DNL Segmentation Service]-overzicht

Adobe Experience Platform [!DNL Segmentation Service] biedt een gebruikersinterface en de RESTful-API waarmee u een publiek kunt maken via segmentdefinities of andere bronnen op basis van uw [!DNL Real-Time Customer Profile] -gegevens. Deze doelgroepen worden centraal geconfigureerd en onderhouden op [!DNL Experience Platform], en zijn gemakkelijk toegankelijk via elke Adobe-toepassing.

Dit document biedt een overzicht van [!DNL Segmentation Service] en de rol die het speelt in Adobe Experience Platform.

## Aan de slag met [!DNL Segmentation Service]

U moet de volgende belangrijke termen begrijpen die in dit document worden gebruikt:

- **Publiek**: Een inzameling van mensen die gelijkaardig gedrag en/of kenmerken delen. Deze verzameling personen kan worden gegenereerd door Adobe Experience Platform met behulp van segmentdefinities (door Experience-Platform gegenereerde doelgroep) of op basis van externe bronnen (extern gegenereerde doelgroep).
- **de definitie van het Segment**: De regelreeks Adobe Experience Platform gebruikt om zeer belangrijke kenmerken of gedrag van een doelpubliek te beschrijven.
- **Segment**: Het besluit om Profielen in publiek te scheiden.

## Hoe segmentatie werkt

De segmentatie is het proces om specifieke attributen of gedrag te bepalen die door een ondergroep van profielen van uw opslag van het Profiel worden gedeeld om een verhandelbare groep mensen van uw klantenbasis te onderscheiden. In een e-mailcampagne met de naam &quot;Hebt u vergeten uw gulders te kopen?&quot; wilt u bijvoorbeeld een publiek van alle gebruikers die in de afgelopen 30 dagen naar schoenen hebben gezocht, maar die geen aankoop hebben gedaan.

Wanneer een publiek conceptueel is gedefinieerd, wordt het ingebouwd in [!DNL Experience Platform] . Doorgaans worden soorten publiek opgebouwd door de marketeter of publieksspecialist, hoewel sommige organisaties de voorkeur geven aan het maken ervan door hun marketingafdeling, in samenwerking met hun gegevensanalisten. Wanneer de gegevens die naar [!DNL Experience Platform] worden verzonden worden gereviseerd, kan de gegevensanalist het publiek op twee manieren maken: door een segmentdefinitie te maken door te selecteren welke velden en waarden worden gebruikt om de regels of voorwaarden van het publiek te maken, of door een publiek samen te stellen met de compositie van het publiek.

## Soorten publiek maken

Op Adobe Experience Platform kunt u een publiek op meerdere manieren maken, bijvoorbeeld via composities, segmentdefinities, gefedereerde gegevens en Gegevens-Distiller.

### Samenstelling publiek

Wanneer u een publiek rechtstreeks samenstelt in Experience Platform, kunt u Audience Composition gebruiken. Leren hoe te om de Samenstelling van het Publiek te gebruiken om een publiek tot stand te brengen, gelieve de [&#x200B; gids van de Samenstelling van het Publiek &#x200B;](./ui/audience-composition.md) voor meer informatie te lezen.

### Segmentdefinities

Segmentdefinities worden uiteindelijk gedefinieerd met [!DNL Profile Query Language] (PQL), ongeacht of ze met de API of met [!DNL Segment Builder] zijn gemaakt. Dit is waar de conceptuele segmentdefinitie in de gebouwde taal wordt beschreven om profielen terug te winnen die aan de criteria voldoen. Voor meer informatie, zie het [&#x200B; overzicht van PQL &#x200B;](./pql/overview.md).

Leren om segmenten in [!DNL Segment Builder] (de implementatie UI van [!DNL Segmentation Service]) tot stand te brengen en te gebruiken, zie de [&#x200B; gids van de Bouwer van het Segment &#x200B;](./ui/segment-builder.md).

Voor informatie bij de bouw van segmentdefinities die API gebruiken, zie het leerprogramma bij [&#x200B; het creëren van segmentdefinities gebruikend API &#x200B;](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Als een schema wordt uitgebreid, moeten alle toekomstige uploads nieuwe toegevoegde gebieden dienovereenkomstig bijwerken. Voor meer informatie bij het aanpassen [!DNL Experience Data Model] (XDM), bezoek het [&#x200B; leerprogramma van de Redacteur van het Schema &#x200B;](../xdm/tutorials/create-schema-ui.md).
>
>Bovendien, als een de vervalwaarde van de Gebeurtenis van de Ervaring op de dataset wordt toegelaten, zou dit het lidmaatschap van de gecreeerde segmentdefinitie kunnen beïnvloeden. Gelieve te lezen de gids over [&#x200B; Verlopen van de Gebeurtenis van de Ervaring &#x200B;](../profile/event-expirations.md) voor meer informatie over hoe deze eigenschap segmentatie kan beïnvloeden.

### Samenstelling van Federated-doelgroep {#fac}

Naast publiekssamenstellingen en segmentdefinities kunt u Adobe Federated Audience Composition gebruiken om nieuwe soorten publiek te maken van bedrijfsgegevenssets zonder onderliggende gegevens te kopiëren en die soorten publiek op te slaan in Adobe Experience Platform Audience Portal. U kunt bestaande soorten publiek in Adobe Experience Platform ook verrijken door samengestelde publieksgegevens te gebruiken die van het entrepot van ondernemingsgegevens zijn gefedereerd. Gelieve te lezen de gids op [&#x200B; Federated de Samenstelling van het Publiek &#x200B;](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/home).

## Soorten publiek evalueren {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Evaluatiemethoden"
>abstract="Experience Platform biedt momenteel ondersteuning voor drie methoden om het publiek te evalueren: streamingsegmentatie, batchsegmentatie en randsegmentatie."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Streaming evaluatie"
>abstract="Streaming segmentatie is een doorlopend proces voor gegevensselectie dat uw publiek bijwerkt als reactie op gebruikersactiviteit."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/methods/streaming-segmentation.html?lang=nl-NL" text="Evalueer gebeurtenissen in bijna real time met het stromen segmentatie"

Experience Platform biedt momenteel ondersteuning voor drie methoden om het publiek te evalueren: streamingsegmentatie, batchsegmentatie en randsegmentatie.

### Streaming segmentering {#streaming}

Streaming segmentatie is een doorlopend proces voor gegevensselectie dat uw publiek bijwerkt als reactie op gebruikersactiviteit. Nadat een publiek is samengesteld en opgeslagen, wordt de segmentdefinitie toegepast op binnenkomende gegevens in [!DNL Real-Time Customer Profile] . Toevoegingen en verwijderingen voor het publiek worden regelmatig verwerkt, zodat het doelpubliek relevant blijft.

Meer over het stromen segmentatie leren, te lezen gelieve de [&#x200B; het stromen segmentatiedocumentatie &#x200B;](./methods/streaming-segmentation.md).

### Batchsegmentatie {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Batchevaluatie"
>abstract="Als alternatief voor een lopend proces van de gegevensselectie, verplaatst de partijsegmentatie alle profielgegevens in één keer door segmentdefinities om het overeenkomstige publiek te veroorzaken. Nadat u het publiek hebt gemaakt, wordt het opgeslagen en opgeslagen zodat u het voor gebruik kunt exporteren."

Als alternatief voor een lopend proces van de gegevensselectie, verplaatst de partijsegmentatie alle profielgegevens in één keer door segmentdefinities om het overeenkomstige publiek te veroorzaken. Nadat het publiek is gemaakt, wordt het opgeslagen en opgeslagen zodat u het voor gebruik kunt exporteren.

Het batchpubliek wordt automatisch elke 24 uur geëvalueerd. Als u een partijpubliek op bestelling wilt evalueren, kunt u een segmentbaan gebruiken. Om meer over segmentbanen te leren, te lezen gelieve de [&#x200B; documentatie van segmentbanen &#x200B;](./api/segment-jobs.md).

### Edge-segmentatie {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Edge-evaluatie"
>abstract="Edge-segmentatie is de mogelijkheid om segmenten in Experience Platform ogenblikkelijk op de Edge Network te evalueren, zodat gebruikers van dezelfde pagina en van volgende pagina&#39;s met een eigen personalisatie kunnen werken."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/methods/edge-segmentation.html?lang=nl-NL" text="Edge-segmentatiegids"

De segmentatie van Edge is de capaciteit om segmenten in Experience Platform onmiddellijk [&#x200B; op Edge Network &#x200B;](../landing/edge-and-hub-comparison.md) te evalueren, toelatend zelfde-pagina en volgende-pagina verpersoonlijkingsgebruiksgevallen.

Meer over randsegmentatie leren, te lezen gelieve het [&#x200B; overzicht van de randsegmentatie &#x200B;](./methods/edge-segmentation.md).

## Toegang tot segmenteringsresultaten

Leren hoe te om tot een geëxporteerd publiek toegang te hebben, zie het [&#x200B; zelfstudie van de segmentdefinitieevaluatie &#x200B;](./tutorials/evaluate-a-segment.md).

## Metagegevens voor segmentdefinitie

Metagegevens voor segmentdefinitie vergemakkelijken indexering als een van uw doelgroepen opnieuw moet worden gebruikt en/of moet worden gecombineerd.

Voor het samenstellen van een segmentdefinitie (via de API of [!DNL Segment Builder] ) moet u een naam definiëren en beleid voor samenvoegen definiëren.

### Segmentdefinitienamen

Wanneer u een nieuwe segmentdefinitie maakt, moet u een naam opgeven. De segmentdefinitienaam wordt gebruikt om een bepaalde segmentdefinitie onder de inzameling te identificeren die door [!DNL Segmentation Service] wordt gebouwd. Segmentdefinitienamen moeten daarom beschrijvend, beknopt en uniek zijn.

>[!NOTE]
>
>Wanneer het plannen van een segmentdefinitie, herinner dat de segmentdefinities van, en gecombineerd met, een andere segmentdefinitie kunnen worden van verwijzingen voorzien. Wanneer het selecteren van een naam, overweeg de mogelijkheid dat uw segmentdefinitie herbruikbare gedeelten kan bevatten.

### Beleid samenvoegen

Het beleid van de fusie is regels die door [!DNL Profile] worden gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en in een verenigde mening onder bepaalde voorwaarden zullen worden gecombineerd.

Als er geen samenvoegbeleid is gedefinieerd, wordt het standaard [!DNL Experience Platform] samenvoegbeleid gebruikt. Als u liever een samenvoegingsbeleid wilt gebruiken dat specifiek is voor uw organisatie, kunt u uw eigen beleid maken en dit markeren als de standaardinstelling van uw organisatie.

Meer informatie over fusiebeleid kan in de [&#x200B; gids van het samenvoegingsbeleid &#x200B;](../profile/api/merge-policies.md) worden gevonden.

>[!NOTE]
>
>De schatting van de omvang van het publiek is gebaseerd op het standaardbeleid voor het samenvoegen van profielen van de organisatie.

### Metagegevens andere segmentdefinitie

Naast naam- en samenvoegbeleid biedt [!DNL Segment Builder] u een extra metagegevensveld voor een beschrijving waarin u het doel van de segmentdefinitie kunt samenvatten.

## Geavanceerde segmentatiefuncties

De definities van het segment kunnen worden gevormd om een publiek op een aan de gang zijnde basis voortdurend te produceren door [&#x200B; het stromen gegevens te combineren ingebed &#x200B;](../ingestion/streaming-ingestion/overview.md) met om het even welke volgende geavanceerde segmenteringseigenschappen:

- [Opeenvolgende segmentatie](#sequential)
- [Dynamische segmentatie](#dynamic)
- [Segmentatie van meerdere entiteiten](#multi-entity)

Deze geavanceerde functies worden in de volgende secties nader besproken.

### Opeenvolgende segmentatie {#sequential}

Een standaardreis van de gebruiker is sequentieel van aard. Met Adobe Experience Platform kunt u een geordende reeks doelgroepen definiëren die deze reis weerspiegelen. Daarom kunt u sequenties van gebeurtenissen vastleggen zoals deze zich voordoen. U kunt gebeurtenissen in de gewenste volgorde rangschikken met de tijdlijn van de visuele gebeurtenis in de [!DNL Segment Builder] .

Een voorbeeld van een klantenreis die opeenvolgende segmentatie zou vereisen zou productmening > product toevoegen > controle > Geen aankoop zijn.

### Dynamische segmentatie {#dynamic}

Dynamische segmentatie lost de scalability problemen op die markten traditioneel worden geconfronteerd wanneer het opbouwen van publiek voor marketing campagnes.

In tegenstelling tot statische segmentatie die u vereist om elk mogelijk gebruiksgeval uitdrukkelijk en herhaaldelijk te vangen, gebruikt de dynamische segmentatie variabelen om de regellogica te bouwen en dynamisch verhoudingen uit te drukken.

Om de waarde van deze geavanceerde segmenteringseigenschap te illustreren, overweeg een gegevensarchitect die met een telleraar samenwerkt om klanten te identificeren die aankopen buiten hun huisstaat maakten.

De statische segmentatie vereist u om individuele segmenten met een uniek attribuut van de huisstaat te bepalen, alvorens voor aankoopgebeurtenissen te filtreren die niet de huisstaat evenaren. Een expliciete segmentdefinitie van dit type zou &quot;Ik zoek mensen van Utah waar de staat van hun aankoop niet Utah is&quot;lezen. Als u een publiek wilt maken met deze methode, moet u één segmentdefinitie definiëren voor elke staat in de VS, voor in totaal 50 segmenten.

Als resultaat van de verschillende combinaties van de segmentdefinitie die onvermijdelijk voorkomen aangezien u schrapt, wordt het handproces dat voor statische segmentatie wordt vereist meer tijdrovend, verminderend uw algemene efficiency.

Door een variabele toe te wijzen aan het attribuut van de koopstaat, vereenvoudigt uw dynamische segmentdefinitie om &quot;me een aankoop te vinden waar de staat van die aankoop niet gelijk aan de huisstaat van de klant is&quot;. Zo kunt u vervolgens 50 statische segmenten verenigen in één dynamische segmentdefinitie.

### Segmentatie van meerdere entiteiten {#multi-entity}

Met de geavanceerde segmentatiefunctie voor meerdere entiteiten kunt u [!DNL Real-Time Customer Profile] -gegevens uitbreiden met aanvullende gegevens die zijn gebaseerd op producten, winkels of andere personen, ook wel &#39;dimensie&#39;-entiteiten genoemd. Als gevolg hiervan heeft [!DNL Segmentation Service] tijdens de segmentdefinitie toegang tot aanvullende velden, alsof deze native zijn in de [!DNL Profile] -gegevensopslag. De segmentatie van meerdere entiteiten verstrekt flexibiliteit wanneer het identificeren van publiek dat op gegevens wordt gebaseerd relevant voor uw unieke bedrijfsbehoeften. Voor meer informatie, met inbegrip van gebruiksgevallen en werkschema&#39;s, verwijs naar de [&#x200B; gids van de multi-entiteitsegmentatie &#x200B;](./tutorials/multi-entity-segmentation.md).

## [!DNL Segmentation Service] gegevenstypen

[!DNL Segmentation Service] ondersteunt diverse primitieve en complexe gegevenstypen. De gedetailleerde informatie, met inbegrip van een lijst van gesteunde gegevenstypes kan in de [&#x200B; gesteunde gids van gegevenstypes &#x200B;](./data-types.md) worden gevonden.

## Volgende stappen

[!DNL Segmentation Service] biedt een geconsolideerde workflow voor het opbouwen van soorten publiek op basis van [!DNL Real-Time Customer Profile] -gegevens.

Voor meer informatie bij het gebruiken van de Dienst UI van de Segmentatie, te lezen gelieve het [&#x200B; overzicht UI van de Dienst van de Segmentatie &#x200B;](./ui/overview.md).

Leren hoe te om publiek in UI samen te stellen, gelieve de [&#x200B; gids van de Samenstelling van het publiek &#x200B;](./ui/audience-composition.md) te lezen. Leren hoe te om segmentdefinities in UI te bepalen, zie de [&#x200B; gids van de Bouwer van het Segment &#x200B;](./ui/overview.md). Voor informatie bij de bouw van segmentdefinities die API gebruiken, zie het leerprogramma bij [&#x200B; het creëren van segmentdefinities gebruikend API &#x200B;](./tutorials/create-a-segment.md).
