---
keywords: Experience Platform;home;populaire onderwerpen;paypal;Paypal
solution: Experience Platform
title: Een PayPal Source Connection maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een PayPal-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
source-git-commit: a32d0d7ed7d18454099d2b55b3f6809cfbcd9b62
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Een [!DNL PayPal] bronverbinding maken in de gebruikersinterface

>[!IMPORTANT]
>
>De bron [!DNL PayPal] wordt eind mei 2025 vervangen.

Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL PayPal] bronconnector met behulp van de gebruikersinterface van Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL PayPal] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/payments.md)

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL PayPal] accountplatform, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De URL van de instantie [!DNL PayPal] . |
| `clientID` | De client-id die aan uw [!DNL PayPal] -toepassing is gekoppeld. |
| `clientSecret` | Het clientgeheim dat aan de toepassing [!DNL PayPal] is gekoppeld. |

Voor meer informatie over begonnen worden, verwijs naar dit [[!DNL PayPal]  document ](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Sluit uw [!DNL PayPal] -account aan

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL PayPal] -account te koppelen aan Platform.

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Payments]** de optie **[!UICONTROL PayPal]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe [!DNL PayPal] -connector te maken.

![ catalogus ](../../../../images/tutorials/create/paypal/catalog.png)

De pagina **[!UICONTROL Connect to PayPal]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL PayPal] -gegevens op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ verbind ](../../../../images/tutorials/create/paypal/connect.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL PayPal] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![ bestaand ](../../../../images/tutorials/create/paypal/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL PayPal] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om de gegevens van de Betaling in Platform ](../../dataflow/payments.md) te brengen.
