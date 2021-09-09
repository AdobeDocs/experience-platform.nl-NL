---
keywords: Experience Platform;thuis;populaire onderwerpen;Veeva CRM;veeva
solution: Experience Platform
title: Een Veeva CRM-bronverbinding maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Veeva CRM-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 1%

---

# Een [!DNL Veeva CRM]-bronverbinding maken in de gebruikersinterface

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om extern gesourceerde gegevens van CRM op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Veeva CRM]-bronconnector met behulp van de [!DNL Platform]-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Veeva CRM] rekening hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan [vormend een dataflow](../../dataflow/crm.md).

### Vereiste referenties verzamelen

| Credentials | Beschrijving |
| ---------- | ----------- |
| `environmentUrl` | De URL van de broninstantie [!DNL Veeva CRM]. |
| `username` | De gebruikersnaam voor de [!DNL Veeva CRM]-gebruikersaccount. |
| `password` | Het wachtwoord voor de [!DNL Veeva CRM] gebruikersaccount. |
| `securityToken` | Het beveiligingstoken voor de [!DNL Veeva CRM]-gebruikersaccount. |

Voor meer informatie over aan de slag gaan, verwijs naar [dit document van CRM van Veeva]

## Uw [!DNL Veeva CRM]-account aansluiten

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Veeva CRM]-account te koppelen aan [!DNL Platform].

Selecteer **[!UICONTROL Sources]** in de gebruikersinterface van het Platform in de linkernavigatiebalk voor toegang tot de werkruimte [!UICONTROL Sources]. In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer [!UICONTROL CRM] onder de categorie **[!UICONTROL Veeva CRM]** en selecteer **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/veeva/catalog.png)

De pagina **[!UICONTROL Connect Veeva CRM account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL Veeva CRM]-account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![bestaand](../../../../images/tutorials/create/veeva/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u een naam, een optionele beschrijving en uw [!DNL Veeva CRM]-referenties op. Wanneer gebeëindigd, selecteer **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding toe om te vestigen.

![new](../../../../images/tutorials/create/veeva/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Veeva CRM]-account. U kunt nu doorgaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar Platform](../../dataflow/crm.md).
