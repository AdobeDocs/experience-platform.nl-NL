---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Microsoft SQL Server-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# Creeer een [!DNL Microsoft] SQL de bronschakelaar van de Server in UI

> [!NOTE]
> De [!DNL Microsoft] SQL schakelaar van de Server is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om extern gesourceerde gegevens op een geplande basis in te voeren. Dit leerprogramma verstrekt stappen voor het creëren van een [!DNL Microsoft] SQL van de Server (hierna genoemd &quot;SQL Server&quot;) bronschakelaar gebruikend het [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een SQL de basisverbinding van de Server hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een dataflow](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u verbinding wilt maken met SQL Server [!DNL Platform], moet u de volgende verbindingseigenschap opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die is gekoppeld aan uw SQL Server-account. Het patroon van de SQL-serververbindingstekenreeks is: `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |

Gelieve te verwijzen naar [dit document](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server) voor meer informatie over het worden begonnen met SQL Server.

## Uw SQL Server-account verbinden

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen hieronder volgen om een nieuwe binnenkomende basisverbinding tot stand te brengen om uw SQL rekening van de Server aan te verbinden [!DNL Platform].

Login aan <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> en selecteer dan **[!UICONTROL Bronnen]** van de linkernavigatiebar om tot de werkruimte van *[!UICONTROL Bronnen]* toegang te hebben. In het scherm *[!UICONTROL Catalogus]* worden diverse bronnen weergegeven waarvoor u binnenkomende basisverbindingen kunt maken met. Elke bron toont het aantal bestaande basisverbindingen dat aan deze verbindingen is gekoppeld.

Onder de categorie *[!UICONTROL Databases]* selecteert u **[!UICONTROL Microsoft SQL Server]** om een informatiebalk aan de rechterkant van het scherm weer te geven. De informatiebalk bevat een korte beschrijving van de geselecteerde bron en opties voor het maken van verbinding met de bron of het bekijken van de documentatie. Selecteer **[!UICONTROL Connect-bron]** als u een nieuwe binnenkomende basisverbinding wilt maken.

![](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

De pagina *[!UICONTROL Verbinding maken met Microsoft SQL Server]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Voor de inputvorm die verschijnt, verstrek de basisverbinding met een naam, een facultatieve beschrijving, en uw SQL geloofsbrieven van de Server. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe basisverbinding enige tijd tot stand brengen.

![](../../../../images/tutorials/create/microsoft-sql-server/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de SQL Server-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

## Volgende stappen

Door dit leerprogramma te volgen, hebt u een basisverbinding aan uw SQL rekening van de Server gevestigd. U kunt nu verdergaan aan het volgende leerprogramma en een dataflow [vormen om gegevens in Platform](../../dataflow/databases.md)te brengen.