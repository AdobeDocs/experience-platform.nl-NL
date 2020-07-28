---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmenteringsservice Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 96b6f820e5d372446c4927e7719aedadb2b11bc9
workflow-type: tm+mt
source-wordcount: '1974'
ht-degree: 0%

---


# Overzicht [!DNL Segmentation Service] van Adobe Experience Platforms

Adobe Experience Platform [!DNL Segmentation Service] verstrekt een gebruikersinterface en RESTful API die u toestaat om segmenten te bouwen en publiek van uw [!DNL Real-time Customer Profile] gegevens te produceren. Deze segmenten worden centraal gevormd en gehandhaafd [!DNL Platform], en gemakkelijk toegankelijk door om het even welke oplossing van Adobe.

Dit document biedt een overzicht van [!DNL Segmentation Service] en de rol die het in Adobe Experience Platform speelt.

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

Een standaardreis van de gebruiker is sequentieel van aard. Met Adobe Experience Platform kunt u een geordende reeks segmenten definiëren die deze reis weerspiegelen en zo reeksen gebeurtenissen vastleggen zoals deze zich voordoen. U kunt gebeurtenissen in de gewenste volgorde rangschikken met de tijdlijn van de visuele gebeurtenis in de [!DNL Segment Builder]tijdlijn.

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

Met de geavanceerde functie voor segmentatie van meerdere entiteiten kunt u segmenten maken met behulp van meerdere XDM-klassen en zo extensies toevoegen aan persoonlijke schema&#39;s. Dit betekent dat u tijdens de segmentdefinitie toegang [!DNL Segmentation Service] kunt krijgen tot aanvullende velden alsof deze native zijn in de profielgegevensopslag.

De segmentatie van meerdere entiteiten verstrekt de flexibiliteit nodig om publiek te identificeren dat op gegevens wordt gebaseerd relevant voor uw bedrijfsbehoeften. Dit proces kan snel en gemakkelijk worden gedaan zonder deskundigheid in het vragen van gegevensbestanden te vereisen. Dit laat u toe om zeer belangrijke gegevens aan uw segmenten toe te voegen zonder het moeten dure veranderingen in gegevensstromen aanbrengen of op een achterste-eindgegevenssamenvoeging wachten.

De volgende video is bedoeld om uw begrip van multi-entiteitsegmentatie te steunen, en schetst zowel multi-entiteitsegmentatie als segmentcontext (segmentlading).

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

### Hoofdlettergebruik: Prijsgerichte promotie

Als u de waarde van deze geavanceerde segmentatiefunctie wilt illustreren, kunt u overwegen om een gegevensarchitect samen te voegen met een marketer.

