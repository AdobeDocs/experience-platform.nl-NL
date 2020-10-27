---
keywords: Experience Platform;home;popular topics; delete dataflows
description: De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het verwijderen van gegevensstromen uit de werkruimte Bronnen.
solution: Experience Platform
title: Gegevensstromen verwijderen
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: cbd9b3ed0cf43d582d734098b9ce58fc074fb375
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# Gegevensstromen verwijderen

De bronschakelaars in Adobe Experience Platform verstrekken de capaciteit om van buitenaf afkomstige gegevens op een geplande basis in te voeren. Deze zelfstudie biedt stappen voor het verwijderen van gegevensstromen uit de werkruimte **[!UICONTROL Bronnen]** .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Systeem](../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   - [Basisbeginselen van de schemacompositie](../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   - [Zelfstudie](../../../xdm/tutorials/create-schema-ui.md)Schema-editor: Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## Gegevensstromen verwijderen met behulp van de gebruikersinterface

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte **[!UICONTROL Bronnen]** . In het scherm **[!UICONTROL Catalogus]** worden diverse bronnen weergegeven waarvoor u accounts en gegevensstromen kunt maken. Elke bron toont het aantal bestaande rekeningen en gegevensstromen verbonden aan hen.

Selecteer **[!UICONTROL Gegevensstromen]** om tot de pagina **[!UICONTROL Dataflows]** toegang te hebben.

![dataset-flow-activity](../../images/tutorials/delete/dataflows.png)

Er wordt een lijst met bestaande gegevensstromen weergegeven. Op deze pagina vindt u een lijst met sorteerbare gegevens voor bestaande gegevensstromen, zoals bron, gebruikersnaam, uitvoerstatus en datum van laatste uitvoering. Selecteer het **trechter-pictogram** linksboven om te sorteren.

![dataflows-list](../../images/tutorials/delete/dataflows-list.png)

Het sorteervenster wordt aan de linkerkant van het scherm weergegeven met een lijst met beschikbare bronnen.
Met de sorteerfunctie kunt u meerdere bronnen selecteren.

Selecteer de bron die u wilt openen en zoek de gegevensstroom die u wilt verwijderen uit de lijst met gegevensstromen in de hoofdinterface. In het voorbeeld is de geselecteerde bron **[!DNL Azure Blob Storage]** en is de naam van de gegevensstroom **[!UICONTROL Klantprofielen dataflow]**. Wanneer u meerdere bronnen selecteert in het sorteervenster, worden de meest recent gemaakte gegevensstromen eerst weergegeven omdat de lijst is gesorteerd op de gemaakte datum.

Selecteer de gegevensstroom die u wilt verwijderen.

![gegevensstroom sorteren](../../images/tutorials/delete/dataflows-sort.png)

Het deelvenster **[!UICONTROL Eigenschappen]** wordt aan de rechterkant van het scherm weergegeven met informatie over de geselecteerde gegevensstroom en een optie voor het **[!UICONTROL bewerken van het schema]**.

Selecteer **[!UICONTROL Verwijderen]** om de gegevensstroom te verwijderen.

![gegevensstroom sorteren](../../images/tutorials/delete/dataflows-properties.png)

Er wordt een laatste bevestigingsvenster weergegeven. Selecteer **[!UICONTROL Verwijderen]** om het proces te voltooien.

![delete](../../images/tutorials/delete/delete.png)

Na enkele ogenblikken verschijnt er een groen bevestigingsvak onder aan het scherm om te bevestigen dat het verwijderen is gelukt.

![bevestigd](../../images/tutorials/delete/confirmed.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes de werkruimte **[!UICONTROL Bronnen]** gebruikt om bestaande gegevensstromen te schrappen.

Raadpleeg de zelfstudie over het [!DNL Flow Service] verwijderen van verbindingen met de Flow Service API voor informatie over hoe u deze bewerkingen programmatisch kunt uitvoeren met de [API.](../../tutorials/api/delete.md)