---
keywords: Experience Platform;home;populaire onderwerpen;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics;dynamics
solution: Experience Platform
title: Creeer een Verbinding van de Bron van de Dynamica van Microsoft in UI
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Microsoft Dynamics-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# Een [!DNL Microsoft Dynamics]-bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Microsoft Dynamics]-bronverbinding (hierna &quot;[!DNL Dynamics]&quot; genoemd) met behulp van de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Dynamics] rekening hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [vormend een dataflow voor een bron van CRM](../../dataflow/crm.md).

### Vereiste referenties verzamelen

| Credentials | Beschrijving |
| ---------- | ----------- |
| `serviceUri` | De service-URL van uw [!DNL Dynamics]-instantie. |
| `username` | De gebruikersnaam voor uw [!DNL Dynamics] gebruikersaccount. |
| `password` | Het wachtwoord voor uw [!DNL Dynamics]-account. |
| `servicePrincipalId` | De client-id van uw [!DNL Dynamics]-account. Deze ID wordt vereist wanneer het gebruiken van de dienst hoofd en op sleutel-gebaseerde authentificatie. |
| `servicePrincipalKey` | De geheime sleutel van de dienst belangrijkste geheim. Deze referentie wordt vereist wanneer het gebruiken van de dienst belangrijkste en op sleutel-gebaseerde authentificatie. |

Raadpleeg [this [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth) voor meer informatie over aan de slag gaan.

## Uw [!DNL Dynamics]-account aansluiten

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Dynamics]-account te koppelen aan het Platform.

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Sources]** in de linkernavigatiebalk om de werkruimte [!UICONTROL Sources] te openen. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL Microsoft Dynamics]** onder de categorie **[!UICONTROL CRM]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL Configure]**. Anders, selecteer **[!UICONTROL Add data]** om een nieuwe [!DNL Dynamics] schakelaar tot stand te brengen.

![catalogus](../../../../images/tutorials/create/ms-dynamics/catalog.png)

De pagina **[!UICONTROL Connect to Dynamics]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, uitgezocht **[!UICONTROL New account]**. Geef op het invoerformulier dat wordt weergegeven een naam en een optionele beschrijving voor uw nieuwe [!DNL Dynamics]-account.

De [!DNL Dynamics] schakelaar verstrekt u verschillende authentificatietypen voor toegang. Selecteer [!UICONTROL Account authentication] onder **[!UICONTROL Basic authentication]** om op wachtwoord gebaseerde referenties te gebruiken.

Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe account enige tijd over om op te richten.

![basisverificatie](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

U kunt ook **[!UICONTROL Service-principal and key authentication]** selecteren en uw [!DNL Dynamics]-account aansluiten met een combinatie van [!UICONTROL Service principal ID] en [!UICONTROL Service principal key].

>[!IMPORTANT]
>
> Basisverificatie in [!DNL Dynamics] kan worden geblokkeerd door tweefasenverificatie, die momenteel niet door Platform wordt ondersteund. In dit geval, wordt het geadviseerd om op sleutel-gebaseerde authentificatie te gebruiken om een bronschakelaar tot stand te brengen gebruikend [!DNL Dynamics].

![op sleutels gebaseerde verificatie](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Credentials | Beschrijving |
| ---------- | ----------- |
| [!UICONTROL Service principal ID] | De client-id van uw [!DNL Dynamics]-account. Deze ID wordt vereist wanneer het gebruiken van de dienst hoofd en op sleutel-gebaseerde authentificatie. |
| [!UICONTROL Service principal key] | De geheime sleutel van de dienst belangrijkste geheim. Deze referentie wordt vereist wanneer het gebruiken van de dienst belangrijkste en op sleutel-gebaseerde authentificatie. |

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Dynamics]-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** in de rechterbovenhoek om door te gaan.

![bestaand](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Dynamics]-account. U kunt nu doorgaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar Platform](../../dataflow/crm.md).
