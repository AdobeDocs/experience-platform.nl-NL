---
title: Creeer een Verbinding van de Bron van de Analyse van de Azure synapse in UI
description: Leer hoe u een Azure synapse Analytics-bronverbinding (hierna "Synapse" genoemd) maakt met behulp van de Adobe Experience Platform-gebruikersinterface.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 1f1ce317-eaaf-4ad2-a5fb-236983220bd7
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 1%

---

# Een [!DNL Azure Synapse Analytics] bronverbinding in de gebruikersinterface

>[!IMPORTANT]
>
>De [!DNL Azure Synapse Analytics] De bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Azure Synapse Analytics] (hierna &quot;[!DNL Synapse]&quot;) bronaansluiting met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Synapse] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Om toegang te krijgen tot uw [!DNL Synapse] account op [!DNL Platform]moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die aan uw [!DNL Synapse] verificatie. De [!DNL Synapse] verbindingstekenpatroon is `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |

Voor meer informatie over deze waarde raadpleegt u [dit [!DNL Synapse] document](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-sql-data-warehouse).

## Verbind uw [!DNL Synapse] account

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Synapse] account aan [!DNL Platform].

Aanmelden bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de **[!UICONTROL Sources]** werkruimte. De **[!UICONTROL Catalog]** in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de **[!UICONTROL Databases]** categorie, selecteert u **[!UICONTROL Azure Synapse Analytics]**. Als dit de eerste keer is met deze connector, selecteert u **[!UICONTROL Configure]**. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe [!DNL Synapse] -aansluiting.

![](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

De **[!UICONTROL Connect to Azure Synapse Analytics]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New account]**. Geef op het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Synapse] referenties. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de optie [!DNL Synapse] account waarmee u verbinding wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Synapse] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar [!DNL Platform]](../../dataflow/databases.md).
