---
keywords: Experience Platform;thuis;populaire onderwerpen;uitspringen;Schuiven
solution: Experience Platform
title: Een schopify-bronverbinding maken in de gebruikersinterface
topic: overview
type: Tutorial
description: Leer hoe u een Shopify-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: cc23228cb410dc4c70a56c5142be00c2ca1c40d3
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---


# Een [!DNL Shopify]-bronverbinding maken in de gebruikersinterface

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Shopify]-bronconnector met behulp van de [!DNL Platform]-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [XDM-systeem](../../../../../xdm/home.md) (Experience Data Model): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een [!DNL Shopify] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [vormend een dataflow voor een eCommerce schakelaar](../../dataflow/ecommerce.md).

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL Shopify]-account op [!DNL Platform], moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het eindpunt van uw [!DNL Shopify]-server. |
| `accessToken` | Het toegangstoken voor uw [!DNL Shopify] gebruikersrekening. |

Raadpleeg dit [[!DNL Shopify] document](https://shopify.dev/concepts/about-apis/authentication) voor meer informatie over aan de slag gaan.

## Uw [!DNL Shopify]-account aansluiten

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Shopify]-account te koppelen aan [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Sources]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Sources]** te openen. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL Shopify]** onder de categorie **[!UICONTROL eCommerce]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL Configure]**. Anders, selecteer **[!UICONTROL Add data]** om een nieuwe [!DNL Shopify] schakelaar tot stand te brengen.

![catalogus](../../../../images/tutorials/create/shopify/catalog.png)

De pagina **[!UICONTROL Connect to Shopify]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, uitgezocht **[!UICONTROL New account]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Shopify]-referenties op. Wanneer gebeëindigd, selecteer **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding toe om te vestigen.

![verbinden](../../../../images/tutorials/create/shopify/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Shopify]-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![bestaand](../../../../images/tutorials/create/shopify/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Shopify]-account. U kunt nu doorgaan naar de volgende zelfstudie en [een gegevensstroom configureren om eCommerce-gegevens over te brengen naar [!DNL Platform]](../../dataflow/ecommerce.md).