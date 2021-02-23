---
keywords: Experience Platform;home;populaire onderwerpen;Oracle Object Storage;oracle-objectopslag
solution: Experience Platform
title: Creeer een Verbinding van de Bron van de Opslag van de Objecten van het Oracle in UI
topic: ' - overzicht'
type: Tutorial
description: Leer hoe u een Oracle Object Storage-bronverbinding maakt met de Adobe Experience Platform-interface.
translation-type: tm+mt
source-git-commit: c1453a9f0be42f834d35af871051324df8dadf80
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---


# Een [!DNL Oracle Object Storage]-bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Oracle Object Storage]-bronverbinding met de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Vereiste referenties verzamelen

Als u verbinding wilt maken met [!DNL Oracle Object Storage], moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `serviceUrl` | Het [!DNL Oracle Object Storage] eindpunt dat voor authentificatie wordt vereist. De eindpuntnotatie is: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | De [!DNL Oracle Object Storage] toegangs zeer belangrijke identiteitskaart die voor authentificatie wordt vereist. |
| `secretKey` | Het [!DNL Oracle Object Storage] wachtwoord vereist voor authentificatie. |
| `bucketName` | De toegestane emmernaam wordt vereist als de gebruiker toegang beperkt heeft. De naam van het emmertje moet tussen drie en 63 lange karakters zijn, moet beginnen en met of een brief of een aantal beëindigen, en kan slechts kleine letters, aantallen, of koppeltekens (`-`) bevatten. De emmernaam kan niet als IP adres worden geformatteerd. |
| `folderPath` | Het toegestane mappad dat is vereist als de gebruiker de toegang heeft beperkt. |

Voor meer informatie over hoe te om deze waarden te verkrijgen, verwijs naar [de authentificatiegids van de Opslag van de Objecten van het Oracle](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de hieronder stappen volgen om een nieuwe rekening van de Opslag van de Objecten van het Oracle tot stand te brengen om met Platform te verbinden.

## Verbinding maken met Oracle Object Storage

In het Platform UI, selecteer **[!UICONTROL Bronnen]** van de linkernavigatie om tot de [!UICONTROL Bronswerkruimte] toegang te hebben. In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Selecteer **[!UICONTROL Oracle Object Storage]** onder de categorie [!UICONTROL Cloud storage] en selecteer **[!UICONTROL Gegevens toevoegen]**.

![catalogus](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL Oracle Object Storage]-account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL Nieuwe account]** en geeft u een naam, een optionele beschrijving en uw [!DNL Oracle Object Storage]-referenties op. Wanneer gebeëindigd, selecteer **[!UICONTROL verbind met bron]** en laat dan wat tijd voor de nieuwe verbinding toe om te vestigen.

![new](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Oracle Object Storage]-account. U kunt nu doorgaan naar de volgende zelfstudie over [het configureren van een gegevensstroom om gegevens van uw cloudopslag over te brengen naar Platform](../../dataflow/batch/cloud-storage.md).
