---
keywords: Experience Platform;home;populaire onderwerpen; accounts verwijderen
description: Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde gegevens in te voeren. Deze zelfstudie biedt stappen voor het verwijderen van accounts in de werkruimte Bronnen.
solution: Experience Platform
title: Source Connection Accounts verwijderen in de gebruikersinterface
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Bronverbindingsaccounts verwijderen

Source-connectors in Adobe Experience Platform bieden de mogelijkheid om volgens een schema extern gesourceerde gegevens in te voeren. Deze zelfstudie bevat stappen voor het verwijderen van accounts uit de werkruimte van **[!UICONTROL Sources]** .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]  Systeem ](../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   - [ Grondbeginselen van schemacompositie ](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [ het leerprogramma van de Redacteur van het Schema ](../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

## Accounts verwijderen via de gebruikersinterface

>[!TIP]
>
>Voordat u de bronaccount verwijdert, moet u eerst bestaande gegevensstromen verwijderen die aan de bronaccount zijn gekoppeld. Om bestaande dataflows te schrappen, verwijs naar het leerprogramma bij [ het schrappen van brondataflows in UI ](./delete.md).

Login aan [ Adobe Experience Platform ](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarvoor u accounts en gegevensstromen kunt maken. Elke bron toont het aantal bestaande rekeningen en gegevensstromen verbonden aan hen.

Selecteer **[!UICONTROL Accounts]** om de pagina van **[!UICONTROL Accounts]** te openen.

![ catalogus-rekeningen ](../../images/tutorials/delete-accounts/catalog.png)

Er wordt een lijst met bestaande accounts weergegeven. Op deze pagina vindt u een lijst met sorteerbare gegevens voor bestaande accounts, zoals bron, gebruikersnaam, gekoppelde gegevens en gemaakte datum. Selecteer het **kanaalpictogram** op de bovenkant verlaten aan soort.

![ dataflows-list ](../../images/tutorials/delete-accounts/accounts.png)

Het sorteervenster wordt aan de linkerkant van het scherm weergegeven met een lijst met beschikbare bronnen. Met de sorteerfunctie kunt u meerdere bronnen selecteren.

Selecteer de bron die u wilt openen en zoek de account die u wilt verwijderen uit de lijst met accounts in de hoofdinterface. In het voorbeeld is de geselecteerde bron **[!DNL Azure Blob Storage]** en is de naam van de account **[!UICONTROL blobTestConnector]** . Wanneer u meerdere bronnen selecteert in het sorteervenster, worden de laatst gemaakte accounts eerst weergegeven omdat de lijst is gesorteerd op de gemaakte datum.

Selecteer het account dat u wilt verwijderen.

![ dataflows-sort ](../../images/tutorials/delete-accounts/sort.png)

Het deelvenster **[!UICONTROL Properties]** wordt aan de rechterkant van het scherm weergegeven met informatie over de geselecteerde account.

Selecteer de ovalen (`...`) naast de naam van de account die u wilt verwijderen. Er wordt een pop-upvenster weergegeven met opties voor **[!UICONTROL Add data]** , **[!UICONTROL Edit details]** en **[!UICONTROL Delete]** . Selecteer **[!UICONTROL Delete]** om het account te verwijderen.

![ dataflows-sort ](../../images/tutorials/delete-accounts/delete.png)

Er wordt een laatste bevestigingsvenster weergegeven. Selecteer **[!UICONTROL Delete]** om het proces te voltooien.

![ schrapping ](../../images/tutorials/delete-accounts/confirm.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de werkruimte van **[!UICONTROL Sources]** gebruikt om bestaande accounts te verwijderen.

Voor stappen op hoe te om deze verrichtingen programmatically uit te voeren gebruikend [!DNL Flow Service] API, te verwijzen gelieve naar het leerprogramma op [ het schrappen van verbindingen gebruikend de Dienst API van de Stroom ](../../tutorials/api/delete.md)
