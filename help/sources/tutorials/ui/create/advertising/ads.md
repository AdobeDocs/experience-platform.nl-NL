---
keywords: Experience Platform;home;populaire onderwerpen;Google AdWords;Google AdWords-bronconnector;google adwords-connector
solution: Experience Platform
title: Een Google AdWords-bronverbinding maken in de gebruikersinterface
topic: overview
type: Tutorial
description: Leer hoe u een Google AdWords-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# Een [!DNL Google AdWords]-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
>De [!DNL Google AdWords] schakelaar is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Google AdWords]-bronconnector met behulp van de [!DNL Platform]-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Google AdWords] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [vormend een dataflow](../../dataflow/payments.md)

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL Google AdWords]-account [!DNL Platform], moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `clientCustomerId` | De client-id van de [!DNL AdWords]-account. |
| `developerToken` | Het ontwikkelaarstoken verbonden aan de managerrekening. |
| `refreshToken` | Het vernieuwingstoken dat van [!DNL Google] wordt verkregen om toegang tot [!DNL AdWords] toe te staan. |
| `clientId` | De client-id van de [!DNL Google]-toepassing die wordt gebruikt om het vernieuwingstoken te verkrijgen. |
| `clientSecret` | Het clientgeheim van de toepassing [!DNL Google] die wordt gebruikt om het vernieuwingstoken te verkrijgen. |

Raadpleeg dit [[!DNL Google AdWords] document](https://developers.google.com/adwords/api/docs/guides/authentication) voor meer informatie over aan de slag gaan.

## Uw [!DNL Google AdWords]-account aansluiten

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Google AdWords]-account te koppelen aan [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Bronnen]** te openen. Het scherm **[!UICONTROL Catalog]** toont een verscheidenheid van bronnen waarvoor u een rekening kunt tot stand brengen met.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL Google AdWords]** onder de categorie **[!UICONTROL Reclame]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders, uitgezocht **[!UICONTROL voeg gegevens]** toe om een nieuwe [!DNL Google AdWords] schakelaar tot stand te brengen.

![catalogus](../../../../images/tutorials/create/ads/catalog.png)

De pagina **[!UICONTROL Verbinding maken met Google AdWords]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, selecteer **[!UICONTROL Nieuwe rekening]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Google AdWords]-referenties op. Selecteer **[!UICONTROL Connect]** als u klaar bent en wacht dan enige tijd tot de nieuwe verbinding tot stand is gebracht.

![verbinden](../../../../images/tutorials/create/ads/connect.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Google AdWords]-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/ads/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Google AdWords]-account. U kunt nu doorgaan naar de volgende zelfstudie en [een gegevensstroom configureren om advertentiegegevens over te brengen naar [!DNL Platform]](../../dataflow/advertising.md).