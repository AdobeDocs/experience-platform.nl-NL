---
keywords: Experience Platform;thuis;populaire onderwerpen;Teradata Vantage
title: Een Teradata Vantage Source Connection maken in de gebruikersinterface
description: Leer hoe u een Teradata Vantage-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
source-git-commit: f140dac67ccd09ec1e6cab794f53e0090af55442
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 1%

---

# (Beta) Maak een [!DNL Teradata Vantage] bronverbinding in de gebruikersinterface

>[!NOTE]
>
> De [!DNL Teradata Vantage] De bron is in bèta. Zie de [Overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Teradata Vantage] bronaansluiting die gebruikmaakt van de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Experience Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Vereiste referenties verzamelen

Om toegang te krijgen tot uw [!DNL Teradata Vantage] account op Platform, moet u de volgende verificatiewaarde opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Verbindingstekenreeks | Een verbindingstekenreeks is een tekenreeks die informatie bevat over een gegevensbron en over de manier waarop u hiermee verbinding kunt maken. Het patroon van de verbindingstekenreeks voor [!DNL Teradata Vantage] is `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

Raadpleeg voor meer informatie over aan de slag gaan [[!DNL Teradata Vantage] document](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Verbind uw [!DNL Teradata Vantage] account

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder de [!UICONTROL Databases] categorie, selecteert u **[!UICONTROL Teradata Vantage]** en selecteer vervolgens **[!UICONTROL Add data]**.

![](../../../../images/tutorials/create/teradata/catalog.png)

De **[!UICONTROL Connect to Teradata Vantage]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de optie [!DNL Teradata Vantage] account waarmee u verbinding wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![](../../../../images/tutorials/create/teradata/existing.png)

### Nieuwe account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New account]**. Geef op het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Teradata Vantage] referenties. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![](../../../../images/tutorials/create/teradata/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw Teradata Vantage-account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens naar het Platform te brengen](../../dataflow/databases.md).
