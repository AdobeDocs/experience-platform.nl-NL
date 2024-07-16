---
solution: Experience Platform
title: De Gids van de Beperkingen UI van de Tijd van de Vervorming van de Refactoring
description: De Bouwer van het segment verstrekt een rijke werkruimte die u toestaat om met de gegevenselementen van het Profiel in wisselwerking te staan. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van regels, zoals tegels voor slepen en neerzetten die worden gebruikt om gegevenseigenschappen te vertegenwoordigen.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 665bbd1904e857336a4fb677230389d7977f6b60
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Tijd beperkte reactoring {#refactorization}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_constraints"
>title="Tijd beperkte reactoring"
>abstract="De regel-niveau en groep-vlakke tijdbeperkingen zijn verwijderd om tijdbeperkingsgebruik te verduidelijken. Schrijf de restrictie opnieuw als een beperking op canvasniveau of op kaartniveau."

De release van januari 2024 voor Adobe Experience Platform heeft wijzigingen aangebracht in Adobe Experience Platform Segmentation Service die nieuwe beperkingen toevoegen aan waar tijdbeperkingen kunnen worden gedefinieerd. Deze wijzigingen zijn van invloed op pas gemaakte of bewerkte segmenten die zijn gemaakt met de gebruikersinterface van Segment Builder. Deze gids verklaart hoe te om deze veranderingen te verlichten.

Vóór de versie van Januari 2024, verwijzen alle regel-niveau, groep-niveau, en canvas-vlakke tijdbeperkingen overtollig naar zelfde timestamp. Om tijdbeperkingsgebruik te verduidelijken, zijn regel-niveau en groep-vlakke tijdbeperkingen verwijderd. Om deze verandering aan te passen, moeten alle tijdbeperkingen **** als **canvas-niveau** of **kaart-niveau** tijdbeperkingen worden herschreven.

Eerder kon aan een afzonderlijke gebeurtenis meerdere regels voor tijdbeperking zijn gekoppeld. Met deze recente update, zal het proberen om een tijdbeperking aan een regel toe te voegen nu in een **fout** resulteren.

![ de regel-vlakke tijdbeperking wordt benadrukt. De fout die vervolgens optreedt, wordt ook gemarkeerd. ](../images/ui/segment-refactoring/rule-time-constraint.png)

Tijdbeperkingen kunnen nu alleen op canvasniveau of op kaartniveau worden toegepast.

Wanneer u een tijdbeperking op canvasniveau toepast, kunt u nog steeds alle beschikbare tijdbeperkingen selecteren.

>[!NOTE]
>
>Als er slechts één **kaart op het canvas is, is het toepassen van de tijdbeperking op de kaart** gelijkwaardig **aan het toepassen van de tijdbeperking op canvas-niveau.**
>
>Als er **veelvoudige** kaarten op het canvas zijn, zal het toepassen van de tijdbeperking op canvas-niveau die tijdbeperking op **alle** kaarten op het canvas toepassen.

![ de canvas-vlakke tijdbeperking wordt benadrukt.](../images/ui/segment-refactoring/canvas-time-constraint.png)

Als u een tijdbeperking op kaartniveau wilt toepassen, selecteert u de specifieke kaart waarop u de tijdbeperking wilt toepassen. De container **[!UICONTROL Event Rules]** wordt weergegeven. U kunt nu de tijdbeperking selecteren die u op de kaart wilt toepassen.

![ de kaart-vlakke tijdbeperking wordt benadrukt.](../images/ui/segment-refactoring/card-time-constraint.png)
