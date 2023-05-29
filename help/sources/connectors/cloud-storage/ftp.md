---
keywords: Experience Platform;home;populaire onderwerpen;FTP;ftp;
solution: Experience Platform
title: Overzicht van FTP-bronverbinding
description: Leer hoe u een FTP-server verbindt met Adobe Experience Platform via API's of de gebruikersinterface.
exl-id: a6186fad-8a7b-4103-80c7-a522ff69fe9e
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# (Bèta) FTP-connector

>[!NOTE]
>
>De FTP-connector bevindt zich in bèta. Zie de [Overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform], en [!DNL Azure], zodat u uw gegevens van deze systemen kunt overbrengen.

Opslagbronnen in de cloud kunnen uw eigen gegevens overbrengen naar [!DNL Platform] zonder dat het downloaden, opmaken of uploaden nodig is. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema. [!DNL Platform] kunt u gegevens van een FTP- of SFTP-server via batches inbrengen.

>[!IMPORTANT]
>
>Bij het maken van een gegevensstroom met de FTP-bronconnector wordt het ten zeerste aanbevolen om een eenmalig insluitingsschema in te stellen omdat er nog steeds problemen zijn met incrementele updates die worden aangetroffen in FTP-servers.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- Directory- en bestandsnamen mogen niet eindigen met een slash (`/`). Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?`.
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000`zijn, hoewel geldig in NTFS-bestandsnamen, geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [RFC 2616, punt 2.2: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM4, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (..), en twee stiptekens (.).

## FTP verbinden met [!DNL Platform]

In de onderstaande documentatie vindt u informatie over hoe u een FTP-server kunt verbinden met [!DNL Platform] API&#39;s of de gebruikersinterface gebruiken:

### API&#39;s gebruiken

- [Een FTP-basisverbinding maken met de Flow Service API](../../tutorials/api/create/cloud-storage/ftp.md)
- [De gegevensstructuur en inhoud van een cloudopslagbron verkennen met behulp van de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Een gegevensstroom maken voor een cloudopslagbron met behulp van de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### De gebruikersinterface gebruiken

- [Een FTP-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/ftp.md)
- [Een gegevensstroom maken voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
