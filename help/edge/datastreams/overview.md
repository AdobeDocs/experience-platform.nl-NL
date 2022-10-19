---
title: Overzicht gegevensstromen
description: Sluit de integratie van uw client-side Experience Platform SDK aan op Adobe-producten en andere doelen.
keywords: configuratie;gegevensstreams;datastreamId;edge;datastream id;Environment Settings;edgeConfigId;identity;id sync ingeschakeld;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;clientcode;Eigenschapcontrole;Doel-id;Cookie-doelen;url-doelen;Analytics Settings Blockreport suite ID;Data Prep;Data Prep;Mapper XDM Mapper;Mapper on Edge;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 2cec87d3f45b1b774925a9b669b53a958e65e57a
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# Overzicht gegevensstromen

Een gegevensstroom vertegenwoordigt de server-zijconfiguratie wanneer het uitvoeren van het Web van Adobe Experience Platform en Mobiele SDKs. Terwijl de [configureren, opdracht](../fundamentals/configuring-the-sdk.md) in SDK controleert dingen die op de cliënt (zoals moeten worden behandeld `edgeDomain`), worden in gegevensstreams alle andere configuraties voor de SDK afgehandeld. Wanneer een aanvraag naar het Adobe Experience Platform Edge-netwerk wordt verzonden, `edgeConfigId` wordt gebruikt om naar de gegevensstroom te verwijzen. Hierdoor kunt u de serverconfiguratie bijwerken zonder dat u codewijzigingen hoeft aan te brengen op uw website.

U kunt gegevensstromen tot stand brengen en beheren door te selecteren **[!UICONTROL Datastreams]** in de linkernavigatie binnen de UI van Adobe Experience Platform of UI van de Inzameling van Gegevens.

![Het tabblad Gegevensstromen in de gebruikersinterface](../assets/datastreams/overview/datastreams-tab.png)

Voor meer informatie over hoe te om een gegevensstroom in UI te vormen, zie [configuratiegids](./configure.md).

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

Alle gegevens in doorvoer via het Edge-netwerk worden via beveiligde, gecodeerde verbindingen uitgevoerd met [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Als de gegevensstroom gegevens in Experience Platform brengt, worden de gegevens dan gecodeerd in rust in het de gegevensmeer van het Experience Platform. Document weergeven op [gegevenscodering in Experience Platform](../../landing/governance-privacy-security/encryption.md) voor meer informatie .

### Gegevensbeheer {#governance}

De stromen van gegevensstromen hefboomwerkingen de ingebouwde mogelijkheden van het gegevensbeheer van het Experience Platform om gevoelige gegevens te verhinderen worden verzonden naar de niet-HIPAA-klaar diensten. Door specifieke gebieden te etiketteren die gevoelige gegevens in uw gegevensstroomschema&#39;s bevatten, kunt u korrelige controle nemen over welke gegevensgebieden voor specifieke doeleinden kunnen worden gebruikt.

De volgende video verstrekt een kort overzicht van hoe de beperkingen van het gegevensgebruik voor gegevensstromen in UI worden gevormd en worden afgedwongen:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

In Experience Platform kunt u [labels voor gevoelig gegevensgebruik](../../data-governance/labels/reference.md#sensitive) aan schema&#39;s en gebieden die gegevens bevatten die uw organisatie gevoelig acht. De `RHD` wordt gebruikt om beschermde gezondheidsinformatie (PHI) aan te geven, en `S1` label geeft geolocatiegegevens aan.

>[!NOTE]
>
>Voor meer informatie over het toepassen van labels voor gegevensgebruik in de [!UICONTROL Schemas] tabblad in de gebruikersinterface van het Experience Platform of de gebruikersinterface van de gegevensverzameling, raadpleegt u de [zelfstudie over schemalabels](../../xdm/tutorials/labels.md).

Wanneer het creëren van een nieuwe gegevensstroom, als het geselecteerde schema gevoelige etiketten van het gegevensgebruik bevat, kan de gegevensstroom slechts worden gevormd om die gegevens naar HIPAA-klaar bestemmingen te verzenden. Momenteel, is de enige bestemming HIPAA-klaar die door gegevensstromen wordt gesteund Adobe Experience Platform. Andere bestemmingsdiensten met inbegrip van Adobe Target, Adobe Analytics, Adobe Audience Manager, gebeurtenis het door:sturen, en randbestemmingen zijn gehandicapt voor gegevensstromen die gevoelige etiketten van het gegevensgebruik bevatten.

Als een schema in een bestaande gegevensstroom met de niet-HIPAA-klaar diensten wordt gebruikt, die een gevoelig etiket van het gegevensgebruik aan het schema proberen toe te voegen resulteert in een bericht van de beleidsschending en de actie wordt verhinderd. Het bericht specificeert welke datastream de schending teweegbracht en stelt voor om het even welke niet-HIPAA-klaar diensten uit de datastream te verwijderen om de kwestie op te lossen.

### Controlelogboeken

In Experience Platform kunnen gegevensstroomactiviteiten worden gecontroleerd in de vorm van auditlogboeken. Een controlelogboek vertelt **wie** uitgevoerd **wat** actie, en **wanneer**, samen met andere contextuele gegevens die u kunnen helpen problemen met betrekking tot gegevensstromen oplossen om uw zaken te helpen aan het beleid en de regelgevende vereisten van het collectieve gegevensbeheer voldoen.

Wanneer een gebruiker een gegevensstroom maakt, bijwerkt of verwijdert, wordt een controlelogboek gemaakt om de handeling op te nemen. Dit gebeurt ook wanneer een gebruiker een toewijzing maakt, bijwerkt of verwijdert via [Gegevensvoorvoegsel voor gegevensverzameling](./data-prep.md). Ongeacht of het een gegevensstroom of een afbeelding was die werd bijgewerkt, wordt het resulterende controlelogboek gecategoriseerd onder [!UICONTROL Datastreams] brontype.

Zie de documentatie op [auditlogboeken](../../landing/governance-privacy-security/audit-logs/overview.md) voor meer informatie over hoe te om logboeken van gegevensstromen en andere gesteunde diensten te interpreteren.

## Volgende stappen

Deze gids verstrekte een overzicht op hoog niveau van gegevensstromen en hun gebruik in de Inzameling van Gegevens en de verwerking van gevoelige gegevens. Voor stappen over hoe te opstelling een nieuwe gegevensstroom, zie [configuratiehandleiding voor gegevensstroom](./configure.md).
