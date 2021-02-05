---
keywords: Experience Platform;thuis;populaire onderwerpen; accounts verwijderen
description: De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het verwijderen van accounts in de werkruimte Bronnen.
solution: Experience Platform
title: Bronverbindingsaccounts verwijderen in de gebruikersinterface
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---


# Bronverbindingsaccounts verwijderen

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het verwijderen van accounts in de werkruimte **[!UICONTROL Bronnen]**.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../xdm/tutorials/create-schema-ui.md) Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## Accounts verwijderen via de gebruikersinterface

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer **[!UICONTROL Bronnen]** in de linkernavigatiebalk om de werkruimte **[!UICONTROL Bronnen]** te openen. Het scherm **[!UICONTROL Catalog]** toont een verscheidenheid van bronnen waarvoor u rekeningen en dataflows met kunt tot stand brengen. Elke bron toont het aantal bestaande rekeningen en gegevensstromen verbonden aan hen.

Selecteer **[!UICONTROL Accounts]** om tot de **[!UICONTROL Accounts]** pagina toegang te hebben.

![catalogusaccounts](../../images/tutorials/delete-accounts/catalog.png)

Er wordt een lijst met bestaande accounts weergegeven. Op deze pagina vindt u een lijst met sorteerbare gegevens voor bestaande accounts, zoals bron, gebruikersnaam, gekoppelde gegevens en gemaakte datum. Selecteer het **trechter-pictogram** linksboven om te sorteren.

![dataflows-list](../../images/tutorials/delete-accounts/accounts.png)

Het sorteervenster wordt aan de linkerkant van het scherm weergegeven met een lijst met beschikbare bronnen. Met de sorteerfunctie kunt u meerdere bronnen selecteren.

Selecteer de bron die u wilt openen en zoek de account die u wilt verwijderen uit de lijst met accounts in de hoofdinterface. In het voorbeeld is de geselecteerde bron **[!DNL Azure Blob Storage]** en de accountnaam is **[!UICONTROL blobTestConnector]**. Wanneer u meerdere bronnen selecteert in het sorteervenster, worden de laatst gemaakte accounts eerst weergegeven omdat de lijst is gesorteerd op de gemaakte datum.

Selecteer het account dat u wilt verwijderen.

![gegevensstroom sorteren](../../images/tutorials/delete-accounts/sort.png)

Het deelvenster **[!UICONTROL Eigenschappen]** wordt aan de rechterkant van het scherm weergegeven met informatie over de geselecteerde account.

Selecteer de ovalen (`...`) naast de naam van de account die u wilt verwijderen. Er wordt een pop-upvenster weergegeven met opties voor **[!UICONTROL Gegevens toevoegen]**, **[!UICONTROL Details bewerken]** en **[!UICONTROL Verwijderen]**. Selecteer **[!UICONTROL Delete]** om de account te verwijderen.

![gegevensstroom sorteren](../../images/tutorials/delete-accounts/delete.png)

Er verschijnt een laatste bevestigingsvenster. Selecteer **[!UICONTROL Verwijderen]** om het proces te voltooien.

![delete](../../images/tutorials/delete-accounts/confirm.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes **[!UICONTROL Bronnen]** werkruimte gebruikt om bestaande rekeningen te schrappen.

Raadpleeg de zelfstudie over [het verwijderen van verbindingen met de Flow Service API](../../tutorials/api/delete.md) voor informatie over het programmatisch uitvoeren van deze bewerkingen met de [!DNL Flow Service]-API