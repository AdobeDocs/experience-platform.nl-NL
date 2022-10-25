---
keywords: Experience Platform;home;populaire onderwerpen;Oracle Service Cloud;oracle service cloud
title: Een Cloud Source Connection voor de service Oracle maken in de gebruikersinterface
description: Leer hoe u een Oracle Service Cloud-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
source-git-commit: 8e4f2170489d7e4e73bbc726e3253fac97c9f9f3
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# (Beta) Een Cloud-bronverbinding voor Oracles maken in de gebruikersinterface

>[!NOTE]
>
>De Oracle Service Cloud-bron is in bèta. Zie de [overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Deze zelfstudie bevat stappen voor het maken van een Oracle Service Cloud-bronverbinding via de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige Cloud-bronverbinding voor Oracle Service hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/customer-success.md)

### Vereiste referenties verzamelen

Voor toegang tot uw Oracle Service Cloud-account op [!DNL Platform]moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Host | De host-URL van uw Oracle Service Cloud-instantie. |
| Gebruikersnaam | De gebruikersnaam voor uw Oracle Service Cloud-gebruikersaccount. |
| Wachtwoord | Het wachtwoord voor uw Oracle Service Cloud-account. |

Raadpleeg voor meer informatie over het verifiëren van uw Oracle Service Cloud-account de [[!DNL Oracle] handleiding voor verificatie](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

## Verbinding maken met uw Oracle Service Cloud-account

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] op het scherm worden diverse bronnen weergegeven die kunnen worden gebruikt om een account te maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder de [!UICONTROL Customer success] categorie, selecteert u **[!UICONTROL Oracle Service Cloud]** en selecteer vervolgens **[!UICONTROL Add data]**.

![De broncatalogus met de Oracle Service Cloud-bron gemarkeerd.](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

De **[!UICONTROL Connect to Oracle Service Cloud]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u het Oracle Service Cloud-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om verder te gaan.

![De bestaande accountinterface.](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### Nieuwe account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New account]**. Geef op het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw Oracle Service Cloud-referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![De nieuwe accountinterface met plaatsaanduidingswaarden voor.](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw Oracle Service Cloud-account. U kunt nu verdergaan met de volgende zelfstudie en [een dataflow configureren om gegevens voor klantresultaten in Platform te brengen](../../dataflow/crm.md).
