---
keywords: Experience Platform;home;populaire onderwerpen;paypal;Paypal
solution: Experience Platform
title: Een PayPal-bronverbinding maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een PayPal-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
source-git-commit: 6b6bd67e70267e81c144c37549b0dcba20534eb6
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---

# Een [!DNL PayPal]-bronverbinding maken in de gebruikersinterface

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL PayPal]-bronconnector met behulp van de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL PayPal] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [vormend een dataflow](../../dataflow/payments.md)

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot het Platform van uw [!DNL PayPal]-account, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De URL van de instantie [!DNL PayPal]. |
| `clientID` | De client-id die is gekoppeld aan uw [!DNL PayPal]-toepassing. |
| `clientSecret` | Het clientgeheim dat is gekoppeld aan uw [!DNL PayPal]-toepassing. |

Raadpleeg dit [[!DNL PayPal] document](https://developer.paypal.com/docs/api/overview/#get-credentials) voor meer informatie over aan de slag gaan

## Uw [!DNL PayPal]-account aansluiten

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL PayPal]-account te koppelen aan het Platform.

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Sources]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Sources]** te openen. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL PayPal]** onder de categorie **[!UICONTROL Payments]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL Configure]**. Anders, selecteer **[!UICONTROL Add data]** om een nieuwe [!DNL PayPal] schakelaar tot stand te brengen.

![catalogus](../../../../images/tutorials/create/paypal/catalog.png)

De pagina **[!UICONTROL Connect to PayPal]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, uitgezocht **[!UICONTROL New account]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL PayPal]-referenties op. Wanneer gebeëindigd, selecteer **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding toe om te vestigen.

![verbinden](../../../../images/tutorials/create/paypal/connect.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL PayPal]-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![bestaand](../../../../images/tutorials/create/paypal/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL PayPal]-account. U kunt nu doorgaan naar de volgende zelfstudie en [een gegevensstroom configureren om betalingsgegevens over te brengen naar Platform](../../dataflow/payments.md).
