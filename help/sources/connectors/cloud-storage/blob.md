---
keywords: Experience Platform;home;populaire onderwerpen;Blob;blob;Azure Blob;azure blob
solution: Experience Platform
title: Azure Blob Source Connector - Overzicht
topic-legacy: overview
description: Leer hoe u Azure Blob met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: 251da91844311d08766ee2407ae0b775d4ac6aba
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Azure Blob-connector

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform], en [!DNL Azure]. U kunt uw gegevens van deze systemen overbrengen naar [!DNL Platform].

Opslagbronnen in de cloud kunnen uw eigen gegevens overbrengen naar [!DNL Platform] zonder dat het downloaden, opmaken of uploaden nodig is. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema. [!DNL Platform] stelt u in staat gegevens over te brengen van [!DNL Azure Blob] door partijen.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

>[!IMPORTANT]
>
>De [!DNL Azure Blob] de bron steunt geen connectiviteit van zelfde-gebied aan Experience Platform. Als uw Azure instantie het zelfde netwerkgebied zoals Experience Platform gebruikt, dan kan een verbinding aan de bronnen van het Experience Platform niet worden gevestigd. Gebruik niet de Azure East US 2, Azure West Europe en Azure Australia East regions bij het opzetten van uw [!DNL Azure Blob] bron. Momenteel wordt alleen connectiviteit tussen regio&#39;s ondersteund.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- Directory- en bestandsnamen mogen niet eindigen met een slash (`/`). Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?`.
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000`zijn, hoewel geldig in NTFS-bestandsnamen, geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [RFC 2616, punt 2.2: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM4, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (..), en twee stiptekens (.).

## Verbinden [!DNL Azure Blob] tot [!DNL Platform]

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen Azure Blob en Adobe Experience Platform via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een Azure Blob-basisverbinding maken met de Flow Service API](../../tutorials/api/create/cloud-storage/blob.md)
- [De gegevensstructuur en inhoud van een cloudopslagbron verkennen met behulp van de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Een gegevensstroom maken voor een cloudopslagbron met behulp van de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### De gebruikersinterface gebruiken

- [Een Azure Blob-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/blob.md)
- [Een gegevensstroom maken voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
