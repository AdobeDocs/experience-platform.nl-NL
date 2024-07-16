---
title: Overzicht gegevensstromen
description: Leer hoe de gegevensstromen u helpen uw cliënt-zijintegratie van Experience Platform SDK met de producten van de Adobe en derdebestemmingen verbinden.
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---

# Overzicht gegevensstromen

Een gegevensstroom vertegenwoordigt de server-zijconfiguratie wanneer het uitvoeren van het Web van Adobe Experience Platform en Mobiele SDKs. Terwijl de opdracht [`configure`](/help/web-sdk/commands/configure/overview.md) in de SDK de zaken bepaalt die op de client moeten worden afgehandeld (zoals `edgeDomain` ), verwerken gegevensstromen alle andere configuraties voor de SDK. Wanneer een aanvraag naar de Adobe Experience Platform-Edge Network wordt verzonden, wordt `edgeConfigId` gebruikt om naar de gegevensstroom te verwijzen. Hierdoor kunt u de serverconfiguratie bijwerken zonder dat u codewijzigingen hoeft aan te brengen op uw website.

U kunt gegevensstromen tot stand brengen en beheren door **[!UICONTROL Datastreams]** in de linkernavigatie binnen de UI van Adobe Experience Platform of UI van de Inzameling van Gegevens te selecteren.

![ Het lusje van gegevensstromen in UI ](assets/overview/datastreams-tab.png)

Voor meer informatie over hoe te om een gegevensstroom in UI te vormen, zie de [ configuratiegids ](./configure.md).

## Vertrouwelijke gegevens in gegevensstromen verwerken {#sensitive}

>[!IMPORTANT]
>
>De inhoud van dit document is geen juridisch advies en is niet bedoeld ter vervanging van juridisch advies. Raadpleeg de juridische afdeling van uw bedrijf voor advies over de verwerking van gevoelige gegevens.

Het beleid en de regelgevende vereisten van het bedrijfsgegevensbeheer verhogen beperkingen op hoe de gevoelige klantengegevens kunnen worden verzameld, worden verwerkt, en worden gebruikt. Dit omvat het verzamelen, verwerken en gebruiken van beschermde gezondheidsgegevens (PHI), die onderworpen zijn aan regelingen zoals de Health Insurance Portability and Accountability Act (HIPAA).

De stromen van gegevensstromen verstrekt drie methodes om u bij de veilige behandeling van uw gevoelige gegevens te helpen:

* [Verbeterde codering](#encryption)
* [Gegevensbeheer](#governance)
* [Controlelogboeken](#audit-logs)

### Verbeterde codering {#encryption}

Alle gegevens in doorgang door de Edge Network over veilige, gecodeerde verbindingen wordt geleid gebruikend [ HTTPS TLS 1.2 ](https://datatracker.ietf.org/doc/html/rfc5246). Als de gegevensstroom gegevens in Experience Platform brengt, worden de gegevens dan gecodeerd in rust in het de gegevensmeer van het Experience Platform. Zie het document over [ gegevensencryptie in Experience Platform ](../landing/governance-privacy-security/encryption.md) voor meer informatie.

### Gegevensbeheer {#governance}

De stromen van gegevens gebruiken de Experience Platform ingebouwde mogelijkheden van het gegevensbeheer om gevoelige gegevens te verhinderen worden verzonden naar de niet-HIPAA-klaar diensten. Door specifieke gebieden te etiketteren die gevoelige gegevens in uw gegevensstroomschema&#39;s bevatten, kunt u korrelige controle nemen over welke gegevensgebieden voor specifieke doeleinden kunnen worden gebruikt.

De volgende video verstrekt een kort overzicht van hoe de beperkingen van het gegevensgebruik voor gegevensstromen in UI worden gevormd en worden afgedwongen:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

In Experience Platform, kunt u [ gevoelige etiketten van het gegevensgebruik ](../data-governance/labels/reference.md#sensitive) op schema&#39;s en gebieden toepassen die gegevens bevatten die uw organisatie gevoelig acht. Het label `RHD` wordt bijvoorbeeld gebruikt om PHI-gegevens (Protected Health Information) aan te geven en het label `S1` geeft gegevens over de geolocatie aan.

>[!NOTE]
>
>Voor details op hoe te om de etiketten van het gegevensgebruik binnen het [!UICONTROL Schemas] lusje in het Experience Platform UI of de Inzameling UI van Gegevens toe te passen, zie het [ schema etiketterend leerprogramma ](../xdm/tutorials/labels.md).

Wanneer u een gegevensstroom creeert, als het geselecteerde schema gevoelige etiketten van het gegevensgebruik bevat, kunt u de gegevensstroom slechts vormen om die gegevens naar bestemmingen te verzenden HIPAA-klaar. Momenteel, is de enige bestemming HIPAA-klaar die door gegevensstromen wordt gesteund Adobe Experience Platform. Andere bestemmingsdiensten met inbegrip van Adobe Target, Adobe Analytics, Adobe Audience Manager, gebeurtenis het door:sturen, en randbestemmingen zijn gehandicapt voor gegevensstromen die gevoelige etiketten van het gegevensgebruik bevatten.

Als een schema in een bestaande gegevensstroom met de niet-HIPAA-klaar diensten wordt gebruikt, die een gevoelig etiket van het gegevensgebruik aan het schema proberen toe te voegen resulteert in een bericht van de beleidsschending en de actie wordt verhinderd. Het bericht specificeert welke datastream de schending teweegbracht en stelt voor om het even welke niet-HIPAA-klaar diensten uit de datastream te verwijderen om de kwestie op te lossen.

### Controlelogboeken

In Experience Platform kunnen gegevensstroomactiviteiten worden gecontroleerd in de vorm van auditlogboeken. De logboeken van de controle wijzen op **die** **uitvoerde wat** actie, en **wanneer**, samen met andere contextafhankelijke gegevens die u kunnen helpen kwesties met betrekking tot gegevensstromen problemen oplossen om uw zaken te helpen aan het beleid en de regelgevende vereisten van het collectieve gegevensbeheer voldoen.

Wanneer een gebruiker een gegevensstroom maakt, bijwerkt of verwijdert, wordt een controlelogboek gemaakt om de handeling op te nemen. Het zelfde komt voor wanneer een gebruiker creeert, bijwerkt, of schrapt een afbeelding door [ Prep van Gegevens voor de Inzameling van Gegevens ](./data-prep.md). Ongeacht of het een gegevensstroom of een afbeelding was die werd bijgewerkt, wordt het resulterende controlelogboek gecategoriseerd onder het [!UICONTROL Datastreams] middeltype.

Zie de documentatie op [ controlelogboeken ](../landing/governance-privacy-security/audit-logs/overview.md) voor meer informatie over hoe te om logboeken van gegevensstromen en andere gesteunde diensten te interpreteren.

## Volgende stappen

Deze gids verstrekte een overzicht op hoog niveau van gegevensstromen en hun gebruik in de Inzameling van Gegevens en de verwerking van gevoelige gegevens. Voor stappen op hoe te opstelling een nieuwe gegevensstroom, zie de [ gids van de gegevensstroomconfiguratie ](./configure.md).
