---
title: Een Microsoft SQL Server Source Connection maken in de gebruikersinterface
description: Leer hoe u een Microsoft SQL Server-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# Een [!DNL Microsoft SQL Server] bronverbinding maken in de gebruikersinterface

Lees deze zelfstudie om te leren hoe u uw [!DNL Microsoft SQL Server] -account kunt verbinden met Adobe Experience Platform via de gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL SQL Server] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [&#x200B; vormend een dataflow &#x200B;](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u verbinding wilt maken met [!DNL SQL Server] on [!DNL Experience Platform] , moet u de volgende eigenschap voor verbinding opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Verbindingstekenreeks | De verbindingstekenreeks die aan uw [!DNL Microsoft SQL Server] account is gekoppeld. Het patroon van de verbindingstekenreeks is afhankelijk van de servernaam of de instantienaam van de gegevensbron:<ul><li>Verbindingstekenreeks met servernaam: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Verbindingstekenreeks met instantienaam: `Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` <br> `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` </li></ul> |

Voor meer informatie over begonnen worden, verwijs naar [&#x200B; dit  [!DNL SQL Server]  document &#x200B;](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## Sluit uw [!DNL SQL Server] -account aan

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de *categorie van Gegevensbestanden*, selecteer **[!DNL Microsoft SQL Server]**, en selecteer dan **[!UICONTROL Set up]**.

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account bestaat, verandert deze optie in **[!UICONTROL Add data]** .

![&#x200B; de broncatalogus met de Bron van de Server van Microsoft SQL selecteerde.](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

De pagina **[!UICONTROL Connect to Microsoft SQL Server]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

>[!BEGINTABS]

>[!TAB  creeer een nieuwe rekening ]

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam, een optionele beschrijving en uw referenties op.

Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![&#x200B; de nieuwe rekeningsinterface met de ingevoerde en benadrukte gegevens van de bronverbinding.](../../../../images/tutorials/create/microsoft-sql-server/new.png)

>[!TAB  Gebruik een bestaande rekening ]

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en selecteert u vervolgens de account die u wilt gebruiken in de bestaande accountcatalogus.

Selecteer **[!UICONTROL Next]** om door te gaan.

![&#x200B; de bestaande rekeningsinterface die een lijst van de bestaande rekeningen toont.](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL SQL Server] -account. U kunt nu aan het volgende leerprogramma verdergaan en [&#x200B; een dataflow vormen om gegevens in  [!DNL Experience Platform]](../../dataflow/databases.md) te brengen.
