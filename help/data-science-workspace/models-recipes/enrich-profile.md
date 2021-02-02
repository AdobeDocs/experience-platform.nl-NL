---
keywords: Experience Platform;machine het leren model;De Werkruimte van de Wetenschap van Gegevens;In real time het Profiel van de Klant;populaire onderwerpen;machine het leren inzicht
solution: Experience Platform
title: Klantprofiel in realtime verrijken met kennis van machinaal leren
topic: tutorial
type: Tutorial
description: Dit document biedt een handleiding voor het verrijken van realtime klantprofiel met door de computer geleerd inzichten.
translation-type: tm+mt
source-git-commit: 62e6bb7e72637b06808ff87dc21f40af2c4e2d45
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# Verrijk [!DNL Real-time Customer Profile] met kennis van machine-leren

Adobe Experience Platform [!DNL Data Science Workspace] biedt de gereedschappen en bronnen voor het maken, evalueren en gebruiken van modellen voor het leren van machines om gegevensvoorspellingen en inzichten te genereren. Wanneer machinaal-leert inzichten in een [!DNL Profile]-Toegelaten dataset worden opgenomen, worden die zelfde gegevens ook opgenomen zoals [!DNL Profile] verslagen die dan kunnen worden gesegmenteerd gebruikend [!DNL Adobe Experience Platform Segmentation Service]. Aangezien profiel en tijdreeksgegevens worden opgenomen, beslist het Profiel van de Klant in real time automatisch om die gegevens van segmenten door een aan de gang zijnde proces te omvatten of uit te sluiten die het stromen segmentatie wordt genoemd, alvorens het met bestaande gegevens samen te voegen en de verenigingsmening bij te werken. Dientengevolge, kunt u onmiddellijk berekeningen uitvoeren en besluiten nemen om verbeterde, geïndividualiseerde ervaringen aan klanten te leveren aangezien zij met uw merk in wisselwerking staan.

Dit document bevat koppelingen naar zelfstudies waarmee u [!DNL Real-time Customer Profile] kunt verrijken met uw door de computer geleerd inzichten.

## Aan de slag

Voor het voltooien van de onderstaande lesbestanden hebt u een goed inzicht nodig in het opnemen van [!DNL Profile]-gegevens en het maken van segmenten. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een volledige, verenigde vertegenwoordiging van elke individuele klant die op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Identity Service]](../../identity-service/home.md): Hiermee wordt  [!DNL Real-time Customer Profile] door het overbruggen van identiteiten mogelijk van verschillende gegevensbronnen die in Platform worden opgenomen.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.

Naast de bovengenoemde documenten, wordt het ten zeerste geadviseerd dat u ook de volgende gidsen op schema&#39;s en de Redacteur van het Schema bekijkt:

- [Basisbeginselen van de schemacompositie](../../xdm/schema/composition.md): Beschrijft schema&#39;s XDM, bouwstenen, principes, en beste praktijken voor het samenstellen van schema&#39;s die binnen moeten worden gebruikt  [!DNL Experience Platform].
- [Zelfstudie](../../xdm/tutorials/create-schema-ui.md) Schema-editor: Verstrekt gedetailleerde instructies voor het creëren van schema&#39;s gebruikend de Redacteur van het Schema binnen  [!DNL Experience Platform].

## Een uitvoerschema en gegevensset maken en configureren {#create-an-output-schema-and-dataset}

De eerste stap in het verrijken van [!DNL Real-time Customer Profile] met het scoren van inzichten is het weten van welk echt voorwerp (zoals een persoon) uw gegevens bepaalt. Dankzij een goed begrip van uw gegevens kunt u een structuur beschrijven en ontwerpen om betekenis toe te voegen, vergelijkbaar met het ontwerpen van een relationele database.

Het samenstellen van een schema begint door een klasse toe te wijzen. De klassen bepalen de gedragsaspecten van de gegevens het schema (verslag of tijdreeks) zal bevatten. Om uw eigen schema&#39;s te beginnen maken, volg de stappen in het leerprogramma op [creërend een schema gebruikend de Redacteur van het Schema](../../xdm/tutorials/create-schema-ui.md). Merk op dat alvorens u een dataset voor [!DNL Profile] kunt toelaten, u het schema van de dataset moet vormen om een primair identiteitsgebied te hebben en dan het schema voor [!DNL Profile] toe te laten. Wanneer gegevens in een [!DNL Profile]-Toegelaten dataset worden opgenomen, worden die zelfde gegevens ook opgenomen zoals [!DNL Profile] verslagen.

Als u verkiest om een schema samen te stellen gebruikend [!DNL Schema Registry] API in plaats daarvan, begin door [[!DNL Schema Registry] ontwikkelaarsgids](../../xdm/api/getting-started.md) te lezen alvorens de leerprogramma [het creëren van een schema te proberen gebruikend API](../../xdm/tutorials/create-schema-api.md).

Zodra uw schema en dataset worden voorbereid, kunt u het schrapen gegevens aan de dataset produceren en opnemen door het schrapen looppas uit te voeren gebruikend een aangewezen model.

## Segmenten maken met de [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Nadat u uw het scoren gegevensinzichten aan uw [!DNL Profile]-Toegelaten dataset hebt geproduceerd en opgenomen, kunt u dynamische segmenten tot stand brengen gebruikend [!DNL Segment Builder].

[!DNL Segment Builder] verstrekt een rijke werkruimte die u toestaat om met [!DNL Profile] gegevenselementen in wisselwerking te staan. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van regels, zoals tegels voor slepen en neerzetten die worden gebruikt om gegevenseigenschappen te vertegenwoordigen. Volg de [[!DNL Segment Builder] gebruikershandleiding](../../segmentation/ui/segment-builder.md) om informatie te leren over:

- Segmentdefinities maken met een combinatie van kenmerken, gebeurtenissen en bestaand publiek als bouwstenen.
- Het gebruiken van het canvas en de containers van de regelbouwer om de orde te controleren waarin de segmentregels worden uitgevoerd.
- Het bekijken van ramingen van uw prospectief publiek, toestaand u om uw segmentdefinities zonodig aan te passen.
- Het toelaten van alle segmentdefinities voor geplande segmentatie.
- Opgegeven segmentdefinities voor streaming segmentatie inschakelen.

## Volgende stappen {#next-steps}

Lees voor meer informatie over segmenten en de [!DNL Segment Builder] het [Overzicht van de segmentatieservice](../../segmentation/home.md).

Lees voor meer informatie over [!DNL Real-time Customer Profile] het [Real-time overzicht van het Klantprofiel](../../profile/home.md)