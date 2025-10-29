---
title: Snowflake Streaming Source Connector - Overzicht
description: Leer hoe u een bronverbinding en gegevensstroom kunt maken om streaminggegevens van uw Snowflake-instantie naar Adobe Experience Platform in te voeren
badgeUltimate: label="Ultimate" type="Positive"
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 0%

---

# [!DNL Snowflake] streamingbron

>[!IMPORTANT]
>
>* De [!DNL Snowflake] -streamingbron is in de API beschikbaar voor gebruikers die Real-Time CDP Ultimate hebben aangeschaft.
>
>* U kunt nu de [!DNL Snowflake] -streamingbron gebruiken wanneer u Adobe Experience Platform uitvoert op Amazon Web Services (AWS). Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [&#x200B; multi-wolkenoverzicht van Experience Platform &#x200B;](../../../landing/multi-cloud.md).

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het streamen van gegevens uit een [!DNL Snowflake] -database.

## De [!DNL Snowflake] streamingbron

De [!DNL Snowflake] streamingbron werkt door gegevens te laten laden door periodiek een SQL-query uit te voeren en een uitvoerrecord te maken voor elke rij in de resulterende set.

Met [!DNL Kafka Connect] houdt de [!DNL Snowflake] streamingbron de meest recente record bij die van elke tabel wordt ontvangen, zodat deze op de juiste locatie voor de volgende herhaling kan beginnen. De bron gebruikt deze functionaliteit om gegevens te filteren en slechts de bijgewerkte rijen van een lijst op elke herhaling te krijgen.

## Vereisten

In de volgende sectie worden de vereiste stappen beschreven die moeten worden uitgevoerd voordat u gegevens kunt streamen van uw [!DNL Snowflake] -database naar Experience Platform:

### IP adres lijst van gewenste personen

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform aan te sluiten. Voor meer informatie, lees de gids op [&#x200B; voegend op lijst van gewenste personen IP adressen om met Experience Platform &#x200B;](../../ip-address-allow-list.md) voor meer informatie te verbinden.

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Amazon Redshift] en Experience Platform via API&#39;s of de gebruikersinterface:

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Snowflake] als u de volgende verbindingseigenschappen opgeeft:

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

| Credentials | Beschrijving |
| --- | --- |
| `account` | De volledige account-id (naam van account of accountlocator) van uw [!DNL Snowflake] -account is toegevoegd met het achtervoegsel `snowflakecomputing.com` . De account-id kan verschillende indelingen hebben: <ul><li>{ORG_NAME} - {ACCOUNT_NAME} .snowflakecomputing.com (b.v. `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID} .snowflakecomputing.com (bijvoorbeeld `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD} .snowflakecomputing.com (bijvoorbeeld `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> Voor meer informatie, lees [[!DNL Snowflake document on account identifiers] &#x200B;](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] -pakhuis is onafhankelijk van elkaar en moet afzonderlijk worden benaderd wanneer u gegevens naar Experience Platform overbrengt. |
| `database` | De database [!DNL Snowflake] bevat de gegevens die u aan de Experience Platform wilt toevoegen. |
| `username` | De gebruikersnaam voor de [!DNL Snowflake] -account. |
| `password` | Het wachtwoord voor de [!DNL Snowflake] -gebruikersaccount. |
| `role` | (Optioneel) Een op maat gedefinieerde rol die voor een gebruiker, voor een bepaalde verbinding kan worden opgegeven. Als deze waarde niet is opgegeven, wordt deze standaard ingesteld op `public` . |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Snowflake] is `51ae16c2-bdad-42fd-9fce-8d5dfddaf140` . |

>[!TAB  zeer belangrijk-paar authentificatie ]

Als u sleutelparverificatie wilt gebruiken, moet u een 2048-bits RSA-sleutelpaar genereren en de volgende waarden opgeven wanneer u een account voor uw [!DNL Snowflake] -bron maakt.

| Credentials | Beschrijving |
| --- | --- |
| `account` | Een accountnaam vormt een unieke identificatie van een account binnen uw organisatie. In dit geval moet u een account op unieke wijze identificeren voor verschillende [!DNL Snowflake] -organisaties. Hiervoor moet u de naam van uw organisatie aan de accountnaam toevoegen. Bijvoorbeeld: `orgname-account_name` . Lees de gids bij [&#x200B; het terugwinnen van uw  [!DNL Snowflake]  rekeningsherkenningsteken &#x200B;](./snowflake.md#retrieve-your-account-identifier) voor extra begeleiding. Raadpleeg voor meer informatie de [[!DNL Snowflake] documentatie](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | De gebruikersnaam van uw [!DNL Snowflake] -account. |
| `privateKey` | De [!DNL Base64-] gecodeerde privé sleutel van uw [!DNL Snowflake] rekening. U kunt gecodeerde of niet-gecodeerde persoonlijke sleutels genereren. Als u een gecodeerde persoonlijke sleutel gebruikt, moet u ook een persoonlijke-sleutelwachtwoord opgeven bij verificatie met behulp van Experience Platform. Lees de gids op [&#x200B; het terugwinnen van uw  [!DNL Snowflake]  privé sleutel &#x200B;](./snowflake.md) voor meer informatie. |
| `passphrase` | Passphrase is een extra laag van veiligheid die u moet gebruiken wanneer het voor authentiek verklaren met een gecodeerde privé sleutel. U hoeft de wachtwoordzin niet op te geven als u een niet-gecodeerde persoonlijke sleutel gebruikt. |
| `database` | De [!DNL Snowflake] -database die de gegevens bevat die u aan Experience Platform wilt toevoegen. |
| `warehouse` | Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] -pakhuis is onafhankelijk van elkaar en moet afzonderlijk worden benaderd wanneer u gegevens naar Experience Platform overbrengt. |

Voor meer informatie over deze waarden, verwijs de [[!DNL Snowflake]  sleutel-paar authentificatiegids &#x200B;](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Uw account-id ophalen {#retrieve-your-account-identifier}

Als u uw [!DNL Snowflake] -instantie wilt verifiëren met Experience Platform, moet u uw account-id opvragen via het [!DNL Snowflake] UI-dashboard.

Voer de volgende stappen uit om uw account-id te zoeken:

* Navigeer aan uw rekening op het [[!DNL Snowflake]  toepassingsUI dashboard &#x200B;](https://app.snowflake.com/).
* Selecteer in de linkernavigatie **[!DNL Accounts]** , gevolgd door **[!DNL Active Accounts]** in de koptekst.
* Selecteer vervolgens het informatiepictogram en selecteer en kopieer de domeinnaam van de huidige URL.

### Persoonlijke sleutel ophalen {#retrieve-your-private-key}

Als u sleutelparverificatie wilt gebruiken voor uw [!DNL Snowflake] -verbinding, moet u een persoonlijke sleutel genereren voordat u verbinding maakt met Experience Platform.

>[!BEGINTABS]

>[!TAB  creeer een gecodeerde privé sleutel ]

Voer de volgende opdracht op uw terminal uit om de gecodeerde [!DNL Snowflake] persoonlijke sleutel te genereren:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

Als dit lukt, ontvangt u de persoonlijke sleutel in de PEM-indeling.

```shell
|-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
|-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB  creeer een niet gecodeerde privé sleutel ]

