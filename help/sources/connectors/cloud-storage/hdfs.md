---
keywords: Experience Platform;home;populaire onderwerpen;HDFS;hdfs;Apache HDFS;apache hdfs
solution: Experience Platform
title: HDFS-aansluiting
topic: overview
description: In de onderstaande documentatie vindt u informatie over het aansluiten van Apache HDFS op een Platform met behulp van API's of de gebruikersinterface.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# (Bèta) [!DNL Apache] HDFS-connector

>[!NOTE]
>
>De Apache HDFS-connector is in bèta. Zie [Bronoverzicht](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform] en [!DNL Azure], zodat u uw gegevens van deze systemen kunt overbrengen. Ingebedde gegevens kunnen worden opgemaakt als JSON, Parquet of gescheiden. Ondersteuning voor leveranciers van cloudopslag omvat [!DNL Apache] HDFS.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) pagina voor meer informatie.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- Directory- en bestandsnamen mogen niet eindigen met een slash (`/`). Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?`.
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Zie [RFC 2616, Section 2.2 voor regels die Unicode-tekenreeksen in HTTP/1.1 besturen: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM4, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (..), en twee stiptekens (.).

## [!DNL Apache] HDFS aansluiten op [!DNL Platform]

In de onderstaande documentatie vindt u informatie over het aansluiten van [!DNL Apache] HDFS op [!DNL Platform] via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een HDFS-aansluiting maken met de Flow Service API](../../tutorials/api/create/cloud-storage/hdfs.md)
- [Een systeem voor cloudopslag verkennen met de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Gegevens voor cloudopslag verzamelen met de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### De gebruikersinterface gebruiken

- [Een Apache HDFS-bronaansluiting maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/hdfs.md)
- [Een gegevensstroom configureren voor een aansluiting voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)