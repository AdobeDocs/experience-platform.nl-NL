---
keywords: Experience Platform;home;populaire onderwerpen;Azure Table Storage;azure table storage;ats;ATS
solution: Experience Platform
title: Een Azure Table Storage Source Connection maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een Azure Table Storage-bronverbinding maakt met de Adobe Experience Platform UI.
exl-id: 045cb954-e3e1-439d-a3cd-170d688dfbc8
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Een [!DNL Azure Table Storage] bronverbinding maken in de gebruikersinterface

Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Azure Table Storage] (hierna &quot;ATS&quot; genoemd) bronconnector via de [!DNL Experience Platform] -gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige verbinding ATS hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw ATS-account op [!DNL Experience Platform] , moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | Een verbindingstekenreeks waarmee verbinding wordt gemaakt met de instantie [!DNL Azure Table Storage] . De verbindingstekenreeks waarmee verbinding moet worden gemaakt met een ATS-instantie. Het patroon van de verbindingstekenreeks voor ATS is `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Voor meer informatie over begonnen worden, verwijs naar [ dit  [!DNL Azure Table Storage]  document ](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## Sluit uw [!DNL Azure Table Storage] -account aan

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw ATS-account te koppelen aan [!DNL Experience Platform] .

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Databases]** de optie **[!UICONTROL Azure Table Storage]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe ATS-connector te maken.

![ catalogus ](../../../../images/tutorials/create/ats/catalog.png)

De pagina **[!UICONTROL Connect to Azure Table Storage]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw ATS-referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ verbind ](../../../../images/tutorials/create/ats/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de ATS-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![ bestaand ](../../../../images/tutorials/create/ats/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw ATS-account tot stand gebracht. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in  [!DNL Experience Platform]](../../dataflow/databases.md) te brengen.
