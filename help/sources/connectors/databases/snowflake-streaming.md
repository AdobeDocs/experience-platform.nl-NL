---
title: Overzicht van Snowflake-streamingbronconnector
description: Leer hoe u een bronverbinding en gegevensstroom kunt maken om streaminggegevens van uw Snowflake-instantie naar Adobe Experience Platform in te voeren
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: cfe5f34316e9db072f0a320143354f2771b4a3a9
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 1%

---

# [!DNL Snowflake] streamingbron

>[!IMPORTANT]
>
>* De [!DNL Snowflake] streamingbron is in bèta. Lees de [Overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.
>* De [!DNL Snowflake] De streamingbron is beschikbaar in de broncatalogus voor klanten die Real-Time CDP Ultimate hebben aangeschaft.


Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

Experience Platform biedt ondersteuning voor het streamen van gegevens van een [!DNL Snowflake] database.

## De [!DNL Snowflake] streamingbron

De [!DNL Snowflake] het stromen bron werkt door gegevens te hebben die door een SQL vraag periodiek worden geladen uit te voeren en een outputverslag voor elke rij in de resulterende reeks te creëren.

Met [!DNL Kafka Connect]de [!DNL Snowflake] streamingbron volgt de meest recente record die de bron van elke tabel ontvangt, zodat deze op de juiste locatie voor de volgende herhaling kan beginnen. De bron gebruikt deze functionaliteit om gegevens te filteren en slechts de bijgewerkte rijen van een lijst op elke herhaling te krijgen.

## Vereisten

In de volgende sectie worden de vereiste stappen beschreven die moeten worden uitgevoerd voordat u gegevens kunt streamen vanuit uw [!DNL Snowflake] database naar Experience Platform:

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om te verbinden met [!DNL Snowflake]moet u de volgende eigenschappen voor de verbinding opgeven:

| Credentials | Beschrijving |
| --- | --- |
| `account` | De volledige accountnaam die aan uw [!DNL Snowflake] account. Een volledig gekwalificeerde [!DNL Snowflake] de naam van uw account bevat uw accountnaam, regio en cloudplatform. Bijvoorbeeld, `cj12345.east-us-2.azure`. Raadpleeg deze voor meer informatie over accountnamen [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | De [!DNL Snowflake] Het pakhuis beheert het proces van de vraaguitvoering voor de toepassing. Elk [!DNL Snowflake] magazijn is onafhankelijk van elkaar en moet individueel worden benaderd wanneer gegevens naar het Platform worden overgebracht. |
| `database` | De [!DNL Snowflake] de database bevat de gegevens die u het Platform wilt brengen. |
| `username` | De gebruikersnaam voor de [!DNL Snowflake] account. |
| `password` | Het wachtwoord voor de [!DNL Snowflake] gebruikersaccount. |
| `role` | (Optioneel) Een op maat gedefinieerde rol die voor een gebruiker, voor een bepaalde verbinding kan worden opgegeven. Indien niet opgegeven, wordt deze waarde standaard ingesteld op `public`. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Snowflake] is `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

Voor meer informatie over authentificatie, verwijs naar dit [[!DNL Snowflake] document](<https://docs.snowflake.com/en/user-guide/key-pair-auth.html>).

### Rolinstellingen configureren {#configure-role-settings}

U moet voorrechten aan een rol vormen, zelfs als de standaard openbare rol wordt toegewezen, om uw bronverbinding toe te staan om tot relevante toegang te hebben [!DNL Snowflake] database, schema en tabel. De verschillende rechten voor verschillende [!DNL Snowflake] entiteiten:

| [!DNL Snowflake] entiteit | Rolvoorrecht vereisen |
| --- | --- |
| Warehouse | WERKEN, GEBRUIKEN |
| Database | GEBRUIK |
| Schema | GEBRUIK |
| Tabel | SELECT |

>[!NOTE]
>
>De auto-hervat en auto-onderbreekt moeten in de geavanceerde montagesconfiguratie van uw pakhuis worden toegelaten.

Voor meer informatie over rol en voorrechtbeheer raadpleegt u de [[!DNL Snowflake] API-referentie](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Beperkingen en veelgestelde vragen {#limitations-and-frequently-asked-questions}

* De gegevensdoorvoer voor de [!DNL Snowflake] bron is 2000 records per seconde.
* De prijs kan afhankelijk van de hoeveelheid tijd variëren dat een pakhuis actief is en de grootte van het pakhuis. Voor de [!DNL Snowflake] bronintegratie, de kleinste grootte, x-kleine pakhuis is voldoende. Voorgesteld wordt automatische schorsing in te schakelen, zodat het entrepot in zijn eentje kan worden stilgelegd wanneer het niet in gebruik is.
* De [!DNL Snowflake] bron opinieert het gegevensbestand voor nieuwe gegevens om de 10 seconden.
* Configuratieopties:
   * U kunt een `backfill` Booleaanse markering voor uw [!DNL Snowflake] bron bij het maken van een bronverbinding.
      * Als backfill is ingesteld op true, wordt de waarde voor timestamp.initial ingesteld op 0. Dit betekent dat gegevens met een tijdstempelkolom die langer is dan 0 tijdperk worden opgehaald.
      * Als backfill is ingesteld op false, wordt de waarde voor timestamp.initial ingesteld op -1. Dit betekent dat gegevens met een tijdstempelkolom die langer is dan de huidige tijd (de tijd waarin de bron begint op te nemen), worden opgehaald.
   * De tijdstempelkolom moet als type worden opgemaakt: `TIMESTAMP_LTZ` of `TIMESTAMP_NTZ`. Als de tijdstempelkolom is ingesteld op `TIMESTAMP_NTZ`, dan zouden de types in UTC tijd in het gegevensbestand moeten worden opgeslagen.

## Volgende stappen

De volgende zelfstudie bevat stappen voor het tot stand brengen van een verbinding met uw [!DNL Snowflake] streamingbron naar Experience Platform met behulp van de API:

* [Gegevens streamen van een [!DNL Snowflake] database naar Experience Platform met behulp van de Flow Service API](../../tutorials/api/create/databases/snowflake-streaming.md)

