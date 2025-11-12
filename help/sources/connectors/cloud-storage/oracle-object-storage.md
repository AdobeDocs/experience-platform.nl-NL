---
keywords: Experience Platform;home;populaire onderwerpen;Oracle Object Storage;orace object storage
solution: Experience Platform
title: Oracle Object Storage Source Connector - Overzicht
description: Leer hoe u Oracle Object Storage met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: 5e8b85c8-9f01-49a6-9556-7b9c7518fb4b
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Oracle Object Storage-connector

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS [!DNL Google Cloud Platform] , zodat u gegevens van deze systemen naar Experience Platform kunt overbrengen voor gebruik in downstreamservices en -doelen.

Opslagbronnen in de cloud kunnen uw gegevens naar Experience Platform brengen zonder dat ze hoeven te worden gedownload, opgemaakt of geüpload. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in de bronwerkstroom. Met Experience Platform kunt u gegevens van [!DNL Oracle Object Storage] tot en met batches inbrengen.

## IP adres lijst van gewenste personen

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform aan te sluiten. Voor meer informatie, lees de gids op [ voegend op lijst van gewenste personen IP adressen om met Experience Platform ](../../ip-address-allow-list.md) voor meer informatie te verbinden.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag:

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- De folder en de dossiernamen kunnen niet met een voorwaartse schuine streep (`/`) beëindigen. Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?` .
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar zijn geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens niet toegestaan, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.). Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [ RFC 2616, Sectie 2.2: BasisRegels ](https://www.ietf.org/rfc/rfc2616.txt) en [ RFC 3987 ](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (.) en twee stippen ( ...).

## Verbinden [!DNL Oracle Object Storage] met Experience Platform

In de onderstaande documentatie vindt u informatie over hoe u Oracle Object Storage via API&#39;s of de gebruikersinterface kunt verbinden met Adobe Experience Platform:

### API&#39;s gebruiken

- [Een Oracle Object Storage-basisverbinding maken met de Flow Service API](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [De gegevensstructuur en inhoud van een cloudopslagbron verkennen met behulp van de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Een gegevensstroom maken voor een cloudopslagbron met behulp van de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### UI gebruiken

- [Een Oracle Object Storage-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [Een gegevensstroom maken voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
