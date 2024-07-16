---
title: Een CSV-bestand toewijzen aan een XDM-schema met behulp van door AI gegenereerde Recommendations
description: In deze zelfstudie wordt uitgelegd hoe u een CSV-bestand met behulp van door AI gegenereerde aanbevelingen kunt toewijzen aan een XDM-schema.
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: 6632086641004c2b788a28cbc47ac6d8bd4eace3
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# Een CSV-bestand toewijzen aan een XDM-schema met behulp van door AI gegenereerde aanbevelingen

>[!NOTE]
>
>Voor informatie over algemeen beschikbare CSV afbeeldingsmogelijkheden in Platform, zie het document op [ afbeelding een Csv- dossier aan een bestaand schema ](./existing-schema.md).

Als u CSV-gegevens in [!DNL Adobe Experience Platform] wilt invoeren, moeten de gegevens worden toegewezen aan een [!DNL Experience Data Model] (XDM)-schema. U kunt verkiezen om aan [ een bestaand schema ](./existing-schema.md) in kaart te brengen, maar als u niet precies weet welk schema te gebruiken of hoe het zou moeten worden gestructureerd, kunt u dynamische aanbevelingen gebruiken die op machine-leert (ML) modellen binnen Platform UI worden gebaseerd.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende componenten van [!DNL Platform] :

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Platform] gegevens voor de klantervaring indeelt.
   * Bij een minimum, moet u het concept [ gedrag in XDM ](../../../xdm/home.md#data-behaviors) begrijpen, zodat kunt u besluiten of om uw gegevens aan een [!UICONTROL Profile] klasse (verslaggedrag) of [!UICONTROL ExperienceEvent] klasse (tijd-reeksen gedrag) in kaart te brengen.
* [ Inname van de Partij ](../../batch-ingestion/overview.md): De methode waardoor [!DNL Platform] gegevens van user-provided gegevensbestanden opneemt.
* [ Prep van Gegevens van Adobe Experience Platform ](../../batch-ingestion/overview.md): Een reeks mogelijkheden die u toestaan om opgenomen gegevens in kaart te brengen en om te zetten om met schema&#39;s in overeenstemming te zijn XDM. De documentatie over [ Prep functies van Gegevens ](../../../data-prep/functions.md) is specifiek relevant voor schemaafbeelding.

## Gegevens over gegevensstroom opgeven

Selecteer **[!UICONTROL Sources]** in de gebruikersinterface van het Experience Platform in de linkernavigatie. Navigeer in de weergave **[!UICONTROL Catalog]** naar de categorie **[!UICONTROL Local system]** . Selecteer onder **[!UICONTROL Local file upload]** de optie **[!UICONTROL Add data]** .

![ de [!UICONTROL Sources] catalogus in Platform UI, met [!UICONTROL Add data] onder [!UICONTROL Local file upload] die wordt geselecteerd.](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

De **[!UICONTROL Map CSV XDM schema]** -workflow wordt weergegeven, vanaf de **[!UICONTROL Dataflow detail]** -stap.

Selecteer **[!UICONTROL Create a new schema using ML recommendations]** , zodat er nieuwe besturingselementen worden weergegeven. Kies de juiste klasse voor de CSV-gegevens die u wilt toewijzen ([!UICONTROL Profile] of [!UICONTROL ExperienceEvent]). U kunt optioneel het vervolgkeuzemenu gebruiken om de relevante branche voor uw bedrijf te selecteren of leeg laten als de opgegeven categorieën niet op u van toepassing zijn. Als uw organisatie onder a [ zaken-aan-zaken (B2B) ](../../../xdm/tutorials/relationship-b2b.md) model werkt, selecteer **[!UICONTROL B2B data]** checkbox.

![ de [!UICONTROL Dataflow detail] stap met de geselecteerde de aanbeveling van ML optie. [!UICONTROL Profile] wordt geselecteerd voor de klasse en [!UICONTROL Telecommunications] geselecteerd voor de industrie ](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

Van hier, verstrek een naam voor het schema dat van de CSV- gegevens zal worden gecreeerd, en een naam voor de outputdataset die de gegevens zal bevatten die onder dat schema worden opgenomen.

U kunt naar keuze de volgende extra eigenschappen voor dataflow vormen alvorens te werk te gaan:

| Invoernaam | Beschrijving |
| --- | --- |
| [!UICONTROL Description] | Een beschrijving voor de gegevensstroom. |
| [!UICONTROL Error diagnostics] | Wanneer toegelaten, worden de foutenmeldingen geproduceerd voor onlangs opgenomen partijen, die kunnen worden bekeken wanneer het halen van de overeenkomstige partij in [ API ](../../batch-ingestion/api-overview.md). |
| [!UICONTROL Partial ingestion] | Als deze optie is ingeschakeld, worden geldige records voor nieuwe batchgegevens opgenomen binnen een opgegeven foutdrempel. Deze drempel staat u toe om het percentage aanvaardbare fouten te vormen alvorens de volledige partij ontbreekt. |
| [!UICONTROL Dataflow details] | Geef een naam en een optionele beschrijving voor de gegevensstroom op die de CSV-gegevens naar Platform overbrengt. Aan de gegevensstroom wordt automatisch een standaardnaam toegewezen wanneer u deze workflow start. Het wijzigen van de naam is optioneel. |
| [!UICONTROL Alerts] | Selecteer uit een lijst van [ in-product alarm ](../../../observability/alerts/overview.md) dat u betreffende de status van dataflow wilt ontvangen zodra het in werking is gesteld. |

{style="table-layout:auto"}

Wanneer u klaar bent met het configureren van de gegevensstroom, selecteert u **[!UICONTROL Next]** .

![ de [!UICONTROL Dataflow detail] sectie wordt voltooid.](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## Gegevens selecteren

Gebruik in de stap **[!UICONTROL Select data]** de linkerkolom om het CSV-bestand te uploaden. U kunt **[!UICONTROL Choose files]** selecteren om een dialoogvenster voor bestandsverkenning te openen waarin u het bestand kunt selecteren. U kunt het bestand ook rechtstreeks naar de kolom slepen.

![ de [!UICONTROL Choose files] knoop en belemmering-en-dalingsgebied binnen de [!UICONTROL Select data] stap wordt benadrukt.](../../images/tutorials/map-csv-recommendations/upload-files.png)

Na het uploaden van het bestand wordt een voorbeeldgegevenssectie weergegeven met de eerste tien rijen van de ontvangen gegevens, zodat u kunt controleren of deze correct zijn geüpload. Selecteer **[!UICONTROL Next]** om door te gaan.

![ de gegevensrijen van de Steekproef zijn bevolkt binnen de werkruimte ](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## Schema-toewijzingen configureren

De modellen van XML worden in werking gesteld om een nieuw schema te produceren dat op uw dataflow configuratie en uw geupload Csv- dossier wordt gebaseerd. Wanneer het proces is voltooid, wordt de stap [!UICONTROL Mapping] gevuld om de toewijzingen voor elk afzonderlijk veld weer te geven naast de volledig navigeerbare weergave van de gegenereerde schemastructuur.

![ de [!UICONTROL Mapping] stap in UI, die alle in kaart gebrachte gebieden CSV en de resulterende schemastructuur toont.](../../images/tutorials/map-csv-recommendations/schema-generated.png)

>[!NOTE]
>
>U kunt alle velden in uw schema filteren op basis van verschillende criteria tijdens de toewijzingsworkflow van bron naar doel voor velden. Standaard worden alle toegewezen velden weergegeven. Om de getoonde gebieden te veranderen, selecteer het filterpictogram naast het gebied van de onderzoeksinput en kies van de dropdown opties.<br> ![ het kaartingsstadium van CSV aan het werkschema van de het schemaverwezenlijking XDM met het filterpictogram en dropdown benadrukt menu.](../../images/tutorials/map-csv-recommendations/source-field-to-target-mapping-filter.png " het kaartingsstadium van CSV aan het werkschema van de het schemaverwezenlijking XDM met het benadrukte filterpictogram en dropdown menu."){width="100" zoomable="yes"}

Van hier, kunt u naar keuze [ de gebiedstoewijzingen ](#edit-mappings) of [ uitgeven de gebiedsgroepen zij met ](#edit-schema) volgens uw behoeften worden geassocieerd. Selecteer **[!UICONTROL Finish]** als u tevreden bent om de toewijzing te voltooien en de dataflow die u eerder hebt geconfigureerd, te starten. De gegevens CSV wordt opgenomen in het systeem en bevolkt een dataset die op de geproduceerde schemastructuur wordt gebaseerd, klaar om door de stroomafwaartse diensten van het Platform worden verbruikt.

![ de [!UICONTROL Finish] knoop die wordt geselecteerd, die het proces voltooit van de afbeelding CSV.](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### Veldtoewijzingen bewerken {#edit-mappings}

Gebruik de voorvertoning van de veldtoewijzing om bestaande toewijzingen te bewerken of volledig te verwijderen. Voor meer informatie over hoe te om een afbeelding te beheren die in UI wordt geplaatst, verwijs naar de [ gids UI voor de afbeelding van de Prep van Gegevens ](../../../data-prep/ui/mapping.md#mapping-interface).

### Veldgroepen bewerken {#edit-field-groups}

De CSV-velden worden automatisch toegewezen aan bestaande XDM-veldgroepen met behulp van XML-modellen. Als u de veldgroep voor een bepaald CSV-veld wilt wijzigen, selecteert u **[!UICONTROL Edit]** naast de schemastructuur.

![ de [!UICONTROL Edit] knoop die naast de schemaboom wordt geselecteerd.](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

Er wordt een dialoogvenster weergegeven waarin u de weergavenaam, het gegevenstype en de veldgroep voor een veld in de toewijzing kunt bewerken. Selecteer uitgeven pictogram (![ geeft pictogram ](../../images/tutorials/map-csv-recommendations/edit-icon.png) uit) naast een brongebied om zijn details in de juiste kolom uit te geven alvorens **[!UICONTROL Apply]** te selecteren.

![ de geadviseerde gebiedsgroep voor een brongebied dat wordt veranderd.](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

Wanneer u klaar bent met het aanpassen van de schemaaanbevelingen voor uw brongebieden, uitgezocht **[!UICONTROL Save]** om de veranderingen toe te passen.

## Volgende stappen

Deze gids behandelde hoe te om een Csv- dossier aan een XDM- schema in kaart te brengen gebruikend AI-Gegenereerde aanbevelingen, die u toestaan om die gegevens in Platform door partijingesetion te brengen.

Voor stappen bij het in kaart brengen van een Csv- dossier aan een bestaand schema, verwijs naar het [ bestaande schema in kaart brengende werkschema ](./existing-schema.md). Voor informatie bij het stromen gegevens aan Platform in real time door prebuilt bronverbindingen, verwijs naar het [ overzicht van bronnen ](../../../sources/home.md).
