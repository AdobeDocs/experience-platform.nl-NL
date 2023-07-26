---
title: Uw Phoenix-account aansluiten via de gebruikersinterface van het Experience Platform
description: Leer hoe u uw Phoenix-account koppelt en gegevens uit uw Phoenix-database naar het Experience Platform brengt via de gebruikersinterface.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: b7e42eb180b8f16344afedadf763c33bcf22fa35
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 1%

---

# Verbind uw [!DNL Phoenix] account aan Experience Platform met behulp van de gebruikersinterface

Deze zelfstudie bevat stappen voor het tot stand brengen van een verbinding met uw [!DNL Phoenix] account en gegevens van uw [!DNL Phoenix] database naar Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u al een geverifieerde [!DNL Phoenix] -account, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [het vormen van een gegevensstroom voor een gegevensbestand](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Voor toegang tot uw [!DNL Phoenix] account op Experience Platform, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| --- | --- |
| Host | Het IP adres of hostnaam van [!DNL Phoenix] server. |
| Poort | De TCP-poort die de [!DNL Phoenix] server gebruikt om naar clientverbindingen te luisteren. Als u verbinding maakt met [!DNL Azure HDInsights]en geeft u de poort op als 443. Als deze parameter niet wordt opgegeven, wordt de standaardwaarde 8765 gebruikt. |
| HTTP-pad | De gedeeltelijke URL die overeenkomt met de [!DNL Phoenix] server. Geef /hbasephoenix0 op als u de [!DNL Azure HDInsights] cluster. |
| Gebruikersnaam | De gebruikersnaam die u gebruikt om toegang te krijgen tot de [!DNL Phoenix] server. |
| Wachtwoord | Het wachtwoord dat overeenkomt met de gebruiker. |
| SSL inschakelen | Een schakeloptie waarmee wordt opgegeven of de verbindingen met de server via SSL zijn gecodeerd. |

Raadpleeg voor meer informatie over aan de slag gaan [dit [!DNL Phoenix] document](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om verbinding te maken met uw [!DNL Phoenix] aan Experience Platform.

## Verbind uw [!DNL Phoenix] account

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot de bronwerkruimte toegang te hebben. De *[!UICONTROL Catalog]* het scherm toont een verscheidenheid van bronnen beschikbaar in de catalogus van bronnen van het Experience Platform.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook een specifieke bron zoeken met de zoekoptie.

Selecteren **[!UICONTROL Databases]** in de lijst met categorieën bronnen en selecteer vervolgens **[!UICONTROL Add data]** van de [!DNL Phoenix] kaart.

>[!TIP]
>
>De bronnen in de broncatalogus kunnen verschillende herinneringen afhankelijk van de status van de bron tonen.
> 
>* **[!UICONTROL Add data]** betekent dat er bestaande geverifieerde accounts zijn gekoppeld aan de geselecteerde bron.
>
>* **[!UICONTROL Set up]** Dit betekent dat u gebruikersgegevens moet opgeven en een nieuw account moet verifiëren om de geselecteerde bron te kunnen gebruiken.

![De broncatalogus in de gebruikersinterface van het Experience Platform met de Phoenix-bronkaart geselecteerd.](../../../../images/tutorials/create/phoenix/catalog.png)

De **[!UICONTROL Connect to Phoenix]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

>[!BEGINTABS]

>[!TAB Een bestaande Phoenix-account gebruiken]

Als u een bestaande account wilt gebruiken, selecteert u [!UICONTROL Existing account] en selecteer vervolgens de account die u wilt gebruiken in de lijst die wordt weergegeven. Selecteer [!UICONTROL Next] om verder te gaan.

![Een lijst met geverifieerde Phoenix-databaseaccounts die al in uw organisatie bestaan.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB Een nieuwe Phoenix-account maken]

Als u een nieuwe account wilt gebruiken, selecteert u [!UICONTROL New account] en geef een naam, beschrijving en uw [!DNL Phoenix] verificatiegegevens. Selecteer [!UICONTROL Connect to source] en wacht een paar seconden tot de nieuwe verbinding tot stand is gebracht.

![De nieuwe accountinterface waarin u verificatiegegevens kunt opgeven en een Phoenix-account kunt maken.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Phoenix] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens naar het Experience Platform te brengen](../../dataflow/databases.md).
