---
keywords: Experience Platform;home;populaire onderwerpen;FTP;ftp
solution: Experience Platform
title: Een FTP Source-verbinding maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een FTP-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Een FTP-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
>De FTP-connector bevindt zich in bèta. Zie het [&#x200B; Bronoverzicht &#x200B;](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Deze zelfstudie bevat stappen voor het maken van een FTP-bronverbinding met de gebruikersinterface van Adobe Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige verbinding van FTP hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [&#x200B; vormend een dataflow &#x200B;](../../dataflow/batch/cloud-storage.md).

### Vereiste referenties verzamelen

Als u verbinding wilt maken met FTP, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De naam of het IP-adres dat aan uw FTP-server is gekoppeld. |
| `username` | De gebruikersnaam met toegang tot uw FTP-server. |
| `password` | Het wachtwoord voor uw FTP-server. |

## Verbinding maken met uw FTP-server

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om een nieuwe FTP-account te maken voor verbinding met Experience Platform.

Login aan [&#x200B; Adobe Experience Platform &#x200B;](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de [!UICONTROL Sources] werkruimte toegang te hebben. In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een inkomende account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie [!UICONTROL Cloud storage] de optie **[!UICONTROL FTP]** . Selecteer **[!UICONTROL Configure]** als dit de eerste keer is dat u deze connector gebruikt. Anders selecteert u **[!UICONTROL Add data]** om een nieuwe FTP-verbinding te maken.

![&#x200B; catalogus &#x200B;](../../../../images/tutorials/create/ftp/catalog.png)

De pagina **[!UICONTROL Connect to FTP]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Voer in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw referenties in. Als u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![&#x200B; nieuw &#x200B;](../../../../images/tutorials/create/ftp/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de FTP-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![&#x200B; bestaand &#x200B;](../../../../images/tutorials/create/ftp/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw FTP-account tot stand gebracht. U kunt nu aan het volgende leerprogramma verdergaan en [&#x200B; een dataflow vormen om gegevens van uw wolkenopslag in Experience Platform &#x200B;](../../dataflow/batch/cloud-storage.md) te brengen.
