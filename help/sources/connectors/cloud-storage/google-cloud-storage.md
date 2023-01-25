---
keywords: Experience Platform;home;populaire onderwerpen;Google Cloud Storage;Google Cloud-opslag
solution: Experience Platform
title: Overzicht van Google Cloud Storage Source Connector
description: Leer hoe u Google Cloud Storage met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: ae22e423119bf378a068349d481f0717a75171bb
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# Google Cloud Storage-connector

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform], en [!DNL Azure], zodat u uw gegevens van deze systemen kunt overbrengen.

Met bronnen voor cloudopslag kunt u uw eigen gegevens in het Platform plaatsen zonder dat u deze hoeft te downloaden, opmaken of uploaden. De opgenomen gegevens kunnen als JSON of Parquet worden geformatteerd die met het Model van de Gegevens van de Ervaring (XDM), of in een afgebakend formaat volgzaam is. Elke stap van het proces is geïntegreerd in de bronwerkstroom. Met Platform kunt u gegevens van [!DNL Google Cloud Storage] door partijen.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Vereiste instellingen voor verbinding met uw [!DNL Google Cloud Storage] account

Om met Platform te verbinden moet u eerst interoperabiliteit voor uw toelaten [!DNL Google Cloud Storage] account. Voor toegang tot de interoperabiliteitsinstelling opent u [!DNL Google Cloud Platform] en selecteert u **[!UICONTROL Settings]** van de **[!UICONTROL Cloud Storage]** in het navigatievenster.

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

De **[!UICONTROL Settings]** wordt weergegeven. Hier kunt u informatie over uw [!DNL Google] project-id en details over uw [!DNL Google Cloud Storage] account. Om tot interoperabiliteitsmontages toegang te hebben, selecteer **[!UICONTROL Interoperability]** in de bovenste koptekst.

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

De **[!UICONTROL Interoperability]** De pagina bevat informatie over authentificatie, toegangstoetsen, en het standaardproject verbonden aan uw de dienstrekening. Als u een nieuwe toegangstoets-id en een geheime toegangssleutel voor uw serviceaccount wilt genereren, selecteert u **[!UICONTROL Create a Key for a Service Account]**.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

U kunt uw onlangs gegenereerde toegangstoets-id en geheime toegangssleutel gebruiken om uw [!DNL Google Cloud Storage] aan Platform.

Lees voor meer informatie de handleiding op [het creëren van en het beheren van de sleutels van de de dienstrekening](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) van de [!DNL Google Cloud] documentatie.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- Directory- en bestandsnamen mogen niet eindigen met een slash (`/`). Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?`.
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000`zijn, hoewel geldig in NTFS-bestandsnamen, geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [RFC 2616, punt 2.2: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM4, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (..), en twee stiptekens (.).

## Verbinden [!DNL Google Cloud Storage] naar Platform

In de onderstaande documentatie vindt u informatie over het maken van een verbinding [!DNL Google Cloud Storage] Platforms met behulp van API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een Google Cloud Storage-basisverbinding maken met de Flow Service API](../../tutorials/api/create/cloud-storage/google.md)
- [De gegevensstructuur en inhoud van een cloudopslagbron verkennen met behulp van de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Een gegevensstroom maken voor een cloudopslagbron met behulp van de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### De gebruikersinterface gebruiken

- [Een Google Cloud Storage-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Een gegevensstroom maken voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
