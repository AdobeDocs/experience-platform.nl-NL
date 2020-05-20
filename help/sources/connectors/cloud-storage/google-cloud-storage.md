---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Google Cloud Storage-connector
topic: overview
translation-type: tm+mt
source-git-commit: 256a193e56e69078d1c01c622656f0b1a18e73ff
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# Google Cloud Storage-connector

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, Google Cloud Platform en Azure. U kunt uw gegevens van deze systemen overbrengen naar Platform.

Met bronnen voor cloudopslag kunt u uw eigen gegevens overbrengen naar Platform zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema. Met Platform kunt u gegevens van Google Cloud Storage via batches inbrengen.

## Setup vereist voor het verbinden van uw Google Cloud Storage-account

Als u verbinding wilt maken met Platform, moet u eerst interoperabiliteit inschakelen voor uw Google Cloud Storage-account. Als u toegang wilt tot de instelling voor interoperabiliteit, opent u het Google Cloud-platform en selecteert u **[!UICONTROL Instellingen]** in de optie **[!UICONTROL Opslag]** in het navigatievenster.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

De pagina **[!UICONTROL Instellingen]** wordt weergegeven. Hier vindt u informatie over uw Google-project-id en informatie over uw Google Cloud Storage-account. Om tot interoperabiliteitsmontages toegang te hebben, selecteer **[!UICONTROL Interoperabiliteit]** van de hoogste kopbal.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

De pagina **[!UICONTROL Interoperability]** bevat informatie over authentificatie, toegangstoetsen, en het standaardproject verbonden aan uw gebruikersrekening. Als u nog geen standaardproject voor interoperabele toegang hebt opgezet, kunt u omhoog van binnen het *[!UICONTROL Standaardproject voor interoperabele toegangssectie]* opstelling. Als reeds een standaardproject is gevestigd, zal de sectie een bevestiging tonen dat een project als gebrek is geplaatst.

Selecteer **[!UICONTROL Een sleutel]** maken om een nieuwe toegangs-id en een geheime toegangssleutel voor uw gebruikersaccount te genereren.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

U kunt uw onlangs gegenereerde toegangs-id en geheime toegangssleutel gebruiken om uw Google Cloud Storage-account aan te sluiten op Platform.

In de onderstaande documentatie vindt u informatie over hoe u Google Cloud Storage kunt verbinden met Platform via API&#39;s of de gebruikersinterface:

## Google Cloud-opslag verbinden met platform

In de onderstaande documentatie vindt u informatie over hoe u Google Cloud Storage kunt verbinden met Platform via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een Google Cloud Storage-connector maken met de Flow Service API](../../tutorials/api/create/cloud-storage/google.md)
- [Een systeem voor cloudopslag verkennen met de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Gegevens voor cloudopslag verzamelen met de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### De gebruikersinterface gebruiken

- [Een Google Cloud Storage-bronconnector maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Een gegevensstroom configureren voor een aansluiting voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)