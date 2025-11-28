---
title: Overzicht Snowflake Source Connector
description: Leer hoe u Snowflake met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 687363ab664e43cc854b535760dfbfc55acefd2c
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 2%

---

# [!DNL Snowflake] bron

>[!IMPORTANT]
>
>* De [!DNL Snowflake] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.
>* Standaard wordt [!DNL Snowflake] source `null` geïnterpreteerd als een lege tekenreeks. Neem contact op met uw Adobe-vertegenwoordiger om ervoor te zorgen dat de `null` -waarden correct worden geschreven zoals `null` in Adobe Experience Platform.
>* Experience Platform kan alleen gegevens invoeren als tijdzones voor alle batchbronnen op basis van tabellen zijn geconfigureerd voor UTC. Het enige tijdstempel dat wordt ondersteund voor de [!DNL Snowflake] -bron is TIMESTAMP_NTZ met UTC-tijd.

[!DNL Snowflake] is een gegevensopslagplatform in de cloud dat is ontworpen om organisaties in staat te stellen grote hoeveelheden gegevens efficiënt op te slaan, te verwerken en te analyseren. [!DNL Snowflake] is ontworpen om de schaalbaarheid en flexibiliteit van de cloud te benutten en ondersteunt gegevensintegratie, geavanceerde analyses en naadloze uitwisseling tussen teams. Als volledig beheerde dienst, [!DNL Snowflake] elimineert onderhoudsingewikkeldheid gemeenschappelijk voor traditionele gegevensbestanden, toelatend u om zich op het afleiden van inzichten en waarde van uw gegevens te concentreren.

U kunt de bron van [!DNL Snowflake] gebruiken om verbinding te maken en uw gegevens van [!DNL Snowflake] naar Adobe Experience Platform te brengen. Lees de onderstaande documentatie voor meer informatie over het instellen van de [!DNL Snowflake] -bron en het maken van verbinding met Experience Platform.

## Vereisten {#prerequisites}

In deze sectie worden de instellingstaken beschreven die u moet uitvoeren voordat u de [!DNL Snowflake] -bron kunt verbinden met Experience Platform.

