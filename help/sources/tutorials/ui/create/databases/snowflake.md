---
title: Creeer een Verbinding van de Bron van de Snowflake in UI
type: Tutorial
description: Leer hoe u een Snowflake-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 1%

---

# Een [!DNL Snowflake] bronverbinding in de gebruikersinterface

>[!IMPORTANT]
>
>De [!DNL Snowflake] De bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Snowflake] bronaansluiting die de Adobe Experience Platform-gebruikersinterface gebruikt.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Vereiste referenties verzamelen

U moet waarden opgeven voor de volgende referentie-eigenschappen om uw [!DNL Snowflake] bron.

>[!BEGINTABS]

>[!TAB Verificatie met accountsleutel]

| Credentials | Beschrijving |
| ---------- | ----------- |
| Account | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor een ander account [!DNL Snowflake] organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `orgname-account_name`. Voor meer informatie over accountnamen leest u de [!DNL Snowflake] documentatie over [account-id&#39;s](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Warehouse | De [!DNL Snowflake] Het pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] Het pakhuis is onafhankelijk van elkaar en moet individueel worden betreden wanneer het brengen van gegevens naar Platform. |
| Database | De [!DNL Snowflake] Het gegevensbestand bevat de gegevens u het Platform wilt brengen. |
| Gebruikersnaam | De gebruikersnaam voor de [!DNL Snowflake] account. |
| Wachtwoord | Het wachtwoord voor de [!DNL Snowflake] gebruikersaccount. |
| Rol | De standaardtoegangsbeheerrol die in de [!DNL Snowflake] sessie. De rol zou een bestaande moeten zijn die reeds aan de gespecificeerde gebruiker is toegewezen. De standaardrol is `PUBLIC`. |
| Verbindingstekenreeks | De verbindingstekenreeks waarmee u verbinding maakt met uw [!DNL Snowflake] -instantie. Het patroon van de verbindingstekenreeks voor [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Verificatie sleutelpaar]

Om zeer belangrijk-paarauthentificatie te gebruiken, moet u een zeer belangrijk paar met 2048 bits RSA produceren en dan de volgende waarden verstrekken wanneer het creëren van een rekening voor uw [!DNL Snowflake] bron.

| Credentials | Beschrijving |
| --- | --- |
| Account | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor een ander account [!DNL Snowflake] organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `orgname-account_name`. Voor meer informatie over accountnamen leest u de [!DNL Snowflake] documentatie over [account-id&#39;s](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Gebruikersnaam | De gebruikersnaam van uw [!DNL Snowflake] account. |
| Persoonlijke sleutel | De [!DNL Base64-]gecodeerde persoonlijke sleutel van uw [!DNL Snowflake] account. U kunt gecodeerde of niet-gecodeerde persoonlijke sleutels genereren. Als u een gecodeerde persoonlijke sleutel gebruikt, moet u ook een persoonlijke-sleutelwachtwoord opgeven wanneer u verificatie uitvoert op basis van een Experience Platform. |
| Wachtwoordgroep voor persoonlijke sleutel | Persoonlijke sleutel passphrase is een extra laag van veiligheid die u moet gebruiken wanneer het voor authentiek verklaren met een gecodeerde privé sleutel. U hoeft de wachtwoordzin niet op te geven als u een niet-gecodeerde persoonlijke sleutel gebruikt. |
| Database | De [!DNL Snowflake] database die de gegevens bevat die u aan het Experience Platform wilt toevoegen. |
| Warehouse | De [!DNL Snowflake] Het pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] Het pakhuis is onafhankelijk van elkaar en moet individueel worden betreden wanneer het brengen van gegevens naar Platform. |

Zie voor meer informatie over deze waarden [dit Snowflake-document](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

Om tot uw rekening van de Snowflake op Experience Platform toegang te hebben, moet u de volgende authentificatiewaarde verstrekken:

>[!NOTE]
>
>U moet de instelling `PREVENT_UNLOAD_TO_INLINE_URL` markeren naar `FALSE` om gegevens uit uw [!DNL Snowflake] database naar Experience Platform.

## Uw Snowflake-account verbinden

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder de [!UICONTROL Databases] categorie, selecteert u **[!UICONTROL Snowflake]** en selecteer vervolgens **[!UICONTROL Add data]**.

![De catalogus met bronnen [!DNL Snowflake] gemarkeerd.](../../../../images/tutorials/create/snowflake/catalog.png)

De **[!UICONTROL Connect to Snowflake]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de optie [!DNL Snowflake] account waarmee u verbinding wilt maken en selecteer **[!UICONTROL Next]** om verder te gaan.

![De bestaande accountinterface in de workflow voor bronnen.](../../../../images/tutorials/create/snowflake/existing.png)

### Nieuwe account

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam en een optionele beschrijving voor uw nieuwe [!DNL Snowflake] account.

![De nieuwe accountinterface in de workflow voor bronnen.](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB Verificatie met accountsleutel]

Als u verificatie met accountsleutels wilt gebruiken, geeft u de verbindingstekenreeks op in het invoerformulier en selecteert u vervolgens **[!UICONTROL Connect to source]**.

![De verificatieinterface van de accountsleutel.](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB Verificatie sleutelpaar]

Om zeer belangrijk-paarauthentificatie te gebruiken, verstrek waarden voor uw rekening, gebruikersbenaming, privé sleutel, privé zeer belangrijke passphrase, gegevensbestand, en pakhuis, dan uitgezocht **[!UICONTROL Connect to source]**.

![De account key-pair authenticatie interface.](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw account voor Snowflaken tot stand gebracht. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar [!DNL Platform]](../../dataflow/databases.md).
