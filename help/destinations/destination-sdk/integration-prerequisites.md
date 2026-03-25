---
description: Om Destination SDK te gebruiken, moet een partnerbedrijf aan de eerste vereisten voldoen die in dit document worden vermeld.
title: Integratievereisten
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Integratievereisten

Om Destination SDK te gebruiken, zorg ervoor dat u aan de technische en partnerschapeerste vereisten voldoet die in de hieronder secties worden vermeld.

## Technische vereisten/API-vereisten voor streamingdoelen {#streaming-prerequisites}

1. U hebt een REST API-eindpunt voor [!DNL Adobe Experience Platform] om de volgende gegevenstypen aan te leveren:
   * Publiek lidmaatschapsinformatie;
   * Profielidentiteitsgegevens;
   * (Optioneel) Aanvullende kenmerken voor profielverrijking.
2. Uw REST API eindpunt steunt basis, dragertoken, of de OAuth 2.0 authentificatieprotocollen.
3. (Optioneel) U hebt een publiek dat API- of API- of API-eindpunt voor programmatisch metagegevensbeheer maakt/bijwerkt/verwijdert.

## Technische vereisten voor batchbestemmingen {#batch-prerequisites}

1. U hebt een doellocatie die wordt gehost op [!DNL Amazon S3] , [!DNL Azure Blob] , [!DNL Azure Data Lake Storage] , [!DNL SFTP] , [!DNL Google Cloud] of een private [!DNL Data Landing Zone] , waar u bestanden kunt ontvangen die uit Experience Platform zijn geëxporteerd.
2. Uw bestemmingsplatform kan dossiers in het formaat opnemen dat via de [&#x200B; wordt gevormd dossier het formatteren opties &#x200B;](functionality/destination-server/file-formatting.md) in Destination SDK voor partijbestemmingen.
3. (Optioneel) U hebt een publiek dat API- of API- of API-eindpunt ([!DNL CRUD]) voor programmatisch metagegevensbeheer maakt, ophaalt, bijwerkt of verwijdert.

## Partnerschapvoorwaarden {#partnership-prerequisites}

Als u een Onafhankelijke Verkoper van de Software (ISV) of Integrator van het Systeem (SI) bent die Destination SDK probeert te gebruiken, lees de partnerschapsvereisten voor ISVs en SIs in [&#x200B; die toegangssectie &#x200B;](overview.md#get-access) krijgen.
