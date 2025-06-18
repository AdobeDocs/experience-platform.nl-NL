---
title: Overzicht Azure Synapse Analytics Source Connector
description: Leer hoe u Azure Synapse Analytics via API's of de gebruikersinterface kunt verbinden met Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2025-06-17T00:00:00Z
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# [!DNL Azure Synapse Analytics]

>[!IMPORTANT]
>
>De [!DNL Azure Synapse Analytics] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.

[!DNL Azure Synapse Analytics] is een cloudgebaseerde analyseservice die grote gegevens en gegevensopslag verenigt. U kunt gegevens opnemen, verkennen, voorbereiden en analyseren met SQL-, [!DNL Spark] - of real-time hulpprogramma&#39;s - allemaal zonder uw gegevens te verplaatsen.

U kunt de bron van [!DNL Azure Synapse Analytics] gebruiken om uw account te verbinden en uw gegevens naar Adobe Experience Platform te brengen.

## Vereisten {#prerequisites}

Lees de volgende secties om de vereiste instellingen te voltooien voordat u uw [!DNL Azure Synapse Analytics] -account aansluit op Experience Platform.

### IP adres lijst van gewenste personen

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform aan te sluiten. Voor meer informatie, lees de gids op [ voegend op lijst van gewenste personen IP adressen om met Experience Platform ](../../ip-address-allow-list.md) voor meer informatie te verbinden.

### Machtigingen configureren

Als u uw bronaccount wilt verbinden met Experience Platform, moet voor uw account de volgende twee machtigingen zijn ingeschakeld:

* **Bronnen van de Mening**
* **beheert Bronnen**

Als u deze toestemmingen niet hebt, contacteer uw productbeheerder om toegang te verzoeken. Voor meer informatie, lees de [ gids UI van de toegangscontrole ](../../../access-control/ui/overview.md).

### Verifiëren voor Experience Platform

U kunt sleutelverificatie van uw account of service-principal sleutelverificatie gebruiken om uw [!DNL Azure Synapse Analytics] aan te sluiten op Experience Platform.

>[!BEGINTABS]

>[!TAB  de belangrijkste authentificatie van de Rekening ]

Geef waarden op voor de volgende gebruikersgegevens om uw [!DNL Azure Synapse Analytics] -database met accountsleutelverificatie te verbinden met Experience Platform.

| Credentials | Beschrijving |
| --- | --- |
| Verbindingstekenreeks | Dit is het **verbindingskoord** dat voor het voor authentiek verklaren met [!DNL Azure Synapse Analytics] wordt gebruikt. De standaardindeling is: `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30` . U moet de plaatsaanduidingen vervangen door de verbindingsgegevens die u zelf hebt. |
| Verbinding, specificatie-id | **verbindingsspecificatie** verstrekt de schakelaareigenschappen van een gegevensbron. Dit omvat details zoals authentificatiespecificaties en vereisten voor het creëren van zowel **basis** als **bron** verbindingen. Voor [!DNL Azure Synapse Analytics] is de specificatie-id van de verbinding: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` . **Nota:** Deze referentie is slechts noodzakelijk wanneer het verbinden via APIs. |

>[!TAB  de belangrijkste zeer belangrijke authentificatie van de Dienst ]

Om uw geloofsbrieven voor de dienst belangrijkste zeer belangrijke authentificatie terug te winnen, aan [[!DNL Microsfot Entra admin center] ](https://entra.microsoft.com/#home) te navigeren en waarden voor het volgende terug te winnen:

* Toepassings-id
* Weergavenaam
* Geheim
* Tenant-id

Daarna, navigeer aan uw [[!DNL Azure Synapse Analytics]  instantie ](https://azure.microsoft.com/en-ca/products/synapse-analytics) en selecteer dan de optie om een gebruiker van een externe leverancier tot stand te brengen. Van hier, verstrek de aangewezen toestemmingen voor het de diensthoofd op het schema. **NOTA:**: U moet &quot;UITGEZOCHT&quot;omvatten aangezien het voor schemavoorproef, gelijkend op &quot;KOPIE&quot;wordt vereist. Een voorbeeldopdracht kan bijvoorbeeld:

```SQL
GRANT SELECT ON SCHEMA::dbo TO {APP_ID};
```

Geef waarden op voor de volgende referenties om uw [!DNL Azure Synapse Analytics] -database te verbinden met Experience Platform via de service-principal-sleutelverificatie.

| Credentials | Beschrijving |
| --- | --- |
| Server | De volledig gekwalificeerde domeinnaam van het SQL-eindpunt van [!DNL Azure Synapse Analytics] . |
| Database | De naam van de specifieke database in de [!DNL Azure Synapse Analytics] -werkruimte. |
| Aannemer | De [!DNL Azure Active Directory] huurder-id die aan uw [!DNL Azure] -abonnement is gekoppeld. |
| Service principal ID | De client-id van een [!DNL Azure Active Directory] -toepassing. |
| Sleutelsleutel service | Het cliëntgeheim of wachtwoord verbonden aan het de diensthoofd. |
| Verbinding, specificatie-id | **verbindingsspecificatie** verstrekt de schakelaareigenschappen van een gegevensbron. Dit omvat details zoals authentificatiespecificaties en vereisten voor het creëren van zowel **basis** als **bron** verbindingen. Voor [!DNL Azure Synapse Analytics] is de specificatie-id van de verbinding: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` . **Nota:** Deze referentie is slechts noodzakelijk wanneer het verbinden via APIs. |

Voor meer informatie, lees de [[!DNL Azure]  documentatie bij het beheren van identiteiten voor  [!DNL Azure Synapse Analytics] ](https://learn.microsoft.com/en-us/azure/synapse-analytics/synapse-service-identity).

>[!ENDTABS]

## Verbinding maken [!DNL Azure Synapse Analytics] met Experience Platform via API&#39;s

* [Verbind  [!DNL Azure Synapse Analytics]  met Experience Platform gebruikend de Dienst API van de Stroom](../../tutorials/api/create/databases/synapse-analytics.md)
* [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
* [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbinding maken [!DNL Azure Synapse Analytics] met Experience Platform via de gebruikersinterface

* [Verbind  [!DNL Azure Synapse Analytics]  met Experience Platform in UI](../../tutorials/ui/create/databases/synapse-analytics.md)
* [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)

