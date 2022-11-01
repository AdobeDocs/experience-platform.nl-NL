---
title: Een CSV-bestand toewijzen aan een XDM-schema met behulp van door AI gegenereerde Recommendations (bèta)
description: In deze zelfstudie wordt uitgelegd hoe u een CSV-bestand met behulp van door AI gegenereerde aanbevelingen kunt toewijzen aan een XDM-schema.
source-git-commit: d6f858af8bc44be74b1aaf12b973fb6818c1b2a5
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 0%

---

# Een CSV-bestand toewijzen aan een XDM-schema met behulp van door AI gegenereerde aanbevelingen (bèta)

>[!IMPORTANT]
>
>Deze functie bevindt zich momenteel in bèta en uw organisatie heeft er wellicht nog geen toegang toe. De documentatie en functionaliteit kunnen worden gewijzigd.
>
>Zie het document over [een CSV-bestand toewijzen aan een bestaand schema](./existing-schema.md).

Om CSV-gegevens in te nemen [!DNL Adobe Experience Platform], moeten de gegevens worden toegewezen aan een [!DNL Experience Data Model] (XDM) schema. U kunt kiezen om toe te wijzen aan [een bestaand schema](./existing-schema.md), maar als u niet precies weet welk schema te gebruiken of hoe het zou moeten worden gestructureerd, kunt u dynamische aanbevelingen gebruiken die op machine-leert (ML) modellen in de UI van het Platform worden gebaseerd.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van [!DNL Platform]:

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Platform] organiseert de gegevens van de klantenervaring.
   * Op zijn minst moet u het concept van [gedragingen in XDM](../../../xdm/home.md#data-behaviors), zodat u kunt besluiten of u uw gegevens aan een [!UICONTROL Profile] klasse (recordgedrag) of [!UICONTROL ExperienceEvent] klasse (tijdreeksgedrag).
* [Inname in batch](../../batch-ingestion/overview.md): De methode waarbij [!DNL Platform] Hiermee worden gegevens uit door de gebruiker opgegeven gegevensbestanden opgenomen.
* [Adobe Experience Platform Data Prep](../../batch-ingestion/overview.md): Een reeks mogelijkheden die u toestaan om opgenomen gegevens in kaart te brengen en om te zetten om aan schema&#39;s in overeenstemming te zijn XDM. De documentatie over [Functies Data Prep](../../../data-prep/functions.md) is specifiek relevant voor schema-toewijzing.

## Gegevens over gegevensstroom opgeven

Selecteer in de gebruikersinterface van het Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie. Op de **[!UICONTROL Catalog]** bekijken, naar de **[!UICONTROL Local system]** categorie. Selecteer onder **[!UICONTROL Local file upload]** de optie **[!UICONTROL Add data]**.

![De [!UICONTROL Sources] catalogus in de gebruikersinterface van het Platform, met [!UICONTROL Add data] krachtens [!UICONTROL Local file upload] geselecteerd](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

De **[!UICONTROL Map CSV XDM schema]** wordt weergegeven, vanaf de **[!UICONTROL Dataflow detail]** stap.

Selecteren **[!UICONTROL Create a new schema using ML recommendations]**, waardoor nieuwe besturingselementen worden weergegeven. Kies de juiste klasse voor de CSV-gegevens die u wilt toewijzen ([!UICONTROL Profile] of [!UICONTROL ExperienceEvent]). U kunt optioneel het vervolgkeuzemenu gebruiken om de relevante branche voor uw bedrijf te selecteren of leeg laten als de opgegeven categorieën niet op u van toepassing zijn. Als uw organisatie onder een [business-to-business (B2B)](../../../xdm/tutorials/relationship-b2b.md) model, selecteer **[!UICONTROL B2B data]** selectievakje.

![De [!UICONTROL Dataflow detail] met de optie voor ML-aanbevelingen geselecteerd. [!UICONTROL Profile] is geselecteerd voor de klasse en [!UICONTROL Telecommunications] geselecteerd voor de industrie](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

Van hier, verstrek een naam voor het schema dat van de CSV- gegevens zal worden gecreeerd, en een naam voor de outputdataset die de gegevens zal bevatten die onder dat schema worden opgenomen.

U kunt naar keuze de volgende extra eigenschappen voor dataflow vormen alvorens te werk te gaan:

| Invoernaam | Beschrijving |
| --- | --- |
| [!UICONTROL Description] | Een beschrijving voor de gegevensstroom. |
| [!UICONTROL Error diagnostics] | Als deze optie is ingeschakeld, worden foutberichten gegenereerd voor nieuw opgenomen batches, die kunnen worden weergegeven wanneer de bijbehorende batch in het dialoogvenster [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL Partial ingestion] | Als deze optie is ingeschakeld, worden geldige records voor nieuwe batchgegevens opgenomen binnen een opgegeven foutdrempel. Deze drempel staat u toe om het percentage aanvaardbare fouten te vormen alvorens de volledige partij ontbreekt. |
| [!UICONTROL Dataflow details] | Geef een naam en een optionele beschrijving op voor de gegevensstroom waarmee de CSV-gegevens in het Platform worden geplaatst. Aan de gegevensstroom wordt automatisch een standaardnaam toegewezen wanneer u deze workflow start. Het wijzigen van de naam is optioneel. |
| [!UICONTROL Alerts] | Selecteren in een lijst met [waarschuwingen in producten](../../../observability/alerts/overview.md) dat u betreffende de status van de gegevensstroom wilt ontvangen zodra het in werking is gesteld. |

{style=&quot;table-layout:auto&quot;}

Wanneer u klaar bent met het configureren van de gegevensstroom, selecteert u **[!UICONTROL Next]**.

![De [!UICONTROL Dataflow detail] sectie is voltooid](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## Gegevens selecteren

Op de **[!UICONTROL Select data]** de linkerkolom gebruiken om uw CSV-bestand te uploaden. U kunt **[!UICONTROL Choose files]** om een dialoogvenster voor bestandsverkenning te openen waarin u het bestand kunt selecteren. U kunt het bestand ook rechtstreeks naar de kolom slepen.

![De [!UICONTROL Choose files] en gebied voor slepen en neerzetten gemarkeerd in het deelvenster [!UICONTROL Select data] stap](../../images/tutorials/map-csv-recommendations/upload-files.png)

Na het uploaden van het bestand wordt een voorbeeldgegevenssectie weergegeven met de eerste tien rijen van de ontvangen gegevens, zodat u kunt controleren of deze correct zijn geüpload. Selecteren **[!UICONTROL Next]** om door te gaan.

![Voorbeeldgegevensrijen worden ingevuld in de werkruimte](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## Schema-toewijzingen configureren

De modellen van XML worden in werking gesteld om een nieuw schema te produceren dat op uw dataflow configuratie en uw geupload Csv- dossier wordt gebaseerd. Wanneer het proces is voltooid, wordt [!UICONTROL Mapping] De stap wordt gevuld om de toewijzingen voor elk afzonderlijk veld weer te geven naast de volledig navigeerbare weergave van de gegenereerde schemastructuur.

![De [!UICONTROL Mapping] stap in UI, tonend alle CSV in kaart gebrachte gebieden en de resulterende schemastructuur](../../images/tutorials/map-csv-recommendations/schema-generated.png)

Van hier kunt u optioneel [veldtoewijzingen bewerken](#edit-mappings) of [de veldgroepen wijzigen waaraan ze zijn gekoppeld](#edit-schema) afhankelijk van uw behoeften. Selecteer **[!UICONTROL Finish]** om de afbeelding te voltooien en de dataflow in werking te stellen u vroeger vormde. De CSV-gegevens worden in het systeem opgenomen en vullen een gegevensset in die is gebaseerd op de gegenereerde schemastructuur en die klaar is om te worden verbruikt door downstream-services van Platforms.

![De [!UICONTROL Finish] knop die wordt geselecteerd, het CSV-toewijzingsproces voltooien](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### Veldtoewijzingen bewerken {#edit-mappings}

Gebruik de voorvertoning van de veldtoewijzing om bestaande toewijzingen te bewerken of volledig te verwijderen. Raadpleeg voor meer informatie over het beheren van een toewijzingsset in de gebruikersinterface de [UI-handleiding voor gegevenstoewijzing](../../../data-prep/ui/mapping.md#mapping-interface).

### Veldgroepen bewerken {#edit-field-groups}

De CSV-velden worden automatisch toegewezen aan bestaande XDM-veldgroepen met behulp van XML-modellen. Als u de veldgroep voor een bepaald CSV-veld wilt wijzigen, selecteert u **[!UICONTROL Edit]** naast de schemastructuur.

![De [!UICONTROL Edit] knop die wordt geselecteerd naast de schemaboom](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

Er wordt een dialoogvenster weergegeven waarin u de weergavenaam, het gegevenstype en de veldgroep voor een veld in de toewijzing kunt bewerken. Selecteer het bewerkingspictogram (![Pictogram Bewerken](../../images/tutorials/map-csv-recommendations/edit-icon.png)) naast een bronveld om de details in de rechterkolom te bewerken voordat u het veld selecteert **[!UICONTROL Apply]**.

![De aanbevolen veldgroep voor een bronveld dat wordt gewijzigd](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

Wanneer u klaar bent met het aanpassen van de schemaaanbevelingen voor uw brongebieden, selecteer **[!UICONTROL Save]** om de wijzigingen toe te passen.

## Volgende stappen

Deze gids behandelde hoe te om een Csv- dossier aan een XDM- schema in kaart te brengen gebruikend AI-Gegenereerde aanbevelingen, die u toestaan om die gegevens in Platform door partijopname te brengen.

Voor stappen voor het toewijzen van een CSV-bestand aan een bestaand schema raadpleegt u de [bestaande schema-toewijzingsworkflow](./existing-schema.md). Voor informatie over het stromen gegevens aan Platform in real time door prebuilt bronverbindingen, verwijs naar [overzicht van bronnen](../../../sources/home.md).
