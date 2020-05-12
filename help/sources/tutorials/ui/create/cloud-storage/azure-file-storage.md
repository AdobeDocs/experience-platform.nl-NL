---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Azure File Storage-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: aa1c6cb0f5702cfe444cb2046e4460e404f13e57
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# Een Azure File Storage-bronconnector maken in de gebruikersinterface

De bronschakelaars in het Platform van de Ervaring van Adobe verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het verifiëren van een Azure File Storage-bronconnector met behulp van de Platform-gebruikersinterface.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

- [XDM-systeem](../../../../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [Klantprofiel](../../../../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een verbinding van de Opslag van het Dossier hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan bij het [vormen van een gegevensstroom](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Om uw Azure-bronconnector voor bestandsopslag te verifiëren, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het eindpunt van de Azure File Storage-instantie waartoe u toegang hebt. |
| `userId` | De gebruiker met voldoende toegang tot het Azure eindpunt van de Opslag van het Dossier. |
| `password` | De Azure File Storage-toegangssleutel. |

Raadpleeg [dit Azure File Storage-document](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)voor meer informatie over hoe u aan de slag gaat.

## Verbind uw Azure File Storage-account

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om een nieuwe Azure File Storage-account te maken waarmee u verbinding kunt maken met Platform.

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte *[!UICONTROL Bronnen]* . In het scherm *[!UICONTROL Catalogus]* worden diverse bronnen weergegeven waarmee u een binnenkomende account kunt maken. Elke bron toont het aantal bestaande accounts en gegevensstromen dat aan deze accounts is gekoppeld.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie *[!UICONTROL Databases]* de optie **[!UICONTROL Azure File Storage]** ( **Azure-bestandsopslag)** op het plus-pictogram (+)om een nieuwe Azure File Storage-connector te maken.

![catalogus](../../../../images/tutorials/create/azure-file-storage/catalog.png)

De pagina *[!UICONTROL Connect to Azure File Storage]* wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven, de verbinding een naam, een optionele beschrijving en de gegevens voor de bestandsopslag op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe account enige tijd beginnen.

![verbinden](../../../../images/tutorials/create/azure-file-storage/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de Azure File Storage-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![bestaand](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw Azure File Storage-account. U kunt nu verdergaan met de volgende zelfstudie en een gegevensstroom [configureren om gegevens van uw cloudopslag over te brengen naar Platform](../../dataflow/batch/cloud-storage.md).