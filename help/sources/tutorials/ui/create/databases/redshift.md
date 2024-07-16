---
title: Een Amazon Redshift Source-verbinding maken in de gebruikersinterface
description: Leer hoe u een Amazon Redshift-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Sluit uw [!DNL Amazon Redshift] -account aan met de werkruimte Bronnen

>[!IMPORTANT]
>
>De [!DNL Amazon Redshift] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

Deze zelfstudie bevat stappen voor het tot stand brengen van een verbinding tussen uw [!DNL Amazon Redshift] -account (hierna &quot;[!DNL Redshift]&quot; genoemd) en Adobe Experience Platform via de gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

- [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   - [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Redshift] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL Redshift] -account op Experience Platform, moet u de volgende waarden opgeven:

| **Referentie** | **Beschrijving** |
| -------------- | --------------- |
| Server | De server die aan uw [!DNL Redshift] account is gekoppeld. |
| Poort | De TCP-poort die een [!DNL Redshift] -server gebruikt om te luisteren naar clientverbindingen. |
| Gebruikersnaam | De gebruikersnaam die aan uw [!DNL Redshift] -account is gekoppeld. |
| Wachtwoord | Het wachtwoord dat aan uw [!DNL Redshift] account is gekoppeld. |
| Database | De [!DNL Redshift] -database die u opent. |

Voor meer informatie over begonnen worden, verwijs naar [ dit  [!DNL Redshift]  document ](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Redshift] -account te koppelen aan het Experience Platform.

## Sluit uw [!DNL Redshift] -account aan

>[!NOTE]
>
>De standaard coderingsstandaard voor [!DNL Redshift] is Unicode. Dit kan niet worden gewijzigd.

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Databases]** de optie **[!UICONTROL Amazon Redshift]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe [!DNL Redshift] -connector te maken.

![](../../../../images/tutorials/create/redshift/catalog.png)

De pagina **[!UICONTROL Connect to Amazon Redshift]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Redshift] -gegevens op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![](../../../../images/tutorials/create/redshift/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Redshift] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![](../../../../images/tutorials/create/redshift/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Redshift] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in Experience Platform ](../../dataflow/databases.md) te brengen.
