---
title: Overzicht Snowflake Source Connector
description: Leer hoe u Snowflake met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 0476c42924bf0163380e650141fad8e50b98d4cf
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 1%

---

# [!DNL Snowflake] bron

>[!IMPORTANT]
>
>* De [!DNL Snowflake] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.
>* Standaard wordt [!DNL Snowflake] source `null` geïnterpreteerd als een lege tekenreeks. Neem contact op met uw Adobe-vertegenwoordiger om ervoor te zorgen dat de `null` -waarden correct worden geschreven zoals `null` in Adobe Experience Platform.
>* Experience Platform kan alleen gegevens invoeren als tijdzones voor alle batchbronnen op basis van tabellen zijn geconfigureerd voor UTC. Het enige tijdstempel dat wordt ondersteund voor de [!DNL Snowflake] -bron is TIMESTAMP_NTZ met UTC-tijd.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een database van derden. Experience Platform kan verbinding maken met verschillende typen databases, zoals relationele databases, NoSQL-databases of gegevensopslagruimten. Ondersteuning voor databaseproviders is onder andere [!DNL Snowflake] .

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
| `account` | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor verschillende [!DNL Snowflake] -organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `orgname-account_name` . Lees de sectie op [&#x200B; het terugwinnen van uw  [!DNL Snowflake]  rekeningsherkenningsteken &#x200B;](#retrieve-your-account-identifier) voor extra begeleiding. Raadpleeg voor meer informatie de [[!DNL Snowflake] documentatie](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
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
| `account` | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor verschillende [!DNL Snowflake] -organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `orgname-account_name` . Lees de sectie op [&#x200B; het terugwinnen van uw  [!DNL Snowflake]  rekeningsherkenningsteken &#x200B;](#retrieve-your-account-identifier) voor extra begeleiding. Raadpleeg voor meer informatie de [[!DNL Snowflake] documentatie](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
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
| `account` | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor verschillende [!DNL Snowflake] -organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `orgname-account_name` . Lees de gids bij [&#x200B; het terugwinnen van uw  [!DNL Snowflake]  rekeningsherkenningsteken &#x200B;](#etrieve-your-account-identifier) voor extra begeleiding. Raadpleeg voor meer informatie de [[!DNL Snowflake] documentatie](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | De gebruikersnaam van uw [!DNL Snowflake] -account. |
| `privateKey` | De persoonlijke sleutel voor uw [!DNL Snowflake] -gebruiker, base64-gecodeerd als één regel zonder kopteksten of regeleinden. Als u het bestand wilt voorbereiden, kopieert u de inhoud van het PEM-bestand, verwijdert u de `BEGIN`/`END` -regels en alle regeleinden en codeert u het resultaat met base64. Lees de sectie op [&#x200B; het terugwinnen van uw privé sleutel &#x200B;](#retrieve-your-private-key) voor meer informatie. **Nota:** Gecodeerde privé sleutels worden momenteel niet gesteund voor een verbinding van AWS. |
| `port` | Het poortnummer dat door [!DNL Snowflake] wordt gebruikt wanneer verbinding wordt gemaakt met een server via internet. |
| `database` | De [!DNL Snowflake] -database die de gegevens bevat die u aan Experience Platform wilt toevoegen. |
| `warehouse` | Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] -pakhuis is onafhankelijk van elkaar en moet afzonderlijk worden benaderd wanneer u gegevens naar Experience Platform overbrengt. |

Voor meer informatie over deze waarden, verwijs de [[!DNL Snowflake]  sleutel-paar authentificatiegids &#x200B;](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Uw account-id ophalen {#retrieve-your-account-identifier}

U moet uw account-id ophalen van het [!DNL Snowflake] UI-dashboard omdat u de account-id gebruikt om uw [!DNL Snowflake] -instantie op Experience Platform te verifiëren.

Uw account-id ophalen:

* Navigeer aan uw rekening op het [[!DNL Snowflake]  toepassingsUI dashboard &#x200B;](https://app.snowflake.com/).
* Selecteer in de linkernavigatie **[!DNL Accounts]** , gevolgd door **[!DNL Active Accounts]** in de koptekst.
* Selecteer vervolgens het informatiepictogram en selecteer en kopieer de domeinnaam van de huidige URL.

![&#x200B; het dashboard van Snowflake UI met de geselecteerde domeinnaam.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Persoonlijke sleutel ophalen {#retrieve-your-private-key}

Als u sleutelparverificatie gebruikt voor uw [!DNL Snowflake] -verbinding, moet u ook uw persoonlijke sleutel genereren voordat u verbinding maakt met Experience Platform.

>[!BEGINTABS]

>[!TAB  creeer een gecodeerde privé sleutel ]

Voer de volgende opdracht op uw terminal uit om de gecodeerde [!DNL Snowflake] persoonlijke sleutel te genereren:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

Als dit lukt, ontvangt u de persoonlijke sleutel in de PEM-indeling.

```shell
-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB  creeer een niet gecodeerde privé sleutel ]

Als u de niet-gecodeerde [!DNL Snowflake] persoonlijke sleutel wilt genereren, voert u de volgende opdracht uit op uw terminal:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

Als dit lukt, ontvangt u de persoonlijke sleutel in de PEM-indeling.

```shell
-----BEGIN PRIVATE KEY-----
MIIE6T...
-----END PRIVATE KEY-----
```

>[!ENDTABS]

Neem vervolgens uw persoonlijke sleutel en codeer deze in [!DNL Base64] . Zorg ervoor dat u geen transformaties of opmaakconversies uitvoert op de persoonlijke sleutel van [!DNL Snowflake] . Bovendien moet u ervoor zorgen dat er geen navolgende nieuwe-regeltekens aan het einde van de persoonlijke sleutel staan voordat u deze codeert in [!DNL Base64] .

### Configuraties verifiëren

Voordat u een bronverbinding voor uw [!DNL Snowflake] gegevens kunt maken, moet u ook controleren of aan de volgende configuraties is voldaan:

* Het standaardpakhuis dat aan een bepaalde gebruiker wordt toegewezen moet het zelfde zijn als het pakhuis dat u wanneer het voor authentiek verklaren aan Experience Platform invoert.
* De standaardrol die aan een bepaalde gebruiker wordt toegewezen moet toegang tot het zelfde gegevensbestand hebben dat u wanneer het voor authentiek verklaren aan Experience Platform invoert.

Om uw rol en pakhuis te verifiëren:

* Selecteer **[!DNL Admin]** in de linkernavigatie en selecteer vervolgens **[!DNL Users & Roles]** .
* Selecteer de juiste gebruiker en selecteer vervolgens de ellipsen (`...`) in de rechterbovenhoek.
* Navigeer in het [!DNL Edit user] -venster dat wordt weergegeven naar [!DNL Default Role] om de rol weer te geven die aan de opgegeven gebruiker is gekoppeld.
* Navigeer in hetzelfde venster naar [!DNL Default Warehouse] om het pakhuis weer te geven dat aan de opgegeven gebruiker is gekoppeld.

![&#x200B; Snowflake UI waar u uw rol en pakhuis kunt verifiëren.](../../images/tutorials/create/snowflake/snowflake-configs.png)

Nadat de codering is voltooid, kunt u die [!DNL Base64] gecodeerde persoonlijke sleutel op Experience Platform gebruiken om uw [!DNL Snowflake] -account te verifiëren.

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Snowflake] en Experience Platform via API&#39;s of de gebruikersinterface:

## Verbinding maken [!DNL Snowflake] met Experience Platform via API&#39;s

* [Een Snowflake-basisverbinding maken met de Flow Service API](../../tutorials/api/create/databases/snowflake.md)
* [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
* [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbinding maken [!DNL Snowflake] met Experience Platform via de gebruikersinterface

* [Een Snowflake-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/databases/snowflake.md)
* [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)