Als u de niet-gecodeerde [!DNL Snowflake] persoonlijke sleutel wilt genereren, voert u de volgende opdracht uit op uw terminal:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

Als dit lukt, ontvangt u de persoonlijke sleutel in de PEM-indeling.

```shell
|-----BEGIN PRIVATE KEY-----
MIIE6T...
|-----END PRIVATE KEY-----
```

>[!ENDTABS]

Nadat u de persoonlijke sleutel hebt gegenereerd, codeert u deze rechtstreeks in [!DNL Base64] zonder wijzigingen aan te brengen in de indeling of inhoud. Zorg ervoor dat er aan het einde van de persoonlijke sleutel geen extra spaties of lege regels (inclusief volgnewlines) staan voordat u gaat coderen.

### Configuraties verifiëren

Voordat u een bronverbinding voor uw [!DNL Snowflake] gegevens kunt maken, moet u ook controleren of aan de volgende configuraties is voldaan:

* Het standaardpakhuis dat aan een bepaalde gebruiker wordt toegewezen moet het zelfde zijn als het pakhuis dat u wanneer het voor authentiek verklaren aan Experience Platform invoert.
* De standaardrol die aan een bepaalde gebruiker wordt toegewezen moet toegang tot het zelfde gegevensbestand hebben dat u wanneer het voor authentiek verklaren aan Experience Platform invoert.

Om uw rol en pakhuis te verifiëren:

* Selecteer **[!DNL Admin]** in de linkernavigatie en selecteer vervolgens **[!DNL Users & Roles]** .
* Selecteer de juiste gebruiker en selecteer vervolgens de ellipsen (`...`) in de rechterbovenhoek.
* Navigeer in het [!DNL Edit user] -venster dat wordt weergegeven naar [!DNL Default Role] om de rol weer te geven die aan de opgegeven gebruiker is gekoppeld.
* Navigeer in hetzelfde venster naar [!DNL Default Warehouse] om het pakhuis weer te geven dat aan de opgegeven gebruiker is gekoppeld.

Nadat de codering is voltooid, kunt u die [!DNL Base64] gecodeerde persoonlijke sleutel op Experience Platform gebruiken om uw [!DNL Snowflake] -account te verifiëren.

### Rolinstellingen configureren {#configure-role-settings}

U moet voorrechten aan een rol vormen, zelfs als de standaard openbare rol wordt toegewezen, om uw bronverbinding toe te staan om tot het relevante [!DNL Snowflake] gegevensbestand, schema, en lijst toegang te hebben. De verschillende rechten voor verschillende [!DNL Snowflake] -entiteiten zijn als volgt:

