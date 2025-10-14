---
keywords: Experience Platform;home;populaire onderwerpen;Square;square
title: Een vierkante Source-verbinding maken in de gebruikersinterface
description: Leer hoe u een vierkante bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Een [!DNL Square] bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Square] bronaansluiting met behulp van de Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

### Vereiste referenties verzamelen

U moet de volgende waarden opgeven om toegang te krijgen tot uw [!DNL Square] -account Experience Platform:

| Credentials | Beschrijving |
| --- | --- |
| Host | De URL van de instantie [!DNL Square] . |
| Client-id | De client-id die aan uw [!DNL Square] -account is gekoppeld. |
| Clientgeheim | Het clientgeheim dat aan uw [!DNL Square] -account is gekoppeld. |
| Toegangstoken | Het toegangstoken wordt gebruikt om uw [!DNL Square] rekening met authentificatie te verifiëren OAuth 2.0. Het toegangstoken kan uit [!DNL Square] worden verkregen. |
| Token vernieuwen | Vernieuw teken wordt gebruikt om nieuwe toegangstoken te produceren zodra uw huidige toegangstoken verloopt. Het token voor vernieuwen kan worden opgehaald uit [!DNL Square] . |

Voor meer informatie over deze geloofsbrieven en hoe te om hen te verkrijgen, zie de [[!DNL Square]  documentatie over OAuth &#x200B;](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Square] -account te koppelen aan Experience Platform.

## Sluit uw [!DNL Square] -account aan

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie [!UICONTROL Payments] de optie **[!UICONTROL Square]** en selecteer vervolgens **[!UICONTROL Add data]** .

![&#x200B; catalogus &#x200B;](../../../../images/tutorials/create/square/catalog.png)

De pagina **[!UICONTROL Connect to Square]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL Square] -account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u vervolgens **[!UICONTROL Next]** om door te gaan.

![&#x200B; bestaand &#x200B;](../../../../images/tutorials/create/square/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u vervolgens een naam, een optionele beschrijving en de juiste waarden voor uw [!DNL Square] -referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![&#x200B; nieuw &#x200B;](../../../../images/tutorials/create/square/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een bronverbinding gemaakt en geverifieerd tussen uw [!DNL Square] -account en Experience Platform. U kunt nu aan het volgende leerprogramma verdergaan en [&#x200B; tot een dataflow leiden om betalingsgegevens in Experience Platform &#x200B;](../../dataflow/payments.md) te brengen.
