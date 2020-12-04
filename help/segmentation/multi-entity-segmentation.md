---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment service;segments;Segments;multi-entity;multi-entity segmentation;multi-entity segments;
solution: Experience Platform
title: Segmentatie van meerdere entiteiten
topic: overview
description: De segmentatie van meerdere entiteiten is de capaciteit om de gegevens van het Profiel met extra gegevens uit te breiden die op producten, opslag, of andere niet-profielklassen worden gebaseerd. Zodra verbonden, worden de gegevens van extra klassen beschikbaar alsof zij aan het schema van het Profiel inheems waren.
translation-type: tm+mt
source-git-commit: 4dd5a91146b116953ba180e3f39d24b4e1ec289e
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---


# Segmentatie van meerdere entiteiten

Segmentatie met meerdere entiteiten is een geavanceerde functie die beschikbaar is als onderdeel van Adobe Experience Platform [!DNL Segmentation Service]. Met deze functie kunt u [!DNL Real-time Customer Profile] gegevens uitbreiden met extra gegevens van andere personen (ook wel &#39;dimensie-entiteiten&#39; genoemd) die uw organisatie kan definiëren, zoals gegevens die betrekking hebben op producten of winkels. De segmentatie van meerdere entiteiten verstrekt flexibiliteit wanneer het bepalen van publiekssegmenten die op gegevens relevant voor uw unieke bedrijfsbehoeften worden gebaseerd en kan zonder het hebben van deskundigheid in het vragen van gegevensbestanden worden uitgevoerd. Met de segmentatie van meerdere entiteiten, kunt u zeer belangrijke gegevens aan uw segmenten toevoegen zonder het moeten dure veranderingen in gegevensstromen aanbrengen of op een achterste-eindgegevenssamenvoeging wachten.

## Aan de slag

De segmentatie van meerdere entiteiten vereist een goed begrip van de verschillende diensten van Adobe Experience Platform die bij segmentatie betrokken zijn. Lees de volgende documentatie voordat u doorgaat met deze handleiding:

* [[!DNL Real-time Customer Profile]](../profile/home.md): Verstrekt een verenigd consumentenprofiel in real time, dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
   * [Profielhulplijnen](../profile/guardrails.md): Aanbevolen procedures voor het maken van gegevensmodellen die worden ondersteund door [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Hiermee kunt u segmenten samenstellen op basis van [!DNL Real-time Customer Profile] gegevens.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../xdm/schema/composition.md#union): Leer beste praktijken voor het samenstellen van schema&#39;s die in Experience Platform moeten worden gebruikt.

## Gebruiksscenario’s

Om de waarde van de segmentatie van meerdere entiteiten te illustreren, overweeg drie standaard marketing gebruiksgevallen die de uitdagingen tonen die in de meeste marketing toepassingen aanwezig zijn:

### Aankoopgegevens online en offline combineren

Een marketeer die een e-mailcampagne bouwt kan geprobeerd hebben om een segment voor een doelpubliek te bouwen door recente aankopen van de klantenopslag binnen de laatste drie maanden te gebruiken. In het ideale geval vereist dit segment zowel de naam van het item als de naam van de winkel waar de aankoop is gedaan. Eerder, zou de uitdaging de opslag herkenningsteken van de koopgebeurtenis hebben gevangen en het toewijzen aan een individueel klantenprofiel.

### E-mailherbestemming voor het verlaten van het winkelwagentje

Het is vaak complex om gebruikers te creëren en in segmenten te kwalificeren die kartontroeping richten. Als u weet welke producten u wilt opnemen in een gepersonaliseerde campagne voor heroriëntering, moet u weten welke producten elk individu heeft opgegeven. Deze gegevens zijn gekoppeld aan commerciële gebeurtenissen die voorheen lastig waren om gegevens te controleren en te extraheren.

## Meerdere-entiteitssegmenten maken

Het creëren van een multi-entiteitsegment vereist eerst het bepalen van relaties tussen schema&#39;s alvorens API of de Bouwer UI van het Segment te gebruiken om de segmentdefinitie te bouwen. [!DNL Segmentation]

### Relaties definiëren

Het bepalen van verhoudingen binnen de structuur van uw schema&#39;s van de Gegevens van de Ervaring (XDM) is een integraal deel van multi-entiteitsegmentverwezenlijking. Voor verhoudingen, moet het gebied in de bestemming als primaire identiteit van dat schema worden gemerkt. Een identiteit kan alleen worden gemarkeerd op tekenreeksen en kan niet worden gemarkeerd op arrays. Bovendien, moeten de verhoudingen niet noodzakelijk één-op-één zijn, aangezien u profielen en ervaringsgebeurtenissen met veelvoudige bestemmingen kunt verbinden.

Het bepalen van verhoudingen kan of gebruikend de Registratie API van het Schema of de Redacteur van het Schema worden gedaan. Voor gedetailleerde stappen die tonen hoe te om een verhouding tussen twee schema&#39;s te bepalen, gelieve te kiezen van de volgende leerprogramma&#39;s:

* [Een relatie tussen twee schema&#39;s definiëren met behulp van de API](../xdm/tutorials/relationship-api.md)
* [Het bepalen van een verhouding tussen twee schema&#39;s gebruikend de Redacteur UI van het Schema](../xdm/tutorials/relationship-ui.md)

### Een segment met meerdere entiteiten maken

Zodra u de noodzakelijke verhoudingen XDM hebt bepaald, kunt u beginnen om een multi-entiteitsegment te bouwen. Dit kan worden gedaan gebruikend of de Segmentatie API of de Bouwer UI van het Segment. Kies voor meer informatie een van de volgende hulplijnen:

* [Een segment maken met de segmentatie-API](./tutorials/create-a-segment.md)
* [Een segment maken met de gebruikersinterface van Segment Builder](./ui/overview.md)

## Segmenten met meerdere entiteiten evalueren en openen

Nadat u een segment hebt gemaakt, kunt u de segmentresultaten evalueren en openen met de segmentatie-API. Het evalueren van een segment met meerdere entiteiten lijkt sterk op het evalueren van een standaardsegment. Dit proces kan alleen worden uitgevoerd met de segmentatie-API. Voor een gedetailleerde gids die toont hoe te om API te gebruiken om segmenten te evalueren en toegang te krijgen tot, gelieve de [evaluerende en tot segmenten](./tutorials/evaluate-a-segment.md) leerprogramma te lezen.