In dit voorbeeld verbindt de gegevensarchitect gegevens voor een individu (samengesteld uit schema&#39;s met [!DNL XDM Individual Profile] en [!DNL XDM ExperienceEvent] als hun basisklassen) met een andere klasse gebruikend een sleutel. Zodra verbonden, kan de gegevensarchitect of de telleraar deze nieuwe gebieden tijdens segmentdefinitie gebruiken alsof zij aan het schema van de basisklasse inheems waren.

**Het probleem**

De gegevensarchitect en de markator werken beide voor dezelfde kledingdetailhandelaar. De detailhandelaar heeft meer dan 1000 winkels in Noord-Amerika en verlaagt periodiek de productprijzen gedurende hun levenscyclus. Als gevolg hiervan wil de marketeter een speciale campagne voeren om kopers die voor deze objecten hebben gewinkeld de kans te geven ze tegen de verlaagde prijs te kopen.

De middelen van de gegevensarchitect omvatten toegang tot Webgegevens van klant het doorbladeren evenals de gegevens van de karttoevoeging die productSKU herkenningstekens bevatten. Zij hebben ook toegang tot een aparte &quot;producten&quot;-klasse, waar aanvullende productinformatie (inclusief productprijs) wordt opgeslagen. Hun advies is om zich te concentreren op klanten die de afgelopen 14 dagen een product aan hun winkelwagentje hebben toegevoegd, maar het object niet hebben gekocht, waarvan de prijs nu is gedaald.

**De oplossing**

>[!NOTE]
>
>In dit voorbeeld gaan we ervan uit dat de gegevensarchitect al een id-naamruimte heeft ingesteld.

Gebruikend API, brengt de gegevensarchitect de sleutel van het [!DNL ExperienceEvent] schema met de &quot;producten&quot;klasse in verband. Dit staat de gegevensarchitect toe om van de extra gebieden van de &quot;producten&quot;klasse gebruik te maken alsof zij aan het [!DNL ExperienceEvent] schema inheems zijn. Als laatste stap van het configuratiewerk, moet de gegevensarchitect de aangewezen gegevens in brengen [!DNL Real-time Customer Profile]. Dit wordt gedaan door de &quot;producten&quot;dataset voor gebruik met toe te laten [!DNL Profile]. Met het configuratiewerk volledig, of de gegevensarchitect of de telleraar kan het doelsegment binnen bouwen [!DNL Segment Builder].

Zie het overzicht [van de](../xdm/schema/composition.md#union) schemacompositie leren hoe te om verhoudingen over klassen te bepalen XDM.

<!-- ## Personalization payload

Segments can now carry a payload of contextual details to enable deep personalization of Adobe Solutions as well as external non-Adobe applications. These payloads can be added while defining your target segment.

With contextual data built into the segment itself, this advanced Segmentation Service feature allows you to better connect with your customer.

Segment Payload helps you answer questions surrounding your customer’s frame of reference such as:
- What: What product was purchased? What product should be recommended next?
- When: At what time and date did the purchase occur?
- Where: In which store or city did the customer make their purchase?

While this solution does not change the binary nature of segment membership, it does add additional context to each profile through an associated segment membership object. Each segment membership object has the capacity to include three kinds of contextual data:

- **Identifier**: this is the ID for the segment 
- **Attributes**: this would include information about the segment ID such as last qualification time, XDM version, status and so on.
- **Event data**: Specific aspects of experience events which resulted in the profile qualifying for the segment

Adding this specific data to the segment itself allows execution engines to personalize the experience for the customers in their target audience. -->

### Gebruik hoofdletters

Om de waarde van deze geavanceerde segmenteringseigenschap te illustreren, overweeg drie standaardgebruiksgevallen die de uitdagingen illustreren die in marketing toepassingen voorafgaand aan de verhoging van de Lading van het Segment aanwezig waren:
- E-mailpersonalisatie
- E-mailheroriëntering
- Opnieuw richten van advertenties

**E-mailpersonalisatie**

Een marketeer die een e-mailcampagne bouwt kan geprobeerd hebben om een segment voor een doelpubliek te bouwen door recente aankopen van de klantenopslag binnen de laatste drie maanden te gebruiken. In het ideale geval vereist dit segment zowel de naam van het item als de naam van de winkel waar de aankoop is gedaan. Voorafgaand aan verbetering, de uitdaging was het vangen van het opslagherkenningsteken van de aankoopgebeurtenis en het toewijzen van het aan het profiel van die klant.

**E-mailheroriëntering**

Het is vaak complex om segmenten te maken en te kwalificeren voor e-mailcampagnes die gericht zijn op het verlaten van een winkelwagentje. Voorafgaand aan de verbetering, wist welke producten om in een gepersonaliseerd bericht te omvatten moeilijk was toe te schrijven aan de beschikbaarheid van de vereiste gegevens. De gegevens waarvoor de producten werden verlaten zijn gebonden aan ervaringsgebeurtenissen die vroeger om gegevens te controleren en te halen uitbraken.

**Opnieuw richten van advertenties**

Een andere traditionele uitdaging voor marketers is het creëren van advertenties om klanten met verlaten winkelwagentjes te richten. Hoewel de segmentdefinities deze uitdaging aanpasten, was er vóór de verbetering geen formele methode om onderscheid te maken tussen aangekochte en verlaten producten. Nu kunt u specifieke datasets tijdens segmentdefinitie richten.

## [!DNL Segmentation Service] gegevenstypen

[!DNL Segmentation Service] ondersteunt diverse gegevenstypen, waaronder:

- String
- Uniforme resource-id
- Enum
- Getal
- Lang
- Geheel
- Kort
- Byte
- Boolean
- Datum
- Datum/tijd
- Array
- Object
- Kaart
- Gebeurtenissen
- Extern publiek
- Segmenten

Meer gedetailleerde informatie over deze ondersteunde gegevenstypen vindt u in het document [met](./data-types.md)ondersteunde gegevenstypen.

## Volgende stappen

[!DNL Segmentation Service] biedt een geconsolideerde workflow voor het samenstellen van segmenten op basis van [!DNL Real-time Customer Profile] gegevens. Samenvattend:

- [!DNL Segmentation] Dit is het proces waarbij u een subset van profielen definieert vanuit het profielarchief, zodat u gedrag of kenmerken van een gewenste verhandelbare groep kunt karakteriseren. [!DNL Segmentation Service] maakt dit proces mogelijk.
- Wanneer het plannen van een segment, houd in mening dat een segment van, en gecombineerd met, een ander segment kan worden van verwijzingen voorzien.
- Een segment kan van regels worden gebouwd die op profielgegevens, verwante tijdreeksgegevens, of allebei worden gebaseerd.
- Segmenten kunnen op aanvraag of continu worden geëvalueerd. Wanneer geëvalueerd op bestelling, worden alle profielgegevens overgegaan door de segmentdefinities in één keer. Wanneer voortdurend geëvalueerd, stromen de gegevens door segmentdefinities aangezien het ingaat [!DNL Platform].

Leer hoe te om segmenten in UI te bepalen, zie de gids [van de Bouwer van het](./ui/overview.md)Segment. Zie de zelfstudie over het [maken van segmenten met de API](./tutorials/create-a-segment.md)voor informatie over het maken van segmentdefinities met de API.