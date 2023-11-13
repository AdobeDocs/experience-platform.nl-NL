---
title: Creeer een Verbinding van de Bron van de Snowflake in UI
type: Tutorial
description: Leer hoe u een Snowflake-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 669b47753a9c9400f22aa81d08a4d25bb5e414c5
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 2%

---

# Een [!DNL Snowflake] bronverbinding in de gebruikersinterface

>[!IMPORTANT]
>
>De [!DNL Snowflake] De bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Snowflake] bronaansluiting die de Adobe Experience Platform-gebruikersinterface gebruikt.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende componenten van Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Vereiste referenties verzamelen

Voor toegang tot uw account voor Snowflaken op [!DNL Platform]moet u de volgende verificatiewaarde opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Account | De volledige accountnaam die aan uw [!DNL Snowflake] account. Volledig gekwalificeerd [!DNL Snowflake] de naam van uw account bevat uw accountnaam, regio en cloudplatform. Bijvoorbeeld, `cj12345.east-us-2.azure`. Raadpleeg deze voor meer informatie over accountnamen [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| Warehouse | De [!DNL Snowflake] Het pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] Het pakhuis is onafhankelijk van elkaar en moet individueel worden betreden wanneer het brengen van gegevens naar Platform. |
| Database | De [!DNL Snowflake] Het gegevensbestand bevat de gegevens u het Platform wilt brengen. |
| Gebruikersnaam | De gebruikersnaam voor de [!DNL Snowflake] account. |
| Wachtwoord | Het wachtwoord voor de [!DNL Snowflake] gebruikersaccount. |
| Rol | De standaardtoegangsbeheerrol die in de [!DNL Snowflake] sessie. De rol zou een bestaande moeten zijn die reeds aan de gespecificeerde gebruiker is toegewezen. De standaardrol is `PUBLIC`. |
| Verbindingstekenreeks | De verbindingstekenreeks waarmee u verbinding maakt met uw [!DNL Snowflake] -instantie. Het patroon van de verbindingstekenreeks voor [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

Zie voor meer informatie over deze waarden [dit Snowflake-document](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!NOTE]
>
>U moet de instelling `PREVENT_UNLOAD_TO_INLINE_URL` markeren naar `FALSE` om gegevens uit uw [!DNL Snowflake] database naar Experience Platform.

## Uw Snowflake-account verbinden

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder de [!UICONTROL Databases] categorie, selecteert u **[!UICONTROL Snowflake]** en selecteer vervolgens **[!UICONTROL Add data]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

De **[!UICONTROL Connect to Snowflake]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de Snowflake-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om verder te gaan.

![](../../../../images/tutorials/create/snowflake/existing.png)

### Nieuwe account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New account]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en de gegevens van de Snowflake op. Selecteer **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![](../../../../images/tutorials/create/snowflake/new.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw account voor Snowflaken tot stand gebracht. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar [!DNL Platform]](../../dataflow/databases.md).
