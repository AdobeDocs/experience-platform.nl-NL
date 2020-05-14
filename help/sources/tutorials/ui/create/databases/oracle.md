---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Oracle DB-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---


# Een Oracle-bronconnector maken in de gebruikersinterface

> [!NOTE]
> De Oracle-connector is in bèta. De functies en documentatie kunnen worden gewijzigd.

De bronschakelaars in het Platform van de Ervaring van Adobe verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een Oracle-bronconnector met behulp van de gebruikersinterface van Platform.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige Oracle DB-verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie over het [configureren van een gegevensstroom](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u toegang wilt tot uw Oracle-account op Platform, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met Oracle. Het Oracle-verbindingspatroon is: `Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>`. |
| `connectionSpec.id` | De unieke id die nodig is om een verbinding te maken. De verbindingsspecificatie-id voor Oracle is `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

Raadpleeg [dit Oracle-document](https://docs.oracle.com/database/121/ODPNT/featConnecting.htm#ODPNT199)voor meer informatie over aan de slag gaan.

## Verbinding maken met uw Oracle-account

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om een nieuwe Oracle-account te maken voor verbinding met Platform.

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte *[!UICONTROL Bronnen]* . Het scherm van de *[!UICONTROL Catalogus]* toont een verscheidenheid van bronnen waarvoor u binnenkomende rekening kunt tot stand brengen, en elke bron toont het aantal bestaande rekeningen en datasetstromen verbonden aan hen.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie *Databases* de optie **[!UICONTROL Oracle DB]** en klik **op het pictogram + (+)** om een nieuwe Oracle-connector te maken.

![catalogus](../../../../images/tutorials/create/oracle/catalog.png)

De pagina *[!UICONTROL Verbinding maken met Oracle DB]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven, de verbinding een naam, een optionele beschrijving en uw Oracle-referenties. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe account enige tijd beginnen.

![verbinden](../../../../images/tutorials/create/oracle/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de Oracle-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/oracle/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw Oracle-account tot stand gebracht. U kunt nu doorgaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens over te brengen naar Platform](../../dataflow/databases.md).