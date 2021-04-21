---
keywords: Experience Platform;home;populaire onderwerpen;FTP;ftp;
solution: Experience Platform
title: Overzicht van FTP-bronverbinding
topic-legacy: overview
description: Leer hoe u een FTP-server verbindt met Adobe Experience Platform via API's of de gebruikersinterface.
exl-id: a6186fad-8a7b-4103-80c7-a522ff69fe9e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# (Bèta) FTP-connector

>[!NOTE]
>
>De FTP-connector bevindt zich in bèta. Zie [Bronoverzicht](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform] en [!DNL Azure], zodat u uw gegevens van deze systemen kunt overbrengen.

Opslagbronnen in de cloud kunnen uw eigen gegevens naar [!DNL Platform] brengen zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema. [!DNL Platform] kunt u gegevens van een FTP- of SFTP-server via batches inbrengen.

>[!IMPORTANT]
>
>Bij het maken van een gegevensstroom met de FTP-bronconnector wordt het ten zeerste aanbevolen om een eenmalig insluitingsschema in te stellen omdat er nog steeds problemen zijn met incrementele updates die worden aangetroffen in FTP-servers.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) pagina voor meer informatie.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- Directory- en bestandsnamen mogen niet eindigen met een slash (`/`). Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?`.
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Zie [RFC 2616, Section 2.2 voor regels die Unicode-tekenreeksen in HTTP/1.1 besturen: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM4, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (..), en twee stiptekens (.).

## FTP verbinden met [!DNL Platform]

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen een FTP-server en [!DNL Platform] via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een FTP-bronverbinding maken met de Flow Service API](../../tutorials/api/create/cloud-storage/ftp.md)
- [Een systeem voor cloudopslag verkennen met de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Gegevens voor cloudopslag verzamelen met de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### De gebruikersinterface gebruiken

- [Een FTP-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/ftp.md)
- [Een gegevensstroom configureren voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
