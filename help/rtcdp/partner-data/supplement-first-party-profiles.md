---
title: Eigen profielen aanvullen met door partners verstrekte attributen
description: Leer hoe u eigen profielen kunt aanvullen met kenmerken van vertrouwde gegevenspartners om uw databasis te verbeteren, nieuwe inzichten in uw klantenbestand te verkrijgen en uw doelgroepen beter te optimaliseren.
feature: Use Cases, Profile Enrichment
exl-id: ee21b988-88f9-4c8e-bd82-7fc55c37ec24
source-git-commit: f9917d6a6de81f98b472cff9b41f1526ea51cdae
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 3%

---

# Eigen profielen aanvullen met door partners verstrekte attributen

>[!AVAILABILITY]
>
>* Deze functionaliteit is beschikbaar voor klanten die een licentie hebben verkregen voor Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Premiere, Real-Time CDP Ultimate. Meer informatie over deze pakketten vindt u in de [productbeschrijvingen](https://helpx.adobe.com/legal/product-descriptions.html) en neem contact op met uw Adobe voor meer informatie.

Voeg eerst-partijprofielen met attributen van vertrouwde op gegevenspartners toe om uw gegevensstichting te verbeteren en nieuwe inzichten in uw klantenbasis te verkrijgen en betere publieksoptimalisering te bereiken.

![Verrijken profielen met door partners opgegeven kenmerken gebruiken een visueel overzicht op hoog niveau.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-overview.png)

## Waarom dit gebruiksgeval overwegen {#why-this-use-case}

De meeste merken, zelfs die die met eerste partijgegevens rijk zijn, kunnen van het stroomlijnen van hun gegevens profiteren en het bereiken van een genuanceerder inzicht in klanten, hun gedrag, patronen, en voorkeur.

Adobe Real-time Customer Data Platform kan merken helpen hun gegevens van de eerste partij op verantwoordelijke wijze aan te vullen met waardevolle inzichten, id&#39;s en kenmerken van een of meer vertrouwde partners.

Adobe begrijpt dat er geen uniforme benadering is en maakt naadloze interoperabiliteit met gegevens en identiteitspartners mogelijk om geïndividualiseerde en doordachte betrokkenheid in alle fasen van de levenscyclus van de klant te bevorderen. Deze mogelijkheden worden geschraagd door een vertrouwd op gegeven governance kader, dat voor genuanceerde controle toestaat op waar en hoe de partnergegevens worden gebruikt. Bijvoorbeeld, kunt u partner verstrekte inzichten voor segmentatie maar niet voor verpersoonlijking willen gebruiken.

Bijvoorbeeld, volg de stappen in dit gebruiksgeval worden beschreven wanneer u uw klantenverslagen met demografische en intentsignalen moet verrijken die.

## Vereisten en planning {#prerequisites-and-planning}

Aangezien u overweegt om uw eigen first-party profielen met attributen van gegevenspartners aan te vullen, zou u de volgende details over de lijn van de gegevensverrijking met de gegevenspartner moeten bespreken en richten:

* Denk aan de locatie waar de publiekslijst uit Real-Time CDP wordt geëxporteerd, zodat deze met de leverancier van gegevens kan worden gedeeld. Deze locatie moet het exporteren van bestanden ondersteunen.
* Wat zijn de herkenningstekens die door de gegevensverkoper worden verwacht zodat kunnen zij op extra attributen laag?
* Hoe zal het dossier dat partner-verstrekte attributen bevat terug in Real-Time CDP worden opgenomen? De bestanden kunnen bijvoorbeeld worden ingevoerd via cloudopslagbronconnectors, zoals [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) of [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* Wat is het gemak waarmee u partner-verstrekte attributen om teruggebracht naar Real-Time CDP en verfrist verwacht te worden?

>[!WARNING]
>
>De extra door partners opgegeven kenmerken die in Real-Time CDP worden ingevoerd, zijn van invloed op uw *gemiddelde profielrijkheid*. Lees de [Real-time Customer Data Platform-productbeschrijving](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) voor meer informatie over profielrijkdom.

## Video doorloopt {#video-walkthrough}

Bekijk hieronder het videoleerprogramma voor een analyse van hoe te om het eerste partijpubliek met partner-verstrekte attributen aan te vullen:

>[!VIDEO](https://video.tv.adobe.com/v/3423075/?learn=on)

## Hoe het gebruiksgeval te bereiken: overzicht op hoog niveau {#achieve-the-use-case-high-level}

![Verrijken profielen met door partners opgegeven kenmerken gebruiken een visueel overzicht op hoog niveau.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-steps.png)

1. Als **klant**, geeft u licenties voor kenmerken van de **gegevenspartner**.
2. Als **klant**, breidt u uw profielgegevens en governancemodel uit om **partner**-provided attributes.
3. Als **klant**, bevindt u zich aan boord van het publiek dat u wilt verrijken met de gegevenspartner. Over het algemeen worden deze doelgroepen afgezet tegen invoer-id&#39;s, zoals PII-elementen (Personeel Identified Information), zoals e-mail, naam, adres of andere elementen.
4. De **partner** voegt gelicentieerde kenmerken toe voor de profielen waarmee ze kunnen overeenkomen. Optioneel: [Partner-id](/help/identity-service/features/namespaces.md) kan in partner worden omvat en worden opgenomen scoped identiteitskaart namespace.
5. Als **klant**, laadt u kenmerken van de gegevenspartner in klantprofielen in Real-Time CDP.

## Hoe het gebruiksgeval te bereiken: Step-by-step instructies {#step-by-step-instructions}

Lees de onderstaande secties door, die koppelingen naar verdere documentatie bevatten, om alle stappen in het bovenstaande overzicht op hoog niveau te voltooien.

### De attributen van de vergunning van de partner {#license-attributes-from-partner}

Deze stap wordt behandeld in [voorwaarden](#prerequisites-and-planning) en de Adobe gaat ervan uit dat u de juiste contractuele overeenkomsten hebt met vertrouwde gegevensleveranciers om uw first-party profielen te verhogen.

### Breid uw profielgegevens en governancemodel uit om partner-verstrekte attributen aan te passen. {#extend-governance-model}

Op dit punt, breidt u uw gegevensbeheerkader in Real-Time CDP uit om partner-verstrekte attributen aan te passen.

U kunt nu een nieuw schema maken van de **[!UICONTROL XDM Individual Profile]** klasse, of breid een bestaand schema van het zelfde type uit om partner-verstrekte attributen te omvatten. De Adobe adviseert sterk om een nieuw schema met een nieuwe reeks gebiedsgroepen tot stand te brengen die de extra attributen van de gegevensverkoper het best vertegenwoordigen. Dit zorgt ervoor dat uw gegevensschema&#39;s schoon zijn en onafhankelijk van elkaar kunnen evolueren.

Om partner-verstrekte attributen in een schema te omvatten, kunt u of een nieuwe gebiedsgroep met de attributen tot stand brengen die u verwacht, of u kunt één van de preconfigured gebiedsgroepen gebruiken die door Adobe worden verstrekt.

Lees de documentatiepagina&#39;s hieronder voor meer informatie:

* [De grondbeginselen van de schemacompositie](/help/xdm/schema/composition.md)
* [Overzicht van de [!UICONTROL XDM Individual Profile] class](/help/xdm/classes/individual-profile.md)
* [Schema&#39;s maken en bewerken in de gebruikersinterface](/help/xdm/ui/resources/schemas.md)
* [Groepen schemavelden maken en bewerken in de gebruikersinterface](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

Ook in deze stap, denk over hoe uw model van gegevensbeheer verandert aangezien u uw gegevensbeheerstrategie uitbreidt om dergegevens te omvatten die door de partner worden verstrekt. Verken de overwegingen in de documentatiekoppelingen hieronder:

* (**Binnenkort beschikbaar**) Houd gegevens van derden in een aparte gegevensset, zodat u deze gegevens eenvoudig kunt verwijderen en integraties ongedaan kunt maken.
* (**Binnenkort beschikbaar**) Gebruik de [gegevenssetvervaldatum](/help/hygiene/ui/dataset-expiration.md) functionaliteit op de dataset voor cliënten die de toe:voegen-op van de gegevenshygiëne kochten.
* (**Binnenkort beschikbaar**) Wees voorzichtig bij het maken van afgeleide gegevenssets die gegevens van derden opvragen, omdat de enige oplossing om de gegevens van derden te verwijderen, na elkaar is dat de gehele afgeleide gegevensset wordt verwijderd.

>[!TIP]
>
>Als u ervoor kiest om uw klantprofielen aan te vullen met een op personen gebaseerde id van de gegevensleverancier, kunt u een nieuw identiteitstype van het type maken **[[!UICONTROL Partner ID]](/help/identity-service/features/namespaces.md)**.
>
>Lees meer over Partner ID in [sectie met identiteitstypen](/help/identity-service/features/namespaces.md).
>Meer informatie [identiteitsvelden definiëren](/help/xdm/ui/fields/identity.md) in de gebruikersinterface van het Experience Platform.

### Exporteer het publiek dat u wilt verrijken wanneer u PII (Personal Identified Information) of PII (hashed-PII) uitschakelt {#export-audiences}

Exporteer het publiek dat de partner moet verrijken. Gebruik de cloudopslagbestemmingen van Real-Time CDP, zoals Amazon S3 of SFTP. Lees de volgende documentatiepagina&#39;s om deze stap te voltooien:

* [Amazon S3-bestemming](/help/destinations/catalog/cloud-storage/amazon-s3.md) documentatiepagina
* [SFTP-bestemming](/help/destinations/catalog/cloud-storage/sftp.md) documentatiepagina
* Procedure [verbinding maken met een doel](/help/destinations/ui/connect-destination.md)
* Procedure [gegevens exporteren naar een locatie voor cloudopslag](/help/destinations/ui/activate-batch-profile-destinations.md)

### Uw gegevenspartner voegt erkende attributen voor de profielen toe die zij kunnen aanpassen {#partner-appends-attributes}

In deze stap, voegt uw gegevenspartner vergunning gegeven attributen voor het uitgevoerde publiek toe. De uitvoer is over het algemeen beschikbaar als een plat bestand dat weer in Real-Time CDP kan worden ingevoerd. Meer informatie over [bestanden opnemen in Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file).

### Real-Time CDP voegt verrijkte kenmerken toe aan het klantprofiel {#ingest-data}

U moet nu gegevens van de partner door een bronschakelaar opnemen om de verrijkte gegevens terug naar Real-Time CDP te brengen en uw profielen met partner-verstrekte gegevens aan te vullen.

Sommige geadviseerde bronschakelaars voor dit doel zouden kunnen zijn:

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## Beperkingen en problemen oplossen {#limitations-and-troubleshooting}

Houd rekening met de volgende beperkingen wanneer u het op deze pagina beschreven gebruiksgeval bekijkt:

* Als u om Partner IDs te gebruiken selecteert, ben zich ervan bewust dat deze IDs niet wanneer het bouwen van uw wordt gebruikt [identiteitsgrafiek](/help/identity-service/features/identity-graph-viewer.md).

## Andere gebruiksgevallen die worden bereikt via ondersteuning van partnergegevens {#other-use-cases}

Verken verdere gebruiksgevallen die door de steun van partnergegevens in Real-Time CDP worden toegelaten:

* Gebruik gegevensondersteuning van derden in Real-Time CDP voor [breid uw profielbasis met perspectiefprofielen van gegevenspartners uit en verbind met hen om nieuwe klanten te verwerven of te bereiken](/help/rtcdp/partner-data/prospecting.md).
* [Onsite ervaringen voor onbekende bezoekers personaliseren met de erkenning van bezoekers met hulp van partners](/help/rtcdp/partner-data/onsite-personalization.md) tijdens het bezoek zonder dat de gebruiker dit heeft geverifieerd of dat hij of zij een eerdere geschiedenis heeft met uw merk.
* [Uitgebreide activering van perspectiefprofielen en perspectiefpubliek](/help/destinations/ui/activate-prospect-audiences.md) om doelen te selecteren.
