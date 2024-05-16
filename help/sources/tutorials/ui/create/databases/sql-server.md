---
title: Een Microsoft SQL Server-bronverbinding maken in de gebruikersinterface
description: Leer hoe u een Microsoft SQL Server-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 1%

---

# Een [!DNL Microsoft SQL Server] bronverbinding in de gebruikersinterface

Lees deze zelfstudie om te leren hoe u verbinding kunt maken met uw [!DNL Microsoft SQL Server] met de gebruikersinterface naar Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u al een geldige [!DNL SQL Server] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u verbinding wilt maken met [!DNL SQL Server] op [!DNL Platform]moet u de volgende eigenschap voor de verbinding opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Verbindingstekenreeks | De verbindingstekenreeks die aan uw [!DNL Microsoft SQL Server] account. Het patroon van de verbindingstekenreeks is afhankelijk van de servernaam of de instantienaam van de gegevensbron:<ul><li>Verbindingstekenreeks met servernaam: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Verbindingstekenreeks met instantienaam:`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |

Raadpleeg voor meer informatie over aan de slag gaan [dit [!DNL SQL Server] document](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## Verbind uw [!DNL SQL Server] account

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de *Databases* categorie, selecteert u **[!DNL Microsoft SQL Server]** en selecteer vervolgens **[!UICONTROL Set up]**.

>[!TIP]
>
>De bronnen in de broncatalogus geven de **[!UICONTROL Set up]** als een bepaalde bron nog geen geverifieerde account heeft. Als er eenmaal een geverifieerd account is, wordt deze optie gewijzigd in **[!UICONTROL Add data]**.

![De broncatalogus met de Microsoft SQL Server-bron geselecteerd.](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

De **[!UICONTROL Connect to Microsoft SQL Server]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

>[!BEGINTABS]

>[!TAB Een nieuwe account maken]

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geef een naam, een optionele beschrijving en uw referenties op.

Selecteer **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![De nieuwe accountinterface met de ingevoerde en gemarkeerde bronverbindingsgegevens.](../../../../images/tutorials/create/microsoft-sql-server/new.png)

>[!TAB Een bestaande account gebruiken]

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en selecteer vervolgens de account die u wilt gebruiken in de bestaande accountcatalogus.

Selecteren **[!UICONTROL Next]** om verder te gaan.

![De bestaande accountinterface die een lijst met bestaande accounts weergeeft.](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL SQL Server] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar [!DNL Platform]](../../dataflow/databases.md).
