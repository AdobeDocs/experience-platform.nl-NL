---
title: Overzicht van de PostSQL Source Connector
description: Meer informatie over de PostgreSQL-bron op Adobe Experience Platform.
exl-id: 27b891c5-5fc5-4539-8f98-e3a53e2eefe3
source-git-commit: 98d1bec3cd453f3a20b8871b891b5464ddd44a09
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# [!DNL PostgreSQL]

Lees dit document voor meer informatie over de stappen die u moet uitvoeren voordat u de [!DNL PostgreSQL] -database kunt verbinden met Adobe Experience Platform.

## Vereisten {#prerequisites}

Lees de volgende secties om de vereiste setup te voltooien voordat u de [!DNL PostgreSQL] -database verbindt met Experience Platform.

### IP adres lijst van gewenste personen

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform op of Azure of Amazon Web Services (AWS) aan te sluiten. Voor meer informatie, lees de gids op [ voegend op lijst van gewenste personen IP adressen om met Experience Platform op Azure en AWS ](../../ip-address-allow-list.md) voor meer informatie te verbinden.

### Verifiëren voor Experience Platform in Azure {#azure}

U moet waarden opgeven voor de volgende verificatiereferenties om [!DNL PostgreSQL] te verbinden met Experience Platform on Azure.

>[!BEGINTABS]

>[!TAB  de belangrijkste authentificatie van de Rekening ]

Geef waarden op voor de volgende gebruikersgegevens om uw [!DNL PostgreSQL] -database in Azure te verbinden met Experience Platform via accountsleutelverificatie.

| Credentials | Beschrijving |
| --- | --- |
| `connectionString` | De verbindingstekenreeks die aan uw [!DNL PostgreSQL] account is gekoppeld. Het patroon van de [!DNL PostgreSQL] verbindingstekenreeks is: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}` . |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL PostgreSQL] is `74a1c565-4e59-48d7-9d67-7c03b8a13137` . |

Lees de [[!DNL PostgreSQL]  documentatie ](https://www.postgresql.org/docs/current/) voor meer informatie.

>[!TAB  Basisauthentificatie ]

Geef waarden op voor de volgende gebruikersgegevens om uw [!DNL PostgreSQL] -database met Experience Platform on Azure te verbinden met behulp van basisverificatie.

| Credentials | Beschrijving |
| --- | --- |
| `server` | De naam of het IP-adres van uw [!DNL PostgreSQL] -database. |
| `port` | De TCP-poort van uw [!DNL PostgreSQL] -server. |
| `username` | De gebruikersnaam die is gekoppeld aan uw [!DNL PostgreSQL] -databaseverificatie. |
| `password` | Het wachtwoord dat is gekoppeld aan uw [!DNL PostgreSQL] -databaseverificatie. |
| `database` | De naam van de [!DNL PostgreSQL] -database waarmee u verbinding wilt maken. |
| `sslMode` | De methode [!DNL Secure Sockets Layer] (SSL) die op uw verbinding moet worden toegepast. De beschikbare waarden zijn: <ul><li>`Disable`: Gebruik deze optie om SSL uit te schakelen. Als voor uw server een SSL-configuratie is vereist, mislukt de verbinding.</li><li>`Allow`: gebruik deze optie om SSL-verbindingen toe te staan. Niet-SSL verbindingen kunnen nog worden gebruikt als de server hen steunt.</li><li>`Prefer`: gebruik deze optie om SSL-verbindingen te verkiezen omdat de server deze ondersteunt. Met deze optie kunt u ook niet-SSL-verbindingen maken.</li><li>`Require`: Gebruik deze optie om SSL-verbindingen verplicht te maken. Als de server geen SSL ondersteunt, mislukken de verbindingen.</li><li>`Verify-Ca`: gebruik deze optie om servercertificaten te verifiëren wanneer er geen verbinding is als de server geen SSL ondersteunt.</li><li>`Verify-Full`: gebruik deze optie om servercertificaten met de naam van de host te verifiëren bij een verbroken verbinding als de server geen SSL ondersteunt.</li></ul> |

Lees de [[!DNL PostgreSQL]  documentatie ](https://www.postgresql.org/docs/current/) voor meer informatie.

>[!ENDTABS]

### Verifiëren voor Experience Platform op Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](../../../landing/multi-cloud.md).

Geef waarden op voor de volgende referenties om uw [!DNL PostgreSQL] -database op AWS aan te sluiten op Experience Platform met behulp van basisverificatie.

| Credentials | Beschrijving |
| --- | --- |
| `server` | De naam of het IP-adres van uw [!DNL PostgreSQL] -database. |
| `port` | De TCP-poort van uw [!DNL PostgreSQL] -server. |
| `username` | De gebruikersnaam die is gekoppeld aan uw [!DNL PostgreSQL] -databaseverificatie. |
| `password` | Het wachtwoord dat is gekoppeld aan uw [!DNL PostgreSQL] -databaseverificatie. |
| `database` | De naam van de [!DNL PostgreSQL] -database waarmee u verbinding wilt maken. |
| `sslMode` | De methode [!DNL Secure Sockets Layer] (SSL) die op uw verbinding moet worden toegepast. De beschikbare waarden zijn: <ul><li>`Disable`: Gebruik deze optie om SSL uit te schakelen. Als voor uw server een SSL-configuratie is vereist, mislukt de verbinding.</li><li>`Allow`: gebruik deze optie om SSL-verbindingen toe te staan. Niet-SSL verbindingen kunnen nog worden gebruikt als de server hen steunt.</li><li>`Prefer`: gebruik deze optie om SSL-verbindingen te verkiezen omdat de server deze ondersteunt. Met deze optie kunt u ook niet-SSL-verbindingen maken.</li><li>`Require`: Gebruik deze optie om SSL-verbindingen verplicht te maken. Als de server geen SSL ondersteunt, mislukken de verbindingen.</li><li>`Verify-Ca`: gebruik deze optie om servercertificaten te verifiëren wanneer er geen verbinding is als de server geen SSL ondersteunt.</li><li>`Verify-Full`: gebruik deze optie om servercertificaten met de naam van de host te verifiëren bij een verbroken verbinding als de server geen SSL ondersteunt.</li></ul> |

Lees de [[!DNL PostgreSQL]  documentatie ](https://www.postgresql.org/docs/current/) voor meer informatie.

## Verbinding maken [!DNL PostgreSQL] met Experience Platform via API&#39;s

* [Creeer a [!DNL PostgreSQL]  basisverbinding gebruikend de Dienst API van de Stroom](../../tutorials/api/create/databases/postgres.md)
* [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
* [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbinding maken [!DNL PostgreSQL] met Experience Platform via de gebruikersinterface

* [Creeer a [!DNL PostgreSQL]  bronverbinding in UI](../../tutorials/ui/create/databases/postgres.md)
* [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)
