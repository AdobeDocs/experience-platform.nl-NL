---
keywords: Experience Platform;thuis;populaire onderwerpen;update dataflows;geef programma uit
description: Dit leerprogramma behandelt de stappen voor het bijwerken van een gegevensstroomprogramma, met inbegrip van zijn innamefrequentie en intervalsnelheid, gebruikend de Bronwerkruimte.
solution: Experience Platform
title: Een Source Connection Dataflow bijwerken in de gebruikersinterface
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: cef5c203acf3318445399669336166e6627ebe66
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Dataflows bijwerken in de gebruikersinterface

Deze zelfstudie biedt u stappen voor het bijwerken van een bestaande gegevensstroom, inclusief het schema en de toewijzing ervan, aan de hand van de werkruimte voor bronnen.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Sandboxes ](../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## Dataflows bijwerken {#update-dataflows}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflows_daysRemaining"
>title="Vervaldatum gegevensset"
>abstract="Deze kolom wijst op het aantal dagen dat de doeldataset heeft verlaten alvorens het automatisch verloopt.<br> A dataflow zal ontbreken als de doeldataset is verlopen. Om dataflow te verhinderen te ontbreken, zorg ervoor dat een doeldataset wordt geplaatst om op de correcte datum te verlopen. Raadpleeg de documentatie voor informatie over het bijwerken van vervaldatums."

Selecteer in de gebruikersinterface van het platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . Selecteer **[!UICONTROL Dataflows]** in de bovenste koptekst om een lijst met bestaande gegevensstromen weer te geven.

![ catalogus ](../../images/tutorials/update-dataflows/catalog.png)

De pagina [!UICONTROL Dataflows] bevat een lijst van alle bestaande gegevensstromen, met inbegrip van informatie over hun overeenkomstige doeldataset, bron, en rekeningsnaam.

Om door de lijst te sorteren, selecteer de filter ![ filter ](../../images/tutorials/update/filter.png) op de bovenkant verlaten om het soortpaneel te gebruiken.

![ filter-dataflows ](../../images/tutorials/update-dataflows/filter-dataflows.png)

Het deelvenster Sorteren bevat een lijst met alle beschikbare bronnen. U kunt meer dan één bron in de lijst selecteren om tot een gefilterde selectie van gegevensstromen toegang te hebben die tot verschillende bronnen behoren.

Selecteer de bron waarmee u wilt werken om een lijst met de bestaande gegevensstromen weer te geven. Nadat u de gegevensstroom hebt geïdentificeerd die u wilt bijwerken, selecteert u de ovalen (`...`) naast de naam van de gegevensstroom.

![ geef-bron uit ](../../images/tutorials/update-dataflows/edit-source.png)

Er wordt een vervolgkeuzemenu weergegeven waarin u opties kunt opgeven om de gegevensstroom die u hebt geselecteerd bij te werken. Van hier, kunt u verkiezen om de de kaartreeksen van een dataflow en innameprogramma bij te werken. U kunt ook opties selecteren om de gegevensstroom te inspecteren in het controledashboard, u te abonneren op waarschuwingen en de gegevensstroom uit te schakelen of te verwijderen.

Selecteer **[!UICONTROL Update dataflow]** als u de gegevens van uw gegevensstroom wilt bijwerken.

![ update-dataflow ](../../images/tutorials/update-dataflows/update-dataflow.png)

### Gegevens toevoegen

De stap [!UICONTROL Add data] wordt weergegeven. Selecteer de juiste gegevensindeling om de inhoud van de geselecteerde gegevens te bekijken en selecteer vervolgens **[!UICONTROL Next]** om door te gaan.

![ toe:voegen-gegevens ](../../images/tutorials/update-dataflows/add-data.png)

### Gegevens

In de [!UICONTROL Dataflow detail] pagina, kunt u een bijgewerkte naam en een beschrijving voor uw gegevensstroom verstrekken evenals de de foutendrempel van uw gegevensstroom aanpassen. Tijdens deze stap, kunt u montages voor uw waakzaam abonnement ook vormen of wijzigen.

Als u de bijgewerkte waarden hebt opgegeven, selecteert u **[!UICONTROL Next]** .

![ dataflow-detail ](../../images/tutorials/update-dataflows/dataflow-detail.png)

### Toewijzing

>[!NOTE]
>
>De bewerkingstoewijzingsfunctie wordt momenteel niet ondersteund voor de volgende bronnen: Adobe Analytics, Adobe Audience Manager, HTTP API en [!DNL Marketo Engage] .

De pagina [!UICONTROL Mapping] biedt u een interface waarin u aan uw gegevensstroom gekoppelde sets kunt toevoegen en verwijderen.

De toewijzingsinterface toont de bestaande de afbeeldingsreeks van uw gegevensstroom en niet een nieuwe geadviseerde toewijzingsreeks. De updates van de toewijzing worden slechts toegepast op dataflow looppas die in de toekomst wordt gepland. Voor een dataflow die was gepland voor eenmalige invoer, kunnen de sets met toewijzingen niet worden bijgewerkt.

Van hier, kunt u de toewijzingsinterface gebruiken om de afbeeldingsreeksen te wijzigen die op uw gegevensstroom worden toegepast. Voor uitvoerige stappen op hoe te om de kaartinterface te gebruiken, zie de [ gids UI van de gegevens prep ](../../../data-prep/ui/mapping.md) voor meer informatie.

![ afbeelding ](../../images/tutorials/update-dataflows/mapping.png)

### Planning

De stap [!UICONTROL Scheduling] verschijnt, die u toestaat om het de innameschema van uw gegevensstroom bij te werken en automatisch de geselecteerde brongegevens met de bijgewerkte afbeeldingen in te nemen.

>[!NOTE]
>
>U kunt geen dataflow opnieuw plannen die voor eenmalig opnemen was gepland.

![ nieuw-programma ](../../images/tutorials/update-dataflows/new-schedule.png)

U kunt ook het schema voor inname van uw gegevensstroom bijwerken met behulp van de optie voor inlineupdate die is opgegeven op de pagina met gegevensstromen.

Selecteer op de pagina met gegevensstromen de ovalen (`...`) naast de naam van de gegevensstroom en selecteer vervolgens **[!UICONTROL Edit schedule]** in het vervolgkeuzemenu dat wordt weergegeven.

![ uitgeven-programma ](../../images/tutorials/update-dataflows/edit-schedule.png)

Het dialoogvenster **[!UICONTROL Edit schedule]** bevat opties waarmee u de invoerfrequentie en de intervalsnelheid van uw gegevensstroom kunt bijwerken. Selecteer **[!UICONTROL Save]** als u de bijgewerkte frequentie- en intervalwaarden hebt ingesteld.

![ programma-pop-up ](../../images/tutorials/update-dataflows/schedule-pop-up.png)

### Controleren

De stap **[!UICONTROL Review]** wordt weergegeven, zodat u uw gegevensstroom kunt controleren voordat deze wordt bijgewerkt.

Nadat u de gegevensstroom hebt gereviseerd, selecteert u **[!UICONTROL Finish]** en laat u enige tijd over voor de gegevensstroom met de nieuwe toewijzingssets die worden gemaakt.

![ overzicht ](../../images/tutorials/update-dataflows/review.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u de werkruimte van [!UICONTROL Sources] gebruikt om het innameprogramma en de sets met toewijzingen van uw gegevensstroom bij te werken.

Voor stappen op hoe te om deze verrichtingen programmatically uit te voeren gebruikend [!DNL Flow Service] API, te verwijzen gelieve naar het leerprogramma op [ het bijwerken dataflows gebruikend de Dienst API van de Stroom ](../../tutorials/api/update-dataflows.md).
