---
title: Verlopen gegevensset beheren
description: Leer hoe te om een datasetvervaldatum in Adobe Experience Platform UI te plannen.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 7931c8fe4a1ca5d255a80e7e6b0deb976d53c3de
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Verlopen gegevenssets beheren {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="Ongewenste of verlopen klantenverslagen en datasets verwijderen"
>abstract="<h2>Beschrijving</h2><p>Om de levenscyclus van uw gegevens van het Experience Platform niet met regelgevende naleving te beheren, kunt u consumentenverslagen en planningsvervaldata voor datasets schrappen. Zie het gebruiksgevalblok &#39;Privacy-aanvragen van betrokkenen respecteren&#39; voor het maken of beheren van verzoeken om gegevens over onderwerpen.</p>"

De [[!UICONTROL Data Lifecycle] werkruimte](./overview.md) in Adobe Experience Platform UI staat u toe om termijnen voor datasets te plannen. Wanneer een dataset zijn vervaldatum bereikt, beginnen het gegevens meer, de Dienst van de Identiteit, en het Profiel van de Klant in real time afzonderlijke processen om de inhoud van de dataset uit hun respectieve diensten te verwijderen. Zodra de gegevens van alle drie de diensten worden geschrapt, wordt de vervaldatum duidelijk volledig.

>[!WARNING]
>
>Als een dataset wordt geplaatst om te verlopen, moet u om het even welke gegevensstromen manueel veranderen die gegevens in die dataset kunnen opnemen zodat uw stroomafwaartse werkschema&#39;s niet negatief worden beïnvloed.

Dit document behandelt hoe te om datasettermijnen in het Platform UI te plannen en te beheren.

>[!NOTE]
>
>Gegevens worden momenteel niet verwijderd uit het Adobe Experience Platform Edge Network vanwege de vervaldatum van de gegevensset. Nochtans, is er geen mogelijkheid dat de gegevens binnen het Netwerk van de Rand blijven nadat de dataset wordt geplaatst om te verlopen. Dit komt doordat de 14-daagse licentieovereenkomst voor Dataset Expiration samenvalt met de periode van 14 dagen waarin gegevens in het Edge Network aanwezig zijn voordat deze worden verwijderd.

## Een gegevensset plannen die vervalt {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="Instructies"
>abstract="<ul><li>Selecteren <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html">Levenscyclus gegevens</a> in de linkernavigatie selecteert u vervolgens <b>Aanvraag maken</b>.</li><li>Als u records wilt verwijderen:</li>   <li>Selecteren <b>Opnemen</b>.</li>   <li>Selecteer een specifieke dataset om verslagen van te schrappen of de optie te kiezen om hen van alle datasets te schrappen.</li>   <li>Vermeld de identiteit van de consumenten van wie de gegevens moeten worden verwijderd. Selecteren <b>Identiteit toevoegen</b> om de identiteiten één voor één te verstrekken of selecteren <b>Bestanden kiezen</b> om in plaats daarvan een JSON-bestand met identiteiten te uploaden.</li>   <li>Selecteer indien nodig <b>Sjabloon</b> om de verwachte indeling van het JSON-bestand weer te geven.</li><li>Zie de documentatie voor instructies als u wilt <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html#schedule-dataset-expiration">vervaldata voor gegevenssets</a>.</li></ul>"

Als u een aanvraag wilt maken, selecteert u **[!UICONTROL Create request]** van de hoofdpagina in de werkruimte.

>[!IMPORTANT]
>
U kunt tot 20 tezelfdertijd geplande datasettermijnen hebben. Dit betekent dat u 20 datasets kunt hebben die om op elk ogenblik worden gepland worden geschrapt. Er zijn geen beperkingen aan de duur of het jaar waarvoor deze vervaldata worden vastgesteld. Bijvoorbeeld, als u 20 geplande datasettermijnen hebt en één dataset morgen zal worden geschrapt, kunt u geen meer vervalsingen plaatsen tot nadat die dataset is geschrapt.

![De [!UICONTROL Data Lifecycle] werkruimte met [!UICONTROL Create request] gemarkeerd.](../images/ui/ttl/create-request-button.png)

De workflow voor het maken van aanvragen wordt weergegeven. Onder de [!UICONTROL Requested Action] sectie, selecteert u **[!UICONTROL Delete Dataset]** om de controles voor datasetvervalplanning bij te werken.

![De workflow voor het maken van aanvragen met de [!UICONTROL Delete dataset] gemarkeerd.](../images/ui/ttl/dataset-selected.png)

### Selecteer een datum en een dataset {#select-date-and-dataset}

Onder de **[!UICONTROL Requested Action]** selecteert u een datum waarop de gegevensset moet worden verwijderd. U kunt de datum handmatig invoeren (in de notatie `mm/dd/yyyy`) of selecteer het kalenderpictogram (![Een kalenderpictogram.](../images/ui/ttl/calendar-icon.png)) om de datum in een dialoogvenster te selecteren.

![Een kalenderdialoog met een geselecteerde en benadrukte vervaldatum voor de dataset.](../images/ui/ttl/select-date.png)

Volgende, onder **[!UICONTROL Dataset Details]**, selecteert u het databasepictogram (![The database icon.](../images/ui/ttl/database-icon.png)) om een dialoogvenster voor de selectie van gegevenssets te openen. Kies een dataset in de lijst waarop u de vervaldatum wilt toepassen en selecteer **[!UICONTROL Done]**.

![De [!UICONTROL Select dataset] dialoog met een geselecteerde dataset en [!UICONTROL Done] gemarkeerd.](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
Alleen gegevenssets die tot de huidige sandbox behoren, worden weergegeven.

### De aanvraag verzenden {#submit-request}

De [!UICONTROL Dataset Details] de sectie bevolkt om de primaire identiteit en het schema voor de geselecteerde dataset te omvatten. Onder **[!UICONTROL Request settings]** voert u een naam en een optionele beschrijving in voor de aanvraag, gevolgd door **[!UICONTROL Submit]**.

![Een volledig volledig verzoek van de datasetvervaldatum met [!UICONTROL Request settings] en [!UICONTROL Submit] gemarkeerd.](../images/ui/ttl/submit.png)

A [!UICONTROL Confirm request] wordt weergegeven. U wordt gevraagd om de naam van de dataset en de datum te bevestigen dat de dataset door zal worden geschrapt. Selecteren **[!UICONTROL Submit]** om door te gaan.

Nadat het verzoek is verzonden, wordt een werkorder gemaakt en wordt deze weergegeven op het hoofdtabblad van het dialoogvenster [!UICONTROL Data Lifecycle] werkruimte. Van hier, kunt u de status van de het werkorde controleren aangezien het het verzoek verwerkt.

>[!NOTE]
>
Zie de overzichtssectie over [tijdlijnen en transparantie](../home.md#dataset-expiration-transparency) voor details over hoe de gegevensreeksen verlopen worden verwerkt zodra zij worden uitgevoerd.

## Een gegevensset bewerken of annuleren {#edit-or-cancel}

Als u een gegevensset wilt bewerken of annuleren, selecteert u **[!UICONTROL Dataset]** op de belangrijkste pagina van de werkruimte, en selecteer de datasetvervaldatum van de lijst.

Op de detailspagina van de datasetvervaldatum, toont de juiste spoorstaaf controles om de geplande schrapping uit te geven of te annuleren.

## Volgende stappen

Dit document behandelde hoe te om datasettermijnen in Experience Platform UI te plannen. Voor informatie over hoe te om andere taken van de gegevensminimalisering in UI uit te voeren, verwijs naar [overzicht van de gebruikersinterface van de gegevenslevenscyclus](./overview.md).

Om te leren hoe te om datasetvervaldatums te plannen gebruikend de gegevens hygiëne API, verwijs naar [eindpuntgids gegevensset](../api/dataset-expiration.md).
