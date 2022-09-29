---
keywords: Experience Platform;machine het leren model;De Werkruimte van de Wetenschap van Gegevens;In real time het Profiel van de Klant;populaire onderwerpen;machine het leren inzicht
solution: Experience Platform
title: Verrijk het Profiel van de Klant in real time met het Leren van de Machine Inzichten
topic-legacy: tutorial
type: Tutorial
description: Dit document biedt een handleiding voor het verrijken van realtime klantprofiel met kennis van machinaal leren.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 89a9b64f2fb238c08a281f29a035ce0b24b34804
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Verrijken [!DNL Real-time Customer Profile] met kennis van machine leren

Adobe Experience Platform [!DNL Data Science Workspace] biedt de tools en bronnen om modellen voor machinaal leren te maken, te evalueren en te gebruiken om gegevensvoorspellingen en inzichten te genereren. Wanneer inzichten van het leren van machines worden opgenomen in een [!DNL Profile]-enabled dataset, dat de zelfde gegevens ook worden opgenomen zoals [!DNL Profile] records die vervolgens kunnen worden gesegmenteerd [!DNL Adobe Experience Platform Segmentation Service].

Dit document bevat koppelingen naar zelfstudies waarmee u documenten kunt verrijken [!DNL Real-time Customer Profile] met uw computerleerinzichten.

## Aan de slag

Voor het voltooien van de onderstaande lesbestanden hebt u een goed inzicht in het gebruik van [!DNL Profile] gegevens en segmenten maken. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een volledige, verenigde vertegenwoordiging van elke individuele klant die op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Identity Service]](../../identity-service/home.md): Inschakelen [!DNL Real-time Customer Profile] door identiteiten te overbruggen van verschillende gegevensbronnen die in Platform worden opgenomen.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.

Naast de bovengenoemde documenten, wordt het ten zeerste geadviseerd dat u ook de volgende gidsen op schema&#39;s en de Redacteur van het Schema bekijkt:

- [Basisbeginselen van de schemacompositie](../../xdm/schema/composition.md): Beschrijft schema&#39;s XDM, bouwstenen, principes, en beste praktijken voor het samenstellen van schema&#39;s die binnen moeten worden gebruikt [!DNL Experience Platform].
- [Zelfstudie Schema Editor](../../xdm/tutorials/create-schema-ui.md): Verstrekt gedetailleerde instructies voor het creëren van schema&#39;s gebruikend de Redacteur van het Schema binnen [!DNL Experience Platform].

## Een uitvoerschema en gegevensset maken en configureren {#create-an-output-schema-and-dataset}

De eerste stap naar verrijking [!DNL Real-time Customer Profile] met scorende inzichten is weten welk object in de praktijk (zoals een persoon) uw gegevens definiëren. Dankzij een goed begrip van uw gegevens kunt u een structuur beschrijven en ontwerpen om betekenis toe te voegen, vergelijkbaar met het ontwerpen van een relationele database.

Het samenstellen van een schema begint door een klasse toe te wijzen. De klassen bepalen de gedragsaspecten van de gegevens het schema (verslag of tijdreeks) zal bevatten. Volg de stappen in de zelfstudie om uw eigen schema&#39;s te maken op [een schema maken met de Schema-editor](../../xdm/tutorials/create-schema-ui.md). Merk op alvorens u een dataset voor kunt toelaten [!DNL Profile], moet u het schema van de dataset vormen om een primair identiteitsgebied te hebben en dan het schema voor toe te laten [!DNL Profile]. Wanneer gegevens in een [!DNL Profile]-enabled dataset, dat de zelfde gegevens ook worden opgenomen zoals [!DNL Profile] records.

Als u liever een schema samenstelt met de opdracht [!DNL Schema Registry] API in plaats daarvan, begin door te lezen [[!DNL Schema Registry] ontwikkelaarsgids](../../xdm/api/getting-started.md) voordat u de zelfstudie hebt ingeschakeld [een schema maken met de API](../../xdm/tutorials/create-schema-api.md).

Zodra uw schema en dataset worden voorbereid, kunt u het schrapen gegevens aan de dataset produceren en opnemen door het schrapen looppas uit te voeren gebruikend een aangewezen model.

## Segmenten maken met de opdracht [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Nadat u uw het scoren gegevensinzichten aan uw hebt geproduceerd en gegeten [!DNL Profile]- toegelaten dataset, kunt u dynamische segmenten tot stand brengen gebruikend [!DNL Segment Builder].

De [!DNL Segment Builder] biedt een rijke werkruimte waarmee u kunt werken met [!DNL Profile] gegevenselementen. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van regels, zoals tegels voor slepen en neerzetten die worden gebruikt om gegevenseigenschappen te vertegenwoordigen. Volg de [[!DNL Segment Builder] gebruikershandleiding](../../segmentation/ui/segment-builder.md) voor meer informatie over:

- Segmentdefinities maken met een combinatie van kenmerken, gebeurtenissen en bestaand publiek als bouwstenen.
- Het gebruiken van het canvas en de containers van de regelbouwer om de orde te controleren waarin de segmentregels worden uitgevoerd.
- Het bekijken van ramingen van uw prospectief publiek, toestaand u om uw segmentdefinities zonodig aan te passen.
- Het toelaten van alle segmentdefinities voor geplande segmentatie.
- Opgegeven segmentdefinities voor streaming segmentatie inschakelen.

## Volgende stappen {#next-steps}

Meer informatie over segmenten en de [!DNL Segment Builder], lees de [Overzicht van segmentatieservice](../../segmentation/home.md).

Meer informatie over [!DNL Real-time Customer Profile], lees de [Overzicht van het realtime klantprofiel](../../profile/home.md)
