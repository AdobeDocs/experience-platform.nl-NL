---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creeer een GreenPlum bronschakelaar in UI
topic: overview
translation-type: tm+mt
source-git-commit: a015d2612bc5a72004e15dc5706c7718617a0af4
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---


# Creeer een GreenPlum bronschakelaar in UI

> [!NOTE]
> De GreenPlum-connector is in bèta. De functies en documentatie kunnen worden gewijzigd.

De bronschakelaars in het Platform van de Ervaring van Adobe verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een GreenPlum-bronconnector met behulp van de gebruikersinterface van Platform.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een geldige verbinding GreenPlum hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een gegevensstroom](../../dataflow/databases.md).

### Vereiste referenties verzamelen

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes met GreenPlum gebruikend de Dienst API van de Stroom te verbinden.

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met uw instantie GreenPlum. Het patroon van de verbindingstekenreeks voor GreenPlum is `HOST=<server>;PORT=<port>;DB=<database>;UID=<user name>;PWD=<password>` |

Raadpleeg [dit GreenPlum-document](https://gpdb.docs.pivotal.io/580/security-guide/topics/Authenticate.html#topic_fzv_wb2_jr__config_ssl_client_conn)voor meer informatie over aan de slag gaan.

## Maak verbinding met uw GreenPlum-account

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen volgen hieronder om een nieuw rekening te creëren GreenPlum om met Platform te verbinden.

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte *[!UICONTROL Bronnen]* . Het scherm van de *[!UICONTROL Catalogus]* toont een verscheidenheid van bronnen waarvoor u een binnenkomende rekening met kunt tot stand brengen, en elke bron toont het aantal bestaande rekeningen en datasetstromen verbonden aan hen.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de categorie *[!UICONTROL Databases]* selecteert u de optie **[!UICONTROL GreenPlum]** en klikt u **op het pictogram + (+)** om een nieuwe aansluiting GreenPlum te maken.

![catalogus](../../../../images/tutorials/create/greenplum/catalog.png)

De pagina *[!UICONTROL Verbinding maken met GreenPlum]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Geef op het invoerformulier dat wordt weergegeven, de verbinding een naam, een optionele beschrijving en uw GreenPlum-referenties. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe account enige tijd beginnen.

![verbinden](../../../../images/tutorials/create/greenplum/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u het GreenPlum-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** in de rechterbovenhoek om door te gaan.

![bestaand](../../../../images/tutorials/create/greenplum/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw GreenPlum-account tot stand gebracht. U kunt nu doorgaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens over te brengen naar Platform](../../dataflow/databases.md).