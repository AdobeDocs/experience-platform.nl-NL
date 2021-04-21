---
keywords: Experience Platform;home;populaire onderwerpen;FTP;ftp
solution: Experience Platform
title: Een FTP-bronverbinding maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een FTP-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Een FTP-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
>De FTP-connector bevindt zich in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Deze zelfstudie bevat stappen voor het maken van een FTP-bronverbinding met de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige FTP-verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie over [het configureren van een gegevensstroom](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Als u verbinding wilt maken met FTP, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De naam of het IP-adres dat aan uw FTP-server is gekoppeld. |
| `username` | De gebruikersnaam met toegang tot uw FTP-server. |
| `password` | Het wachtwoord voor uw FTP-server. |

## Verbinding maken met uw FTP-server

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om een nieuwe FTP-account te maken waarmee u verbinding kunt maken met het Platform.

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Sources]** in de linkernavigatiebalk om de werkruimte [!UICONTROL Sources] te openen. Het scherm [!UICONTROL Catalog] toont een verscheidenheid van bronnen waarvoor u een binnenkomende rekening kunt tot stand brengen met.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL FTP]** onder de categorie [!UICONTROL Cloud storage]. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL Configure]**. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe FTP-verbinding te maken.

![catalogus](../../../../images/tutorials/create/ftp/catalog.png)

De pagina **[!UICONTROL Connect to FTP]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, uitgezocht **[!UICONTROL New account]**. Voer in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw referenties in. Wanneer gebeëindigd, selecteer **[!UICONTROL Connect]** en laat dan wat tijd voor de nieuwe verbinding toe om te vestigen.

![new](../../../../images/tutorials/create/ftp/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de FTP-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![bestaand](../../../../images/tutorials/create/ftp/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw FTP-account tot stand gebracht. U kunt nu verdergaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag naar Platform te brengen](../../dataflow/batch/cloud-storage.md).
