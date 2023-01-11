---
keywords: Experience Platform;home;populaire onderwerpen;bijgewerkte accounts
description: In sommige omstandigheden kan het nodig zijn de details van een bestaande bronrekening bij te werken. De werkruimte Bronnen biedt u de mogelijkheid om details van een bestaande batch- of streamingverbinding toe te voegen, te bewerken en te verwijderen, inclusief de naam, beschrijving en referenties.
solution: Experience Platform
title: Accountgegevens van bronverbinding bijwerken in de gebruikersinterface
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Accountgegevens bijwerken in de gebruikersinterface

In sommige omstandigheden kan het nodig zijn de details van een bestaande bronrekening bij te werken. De [!UICONTROL Sources] biedt u de mogelijkheid om details van een bestaande batch- of streamingverbinding toe te voegen, te bewerken en te verwijderen, inclusief de naam, beschrijving en gegevens.

Deze zelfstudie bevat stappen voor het bijwerken van de gegevens en referenties van een bestaande account via het dialoogvenster [!UICONTROL Sources] werkruimte.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [Bronnen](../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
- [Sandboxen](../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Accounts bijwerken

Aanmelden bij de [UI Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. Selecteren **[!UICONTROL Accounts]** in de bovenste koptekst om bestaande accounts weer te geven.

![catalogus](../../images/tutorials/update/catalog.png)

De **[!UICONTROL Accounts]** wordt weergegeven. Op deze pagina vindt u een lijst met weer te geven accounts, waaronder informatie over de bron, gebruikersnaam, het aantal gegevensstromen en de aanmaakdatum.

Filterpictogram selecteren ![filter](../../images/tutorials/update/filter.png) bovenaan links om het deelvenster Sorteren te starten.

![accounts-list](../../images/tutorials/update/accounts-list.png)

Het deelvenster Sorteren bevat een lijst met alle bronnen. U kunt meerdere bronnen in de lijst selecteren om een gefilterde selectie van accounts te openen die aan verschillende bronnen zijn gekoppeld.

Selecteer de bron waarmee u wilt werken om een lijst met bestaande accounts weer te geven. Nadat u de account hebt geïdentificeerd die u wilt bijwerken, selecteert u de ovalen (`...`) naast de accountnaam.

![rekeningen sorteren](../../images/tutorials/update/accounts-sort.png)

Er wordt een vervolgkeuzemenu weergegeven met opties voor **[!UICONTROL Add data]**, **[!UICONTROL Edit details]**, en **[!UICONTROL Delete]**. Selecteren **[!UICONTROL Edit details]** in het menu om uw account bij te werken.

![update](../../images/tutorials/update/update.png)

De **[!UICONTROL Edit account details]** kunt u de naam, beschrijving en verificatiereferenties van een account bijwerken. Als u de gewenste gegevens hebt bijgewerkt, selecteert u **[!UICONTROL Save]**.

![bewerken van accountgegevens](../../images/tutorials/update/edit-account-details.png)

Na enkele ogenblikken verschijnt onder aan het scherm een bevestigingsvak om te bevestigen dat de update is gelukt.

![bevestigd](../../images/tutorials/update/update-confirmed.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de opdracht [!UICONTROL Sources] werkruimte om de informatie van een bestaand bronaccount bij te werken.

Voor stappen op hoe te om deze verrichtingen programmatically uit te voeren gebruikend [!DNL Flow Service] API, raadpleeg de zelfstudie op [bijwerken, verbindingsgegevens met behulp van de Flow Service API](../../tutorials/api/update.md).
