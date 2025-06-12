---
title: Snowflake verbinden met Experience Platform via de gebruikersinterface
type: Tutorial
description: Leer hoe u een Snowflake-bronverbinding maakt met de interface van Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: d8d9303e358c66c4cd891d6bf59a801c09a95f8e
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 1%

---

# Verbinding maken [!DNL Snowflake] met Experience Platform via de gebruikersinterface

>[!IMPORTANT]
>
>De [!DNL Snowflake] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.

Lees deze handleiding voor informatie over hoe u uw [!DNL Snowflake] -account kunt verbinden met Adobe Experience Platform via de gebruikersinterface.

## Aan de slag

>[!WARNING]
>
>De basisauthentificatie (of de authentificatie van de rekeningssleutel) voor [!DNL Snowflake] bron zal op November 2025 worden afgekeurd. U moet naar op sleutel-paar gebaseerde authentificatie bewegen om de bron te blijven gebruiken en gegevens van uw gegevensbestand in te voeren aan Experience Platform. Voor meer informatie over de veroudering, lees de [[!DNL Snowflake]  beste praktijkgids bij het verlichten van de risico&#39;s van credentieel compromis ](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/).

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

>[!NOTE]
>
>U moet de markering `PREVENT_UNLOAD_TO_INLINE_URL` instellen op `FALSE` om gegevens uit uw [!DNL Snowflake] -database te kunnen verwijderen naar Experience Platform.

## Navigeren door de catalogus met bronnen {#navigate}

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!DNL Snowflake]** onder de categorie *[!UICONTROL Databases]* en selecteer vervolgens **[!UICONTROL Set up]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account bestaat, verandert deze optie in **[!UICONTROL Add data]** .

![ de broncatalogus met de geselecteerde kaart van Snowflake.](../../../../images/tutorials/create/snowflake/catalog.png)

## Een bestaande account gebruiken {#existing}

Vervolgens gaat u naar de verificatiestap van de workflow voor bronnen. Hier kunt u een bestaand account gebruiken of een nieuw account maken.

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL Snowflake] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![ de bestaande rekeningsinterface in het bronwerkschema.](../../../../images/tutorials/create/snowflake/existing.png)

## Een nieuwe account maken {#create}

Als u geen bestaand account hebt, moet u een nieuw account maken door de vereiste verificatiereferenties op te geven die overeenkomen met uw bron.

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam op en voegt u desgewenst een beschrijving voor uw account toe.

### Verbinding maken met Experience Platform on Azure {#azure}

U kunt uw [!DNL Snowflake] -account op Azure verbinden met Experience Platform via accountsleutelverificatie of sleutelpaarverificatie.

>[!BEGINTABS]

>[!TAB  de belangrijkste authentificatie van de Rekening ]

Selecteer **[!UICONTROL Account key authentication]** als u accountsleutelverificatie wilt gebruiken, geef uw verbindingstekenreeks op in het invoerformulier en selecteer vervolgens **[!UICONTROL Connect to source]** .

![ de interface van de rekeningszeer belangrijke authentificatie.](../../../../images/tutorials/create/snowflake/account-key-auth.png)

| Credentials | Beschrijving |
| --- | --- |
| Account | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor verschillende [!DNL Snowflake] -organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `orgname-account_name` . Lees de gids bij [ het terugwinnen van uw  [!DNL Snowflake]  rekeningsherkenningsteken ](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) voor extra begeleiding. Raadpleeg voor meer informatie de [[!DNL Snowflake] documentatie](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Warehouse | Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] -pakhuis is onafhankelijk van elkaar en moet afzonderlijk worden benaderd wanneer u gegevens naar Experience Platform overbrengt. |
| Database | De database [!DNL Snowflake] bevat de gegevens die u aan de Experience Platform wilt toevoegen. |
| Gebruikersnaam | De gebruikersnaam voor de [!DNL Snowflake] -account. |
| Wachtwoord | Het wachtwoord voor de [!DNL Snowflake] -gebruikersaccount. |
| Rol | De standaardtoegangsbeheerrol die in de [!DNL Snowflake] -sessie moet worden gebruikt. De rol zou een bestaande moeten zijn die reeds aan de gespecificeerde gebruiker is toegewezen. De standaardrol is `PUBLIC` . |
| Verbindingstekenreeks | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met de instantie [!DNL Snowflake] . Het patroon van de verbindingstekenreeks voor [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB  zeer belangrijk-paar authentificatie ]

Selecteer **[!UICONTROL KeyPair authentication]** als u sleutelpaarverificatie wilt gebruiken, geef waarden op voor uw account, gebruikersnaam, persoonlijke sleutel, persoonlijke sleutel, wachtwoordzin voor de persoonlijke sleutel, database en magazijn en selecteer vervolgens **[!UICONTROL Connect to source]** .

