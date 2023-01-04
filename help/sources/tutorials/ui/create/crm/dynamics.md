---
keywords: Experience Platform;home;populaire onderwerpen;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamiek
solution: Experience Platform
title: Een Microsoft Dynamics Source Connection maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Microsoft Dynamics-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# Een [!DNL Microsoft Dynamics] bronverbinding in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Microsoft Dynamics] (hierna &quot;[!DNL Dynamics]&quot;) bronverbinding via de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Dynamics] account, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [het vormen van een dataflow voor een bron van CRM](../../dataflow/crm.md).

### Vereiste referenties verzamelen

| Credentials | Beschrijving |
| ---------- | ----------- |
| `serviceUri` | De service-URL van uw [!DNL Dynamics] -instantie. |
| `username` | De gebruikersnaam voor uw [!DNL Dynamics] gebruikersaccount. |
| `password` | Het wachtwoord voor uw [!DNL Dynamics] account. |
| `servicePrincipalId` | De client-id van uw [!DNL Dynamics] account. Deze ID wordt vereist wanneer het gebruiken van de dienst hoofd en op sleutel-gebaseerde authentificatie. |
| `servicePrincipalKey` | De geheime sleutel van de dienst belangrijkste geheim. Deze referentie wordt vereist wanneer het gebruiken van de dienst belangrijkste en op sleutel-gebaseerde authentificatie. |

Raadpleeg voor meer informatie over aan de slag gaan [dit [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Verbind uw [!DNL Dynamics] account

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Dynamics] aan Platform.

Aanmelden bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De **[!UICONTROL Catalog]** in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de **[!UICONTROL CRM]** categorie, selecteert u **[!UICONTROL Microsoft Dynamics]**. Als dit de eerste keer is met deze connector, selecteert u **[!UICONTROL Configure]**. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe [!DNL Dynamics] -aansluiting.

![catalogus](../../../../images/tutorials/create/ms-dynamics/catalog.png)

De **[!UICONTROL Connect to Dynamics]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New account]**. Geef in het invoerformulier dat wordt weergegeven een naam en een optionele beschrijving op voor uw nieuwe [!DNL Dynamics] account.

De [!DNL Dynamics] de schakelaar verstrekt u verschillende authentificatietypen voor toegang. Onder [!UICONTROL Account authentication] selecteren **[!UICONTROL Basic authentication]** om op wachtwoord-gebaseerde geloofsbrieven te gebruiken.

Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat vervolgens enige tijd over voor de nieuwe account.

![basisverificatie](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

U kunt ook **[!UICONTROL Service-principal and key authentication]** en sluit uw [!DNL Dynamics] account met een combinatie van [!UICONTROL Service principal ID] en [!UICONTROL Service principal key].

>[!IMPORTANT]
>
> Basisverificatie in [!DNL Dynamics] kan worden geblokkeerd door verificatie met twee factoren, die momenteel niet door Platform wordt ondersteund. In dit geval wordt aangeraden op sleutels gebaseerde verificatie te gebruiken om een bronconnector te maken die [!DNL Dynamics].

![op sleutels gebaseerde verificatie](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Credentials | Beschrijving |
| ---------- | ----------- |
| [!UICONTROL Service principal ID] | De client-id van uw [!DNL Dynamics] account. Deze ID wordt vereist wanneer het gebruiken van de dienst hoofd en op sleutel-gebaseerde authentificatie. |
| [!UICONTROL Service principal key] | De geheime sleutel van de dienst belangrijkste geheim. Deze referentie wordt vereist wanneer het gebruiken van de dienst belangrijkste en op sleutel-gebaseerde authentificatie. |

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de optie [!DNL Dynamics] account waarmee u verbinding wilt maken, selecteert u **[!UICONTROL Next]** in de rechterbovenhoek om verder te gaan.

![bestaand](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Dynamics] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens naar het Platform te brengen](../../dataflow/crm.md).
