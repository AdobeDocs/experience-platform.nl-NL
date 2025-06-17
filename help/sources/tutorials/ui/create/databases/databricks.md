---
title: Connect Azure-databases naar Experience Platform via de gebruikersinterface
description: Leer hoe u Azure Databricks met Experience Platform kunt verbinden via de gebruikersinterface.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
source-git-commit: 2bd16d5a55c5bbeedbc6a6012d9f0229eee8433a
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Verbinding maken [!DNL Azure Databricks] met Experience Platform in de gebruikersinterface

>[!AVAILABILITY]
>
>* De [!DNL Azure Databricks] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time CDP Ultimate hebben aangeschaft.
>
>* De bron [!DNL Azure Databricks] is in bèta. Lees de [ termijnen en voorwaarden ](../../../../home.md#terms-and-conditions) in het bronoverzicht voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Lees deze handleiding voor informatie over hoe u uw [!DNL Azure Databricks] -account kunt verbinden met Adobe Experience Platform via de werkruimte voor bronnen in de gebruikersinterface.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Vereiste referenties verzamelen

Geef waarden op voor de volgende referenties om [!DNL Azure Databricks] te verbinden met Experience Platform.

| Credentials | Beschrijving |
| --- | --- |
| Domein | De URL van de [!DNL Azure Databricks] -werkruimte. Bijvoorbeeld `https://adb-1234567890123456.7.azuredatabricks.net` . |
| Cluster-id | De id van uw cluster in [!DNL Azure Databricks] . Deze cluster moet al een bestaande cluster zijn en moet een interactief cluster zijn. |
| Toegangstoken | Het toegangstoken dat uw [!DNL Azure Databricks] account verifieert. U kunt uw toegangstoken produceren gebruikend de [!DNL Azure Databricks] werkruimte. |
| Database | De naam van uw database in het delta-meer. |

Voor meer informatie, lees het [[!DNL Azure Databricks]  overzicht ](../../../../connectors/databases/databricks.md).

## Navigeren door de catalogus met bronnen

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van *[!UICONTROL Sources]* . Kies een categorie of gebruik de zoekbalk om de bron te zoeken.

Als u verbinding wilt maken met [!DNL Azure Databricks] , gaat u naar de categorie *[!UICONTROL Databases]* , selecteert u de **[!UICONTROL Azure Databricks]** bronkaart en selecteert u vervolgens **[!UICONTROL Set up]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account is gemaakt, verandert deze optie in **[!UICONTROL Add data]** .

![ de broncatalogus van bronnen met de Azure van Gegevensbestanden geselecteerde bronkaart.](../../../../images/tutorials/create/databricks/catalog.png)

### Een bestaande account gebruiken

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en vervolgens de [!DNL Azure Databricks] -account die u wilt gebruiken.

![ de bestaande rekeningeninterface in het bronwerkschema met &quot;Bestaande geselecteerde rekening&quot;.](../../../../images/tutorials/create/databricks/existing.png)

### Een nieuwe account maken

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam en voegt u desgewenst een beschrijving voor uw account toe. Geef vervolgens waarden op voor de volgende verificatiereferenties:

* Domein
* Cluster-id
* Toegangstoken
* Database

![ de nieuwe rekeningsinterface in het bronwerkschema met een rekeningsnaam en facultatieve verstrekte beschrijving.](../../../../images/tutorials/create/databricks/new.png)

Daarnaast moet u de [!UICONTROL Staging SAS URI] -gegevens kopiëren en in de [!DNL Azure Databricks] -omgeving plakken. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat de verbinding enkele ogenblikken tot stand komen.

![ SAS URI die geloofsbrieven opvoeren.](../../../../images/tutorials/create/databricks/sas-uri.png)

## Een gegevensstroom maken voor [!DNL Azure Databricks] -gegevens

Nu u met succes uw [!DNL Azure Databricks] rekening hebt verbonden, kunt u [ nu tot een dataflow leiden en gegevens van uw gegevensbestand in Experience Platform ](../../dataflow/databases.md) opnemen.
