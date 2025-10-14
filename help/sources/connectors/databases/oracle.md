---
title: Overzicht Oracle DB Source Connector
description: Leer hoe u Oracle met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
last-substantial-update: 2025-08-06T00:00:00Z
exl-id: be422cf8-fb24-48c7-8369-34f0f2ec95fc
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# [!DNL Oracle DB]

[!DNL Oracle DB] is een krachtig relationeel databasebeheersysteem dat is ontwikkeld door [!DNL Oracle Corporation] . Met [!DNL Oracle DB] kunt u grote volumes gestructureerde gegevens efficiënt en veilig opslaan, beheren en ophalen.

Gebruik de [!DNL Oracle DB] -bron in de Adobe Experience Platform-broncatalogus om uw database te verbinden en gegevens in te voeren in Experience Platform.

## Vereisten {#prerequisites}

Lees de volgende secties om de vereiste instellingen te voltooien voordat u uw [!DNL Oracle DB] -account aansluit op Experience Platform.

### IP adres lijst van gewenste personen

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform op of Azure of Amazon Web Services (AWS) aan te sluiten. Voor meer informatie, lees de gids op [&#x200B; voegend op lijst van gewenste personen IP adressen om met Experience Platform op Azure en AWS &#x200B;](../../ip-address-allow-list.md) voor meer informatie te verbinden.

### Verifiëren voor Experience Platform in Azure {#azure}

Geef een verbindingstekenreeks op om uw [!DNL Oracle DB] -account te verifiëren en aan te sluiten op Experience Platform on Azure.

| Credentials | Beschrijving |
| --- | --- |
| Verbindingstekenreeks | Een verbindingstekenreeks is een tekenreeks die wordt gebruikt door toepassingen om verbinding te maken met een database. Het patroon van de [!DNL Oracle DB] verbindingstekenreeks is: `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}` . |
| Verbinding, specificatie-id | De verbindingsSPC identiteitskaart keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecs op het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Oracle] is `d6b52d86-f0f8-475f-89d4-ce54c8527328` . **Nota**: Deze referentie wordt slechts vereist wanneer het verbinden door [!DNL Flow Service] API. |

### Verifiëren voor Experience Platform op Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [&#x200B; multi-wolkenoverzicht van Experience Platform &#x200B;](../../../landing/multi-cloud.md).

Geef waarden op voor de volgende referenties om uw [!DNL Oracle DB] -account te verifiëren en aan te sluiten op Experience Platform op AWS.

| Credentials | Beschrijving |
| --- | --- |
| Server | Het IP-adres of hostmodel van de [!DNL Oracle DB] -server. |
| Poort | Het poortnummer van de databaseserver. Het standaardpoortnummer is `1521` . |
| Gebruikersnaam | Het [!DNL Oracle DB] -gebruikersaccount dat wordt gebruikt voor verificatie en toegang tot de database. |
| Wachtwoord | De geheime sleutel verbonden aan uw gebruikersbenaming, die voor authentificatie wordt gebruikt. |
| Database | De specifieke [!DNL Oracle] database-instantie waarmee u verbinding wilt maken. |
| Schema | De container voor databaseobjecten, zoals tabellen, weergaven of procedures. |
| SSL-modus | Een booleaanse waarde die bepaalt of SSL wordt afgedwongen of niet. Deze configuratie is afhankelijk van uw serverondersteuning en is standaard ingesteld op `false` . |
| Verbinding, specificatie-id | De verbindingsSPC identiteitskaart keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecs op het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Oracle] is `d6b52d86-f0f8-475f-89d4-ce54c8527328` . **Nota**: Deze referentie wordt slechts vereist wanneer het verbinden door [!DNL Flow Service] API. |


## Verbind [!DNL Oracle] met [!DNL Experience Platform] gebruikend APIs

- [Connect Oracle DB met behulp van de Flow Service API](../../tutorials/api/create/databases/oracle.md)
- [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
- [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbind [!DNL Oracle] met [!DNL Experience Platform] gebruikend UI

- [Verbind Oracle DB gebruikend de werkruimte van de UI van Experience Platform.](../../tutorials/ui/create/databases/oracle.md)
- [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)
