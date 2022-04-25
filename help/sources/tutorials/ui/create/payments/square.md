---
keywords: Experience Platform;thuis;populaire onderwerpen;Vierkant;vierkant
title: Een vierkante bronverbinding maken in de gebruikersinterface
description: Leer hoe u een vierkante bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
source-git-commit: e905b11040c8de33aa757bd5743605bb36a8009b
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 1%

---

# Een [!DNL Square] bronverbinding in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Square] bronaansluiting die gebruikmaakt van de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

### Vereiste referenties verzamelen

Om toegang te krijgen tot uw [!DNL Square] het Platform van de rekening, moet u de volgende waarden verstrekken:

| Credentials | Beschrijving |
| --- | --- |
| Host | De URL van de [!DNL Square] -instantie. |
| Client-id | De client-id die aan uw [!DNL Square] account. |
| Clientgeheim | Het clientgeheim dat aan uw [!DNL Square] account. |
| Toegangstoken | Het toegangstoken wordt gebruikt om uw voor authentiek te verklaren [!DNL Square] account met OAuth 2.0-verificatie. Het toegangstoken kan worden verkregen van [!DNL Square]. |
| Token vernieuwen | Vernieuw teken wordt gebruikt om nieuwe toegangstoken te produceren zodra uw huidige toegangstoken verloopt. Het vernieuwingstoken kan worden verkregen van [!DNL Square]. |

Voor meer informatie over deze geloofsbrieven en hoe te om hen te verkrijgen, zie [[!DNL Square] documentatie over OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Square] aan Platform.

## Verbind uw [!DNL Square] account

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de [!UICONTROL Payments] categorie, selecteert u **[!UICONTROL Square]** en selecteer vervolgens **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/square/catalog.png)

De **[!UICONTROL Connect to Square]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de optie [!DNL Square] account waarmee u een nieuwe gegevensstroom wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![bestaand](../../../../images/tutorials/create/square/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam, een optionele beschrijving en de juiste waarden voor uw [!DNL Square] referenties. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![new](../../../../images/tutorials/create/square/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een bronverbinding tussen uw [!DNL Square] account en Platform. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom maken om betalingsgegevens in Platform te brengen](../../dataflow/payments.md).
