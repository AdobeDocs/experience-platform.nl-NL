---
keywords: Experience Platform;home;populaire onderwerpen; gegevens verwijderen
description: De werkruimte Bronnen biedt u de mogelijkheid om bestaande batch- en streaming gegevensstromen te verwijderen die fouten bevatten of verouderd zijn.
solution: Experience Platform
title: Gegevensstromen verwijderen in de gebruikersinterface
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# Gegevensstromen verwijderen in de gebruikersinterface

In de werkruimte van [!UICONTROL Sources] kunt u bestaande batch- en streaming-gegevensstromen verwijderen die fouten bevatten of verouderd zijn.

Deze zelfstudie bevat stappen voor het verwijderen van gegevensstromen in de werkruimte van [!UICONTROL Sources] .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [&#x200B; Bronnen &#x200B;](../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
- [&#x200B; Sandboxen &#x200B;](../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## Gegevensstromen verwijderen

In [&#x200B; Experience Platform UI &#x200B;](https://platform.adobe.com), selecteer **[!UICONTROL Sources]** van de linkernavigatie om tot de [!UICONTROL Sources] werkruimte toegang te hebben, en dan **[!UICONTROL Dataflows]** van de hoogste kopbal te selecteren.

![&#x200B; catalogus &#x200B;](../../images/tutorials/delete/catalog.png)

De pagina **[!UICONTROL Dataflows]** wordt weergegeven. Op deze pagina is een lijst van viewable gegevensstromen, met inbegrip van informatie over hun doeldataset, bron, rekeningsnaam, en datum van verwezenlijking.

Selecteer het filterpictogram (![&#x200B; filter-pictogram &#x200B;](/help/images/icons/filter.png)) op de bovenkant verlaten om het soortpaneel te lanceren.

![&#x200B; dataflows &#x200B;](../../images/tutorials/delete/dataflows.png)

Het deelvenster Sorteren bevat een lijst met alle bronnen. U kunt meer dan één bron van de lijst selecteren om tot een gefilterde selectie van gegevensstromen toegang te hebben verbonden aan de bijzondere bronnen u selecteerde.

Selecteer de bron waarmee u wilt werken om een lijst met de bestaande gegevensstromen weer te geven. Nadat u de gegevensstroom hebt geïdentificeerd die u wilt verwijderen, selecteert u de ovalen (`...`) naast de naam van de gegevensstroom.

![&#x200B; dataflows-filter &#x200B;](../../images/tutorials/delete/dataflows-filter.png)

Er wordt een vervolgkeuzemenu weergegeven waarin u opties kunt opgeven om het schema van uw gegevensstroom te bewerken, de gegevensstroom uit te schakelen of deze volledig te verwijderen.

Selecteer **[!UICONTROL Delete]** om de gegevensstroom te verwijderen.

![&#x200B; schrapping &#x200B;](../../images/tutorials/delete/delete.png)

Er wordt een laatste bevestigingsvenster weergegeven. Selecteer **[!UICONTROL Delete]** om het proces te voltooien.

![&#x200B; bevestig &#x200B;](../../images/tutorials/delete/confirm.png)

Na enkele ogenblikken wordt onder aan het scherm een bevestigingsvak weergegeven om te bevestigen dat het verwijderen is gelukt.

![&#x200B; bevestigd &#x200B;](../../images/tutorials/delete/confirmed.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de werkruimte van [!UICONTROL Sources] gebruikt om een bestaande gegevensstroom te verwijderen.

Zie het leerprogramma op [&#x200B; schrappend dataflows gebruikend de Dienst API van de Stroom &#x200B;](../../tutorials/api/delete-dataflows.md) voor stappen op hoe te om deze verrichtingen programmatically uit te voeren gebruikend API vraag.
