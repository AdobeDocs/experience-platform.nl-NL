---
keywords: Experience Platform;home;populaire onderwerpen;Amazon Redshift;amazon redshift;Opnieuw verschuiven;Opnieuw verschuiven
solution: Experience Platform
title: Een Amazon Redshift Source Connection maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een Amazon Redshift-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: 2fb972b0ec8d1f679c6ce104a439265b5cc4d535
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 1%

---

# Een [!DNL Amazon Redshift] bronverbinding in de gebruikersinterface

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Amazon Redshift] (hierna &quot;[!DNL Redshift]&quot;) bronaansluiting met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Redshift] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Om toegang te krijgen tot uw [!DNL Redshift] account op [!DNL Platform]moet u de volgende waarden opgeven:

| **Credentials** | **Beschrijving** |
| -------------- | --------------- |
| `server` | De server die aan uw [!DNL Redshift] account. |
| `username` | De gebruikersnaam die aan uw [!DNL Redshift] account. |
| `password` | Het wachtwoord dat aan uw [!DNL Redshift] account. |
| `database` | De [!DNL Redshift] database die u opent. |

Raadpleeg voor meer informatie over aan de slag gaan [dit [!DNL Redshift] document](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

## Verbind uw [!DNL Redshift] account

>[!NOTE]
>
>De standaard coderingsstandaard voor [!DNL Redshift] is Unicode. Dit kan niet worden gewijzigd.

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Redshift] account aan [!DNL Platform].

Aanmelden bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de **[!UICONTROL Sources]** werkruimte. De **[!UICONTROL Catalog]** in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de **[!UICONTROL Databases]** categorie, selecteert u **[!UICONTROL Amazon Redshift]**. Als dit de eerste keer is met deze connector, selecteert u **[!UICONTROL Configure]**. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe [!DNL Redshift] -aansluiting.

![](../../../../images/tutorials/create/redshift/catalog.png)

De **[!UICONTROL Connect to Amazon Redshift]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New account]**. Geef op het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Redshift] referenties. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![](../../../../images/tutorials/create/redshift/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de optie [!DNL Redshift] account waarmee u verbinding wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![](../../../../images/tutorials/create/redshift/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Redshift] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar [!DNL Platform]](../../dataflow/databases.md).
