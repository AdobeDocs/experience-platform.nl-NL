---
keywords: Experience Platform;home;populaire onderwerpen;map csv;map csv-bestand;map csv-bestand toewijzen aan xdm;map csv aan xdm;ui guide;mapper;mapping;data prep;data voorbereiden;voorbereiden van gegevens;
title: UI-gids voor gegevenprepress
description: Dit document biedt aanwijzingen voor het gebruik van functies voor gegevensvoorvoegsel in de gebruikersinterface van het platform om CSV-bestanden toe te wijzen aan een XDM-schema.
exl-id: fafa4aca-fb64-47ff-a97d-c18e58ae4dae
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 0%

---

# UI-gids voor gegevenprepress

Dit document biedt aanwijzingen voor het gebruik van functies voor gegevensvoorvoegsels in de Adobe Experience Platform-gebruikersinterface om CSV-bestanden toe te wijzen aan een XDM-schema.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende platformcomponenten:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [ Dienst van de Identiteit ](../../identity-service/home.md): Verkrijg een betere mening van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [ Bronnen ](../../sources/home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.

## Gegevens

>[!TIP]
>
>U kunt tot gegevens toegang hebben die door om het even welke bron van de broncatalogus te selecteren. Voor meer informatie, zie het [ overzicht van bronnen ](../../sources/home.md).

Voordat u uw CSV-gegevens kunt toewijzen aan een XDM-schema, moet u eerst de details van de gegevensstroom vaststellen.

De [!UICONTROL Dataflow detail] pagina staat u toe om te selecteren of u uw gegevens CSV in een bestaande doeldataset of een nieuwe doeldataset wilt opnemen. Een bestaande dataset komt met een vooraf gebouwd doelschema om uw gegevens aan in kaart te brengen, terwijl een nieuwe dataset u vereist om een bestaand schema te selecteren, of een nieuw schema tot stand te brengen, om uw gegevens aan in kaart te brengen.

### Een bestaande doelgegevensset gebruiken

Als u uw CSV-gegevens in een bestaande gegevensset wilt opnemen, selecteert u **[!UICONTROL Existing dataset]** . U kunt of een bestaande dataset terugwinnen gebruikend de [!UICONTROL Advanced search] optie of door door de lijst van bestaande datasets in het dropdown menu te scrollen.

Selecteer een gegevensset en geef een naam op voor de gegevensstroom en een optionele beschrijving.

Tijdens dit proces kunt u ook [!UICONTROL Error diagnostics] en [!UICONTROL Partial ingestion] inschakelen. In [!UICONTROL Error diagnostics] kunnen gedetailleerde foutberichten worden gegenereerd voor onjuiste records in de gegevensstroom, terwijl u in [!UICONTROL Partial ingestion] gegevens met fouten kunt invoeren tot een bepaalde drempel die u handmatig definieert. Zie het [ gedeeltelijke overzicht van partijingestie ](../../ingestion/batch-ingestion/partial.md) voor meer informatie.

![ bestaand-dataset ](../images/ui/mapping/existing-dataset.png)

### Een nieuwe doelgegevensset gebruiken

Als u uw CSV-gegevens in een nieuwe gegevensset wilt opnemen, selecteert u **[!UICONTROL New dataset]** en geeft u vervolgens een naam voor de uitvoergegevensset en een optionele beschrijving op. Selecteer vervolgens het schema dat u wilt toewijzen met de optie [!UICONTROL Advanced search] of door door de lijst met bestaande schema&#39;s in het vervolgkeuzemenu te bladeren.

Selecteer een schema, geef een naam voor de gegevensstroom en een optionele beschrijving op en pas vervolgens de [!UICONTROL Error diagnostics] - en [!UICONTROL Partial ingestion] -instellingen toe die u voor de gegevensstroom wilt gebruiken. Selecteer **[!UICONTROL Next]** als u klaar bent.

![ nieuw-dataset ](../images/ui/mapping/new-dataset.png)

## Gegevens selecteren

De stap [!UICONTROL Select data] wordt weergegeven, zodat u een interface hebt om uw lokale bestanden te uploaden en een voorvertoning van de structuur en inhoud ervan weer te geven. Selecteer **[!UICONTROL Choose files]** om een CSV-bestand van uw lokale systeem te uploaden. U kunt ook het CSV-bestand dat u wilt uploaden naar het deelvenster [!UICONTROL Drag and drop files] slepen.

>[!TIP]
>
>Momenteel worden alleen CSV-bestanden ondersteund door lokale bestanden te uploaden. De maximale bestandsgrootte voor elk bestand is 1 GB.

![ kiezen-dossiers ](../images/ui/mapping/choose-files.png)

Nadat het bestand is geüpload, wordt de voorbeeldinterface bijgewerkt en worden de inhoud en de structuur van het bestand weergegeven.

![ voorproef-steekproef-gegevens ](../images/ui/mapping/preview-sample-data.png)

Afhankelijk van het bestand kunt u een kolomscheidingsteken selecteren, zoals tabs, komma&#39;s, pijpen of een aangepast kolomscheidingsteken voor de brongegevens. Selecteer de vervolgkeuzepijl **[!UICONTROL Delimiter]** en selecteer vervolgens het juiste scheidingsteken in het menu.

Selecteer **[!UICONTROL Next]** als u klaar bent.

![ delimiter ](../images/ui/mapping/delimiter.png)

## Toewijzing

De interface **[!UICONTROL mapping]** voorziet u van een uitvoerig hulpmiddel om brongebieden van uw bronschema aan hun aangewezen doelXDM gebieden in het doelschema in kaart te brengen.

![ kaart-csv-aan-xdm ](../images/ui/mapping/map-csv-to-xdm.png)

### De toewijzingsinterface {#mapping-interface}

De toewijzingsinterface bevat een dashboard dat informatie verschaft over de status van uw toewijzingsvelden binnen de context van de innameworkflow. Op het dashboard worden de volgende gegevens over de toewijzingsvelden weergegeven:

| Eigenschap | Beschrijving |
| --- | --- |
| [!UICONTROL Mapped fields] | Hiermee geeft u het totale aantal bronvelden weer dat aan een doel-XDM-veld is toegewezen, ongeacht fouten. |
| [!UICONTROL Required fields] | Hier wordt het aantal vereiste toewijzingsvelden weergegeven. |
| [!UICONTROL Identity fields] | Hiermee geeft u het totale aantal toewijzingsvelden weer dat als identiteit is gedefinieerd. Deze toewijzingsvelden worden aangegeven met een vingerafdrukpictogram. |
| [!UICONTROL Errors] | Geeft het aantal onjuiste toewijzingsvelden weer. |

![ top-panel ](../images/ui/mapping/top-panel.png)

De toewijzingsinterface biedt ook een deelvenster met opties die u kunt kiezen om beter te communiceren of door de toewijzingsvelden te filteren.

![ tweede-paneel ](../images/ui/mapping/second-panel.png)

Als u naar een bepaalde toewijzingsset wilt zoeken, selecteert u **[!UICONTROL Search source fields]** en voert u de naam in van de brongegevens die u wilt isoleren.

![ onderzoek ](../images/ui/mapping/search.png)

Selecteer **[!UICONTROL All source fields]** om een vervolgkeuzemenu met filteropties weer te geven, zodat u de weergave van de toewijzingsinterface beter omlaag kunt versmallen.

De filteropties zijn:

| Source-velden | Beschrijving |
| --- | --- |
| [!UICONTROL All source fields] | Met deze optie worden alle bronvelden van het bronschema weergegeven. Deze optie wordt standaard weergegeven. |
| [!UICONTROL Required fields] | Met deze optie filtert u het bronschema zodat alleen de velden worden weergegeven die nodig zijn om de toewijzing te voltooien. |
| [!UICONTROL Identity fields] | Met deze optie filtert u het bronschema zodat alleen de velden worden weergegeven die zijn gemarkeerd voor Identiteit. |
| [!UICONTROL Mapped fields] | Met deze optie filtert u het bronschema zodat alleen de velden worden weergegeven die al zijn toegewezen. |
| [!UICONTROL Unmapped fields] | Met deze optie filtert u het bronschema zodat alleen de velden worden weergegeven die nog moeten worden toegewezen. |
| [!UICONTROL Fields with recommendation] | Met deze optie filtert u het bronschema om alleen de velden weer te geven die toewijzingsaanbevelingen bevatten. |

Selecteer **[!UICONTROL Fields with errors]** om alle toewijzingsvelden met fouten weer te geven.

![ filter ](../images/ui/mapping/filter.png)

Er wordt een geïsoleerde weergave van onjuiste toewijzingsvelden weergegeven, zodat u fouten kunt verhelpen met intelligente toewijzingsaanbevelingen of met de handmatige toewijzingsstructuur.

![ gebieden-met-fouten ](../images/ui/mapping/fields-with-errors.png)

### Een nieuw veldtype toevoegen

U kunt een nieuw toewijzingsveld of een berekend veld toevoegen door **[!UICONTROL New field type]** te selecteren.

#### Nieuw toewijzingsveld

Als u een nieuw toewijzingsveld wilt toevoegen, selecteert u **[!UICONTROL New field type]** en selecteert u **[!UICONTROL Add new field]** in het vervolgkeuzemenu dat wordt weergegeven.

![ toe:voegen-nieuw-gebied ](../images/ui/mapping/add-new-field.png)

Selecteer vervolgens het bronveld dat u wilt toevoegen in het bronschema dat wordt weergegeven en selecteer **[!UICONTROL Select]** .

![ selecteren-nieuw-gebied ](../images/ui/mapping/select-new-field.png)

De toewijzingsinterface wordt bijgewerkt met het bronveld dat u hebt geselecteerd en een leeg doelveld. Selecteer **[!UICONTROL Map target field]** om het nieuwe bronveld toe te wijzen aan het juiste doel-XDM-veld.

![ kaart-doel-gebied ](../images/ui/mapping/map-target-field.png)

Er wordt een interactieve doelschemastructuur weergegeven, waarmee u handmatig door het doelschema kunt bladeren en het juiste doel-XDM-veld voor uw bronveld kunt vinden.

![ hand-afbeelding ](../images/ui/mapping/manual-mapping.png)

Wanneer gebeëindigd, selecteer het schemapictogram om de interface van het doelschema te sluiten.

![ schema-boom ](../images/ui/mapping/schema-tree.png)

#### Berekende velden {#calculated-fields}

Met berekende velden kunnen waarden worden gemaakt op basis van de kenmerken in het invoerschema. Deze waarden kunnen vervolgens aan kenmerken in het doelschema worden toegewezen en een naam en beschrijving worden gegeven om de referentie eenvoudiger te maken. Berekende velden mogen maximaal 4096 tekens lang zijn.

Als u een berekend veld wilt maken, selecteert u **[!UICONTROL New field type]** en selecteert u vervolgens **[!UICONTROL Add calculated field]**

![ toe:voegen-berekend-gebied ](../images/ui/mapping/add-calculated-field.png)

Het deelvenster **[!UICONTROL Create calculated field]** wordt weergegeven. Het linkerdialoogvenster bevat de velden, functies en operatoren die in berekende velden worden ondersteund. Selecteer een van de tabbladen om functies, velden of operatoren toe te voegen aan de expressie-editor.

| Tabtoets | Beschrijving |
| --- | ----------- |
| [!UICONTROL Function] | Op het tabblad Functies staan de functies die beschikbaar zijn voor het transformeren van de gegevens. Om meer over de functies te leren u binnen berekende gebieden kunt gebruiken, te lezen gelieve de gids op [ gebruikend de functies van de Prep van Gegevens (Mapper) ](../functions.md). |
| [!UICONTROL Field] | Het tabblad Veld bevat velden en kenmerken die beschikbaar zijn in het bronschema. |
| [!UICONTROL Operator] | Het tabblad Operatoren bevat een lijst met operatoren die beschikbaar zijn om de gegevens te transformeren. |

![ lusjes ](../images/ui/mapping/tabs.png)

U kunt handmatig velden, functies en operatoren toevoegen met de expressieeditor in het midden. Selecteer de editor om een expressie te maken. Als u klaar bent, selecteert u **[!UICONTROL Save]** om door te gaan.

![ creeer-berekend-gebied ](../images/ui/mapping/create-calculated-field.png)

### Toewijzing importeren {#import}

U kunt de afbeelding van een bestaande gegevensstroom opnieuw gebruiken om de handmatige configuratietijd van uw gegevensinvoer te verminderen en fouten te beperken. Selecteer **[!UICONTROL Import mapping]** om een bestaande toewijzing opnieuw te gebruiken.

![ invoer-afbeelding ](../images/ui/mapping/import-mapping.png)

Het venster [!UICONTROL Import mapping] wordt weergegeven en bevat een lijst met gegevensstromen waaruit u kunt kiezen.

Selecteer het voorvertoningspictogram om een voorvertoning weer te geven van de toewijzing van de gegevensstroom die u hebt geselecteerd.

![ lijst-afbeelding ](../images/ui/mapping/list-mapping.png)

In het voorvertoningsvenster kunt u bestaande toewijzingen controleren voordat u deze importeert naar uw gegevensstroom. Nadat u de toewijzing hebt geverifieerd, kunt u **[!UICONTROL Back]** selecteren om terug te keren naar de lijst met gegevensstromen en een andere set toewijzingen te inspecteren. U kunt ook **[!UICONTROL Select]** selecteren om door te gaan.

![ voorproef-afbeelding ](../images/ui/mapping/preview-mapping.png)

U kunt ook de toewijzing selecteren die u wilt importeren in de lijst met gegevensstromen. Selecteer de gegevensstroom die de afbeelding bevat die u wilt importeren en selecteer vervolgens **[!UICONTROL Select]** om verder te gaan.

![ selecteren-afbeelding ](../images/ui/mapping/select-mapping.png)

De interface wordt bijgewerkt met de toewijzing u invoerde.

>[!NOTE]
>
>Om het even welke bestaande bijstellingsreeksen die u vestigt of de kaartaanbevelingen van ML worden vervangen door de afbeelding die u uit een bestaande dataflow invoerde.

![ afbeelding-ingevoerde ](../images/ui/mapping/mapping-imported.png)

Selecteer **[!UICONTROL Preview data]** om toewijzingsresultaten van maximaal 100 rijen met steekproefgegevens van de geselecteerde dataset te zien.

![ voorproef-gegevens ](../images/ui/mapping/preview-data.png)

Tijdens de voorvertoning krijgt de identiteitskolom de prioriteit als het eerste veld, omdat dit de belangrijkste informatie is die nodig is voor het valideren van toewijzingsresultaten. Selecteer **[!UICONTROL Close]** als u klaar bent.

![ voorproef-scherm ](../images/ui/mapping/preview-screen.png)

Selecteer **[!UICONTROL Clear all mappings]** als u alle toewijzingsvelden wilt verwijderen.

![ duidelijk-allen ](../images/ui/mapping/clear-all.png)

### De toewijzingsinterface gebruiken

Het platform verstrekt automatisch intelligente aanbevelingen voor auto-in kaart gebrachte gebieden die op het doelschema of de dataset worden gebaseerd dat u selecteerde. U kunt toewijzingsregels handmatig aanpassen aan uw gebruikscase of gedupliceerde toewijzingsvelden corrigeren om eventuele fouten te wissen.

![ afbeelding-interface ](../images/ui/mapping/mapping-interface.png)

Selecteer het gloeilamppictogram in het doelveld dat u wilt aanpassen.

![ afbeelding-recc ](../images/ui/mapping/mapping-recc.png)

Het pop-upvenster [!UICONTROL Mapping recommendations] wordt weergegeven met een lijst aanbevolen doelvelden die aan een bepaald bronveld kunnen worden toegewezen. Standaard wordt de eerste aanbeveling automatisch toegepast.

Soms is er meer dan één aanbeveling beschikbaar voor het bronschema. Wanneer dit gebeurt, toont de kaart de meest prominente aanbeveling, die door een pictogram wordt gevolgd dat het aantal extra beschikbare aanbevelingen bevat. Als u het gloeilamppictogram selecteert, wordt een lijst met aanvullende aanbevelingen weergegeven. U kunt één van de afwisselende aanbevelingen kiezen door checkbox naast de aanbeveling te selecteren u aan in plaats daarvan wilt in kaart brengen.

Hier kunt u het geselecteerde doelveld wijzigen om een fout te corrigeren of het te gebruiken geval te laten overeenkomen.

U kunt ook **[!UICONTROL Select manually]** selecteren om handmatig de interactieve toewijzingsstructuur van het doelschema te gebruiken.

![ recc-paneel ](../images/ui/mapping/recc-panel.png)

De toewijzingsinterface van het doelschema verschijnt in de zelfde mening zoals uw toewijzingsgebieden, toestaand u om kaartparen binnen het zelfde scherm te wijzigen. Selecteer het doelveld dat bij uw gebruikscase past of corrigeer de fouten.

![ selecteren-doel-gebied ](../images/ui/mapping/select-target-field.png)

Als u klaar bent, selecteert u **[!UICONTROL Finish]** om door te gaan.

![ beëindigen ](../images/ui/mapping/finish.png)

## Volgende stappen

Door dit document te lezen, hebt u een CSV-bestand met succes toegewezen aan een doel-XDM-schema met behulp van de toewijzingsinterface in de interface van het Platform. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van Data Prep](../home.md)
* [Overzicht van bronnen](../../sources/home.md)
* [Gegevensstromen van bronnen controleren in de UI](../../dataflows/ui/monitor-sources.md)
