---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Azure Data Explorer-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---


# Een Azure Data Explorer-bronconnector maken in de gebruikersinterface

> [!NOTE]
> De Azure Data Explorer-connector is in bèta. De functies en documentatie kunnen worden gewijzigd.

De bronschakelaars in het Platform van de Ervaring van Adobe verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een Azure Data Explorer-bronconnector (hierna &quot;Data Explorer&quot; genoemd) via de gebruikersinterface van Platform.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige verbinding van de Ontdekkingsreiziger van Gegevens hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een gegevensstroom](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u toegang wilt tot uw gegevensverkenner-account op Platform, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `endpoint` | Het eindpunt van de server van de Ontdekkingsreiziger van Gegevens. |
| `database` | De naam van de gegevensverkenner-database. |
| `tenant` | De unieke huurder-id die wordt gebruikt om verbinding te maken met de gegevensverkenner-database. |
| `servicePrincipalId` | De unieke dienst belangrijkste identiteitskaart die wordt gebruikt om met het gegevensbestand van de Ontdekkingsreiziger van Gegevens te verbinden. |
| `servicePrincipalKey` | De unieke de dienstbelangrijkste sleutel die wordt gebruikt om met het gegevensbestand van de Ontdekkingsreiziger van Gegevens te verbinden. |

Voor meer informatie over begonnen worden verwijs naar [dit document](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)van de Ontdekkingsreiziger van Gegevens.

## Uw Azure Data Explorer-account verbinden

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om een nieuwe gegevensverkenner-account te maken waarmee u verbinding kunt maken met Platform.

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte *Bronnen* . Het scherm van de *[!UICONTROL Catalogus]* toont een verscheidenheid van bronnen waarvoor u binnenkomende rekening kunt tot stand brengen, en elke bron toont het aantal bestaande rekeningen en datasetstromen verbonden aan hen.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie *[!UICONTROL Databases]* de optie **[!UICONTROL Azure Data Explorer]** en klik **op het pictogram + (+)** om een nieuwe Data Explorer-connector te maken.

![catalogus](../../../../images/tutorials/create/data-explorer/catalog.png)

De pagina *[!UICONTROL Connect to Azure Data Explorer]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven, de verbinding een naam, een optionele beschrijving en uw gegevens voor de gegevensverkenner. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe account enige tijd beginnen.

![verbinden](../../../../images/tutorials/create/data-explorer/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de gegevensverkenner-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/data-explorer/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw gegevensverkenner-account. U kunt nu doorgaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens over te brengen naar Platform](../../dataflow/databases.md).