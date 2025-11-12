---
title: Azure Data Lake Storage Gen2 Source Connector - overzicht
description: Leer hoe u Azure Data Lake Storage Gen2 kunt verbinden met Adobe Experience Platform via API's of de gebruikersinterface.
exl-id: 424d7278-44d9-4653-82c0-eb21cbb9b623
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Azure Data Lake Storage Gen2-connector

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform] en [!DNL Azure] , zodat u gegevens van deze systemen kunt overbrengen.

Opslagbronnen in de cloud kunnen uw eigen gegevens naar Experience Platform brengen zonder dat ze hoeven te worden gedownload, opgemaakt of geüpload. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema. Met Experience Platform kunt u gegevens van [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) tot en met batches inbrengen.

## IP adres lijst van gewenste personen

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform aan te sluiten. Voor meer informatie, lees de gids op [&#x200B; voegend op lijst van gewenste personen IP adressen om met Experience Platform &#x200B;](../../ip-address-allow-list.md) voor meer informatie te verbinden.

>[!IMPORTANT]
>
>De [!DNL Azure Data Lake Storage Gen2] -bron ondersteunt geen connectiviteit tussen dezelfde regio&#39;s voor Experience Platform. Als uw [!DNL Azure] -instantie hetzelfde netwerkgebied gebruikt als Experience Platform, kan geen verbinding met Experience Platform-bronnen tot stand worden gebracht. Momenteel wordt alleen connectiviteit tussen regio&#39;s ondersteund.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- De folder en de dossiernamen kunnen niet met een voorwaartse schuine streep (`/`) beëindigen. Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?` .
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar zijn geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [&#x200B; RFC 2616, Sectie 2.2: BasisRegels &#x200B;](https://www.ietf.org/rfc/rfc2616.txt) en [&#x200B; RFC 3987 &#x200B;](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (.) en twee stippen ( ...).

## Verbinden [!DNL Azure Data Lake Storage Gen2] met Experience Platform

>[!NOTE]
>
>De dienst belangrijkste die in het creëren van een [!DNL Azure Data Lake Storage Gen2] rekening wordt gebruikt zou minstens de **rol van Reader van de Gegevens van het Blob van de Opslag moeten hebben** van toegangsbeheer (IAM) wordt toegewezen

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Azure Data Lake Storage Gen2] en Experience Platform via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Creeer een  [!DNL Azure Data Lake Storage Gen2]  basisverbinding gebruikend de Dienst API van de Stroom](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [De gegevensstructuur en inhoud van een cloudopslagbron verkennen met behulp van de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Een gegevensstroom maken voor een cloudopslagbron met behulp van de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### UI gebruiken

- [Creeer een  [!DNL Azure Data Lake Storage Gen2]  bronverbinding in UI](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Een gegevensstroom maken voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
