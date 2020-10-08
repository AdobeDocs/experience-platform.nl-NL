---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment builder;Segment builder
solution: Experience Platform
title: De de veranderingengids van de Bouwer van het Segmentatiesegment van de Dienst
topic: ui guide
description: 'De Bouwer van het segment verstrekt een rijke werkruimte die u toestaat om met de gegevenselementen van het Profiel in wisselwerking te staan. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van regels, zoals tegels voor slepen en neerzetten die worden gebruikt om gegevenseigenschappen te vertegenwoordigen. '
translation-type: tm+mt
source-git-commit: beacce03136e1620ff57fb549f335d2199bb6001
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# Tijd beperkte reactoring

De release van oktober 2020 voor Adobe Experience Platform heeft prestatiewijzigingen geïntroduceerd in Adobe Experience Platform Segmentation Service die nieuwe beperkingen toevoegt aan het gebruik van de OR en AND logische operatoren. Deze wijzigingen zijn van invloed op pas gemaakte of bewerkte segmenten die zijn gemaakt met de gebruikersinterface van Segment Builder. Deze gids verklaart hoe te om deze veranderingen te verlichten.

Vóór de versie van Oktober 2020, verwijzen alle regel-niveau, groep-niveau, en gebeurtenis-vlakke tijdbeperkingen overtollig naar zelfde timestamp. Om tijdbeperkingsgebruik te verduidelijken, zijn regel-niveau en groep-vlakke tijdbeperkingen verwijderd. Om deze verandering aan te passen, moeten alle tijdbeperkingen als gebeurtenis-vlakke tijdbeperkingen worden herschreven.

Eerder kon aan een afzonderlijke gebeurtenis meerdere regels voor tijdbeperking zijn gekoppeld.

![](../images/ui/segment-refactoring/former-time-constraint.png)

Zoals u kunt zien, heeft dit segment twee beperkingen op regel-niveau: Een voor &quot;[!UICONTROL Vandaag]&quot; en een voor &quot;[!UICONTROL Gisteren]&quot;.

Het vorige segment is gelijkwaardig aan het volgende segment — beide gebeurtenis-vlakke tijdbeperkingen zijn verbonden gebruikend een exploitant AND. De eerste tijdbeperking op gebeurtenisniveau verwijst naar een klikgebeurtenis waarvan de naam gelijk is aan &quot;Training&quot; en die vandaag plaatsvindt, terwijl de tweede tijdbeperking op gebeurtenisniveau verwijst naar een klikgebeurtenis waarvan de naam gelijk is aan &quot;Huisdieren&quot; en die gisteren heeft plaatsgevonden.

![](../images/ui/segment-refactoring/time-constraint-1.png) ![](../images/ui/segment-refactoring/time-constraint-2.png)

Dit refactoring van tijdbeperkingen beïnvloedt ook tijdbeperkingen die gebruikend een exploitant OF worden verbonden.