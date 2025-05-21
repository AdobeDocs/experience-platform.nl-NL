---
title: Verbindingsoverzicht MariaDB Source
description: Leer hoe u MariaDB met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
last-substantial-update: 2025-04-29T00:00:00Z
exl-id: 37b8f991-dca9-4f85-9bdd-4927a015e4c0
source-git-commit: bca4f40d452f0a5e70a388872a65640d1fd58533
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# [!DNL MariaDB]

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met [!DNL Experience Platform] -services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een database van derden. [!DNL Experience Platform] kan verbinding maken met verschillende typen databases, zoals relationele databases, NoSQL-databases of gegevensopslagruimten. Ondersteuning voor databaseproviders is onder andere [!DNL MariaDB] .

## Vereisten {#prerequisites}

Lees de volgende secties om de vereiste instellingen te voltooien voordat u uw [!DNL MariaDB] -account aansluit op Experience Platform.

### IP adres lijst van gewenste personen

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform aan te sluiten. Voor meer informatie, lees de gids op [ voegend op lijst van gewenste personen IP adressen om met Experience Platform ](../../ip-address-allow-list.md) voor meer informatie te verbinden.

### Verifiëren voor Experience Platform

U moet waarden opgeven voor de volgende referenties om [!DNL MariaDB] te verbinden met Experience Platform.

>[!BEGINTABS]

>[!TAB  de belangrijkste authentificatie van de Rekening ]

Geef de juiste waarden voor de volgende referenties op om verificatie met de accountsleutel te gebruiken.

| Credentials | Beschrijving |
| --- | --- |
| `connectionString` | De verbindingstekenreeks die aan uw [!DNL MariaDB] -verificatie is gekoppeld. Het patroon van de [!DNL MariaDB] verbindingstekenreeks is: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` . |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL MariaDB] is `3000eb99-cd47-43f3-827c-43caf170f015` . **Nota**: Deze referentie wordt slechts vereist wanneer het verbinden door [!DNL Flow Service] API. |

Voor meer informatie over het verkrijgen van een verbindingskoord, verwijs naar dit [[!DNL MariaDB]  document ](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!TAB  Basisauthentificatie ]

Om basisauthentificatie te gebruiken, verstrek de aangewezen waarden voor de volgende geloofsbrieven.

| Credentials | Beschrijving |
| --- | --- |
| `server` | De naam of IP van uw [!DNL MariaDB] database. |
| `username` | De naam van uw database. |
| `port` | Het havenaantal van het communicatie eindpunt u met verbindt. |
| `password` | De gebruikersnaam die overeenkomt met uw database. |
| `database` | Het wachtwoord dat overeenkomt met uw database. |
| `sslMode` | De methode waarmee gegevens tijdens gegevensoverdracht worden gecodeerd. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL MariaDB] is `3000eb99-cd47-43f3-827c-43caf170f015` . **Nota**: Deze referentie wordt slechts vereist wanneer het verbinden door [!DNL Flow Service] API. |

Voor meer informatie over het verkrijgen van een verbindingskoord, verwijs naar dit [[!DNL MariaDB]  document ](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!ENDTABS]

## Verbinding maken [!DNL MariaDB] met Experience Platform via API&#39;s

- [Een MariaDB-basisverbinding maken met de Flow Service API](../../tutorials/api/create/databases/mariadb.md)
- [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
- [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbinding maken [!DNL MariaDB] met Experience Platform via de gebruikersinterface

- [Een MariaDB-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/databases/mariadb.md)
- [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)
