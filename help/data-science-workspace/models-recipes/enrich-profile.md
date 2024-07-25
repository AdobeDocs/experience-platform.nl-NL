---
keywords: Experience Platform;machine het leren model;De Wetenschap van gegevens Workspace;Real-time het Profiel van de Klant;populaire onderwerpen;machine het leren inzicht
solution: Experience Platform
title: Verrijk het Profiel van de Klant in real time met het Leren van de Machine Inzichten
type: Tutorial
description: Dit document biedt een handleiding voor het verrijken van Real-Time Customer Profile met inzichten in computerleren.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: afa27069c7490848398c92973dd77810564b5993
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Verrijken [!DNL Real-Time Customer Profile] met leergegevens over computers

Adobe Experience Platform [!DNL Data Science Workspace] biedt de gereedschappen en bronnen om modellen voor machinaal leren te maken, te evalueren en te gebruiken om gegevensvoorspellingen en inzichten te genereren. Wanneer inzichten van het machinaal leren in een [!DNL Profile]-Toegelaten dataset worden opgenomen, worden die zelfde gegevens ook opgenomen zoals [!DNL Profile] verslagen die dan kunnen worden gesegmenteerd gebruikend [!DNL Adobe Experience Platform Segmentation Service].

Het segmenteringsproces hangt van de evaluatiemethode voor het publiek af. Als een publiek als **het stromen** wordt gevormd, zal het alle nieuwe updates verwerken die door het model in het profiel in real time worden geschreven. Nochtans, als een publiek voor **partij** evaluatie wordt gevormd, zullen de nieuwe waarden in de volgende partij worden geëvalueerd.

Dit document bevat koppelingen naar zelfstudies waarmee u [!DNL Real-Time Customer Profile] kunt verrijken met de leermogelijkheden van uw computer.

## Aan de slag

Als u de onderstaande lesbestanden wilt voltooien, hebt u een goed begrip nodig van het invoeren van [!DNL Profile] -gegevens en het maken van soorten publiek. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een volledige, uniforme representatie van elke individuele klant op basis van geaggregeerde gegevens van meerdere bronnen.
- [[!DNL Identity Service]](../../identity-service/home.md): schakelt [!DNL Real-Time Customer Profile] in door identiteiten te overbruggen van verschillende gegevensbronnen die in Platform worden opgenomen.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee Platform gegevens voor klantervaring organiseert.

Naast de bovengenoemde documenten, wordt het ten zeerste geadviseerd dat u ook de volgende gidsen op schema&#39;s en de Redacteur van het Schema bekijkt:

- [ Grondbeginselen van schemacompositie ](../../xdm/schema/composition.md): Beschrijft schema&#39;s XDM, bouwstenen, principes, en beste praktijken voor het samenstellen van schema&#39;s die in [!DNL Experience Platform] moeten worden gebruikt.
- [ het leerprogramma van de Redacteur van het Schema ](../../xdm/tutorials/create-schema-ui.md): Verstrekt gedetailleerde instructies voor het creëren van schema&#39;s gebruikend de Redacteur van het Schema binnen [!DNL Experience Platform].

## Een uitvoerschema en een gegevensset maken en configureren {#create-an-output-schema-and-dataset}

De eerste stap in de richting van verrijking van [!DNL Real-Time Customer Profile] met het schalen van inzichten is het weten van welk echt object (zoals een persoon) uw gegevens definiëren. Dankzij een goed begrip van uw gegevens kunt u een structuur beschrijven en ontwerpen om betekenis toe te voegen, vergelijkbaar met het ontwerpen van een relationele database.

Het samenstellen van een schema begint door een klasse toe te wijzen. De klassen bepalen de gedragsaspecten van de gegevens het schema (verslag of tijdreeks) zal bevatten. Begin makend uw eigen schema&#39;s, volg de stappen in het leerprogramma op [ creërend een schema gebruikend de Redacteur van het Schema ](../../xdm/tutorials/create-schema-ui.md). Merk op dat alvorens u een dataset voor [!DNL Profile] kunt toelaten, u het schema van de dataset moet vormen om een primair identiteitsgebied te hebben en dan het schema voor [!DNL Profile] toe te laten. Wanneer gegevens in een [!DNL Profile] -gegevensset worden opgenomen, worden dezelfde gegevens ook opgenomen als [!DNL Profile] -records.

Als u verkiest om een schema samen te stellen gebruikend [!DNL Schema Registry] API in plaats daarvan, begin door de [[!DNL Schema Registry]  ontwikkelaarsgids ](../../xdm/api/getting-started.md) te lezen alvorens de leerprogramma te proberen op [ creërend een schema gebruikend API ](../../xdm/tutorials/create-schema-api.md).

Zodra uw schema en dataset worden voorbereid, kunt u het schrapen gegevens aan de dataset produceren en opnemen door het schrapen looppas uit te voeren gebruikend een aangewezen model.

## Soorten publiek maken met de [!DNL Segment Builder] {#create-audiences-using-the-segment-builder}

Nadat u de inzichten van uw scoringsgegevens naar uw [!DNL Profile] -gegevensset hebt gegenereerd en ingepakt, kunt u een dynamisch publiek maken met de [!DNL Segment Builder] -gegevensset.

[!DNL Segment Builder] biedt een rijke werkruimte waarmee u kunt werken met [!DNL Profile] -gegevenselementen. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van regels, zoals tegels voor slepen en neerzetten die worden gebruikt om gegevenseigenschappen te vertegenwoordigen. Volg de [[!DNL Segment Builder]  gebruikersgids ](../../segmentation/ui/segment-builder.md) om over te leren:

- Segmentdefinities maken met een combinatie van kenmerken, gebeurtenissen en bestaand publiek als bouwstenen.
- Het gebruiken van het canvas en de containers van de regelbouwer om de orde te controleren waarin de publieksregels worden uitgevoerd.
- Het bekijken van ramingen van uw prospectief publiek, toestaand u om uw segmentdefinities zonodig aan te passen.
- Het toelaten van alle segmentdefinities voor geplande segmentatie.
- Opgegeven segmentdefinities voor streaming segmentatie inschakelen.

## Volgende stappen {#next-steps}

Meer over publiek en [!DNL Segment Builder] leren, lees het [ overzicht van de Dienst van de Segmentatie ](../../segmentation/home.md).

Om meer over [!DNL Real-Time Customer Profile] te leren, lees het [ Real-Time overzicht van het Profiel van de Klant ](../../profile/home.md)
