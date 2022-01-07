---
keywords: Experience Platform;thuis;populaire onderwerpen; accounts verwijderen
description: De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het verwijderen van accounts in de werkruimte Bronnen.
solution: Experience Platform
title: Bronverbindingsaccounts verwijderen in de gebruikersinterface
topic-legacy: overview
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 609f7a5de51840fe657ca72df99c90da56c8f466
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Bronverbindingsaccounts verwijderen

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie bevat stappen voor het verwijderen van accounts uit de **[!UICONTROL Sources]** werkruimte.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Systeem](../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   - [Basisbeginselen van de schemacompositie](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie Schema Editor](../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## Accounts verwijderen via de gebruikersinterface

>[!TIP]
>
>Voordat u de bronaccount verwijdert, moet u eerst bestaande gegevensstromen verwijderen die aan de bronaccount zijn gekoppeld. Raadpleeg de zelfstudie over het verwijderen van bestaande gegevensstromen [het schrappen van bronnen dataflows in UI](./delete.md).

Aanmelden bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de **[!UICONTROL Sources]** werkruimte. De **[!UICONTROL Catalog]** het scherm toont een verscheidenheid van bronnen waarvoor u rekeningen en gegevensstromen kunt tot stand brengen met. Elke bron toont het aantal bestaande rekeningen en gegevensstromen verbonden aan hen.

Selecteren **[!UICONTROL Accounts]** toegang tot **[!UICONTROL Accounts]** pagina.

![catalogusaccounts](../../images/tutorials/delete-accounts/catalog.png)

Er wordt een lijst met bestaande accounts weergegeven. Op deze pagina vindt u een lijst met sorteerbare gegevens voor bestaande accounts, zoals bron, gebruikersnaam, gekoppelde gegevens en gemaakte datum. Selecteer **Trechter-pictogram** bovenaan links om te sorteren.

![dataflows-list](../../images/tutorials/delete-accounts/accounts.png)

Het sorteervenster wordt aan de linkerkant van het scherm weergegeven met een lijst met beschikbare bronnen. Met de sorteerfunctie kunt u meerdere bronnen selecteren.

Selecteer de bron die u wilt openen en zoek de account die u wilt verwijderen uit de lijst met accounts in de hoofdinterface. In het voorbeeld is de geselecteerde bron **[!DNL Azure Blob Storage]** en de accountnaam **[!UICONTROL blobTestConnector]**. Wanneer u meerdere bronnen selecteert in het sorteervenster, worden de laatst gemaakte accounts eerst weergegeven omdat de lijst is gesorteerd op de gemaakte datum.

Selecteer het account dat u wilt verwijderen.

![gegevensstroom sorteren](../../images/tutorials/delete-accounts/sort.png)

De **[!UICONTROL Properties]** wordt aan de rechterkant van het scherm weergegeven met informatie over de geselecteerde account.

De ovalen selecteren (`...`) naast de naam van de account die u wilt verwijderen. Er verschijnt een pop-upvenster met opties voor **[!UICONTROL Add data]**, **[!UICONTROL Edit details]**, en **[!UICONTROL Delete]**. Selecteren **[!UICONTROL Delete]** om de account te verwijderen.

![gegevensstroom sorteren](../../images/tutorials/delete-accounts/delete.png)

Er verschijnt een laatste bevestigingsvenster. Selecteer **[!UICONTROL Delete]** om het proces te voltooien.

![delete](../../images/tutorials/delete-accounts/confirm.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de opdracht **[!UICONTROL Sources]** werkruimte om bestaande accounts te verwijderen.

Voor stappen op hoe te om deze verrichtingen programmatically uit te voeren gebruikend [!DNL Flow Service] API, raadpleeg de zelfstudie op [verbindingen verwijderen met de Flow Service API](../../tutorials/api/delete.md)
