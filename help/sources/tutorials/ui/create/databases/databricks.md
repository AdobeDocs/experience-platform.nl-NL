---
title: Databases verbinden met Experience Platform via de gebruikersinterface
description: Leer hoe u databases via de gebruikersinterface met Experience Platform kunt verbinden.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
exl-id: 877e22c0-cb77-45bb-88c9-54fdde2d6905
source-git-commit: 6a30e1983a6dcf8e1340281a9385eb8e73b927f6
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 2%

---

# Verbinding maken [!DNL Databricks] met Experience Platform in de gebruikersinterface

>[!AVAILABILITY]
>
>* De [!DNL Databricks] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time CDP Ultimate hebben aangeschaft.
>
>* De bron [!DNL Databricks] is in bèta. Lees de [ termijnen en voorwaarden ](../../../../home.md#terms-and-conditions) in het bronoverzicht voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Lees deze handleiding voor informatie over hoe u uw [!DNL Databricks] -account kunt verbinden met Adobe Experience Platform via de werkruimte voor bronnen in de gebruikersinterface.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Vereiste referenties verzamelen

Geef waarden op voor de volgende referenties om [!DNL Databricks] te verbinden met Experience Platform.

| Credentials | Beschrijving |
| --- | --- |
| Domein | De URL van de [!DNL Databricks] -werkruimte. Bijvoorbeeld `https://adb-1234567890123456.7.azuredatabricks.net` . |
| Cluster-id | De id van uw cluster in [!DNL Databricks] . Deze cluster moet al een bestaande cluster zijn en moet een interactief cluster zijn. |
| Toegangstoken | Het toegangstoken dat uw [!DNL Databricks] account verifieert. U kunt uw toegangstoken produceren gebruikend de [!DNL Databricks] werkruimte. |
| Database | De naam van uw database in het delta-meer. |

Voor meer informatie raadpleegt u het [[!DNL Databricks] overzicht](../../../../connectors/databases/databricks.md).

## Navigeren door de catalogus met bronnen

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van *[!UICONTROL Sources]* . Kies een categorie of gebruik de zoekbalk om de bron te zoeken.

Als u verbinding wilt maken met [!DNL Databricks] , gaat u naar de categorie *[!UICONTROL Databases]* , selecteert u de **[!UICONTROL Azure Databricks]** bronkaart en selecteert u vervolgens **[!UICONTROL Set up]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account is gemaakt, verandert deze optie in **[!UICONTROL Add data]** .

![ de broncatalogus van bronnen met de geselecteerde de bronkaart van Azure Databricks.](../../../../images/tutorials/create/databricks/catalog.png)

### Een bestaande account gebruiken

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en vervolgens de [!DNL Azure Databricks] -account die u wilt gebruiken.

![ de bestaande rekeningeninterface in het bronwerkschema met &quot;Bestaande geselecteerde rekening&quot;.](../../../../images/tutorials/create/databricks/existing.png)

### Een nieuwe account maken

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam en voegt u desgewenst een beschrijving voor uw account toe. Geef vervolgens waarden op voor de volgende verificatiereferenties:

* Domein
* Cluster-id
* Toegangstoken
* Database
* Catalogus

![ de nieuwe rekeningsinterface in het bronwerkschema met een rekeningsnaam en facultatieve verstrekte beschrijving.](../../../../images/tutorials/create/databricks/new.png)

Daarnaast moet u de [!UICONTROL Staging SAS URI] -gegevens kopiëren en in de [!DNL Azure Databricks] -omgeving plakken. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat de verbinding enkele ogenblikken tot stand komen.

![ SAS URI die geloofsbrieven opvoeren.](../../../../images/tutorials/create/databricks/sas-uri.png)

## Een gegevensstroom maken voor [!DNL Azure Databricks] -gegevens

Nu u met succes uw [!DNL Azure Databricks] rekening hebt verbonden, kunt u [ nu tot een dataflow leiden en gegevens van uw gegevensbestand in Experience Platform ](../../dataflow/databases.md) opnemen.
