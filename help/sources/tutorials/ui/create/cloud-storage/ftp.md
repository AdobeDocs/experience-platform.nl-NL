---
keywords: Experience Platform;home;populaire onderwerpen;FTP;ftp
solution: Experience Platform
title: Een FTP-bronverbinding maken in de gebruikersinterface
topic: overview
type: Tutorial
description: Leer hoe u een FTP-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '463'
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

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatiebalk om de werkruimte [!UICONTROL Bronnen] te openen. Het scherm [!UICONTROL Catalog] toont een verscheidenheid van bronnen waarvoor u een binnenkomende rekening kunt tot stand brengen met.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL FTP]** onder de categorie [!UICONTROL Cloudopslag]. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders selecteert u **[!UICONTROL Gegevens toevoegen]** om een nieuwe FTP-verbinding te maken.

![catalogus](../../../../images/tutorials/create/ftp/catalog.png)

De pagina **[!UICONTROL Verbinding maken met FTP]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Als u nieuwe geloofsbrieven gebruikt, selecteer **[!UICONTROL Nieuwe rekening]**. Voer in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw referenties in. Selecteer **[!UICONTROL Connect]** als u klaar bent en wacht dan enige tijd tot de nieuwe verbinding tot stand is gebracht.

![new](../../../../images/tutorials/create/ftp/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de FTP-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/ftp/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw FTP-account tot stand gebracht. U kunt nu verdergaan naar de volgende zelfstudie en [een gegevensstroom configureren om gegevens van uw cloudopslag naar Platform te brengen](../../dataflow/batch/cloud-storage.md).