### IP adres lijst van gewenste personen

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform aan te sluiten. Voor meer informatie, lees de gids op [&#x200B; voegend op lijst van gewenste personen IP adressen om met Experience Platform &#x200B;](../../ip-address-allow-list.md) voor meer informatie te verbinden.

### Vereiste referenties verzamelen

U moet waarden opgeven voor de volgende referentie-eigenschappen om de [!DNL Snowflake] -bron te verifiëren.

>[!BEGINTABS]

>[!TAB  de zeer belangrijke authentificatie van de Rekening (Azure) ]

Geef waarden op voor de volgende gebruikersgegevens om [!DNL Snowflake] in Azure te verbinden met Experience Platform met behulp van accountsleutelverificatie.

| Credentials | Beschrijving |
| ---------- | ----------- |
| `account` | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor verschillende [!DNL Snowflake] -organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `myorg-myaccount.snowflakecomputing.com` . Lees de sectie op [&#x200B; het terugwinnen van uw  [!DNL Snowflake]  rekeningsherkenningsteken &#x200B;](#retrieve-your-account-identifier) voor extra begeleiding. Raadpleeg voor meer informatie de [[!DNL Snowflake] documentatie](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] -pakhuis is onafhankelijk van elkaar en moet afzonderlijk worden benaderd wanneer u gegevens naar Experience Platform overbrengt. |
| `database` | De database [!DNL Snowflake] bevat de gegevens die u aan de Experience Platform wilt toevoegen. |
| `username` | De gebruikersnaam voor de [!DNL Snowflake] -account. |
| `password` | Het wachtwoord voor de [!DNL Snowflake] -gebruikersaccount. |
| `role` | De standaardtoegangsbeheerrol die in de [!DNL Snowflake] -sessie moet worden gebruikt. De rol zou een bestaande moeten zijn die reeds aan de gespecificeerde gebruiker is toegewezen. De standaardrol is `PUBLIC` . |
| `connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met de instantie [!DNL Snowflake] . Het patroon van de verbindingstekenreeks voor [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` . |

>[!TAB  zeer belangrijk-paar authentificatie (Azure) ]

Om zeer belangrijk-paarauthentificatie te gebruiken, produceer eerst een zeer belangrijk paar met 2048 bits RSA. Geef vervolgens waarden op voor de volgende gebruikersgegevens om in Azure verbinding te maken met Experience Platform met behulp van sleutelparverificatie.

| Credentials | Beschrijving |
| --- | --- |
| `account` | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor verschillende [!DNL Snowflake] -organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `myorg-myaccount.snowflakecomputing.com` . Lees de sectie op [&#x200B; het terugwinnen van uw  [!DNL Snowflake]  rekeningsherkenningsteken &#x200B;](#retrieve-your-account-identifier) voor extra begeleiding. Raadpleeg voor meer informatie de [[!DNL Snowflake] documentatie](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | De gebruikersnaam van uw [!DNL Snowflake] -account. |
| `privateKey` | De [!DNL Base64-] gecodeerde privé sleutel van uw [!DNL Snowflake] rekening. U kunt gecodeerde of niet-gecodeerde persoonlijke sleutels genereren. Als u een gecodeerde persoonlijke sleutel gebruikt, moet u ook een persoonlijke-sleutelwachtwoord opgeven bij verificatie met behulp van Experience Platform. Lees de sectie op [&#x200B; het terugwinnen van uw privé sleutel &#x200B;](#retrieve-your-private-key) voor meer informatie. |
| `privateKeyPassphrase` | Persoonlijke sleutel passphrase is een extra laag van veiligheid die u moet gebruiken wanneer het voor authentiek verklaren met een gecodeerde privé sleutel. U hoeft de wachtwoordzin niet op te geven als u een niet-gecodeerde persoonlijke sleutel gebruikt. |
| `port` | Het poortnummer dat door [!DNL Snowflake] wordt gebruikt wanneer verbinding wordt gemaakt met een server via internet. |
| `database` | De [!DNL Snowflake] -database die de gegevens bevat die u aan Experience Platform wilt toevoegen. |
| `warehouse` | Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] -pakhuis is onafhankelijk van elkaar en moet afzonderlijk worden benaderd wanneer u gegevens naar Experience Platform overbrengt. |

Voor meer informatie over deze waarden, verwijs de [[!DNL Snowflake]  sleutel-paar authentificatiegids &#x200B;](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!TAB  Basisauthentificatie (AWS) ]

Geef waarden op voor de volgende aanmeldingsgegevens om via basisverificatie verbinding te maken met Experience Platform op AWS. [!DNL Snowflake]

>[!WARNING]
>
>De basisauthentificatie (of de authentificatie van de rekeningssleutel) voor [!DNL Snowflake] bron zal op November 2025 worden afgekeurd. U moet naar op sleutel-paar gebaseerde authentificatie bewegen om de bron te blijven gebruiken en gegevens van uw gegevensbestand in te voeren aan Experience Platform. Voor meer informatie over de veroudering, lees de [[!DNL Snowflake]  beste praktijkgids bij het verlichten van de risico&#39;s van credentieel compromis &#x200B;](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/).

| Credentials | Beschrijving |
| --- | --- |
| `host` | De host-URL waarmee uw [!DNL Snowflake] -account verbinding maakt. |
| `port` | Het poortnummer dat door [!DNL Snowflake] wordt gebruikt wanneer verbinding wordt gemaakt met een server via internet. |
| `username` | De gebruikersnaam die aan uw [!DNL Snowflake] -account is gekoppeld. |
| `password` | Het wachtwoord dat aan uw [!DNL Snowflake] account is gekoppeld. |
| `database` | De [!DNL Snowflake] -database vanwaar de gegevens worden opgehaald. |
| `schema` | De naam van het schema dat aan uw [!DNL Snowflake] database is gekoppeld. U moet ervoor zorgen dat de gebruiker u gegevensbestandtoegang tot wilt geven, ook toegang tot dit schema heeft. |
| `warehouse` | Het [!DNL Snowflake] -pakhuis dat u gebruikt. |

>[!TAB  zeer belangrijk-paar authentificatie (AWS) ]

Om zeer belangrijk-paarauthentificatie te gebruiken, produceer eerst een zeer belangrijk paar met 2048 bits RSA. Geef vervolgens waarden op voor de volgende gebruikersgegevens om verbinding te maken met Experience Platform op AWS met behulp van sleutelparverificatie.

| Credentials | Beschrijving |
| --- | --- |
| `account` | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor verschillende [!DNL Snowflake] -organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `http://myorg-myaccount.snowflakecomputing.com/` . Lees de gids bij [&#x200B; het terugwinnen van uw  [!DNL Snowflake]  rekeningsherkenningsteken &#x200B;](#etrieve-your-account-identifier) voor extra begeleiding. Raadpleeg voor meer informatie de [[!DNL Snowflake] documentatie](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | De gebruikersnaam van uw [!DNL Snowflake] -account. |
| `privateKey` | De persoonlijke sleutel voor uw [!DNL Snowflake] -gebruiker, base64-gecodeerd als één regel zonder kopteksten of regeleinden. Als u het bestand wilt voorbereiden, kopieert u de inhoud van het PEM-bestand, verwijdert u de `BEGIN`/`END` -regels en alle regeleinden en codeert u het resultaat met base64. Lees de sectie op [&#x200B; het terugwinnen van uw privé sleutel &#x200B;](#retrieve-your-private-key) voor meer informatie. **Nota:** Gecodeerde privé sleutels worden momenteel niet gesteund voor een verbinding van AWS. |
| `port` | Het poortnummer dat door [!DNL Snowflake] wordt gebruikt wanneer verbinding wordt gemaakt met een server via internet. |
| `database` | De [!DNL Snowflake] -database die de gegevens bevat die u aan Experience Platform wilt toevoegen. |
| `warehouse` | Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] -pakhuis is onafhankelijk van elkaar en moet afzonderlijk worden benaderd wanneer u gegevens naar Experience Platform overbrengt. |

Voor meer informatie over deze waarden, verwijs de [[!DNL Snowflake]  sleutel-paar authentificatiegids &#x200B;](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Uw account-id ophalen {#retrieve-your-account-identifier}

U moet uw account-id ophalen van het [!DNL Snowflake] UI-dashboard, aangezien u dit gebruikt om uw [!DNL Snowflake] -instantie op Experience Platform te verifiëren.

Uw account-id ophalen:

* Gebruik het [[!DNL Snowflake]  dashboard van toepassingsUI &#x200B;](https://app.snowflake.com/) om tot uw rekening toegang te hebben.
* Selecteer in de linkernavigatie **[!DNL Accounts]** en selecteer vervolgens **[!DNL Active Accounts]** in de koptekst.
* Selecteer vervolgens het informatiepictogram en selecteer en kopieer de domeinnaam van de huidige URL.

![&#x200B; het dashboard van Snowflake UI met de geselecteerde domeinnaam.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### RSA-sleutelpaar genereren

Gebruik OpenSSL in de interface van de bevellijn om een zeer belangrijk paar met 2048 bits RSA in formaat te produceren PKCS#8. Het is aan te raden een gecodeerde persoonlijke sleutel voor beveiliging te maken. Voor deze sleutel is een wachtwoordzin vereist.

>[!BEGINTABS]

>[!TAB  produceer een gecodeerde privé sleutel ]

Voer de volgende opdracht op uw terminal uit om de gecodeerde [!DNL Snowflake] persoonlijke sleutel te genereren:

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8# You will be prompted to enter a passphrase. Store this securely!
```

>[!TAB  produceer een niet gecodeerde privé sleutel ]

Als u de niet-gecodeerde [!DNL Snowflake] persoonlijke sleutel wilt genereren, voert u de volgende opdracht uit op uw terminal:

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

>[!ENDTABS]

### Een openbare sleutel genereren op basis van uw persoonlijke sleutel

Voer vervolgens de volgende opdracht in uw opdrachtregelinterface uit om een openbare sleutel te maken op basis van uw persoonlijke sleutel.

```bash
openssl rsa -in rsa_key.p8 -pubout -out rsa_key.pub# You will be prompted to enter the passphrase if the private key is encrypted.
```

### De openbare sleutel toewijzen aan de gebruiker van [!DNL Snowflake]

U moet een [!DNL Snowflake] beheerderrol (als **SECURITYADMIN**) gebruiken om de geproduceerde openbare sleutel met de [!DNL Snowflake] de dienstgebruiker te associëren die Experience Platform zal gebruiken. Als u de inhoud van de openbare sleutel wilt ophalen, opent u het `rsa_key.pub` -bestand en kopieert u de volledige inhoud, met uitzondering van de `-----BEGIN PUBLIC KEY----- and -----END PUBLIC KEY-----` -regels. Voer vervolgens de volgende SQL uit in [!DNL Snowflake] :

```sql
ALTER USER {YOUR_SNOWFLAKE_USERNAME}>SET RSA_PUBLIC_KEY='{PUBLIC_KEY_CONTENT}';
```

### De persoonlijke sleutel coderen in [!DNL Base64]

Experience Platform vereist dat de persoonlijke sleutel [!DNL Base64]-gecodeerd is en als een tekenreeks wordt opgegeven tijdens het instellen van de verbinding. Gebruik een geschikt gereedschap of script om de inhoud van het `rsa_key.p8` -bestand te coderen in één [!DNL Base64] -tekenreeks.

>[!TIP]
>
>Zorg ervoor dat er voor of na het coderingsproces geen extra spaties of regeleinden zijn, inclusief de kop- of voettekstregels `(-----BEGIN ENCRYPTED PRIVATE KEY----- and -----END ENCRYPTED PRIVATE KEY-----)` , omdat dit verificatiefouten kan veroorzaken.

### Configuraties verifiëren

Voordat u de [!DNL Snowflake] -bronverbinding maakt in Experience Platform, moet u ervoor zorgen dat de waarden **[!DNL Default Role]** en **[!DNL Default Warehouse]** van de gebruiker overeenkomen met die van uw provider in Experience Platform. U kunt deze instellingen verifiëren in de gebruikersinterface van [!DNL Snowflake] met de SQL-opdracht van `DESCRIBE USER {USERNAME}` .

U kunt ook de onderstaande stappen volgen om uw instellingen te controleren:

* Selecteer **[!DNL Admin]** in de linkernavigatie en selecteer vervolgens **[!DNL Users & Roles]** .
* Selecteer de juiste gebruiker en selecteer vervolgens de ellipsen (`...`) in de rechterbovenhoek.
* Navigeer in het [!DNL Edit user] -venster dat wordt weergegeven naar [!DNL Default Role] om de rol weer te geven die aan de opgegeven gebruiker is gekoppeld.
* Navigeer in hetzelfde venster naar [!DNL Default Warehouse] om het pakhuis weer te geven dat aan de opgegeven gebruiker is gekoppeld.

![&#x200B; Snowflake UI waar u uw rol en pakhuis kunt verifiëren.](../../images/tutorials/create/snowflake/snowflake-configs.png)

## Volgende stappen

Nadat de installatie is voltooid, kunt u nu doorgaan om uw [!DNL Snowflake] -account aan te sluiten op Experience Platform. Raadpleeg de volgende documentatie voor meer informatie:

### Verbinding maken [!DNL Snowflake] met Experience Platform via API&#39;s

* [Verbind  [!DNL Snowflake]  met Experience Platform gebruikend API](../../tutorials/api/create/databases/snowflake.md)
* [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
* [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

### Verbinding maken [!DNL Snowflake] met Experience Platform via de gebruikersinterface

* [Verbind  [!DNL Snowflake]  met Experience Platform gebruikend UI](../../tutorials/ui/create/databases/snowflake.md)
* [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)
