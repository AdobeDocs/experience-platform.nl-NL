---
keywords: Experience Platform;home;populaire onderwerpen;Salesforce Service Cloud;salesforce-servicelolm
solution: Experience Platform
title: Creëer een verbinding van de Bron van de Dienst van Salesforce Cloud in UI
topic: overview
type: Tutorial
description: Leer hoe u een Salesforce Service Cloud-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a0b016e8adc519bc79701f9fd850b6ddf7d46127
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---


# Een [!DNL Salesforce Service Cloud]-bronverbinding maken in de gebruikersinterface

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een [!DNL Salesforce Service Cloud] (hierna &quot;SSC&quot; genoemd) bronconnector met behulp van de [!DNL Platform]-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een geldige verbinding SSC hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [vormend een dataflow](../../dataflow/customer-success.md)

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw SSC-account op [!DNL Platform], moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `username` | De gebruikersnaam voor de gebruikersaccount. |
| `password` | Het wachtwoord voor de gebruikersaccount. |
| `securityToken` | Het beveiligingstoken voor de gebruikersaccount. |

Raadpleeg [this [!DNL Salesforce Service Cloud] document](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm) voor meer informatie over aan de slag gaan.

## Uw [!DNL Salesforce Service Cloud]-account aansluiten

Zodra u uw vereiste geloofsbrieven hebt verzameld, kunt u de stappen volgen hieronder om uw rekening SSC aan [!DNL Platform] te verbinden.

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Sources]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Sources]** te openen. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL Salesforce Service Cloud]** onder de categorie **[!UICONTROL Customer Success]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL Configure]**. Anders, selecteer **[!UICONTROL Add data]** om een nieuwe schakelaar tot stand te brengen SSC.

![catalogus](../../../../images/tutorials/create/ssc/catalog.png)

De pagina **[!UICONTROL Connect to Salesforce Service Cloud]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, uitgezocht **[!UICONTROL New account]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw SSC-referenties op. Wanneer gebeëindigd, selecteer **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding toe om te vestigen.

![verbinden](../../../../images/tutorials/create/ssc/connect.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de SSC-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![bestaand](../../../../images/tutorials/create/ssc/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw SSC-account tot stand gebracht. U kunt nu doorgaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens voor Klantsucces over te brengen naar [!DNL Platform]](../../dataflow/customer-success.md).