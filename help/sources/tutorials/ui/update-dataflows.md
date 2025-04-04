---
description: Leer hoe u een bestaande gegevensstroom voor bronnen bijwerkt in de gebruikersinterface van Experience Platform.
title: Een Source Connection Dataflow bijwerken in de gebruikersinterface
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 0%

---

# Dataflows bijwerken in de gebruikersinterface

Lees deze zelfstudie voor stappen over het bijwerken van een bestaande gegevensstroom, inclusief de planning en toewijzingsconfiguraties, met gebruik van de werkruimte Bronnen in de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Bronnen ](../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## Dataflows bijwerken {#update-dataflows}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflows_daysRemaining"
>title="Vervaldatum gegevensset"
>abstract="Deze kolom wijst op het aantal dagen dat de doeldataset heeft verlaten alvorens het automatisch verloopt.<br> A dataflow zal ontbreken als de doeldataset is verlopen. Om dataflow te verhinderen te ontbreken, zorg ervoor dat een doeldataset wordt geplaatst om op de correcte datum te verlopen. Raadpleeg de documentatie voor informatie over het bijwerken van vervaldatums."

Selecteer in de gebruikersinterface van Experience Platform **[!UICONTROL Sources]** in de linkernavigatie en selecteer vervolgens **[!UICONTROL Dataflows]** in de bovenste koptekst.

![ de broncatalogus met de gegevens geselecteerde kopbaltabel.](../../images/tutorials/update-dataflows/catalog.png)

>[!TIP]
>
>Met filtermogelijkheden kunt u uw gegevensstromen sorteren en filteren. Lees de gids over [ het filtreren bronvoorwerpen in UI ](./filter.md) voor meer informatie.

Op de pagina [!UICONTROL Dataflows] wordt een lijst weergegeven met alle bestaande gegevensstromen in uw organisatie. Zoek de gegevensstroom die u wilt bijwerken en selecteer dan de ellipsen (`...`) naast het. Er wordt een vervolgkeuzemenu weergegeven met een lijst opties waaruit u kunt kiezen. Hiermee kunt u aanvullende configuraties toevoegen aan de bestaande gegevensstroom.

Selecteer **[!UICONTROL Update dataflow]** als u de gegevensstroom wilt bijwerken.

![ dropdown menu waar de opties om dataflows bij te werken vermeld zijn.](../../images/tutorials/update-dataflows/dropdown_update.png)

U wordt doorgestuurd naar de workflow voor bronnen waar u verder kunt gaan met het bijwerken van aspecten van uw gegevensstroom, inclusief de details in de stap [!UICONTROL Provide dataflow details] .

### Toewijzing bijwerken {#update-mapping}

>[!NOTE]
>
>De bewerkingstoewijzingsfunctie wordt momenteel niet ondersteund voor de volgende bronnen: Adobe Analytics, Adobe Audience Manager, HTTP API en [!DNL Marketo Engage] .

Tijdens dit proces kunt u ook de sets met toewijzingen bijwerken die aan uw gegevensstroom zijn gekoppeld.  De toewijzingsinterface toont de bestaande afbeelding van uw gegevensstroom en geen nieuwe geadviseerde toewijzingsreeks. De updates van de toewijzing worden slechts toegepast op dataflow looppas die in de toekomst wordt gepland. Voor een dataflow die was gepland voor eenmalige invoer, kunnen de sets met toewijzingen niet worden bijgewerkt.

Gebruik de toewijzingsinterface om de toewijzingssets te wijzigen die op de gegevensstroom zijn toegepast. Voor uitvoerige stappen op hoe te om de kaartinterface te gebruiken, zie de [ gids UI van de gegevens prep ](../../../data-prep/ui/mapping.md) voor meer informatie.

![ de afbeeldingsstap van het bronwerkschema. Gebruik deze stap om de afbeeldingen bij te werken verbonden aan uw dataflow.](../../images/tutorials/update-dataflows/mapping.png)

### Tijdschema bijwerken

Zodra u de afbeeldingen van uw gegevensstroom hebt bijgewerkt, kunt u dan verdergaan om uw innameschema bij te werken om uw gegevensstroom met zijn nieuwe toewijzingsgegevens in te voeren. U kunt het innameschema van gegevensstromen slechts bijwerken die aan inname op een terugkerend programma werden gevormd. U kunt geen dataflow opnieuw plannen die voor eenmalig opnemen werd gevormd.

U kunt ook het schema voor inname van uw gegevensstroom bijwerken met behulp van de optie voor inlineupdate die is opgegeven op de pagina met gegevensstromen.

Selecteer op de pagina met gegevensstromen de ovalen (`...`) naast de naam van de gegevensstroom en selecteer vervolgens **[!UICONTROL Edit schedule]** in het vervolgkeuzemenu dat wordt weergegeven.

![ de het plannen stap van het bronwerkschema. Gebruik deze stap om het programma van uw gegevensstroom bij te werken.](../../images/tutorials/update-dataflows/dropdown_edit.png)

Het dialoogvenster **[!UICONTROL Edit schedule]** bevat opties waarmee u de invoerfrequentie en de intervalsnelheid van uw gegevensstroom kunt bijwerken. Selecteer **[!UICONTROL Save]** als u de bijgewerkte frequentie- en intervalwaarden hebt ingesteld.

![ pop-up venster van A dat u kunt gebruiken om het de innameschema van uw gegevensstroom uit te geven.](../../images/tutorials/update-dataflows/edit_schedule.png)

### Gegevensstroom uitschakelen

U kunt de gegevensstroom uitschakelen met hetzelfde vervolgkeuzemenu. Selecteer **[!UICONTROL Disable dataflow]** om de gegevensstroom uit te schakelen.

![ dropdown menu met de optie om dataflow onbruikbaar te maken.](../../images/tutorials/update-dataflows/dropdown_disable.png)

Selecteer vervolgens [!UICONTROL Disable] in het pop-upvenster dat wordt weergegeven.

![ het pop-up venster waar u moet bevestigen dat u uw gegevensstroom wilt onbruikbaar maken.](../../images/tutorials/update-dataflows/disable_dataflow.png)

Als en wanneer u later dit gegevensstroom opnieuw toelaat, zal Experience Platform automatisch terugvullinglooppas plannen om de periode te dekken waarin dataflow werd onbruikbaar gemaakt. Bijvoorbeeld, als dataflow werd gevormd om te lopen uur en gehandicapt 48 uren was, op re-toelatend dit dataflow, zal Experience Platform 48 backfill looppas creëren aan verwerkte de gemiste intervallen.

## Volgende stappen

Aan de hand van deze zelfstudie hebt u de werkruimte van [!UICONTROL Sources] gebruikt om het innameprogramma en de sets met toewijzingen van uw gegevensstroom bij te werken.

Voor stappen op hoe te om deze verrichtingen programmatically uit te voeren gebruikend [!DNL Flow Service] API, te verwijzen gelieve naar het leerprogramma op [ het bijwerken dataflows gebruikend de Dienst API van de Stroom ](../../tutorials/api/update-dataflows.md).
