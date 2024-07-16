---
keywords: Experience Platform;home;populaire onderwerpen;Oracle Object Storage;oracle object storage
solution: Experience Platform
title: Een Oracle Object Storage Source Connection maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een Oracle Object Storage-bronverbinding maakt met de Adobe Experience Platform-interface.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Een [!DNL Oracle Object Storage] Source-verbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Oracle Object Storage] -bronverbinding met de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Vereiste referenties verzamelen

Als u verbinding wilt maken met [!DNL Oracle Object Storage] , moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `serviceUrl` | Het [!DNL Oracle Object Storage] eindpunt dat voor authentificatie wordt vereist. De eindpuntnotatie is: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | De toegangssleutel-id van [!DNL Oracle Object Storage] die is vereist voor verificatie. |
| `secretKey` | Het [!DNL Oracle Object Storage] -wachtwoord dat is vereist voor verificatie. |
| `bucketName` | De toegestane emmernaam wordt vereist als de gebruiker toegang beperkt heeft. De naam van het emmertje moet tussen drie en 63 lange karakters zijn, moet beginnen en met of een brief of een aantal beëindigen, en kan kleine letters, aantallen, of koppeltekens slechts bevatten (`-`). De emmernaam kan niet als IP adres worden geformatteerd. |
| `folderPath` | Het toegestane mappad dat is vereist als de gebruiker de toegang heeft beperkt. |

Voor meer informatie over hoe te om deze waarden te verkrijgen, verwijs naar de [ de authentificatiegids van de Opslag van de Objecten van het Oracle ](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de hieronder stappen volgen om een nieuwe rekening van de Opslag van de Objecten van het Oracle tot stand te brengen om met Platform te verbinden.

## Verbinding maken met Oracle Object Storage

Selecteer in de gebruikersinterface van het platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Selecteer onder de categorie [!UICONTROL Cloud storage] de optie **[!UICONTROL Oracle Object Storage]** en selecteer vervolgens **[!UICONTROL Add data]** .

![ catalogus ](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL Oracle Object Storage] -account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u vervolgens **[!UICONTROL Next]** om door te gaan.

![ bestaand ](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u vervolgens een naam, een optionele beschrijving en uw [!DNL Oracle Object Storage] -referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ nieuw ](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Oracle Object Storage] -account. U kunt nu aan het volgende leerprogramma op [ nu te werk gaan vormend een dataflow om gegevens van uw wolkenopslag in Platform ](../../dataflow/batch/cloud-storage.md) te brengen.
