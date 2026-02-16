---
title: Overzicht uitvoeren en gebruiken
description: Inspecteer, los problemen op, en optimaliseer uw implementaties van Adobe Experience Platform met de Looppas en werkende hulpmiddelen. Verbeter zicht in geplande partijactiviteiten, identificeer configuratiekwesties, en verbeter systeembetrouwbaarheid.
hide: true
hidefromtoc: true
source-git-commit: 3696ebffc4bd1e588a04e5789ff0c7971e636b56
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---


# Overzicht uitvoeren en gebruiken

>[!AVAILABILITY]
>
>Functies voor uitvoeren en werken zijn momenteel in beperkte mate beschikbaar.

Wanneer de partijbanen ontbreken of onvolledige gegevens leveren, moet u snel begrijpen wat de kwestie veroorzaakte. De worteloorzaak zou de kwesties van de gegevensbeschikbaarheid, onjuiste timing, configuratieproblemen, of beperkingen van de systeemcapaciteit kunnen zijn. Zonder duidelijke zichtbaarheid kunt u uren doorbrengen met het onderzoeken van meerdere systemen voordat u het antwoord vindt.

Met [!UICONTROL Run and Operate] -gereedschappen kunt u:

* **inspecteer uw gegevensverrichtingen**: Krijg een volledige mening van de status van de baanuitvoering en gezondheid over al uw werkschema&#39;s.
* **lost sneller problemen op**: Toegang tot gedetailleerde kenmerkende informatie en uitvoeringsgeschiedenis om worteloorzaken snel te identificeren en uw gemiddelde tijd aan resolutie te verminderen.
* **Prevent kwesties proactively**: Analyseer baanpatronen, ontdek configuratieproblemen alvorens zij mislukkingen veroorzaken, en optimaliseer uw gegevensverrichtingen.

## Doelpubliek {#target-audiences}

[!UICONTROL Run and Operate] -gereedschappen zijn ontworpen voor verschillende soorten publiek in uw organisatie:

* **de teams van Gegevens en van IT**: De beheerders van het systeem en gegevensingenieurs die betrouwbare gegevenspijpleidingen handhaven en technische kwesties problemen oplossen.
* **de verrichtingen van de Marketing**: De technologen van de marketing die gegevenslevering aan marketing platforms inspecteren en activeringskwesties oplossen.
* **Implementers**: Praktijken die uitvoeringsefficiency, betrouwbaarheid bevestigen, en technische kwesties problemen oplossen.

## Vereisten {#prerequisites}

Om tot Looppas toegang te hebben en hulpmiddelen in werking te stellen, hebt u **[!UICONTROL View Job Schedules]** en **[!UICONTROL View Profile Management]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig.
De pagina [!UICONTROL Job Schedules] biedt een overzicht van al uw geplande batchverwerkingstaken.
Neem contact op met de systeembeheerder om ervoor te zorgen dat u over de juiste machtigingen beschikt.

## Aan de slag {#getting-started}

U kunt als volgt de gereedschappen Uitvoeren en Bewerken openen via de gebruikersinterface van Experience Platform:

1. Meld u aan bij uw Experience Platform-account en selecteer **[!UICONTROL Run and Operate]** in de linkernavigatie.
2. Selecteer het hulpmiddel dat uw inspectie of het oplossen van problemenbehoeften aanpast.

   >[!NOTE]
   >
   >Momenteel, is het enige beschikbare vermogen [ Programma&#39;s van de Baan ](job-schedules.md).

![ Experience Platform UI die de Looppas toont en linkernav in werking stelt.](assets/overview/run-and-operate.png)

## Beschikbare gereedschappen {#available-tools}

Met de volgende gereedschappen kunt u uw gegevensbewerkingen controleren en optimaliseren.

### Taakschema&#39;s {#job-schedules}

>[!IMPORTANT]
>
>[!UICONTROL Job schedules] is momenteel alleen beschikbaar voor de volgende Real-Time CDP-taken:
>
> * Batchgegevens
> * Inname van batchprofiel
> * Batchsegmentatie
> * Batchdoelactivering.

Met [ Programma&#39;s van de Baan ](job-schedules.md), kunt u alle geplande partijverrichtingen over uw organisatie, per zandbak, met inbegrip van de opname van het gegevenspeer, profielopname, segmentatie, en bestemmingsactivering inspecteren. De status van de baanuitvoering van de mening, prestatiesmetriek, en uitvoeringsgeschiedenis om patronen te identificeren en configuratiekwesties te diagnostiseren die betrouwbaarheid beïnvloeden.

![ UI die van Experience Platform het scherm van de Planningen van de Baan toont.](assets/overview/job-schedules-interface.png)

De dienstprogramma&#39;s verstrekken drie niveaus van onderzoek:

* **[inspecteer baanprogramma&#39;s](job-schedules.md)**: Bekijk alle datasets en hun geplande banen in een chronologie om patronen te identificeren en conflicten over uw volledige pijpleiding te plannen.
* **[identificeer anti-patronen](job-schedules-anti-patterns.md)**: Leer om gemeenschappelijke configuratiekwesties zoals planningsoverlapping, dichte partij het stapelen, en bovenmatige partij te steunen en op te lossen die prestaties beïnvloeden.
* **[de baandetails van de Mening](job-schedules-details.md)**: Boor neer in specifieke datasets en individuele baanlooppas om mislukkingen te onderzoeken, timing te controleren, en verwerkte verslagen te verifiëren.

U kunt ook de afhankelijkheden tussen gegevensverwerkingsfasen begrijpen, zodat u verzekerd bent van een betrouwbare gegevensstroom in uw Experience Platform-workflows.

## Volgende stappen {#next-steps}

Nu u het doel en de mogelijkheden van [!UICONTROL Run and Operate] -gereedschappen begrijpt, verkent u de volgende bronnen om uw kennis te verdiepen:

* Leer over [ partij ingestie ](../ingestion/batch-ingestion/overview.md) om te begrijpen hoe het gegeven in Experience Platform wordt opgenomen
* Leer hoe te om [ baanprogramma&#39;s ](job-schedules.md) voor uw partijopname en activeringen te inspecteren
* Begrijp hoe te [ geplande activeringen ](../destinations/ui/activate-batch-profile-destinations.md) voor partijbestemmingen vormen
* Onderzoek [ dataflow controle ](../dataflows/ui/monitor-destinations.md) voor bestemmingen

