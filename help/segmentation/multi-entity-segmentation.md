---
solution: Experience Platform
title: Overzicht van segmentatie van meerdere entiteiten
description: De segmentatie van meerdere entiteiten is de capaciteit om de gegevens van het Profiel met extra gegevens uit te breiden die op producten, opslag, of andere niet-profielklassen worden gebaseerd. Zodra verbonden, worden de gegevens van extra klassen beschikbaar alsof zij aan het schema van het Profiel inheems waren.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Overzicht van segmentatie over meerdere entiteiten

Segmentatie tussen meerdere entiteiten is een geavanceerde functie die beschikbaar is als onderdeel van Adobe Experience Platform [!DNL Segmentation Service]. Met deze functie kunt u het programma uitbreiden [!DNL Real-Time Customer Profile] gegevens met aanvullende &quot;niet-persoonlijke&quot; gegevens (ook wel &quot;dimensie-entiteiten&quot; genoemd) die uw organisatie kan definiëren, zoals gegevens die betrekking hebben op producten of winkels. De segmentatie van meerdere entiteiten verstrekt flexibiliteit wanneer het bepalen van segmentdefinities die op gegevens relevant voor uw unieke bedrijfsbehoeften worden gebaseerd en kan zonder het hebben van deskundigheid in het vragen van gegevensbestanden worden uitgevoerd. Met de segmentatie van meerdere entiteiten, kunt u zeer belangrijke gegevens aan uw segmentdefinities toevoegen zonder het moeten dure veranderingen in gegevensstromen aanbrengen of op een achterste-eindgegevenssamenvoeging wachten.

## Aan de slag

De segmentatie van meerdere entiteiten vereist een goed begrip van de verschillende diensten van Adobe Experience Platform die bij segmentatie betrokken zijn. Lees de volgende documentatie voordat u doorgaat met deze handleiding:

* [[!DNL Real-Time Customer Profile]](../profile/home.md): Biedt een eenvormig consumentenprofiel in real-time, gebaseerd op geaggregeerde gegevens van meerdere bronnen.
   * [Profielhulplijnen](../profile/guardrails.md): Aanbevolen procedures voor het maken van gegevensmodellen die worden ondersteund door [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Hiermee kunt u een publiek opbouwen op [!DNL Real-Time Customer Profile] gegevens.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../xdm/schema/composition.md#union): Leer de beste werkwijzen voor het samenstellen van schema&#39;s die in Experience Platform moeten worden gebruikt. Als u de segmentatie het beste wilt gebruiken, moet u ervoor zorgen dat uw gegevens als profielen en gebeurtenissen worden opgenomen volgens de [best practices voor gegevensmodellering](../xdm/schema/best-practices.md).

## Gebruiksscenario’s

Om de waarde van de segmentatie van meerdere entiteiten te illustreren, overweeg drie standaard marketing gebruiksgevallen die de uitdagingen tonen die in de meeste marketing toepassingen aanwezig zijn:

### Aankoopgegevens online en offline combineren

Een marketeer die een e-mailcampagne bouwt, heeft mogelijk geprobeerd een publiek op te bouwen door recente aankopen in de winkel van klanten binnen de laatste drie maanden te gebruiken. In het ideale geval vereist dit publiek zowel de naam van het item als de naam van de winkel waar de aankoop is gedaan. Eerder, zou de uitdaging de opslag herkenningsteken van de koopgebeurtenis hebben gevangen en het toewijzen aan een individueel klantenprofiel.

### E-mailherbestemming voor het verlaten van het winkelwagentje

Het is ingewikkeld om gebruikers in segmentdefinities voor het verlaten van winkelwagentjes te maken en te kwalificeren. Als u weet welke producten u wilt opnemen in een gepersonaliseerde campagne voor heroriëntering, moet u weten welke producten elk individu heeft opgegeven. Deze gegevens zijn gekoppeld aan commerciële gebeurtenissen die voorheen lastig waren om gegevens te controleren en te extraheren.

## Segmentdefinities met meerdere entiteiten maken

Het creëren van een multi-entiteitsegmentdefinitie vereist eerst het bepalen van verhoudingen tussen schema&#39;s alvorens te gebruiken [!DNL Segmentation] API of de Bouwer UI van het Segment om de segmentdefinitie te bouwen.

### Relaties definiëren

Het bepalen van verhoudingen binnen de structuur van uw schema&#39;s van de Gegevens van de Ervaring (XDM) is een integraal deel van multi-entiteitsegmentverwezenlijking. Voor verhoudingen, moet het gebied in de bestemming als primaire identiteit van dat schema worden gemerkt. Een identiteit kan alleen worden gemarkeerd op tekenreeksen en kan niet worden gemarkeerd op arrays. Bovendien, moeten de verhoudingen niet noodzakelijk één-op-één zijn, aangezien u profielen en ervaringsgebeurtenissen met veelvoudige bestemmingen kunt verbinden.

Het bepalen van verhoudingen kan of gebruikend de Registratie API van het Schema of de Redacteur van het Schema worden gedaan. Voor gedetailleerde stappen die tonen hoe te om een verhouding tussen twee schema&#39;s te bepalen, gelieve te kiezen van de volgende leerprogramma&#39;s:

* [Een relatie tussen twee schema&#39;s definiëren met behulp van de API](../xdm/tutorials/relationship-api.md)
* [Het bepalen van een verhouding tussen twee schema&#39;s gebruikend de Redacteur UI van het Schema](../xdm/tutorials/relationship-ui.md)

### Een definitie van een segment met meerdere entiteiten maken

Zodra u de noodzakelijke verhoudingen XDM hebt bepaald, kunt u beginnen om een multi-entiteitsegmentdefinitie te bouwen. Dit kan worden gedaan gebruikend of de Segmentatie API of de Bouwer UI van het Segment. Kies voor meer informatie een van de volgende hulplijnen:

* [Een segmentdefinitie maken met de segmentatie-API](./tutorials/create-a-segment.md)
* [Een segmentdefinitie maken met de gebruikersinterface van Segment Builder](./ui/overview.md)

## Segmentdefinities met meerdere entiteiten evalueren en openen

Nadat u een segmentdefinitie hebt gemaakt, kunt u de resultaten evalueren en openen met de segmentatie-API. Het evalueren van een definitie van een segment met meerdere entiteiten lijkt sterk op het evalueren van een standaardsegmentdefinitie. Dit proces kan alleen worden uitgevoerd met de segmentatie-API. Voor een gedetailleerde gids die toont hoe te om API te gebruiken om segmentdefinities te evalueren en te openen, gelieve te lezen [evalueren van en toegang tot segmentdefinities](./tutorials/evaluate-a-segment.md) zelfstudie.
