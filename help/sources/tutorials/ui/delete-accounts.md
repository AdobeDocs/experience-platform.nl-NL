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

- [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   - [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

## Accounts verwijderen via de gebruikersinterface

>[!TIP]
>
>Voordat u de bronaccount verwijdert, moet u eerst bestaande gegevensstromen verwijderen die aan de bronaccount zijn gekoppeld. Om bestaande dataflows te schrappen, verwijs naar het leerprogramma bij [&#x200B; het schrappen van brondataflows in UI &#x200B;](./delete.md).

Login aan [&#x200B; Adobe Experience Platform &#x200B;](https://platform.adobe.com) en selecteer dan **[!UICONTROL Sources]** van de linkernavigatiebar om tot de **[!UICONTROL Sources]** werkruimte toegang te hebben. In het scherm **[!UICONTROL Catalog]** worden diverse bronnen weergegeven waarvoor u accounts en gegevensstromen kunt maken. Elke bron toont het aantal bestaande rekeningen en gegevensstromen verbonden aan hen.

Selecteer **[!UICONTROL Accounts]** om de pagina van **[!UICONTROL Accounts]** te openen.

![&#x200B; catalogus-rekeningen &#x200B;](../../images/tutorials/delete-accounts/catalog.png)

Er wordt een lijst met bestaande accounts weergegeven. Op deze pagina vindt u een lijst met sorteerbare gegevens voor bestaande accounts, zoals bron, gebruikersnaam, gekoppelde gegevens en gemaakte datum. Selecteer het **kanaalpictogram** op de bovenkant verlaten aan soort.

![&#x200B; dataflows-list &#x200B;](../../images/tutorials/delete-accounts/accounts.png)

Het sorteervenster wordt aan de linkerkant van het scherm weergegeven met een lijst met beschikbare bronnen. Met de sorteerfunctie kunt u meerdere bronnen selecteren.

Selecteer de bron die u wilt openen en zoek de account die u wilt verwijderen uit de lijst met accounts in de hoofdinterface. In het voorbeeld is de geselecteerde bron **[!DNL Azure Blob Storage]** en is de naam van de account **[!UICONTROL blobTestConnector]** . Wanneer u meerdere bronnen selecteert in het sorteervenster, worden de laatst gemaakte accounts eerst weergegeven omdat de lijst is gesorteerd op de gemaakte datum.

Selecteer het account dat u wilt verwijderen.

![&#x200B; dataflows-sort &#x200B;](../../images/tutorials/delete-accounts/sort.png)

Het deelvenster **[!UICONTROL Properties]** wordt aan de rechterkant van het scherm weergegeven met informatie over de geselecteerde account.

Selecteer de ovalen (`...`) naast de naam van de account die u wilt verwijderen. Er wordt een pop-upvenster weergegeven met opties voor **[!UICONTROL Add data]** , **[!UICONTROL Edit details]** en **[!UICONTROL Delete]** . Selecteer **[!UICONTROL Delete]** om het account te verwijderen.

![&#x200B; dataflows-sort &#x200B;](../../images/tutorials/delete-accounts/delete.png)

Er wordt een laatste bevestigingsvenster weergegeven. Selecteer **[!UICONTROL Delete]** om het proces te voltooien.

![&#x200B; schrapping &#x200B;](../../images/tutorials/delete-accounts/confirm.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de werkruimte van **[!UICONTROL Sources]** gebruikt om bestaande accounts te verwijderen.

Voor stappen op hoe te om deze verrichtingen programmatically uit te voeren gebruikend [!DNL Flow Service] API, te verwijzen gelieve naar het leerprogramma op [&#x200B; het schrappen van verbindingen gebruikend de Dienst API van de Stroom &#x200B;](../../tutorials/api/delete.md)
