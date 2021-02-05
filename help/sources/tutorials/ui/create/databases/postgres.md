---
keywords: Experience Platform;home;populaire onderwerpen;PSQL;psql;PostgreSQL
solution: Experience Platform
title: Een PostSQL-bronverbinding maken in de gebruikersinterface
topic: overview
type: Tutorial
description: Leer hoe u een PostSQL-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 1%

---


# Een [!DNL PostgreSQL]-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
> De [!DNL PostgreSQL] schakelaar is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

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

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Bronnen]** te openen. Het scherm **[!UICONTROL Catalog]** toont een verscheidenheid van bronnen waarvoor u een rekening kunt tot stand brengen met.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL PostgreSQL DB]** onder de categorie **[!UICONTROL Databases]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders selecteert u **[!UICONTROL Gegevens toevoegen]** om een nieuwe PSQL-connector te maken.

![](../../../../images/tutorials/create/psql/catalog.png)

De pagina **[!UICONTROL Verbinding maken met PSQL]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, selecteer **[!UICONTROL Nieuwe rekening]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw PSQL-gegevens op. Selecteer **[!UICONTROL Connect]** als u klaar bent en wacht dan enige tijd tot de nieuwe verbinding tot stand is gebracht.

![](../../../../images/tutorials/create/psql/connect.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de PSQL-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![](../../../../images/tutorials/create/psql/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw PSQL-account tot stand gebracht. U kunt nu doorgaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar [!DNL Platform]](../../dataflow/databases.md).