---
keywords: Experience Platform;home;populaire onderwerpen;Azure HDInsights;Apache Spark
solution: Experience Platform
title: Een Apache Spark maken op Azure HDInsights Source Connection in de gebruikersinterface
type: Tutorial
description: Leer hoe u een Apache Spark maakt op de Azure HDInsights-bronverbinding met de Adobe Experience Platform-gebruikersinterface.
exl-id: 30d0b740-cec4-486f-9c9b-1579fd04f28b
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Een [!DNL Apache Spark] on [!DNL Azure HDInsights] -bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
> De [!DNL Apache Spark] on [!DNL Azure HDInsights] -connector bevindt zich in bèta. Zie het [ Bronoverzicht ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Apache Spark] on [!DNL Azure HDInsights] -bronconnector met behulp van de [!DNL Platform] -gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Model van de Gegevens van de Ervaring (XDM) Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [ Real-Time Profiel van de Klant ](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een geldige [!DNL Spark] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/databases.md)

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL Spark] account op [!DNL Platform] , moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het IP-adres of de hostnaam van de [!DNL Spark] -server. |
| `username` | De gebruikersnaam die u gebruikt voor toegang tot de [!DNL Spark] -server. |
| `password` | Het wachtwoord dat overeenkomt met de gebruiker. |

Voor meer informatie over begonnen worden, verwijs naar [ dit document van Vonk ](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

## Sluit uw [!DNL Spark] -account aan

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Spark] -account te koppelen aan [!DNL Platform] .

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Databases]** de optie **[!UICONTROL Spark]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe [!DNL Spark] -connector te maken.

![ catalogus ](../../../../images/tutorials/create/spark/catalog.png)

De pagina **[!UICONTROL Connect to Spark]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Spark] -gegevens op. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ nieuw ](../../../../images/tutorials/create/spark/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Spark] -account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![ bestaand ](../../../../images/tutorials/create/spark/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Spark] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in  [!DNL Platform]](../../dataflow/databases.md) te brengen.
