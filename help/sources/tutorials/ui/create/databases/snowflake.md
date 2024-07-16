---
title: Een Snowflake Source Connection maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een Snowflake-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 0%

---

# Een [!DNL Snowflake] bronverbinding maken in de gebruikersinterface

>[!IMPORTANT]
>
>De [!DNL Snowflake] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Snowflake] bronaansluiting met behulp van de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Vereiste referenties verzamelen

U moet waarden opgeven voor de volgende referentie-eigenschappen om de [!DNL Snowflake] -bron te verifiëren.

>[!BEGINTABS]

>[!TAB  de belangrijkste authentificatie van de Rekening ]

| Credentials | Beschrijving |
| ---------- | ----------- |
| Account | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor verschillende [!DNL Snowflake] -organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `orgname-account_name` . Voor meer informatie over rekeningsnamen, lees de [!DNL Snowflake] documentatie over [ rekeningsherkenningstekens ](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Warehouse | Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] -pakhuis is onafhankelijk van elkaar en moet afzonderlijk worden benaderd wanneer u gegevens naar Platform overbrengt. |
| Database | De [!DNL Snowflake] -database bevat de gegevens die u voor het platform wilt gebruiken. |
| Gebruikersnaam | De gebruikersnaam voor de [!DNL Snowflake] -account. |
| Wachtwoord | Het wachtwoord voor de [!DNL Snowflake] -gebruikersaccount. |
| Rol | De standaardtoegangsbeheerrol die in de [!DNL Snowflake] -sessie moet worden gebruikt. De rol zou een bestaande moeten zijn die reeds aan de gespecificeerde gebruiker is toegewezen. De standaardrol is `PUBLIC` . |
| Verbindingstekenreeks | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met de instantie [!DNL Snowflake] . Het patroon van de verbindingstekenreeks voor [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB  zeer belangrijk-paar authentificatie ]

Als u sleutelparverificatie wilt gebruiken, moet u een 2048-bits RSA-sleutelpaar genereren en de volgende waarden opgeven wanneer u een account voor uw [!DNL Snowflake] -bron maakt.

| Credentials | Beschrijving |
| --- | --- |
| Account | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor verschillende [!DNL Snowflake] -organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `orgname-account_name` . Voor meer informatie over rekeningsnamen, lees de [!DNL Snowflake] documentatie over [ rekeningsherkenningstekens ](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Gebruikersnaam | De gebruikersnaam van uw [!DNL Snowflake] -account. |
| Persoonlijke sleutel | De [!DNL Base64-] gecodeerde privé sleutel van uw [!DNL Snowflake] rekening. U kunt gecodeerde of niet-gecodeerde persoonlijke sleutels genereren. Als u een gecodeerde persoonlijke sleutel gebruikt, moet u ook een persoonlijke-sleutelwachtwoord opgeven wanneer u verificatie uitvoert op basis van een Experience Platform. |
| Wachtwoordgroep voor persoonlijke sleutel | Persoonlijke sleutel passphrase is een extra laag van veiligheid die u moet gebruiken wanneer het voor authentiek verklaren met een gecodeerde privé sleutel. U hoeft de wachtwoordzin niet op te geven als u een niet-gecodeerde persoonlijke sleutel gebruikt. |
| Database | De [!DNL Snowflake] -database die de gegevens bevat die u aan het Experience Platform wilt toevoegen. |
| Warehouse | Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] -pakhuis is onafhankelijk van elkaar en moet afzonderlijk worden benaderd wanneer u gegevens naar Platform overbrengt. |

Voor meer informatie over deze waarden, verwijs naar [ dit document van Snowflake ](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

Om tot uw rekening van de Snowflake op Experience Platform toegang te hebben, moet u de volgende authentificatiewaarde verstrekken:

>[!NOTE]
>
>U moet de markering `PREVENT_UNLOAD_TO_INLINE_URL` instellen op `FALSE` om het verwijderen van gegevens uit uw [!DNL Snowflake] -database naar het Experience Platform toe te staan.

## Uw Snowflake-account verbinden

Selecteer in de gebruikersinterface van het platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] .

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Selecteer onder de categorie [!UICONTROL Databases] de optie **[!UICONTROL Snowflake]** en selecteer vervolgens **[!UICONTROL Add data]** .

![ de broncatalogus met [!DNL Snowflake] benadrukte.](../../../../images/tutorials/create/snowflake/catalog.png)

De pagina **[!UICONTROL Connect to Snowflake]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL Snowflake] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![ de bestaande rekeningsinterface in het bronwerkschema.](../../../../images/tutorials/create/snowflake/existing.png)

### Nieuwe account

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam en een optionele beschrijving voor uw nieuwe [!DNL Snowflake] -account.

![ de nieuwe rekeningsinterface in het bronwerkschema.](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB  de belangrijkste authentificatie van de Rekening ]

Als u verificatie met accountsleutels wilt gebruiken, geeft u de verbindingstekenreeks op in het invoerformulier en selecteert u vervolgens **[!UICONTROL Connect to source]** .

![ de interface van de rekeningszeer belangrijke authentificatie.](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB  zeer belangrijk-paar authentificatie ]

Als u sleutelpaarverificatie wilt gebruiken, geeft u waarden op voor uw account, gebruikersnaam, persoonlijke sleutel, persoonlijke sleutelwachtwoord, database en entrepot en selecteert u vervolgens **[!UICONTROL Connect to source]** .

![ de rekening zeer belangrijk-paar authentificatieinterface.](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw account voor Snowflaken tot stand gebracht. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in  [!DNL Platform]](../../dataflow/databases.md) te brengen.
