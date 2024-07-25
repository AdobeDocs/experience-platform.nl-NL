---
title: Geautomatiseerde gegevensset verlopen
description: Leer hoe te om een datasetvervaldatum in Adobe Experience Platform UI te plannen.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 0%

---

# Verlopen van geautomatiseerde gegevenssets {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="Ongewenste of verlopen klantenverslagen en datasets verwijderen"
>abstract="<h2>Beschrijving</h2><p>Om de levenscyclus van uw gegevens van het Experience Platform niet met regelgevende naleving te beheren, kunt u consumentenverslagen en planningsvervaldata voor datasets schrappen. Zie het gebruiksgevalblok &#39;Privacy-aanvragen van betrokkenen respecteren&#39; voor het maken of beheren van verzoeken om gegevens over onderwerpen.</p>"

De [[!UICONTROL Data Lifecycle] werkruimte ](./overview.md) in Adobe Experience Platform UI staat u toe om termijnen voor datasets te plannen. Wanneer een dataset zijn vervaldatum bereikt, beginnen het gegevens meer, de Dienst van de Identiteit, en het Profiel van de Klant in real time afzonderlijke processen om de inhoud van de dataset uit hun respectieve diensten te verwijderen. Zodra de gegevens van alle drie de diensten worden geschrapt, wordt de vervaldatum duidelijk volledig.

>[!WARNING]
>
>Als een dataset wordt geplaatst om te verlopen, moet u om het even welke gegevensstromen manueel veranderen die gegevens in die dataset kunnen opnemen zodat uw stroomafwaartse werkschema&#39;s niet negatief worden beïnvloed.

In dit document wordt beschreven hoe u gegevenssetvervaldatums in de gebruikersinterface van het platform kunt plannen en automatiseren.

>[!NOTE]
>
>Gegevens worden momenteel niet verwijderd uit de Adobe Experience Platform-Edge Network. Er is echter geen mogelijkheid dat gegevens binnen de Edge Network blijven nadat de gegevensset is ingesteld op verlopen. Dit komt doordat de 15-daagse licentieovereenkomst voor Dataset Expiration overlapt met de periode van 14 dagen waarin gegevens binnen de Edge Network bestaan voordat ze worden verwijderd.

Het geavanceerde Beheer van de Levenscyclus van Gegevens steunt datasetschrappingen door het [ eindpunt van de gegevenssetvervalsing ](../api/dataset-expiration.md) en identiteitskaart schrappingen (rij-vlakke gegevens) gebruikend primaire identiteiten via het [ werkordeeindpunt ](../api/workorder.md). U kunt datasetvervalingen en [ verslagschrappingen ](./record-delete.md) door Platform UI ook beheren. Raadpleeg de gekoppelde documentatie voor meer informatie.

>[!NOTE]
>
>Gegevenslevenscyclus ondersteunt het verwijderen van batches niet.

## Een gegevensset plannen die vervalt {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="Instructies"
>abstract="<ul><li>Selecteer <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html"> Levenscyclus van Gegevens </a> in de linkernavigatie, dan selecteren <b> verzoek </b> creëren.</li><li>Als u records wilt verwijderen:</li>   <li>Selecteer <b> Verslag </b>.</li>   <li>Selecteer een specifieke dataset om verslagen van te schrappen of de optie te kiezen om hen van alle datasets te schrappen.</li>   <li>Vermeld de identiteit van de consumenten van wie de gegevens moeten worden verwijderd. Selecteer <b> Identiteit </b> toevoegen om de identiteiten één tegelijkertijd te verstrekken of <b> kiezen dossiers </b> om een JSON- dossier van identiteiten in plaats daarvan te uploaden.</li>   <li>Indien nodig, uitgezochte <b> Malplaatje </b> om het verwachte formaat van het JSON dossier te bekijken.</li><li>Zie de documentatie voor instructies als u <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html#schedule-dataset-expiration"> vervaldata voor datasets </a> wilt plannen.</li></ul>"

Als u een aanvraag wilt maken, selecteert u **[!UICONTROL Create request]** op de hoofdpagina in de werkruimte.

