---
keywords: Experience Platform;home;populaire onderwerpen;Azure File Storage;azure bestandsopslag
solution: Experience Platform
title: Azure File Storage Source Connector - Overzicht
topic: overview
description: Leer hoe u Azure File Storage kunt verbinden met Adobe Experience Platform via API's of de gebruikersinterface.
translation-type: tm+mt
source-git-commit: 7fc99214272d2ce743b3666826c66f5d65e4d2ca
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# (Beta) Azure File Storage-connector

>[!NOTE]
>
>De Azure File Storage-connector is in bèta. Zie [Bronoverzicht](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform] en [!DNL Azure], zodat u uw gegevens van deze systemen kunt overbrengen.

Opslagbronnen in de cloud kunnen uw eigen gegevens naar [!DNL Platform] brengen zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema. [!DNL Platform] kunt u gegevens van  [!DNL Azure File Storage] door partijen brengen.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) pagina voor meer informatie.

>[!IMPORTANT]
>
>De [!DNL Azure File Storage] bronschakelaar steunt momenteel zelfde-gebiedconnectiviteit aan Platform niet. Dit betekent dat als uw Azure-instantie hetzelfde netwerkgebied gebruikt als Platform, een verbinding met bronnen van Platforms niet tot stand kan worden gebracht. Momenteel wordt alleen connectiviteit tussen regio&#39;s ondersteund. Neem contact op met uw Adobe-accountmanager voor meer informatie.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- Directory- en bestandsnamen mogen niet eindigen met een slash (`/`). Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?`.
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Zie [RFC 2616, Section 2.2 voor regels die Unicode-tekenreeksen in HTTP/1.1 besturen: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM4, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (..), en twee stiptekens (.).

## [!DNL Azure File Storage] verbinden met [!DNL Platform]

In de onderstaande documentatie vindt u informatie over hoe u [!DNL Azure File Storage] kunt verbinden met [!DNL Platform] via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een Azure File Storage-bronverbinding maken met de Flow Service API](../../tutorials/api/create/cloud-storage/azure-file-storage.md)
- [Een systeem voor cloudopslag verkennen met de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Gegevens voor cloudopslag verzamelen met de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### De gebruikersinterface gebruiken

- [Een Azure File Storage-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/azure-file-storage.md)
- [Een gegevensstroom configureren voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)