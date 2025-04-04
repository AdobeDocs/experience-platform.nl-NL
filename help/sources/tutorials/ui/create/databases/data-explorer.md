---
keywords: Experience Platform;home;populaire onderwerpen;Azure Data Explorer;azure data explorer;data explorer;Data Explorer
solution: Experience Platform
title: Een Azure Data Explorer Source Connection maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een Azure Data Explorer-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: 561bf948-fc92-4401-8631-e2a408667507
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Een [!DNL Azure Data Explorer] bronverbinding maken in de gebruikersinterface

Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Azure Data Explorer] (hierna &quot;[!DNL Data Explorer]&quot; genoemd) bronconnector met behulp van de [!DNL Experience Platform] -gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Data Explorer] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL Data Explorer] account op [!DNL Experience Platform] , moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `endpoint` | Het eindpunt van de [!DNL Data Explorer] server. |
| `database` | De naam van de [!DNL Data Explorer] -database. |
| `tenant` | De unieke huurder-id die wordt gebruikt om verbinding te maken met de [!DNL Data Explorer] -database. |
| `servicePrincipalId` | De unieke service principal-id die wordt gebruikt om verbinding te maken met de [!DNL Data Explorer] -database. |
| `servicePrincipalKey` | De unieke service principal-sleutel die wordt gebruikt om verbinding te maken met de [!DNL Data Explorer] -database. |

Voor meer informatie over begonnen worden, verwijs naar [ dit  [!DNL Data Explorer]  document ](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

## Sluit uw [!DNL Azure Data Explorer] -account aan

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL Data Explorer] -account te koppelen aan [!DNL Experience Platform] .

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarvoor u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Databases]** de optie **[!UICONTROL Azure Data Explorer]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe Data Explorer-connector te maken.

![ catalogus ](../../../../images/tutorials/create/data-explorer/catalog.png)

De pagina **[!UICONTROL Connect to Azure Data Explorer]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Data Explorer] -gegevens op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ verbind ](../../../../images/tutorials/create/data-explorer/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Data Explorer] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![ bestaand ](../../../../images/tutorials/create/data-explorer/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Data Explorer] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in  [!DNL Experience Platform]](../../dataflow/databases.md) te brengen.
