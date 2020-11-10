---
keywords: Experience Platform;home;popular topics;Phoenix;phoenix
solution: Experience Platform
title: Een Phoenix-bronaansluiting maken in de gebruikersinterface
topic: overview
type: Tutorial
description: Deze zelfstudie bevat stappen voor het maken van een Phoenix-bronaansluiting met behulp van de gebruikersinterface van het Platform.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Creeer een [!DNL Phoenix] bronschakelaar in UI

>[!NOTE]
>
> De [!DNL Phoenix] connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het maken van een [!DNL Phoenix] bronaansluiting met behulp van de [!DNL Platform] gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie](../../../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige [!DNL Phoenix] verbinding hebt, kunt u de rest van dit document overslaan en naar de zelfstudie gaan over het [configureren van een gegevensstroom](../../dataflow/databases.md)

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL Phoenix] [!DNL Platform]account op, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het IP-adres of de hostnaam van de [!DNL Phoenix] server. |
| `port` | De TCP-poort die de [!DNL Phoenix] server gebruikt om te luisteren naar clientverbindingen. Als u verbinding maakt met [!DNL Azure HDInsights], geeft u de poort op als 443. |
| `httpPath` | De gedeeltelijke URL die overeenkomt met de [!DNL Phoenix] server. Specificeer /basephoenix0 als u de [!DNL Azure HDInsights] cluster gebruikt. |
| `username` | De gebruikersnaam die u gebruikt om toegang te krijgen tot de [!DNL Phoenix] server. |
| `password` | Het wachtwoord dat overeenkomt met de gebruiker. |
| `enableSsl` | Een schakeloptie waarmee wordt opgegeven of de verbindingen met de server via SSL zijn gecodeerd. |

Raadpleeg [ [!DNL Phoenix] dit document](https://python-phoenixdb.readthedocs.io/en/latest/api.html)voor meer informatie over aan de slag gaan.

## Uw [!DNL Phoenix] account verbinden

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Phoenix] account te koppelen aan [!DNL Platform].

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte **[!UICONTROL Bronnen]** . In het scherm **[!UICONTROL Catalogus]** worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!UICONTROL Phoenix onder de categorie]** Databases ****. Als dit uw eerste keer gebruikend deze schakelaar is, uitgezocht **[!UICONTROL vorm]**. Anders selecteert u Gegevens **** toevoegen om een nieuw [!DNL Phoenix] account te maken.

![catalogus](../../../../images/tutorials/create/phoenix/catalog.png)

De pagina **[!UICONTROL Verbinding maken met Phoenix]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Nieuwe account

Selecteer **[!UICONTROL Nieuw account]** als u nieuwe referenties gebruikt. Voer in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw [!DNL Phoenix] referenties in. Wanneer u klaar bent, selecteert u **[!UICONTROL Connect]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![verbinden](../../../../images/tutorials/create/phoenix/new.png)

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de [!DNL Phoenix] account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Volgende]** om door te gaan.

![bestaand](../../../../images/tutorials/create/phoenix/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding met uw [!DNL Phoenix] account tot stand gebracht. U kunt nu verdergaan naar de volgende zelfstudie en een gegevensstroom [configureren om gegevens in te voeren [!DNL Platform]](../../dataflow/databases.md).