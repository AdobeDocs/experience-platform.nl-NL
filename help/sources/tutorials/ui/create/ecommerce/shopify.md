---
keywords: Experience Platform;home;populaire onderwerpen;winkelify;Shopify
solution: Experience Platform
title: Een Shopify Source Connection maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een Shopify-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 527cac95-3d9a-4089-98e4-66d746641b85
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Een [!DNL Shopify] bronverbinding maken in de gebruikersinterface

Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Shopify] bronaansluiting met behulp van de gebruikersinterface van [!DNL Experience Platform] .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Model van de Gegevens van de Ervaring (XDM) Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een [!DNL Shopify] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow voor een schakelaar van de eCommerce ](../../dataflow/ecommerce.md).

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL Shopify] account op [!DNL Experience Platform] , moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het eindpunt van de [!DNL Shopify] -server. |
| `accessToken` | Het toegangstoken voor uw [!DNL Shopify] gebruikersaccount. |

Voor meer informatie over begonnen worden, verwijs naar dit [[!DNL Shopify]  document ](https://shopify.dev/concepts/about-apis/authentication).

## Sluit uw [!DNL Shopify] -account aan

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL Shopify] -account te koppelen aan [!DNL Experience Platform] .

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL eCommerce]** de optie **[!UICONTROL Shopify]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe [!DNL Shopify] -connector te maken.

![ catalogus ](../../../../images/tutorials/create/shopify/catalog.png)

De pagina **[!UICONTROL Connect to Shopify]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Shopify] -gegevens op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ verbind ](../../../../images/tutorials/create/shopify/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Shopify] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![ bestaand ](../../../../images/tutorials/create/shopify/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Shopify] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om eCommerce-gegevens in  [!DNL Experience Platform]](../../dataflow/ecommerce.md) te brengen.
