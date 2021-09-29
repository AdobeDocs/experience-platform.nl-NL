---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Bron gegevenslandingszone
topic-legacy: overview
description: Leer hoe u Data Landing Zone kunt verbinden met Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ca7197036283ee15dbf60c113d361a5ea34d65c1
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] is een  [!DNL Azure Blob] opslaginterface die door Adobe Experience Platform is ingericht en waarmee u toegang krijgt tot een veilige, op de cloud gebaseerde opslagvoorziening voor het opnemen en egress van bestanden in en uit Platform via bronnen en doelen. U hebt toegang tot één [!DNL Data Landing Zone] container per zandbak, en het totale gegevensvolume over alle containers is beperkt tot de totale gegevens die van uw Platform worden voorzien Produces en de vergunning van de Diensten. Alle klanten van Platform en zijn toepassingsdiensten zoals [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], en [!DNL Real-time Customer Data Platform] zijn provisioned met één [!DNL Data Landing Zone] container per zandbak. U kunt bestanden lezen en schrijven naar uw container via [!DNL Azure Storage Explorer] of uw opdrachtregelinterface.

[!DNL Data Landing Zone] biedt ondersteuning voor verificatie op basis van SAS en de bijbehorende gegevens zijn beveiligd met standaard  [!DNL Azure Blob] opslagbeveiligingsmechanismen in rust en in doorvoer. Met SAS-verificatie hebt u via een openbare internetverbinding veilig toegang tot uw [!DNL Data Landing Zone]-container. Er zijn geen netwerkveranderingen vereist voor u om tot uw [!DNL Data Landing Zone] container toegang te hebben, wat betekent u geen lijsten van gewenste personen of dwars-regio montages voor uw netwerk hoeft te vormen. Platform dwingt strikte tijd-aan-levende (TTL) zeven dagen op alle dossiers af die aan een [!DNL Data Landing Zone] container worden geupload. Alle bestanden worden na zeven dagen verwijderd.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden bij het benoemen van bestanden of mappen voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- Directory- en bestandsnamen mogen niet eindigen met een slash (`/`). Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?`.
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (zoals `0x00` tot `0x1F`, `\u0081` enzovoort), ook niet toegestaan. Zie [RFC 2616, Section 2.2 voor regels die Unicode-tekenreeksen in HTTP/1.1 besturen: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM4, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (..), en twee stiptekens (.).

## [!DNL Data Landing Zone] verbinden met [!DNL Platform]

In de onderstaande documentatie vindt u informatie over het overbrengen van gegevens van uw [!DNL Data Landing Zone]-container naar Adobe Experience Platform met behulp van API&#39;s of de gebruikersinterface.

### API&#39;s gebruiken

- [Een [!DNL Data Landing Zone] bronverbinding maken met de Flow Service API](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Een gegevensstroom maken voor een cloudopslagbron met behulp van de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### De gebruikersinterface gebruiken

- [Verbind [!DNL Data Landing Zone] met Platform gebruikend UI](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Een gegevensstroom maken voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
