---
keywords: Experience Platform;home;populaire onderwerpen;Salesforce Service Cloud;salesforce-servicelolm
solution: Experience Platform
title: Creëer een verbinding van de Bron van de Dienst van Salesforce Cloud in UI
topic: overview
type: Tutorial
description: Leer hoe u een Salesforce Service Cloud-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# Een [!DNL Salesforce Service Cloud]-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
>De [!DNL Salesforce Service Cloud] schakelaar is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

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

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Bronnen]** te openen. Het scherm **[!UICONTROL Catalog]** toont een verscheidenheid van bronnen waarvoor u een rekening kunt tot stand brengen met.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL Salesforce Service Cloud]** onder de categorie **[!UICONTROL Klantsucces]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders, uitgezocht **[!UICONTROL voeg gegevens]** toe om een nieuwe schakelaar tot stand te brengen SSC.

![catalogus](../../../../images/tutorials/create/ssc/catalog.png)

De pagina **[!UICONTROL Verbinding maken met de Salesforce Service Cloud]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, selecteer **[!UICONTROL Nieuwe rekening]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw SSC-referenties op. Selecteer **[!UICONTROL Connect]** als u klaar bent en wacht dan enige tijd tot de nieuwe verbinding tot stand is gebracht.

![verbinden](../../../../images/tutorials/create/ssc/connect.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de SSC-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/ssc/existing.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding met uw SSC-account tot stand gebracht. U kunt nu doorgaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens voor Klantsucces over te brengen naar [!DNL Platform]](../../dataflow/customer-success.md).