---
keywords: Experience Platform;home;populaire onderwerpen;Teradata Vantage
title: Een Teradata Vantage Source Connection maken in de gebruikersinterface
description: Leer hoe u een Teradata Vantage-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# Een [!DNL Teradata Vantage] bronverbinding maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een [!DNL Teradata Vantage] bronaansluiting met behulp van de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [&#x200B; Sandboxes &#x200B;](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL Teradata Vantage] -account op Experience Platform, moet u de volgende verificatiewaarde opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Verbindingstekenreeks | Een verbindingstekenreeks is een tekenreeks die informatie bevat over een gegevensbron en over de manier waarop u hiermee verbinding kunt maken. Het patroon van de verbindingstekenreeks voor [!DNL Teradata Vantage] is `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}` . |

Voor meer informatie over begonnen worden, verwijs naar dit [[!DNL Teradata Vantage]  document &#x200B;](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Sluit uw [!DNL Teradata Vantage] -account aan

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie [!UICONTROL Databases] de optie **[!UICONTROL Teradata Vantage]** en selecteer vervolgens **[!UICONTROL Set up]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account bestaat, verandert deze optie in **[!UICONTROL Add data]** .

![&#x200B; de broncatalogus met de geselecteerde bron van de Vantage van Teradata.](../../../../images/tutorials/create/teradata/catalog.png)

De pagina **[!UICONTROL Connect to Teradata Vantage]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Teradata Vantage] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![&#x200B; de bestaande rekeningenpagina in de bronwerkruimte.](../../../../images/tutorials/create/teradata/existing.png)

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Teradata Vantage] -gegevens op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![&#x200B; de nieuwe interface van de rekeningsverwezenlijking in de bronwerkruimte.](../../../../images/tutorials/create/teradata/new.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding tot stand gebracht met uw Teradata Vantage-account. U kunt nu aan het volgende leerprogramma verdergaan en [&#x200B; een dataflow vormen om gegevens in Experience Platform &#x200B;](../../dataflow/databases.md) te brengen.
