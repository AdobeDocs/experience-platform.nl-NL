---
title: Gegevensversleuteling in Adobe Experience Platform
description: Leer hoe gegevens worden gecodeerd tijdens de doorvoer en in rust in Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---

# Gegevenscodering in Adobe Experience Platform

Adobe Experience Platform is een krachtig en uitbreidbaar systeem dat gegevens over de klantervaring centraliseert en standaardisert voor alle bedrijfsoplossingen. Alle gegevens die door Experience Platform worden gebruikt, worden doorgestuurd en in rust gecodeerd om uw gegevens veilig te houden. In dit document worden de Experience Platform-versleutelingsprocessen op een hoog niveau beschreven.

In het volgende stroomdiagram ziet u hoe Experience Platform gegevens inneemt, codeert en doorhoudt:

![ een diagram dat illustreert hoe het gegeven wordt ingebed, gecodeerd, en door Experience Platform voortgeduurd.](../images/governance-privacy-security/encryption/flow.png)

## Gegevens in doorvoer {#in-transit}

Alle gegevens in doorgang tussen Experience Platform en om het even welke externe component worden geleid over veilige, gecodeerde verbindingen gebruikend HTTPS [ TLS v1.2 ](https://datatracker.ietf.org/doc/html/rfc5246).

In het algemeen worden gegevens op drie manieren naar Experience Platform overgebracht:

- ](../../collection/home.md) mogelijkheden van de inzameling van 0} Gegevens {staan websites en mobiele toepassingen toe om gegevens naar Experience Platform Edge Network voor het opvoeren en voorbereiding voor opname te verzenden.[
- [ de schakelaars van Source ](../../sources/home.md) stroomgegevens direct aan Experience Platform van de toepassingen van Adobe Experience Cloud en andere bronnen van ondernemingsgegevens.
- De niet-Adobe ETL (extract, transformatie, lading) hulpmiddelen verzenden gegevens naar [ partij ingestie API ](../../ingestion/batch-ingestion/overview.md) voor consumptie.

Nadat het gegeven in het systeem is gebracht en [ in rust ](#at-rest) gecodeerd, verrijken de diensten van Experience Platform en voeren de gegevens op de volgende manieren uit:

- [ Doelen ](../../destinations/home.md) staan u toe om gegevens aan de toepassingen van Adobe en partnertoepassingen te activeren.
- De inheemse toepassingen van Experience Platform zoals [ Customer Journey Analytics ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html) en [ Adobe Journey Optimizer ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/ajo-home) kunnen ook gebruik van de gegevens maken.

### mTLS-protocolondersteuning {#mtls-protocol-support}

U kunt Wederzijdse Veiligheid van de Laag van het Vervoer (mTLS) nu gebruiken om verbeterde veiligheid in uitgaande verbindingen aan de [ bestemming van HTTP API ](../../destinations/catalog/streaming/http-destination.md) en de douaneacties van Adobe Journey Optimizer [ te verzekeren ](https://experienceleague.adobe.com/nl/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions). mTLS is een end-to-end veiligheidsmethode voor wederzijdse authentificatie die ervoor zorgt dat beide partijen die informatie delen wie zij beweren te zijn alvorens de gegevens worden gedeeld. mTLS bevat een extra stap in vergelijking met TLS, waarin de server ook om het certificaat van de client vraagt en dit aan het einde verifieert.

Als u mTLS met de douaneacties van Adobe Journey Optimizer ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration) en de bestemmingswerkschema&#39;s van HTTP van Experience Platform wilt [ gebruiken API, moet het serveradres u in de UI van de klantenactie van Adobe Journey Optimizer of de Doelen UI heeft onbruikbaar gemaakte protocollen van TLS hebben en slechts mTLS toegelaten. Als het TLS 1.2 protocol nog op dat eindpunt wordt toegelaten, wordt geen certificaat verzonden voor de cliëntauthentificatie. Dit betekent dat om mTLS met deze werkschema&#39;s te gebruiken, moet uw &quot;ontvangende&quot;servereindpunt een mTLS **slechts** toegelaten verbindingspunt zijn.

>[!IMPORTANT]
>
>Er is geen aanvullende configuratie vereist in uw aangepaste Adobe Journey Optimizer-actie of HTTP API-bestemming om mTLS te activeren. Dit proces wordt automatisch uitgevoerd wanneer een mTLS-ingeschakeld eindpunt wordt gedetecteerd. De Common Name (CN) en de Alternative Names van het Onderwerp (San) voor elk certificaat zijn beschikbaar in de documentatie als deel van het certificaat en kunnen als extra laag van bezitsbevestiging worden gebruikt als u dit wenst.
>
>RFC 2818, gepubliceerd in mei 2000, vervangt het gebruik van het gebied van de Gemeenschappelijke Naam (CN) in HTTPS certificaten voor onderwerpnaamcontrole. In plaats daarvan wordt aangeraden de extensie &quot;Alternatieve naam onderwerp&quot; (SAN) van het type &quot;naam dns&quot; te gebruiken.

### Certificaten downloaden {#download-certificates}

>[!NOTE]
>
>Het is uw verantwoordelijkheid om het openbare certificaat up-to-date te houden. Controleer of u het certificaat regelmatig controleert, vooral wanneer de vervaldatum nadert. U moet een bladwijzer maken van deze pagina om de laatste kopie in uw omgeving te behouden.

Als u de CN of SAN wilt controleren voor aanvullende validatie door derden, kunt u de relevante certificaten hier downloaden:

- [ het openbare certificaat van Adobe Journey Optimizer ](../images/governance-privacy-security/encryption/AJO-public-certificate.pem)
- [ het openbare certificaat van de Dienst van Doelen ](../images/governance-privacy-security/encryption/destinations-public-cert.pem).

U kunt openbare certificaten ook veilig terugwinnen door een verzoek van GET aan het eindpunt MTLS te doen. Zie de [ openbare documentatie van het certificaateindpunt ](../../data-governance/mtls-api/public-certificate-endpoint.md) voor meer informatie.

## Gegevens in rust {#at-rest}

Gegevens die door Experience Platform worden opgenomen en gebruikt, worden opgeslagen in het datumpigment, een zeer granulaire gegevensopslag die alle gegevens bevat die door het systeem worden beheerd, ongeacht de oorsprong of bestandsindeling. Alle gegevens die in het gegevensmeer worden voortgeduurd worden gecodeerd, opgeslagen en in een geïsoleerde [[!DNL Microsoft Azure Data Lake]  instantie van de Opslag ](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) beheerd die aan uw organisatie uniek is.

Voor details op hoe de gegevens in rust in de Azure Opslag van het meer van Gegevens worden gecodeerd, zie de [ officiële Azure documentatie ](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Volgende stappen

Dit document biedt een uitgebreid overzicht van de manier waarop gegevens in Experience Platform worden gecodeerd. Voor meer informatie over veiligheidsprocedures in Experience Platform, zie het overzicht over [ bestuur, privacy, en veiligheid ](./overview.md) op Experience League, of neem een blik bij [ de veiligheidwhitepaper van Experience Platform ](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
