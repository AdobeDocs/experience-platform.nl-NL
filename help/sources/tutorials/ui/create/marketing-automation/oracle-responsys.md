---
keywords: Experience Platform;home;populaire onderwerpen;bronnen;connectors;orakel;
title: (Beta) Een Oracle Resys-bronverbinding maken met Experience Platform UI
description: Leer hoe u Adobe Experience Platform met Oracle Responsys verbindt via de gebruikersinterface van Experience Platform.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# (Beta) Een [!DNL Oracle Responsys] bronverbinding maken met de gebruikersinterface van Experience Platform

>[!NOTE]
>
>De bron [!DNL Oracle Responsys] is in bèta. Zie het [ Bronoverzicht ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

In deze zelfstudie worden de stappen beschreven waarmee u een [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) -bronverbinding maakt via de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

Als u reeds een voor authentiek verklaarde [!DNL Oracle Responsys] rekening op Experience Platform hebt, dan kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan [ creërend een dataflow om de gegevens van de marketing automatisering aan Experience Platform ](../../dataflow/marketing-automation.md) te brengen.

### Vereiste referenties verzamelen

Als u [!DNL Oracle Responsys] wilt verbinden met Experience Platform, moet u waarden opgeven voor de volgende verificatie-eigenschappen:

| Credentials | Beschrijving |
| --- | --- |
| Endpoint | De URL van het REST-verificatiepunt van uw [!DNL Oracle Responsys] -instantie. |
| Client-id | De client-id van uw [!DNL Oracle Responsys] -instantie. |
| Clientgeheim | Het clientgeheim van de instantie [!DNL Oracle Responsys] . |

Voor meer informatie over authentificatiegeloofsbrieven voor [!DNL Oracle Responsys], zie de [[!DNL Oracle Responsys]  gids over authentificatie ](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Oracle Responsys] -account te koppelen aan Experience Platform.

## Sluit uw [!DNL Oracle Responsys] -account aan

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie [!UICONTROL Marketing automation] de optie **[!UICONTROL Oracle Responsys]** en selecteer vervolgens **[!UICONTROL Add data]** .

![ de de broncatalogus van Adobe Experience Platform met de benadrukte bron van Resys van Oracle.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

De pagina **[!UICONTROL Connect Oracle Responsys account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL Oracle Responsys] -account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u vervolgens **[!UICONTROL Next]** om door te gaan.

![ het bestaande scherm van de rekeningsauthentificatie voor Oracle Responsys.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Nieuwe account

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u vervolgens een naam, een optionele beschrijving en de juiste waarden voor uw [!DNL Oracle Responsys] -referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ het nieuwe scherm van de rekeningsauthentificatie voor Oracle Responsys.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een bronverbinding gemaakt en geverifieerd tussen uw [!DNL Oracle Responsys] -account en Experience Platform. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow creëren om de gegevens van de marketing automatisering aan Experience Platform ](../../dataflow/marketing-automation.md) te brengen.
