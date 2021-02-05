---
keywords: Experience Platform;thuis;populaire onderwerpen;hubspot;Hubspot
solution: Experience Platform
title: Creeer een Verbinding van de Bron van HubSpot in UI
topic: overview
type: Tutorial
description: Leer hoe te om een HubSpot bronverbinding tot stand te brengen gebruikend Adobe Experience Platform UI.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 1%

---


# Een [!DNL HubSpot]-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
> De [!DNL HubSpot] schakelaar is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL HubSpot]-bronconnector met behulp van de [!DNL Platform]-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een [!DNL HubSpot] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [vormend een dataflow](../../dataflow/marketing-automation.md).

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL HubSpot]-account op [!DNL Platform], moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `clientId` | De client-id die is gekoppeld aan uw [!DNL HubSpot]-toepassing. |
| `clientSecret` | Het clientgeheim dat is gekoppeld aan uw [!DNL HubSpot]-toepassing. |
| `accessToken` | Het toegangstoken werd verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |
| `refreshToken` | Het vernieuwingstoken dat wordt verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |

Raadpleeg dit [[!DNL HubSpot] document](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview) voor meer informatie over aan de slag gaan.

## Uw [!DNL HubSpot]-account aansluiten

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL HubSpot]-account te koppelen aan [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Bronnen]** te openen. Het scherm **[!UICONTROL Catalog]** toont een verscheidenheid van bronnen waarvoor u een rekening kunt tot stand brengen met.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL HubSpot]** onder de categorie **[!UICONTROL Marketing automation]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders, uitgezocht **[!UICONTROL voeg gegevens]** toe om een nieuwe [!DNL HubSpot] schakelaar tot stand te brengen.

![catalogus](../../../../images/tutorials/create/hubspot/catalog.png)

De **[!UICONTROL verbind met HubSpot]** pagina verschijnt. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, selecteer **[!UICONTROL Nieuwe rekening]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL HubSpot]-referenties op. Selecteer **[!UICONTROL Connect]** als u klaar bent en wacht dan enige tijd tot de nieuwe verbinding tot stand is gebracht.

![verbinden](../../../../images/tutorials/create/hubspot/connect.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL HubSpot]-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/hubspot/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL HubSpot]-account. U kunt nu doorgaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens van het marketingautomatiseringssysteem over te brengen naar [!DNL Platform]](../../dataflow/marketing-automation.md).