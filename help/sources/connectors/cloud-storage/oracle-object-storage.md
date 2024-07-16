---
keywords: Experience Platform;home;populaire onderwerpen;Oracle Object Storage;oracle object storage
solution: Experience Platform
title: Oracle Object Storage Source Connector - Overzicht
description: Leer hoe u Oracle Object Storage met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: 5e8b85c8-9f01-49a6-9556-7b9c7518fb4b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Oracle Object Storage-connector

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS [!DNL Google Cloud Platform] , zodat u gegevens van deze systemen kunt overbrengen naar Platform voor gebruik in downstreamservices en -doelen.

Met bronnen voor cloudopslag kunt u uw gegevens overbrengen naar Platform zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in de bronwerkstroom. Met Platform kunt u gegevens uit [!DNL Oracle Object Storage] tot en met batches inbrengen.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie het ](../../ip-address-allow-list.md) document van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag:

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- De folder en de dossiernamen kunnen niet met een voorwaartse schuine streep (`/`) beëindigen. Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?` .
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar zijn geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens niet toegestaan, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.). Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [ RFC 2616, Sectie 2.2: BasisRegels ](https://www.ietf.org/rfc/rfc2616.txt) en [ RFC 3987 ](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (.) en twee stippen ( ...).

## Verbinden [!DNL Oracle Object Storage] met platform

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen Oracle Object Storage en Adobe Experience Platform via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een basisverbinding voor Oracle Object Storage maken met de Flow Service API](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [De gegevensstructuur en inhoud van een cloudopslagbron verkennen met behulp van de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Een gegevensstroom maken voor een cloudopslagbron met behulp van de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### UI gebruiken

- [Een Oracle Object Storage-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [Een gegevensstroom maken voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
