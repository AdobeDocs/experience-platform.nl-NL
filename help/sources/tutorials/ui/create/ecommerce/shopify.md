---
keywords: Experience Platform;thuis;populaire onderwerpen;uitspringen;Schuiven
solution: Experience Platform
title: Een schopify-bronverbinding maken in de gebruikersinterface
topic: overview
type: Tutorial
description: Leer hoe u een Shopify-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---


# Een [!DNL Shopify]-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
> De [!DNL Shopify] schakelaar is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

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

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Bronnen]** te openen. Het scherm **[!UICONTROL Catalog]** toont een verscheidenheid van bronnen waarvoor u een rekening kunt tot stand brengen met.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL eCommerce]** **[!UICONTROL Shopify]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders, uitgezocht **[!UICONTROL voeg gegevens]** toe om een nieuwe [!DNL Shopify] schakelaar tot stand te brengen.

![catalogus](../../../../images/tutorials/create/shopify/catalog.png)

De pagina **[!UICONTROL Verbinden met Shopify]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, selecteer **[!UICONTROL Nieuwe rekening]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Shopify]-referenties op. Selecteer **[!UICONTROL Connect]** als u klaar bent en wacht dan enige tijd tot de nieuwe verbinding tot stand is gebracht.

![verbinden](../../../../images/tutorials/create/shopify/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Shopify]-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/shopify/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Shopify]-account. U kunt nu verdergaan op het volgende leerprogramma en [een dataflow vormen om eCommerce-gegevens in [!DNL Platform]](../../dataflow/ecommerce.md) te brengen.