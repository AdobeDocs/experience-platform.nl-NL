---
title: Uw Phoenix-account aansluiten via de gebruikersinterface van het Experience Platform
description: Leer hoe u uw Phoenix-account koppelt en gegevens uit uw Phoenix-database naar het Experience Platform brengt via de gebruikersinterface.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Sluit uw [!DNL Phoenix] -account aan op het Experience Platform via de gebruikersinterface

>[!WARNING]
>
>De bron [!DNL Phoenix] wordt eind mei 2025 vervangen.

Deze zelfstudie bevat stappen voor het tot stand brengen van een verbinding tussen uw [!DNL Phoenix] -account en het naar Experience Platform brengen van gegevens uit uw [!DNL Phoenix] -database.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een voor authentiek verklaarde [!DNL Phoenix] rekening hebt, dan kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow voor een gegevensbestand ](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL Phoenix] -account op Experience Platform, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| --- | --- |
| Host | Het IP-adres of de hostnaam van de [!DNL Phoenix] -server. |
| Poort | De TCP-poort die de [!DNL Phoenix] -server gebruikt om te luisteren naar clientverbindingen. Als u verbinding maakt met [!DNL Azure HDInsights] , geeft u de poort op als 443. Als deze parameter niet wordt opgegeven, wordt de standaardwaarde 8765 gebruikt. |
| HTTP-pad | De gedeeltelijke URL die overeenkomt met de [!DNL Phoenix] -server. Geef /hbasephoenix0 op als u de [!DNL Azure HDInsights] -cluster gebruikt. |
| Gebruikersnaam | De gebruikersnaam die u gebruikt voor toegang tot de [!DNL Phoenix] -server. |
| Wachtwoord | Het wachtwoord dat overeenkomt met de gebruiker. |
| SSL inschakelen | Een schakeloptie waarmee wordt opgegeven of de verbindingen met de server via SSL zijn gecodeerd. |

Voor meer informatie over begonnen worden, verwijs naar [ dit  [!DNL Phoenix]  document ](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL Phoenix] -account te verbinden met het Experience Platform.

## Sluit uw [!DNL Phoenix] -account aan

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte Bronnen. In het scherm *[!UICONTROL Catalog]* worden diverse bronnen weergegeven die beschikbaar zijn in de catalogus met bronnen in het Experience Platform.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook een specifieke bron zoeken met de zoekoptie.

Selecteer **[!UICONTROL Databases]** in de lijst met categorieën bronnen en kies vervolgens **[!UICONTROL Add data]** in de [!DNL Phoenix] -kaart.

>[!TIP]
>
>De bronnen in de broncatalogus kunnen verschillende herinneringen afhankelijk van de status van de bron tonen.
> 
>* **[!UICONTROL Add data]** betekent dat er bestaande geverifieerde accounts zijn gekoppeld aan de geselecteerde bron.
>
>* **[!UICONTROL Set up]** betekent dat u gebruikersgegevens moet opgeven en een nieuw account moet verifiëren om de geselecteerde bron te kunnen gebruiken.

![ de broncatalogus op het Experience Platform UI met de Phoenix geselecteerde bronkaart.](../../../../images/tutorials/create/phoenix/catalog.png)

De pagina **[!UICONTROL Connect to Phoenix]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

>[!BEGINTABS]

>[!TAB  Gebruik een bestaande rekening Phoenix ]

Als u een bestaande account wilt gebruiken, selecteert u [!UICONTROL Existing account] en selecteert u vervolgens de account die u wilt gebruiken in de lijst die wordt weergegeven. Als u klaar bent, selecteert u [!UICONTROL Next] om door te gaan.

![ een lijst van voor authentiek verklaarde Phoenix- gegevensbestandrekeningen die reeds in uw organisatie bestaan.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB  creeer een nieuwe rekening Phoenix ]

Als u een nieuwe account wilt gebruiken, selecteert u [!UICONTROL New account] en geeft u een naam, beschrijving en verificatiegegevens van [!DNL Phoenix] op. Selecteer [!UICONTROL Connect to source] als u klaar bent en wacht een paar seconden totdat de nieuwe verbinding tot stand is gebracht.

![ de nieuwe rekeningsinterface waar u authentificatiegeloofsbrieven kunt verstrekken en een rekening tot stand brengen Phoenix.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Phoenix] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in Experience Platform ](../../dataflow/databases.md) te brengen.
