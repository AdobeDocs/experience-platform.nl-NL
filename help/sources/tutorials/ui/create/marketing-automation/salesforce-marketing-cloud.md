---
keywords: Experience Platform;home;populaire onderwerpen;salesforce marketing cloud;Salesforce Marketing Clud
solution: Experience Platform
title: Creeer een Verbinding van de Bron van de Marketing Cloud Salesforce in UI
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Salesforce-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 531d5619e0643b6195abaa53d1708e0368d45871
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Een [!DNL Salesforce Marketing Cloud] bronverbinding in de gebruikersinterface

>[!NOTE]
>
> De [!DNL Salesforce Marketing Cloud] De bron is in bèta. Zie de [overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Salesforce Marketing Cloud] bronaansluiting die gebruikmaakt van de gebruikersinterface van het Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een [!DNL Salesforce Marketing Cloud] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/marketing-automation.md).

### Vereiste referenties verzamelen

Om toegang te krijgen tot uw [!DNL Salesforce Marketing Cloud] account op Platform, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De hostserver van uw toepassing. Dit is vaak uw subdomein. **Opmerking:** Wanneer u uw `host` waarde, hoeft u alleen het subdomein op te geven en niet de volledige URL. Als de host-URL bijvoorbeeld `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, hoeft u alleen maar in te voeren `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` als uw hostwaarde. |
| `clientId` | De client-id die aan uw [!DNL Salesforce Marketing Cloud] toepassing. |
| `clientSecret` | Het clientgeheim dat aan uw [!DNL Salesforce Marketing Cloud] toepassing. |

Raadpleeg voor meer informatie over aan de slag gaan [[!DNL Salesforce Marketing Cloud] document](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Verbind uw [!DNL Salesforce Marketing Cloud] account

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Salesforce Marketing Cloud] aan Platform.

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt de onderzoeksbar ook gebruiken om onderaan de getoonde schakelaars te versmallen.

Onder de [!UICONTROL Marketing automation] categorie, selecteert u **[!UICONTROL Salesforce Marketing Cloud]** en selecteer vervolgens **[!UICONTROL Set up]**.

![catalogus](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

De **[!UICONTROL Connect to Salesforce Marketing Cloud]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New account]**. Geef op het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Salesforce Marketing Cloud] referenties. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![new](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de optie [!DNL Salesforce Marketing Cloud] account waarmee u verbinding wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![bestaand](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Salesforce Marketing Cloud] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens van het marketingautomatiseringssysteem in Platform te brengen](../../dataflow/marketing-automation.md).
