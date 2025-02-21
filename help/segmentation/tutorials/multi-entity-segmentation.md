---
solution: Experience Platform
title: Overzicht van segmentatie van meerdere entiteiten
description: De segmentatie van meerdere entiteiten is de capaciteit om de gegevens van het Profiel met extra gegevens uit te breiden die op producten, opslag, of andere niet-profielklassen worden gebaseerd. Zodra verbonden, worden de gegevens van extra klassen beschikbaar alsof zij aan het schema van het Profiel inheems waren.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: 630041a7ef82993038ef4510dd08d3bc67bfce41
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Overzicht van segmentatie over meerdere entiteiten

Segmentatie met meerdere entiteiten is een geavanceerde functie die beschikbaar is als onderdeel van Adobe Experience Platform [!DNL Segmentation Service] . Met deze functie kunt u [!DNL Real-Time Customer Profile] -gegevens uitbreiden met aanvullende gegevens van &#39;niet-personen&#39; (ook wel &#39;dimensie-entiteiten&#39; genoemd) die uw organisatie kan definiëren, zoals gegevens die betrekking hebben op producten of winkels. De segmentatie van meerdere entiteiten verstrekt flexibiliteit wanneer het bepalen van segmentdefinities die op gegevens relevant voor uw unieke bedrijfsbehoeften worden gebaseerd en kan zonder het hebben van deskundigheid in het vragen van gegevensbestanden worden uitgevoerd. Met de segmentatie van meerdere entiteiten, kunt u zeer belangrijke gegevens aan uw segmentdefinities toevoegen zonder het moeten dure veranderingen in gegevensstromen aanbrengen of op een achterste-eindgegevenssamenvoeging wachten.

## Aan de slag

De segmentatie van meerdere entiteiten vereist een goed begrip van de verschillende diensten van Adobe Experience Platform die bij segmentatie betrokken zijn. Lees de volgende documentatie voordat u doorgaat met deze handleiding:

* [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform consumentenprofiel in realtime, gebaseerd op geaggregeerde gegevens van meerdere bronnen.
   * [ de gidsen van het Profiel ](../../profile/guardrails.md): Beste praktijken voor het creëren van gegevensmodellen die door [!DNL Profile] worden gesteund.
* [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): hiermee kunt u soorten publiek maken op basis van [!DNL Real-Time Customer Profile] -gegevens.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde raamwerk waarmee Experience Platform gegevens over de ervaring van klanten organiseert.
   * [ Grondbeginselen van schemacompositie ](../../xdm/schema/composition.md#union): Leer beste praktijken voor het samenstellen van schema&#39;s die in Experience Platform moeten worden gebruikt. Om het beste gebruik van Segmentatie te maken, gelieve te verzekeren uw gegevens als profielen en gebeurtenissen volgens de [ beste praktijken voor gegevens modellering ](../../xdm/schema/best-practices.md) worden opgenomen.

## Gebruiksscenario’s

Om de waarde van de segmentatie van meerdere entiteiten te illustreren, overweeg drie standaard marketing gebruiksgevallen die de uitdagingen tonen die in de meeste marketing toepassingen aanwezig zijn:

### Aankoopgegevens online en offline combineren

Een marketeer die een e-mailcampagne bouwt, heeft mogelijk geprobeerd een publiek op te bouwen door recente aankopen in de winkel van klanten binnen de laatste drie maanden te gebruiken. In het ideale geval vereist dit publiek zowel de naam van het item als de naam van de winkel waar de aankoop is gedaan. Eerder, zou de uitdaging de opslag herkenningsteken van de koopgebeurtenis hebben gevangen en het toewijzen aan een individueel klantenprofiel.

### E-mailherbestemming voor het verlaten van het winkelwagentje

Het is ingewikkeld om gebruikers in segmentdefinities voor het verlaten van winkelwagentjes te maken en te kwalificeren. Als u weet welke producten u wilt opnemen in een gepersonaliseerde campagne voor heroriëntering, moet u weten welke producten elk individu heeft opgegeven. Deze gegevens zijn gekoppeld aan commerciële gebeurtenissen die voorheen lastig waren om gegevens te controleren en te extraheren.

## Segmentdefinities met meerdere entiteiten maken

Wanneer u een definitie van een segment met meerdere entiteiten maakt, moet u eerst relaties tussen schema&#39;s definiëren voordat u de gebruikersinterface van de [!DNL Segmentation] API- of segmentbouwer gebruikt om de segmentdefinitie te maken.

### Relaties definiëren

Het bepalen van verhoudingen binnen de structuur van uw schema&#39;s van de Gegevens van de Ervaring (XDM) is een integraal deel van multi-entiteitsegmentverwezenlijking. Voor verhoudingen, moet het gebied in de bestemming als primaire identiteit van dat schema worden gemerkt. Een identiteit kan alleen worden gemarkeerd op tekenreeksen en kan niet worden gemarkeerd op arrays. Bovendien, moeten de verhoudingen niet noodzakelijk één-op-één zijn, aangezien u profielen en ervaringsgebeurtenissen met veelvoudige bestemmingen kunt verbinden.

Het bepalen van verhoudingen kan of gebruikend de Registratie API van het Schema of de Redacteur van het Schema worden gedaan. Voor gedetailleerde stappen die tonen hoe te om een verhouding tussen twee schema&#39;s te bepalen, gelieve te kiezen van de volgende leerprogramma&#39;s:

* [Een relatie tussen twee schema&#39;s definiëren met behulp van de API](../../xdm/tutorials/relationship-api.md)
* [Het bepalen van een verhouding tussen twee schema&#39;s gebruikend de Redacteur UI van het Schema](../../xdm/tutorials/relationship-ui.md)

### Een definitie van een segment met meerdere entiteiten maken

Zodra u de noodzakelijke verhoudingen XDM hebt bepaald, kunt u beginnen om een multi-entiteitsegmentdefinitie te bouwen. Dit kan worden gedaan gebruikend of de Segmentatie API of de Bouwer UI van het Segment. Kies voor meer informatie een van de volgende hulplijnen:

* [Een segmentdefinitie maken met de segmentatie-API](./create-a-segment.md)
* [Een segmentdefinitie maken met de gebruikersinterface van Segment Builder](../ui/overview.md)

## Segmentdefinities met meerdere entiteiten evalueren en openen

Nadat u een segmentdefinitie hebt gemaakt, kunt u de resultaten evalueren en openen met de segmentatie-API. Het evalueren van een definitie van een segment met meerdere entiteiten lijkt sterk op het evalueren van een standaardsegmentdefinitie. Dit proces kan alleen worden uitgevoerd met de segmentatie-API. Voor een gedetailleerde gids die tonen hoe te om API te gebruiken om en segmentdefinities te evalueren toegang te hebben, gelieve [ te lezen evaluerend en tot segmentdefinities ](./evaluate-a-segment.md) leerprogramma toegang te hebben.
