---
title: Databricks
description: Leer over de noodzakelijke stappen nodig om Gegevensbestanden aan Experience Platform te verbinden.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
last-substantial-update: 2025-06-17T00:00:00Z
exl-id: 2f082898-aa0e-47a1-a4bf-077c21afdfee
source-git-commit: 96e395e3b3d977d7eb04c400f6fd290977bf1101
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# [!DNL Databricks]

>[!AVAILABILITY]
>
>* De [!DNL Databricks] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time CDP Ultimate hebben aangeschaft.
>
>* De bron [!DNL Databricks] is in bèta. Lees de [&#x200B; termijnen en voorwaarden &#x200B;](../../home.md#terms-and-conditions) in het bronoverzicht voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

[!DNL Databricks] is een op de cloud gebaseerd platform dat is ontworpen voor gegevensanalyse, leren van machines en AI. U kunt [!DNL Databricks] gebruiken om een holistische omgeving te integreren en te verstrekken voor het bouwen, implementeren en beheren van gegevensoplossingen op schaal.

Gebruik de [!DNL Databricks] -bron om uw account te verbinden en uw [!DNL Databricks] -gegevens in te voeren op Adobe Experience Platform.

## Vereisten

Voer de vereiste stappen uit om uw [!DNL Databricks] -account met Experience Platform te verbinden.

### De gegevens van de container ophalen

Haal uw Experience Platform [!DNL Azure Blob Storage] -gegevens op zodat uw [!DNL Databricks] -account deze later kan openen.

Als u uw referenties wilt ophalen, vraagt u GET het `/credentials` -eindpunt van de [!DNL Connectors] API aan.

**API formaat**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source
```

**Verzoek**

Met het volgende verzoek worden de gegevens voor uw Experience Platform [!DNL Azure Blob Storage] opgehaald.

+++Voorbeeld van een aanvraag weergeven

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Reactie**

Een succesvol antwoord biedt uw referenties ( `containerName` , `SASToken` , `storageAccountName` ) voor toekomstig gebruik in [!DNL Apache Spark] configuration for [!DNL Databricks] .

+++Reactievoorbeeld weergeven

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "expiryDate": "2025-07-05"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `containerName` | De naam van de [!DNL Azure Blob Storage] -container. Deze waarde wordt later gebruikt wanneer u de [!DNL Apache Spark] -configuratie voor [!DNL Databricks] voltooit. |
| `SASToken` | Het token voor gedeelde toegangshandtekeningen voor uw [!DNL Azure Blob Storage] . Deze tekenreeks bevat alle informatie die nodig is om een aanvraag te autoriseren. |
| `storageAccountName` | De naam van uw opslagaccount. |
| `SASUri` | De URI voor de gedeelde toegangshandtekening voor uw [!DNL Azure Blob Storage] . Deze tekenreeks is een combinatie van de URI naar de [!DNL Azure Blob Storage] waarnaar u wordt geverifieerd en de bijbehorende SAS-token. |
| `expiryDate` | De datum waarop uw SAS-token verloopt. U moet uw token vernieuwen vóór de vervaldatum om deze te kunnen blijven gebruiken in uw toepassing voor het uploaden van gegevens naar de [!DNL Azure Blob Storage] . Als u uw token niet handmatig vernieuwt vóór de opgegeven vervaldatum, wordt deze automatisch vernieuwd en wordt er een nieuw token weergegeven wanneer de aanroep van de GET-gebruikersgegevens wordt uitgevoerd. |

+++

### Uw referenties vernieuwen

>[!NOTE]
>
>Uw bestaande referenties worden ingetrokken zodra u uw gegevens vernieuwt. Daarom moet u uw [!DNL Spark] configuraties dienovereenkomstig bijwerken wanneer u uw opslaggeloofsbrieven vernieuwt. Anders mislukt de gegevensstroom.

Als u uw referenties wilt vernieuwen, moet u een POST-aanvraag indienen en `action=refresh` opnemen als een queryparameter.

**API formaat**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh
```

**Verzoek**

In het volgende verzoek worden de referenties voor uw [!DNL Azure Blob Storage] vernieuwd.

+++Voorbeeld van een aanvraag weergeven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Reactie**

Met een succesvol antwoord worden uw nieuwe referenties geretourneerd.

+++Reactievoorbeeld weergeven

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "expiryDate": "2025-07-20"
}
```

+++

### Toegang tot uw [!DNL Azure Blob Storage] configureren

>[!IMPORTANT]
>
>* Als uw cluster is beëindigd, zal de dienst automatisch het tijdens een stroomlooppas opnieuw beginnen. U moet er echter voor zorgen dat uw cluster actief is wanneer u een verbinding of een gegevensstroom maakt. Bovendien moet uw cluster actief zijn als u handelingen uitvoert zoals gegevensvoorvertoning of exploratie, aangezien deze handelingen niet tot gevolg kunnen hebben dat een afgesloten cluster automatisch opnieuw wordt opgestart.
>
>* De [!DNL Azure] -container bevat een map met de naam `adobe-managed-staging` . Om de naadloze opname van gegevens te verzekeren, **wijzigt** deze omslag niet.


Vervolgens moet u ervoor zorgen dat uw [!DNL Databricks] -cluster toegang heeft tot de Experience Platform [!DNL Azure Blob Storage] -account. Hierbij kunt u [!DNL Azure Blob Storage] gebruiken als tussentijdse locatie voor het schrijven van [!DNL delta lake] -tabelgegevens.

Als u toegang wilt bieden, moet u een SAS-token configureren in de [!DNL Databricks] -cluster als onderdeel van uw [!DNL Apache Spark] -configuratie.

Selecteer [!DNL Databricks] in de interface van **[!DNL Advanced options]** en voer vervolgens het volgende in het invoervak [!DNL Spark config] in.

```shell
fs.azure.sas.{CONTAINER_NAME}.{STORAGE-ACCOUNT}.blob.core.windows.net {SAS-TOKEN}
```

| Eigenschap | Beschrijving |
| --- | --- |
| Containernaam | De naam van de container. U kunt deze waarde verkrijgen door uw [!DNL Azure Blob Storage] -gegevens op te halen. |
| Opslagaccount | De naam van uw opslagaccount. U kunt deze waarde verkrijgen door uw [!DNL Azure Blob Storage] -gegevens op te halen. |
| SAS-token | Het token voor gedeelde toegangshandtekeningen voor uw [!DNL Azure Blob Storage] . U kunt deze waarde verkrijgen door uw [!DNL Azure Blob Storage] -gegevens op te halen. |

![&#x200B; de Databases UI op Azure.](../../images/tutorials/create/databricks/databricks-ui.png)

Als deze niet is opgegeven, mislukt de kopieeractiviteit in de flowuitvoering en wordt de volgende fout geretourneerd:

```shell
Unable to access container '{CONTAINER_NAME}' in account '{STORAGE_ACCOUNT}.blob.core.windows.net' using anonymous credentials. No credentials found in the configuration. Public access is not permitted on this storage account.
```

## Verbinden [!DNL Databricks] met Experience Platform

Nu u de vereiste stappen hebt uitgevoerd, kunt u nu doorgaan en uw [!DNL Databricks] -account verbinden met Experience Platform:

* [Verbinding maken via de API](../../tutorials/api/create/databases/databricks.md)
* [Verbind door de bronwerkruimte in UI](../../tutorials/ui/create/databases/databricks.md)
