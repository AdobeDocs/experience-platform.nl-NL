---
solution: Experience Platform
title: Overzicht van industriemodellen
topic: overzicht
description: Leer over de gestandaardiseerde gegevensmodellen voor diverse de industrietakken die kunnen worden geconstrueerd gebruikend de componenten van het Model van de Gegevens van de Ervaring (XDM).
translation-type: tm+mt
source-git-commit: 9862cbcb8d8c74c96dd6bf44c5fa416f4f42fe64
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# Overzicht bedrijfsgegevensmodellen

Het Model van Gegevens van de ervaring (XDM) staat u toe om hoogst klantgerichte schema&#39;s tot stand te brengen om zeer belangrijke gegevens van de klantenervaring met betrekking tot uw zaken te vangen. Adobe Experience Platform biedt een veelzijdige suite standaard XDM-componenten, die concepten vastleggen die in verschillende bedrijfstakken algemeen worden gebruikt, om het modelleren van uw gegevens te helpen stroomlijnen en aan XDM te laten voldoen.

>[!NOTE]
>
>De nieuwe standaardXDM componenten worden onophoudelijk vrijgegeven aan best aangepaste consumentenbehoeften. Voor een lijst van de meest bijgewerkte componenten, kunt u [bestaande middelen in UI](../../ui/explore.md) onderzoeken of naar [officiële XDM bewaarplaats](https://github.com/adobe/xdm/tree/master/components) op GitHub verwijzen.

Afhankelijk van de industrie die uw zaken onder werkt, zullen sommige componenten XDM relevanter voor uw behoeften dan anderen zijn. Bovendien zullen de relaties die u tussen uw XDM-schema&#39;s tot stand brengt, afhankelijk van uw industrie variëren.

Om u te helpen uw gegevensmodelleringsstrategie begeleiden die op uw bepaalde industrie wordt gebaseerd, verstrekt deze gids een verwijzing van de diagrammen van de entiteitverhouding (ERDs) voor verscheidene gesteunde industrie verticals.

## Vereisten

Om ERDs te lezen die in deze gids van verwijzingen wordt voorzien, moet u een werkend inzicht in hebben hoe de componenten XDM aan vormschema&#39;s en hoe XDM- schema&#39;s in Experience Platform als geheel in wisselwerking staan. Lees de volgende overzichtsdocumentatie voordat u verdergaat:

* [XDM-systeemoverzicht](../../home.md): Leer hoe XDM in het ecosysteem van het Platform werkt.
* [Basisbeginselen van de schemacompositie](../../schema/composition.md): Leer hoe de componenten XDM (zoals mixins, klassen, en gegevenstypes) tot de structuur van een schema, evenals de rol van identiteitsgebieden bijdragen.

Het wordt ook geadviseerd dat u [gegevens het modelleren beste praktijken gids](../../schema/best-practices.md) voor algemene richtlijnen over hoe te om uw gegevens aan XDM in kaart te brengen controleert.

## Bedrijfs gegevensmodel ERDs {#erds}

De verticale industriemodellen die hieronder door de ERD&#39;s worden vertegenwoordigd, worden opzettelijk op een gedenormaliseerde manier gecreëerd en met inachtneming van de wijze waarop gegevens in Platform worden opgeslagen.

Voor een bepaalde ERD is elke entiteit die wordt weergegeven in gebaseerd op een onderliggende XDM-klasse. Voor een bepaalde entiteit vertegenwoordigt elke rij die in **bold** wordt gemarkeerd, een combinatie of een gegevenstype, met de relevante velden die hieronder in onbolle tekst worden weergegeven. De belangrijkste velden voor een bepaalde entiteit worden rood gemarkeerd.

>[!NOTE]
>
>Sommige entiteiten kunnen het veld &quot;_ID&quot; bevatten. Dit vertegenwoordigt unieke herkenningsteken (`_id`) dat Platform automatisch aan gebeurtenis of profielentiteiten toewijst wanneer zij worden opgenomen. U kunt er echter desgewenst voor kiezen om uw eigen unieke id-waarden voor dit veld te gebruiken.

Alle eigenschappen die zouden kunnen worden gebruikt om individuele klanten te identificeren zijn duidelijk als &quot;identiteit&quot;, met één van deze eigenschappen duidelijk als &quot;primaire identiteit&quot;.

Entiteitsrelaties zijn gemarkeerd als niet-afhankelijk, omdat op cookies gebaseerde gebeurtenissen vaak niet kunnen bepalen wie de transactie heeft uitgevoerd.

ERD&#39;s zijn beschikbaar voor de volgende verticale handelslijnen:

* [[!UICONTROL Retail]](./retail.md)
* [[!UICONTROL Financial services]](./financial.md)
* [[!UICONTROL Travel and hospitality]](./travel-hospitality.md)

## Volgende stappen

In dit document werd een overzicht gegeven van de ERD&#39;s van het bedrijfsgegevensmodel en de interpretatie ervan. Als u een ERD wilt weergeven, selecteert u een ERD in de bovenstaande lijst.