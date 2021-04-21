---
keywords: Experience Platform;home;populaire onderwerpen;Google Cloud Storage;Google Cloud-opslag
solution: Experience Platform
title: Overzicht van Google Cloud Storage Source Connector
topic-legacy: overview
description: Leer hoe u Google Cloud Storage kunt verbinden met Adobe Experience Platform via API's of de gebruikersinterface.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# Google Cloud Storage-connector

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform] en [!DNL Azure], zodat u uw gegevens van deze systemen kunt overbrengen.

Met bronnen voor cloudopslag kunt u uw eigen gegevens in het Platform plaatsen zonder dat u deze hoeft te downloaden, opmaken of uploaden. De opgenomen gegevens kunnen als JSON of Parquet worden geformatteerd die met het Model van de Gegevens van de Ervaring (XDM), of in een afgebakend formaat volgzaam is. Elke stap van het proces is geïntegreerd in de bronwerkstroom. Met Platform kunt u gegevens uit [!DNL Google Cloud Storage] tot batches invoegen.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) pagina voor meer informatie.

## Vereiste instellingen voor het aansluiten van uw [!DNL Google Cloud Storage]-account

Als u verbinding wilt maken met Platform, moet u eerst interoperabiliteit inschakelen voor uw [!DNL Google Cloud Storage]-account. Als u toegang wilt krijgen tot de interoperabiliteitsinstelling, opent u [!DNL Google Cloud Platform] en selecteert u **[!UICONTROL Settings]** in de optie **[!UICONTROL Cloud Storage]** in het navigatievenster.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

De pagina **[!UICONTROL Settings]** wordt weergegeven. Van hier, kunt u informatie betreffende uw [!DNL Google] project identiteitskaart en details over uw [!DNL Google Cloud Storage] rekening zien. Om tot interoperabiliteitsmontages toegang te hebben, selecteer **[!UICONTROL Interoperability]** van de hoogste kopbal.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

De pagina **[!UICONTROL Interoperability]** bevat informatie over verificatie, toegangstoetsen en het standaardproject dat aan uw serviceaccount is gekoppeld. Selecteer **[!UICONTROL Create a Key for a Service Account]** om een nieuwe toegangs sleutel-id en een geheime toegangstoets voor uw serviceaccount te genereren.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

U kunt uw onlangs geproduceerde toegangs belangrijkste identiteitskaart en geheime toegangssleutel gebruiken om uw [!DNL Google Cloud Storage] rekening met Platform aan te sluiten.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- Directory- en bestandsnamen mogen niet eindigen met een slash (`/`). Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?`.
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Zie [RFC 2616, Section 2.2 voor regels die Unicode-tekenreeksen in HTTP/1.1 besturen: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM4, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (..), en twee stiptekens (.).

## [!DNL Google Cloud Storage] verbinden met Platform

De onderstaande documentatie biedt informatie over hoe u [!DNL Google Cloud Storage] kunt verbinden met een Platform via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een Google Cloud Storage-bronverbinding maken met de Flow Service API](../../tutorials/api/create/cloud-storage/google.md)
- [Een systeem voor cloudopslag verkennen met de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Gegevens voor cloudopslag verzamelen met de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### De gebruikersinterface gebruiken

- [Een Google Cloud Storage-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Een gegevensstroom configureren voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
