---
title: Overzicht MySQL Source Connector
description: Leer hoe u MySQL met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
last-substantial-update: 2025-05-17T00:00:00Z
exl-id: a18e8e69-880f-4bee-b339-726091d6f858
source-git-commit: 7a5dae76c5b58b302b4f3295efc17f40dbb9b18b
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# [!DNL MySQL]

[!DNL MySQL] is een opensource relationeel databasebeheersysteem dat wordt gebruikt om gestructureerde gegevens op te slaan en te beheren. Het organiseert gegevens in lijsten en gebruikt SQL (Gestructureerde Taal van de Vraag) voor het vragen van en het bijwerken van informatie. [!DNL MySQL] wordt op grote schaal gebruikt in webtoepassingen, ondersteunt meerdere platforms en is bekend vanwege de snelheid, betrouwbaarheid en gebruiksgemak. Het is ideaal voor alles, van kleine websites tot grootschalige bedrijfssystemen.

U kunt de [!DNL MySQL] -bron gebruiken om uw account te verbinden en gegevens uit uw [!DNL MySQL] -database in te voeren in Adobe Experience Platform.

## Vereisten {#prerequisites}

Lees de volgende secties om de vereiste instellingen te voltooien voordat u uw [!DNL MySQl] -account aansluit op Experience Platform.

### IP adres lijst van gewenste personen

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform op of Azure of Amazon Web Services (AWS) aan te sluiten. Voor meer informatie, lees de gids op [ voegend op lijst van gewenste personen IP adressen om met Experience Platform op Azure en AWS ](../../ip-address-allow-list.md) voor meer informatie te verbinden.

### Verifiëren voor Experience Platform in Azure {#azure}

U kunt verificatie met accountsleutels of basisverificatie gebruiken om uw [!DNL MySQL] -database te verbinden met Experience Platform on Azure.

>[!BEGINTABS]

>[!TAB  de belangrijkste authentificatie van de Rekening ]

Geef waarden op voor de volgende gebruikersgegevens om uw [!DNL MySQL] -database met accountsleutelverificatie te verbinden met Experience Platform.

| Credentials | Beschrijving |
| --- | --- |
| `connectionString` | De [!DNL MySQL] verbindingstekenreeks die aan uw account is gekoppeld. Het patroon van de [!DNL MySQL] verbindingstekenreeks is: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` . |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecs met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL MySQL] is `26d738e0-8963-47ea-aadf-c60de735468a` . |

Voor meer informatie, lees de [[!DNL MySQL]  documentatie over verbindingskoorden ](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html).

>[!TAB  Basisauthentificatie ]

Geef waarden op voor de volgende referenties om uw [!DNL MySQL] -database te verbinden met Experience Platform met behulp van basisverificatie.

| Credentials | Beschrijving |
| --- | --- |
| `server` | De naam of het IP-adres van uw [!DNL MySQL] -database. |
| `database` | De naam van de [!DNL MySQL] -database waarmee u verbinding wilt maken. |
| `username` | De gebruikersnaam die is gekoppeld aan uw [!DNL MySQL] -databaseverificatie. |
| `password` | Het wachtwoord dat is gekoppeld aan uw [!DNL MySQL] -databaseverificatie. |
| `sslMode` | De methode [!DNL Secure Sockets Layer] (SSL) die op uw verbinding moet worden toegepast. De beschikbare waarden zijn: <ul><li>`DISABLED`: Gebruik deze optie om SSL uit te schakelen. Als uw server een SSL-configuratie vereist, mislukt de verbinding</li><li>`PREFERRED`: gebruik deze optie om SSL-verbindingen te verkiezen omdat de server deze ondersteunt. Met deze optie kunt u ook niet-SSL-verbindingen maken.</li><li>`REQUIRED`: Gebruik deze optie om SSL-verbindingen verplicht te maken. Als de server geen SSL ondersteunt, mislukken de verbindingen.</li><li>`Verify-Ca`: gebruik deze optie om servercertificaten te verifiëren wanneer er geen verbinding is als de server geen SSL ondersteunt.</li><li>`Verify Identity`: gebruik deze optie om servercertificaten met de naam van de host te verifiëren bij een verbroken verbinding als de server geen SSL ondersteunt.</li></ul> |

>[!ENDTABS]

## Verbinding maken [!DNL MySQL] met Experience Platform via API&#39;s

- [Verbind uw  [!DNL MySQL]  gegevensbestand gebruikend de Dienst API van de Stroom](../../tutorials/api/create/databases/mysql.md)
- [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
- [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## MySQL verbinden met Experience Platform via de gebruikersinterface

- [Verbind uw  [!DNL MySQL]  gegevensbestand met Experience Platform gebruikend UI](../../tutorials/ui/create/databases/mysql.md)
- [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)
