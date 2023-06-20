---
title: Een Amazon Redshift Source Connection maken in de gebruikersinterface
description: Leer hoe u een Amazon Redshift-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---

# Verbind uw [!DNL Amazon Redshift] account met gebruik van de werkruimte Bronnen

>[!IMPORTANT]
>
>De [!DNL Amazon Redshift] De bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

Deze zelfstudie bevat stappen voor het tot stand brengen van een verbinding met uw [!DNL Amazon Redshift] (hierna &quot;[!DNL Redshift]&quot;) naar Adobe Experience Platform via de gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   - [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Redshift] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Om toegang te krijgen tot uw [!DNL Redshift] account op Experience Platform, moet u de volgende waarden opgeven:

| **Credentials** | **Beschrijving** |
| -------------- | --------------- |
| Server | De server die aan uw [!DNL Redshift] account. |
| Poort | De haven van TCP die [!DNL Redshift] server gebruikt om naar clientverbindingen te luisteren. |
| Gebruikersnaam | De gebruikersnaam die aan uw [!DNL Redshift] account. |
| Wachtwoord | Het wachtwoord dat aan uw [!DNL Redshift] account. |
| Database | De [!DNL Redshift] database die u opent. |

Raadpleeg voor meer informatie over aan de slag gaan [dit [!DNL Redshift] document](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Redshift] aan Experience Platform.

## Verbind uw [!DNL Redshift] account

>[!NOTE]
>
>De standaard coderingsstandaard voor [!DNL Redshift] is Unicode. Dit kan niet worden gewijzigd.

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

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Redshift] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens naar het Experience Platform te brengen](../../dataflow/databases.md).