>[!IMPORTANT]
>
>Real-Time CDP, Adobe Journey Optimizer, en de gebruikers van de Customer Journey Analytics hebben 20 in afwachting van geplande dataset het werkorden van de vervaldatum. Gebruikers van het gezondheidsschild en het privacyschild hebben 50 geplande werkorders voor het aflopen van gegevenssets in behandeling. Dit betekent dat u 20 of 50 datasets kunt hebben die om op elk ogenblik worden gepland worden geschrapt.<br> Bijvoorbeeld, als u 20 geplande datasettermijnen hebt en één dataset morgen moet worden geschrapt, kunt u geen meer vervalsingen plaatsen tot nadat die dataset is geschrapt.

![ de [!UICONTROL Data Lifecycle] werkruimte met [!UICONTROL Create request] benadrukte.](../images/ui/ttl/create-request-button.png)

De workflow voor het maken van aanvragen wordt weergegeven. Selecteer onder de sectie [!UICONTROL Requested Action] de optie **[!UICONTROL Delete Dataset]** om de besturingselementen voor het plannen van de vervaldatum van de gegevensset bij te werken.

![ het werkschema van de verzoekverwezenlijking met de [!UICONTROL Delete dataset] benadrukte optie.](../images/ui/ttl/dataset-selected.png)

### Selecteer een datum en een dataset {#select-date-and-dataset}

Selecteer onder de sectie **[!UICONTROL Requested Action]** een datum waarop u de gegevensset wilt verwijderen. U kunt de datum manueel ingaan (in het formaat `mm/dd/yyyy`) of het kalenderpictogram (![ A kalenderpictogram selecteren.](/help/images/icons/calendar.png) ) om de datum in een dialoogvenster te selecteren.

![ de kalenderdialoog van A met een geselecteerde en benadrukte vervaldatum voor de dataset.](../images/ui/ttl/select-date.png)

Daarna, onder **[!UICONTROL Dataset Details]**, selecteer het gegevensbestandpictogram (![ het gegevensbestandpictogram.](/help/images/icons/database.png)) om een dialoogvenster voor de selectie van gegevenssets te openen. Kies een dataset in de lijst waarop u de vervaldatum wilt toepassen en selecteer vervolgens **[!UICONTROL Done]** .

![ de [!UICONTROL Select dataset] dialoog met een geselecteerde dataset en [!UICONTROL Done] benadrukte.](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Alleen gegevenssets die tot de huidige sandbox behoren, worden weergegeven.

### De aanvraag verzenden {#submit-request}

De sectie [!UICONTROL Dataset Details] wordt gevuld en bevat nu de primaire identiteit en het schema voor de geselecteerde dataset. Voer onder **[!UICONTROL Request settings]** een naam en een optionele beschrijving voor de aanvraag in, gevolgd door **[!UICONTROL Submit]** .

![ een voltooide vraag van de datasetvervaldatum met [!UICONTROL Request settings] en [!UICONTROL Submit] benadrukte knoop.](../images/ui/ttl/submit.png)

Er wordt een dialoogvenster [!UICONTROL Confirm request] weergegeven. U wordt gevraagd om de naam van de dataset en de datum te bevestigen dat de dataset door zal worden geschrapt. Selecteer **[!UICONTROL Submit]** om door te gaan.

Nadat het verzoek is verzonden, wordt een werkorder gemaakt die wordt weergegeven op het hoofdtabblad van de werkruimte van [!UICONTROL Data Lifecycle] . Van hier, kunt u de status van de het werkorde controleren aangezien het het verzoek verwerkt.

>[!NOTE]
>
>Verwijs naar de overzichtssectie op [ chronologie en transparantie ](../home.md#dataset-expiration-transparency) voor details over hoe de datasettermijnen worden verwerkt zodra zij worden uitgevoerd.

## Een gegevensset bewerken of annuleren {#edit-or-cancel}

Als u een gegevensset wilt bewerken of annuleren, selecteert u **[!UICONTROL Dataset]** op de hoofdpagina van de werkruimte en selecteert u de vervaldatum van de gegevensset in de lijst.

Op de detailspagina van de datasetvervaldatum, toont de juiste spoorstaaf controles om de geplande schrapping uit te geven of te annuleren.

## Volgende stappen

Dit document behandelde hoe te om datasettermijnen in Experience Platform UI te plannen. Voor informatie over hoe te om andere taken van de gegevensminimalisering in UI uit te voeren, verwijs naar het [ overzicht van de gegevenslevenscyclus UI van de gegevenslevenscyclus ](./overview.md).

Leren hoe te om datasetvervalingen te plannen gebruikend de gegevenshygiëne API, verwijs naar de [ gids van het de eindpuntverloopeindpunt van de dataset ](../api/dataset-expiration.md).
