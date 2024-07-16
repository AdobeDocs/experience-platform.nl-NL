---
keywords: Experience Platform;home;populaire onderwerpen;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamiek
solution: Experience Platform
title: Een Microsoft Dynamics Source Connection maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een Microsoft Dynamics-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Een [!DNL Microsoft Dynamics] bronverbinding maken in de gebruikersinterface

Deze zelfstudie biedt stappen om een [!DNL Microsoft Dynamics] (hierna &quot;[!DNL Dynamics]&quot; genoemd) bronverbinding tot stand te brengen die de gebruikersinterface van Adobe Experience Platform gebruikt.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Dynamics] rekening hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow voor een bron van CRM ](../../dataflow/crm.md).

### Vereiste referenties verzamelen

Als u de [!DNL Dynamics] -bron wilt verifiëren, moet u waarden opgeven voor de volgende verbindingseigenschappen:

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

| Credentials | Beschrijving |
| --- | --- |
| `serviceUri` | De service-URL van uw [!DNL Dynamics] -instantie. |
| `username` | De gebruikersnaam voor uw [!DNL Dynamics] -gebruikersaccount. |
| `password` | Het wachtwoord voor uw [!DNL Dynamics] -account. |

>[!TAB  dienst-hoofd en zeer belangrijke authentificatie ]

| Credentials | Beschrijving |
| --- | --- |
| `servicePrincipalId` | De client-id van uw [!DNL Dynamics] -account. Deze ID wordt vereist wanneer het gebruiken van de dienst hoofd en op sleutel-gebaseerde authentificatie. |
| `servicePrincipalKey` | De geheime sleutel van de dienst belangrijkste geheim. Deze referentie wordt vereist wanneer het gebruiken van de dienst belangrijkste en op sleutel-gebaseerde authentificatie. |

>[!ENDTABS]

Voor meer informatie bij het worden begonnen, verwijs naar [ dit  [!DNL Dynamics]  document ](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Sluit uw [!DNL Dynamics] -account aan

Selecteer in de gebruikersinterface van het platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie [!UICONTROL CRM] de optie **[!UICONTROL Microsoft Dynamics]** en selecteer vervolgens **[!UICONTROL Add data]** .

![ de geselecteerde broncatalogus met de Dynamica van Microsoft.](../../../../images/tutorials/create/ms-dynamics/catalog.png)

De pagina **[!UICONTROL Connect Microsoft Dynamics account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL Dynamics] -account die u wilt gebruiken en selecteert u **[!UICONTROL Next]** in de rechterbovenhoek om door te gaan.

![ de bestaande rekeningsinterface.](../../../../images/tutorials/create/ms-dynamics/existing.png)

### Nieuwe account

>[!TIP]
>
>Nadat u een [!DNL Dynamics] basisverbinding hebt gemaakt, kunt u het verificatietype niet wijzigen. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam en een optionele beschrijving voor uw nieuwe [!DNL Dynamics] -account.

![ de nieuwe interface van de rekeningsverwezenlijking.](../../../../images/tutorials/create/ms-dynamics/new.png)

Bij het maken van een [!DNL Dynamics] -account kunt u de basisverificatie of de service-principal en key-verificatie gebruiken.

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

Als u een [!DNL Dynamics] -account met basisverificatie wilt maken, selecteert u [!UICONTROL Basic authentication] en geeft u vervolgens waarden op voor uw [!UICONTROL Service URI] , [!UICONTROL Username] en [!UICONTROL Password] . **Nota**: De fundamentele authentificatie in [!DNL Dynamics] kan door tweefaste authentificatie worden geblokkeerd, die momenteel niet door Platform wordt gesteund. In dit geval wordt aangeraden op toetsen gebaseerde verificatie te gebruiken om een bronconnector te maken met [!DNL Dynamics] .

Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe account enige tijd beginnen.

![ de basisauthentificatieinterface.](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB  dienst-hoofd en zeer belangrijke authentificatie ]

Als u een [!DNL Dynamics] -account met service-principal en sleutelverificatie wilt maken, selecteert u **[!UICONTROL Service-principal and key authentication]** en geeft u vervolgens waarden op voor uw account [!UICONTROL Service principal ID] en [!UICONTROL Service principal key] .

Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe account enige tijd beginnen.

![ de dienst-belangrijkste zeer belangrijke authentificatieinterface.](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Dynamics] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in Platform ](../../dataflow/crm.md) te brengen.
