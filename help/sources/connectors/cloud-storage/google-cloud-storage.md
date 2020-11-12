---
keywords: Experience Platform;home;popular topics;Google Cloud Storage;google cloud storage
solution: Experience Platform
title: Google Cloud Storage-connector
topic: overview
description: In de onderstaande documentatie vindt u informatie over hoe u Google Cloud Storage met Platform kunt verbinden via API's of de gebruikersinterface.
translation-type: tm+mt
source-git-commit: e0a0b7fc28b8cc85c5140d3840e06e5c7078c307
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# Google Cloud Storage-connector

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform]en [!DNL Azure], zodat u gegevens van deze systemen kunt overbrengen.

Met bronnen voor cloudopslag kunt u uw eigen gegevens overbrengen [!DNL Platform] zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema. [!DNL Platform] kunt u gegevens uit batches [!DNL Google Cloud Storage] importeren.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP pagina van de lijst van gewenste personen](../../ip-address-allow-list.md) van het adres voor meer informatie.

## Setup vereist voor verbinding met uw [!DNL Google Cloud Storage] account

Als u verbinding wilt maken met [!DNL Platform], moet u eerst interoperabiliteit voor uw [!DNL Google Cloud Storage] account inschakelen. Als u toegang wilt krijgen tot de instelling voor interoperabiliteit, opent u [!DNL Google Cloud Platform] en selecteert u **[!UICONTROL Instellingen]** in de optie **[!UICONTROL Opslag]** in het navigatievenster.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

De pagina **[!UICONTROL Instellingen]** wordt weergegeven. Hier kunt u informatie over uw [!DNL Google] project-id en gegevens over uw [!DNL Google Cloud Storage] account bekijken. Om tot interoperabiliteitsmontages toegang te hebben, selecteer **[!UICONTROL Interoperabiliteit]** van de hoogste kopbal.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

De pagina **[!UICONTROL Interoperability]** bevat informatie over authentificatie, toegangstoetsen, en het standaardproject verbonden aan uw gebruikersrekening. Als u nog geen standaardproject voor interoperabele toegang hebt opgezet, kunt u omhoog van binnen het **[!UICONTROL Standaardproject voor interoperabele toegangssectie]** opstelling. Als reeds een standaardproject is gevestigd, zal de sectie een bevestiging tonen dat een project als gebrek is geplaatst.

Selecteer **[!UICONTROL Een sleutel]** maken om een nieuwe toegangs-id en een geheime toegangssleutel voor uw gebruikersaccount te genereren.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

U kunt uw onlangs gegenereerde toegangs sleutel-id en geheime toegangssleutel gebruiken om uw [!DNL Google Cloud Storage] account aan te sluiten op [!DNL Platform].

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- Directory- en bestandsnamen mogen niet eindigen met een slash (`/`). Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?`.
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000`, zijn weliswaar geldig in NTFS-bestandsnamen, maar zijn geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Zie [RFC 2616, Section 2.2 voor regels die Unicode-tekenreeksen in HTTP/1.1 bepalen: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM4, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (..), en twee stiptekens (.).

## Verbinden [!DNL Google Cloud Storage] met [!DNL Platform]

In de onderstaande documentatie vindt u informatie over het maken van een verbinding [!DNL Google Cloud Storage] [!DNL Platform] met API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een Google Cloud Storage-connector maken met de Flow Service API](../../tutorials/api/create/cloud-storage/google.md)
- [Een systeem voor cloudopslag verkennen met de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Gegevens voor cloudopslag verzamelen met de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### De gebruikersinterface gebruiken

- [Een Google Cloud Storage-bronconnector maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Een gegevensstroom configureren voor een aansluiting voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)