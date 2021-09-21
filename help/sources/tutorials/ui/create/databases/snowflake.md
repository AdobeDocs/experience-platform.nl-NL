---
keywords: Experience Platform;thuis;populaire onderwerpen;Snowflake
title: Een Snowflake-bronverbinding maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Snowflake-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
source-git-commit: 2e717f33b487430220bd3bb7812558cde81d8852
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 1%

---

# Een [!DNL Snowflake]-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
> De [!DNL Snowflake] schakelaar is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Snowflake]-bronconnector met behulp van de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Platform:

* [Bronnen](../../../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw Snowflake-account op [!DNL Platform], moet u de volgende verificatiewaarde opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Account | De [!DNL Snowflake]-account die u wilt verbinden met Platform. |
| Warehouse | Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] pakhuis is onafhankelijk van elkaar en moet individueel worden betreden wanneer het brengen van gegevens over aan Platform. |
| Database | De [!DNL Snowflake] bevat de gegevens die u het Platform wilt brengen. |
| Gebruikersnaam | De gebruikersnaam voor de [!DNL Snowflake]-account. |
| Wachtwoord | Het wachtwoord voor de [!DNL Snowflake] gebruikersaccount. |
| Verbindingstekenreeks | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met uw [!DNL Snowflake]-instantie. Het patroon van de verbindingstekenreeks voor [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

Raadpleeg [dit Snowflake-document](https://docs.snowflake.com/en/user-guide/oauth-custom.html) voor meer informatie over deze waarden.

## Uw Snowflake-account verbinden

Selecteer **[!UICONTROL Sources]** in de gebruikersinterface van het Platform in de linkernavigatie om de werkruimte [!UICONTROL Sources] te openen. In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Selecteer [!UICONTROL Databases] onder de categorie **[!UICONTROL Snowflake]** en selecteer **[!UICONTROL Add data]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

De pagina **[!UICONTROL Connect to Snowflake]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de Snowflake-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, uitgezocht **[!UICONTROL New account]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw Snowflake-referenties op. Wanneer gebeëindigd, selecteer **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding toe om te vestigen.

![](../../../../images/tutorials/create/snowflake/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw Snowflake-account. U kunt nu doorgaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar [!DNL Platform]](../../dataflow/databases.md).