| [!DNL Snowflake] entiteit | Rolvoorrecht vereisen |
| --- | --- |
| Warehouse | WERKEN, GEBRUIKEN |
| Database | GEBRUIK |
| Schema | GEBRUIK |
| Tabel | SELECT |

>[!NOTE]
>
>De auto-hervat en auto-onderbreekt moeten in de geavanceerde montagesconfiguratie van uw pakhuis worden toegelaten.

Voor meer informatie over rol en voorrechtbeheer, verwijs naar de [[!DNL Snowflake]  API verwijzing &#x200B;](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Unix-tijd converteren naar datumvelden

[!DNL Snowflake Streaming] ontleedt en schrijft ` DATE` gebieden als aantal dagen sinds het tijdperk van Unix (1970-01-01). Een `DATE` -waarde 0 betekent bijvoorbeeld 1 januari 1970, een waarde van 1 betekent 2 januari 1970. Wanneer u het bestand voorbereidt om toewijzingen te maken in de [!DNL Snowflake Streaming] -bron, moet u er daarom voor zorgen dat de `DATE` -kolom wordt weergegeven als een geheel getal.

U kunt {de gegevens en tijdfuncties van de Prep van Gegevens van 0} gebruiken [&#x200B; om de tijd van Unix in datumgebieden om te zetten die in Experience Platform kunnen worden opgenomen. &#x200B;](../../../data-prep/functions.md#date-and-time-functions) Bijvoorbeeld:

```shell
dformat({DATE_COLUMN} * 86400000, "yyyy-MM-dd")
```

In deze functie:

* `{DATE_COLUMN}` is de datumkolom die het gehele getal van de epoche-dag bevat.
* Vermenigvuldigen met 8640000 zet de epochdagen om in milliseconden.
* &#39;yyyy-MM-dd&#39; geeft de gewenste datumnotatie aan.

Deze omzetting zorgt ervoor dat de datum correct in uw dataset wordt vertegenwoordigd.


## Beperkingen en veelgestelde vragen {#limitations-and-frequently-asked-questions}

* De gegevensdoorvoer voor de [!DNL Snowflake] -bron is 2000 records per seconde.
* De prijs kan afhankelijk van de hoeveelheid tijd variëren dat een pakhuis actief is en de grootte van het pakhuis. Voor de [!DNL Snowflake] bronintegratie, is de kleinste grootte, x-kleine pakhuis voldoende. Voorgesteld wordt automatische schorsing in te schakelen, zodat het entrepot in zijn eentje kan worden stilgelegd wanneer het niet in gebruik is.
* De [!DNL Snowflake] -bron vraagt de database om de tien seconden om nieuwe gegevens.
* Configuratieopties:
   * Wanneer u een bronverbinding maakt, kunt u een `backfill` booleaanse markering voor uw [!DNL Snowflake] -bron inschakelen.
      * Als backfill is ingesteld op true, wordt de waarde voor timestamp.initial ingesteld op 0. Dit betekent dat gegevens met een tijdstempelkolom die langer is dan 0 tijdperk worden opgehaald.
      * Als backfill is ingesteld op false, wordt de waarde voor timestamp.initial ingesteld op -1. Dit betekent dat gegevens met een tijdstempelkolom die langer is dan de huidige tijd (de tijd waarin de bron begint op te nemen), worden opgehaald.
   * De tijdstempelkolom moet worden opgemaakt als type: `TIMESTAMP_LTZ` of `TIMESTAMP_NTZ` . Als de tijdstempelkolom is ingesteld op `TIMESTAMP_NTZ` , moet de bijbehorende tijdzone waarin de waarden zijn opgeslagen, via de parameter `timezoneValue` worden doorgegeven. Als deze waarde niet wordt opgegeven, wordt de standaardwaarde voor UTC gebruikt.
      * `TIMESTAMP_TZ` kan niet worden gebruikt in een tijdstempelkolom of in een toewijzing.

## Volgende stappen

>[!NOTE]
>
>Nadat u een streaming gegevensstroom hebt gemaakt of bijgewerkt, moet u de gegevensinvoer kort na vijf minuten pauzeren om te voorkomen dat gegevens verloren gaan of dat gegevens verloren gaan.

In de volgende zelfstudie worden stappen beschreven voor het verbinden van uw [!DNL Snowflake] -streamingbron met Experience Platform met behulp van de API:

* [De gegevens van de stroom van a [!DNL Snowflake]  gegevensbestand aan Experience Platform die de Dienst API van de Stroom gebruiken](../../tutorials/api/create/databases/snowflake-streaming.md)
* [De gegevens van de stroom van a [!DNL Snowflake]  gegevensbestand aan Experience Platform gebruikend de bronwerkruimte in het gebruikersinterface van Experience Platform](../../tutorials/ui/create/databases/snowflake-streaming.md)
