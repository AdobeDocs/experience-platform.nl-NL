---
keywords: Experience Platform;home;populaire onderwerpen;Maria DB;maria db
solution: Experience Platform
title: Een MariaDB Source-verbinding maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een Maria DB-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 259ca112-01f1-414a-bf9f-d94caf4c69df
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# Een [!DNL MariaDB] bronverbinding maken in de gebruikersinterface

Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het maken van een Maria DB-bronconnector met behulp van de gebruikersinterface van [!DNL Experience Platform] .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [ Real-Time Profiel van de Klant ](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een [!DNL MariaDB] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL MariaDB] account op [!DNL Experience Platform] , moet u de volgende waarde opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die aan uw MariaDB-verificatie is gekoppeld. Het patroon van de [!DNL MariaDB] verbindingstekenreeks is: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` . |

Voor meer informatie over begonnen worden, verwijs naar dit [[!DNL MariaDB]  document ](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

## Sluit uw [!DNL Maria DB] -account aan

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL Maria DB] -account te koppelen aan [!DNL Experience Platform] .

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

Selecteer onder de categorie **[!UICONTROL Databases]** de optie **[!UICONTROL Maria DB]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe [!DNL Maria DB] -connector te maken.

![](../../../../images/tutorials/create/maria-db/catalog.png)

De pagina **[!UICONTROL Connect to Maria DB]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL MariaDB] -gegevens op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![](../../../../images/tutorials/create/maria-db/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL MariaDB] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![](../../../../images/tutorials/create/maria-db/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL MariaDB] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in  [!DNL Experience Platform]](../../dataflow/databases.md) te brengen.
