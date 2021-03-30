---
keywords: Experience Platform;home;populaire onderwerpen;PSQL;psql;PostgreSQL
solution: Experience Platform
title: Een PostSQL-bronverbinding maken in de gebruikersinterface
topic: overzicht
type: Tutorial
description: Leer hoe u een PostSQL-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 8851e11e956b393e56714d4d48870b7f68947c18
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 1%

---


# Een [!DNL PostgreSQL]-bronverbinding maken in de gebruikersinterface

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een [!DNL PostgreSQL] (hierna &quot;PSQL&quot; genoemd) bronconnector met behulp van de [!DNL Platform]-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een geldige verbinding PSQL hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [vormend een dataflow](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw PSQL-account op [!DNL Platform], moet u de volgende waarde opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die aan uw PSQL-account is gekoppeld. Het patroon van de PSQL-verbindingstekenreeks is: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |

Raadpleeg dit [PSQL-document](https://www.postgresql.org/docs/9.2/app-psql.html) voor meer informatie over aan de slag gaan.

## Sluit uw PSQL-account aan

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw PSQL-account te koppelen aan [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Sources]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Sources]** te openen. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL PostgreSQL DB]** onder de categorie **[!UICONTROL Databases]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL Configure]**. Anders, selecteer **[!UICONTROL Add data]** om een nieuwe schakelaar tot stand te brengen PSQL.

![](../../../../images/tutorials/create/psql/catalog.png)

De pagina **[!UICONTROL Connect to PSQL]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, uitgezocht **[!UICONTROL New account]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw PSQL-gegevens op. Wanneer gebeëindigd, selecteer **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding toe om te vestigen.

![](../../../../images/tutorials/create/psql/connect.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de PSQL-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![](../../../../images/tutorials/create/psql/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw PSQL-account tot stand gebracht. U kunt nu doorgaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar [!DNL Platform]](../../dataflow/databases.md).