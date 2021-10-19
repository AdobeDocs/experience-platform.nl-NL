---
keywords: Experience Platform;thuis;populaire onderwerpen;Snowflake
title: Een Snowflake-bronverbinding maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Snowflake-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 76b3e3e9bcb27eb2bd6981ae6eb109410ae16336
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Een [!DNL Snowflake] bronverbinding in de gebruikersinterface

>[!NOTE]
>
> De [!DNL Snowflake] -connector bevindt zich in bèta. Zie de [Overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Snowflake] bronaansluiting die gebruikmaakt van de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Vereiste referenties verzamelen

Om toegang te krijgen tot uw Snowflake-account op [!DNL Platform]moet u de volgende verificatiewaarde opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Account | De volledige accountnaam die aan uw [!DNL Snowflake] account. Een volledig gekwalificeerde [!DNL Snowflake] de naam van uw account bevat uw accountnaam, regio en cloudplatform. Bijvoorbeeld, `cj12345.east-us-2.azure`. Raadpleeg deze voor meer informatie over accountnamen [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| Warehouse | De [!DNL Snowflake] Het pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] magazijn is onafhankelijk van elkaar en moet individueel worden benaderd wanneer gegevens naar het Platform worden overgebracht. |
| Database | De [!DNL Snowflake] de database bevat de gegevens die u het Platform wilt brengen. |
| Gebruikersnaam | De gebruikersnaam voor de [!DNL Snowflake] account. |
| Wachtwoord | Het wachtwoord voor de [!DNL Snowflake] gebruikersaccount. |
| Verbindingstekenreeks | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met uw [!DNL Snowflake] -instantie. Het patroon van de verbindingstekenreeks voor [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

Zie voor meer informatie over deze waarden [dit Snowflake-document](https://docs.snowflake.com/en/user-guide/oauth-custom.html).

## Uw Snowflake-account verbinden

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder de [!UICONTROL Databases] categorie, selecteert u **[!UICONTROL Snowflake]** en selecteer vervolgens **[!UICONTROL Add data]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

De **[!UICONTROL Connect to Snowflake]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de Snowflake-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om verder te gaan.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Nieuwe account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New account]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw Snowflake-referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![](../../../../images/tutorials/create/snowflake/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw Snowflake-account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar [!DNL Platform]](../../dataflow/databases.md).
