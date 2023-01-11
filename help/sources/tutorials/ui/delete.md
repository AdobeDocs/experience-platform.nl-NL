---
keywords: Experience Platform;thuis;populaire onderwerpen; gegevensstroom verwijderen
description: De werkruimte Bronnen biedt u de mogelijkheid om bestaande batch- en streaming gegevensstromen te verwijderen die fouten bevatten of verouderd zijn.
solution: Experience Platform
title: Gegevensstromen verwijderen in de gebruikersinterface
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---

# Gegevensstromen verwijderen in de gebruikersinterface

De [!UICONTROL Sources] kunt u bestaande batch- en streaminggegevens met fouten verwijderen of verouderd zijn.

Deze zelfstudie bevat stappen voor het verwijderen van gegevensstromen met behulp van de [!UICONTROL Sources] werkruimte.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [Bronnen](../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
- [Sandboxen](../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Gegevensstromen verwijderen

In de [UI Experience Platform](https://platform.adobe.com), selecteert u **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte en selecteer vervolgens **[!UICONTROL Dataflows]** in de bovenste koptekst.

![catalogus](../../images/tutorials/delete/catalog.png)

De **[!UICONTROL Dataflows]** wordt weergegeven. Op deze pagina is een lijst van viewable gegevensstromen, met inbegrip van informatie over hun doeldataset, bron, rekeningsnaam, en datum van verwezenlijking.

Selecteer het filterpictogram (![filter-icon](../../images/tutorials/delete/filter.png)) linksboven om het deelvenster Sorteren te starten.

![dataflows](../../images/tutorials/delete/dataflows.png)

Het deelvenster Sorteren bevat een lijst met alle bronnen. U kunt meer dan één bron van de lijst selecteren om tot een gefilterde selectie van gegevensstromen toegang te hebben verbonden aan de bijzondere bronnen u selecteerde.

Selecteer de bron waarmee u wilt werken om een lijst met de bestaande gegevensstromen te zien. Nadat u de gegevensstroom hebt geïdentificeerd die u wilt verwijderen, selecteert u de ellipsen (`...`) naast de naam van de gegevensstroom.

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

Er wordt een vervolgkeuzemenu weergegeven waarin u opties kunt opgeven om het schema van uw gegevensstroom te bewerken, de gegevensstroom uit te schakelen of deze volledig te verwijderen.

Selecteren **[!UICONTROL Delete]** om de gegevensstroom te verwijderen.

![delete](../../images/tutorials/delete/delete.png)

Er wordt een laatste bevestigingsvenster weergegeven. Selecteren **[!UICONTROL Delete]** om het proces te voltooien.

![bevestigen](../../images/tutorials/delete/confirm.png)

Na enkele ogenblikken wordt onder aan het scherm een bevestigingsvak weergegeven om te bevestigen dat het verwijderen is gelukt.

![bevestigd](../../images/tutorials/delete/confirmed.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de opdracht [!UICONTROL Sources] om een bestaande gegevensstroom te verwijderen.

Zie de zelfstudie aan [het schrappen van gegevensstromen gebruikend de Dienst API van de Stroom](../../tutorials/api/delete-dataflows.md) voor stappen op hoe te om deze verrichtingen programmatically uit te voeren gebruikend API vraag.
