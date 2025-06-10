---
title: Snowflake Streaming Source Connector - Overzicht
description: Leer hoe u een bronverbinding en gegevensstroom kunt maken om streaminggegevens van uw Snowflake-instantie naar Adobe Experience Platform in te voeren
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-09-24T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# [!DNL Snowflake] streamingbron

>[!IMPORTANT]
>
>* De [!DNL Snowflake] -streamingbron is in de API beschikbaar voor gebruikers die Real-Time CDP Ultimate hebben aangeschaft.
>
>* U kunt nu de [!DNL Snowflake] -streamingbron gebruiken wanneer u Adobe Experience Platform uitvoert op Amazon Web Services (AWS). Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](../../../landing/multi-cloud.md).


Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het streamen van gegevens uit een [!DNL Snowflake] -database.

## De [!DNL Snowflake] streamingbron

De [!DNL Snowflake] streamingbron werkt door gegevens te laten laden door periodiek een SQL-query uit te voeren en een uitvoerrecord te maken voor elke rij in de resulterende set.

Met [!DNL Kafka Connect] houdt de [!DNL Snowflake] streamingbron de meest recente record bij die van elke tabel wordt ontvangen, zodat deze op de juiste locatie voor de volgende herhaling kan beginnen. De bron gebruikt deze functionaliteit om gegevens te filteren en slechts de bijgewerkte rijen van een lijst op elke herhaling te krijgen.

## Vereisten

In de volgende sectie worden de vereiste stappen beschreven die moeten worden uitgevoerd voordat u gegevens kunt streamen van uw [!DNL Snowflake] -database naar Experience Platform:

### Werk uw IP lijst van gewenste personen van het adres bij

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md#ip-address-allow-list-for-streaming-sources) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Amazon Redshift] en Experience Platform via API&#39;s of de gebruikersinterface:

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Snowflake] als u de volgende verbindingseigenschappen opgeeft:

| Credentials | Beschrijving |
| --- | --- |
| `account` | De volledige account-id (naam van account of accountlocator) van uw [!DNL Snowflake] -account is toegevoegd met het achtervoegsel `snowflakecomputing.com` . De account-id kan verschillende indelingen hebben: <ul><li>{ORG_NAME} - {ACCOUNT_NAME} .snowflakecomputing.com (b.v. `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID} .snowflakecomputing.com (bijvoorbeeld `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD} .snowflakecomputing.com (bijvoorbeeld `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> Voor meer informatie, lees [[!DNL Snowflake document on account identifiers] ](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | Het [!DNL Snowflake] pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] -pakhuis is onafhankelijk van elkaar en moet afzonderlijk worden benaderd wanneer u gegevens naar Experience Platform overbrengt. |
| `database` | De database [!DNL Snowflake] bevat de gegevens die u aan de Experience Platform wilt toevoegen. |
| `username` | De gebruikersnaam voor de [!DNL Snowflake] -account. |
| `password` | Het wachtwoord voor de [!DNL Snowflake] -gebruikersaccount. |
| `role` | (Optioneel) Een op maat gedefinieerde rol die voor een gebruiker, voor een bepaalde verbinding kan worden opgegeven. Als deze waarde niet is opgegeven, wordt deze standaard ingesteld op `public` . |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Snowflake] is `51ae16c2-bdad-42fd-9fce-8d5dfddaf140` . |

{style="table-layout:auto"}

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

Voor meer informatie over rol en voorrechtbeheer, verwijs naar de [[!DNL Snowflake]  API verwijzing ](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

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
