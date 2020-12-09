---
keywords: Experience Platform;home;popular topics; delete dataflows
description: De werkruimte Bronnen biedt u de mogelijkheid om bestaande batch- en streaming gegevensstromen te verwijderen die fouten bevatten of verouderd zijn.
solution: Experience Platform
title: Gegevensstromen verwijderen
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 7cb5862112c80e386e697aa2bd503abe49f11a3f
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 1%

---


# Gegevensstromen verwijderen in de gebruikersinterface

Met de werkruimte [!UICONTROL Bronnen] kunt u bestaande batch- en streaming-gegevensstromen verwijderen die fouten bevatten of verouderd zijn.

Dit leerprogramma verstrekt stappen voor het schrappen van gegevensstromen gebruikend de [!UICONTROL werkruimte van Bronnen] .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [Bronnen](../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten.
- [Sandboxen](../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Gegevensstromen verwijderen

In het [Experience Platform UI](https://platform.adobe.com), uitgezochte **[!UICONTROL Bronnen]** van de linkernavigatie om tot de [!UICONTROL Bronwerkruimte] toegang te hebben, en dan **[!UICONTROL Dataflows]** van de hoogste kopbal te selecteren.

![catalogus](../../images/tutorials/delete/catalog.png)

De pagina **[!UICONTROL Gegevensstroom]** wordt weergegeven. Op deze pagina is een lijst van viewable gegevensstromen, met inbegrip van informatie over hun doeldataset, bron, rekeningsnaam, en datum van verwezenlijking.

Selecteer het filterpictogram (![filter-pictogram](../../images/tutorials/delete/filter.png)) linksboven om het deelvenster Sorteren te starten.

![dataflows](../../images/tutorials/delete/dataflows.png)

Het deelvenster Sorteren bevat een lijst met alle bronnen. U kunt meer dan één bron van de lijst selecteren om tot een gefilterde selectie van gegevensstromen toegang te hebben verbonden aan de bijzondere bronnen u selecteerde.

Selecteer de bron waarmee u wilt werken om een lijst met de bestaande gegevensstromen te zien. Nadat u de gegevensstroom hebt geïdentificeerd die u wilt verwijderen, selecteert u de ovalen (`...`) naast de naam van de gegevensstroom.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Er wordt een vervolgkeuzemenu weergegeven waarin u opties kunt opgeven om het schema van uw gegevensstroom te bewerken, de gegevensstroom uit te schakelen of deze volledig te verwijderen.

Selecteer **[!UICONTROL Verwijderen]** om de gegevensstroom te verwijderen.

![delete](../../images/tutorials/delete/delete.png)

Er wordt een laatste bevestigingsvenster weergegeven. Selecteer **[!UICONTROL Verwijderen]** om het proces te voltooien.

![bevestigen](../../images/tutorials/delete/confirm.png)

Na enkele ogenblikken wordt onder aan het scherm een bevestigingsvak weergegeven om te bevestigen dat het verwijderen is gelukt.

![bevestigd](../../images/tutorials/delete/confirmed.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes de werkruimte [!UICONTROL Bronnen] gebruikt om een bestaande gegevensstroom te schrappen.

Zie de zelfstudie over het [verwijderen van gegevensstromen met behulp van de Flow Service API](../../tutorials/api/delete-dataflows.md) voor stappen over hoe u deze bewerkingen programmatisch kunt uitvoeren met behulp van API-aanroepen.