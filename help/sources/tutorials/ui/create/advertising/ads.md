---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Google AdWords-bronconnector maken in de gebruikersinterface
topic: overview
translation-type: tm+mt
source-git-commit: ec2d0a33e0ae92a3153b7bdcad29734e487a0439
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---


# Creeer een [!DNL Google AdWords] bronschakelaar in UI

>[!NOTE]
>De [!DNL Google AdWords] connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Google AdWords] bronaansluiting met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time klantprofiel]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Google AdWords] verbinding hebt, kunt u de rest van dit document overslaan en naar de zelfstudie gaan over het [configureren van een gegevensstroom](../../dataflow/payments.md)

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL Google AdWords] [!DNL Platform]account, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `clientCustomerId` | De klant-id van de [!DNL AdWords] account. |
| `developerToken` | Het ontwikkelaarstoken verbonden aan de managerrekening. |
| `refreshToken` | Het vernieuwingstoken dat van [!DNL Google] voor het verlenen van toegang tot wordt verkregen [!DNL AdWords]. |
| `clientId` | De client-id van de [!DNL Google] toepassing waarmee het vernieuwingstoken wordt opgehaald. |
| `clientSecret` | Het clientgeheim van de [!DNL Google] toepassing die wordt gebruikt om het token voor vernieuwen te verkrijgen. |

Raadpleeg dit [[!DNL Google AdWords] document](https://developers.google.com/adwords/api/docs/guides/authentication)voor meer informatie over aan de slag gaan.

## Uw [!DNL Google AdWords] account verbinden

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Google AdWords] account te koppelen aan [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte **[!UICONTROL Bronnen]** . In het scherm **[!UICONTROL Catalogus]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer in de categorie **[!UICONTROL Advertising]** de optie **[!UICONTROL Google AdWords]**. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders, uitgezocht **[!UICONTROL voeg gegevens]** toe om een nieuwe [!DNL Google AdWords] schakelaar tot stand te brengen.

![catalogus](../../../../images/tutorials/create/ads/catalog.png)

De pagina **[!UICONTROL Verbinding maken met Google AdWords]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Voer in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Google AdWords] referenties in. Wanneer u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![verbinden](../../../../images/tutorials/create/ads/connect.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Google AdWords] account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/ads/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw [!DNL Google AdWords] account tot stand gebracht. U kunt nu doorgaan met de volgende zelfstudie en een gegevensstroom [configureren om advertentiegegevens in te voeren [!DNL Platform]](../../dataflow/advertising.md).