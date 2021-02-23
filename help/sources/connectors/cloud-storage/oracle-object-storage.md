---
keywords: Experience Platform;home;populaire onderwerpen;Oracle Object Storage;oracle-objectopslag
solution: Experience Platform
title: Overzicht van Oracle Object Storage Source Connector
topic: ' - overzicht'
description: Leer hoe u Oracle Object Storage met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
translation-type: tm+mt
source-git-commit: 04c605aedd4c52b54d0f075c169ce919650cdee9
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# Oracle Object Storage-connector

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform], zodat u gegevens van deze systemen in Platform kunt brengen voor gebruik in downstreamservices en -bestemmingen.

Met bronnen voor cloudopslag kunt u uw gegevens in het Platform plaatsen zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in de bronwerkstroom. Met Platform kunt u gegevens uit [!DNL Oracle Object Storage] tot batches invoegen.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) document voor meer informatie.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag:

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- Directory- en bestandsnamen mogen niet eindigen met een slash (`/`). Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?`.
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens niet toegestaan, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.). Zie [RFC 2616, Section 2.2 voor regels die Unicode-tekenreeksen in HTTP/1.1 besturen: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM4, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (..), en twee stiptekens (.).

## [!DNL Oracle Object Storage] verbinden met Platform

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen Oracle Object Storage en Adobe Experience Platform via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een Oracle Object Storage-bronverbinding maken met de Flow Service API](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [Een systeem voor cloudopslag verkennen met de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Gegevens voor cloudopslag verzamelen met de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### De gebruikersinterface gebruiken

- [Een Oracle Object Storage-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [Een gegevensstroom configureren voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)