---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Creeer een de bronschakelaar van de Dynamica van Microsoft in UI
topic: overview
type: Tutorial
description: Dit leerprogramma verstrekt stappen voor het creëren van een de bronschakelaar van de Dynamiek van Microsoft (hierna genoemd "Dynamica") gebruikend het gebruikersinterface van het Platform.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 1%

---


# Creeer een [!DNL Microsoft Dynamics] bronschakelaar in UI

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om extern gesourceerde gegevens van CRM op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het maken van een [!DNL Microsoft Dynamics] (hierna &quot;[!DNL Dynamics]&quot; genoemd) bronconnector met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldig [!DNL Dynamics] account hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie over het [configureren van een gegevensstroom](../../dataflow/crm.md).

### Vereiste referenties verzamelen

| Credentials | Beschrijving |
| ---------- | ----------- |
| `serviceUri` | De service-URL van uw [!DNL Dynamics] instantie. |
| `username` | De gebruikersnaam voor uw [!DNL Dynamics] gebruikersaccount. |
| `password` | Het wachtwoord voor uw [!DNL Dynamics] account. |

Raadpleeg [ [!DNL Dynamics] dit document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)voor meer informatie over aan de slag gaan.

## Uw [!DNL Dynamics] account verbinden

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Dynamics] account te koppelen aan [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte **[!UICONTROL Bronnen]** . In het scherm **[!UICONTROL Catalogus]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Databases]** de optie **[!UICONTROL Dynamics]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders, uitgezocht **[!UICONTROL voeg gegevens]** toe om een nieuwe [!DNL Dynamics] schakelaar tot stand te brengen.

![catalogus](../../../../images/tutorials/create/ms-dynamics/catalog.png)

De pagina **[!UICONTROL Verbinden met dynamiek]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Voer in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Dynamics] referenties in. Wanneer u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![verbinden](../../../../images/tutorials/create/ms-dynamics/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Dynamics] account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** in de rechterbovenhoek om door te gaan.

![bestaand](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw [!DNL Dynamics] account tot stand gebracht. U kunt nu verdergaan naar de volgende zelfstudie en een gegevensstroom [configureren om gegevens in te voeren [!DNL Platform]](../../dataflow/crm.md).