---
title: Overzicht gegevensstromen
description: Leer hoe gegevensstromen u helpen uw cliënt-kant integratie van Experience Platform SDK met de producten van Adobe en derdebestemmingen verbinden.
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---

# Overzicht gegevensstromen

Een gegevensstroom vertegenwoordigt de server-zijconfiguratie voor het Web van Adobe Experience Platform en Mobiele SDKs. Terwijl de opdracht [`configure`](/help/collection/js/commands/configure/overview.md) in de SDK de client-side instellingen (zoals de `edgeDomain` ) verwerkt, beheren gegevensstreams alle andere configuraties.

Wanneer u een aanvraag naar de Edge Network verzendt, verwijst `datastreamId` naar de gegevensstroom waarnaar de gegevens worden verzonden. Zo kunt u de serverconfiguratie bijwerken zonder de code van uw website te wijzigen.

U kunt gegevensstromen tot stand brengen en beheren door **[!UICONTROL Datastreams]** in de linkernavigatie binnen de UI van Adobe Experience Platform of UI van de Inzameling van Gegevens te selecteren.

![ Het lusje van gegevensstromen in UI ](assets/overview/datastreams-tab.png)

Voor meer informatie over hoe te om een gegevensstroom in UI te vormen, zie de [ configuratiegids ](./configure.md).

## Vertrouwelijke gegevens in gegevensstromen verwerken {#sensitive}

>[!IMPORTANT]
>
>De inhoud van dit document is geen juridisch advies en is niet bedoeld ter vervanging van juridisch advies. Raadpleeg de juridische afdeling van uw bedrijf voor advies over de verwerking van gevoelige gegevens.

Het beleid en de regelgevende vereisten van het bedrijfsgegevensbeheer verhogen beperkingen op hoe de gevoelige klantengegevens kunnen worden verzameld, worden verwerkt, en worden gebruikt. Dit omvat het verzamelen, verwerken en gebruiken van beschermde gezondheidsgegevens (PHI), die onderworpen zijn aan regelingen zoals de Health Insurance Portability and Accountability Act (HIPAA).

De stromen van gegevensstromen verstrekken drie methodes om u bij de veilige behandeling van uw gevoelige gegevens te helpen:

* [Verbeterde codering](#encryption)
* [Datagovernance](#governance)
* [Controlelogboeken](#audit-logs)

### Verbeterde codering {#encryption}

Alle gegevens in doorgang door Edge Network wordt geleid over veilige, gecodeerde verbindingen gebruikend [ HTTPS TLS 1.2 ](https://datatracker.ietf.org/doc/html/rfc5246). Als de gegevensstroom gegevens naar Experience Platform brengt, worden de gegevens vervolgens in rust gecodeerd in het Experience Platform data Lake. Zie het document over [ gegevensencryptie in Experience Platform ](../landing/governance-privacy-security/encryption.md) voor meer informatie.

### Datagovernance {#governance}

De gegevensstromen gebruiken de ingebouwde mogelijkheden van het gegevensbeheer van Experience Platform om gevoelige gegevens te verhinderen worden verzonden naar de niet-HIPAA-klaar diensten. Door specifieke gebieden te etiketteren die gevoelige gegevens in uw gegevensstroomschema&#39;s bevatten, kunt u korrelige controle nemen over welke gegevensgebieden voor specifieke doeleinden kunnen worden gebruikt.

De volgende video verstrekt een kort overzicht van hoe de beperkingen van het gegevensgebruik voor gegevensstromen in UI worden gevormd en worden afgedwongen:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

In Experience Platform, kunt u [ gevoelige etiketten van het gegevensgebruik ](../data-governance/labels/reference.md#sensitive) op schema&#39;s en gebieden toepassen die gegevens bevatten die uw organisatie gevoelig acht. Het label `RHD` wordt bijvoorbeeld gebruikt om PHI-gegevens (Protected Health Information) aan te geven en het label `S1` geeft gegevens over de geolocatie aan.

>[!NOTE]
>
>Voor details op hoe te om de etiketten van het gegevensgebruik binnen het [!UICONTROL Schemas] lusje in Experience Platform UI of de Inzameling UI van Gegevens toe te passen, zie het [ schema etiketterend leerprogramma ](../xdm/tutorials/labels.md).

Wanneer u een gegevensstroom creeert, als het geselecteerde schema gevoelige etiketten van het gegevensgebruik bevat, kunt u de gegevensstroom slechts vormen om die gegevens naar bestemmingen te verzenden HIPAA-klaar. Momenteel, is de enige bestemming HIPAA-klaar die door gegevensstromen wordt gesteund Adobe Experience Platform. Andere bestemmingsdiensten met inbegrip van Adobe Target, Adobe Analytics, Adobe Audience Manager, gebeurtenis het door:sturen, en randbestemmingen zijn gehandicapt voor gegevensstromen die gevoelige etiketten van het gegevensgebruik bevatten.

Als een schema in een bestaande gegevensstroom met de niet-HIPAA-klaar diensten wordt gebruikt, die een gevoelig etiket van het gegevensgebruik aan het schema proberen toe te voegen resulteert in een bericht van de beleidsschending en de actie wordt verhinderd. Het bericht specificeert welke datastream de schending teweegbracht en stelt voor om het even welke niet-HIPAA-klaar diensten uit de datastream te verwijderen om de kwestie op te lossen.

### Controlelogboeken

In Experience Platform kunnen gegevensstroomactiviteiten worden gecontroleerd in de vorm van auditlogboeken. De logboeken van de controle wijzen op **die** **uitvoerde wat** actie, en **wanneer**, samen met andere contextafhankelijke gegevens die u kunnen helpen kwesties met betrekking tot gegevensstromen problemen oplossen om uw zaken te helpen aan het beleid en de regelgevende vereisten van het collectieve gegevensbeheer voldoen.

Wanneer een gebruiker een gegevensstroom maakt, bijwerkt of verwijdert, wordt een controlelogboek gemaakt om de handeling op te nemen. Het zelfde komt voor wanneer een gebruiker creeert, bijwerkt, of schrapt een afbeelding door [ Prep van Gegevens voor de Inzameling van Gegevens ](./data-prep.md). Ongeacht of het een gegevensstroom of een afbeelding was die werd bijgewerkt, wordt het resulterende controlelogboek gecategoriseerd onder het [!UICONTROL Datastreams] middeltype.

Zie de documentatie op [ controlelogboeken ](../landing/governance-privacy-security/audit-logs/overview.md) voor meer informatie over hoe te om logboeken van gegevensstromen en andere gesteunde diensten te interpreteren.

## Volgende stappen

Deze gids verstrekte een overzicht op hoog niveau van gegevensstromen en hun gebruik in de Inzameling van Gegevens en de verwerking van gevoelige gegevens. Voor stappen op hoe te opstelling een nieuwe gegevensstroom, zie de [ gids van de gegevensstroomconfiguratie ](./configure.md).
