---
keywords: Experience Platform;home;populaire onderwerpen;salesforce marketing cloud;Salesforce Marketing Clud
solution: Experience Platform
title: Creeer een Verbinding van de Bron van de Marketing Cloud Salesforce in UI
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Salesforce-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
source-git-commit: f196da32f67578ad1d73f3200f6050a7ddab0d88
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 1%

---

# Een [!DNL Salesforce Marketing Cloud]-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
> De bron [!DNL Salesforce Marketing Cloud] is in bèta. Zie [Bronnen overzicht](../../../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bèta-geëtiketteerde bronnen.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Salesforce Marketing Cloud]-bronconnector met behulp van de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een [!DNL Salesforce Marketing Cloud] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [vormend een dataflow](../../dataflow/marketing-automation.md).

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL Salesforce Marketing Cloud]-account op Platform, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De hostserver van uw toepassing. Dit is vaak uw subdomein. |
| `clientId` | De client-id die is gekoppeld aan uw [!DNL Salesforce Marketing Cloud]-toepassing. |
| `clientSecret` | Het clientgeheim dat is gekoppeld aan uw [!DNL Salesforce Marketing Cloud]-toepassing. |

Raadpleeg dit [[!DNL Salesforce Marketing Cloud] document](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm) voor meer informatie over aan de slag gaan.

## Uw [!DNL Salesforce Marketing Cloud]-account aansluiten

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Salesforce Marketing Cloud]-account te koppelen aan het Platform.

Selecteer **[!UICONTROL Sources]** in de gebruikersinterface van het Platform in de linkernavigatie om de werkruimte [!UICONTROL Sources] te openen. In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt de onderzoeksbar ook gebruiken om onderaan de getoonde schakelaars te versmallen.

Selecteer [!UICONTROL Marketing automation] onder de categorie **[!UICONTROL Salesforce Marketing Cloud]** en selecteer **[!UICONTROL Set up]**.

![catalogus](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

De pagina **[!UICONTROL Connect to Salesforce Marketing Cloud]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, uitgezocht **[!UICONTROL New account]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Salesforce Marketing Cloud]-referenties op. Wanneer gebeëindigd, selecteer **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding toe om te vestigen.

![new](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Salesforce Marketing Cloud]-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![bestaand](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Salesforce Marketing Cloud]-account. U kunt nu doorgaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens van het marketingautomatiseringssysteem over te brengen naar Platform](../../dataflow/marketing-automation.md).
