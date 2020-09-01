---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Google Cloud Storage-connector
topic: overview
translation-type: tm+mt
source-git-commit: 1bb896f7629d7b71b94dd107eeda87701df99208
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Google Cloud Storage-connector

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform]en [!DNL Azure], zodat u gegevens van deze systemen kunt overbrengen.

Met bronnen voor cloudopslag kunt u uw eigen gegevens overbrengen [!DNL Platform] zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema. [!DNL Platform] kunt u gegevens uit batches [!DNL Google Cloud Storage] importeren.

## IP adres lijst van gewenste personen

De volgende IP adressen moeten aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen.

### Oost-Amerikaanse regio

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### West-Europa

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australië - oost

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

## Setup vereist voor verbinding met uw [!DNL Google Cloud Storage] account

Als u verbinding wilt maken met [!DNL Platform], moet u eerst interoperabiliteit voor uw [!DNL Google Cloud Storage] account inschakelen. Als u toegang wilt krijgen tot de instelling voor interoperabiliteit, opent u [!DNL Google Cloud Platform] en selecteert u **[!UICONTROL Instellingen]** in de optie **[!UICONTROL Opslag]** in het navigatievenster.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

De pagina **[!UICONTROL Instellingen]** wordt weergegeven. Hier kunt u informatie over uw [!DNL Google] project-id en gegevens over uw [!DNL Google Cloud Storage] account bekijken. Om tot interoperabiliteitsmontages toegang te hebben, selecteer **[!UICONTROL Interoperabiliteit]** van de hoogste kopbal.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

De pagina **[!UICONTROL Interoperability]** bevat informatie over authentificatie, toegangstoetsen, en het standaardproject verbonden aan uw gebruikersrekening. Als u nog geen standaardproject voor interoperabele toegang hebt opgezet, kunt u omhoog van binnen het **[!UICONTROL Standaardproject voor interoperabele toegangssectie]** opstelling. Als reeds een standaardproject is gevestigd, zal de sectie een bevestiging tonen dat een project als gebrek is geplaatst.

Selecteer **[!UICONTROL Een sleutel]** maken om een nieuwe toegangs-id en een geheime toegangssleutel voor uw gebruikersaccount te genereren.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

U kunt uw onlangs gegenereerde toegangs sleutel-id en geheime toegangssleutel gebruiken om uw [!DNL Google Cloud Storage] account aan te sluiten op [!DNL Platform].

## Verbinden [!DNL Google Cloud Storage] met [!DNL Platform]

In de onderstaande documentatie vindt u informatie over het maken van een verbinding [!DNL Google Cloud Storage] [!DNL Platform] met API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een Google Cloud Storage-connector maken met de Flow Service API](../../tutorials/api/create/cloud-storage/google.md)
- [Een systeem voor cloudopslag verkennen met de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Gegevens voor cloudopslag verzamelen met de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### De gebruikersinterface gebruiken

- [Een Google Cloud Storage-bronconnector maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Een gegevensstroom configureren voor een aansluiting voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)