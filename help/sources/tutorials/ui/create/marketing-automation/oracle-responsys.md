---
keywords: Experience Platform;huis;populaire onderwerpen;bronnen;schakelaars;oracle;
title: (Bèta) creeer een Oracle Resys bronverbinding gebruikend Platform UI
description: Leer hoe te om Adobe Experience Platform met Oracle te verbinden Resys gebruikend Platform UI.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# (Beta) Maak een [!DNL Oracle Responsys] bronverbinding met platforminterface

>[!NOTE]
>
>De [!DNL Oracle Responsys] De bron is in bèta. Zie de [Overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Deze zelfstudie bevat stappen voor het maken van een [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) bronverbinding via de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Platform:

* [Bronnen](../../../../home.md): Platform staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [Sandboxen](../../../../../sandboxes/home.md): Platform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Als u al een geverifieerde [!DNL Oracle Responsys] account op Platform, dan kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [een gegevensstroom maken om gegevens over marketingautomatisering naar het platform te brengen](../../dataflow/marketing-automation.md).

### Vereiste referenties verzamelen

Om verbinding te maken [!DNL Oracle Responsys] aan Platform, moet u waarden voor de volgende authentificatieeigenschappen verstrekken:

| Credentials | Beschrijving |
| --- | --- |
| Endpoint | De URL van het REST-verificatiepunt van uw [!DNL Oracle Responsys] -instantie. |
| Client-id | De client-id van uw [!DNL Oracle Responsys] -instantie. |
| Clientgeheim | Het clientgeheim van uw [!DNL Oracle Responsys] -instantie. |

Voor meer informatie over verificatiereferenties voor [!DNL Oracle Responsys], zie de [[!DNL Oracle Responsys] handleiding voor verificatie](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Oracle Responsys] account aan Platform.

## Verbind uw [!DNL Oracle Responsys] account

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de [!UICONTROL Marketing automation] categorie, selecteert u **[!UICONTROL Oracle Responsys]** en selecteer vervolgens **[!UICONTROL Add data]**.

![De Adobe Experience Platform-broncatalogus met de gemarkeerde bron Resys van het Oracle.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

De **[!UICONTROL Connect Oracle Responsys account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de optie [!DNL Oracle Responsys] account waarmee u een nieuwe gegevensstroom wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![Het bestaande scherm van de rekeningsauthentificatie voor Oracle Responsys.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Nieuwe account

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam, een optionele beschrijving en de juiste waarden voor uw [!DNL Oracle Responsys] referenties. Selecteer **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![Het nieuwe scherm van de rekeningsauthentificatie voor Oracle Responsys.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een bronverbinding tussen uw [!DNL Oracle Responsys] account en platform. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom maken om gegevens over marketingautomatisering naar het platform te brengen](../../dataflow/marketing-automation.md).
