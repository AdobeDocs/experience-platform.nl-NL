---
keywords: Experience Platform;home;populaire onderwerpen;Azure File Storage;Azure File Storage-connector
solution: Experience Platform
title: Een Azure File Storage Source Connection maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een Azure File Storage-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 25d483b6-3975-4e80-9dbe-28b7b91cb063
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# Een [!DNL Azure File Storage] bronverbinding maken in de gebruikersinterface

Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het verifiëren van een [!DNL Azure File Storage] bronconnector met behulp van de gebruikersinterface van [!DNL Platform] .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   - [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Azure File Storage] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Als u de [!DNL Azure File Storage] bronconnector wilt verifiëren, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het eindpunt van de instantie [!DNL Azure File Storage] waartoe u toegang hebt. |
| `userId` | De gebruiker met voldoende toegang tot het [!DNL Azure File Storage] eindpunt. |
| `password` | De toegangssleutel van [!DNL Azure File Storage]. |

Voor meer informatie over begonnen worden verwijs naar [ dit  [!DNL Azure File Storage]  document ](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

## Sluit uw [!DNL Azure File Storage] -account aan

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL Azure File Storage] -account te koppelen aan [!DNL Platform] .

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Databases]** de optie **[!UICONTROL Azure File Storage]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe [!DNL Azure File Storage] -connector te maken.

![ catalogus ](../../../../images/tutorials/create/azure-file-storage/catalog.png)

De pagina **[!UICONTROL Connect to Azure File Storage]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Azure File Storage] -gegevens op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ verbind ](../../../../images/tutorials/create/azure-file-storage/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Azure File Storage] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![ bestaand ](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Azure File Storage] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens van uw wolkenopslag in  [!DNL Platform]](../../dataflow/batch/cloud-storage.md) te brengen.
