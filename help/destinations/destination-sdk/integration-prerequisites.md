---
description: Om Destination SDK te gebruiken, moet een partnerbedrijf aan de eerste vereisten voldoen die in dit document worden vermeld.
title: Integratievereisten
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Integratievereisten

Om Destination SDK te gebruiken, zorg ervoor dat u aan de technische en partnerschapeerste vereisten voldoet die in de hieronder secties worden vermeld.

## Technische en API-vereisten voor streamingdoelen {#streaming-prerequisites}

1. U hebt een REST API eindpunt voor Adobe Experience Platform om de volgende types van gegevens te leveren aan:
   * Publiek lidmaatschapsinformatie;
   * Profielidentiteitsgegevens;
   * (Optioneel) Aanvullende kenmerken voor profielverrijking.
2. Uw REST API eindpunt steunt basis, dragertoken, of de OAuth 2.0 authentificatieprotocollen.
3. (Optioneel) U hebt een publiek dat API- of API- of API-eindpunt voor programmatisch metagegevensbeheer maakt/bijwerkt/verwijdert.

## Technische vereisten voor batchbestemmingen {#batch-prerequisites}

1. U hebt een doellocatie die wordt gehost op [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], [!DNL SFTP], [!DNL Google Cloud], of een particulier [!DNL Data Landing Zone], waar u bestanden kunt ontvangen die uit het Experience Platform zijn geëxporteerd.
2. Uw doelplatform kan bestanden opnemen in de indeling die is geconfigureerd via het [opties voor bestandsindeling](functionality/destination-server/file-formatting.md) in Destination SDK voor batchbestemmingen.
3. (Optioneel) U hebt een publiek dat bestanden maakt, ophaalt, bijwerkt of verwijdert ([!DNL CRUD]) API- of API-eindpunt voor programmatisch metagegevensbeheer.

## Partnerschapvoorwaarden {#partnership-prerequisites}

Als u een Onafhankelijke Verkoper van de Software (ISV) of Integrator van het Systeem (SI) bent die Destination SDK probeert te gebruiken, lees de partnerschapvereisten voor ISVs en SIs in [toegang krijgen tot sectie](overview.md#get-access).
