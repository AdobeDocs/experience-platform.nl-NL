---
title: (Bèta) Voeg eerste-partijprofielen met partner-verstrekte attributen toe
description: Leer hoe te om eerste-partijprofielen met attributen van vertrouwde op gegevenspartners aan te vullen om uw gegevensstichting te verbeteren, nieuwe inzichten in uw klantenbasis, en betere publieksoptimalisering te verkrijgen
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: c4f34afb7a05707ed9f62f09685ff50a1de2ef93
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 0%

---

# Voeg eerste-partijprofielen met partner-verstrekte attributen toe

>[!AVAILABILITY]
>
>* Deze bètafunctionaliteit is beschikbaar voor klanten die een licentie hebben verkregen voor Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-time CDP, Real-Time CDP Premiere, Real-Time CDP Ultimate. Meer informatie over deze pakketten vindt u in het dialoogvenster [productbeschrijvingen](https://helpx.adobe.com/legal/product-descriptions.html) en neem contact op met uw Adobe-vertegenwoordiger voor meer informatie.

Voeg eerst-partijprofielen met attributen van vertrouwde op gegevenspartners toe om uw gegevensstichting te verbeteren en nieuwe inzichten in uw klantenbasis te verkrijgen en betere publieksoptimalisering te bereiken.

![Verrijken profielen met door partners opgegeven kenmerken gebruiken een visueel overzicht op hoog niveau.](/help/rtcdp/assets/partner-data/enrichment-use-case-overview.png)

## Vereisten en planning {#prerequisites-and-planning}

Aangezien u overweegt om uw eigen first-party profielen met attributen van gegevenspartners aan te vullen, zou u de volgende details over de lijn van de gegevensverrijking met de gegevenspartner moeten bespreken en richten:

* Denk aan de locatie waar de publiekslijst uit Real-Time CDP wordt geëxporteerd, zodat deze met de leverancier van gegevens kan worden gedeeld. Deze locatie moet het exporteren van bestanden ondersteunen.
* Wat zijn de herkenningstekens die door de gegevensverkoper worden verwacht zodat kunnen zij op extra attributen laag?
* Hoe zal het dossier dat partner-verstrekte attributen bevat terug in real time CDP worden opgenomen? De bestanden kunnen bijvoorbeeld worden ingevoerd via cloudopslagbronconnectors, zoals [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) of [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* Wat is het gemak waarmee u partner-verstrekte attributen om teruggebracht naar Real-Time CDP en verfrist verwacht te worden?

>[!WARNING]
>
>De extra door partners opgegeven kenmerken die in Real-Time CDP worden ingevoerd, zijn van invloed op uw *gemiddelde profielrijkheid*. Lees de [Real-time Customer Data Platform-productbeschrijving](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) voor meer informatie over profielrijkdom.

## Hoe wordt het gebruiksgeval bereikt: overzicht op hoog niveau {#achieve-the-use-case-high-level}

![Verrijken profielen met door partners opgegeven kenmerken gebruiken een visueel overzicht op hoog niveau.](/help/rtcdp/assets/partner-data/enrichment-use-case-steps.png)

1. Als **klant**, geeft u licenties voor kenmerken van de **gegevenspartner**.
2. Als **klant**, breidt u uw profielgegevens en governancemodel uit om **partner**-provided attributes.
3. Als **klant** Aan boord gaat u het publiek dat u wilt verrijken met de gegevenspartner. Over het algemeen worden deze doelgroepen afgezet tegen invoer-id&#39;s, zoals PII-elementen (Personeel Identified Information), zoals e-mail, naam, adres of andere elementen.
4. De **partner** voegt gelicentieerde kenmerken toe voor de profielen waarmee ze kunnen overeenkomen. Optioneel: [Partner-id](/help/identity-service/namespaces.md) kan in partner worden omvat en worden opgenomen scoped identiteitskaart namespace.
5. Als **klant**, laadt u kenmerken van de gegevenspartner in klantprofielen in Real-Time CDP.

## Hoe wordt het gebruiksgeval bereikt: Stapsgewijze instructies {#step-by-step-instructions}

Lees de onderstaande secties door, die koppelingen naar verdere documentatie bevatten, om alle stappen in het bovenstaande overzicht op hoog niveau te voltooien.

### De attributen van de vergunning van de partner {#license-attributes-from-partner}

Deze stap wordt behandeld in de eerste vereisten en Adobe veronderstelt dat u de juiste contractuele overeenkomsten met vertrouwde gegevensverkopers hebt om uw eerste partijprofielen te verhogen.

### Breid uw profielgegevens en governancemodel uit om partner-verstrekte attributen aan te passen. {#extend-governance-model}

Op dit punt, breidt u uw gegevensbeheerkader in Real-Time CDP uit om partner-verstrekte attributen aan te passen.

U kunt nu een nieuw schema maken van de **[!UICONTROL XDM Individual Profile]** klasse, of breid een bestaand schema van het zelfde type uit om partner-verstrekte attributen te omvatten. Adobe adviseert sterk om een nieuw schema met een nieuwe reeks gebiedsgroepen te creëren die de extra attributen van de gegevensverkoper het best vertegenwoordigen. Dit zorgt ervoor dat uw gegevensschema&#39;s schoon zijn en van elkaar onafhankelijk kunnen evolueren.

Om partner-verstrekte attributen in een schema te omvatten, kunt u of een nieuwe gebiedsgroep met de attributen tot stand brengen die u verwacht, of u kunt één van de uit-van-de-doos gebiedsgroepen gebruiken die door Adobe worden verstrekt.

Lees de documentatiepagina&#39;s hieronder voor meer informatie:

* [De grondbeginselen van de schemacompositie](/help/xdm/schema/composition.md)
* [Overzicht van de [!UICONTROL XDM Individual Profile] class](/help/xdm/classes/individual-profile.md)
* [Schema&#39;s maken en bewerken in de gebruikersinterface](/help/xdm/ui/resources/schemas.md)
* [Groepen schemavelden maken en bewerken in de gebruikersinterface](/help/xdm/ui/resources/field-groups.md)
* [Schema&#39;s maken en bewerken met de API](/help/xdm/api/schemas.md#create)
* [Een bestaand schema bijwerken om veldgroepen toe te voegen met behulp van de API](/help/xdm/api/schemas.md#patch)
* Koppeling maken naar nieuwe documentatiepagina van veldgroep wanneer deze bestaat

Ook in deze stap, denk over hoe uw model van gegevensbeheer verandert aangezien u uw gegevensbeheerstrategie uitbreidt om dergegevens te omvatten die door de partner worden verstrekt. Verken de overwegingen in de documentatiekoppelingen hieronder:

* (**Binnenkort beschikbaar**) Gegevens van derden in een aparte gegevensset houden, zodat het verwijderen en ongedaan maken van integraties eenvoudig is
* (**Binnenkort beschikbaar**) Gebruik TTL op de dataset voor cliënten die de gegevenshygiëne toe:voegen-on hebben
* (**Binnenkort beschikbaar**) Voorzichtigheid betrachten bij het maken van afgeleide gegevenssets die gegevens van derden opvragen, omdat de enige oplossing om de gegevens van derden te verwijderen, na elkaar bestaat uit het verwijderen van de gehele afgeleide gegevensset

>[!TIP]
>
>Als u ervoor kiest om uw klantprofielen aan te vullen met een op personen gebaseerde id van de gegevensleverancier, kunt u een nieuw identiteitstype van het type maken **[[!UICONTROL Partner ID]](/help/identity-service/namespaces.md)**.
>
>Lees meer over Partner ID in [sectie met identiteitstypen](/help/identity-service/namespaces.md).
> Meer informatie [identiteitsvelden definiëren](/help/xdm/ui/fields/identity.md) in de gebruikersinterface van het Experience Platform.


### Exporteer het publiek dat u wilt verrijken met PII (Personal Identified Information) of Hashed-PII {#export-audiences}

Exporteer het publiek dat de partner moet verrijken. Gebruik de bestemmingen van de wolkenopslag die door CDP in real time, zoals Amazon S3 of SFTP worden verstrekt. Lees de volgende documentatiepagina&#39;s om deze stap te voltooien:

* [Amazon S3-bestemming](/help/destinations/catalog/cloud-storage/amazon-s3.md) documentatiepagina
* [SFTP-bestemming](/help/destinations/catalog/cloud-storage/sftp.md) documentatiepagina
* Procedure [verbinding maken met een doel](/help/destinations/ui/connect-destination.md)
* Procedure [gegevens exporteren naar een locatie voor cloudopslag](/help/destinations/ui/activate-batch-profile-destinations.md)


### De partner voegt erkende attributen voor de profielen toe die zij tegenover kunnen aanpassen {#partner-appends-attributes}

In deze stap, voegt de partner vergunning gegeven attributen voor het uitgevoerde publiek toe. De uitvoer is over het algemeen beschikbaar als een plat bestand dat weer in Real-Time CDP kan worden ingevoerd.

### Real-Time CDP voegt verrijkte kenmerken toe aan het klantprofiel {#ingest-data}

U moet nu gegevens van de partner door een bronschakelaar opnemen om de verrijkte gegevens terug naar Real-Time CDP te brengen en uw profielen met partner-verstrekte gegevens aan te vullen.

Sommige geadviseerde bronschakelaars voor dit doel zouden kunnen zijn:

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## Beperkingen en problemen oplossen {#limitations-and-troubleshooting}

Houd rekening met de volgende beperkingen wanneer u het op deze pagina beschreven gebruiksgeval bekijkt:

Als u om Partner IDs te gebruiken selecteert, merk op dat deze niet worden gebruikt in om uw te bouwen [identiteitsgrafiek](/help/identity-service/ui/identity-graph-viewer.md).

## Andere gebruiksgevallen die worden bereikt via ondersteuning van partnergegevens {#other-use-cases}

Verken verdere gebruiksgevallen die door de steun van partnergegevens in Real-Time CDP worden toegelaten:

* (**Binnenkort beschikbaar**) [!BADGE Beta]{type=Informative}**Leverancier met hulp van erkenning** voor het aanpassen van de ervaringen ter plaatse tijdens het bezoek en voor het opnieuw toewijzen van doelen na het bezoek, zonder dat de gebruiker dit heeft geverifieerd of een eerdere geschiedenis met uw merk heeft.
* (**Binnenkort beschikbaar**) [!BADGE Beta]{type=Informative}**Uitgebreide activering** het gebruiken van Partner IDs aan het publiceren van ecosystemen die geen PII of gehakt PII goedkeuren.