![ de rekening zeer belangrijk-paar authentificatieinterface.](../../../../images/tutorials/create/snowflake/key-pair-auth.png)

Met zeer belangrijk-paarauthentificatie, moet u een zeer belangrijk paar met 2048 bits RSA produceren en dan de volgende waarden verstrekken wanneer het creëren van een rekening voor uw [!DNL Snowflake] bron.

| Credentials | Beschrijving |
| --- | --- |
| Account | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor verschillende [!DNL Snowflake] -organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `orgname-account_name` . Lees de gids bij [ het terugwinnen van uw  [!DNL Snowflake]  rekeningsherkenningsteken ](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) voor extra begeleiding. Raadpleeg voor meer informatie de [[!DNL Snowflake] documentatie](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| Gebruikersnaam | De gebruikersnaam van uw [!DNL Snowflake] -account. |
| Persoonlijke sleutel | De [!DNL Base64-] gecodeerde privé sleutel van uw [!DNL Snowflake] rekening. U kunt gecodeerde of niet-gecodeerde persoonlijke sleutels genereren. Als u een gecodeerde persoonlijke sleutel gebruikt, moet u ook een persoonlijke-sleutelwachtwoord opgeven bij verificatie met behulp van Experience Platform. Lees de gids op [ het terugwinnen van uw  [!DNL Snowflake]  privé sleutel ](../../../../connectors/databases/snowflake.md) voor meer informatie. |
| Wachtwoordgroep voor persoonlijke sleutel | Persoonlijke sleutel passphrase is een extra laag van veiligheid die u moet gebruiken wanneer het voor authentiek verklaren met een gecodeerde privé sleutel. U hoeft de wachtwoordzin niet op te geven als u een niet-gecodeerde persoonlijke sleutel gebruikt. |
| Database | De [!DNL Snowflake] -database die de gegevens bevat die u aan Experience Platform wilt toevoegen. |
| Warehouse | Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] -pakhuis is onafhankelijk van elkaar en moet afzonderlijk worden benaderd wanneer u gegevens naar Experience Platform overbrengt. |

Voor meer informatie over deze waarden, verwijs naar [ dit document van Snowflake ](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Verbinding maken met Experience Platform op AWS {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](../../../../../landing/multi-cloud.md).

Als u een nieuwe [!DNL Snowflake] -account wilt maken en verbinding wilt maken met Experience Platform op AWS, controleert u of u zich in een VA6-sandbox bevindt en geeft u vervolgens de vereiste gegevens voor verificatie op.

![ de nieuwe rekeningsstap in het bronwerkschema waar u Snowflake met Experience Platform op AWS kunt verbinden.](../../../../images/tutorials/create/snowflake/aws-auth.png)

| Credentials | Beschrijving |
| --- | --- |
| Host | De host-URL waarmee uw [!DNL Snowflake] -account verbinding maakt. |
| Poort | Het poortnummer dat door [!DNL Snowflake] wordt gebruikt wanneer verbinding wordt gemaakt met een server via internet. |
| Gebruikersnaam | De gebruikersnaam die aan uw [!DNL Snowflake] -account is gekoppeld. |
| Wachtwoord | Het wachtwoord dat aan uw [!DNL Snowflake] account is gekoppeld. |
| Database | De [!DNL Snowflake] -database vanwaar de gegevens worden opgehaald. |
| Schema | De naam van het schema dat aan uw [!DNL Snowflake] database is gekoppeld. U moet ervoor zorgen dat de gebruiker u gegevensbestandtoegang tot wilt geven, ook toegang tot dit schema heeft. |
| Warehouse | Het [!DNL Snowflake] -pakhuis dat u gebruikt. |

### Voorvertoning van voorbeeldgegevens overslaan {#skip-preview-of-sample-data}

Tijdens de stap voor gegevensselectie kan er een time-out optreden wanneer u grote tabellen of bestanden met gegevens opgeeft. U kunt gegevensvoorvertoning overslaan om de time-out te omzeilen en toch uw schema weer te geven, zij het zonder voorbeeldgegevens. Als u de gegevensvoorvertoning wilt overslaan, schakelt u de schakeloptie **[!UICONTROL Skip previewing sample data]** in.

De rest van de workflow blijft ongewijzigd. Het enige voorbehoud is dat bij het overslaan van de gegevensvoorvertoning berekende en vereiste velden mogelijk niet automatisch worden gevalideerd tijdens de toewijzingsstap. Vervolgens moet u deze velden handmatig valideren tijdens de toewijzing.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw Snowflake-account tot stand gebracht. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in  [!DNL Experience Platform]](../../dataflow/databases.md) te brengen.
