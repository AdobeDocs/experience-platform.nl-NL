---
keywords: Experience Platform;thuis;populaire onderwerpen;Veeva CRM;veeva
solution: Experience Platform
title: Een Veeva CRM-bronverbinding maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Veeva CRM-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 4ef76c28-9bd2-4e54-a3d6-dceb89162337
source-git-commit: ea20a850a5d83f648c699119913aa31e2ea16233
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 1%

---

# Een [!DNL Veeva CRM] bronverbinding in de gebruikersinterface

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om extern gesourceerde gegevens van CRM op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Veeva CRM] bronaansluiting met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Veeva CRM] account, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/crm.md).

### Vereiste referenties verzamelen

| Credentials | Beschrijving |
| ---------- | ----------- |
| `environmentUrl` | De URL van de [!DNL Veeva CRM] broninstantie. |
| `username` | De gebruikersnaam voor de [!DNL Veeva CRM] gebruikersaccount. |
| `password` | Het wachtwoord voor de [!DNL Veeva CRM] gebruikersaccount. |
| `securityToken` | De beveiligingstoken voor de [!DNL Veeva CRM] gebruikersaccount. |

Raadpleeg voor meer informatie over aan de slag gaan [[!DNL Veeva CRM] document](https://developer.veevacrm.com/doc/Content/rest-api.htm).

## Verbind uw [!DNL Veeva CRM] account

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Veeva CRM] account aan [!DNL Platform].

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de [!UICONTROL CRM] categorie, selecteert u **[!UICONTROL Veeva CRM]** en selecteer vervolgens **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/veeva/catalog.png)

De **[!UICONTROL Connect Veeva CRM account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de optie [!DNL Veeva CRM] account waarmee u een nieuwe gegevensstroom wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![bestaand](../../../../images/tutorials/create/veeva/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam, een optionele beschrijving en uw [!DNL Veeva CRM] referenties. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![new](../../../../images/tutorials/create/veeva/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Veeva CRM] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens naar het Platform te brengen](../../dataflow/crm.md).
