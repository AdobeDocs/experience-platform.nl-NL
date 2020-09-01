---
keywords: Experience Platform;home;popular topics;data governance;data usage label;policy service;data usage labels user guide
solution: Experience Platform
title: Gebruiksaanwijzing voor labels voor gegevensgebruik
topic: labels
description: In deze gebruikershandleiding vindt u de stappen voor het werken met labels voor gegevensgebruik (ook wel DULE-labels genoemd) in de Adobe Experience Platform-gebruikersinterface.
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---


# Gebruiksaanwijzing voor labels voor gegevensgebruik

In deze gebruikershandleiding vindt u de stappen voor het werken met labels voor gegevensgebruik (ook wel DULE-labels genoemd) in de [!DNL Experience Platform] gebruikersinterface. Voordat u de gids gebruikt, raadpleegt u het overzicht [van](../home.md) gegevensbeheer voor een robuustere inleiding op het DULE-kader.

## De etiketten van het gegevensgebruik op het datasetniveau beheren

Om de etiketten van het gegevensgebruik op het datasetniveau te beheren, moet u een bestaande dataset selecteren of nieuwe creëren. Nadat u zich hebt aangemeld bij Adobe Experience Platform, selecteert u **[!UICONTROL Datasets]** in de linkernavigatie om de werkruimte _Datasets_ te openen. Deze pagina maakt een lijst van alle gecreeerde datasets die tot uw organisatie behoren, samen met nuttige details met betrekking tot elke dataset.

![Tabblad Gegevensset in werkruimte Gegevens](../images/labels/datasets.png)

De volgende sectie verstrekt stappen voor het creëren van een nieuwe dataset om etiketten op toe te passen. Als u etiketten voor een bestaande dataset wenst uit te geven, selecteer de dataset van de lijst en ga vooruit naar het [toevoegen van de etiketten van het gegevensgebruik aan de dataset](#add-labels).

### Een nieuwe gegevensset maken

>[!NOTE]
>
>In dit voorbeeld, wordt een dataset gecreeerd gebruikend een pre-gevormd [!DNL Experience Data Model] (XDM) schema. Voor meer informatie over schema&#39;s XDM, zie het [XDM Overzicht](../../xdm/home.md) van het Systeem en de [grondbeginselen van schemacompositie](../../xdm/schema/composition.md).

Als u een nieuwe gegevensset wilt maken, klikt u op Gegevensset **** maken rechtsboven in de werkruimte **[!UICONTROL Datasets]** .

![](../images/labels/create_dataset.png)

Het scherm Gegevensset **[!UICONTROL maken]** wordt weergegeven. Klik hier op Gegevensset **[!UICONTROL maken van schema]**.

![Dataset maken van schema](../images/labels/dataset_create.png)

Het **[!UICONTROL Uitgezochte scherm van het Schema]** verschijnt, dat van alle beschikbare schema&#39;s een lijst maakt die u voor het creëren van een dataset kunt gebruiken. Klik op het keuzerondje naast een schema om het te selecteren. In de sectie **[!UICONTROL Schema]** rechts ziet u aanvullende details over het geselecteerde schema. Als u een schema hebt geselecteerd, klikt u op **[!UICONTROL Volgende]**.

![Datasetschema selecteren](../images/labels/dataset_schema.png)

Het scherm Gegevensset **[!UICONTROL configureren]** wordt weergegeven. Geef een **naam** (vereist) en een **beschrijving** (optioneel, maar aanbevolen) voor de nieuwe gegevensset op en klik vervolgens op **[!UICONTROL Voltooien]**.

![Gegevensset configureren met naam en beschrijving](../images/labels/dataset_configure.png)

De pagina Activiteit **[!UICONTROL van de]** Dataset verschijnt, tonend informatie over de pas gecreëerde dataset. In dit voorbeeld krijgt de dataset de naam &quot;Loyalty-leden&quot;. In de bovenste navigatie ziet u daarom **Datasets > Loyalty-leden**.

![Pagina Gegevensactiviteit](../images/labels/dataset_activity.png)

### Gegevensgebruikslabels toevoegen aan de gegevensset {#add-labels}

Na het creëren van een nieuwe dataset of het selecteren van een bestaande dataset van de lijst in de werkruimte van **[!UICONTROL Datasets]** , klik **[!UICONTROL Gegevensbeheer]** om de werkruimte van het Beheer van **** Gegevens te openen. De werkruimte staat u toe om de etiketten van het gegevensgebruik op het datasetniveau en gebiedsniveau te beheren.

![Tabblad Gegevensbeheer gegevensset](../images/labels/dataset_data_governance.png)

Om de etiketten van het gegevensgebruik op het datasetniveau uit te geven, begin door het potloodpictogram naast de naam van de dataset te klikken.

![Labels op gegevensniveau bewerken](../images/labels/dataset_labels_edit_button.png)

Het dialoogvenster **[!UICONTROL Regellabels]** bewerken wordt geopend. Controleer in het dialoogvenster de vakken naast de labels die u op de gegevensset wilt toepassen. Herinner dat deze etiketten door alle gebieden binnen de dataset zullen worden geërft. De koptekst **[!UICONTROL Toegepaste labels]** wordt bijgewerkt terwijl u elk selectievakje inschakelt en de door u gekozen labels worden weergegeven. Als u de gewenste labels hebt geselecteerd, klikt u op Wijzigingen **** opslaan.

<img alt="Regelgevingslabels toepassen op datumniveau" src="../images/labels/apply-labels-dataset.png" width="700"><br>

De werkruimte **[!UICONTROL Gegevensbeheer]** verschijnt opnieuw, die de etiketten tonen die u op het datasetniveau hebt toegepast. U kunt ook zien dat de labels onderaan elk van de velden in de gegevensset worden overgeërfd.

![Labels voor gegevenssets die zijn overgeërfd door velden](../images/labels/dataset_inherited_labels.png)

U ziet dat een &quot;x&quot; wordt weergegeven naast de labels op datasetniveau, zodat u de labels kunt verwijderen. De overgeërfde labels naast elk veld hebben geen &quot;x&quot; en worden &quot;grijs&quot; weergegeven zonder dat u deze kunt verwijderen of bewerken. Dit komt doordat **overgeërfde velden alleen**-lezen zijn, wat betekent dat ze niet op veldniveau kunnen worden verwijderd.

De **[!UICONTROL Show Geërfte schakeloptie van Etiketten]** is door gebrek, dat u toestaat om het even welke etiketten te zien die neer van de dataset aan zijn gebieden worden geërft. Als u de schakeloptie uitschakelt, worden alle overgeërfde labels in de gegevensset verborgen.

![Overerfde labels verbergen](../images/labels/hide_inherited_labels.png)

## De etiketten van het gegevensgebruik op het niveau van het datasetgebied beheren

Als u doorgaat met de workflow voor het [toevoegen en bewerken van labels voor gegevensgebruik op het niveau](#add-labels)van de gegevensset, kunt u ook labels op veldniveau beheren in de werkruimte **[!UICONTROL Gegevensbeheer]** voor die gegevensset.

Als u gegevensgebruikslabels op een afzonderlijk veld wilt toepassen, schakelt u het selectievakje naast de veldnaam in en klikt u op **[!UICONTROL Regellabels]** bewerken.

![Veldlabels bewerken](../images/labels/fields_single_field.png)

Het dialoogvenster **[!UICONTROL Regellabels]** bewerken wordt weergegeven. In het dialoogvenster worden kopteksten weergegeven met de geselecteerde velden, toegepaste labels en overgeërfde labels. De overgeërfde labels (C2 en C5) worden grijs weergegeven in het dialoogvenster. Zij zijn read-only etiketten die van het datasetniveau worden geërft en zijn daarom slechts editable op het datasetniveau.

<img alt="Regellabels bewerken voor een afzonderlijk veld" src="../images/labels/field-label-inheritance.png" width="700"><br>

Selecteer labels op veldniveau door op het selectievakje naast elk label te klikken dat u wilt gebruiken. Terwijl u labels selecteert, wordt de koptekst **[!UICONTROL Toegepaste labels]** bijgewerkt met labels die zijn toegepast op de velden die worden weergegeven in de koptekst **[!UICONTROL Geselecteerde velden]** . Als u klaar bent met het selecteren van labels op veldniveau, klikt u op Wijzigingen **** opslaan.

<img alt="Labels op veldniveau toepassen" src="../images/labels/apply-labels-field.png" width="700"><br>

De werkruimte **[!UICONTROL Gegevensbeheer]** wordt opnieuw weergegeven, waardoor nu de geselecteerde labels op veldniveau in de rij naast de veldnaam worden weergegeven. Het label op veldniveau heeft een &#39;x&#39; naast het label, zodat u het label kunt verwijderen.

![Veld dat labels op veldniveau weergeeft](../images/labels/fields_show_field_level_labels.png)

U kunt deze stappen herhalen om door te gaan met het toevoegen en bewerken van labels op veldniveau voor extra velden, waaronder het selecteren van meerdere velden om labels op veldniveau tegelijk toe te passen.

![Selecteer meerdere velden om labels op veldniveau tegelijk toe te passen.](../images/labels/fields_select_multiple.png)

Het is belangrijk om te herinneren dat de overerving zich van top-level slechts (dataset → gebieden) beweegt, betekenend dat de etiketten die op het gebiedsniveau worden toegepast niet aan andere gebieden of datasets worden verspreid.

## Aangepaste labels beheren

U kunt uw eigen labels voor aangepast gebruik maken in de werkruimte **[!UICONTROL Beleid]** in de [!DNL Experience Platform] gebruikersinterface. Klik op **[!UICONTROL Beleid]** in de linkernavigatie en klik vervolgens op **[!UICONTROL Labels]** om een lijst met bestaande labels weer te geven. Klik hier op Label **** maken.

![](../images/labels/create-label-btn.png)

Het **[!UICONTROL dialoogvenster Label]** maken wordt weergegeven. Geef vanaf hier de volgende informatie op voor het nieuwe label:

* **[!UICONTROL Id]**: Een unieke id voor het label. Deze waarde wordt gebruikt voor opzoekdoeleinden en moet daarom kort en beknopt zijn.
* **[!UICONTROL Naam]**: Een vriendelijke weergavenaam voor het label.
* **[!UICONTROL Omschrijving]**: (Optioneel) Een beschrijving van het label voor verdere context.

When finished, click **[!UICONTROL Create]**.

![](../images/labels/create-label.png)

Het dialoogvenster wordt gesloten en het nieuwe aangepaste label wordt weergegeven in de lijst onder het tabblad **[!UICONTROL Labels]** .

![](../images/labels/label-created.png)

Het label kan nu worden geselecteerd onder **[!UICONTROL Aangepaste labels]** wanneer u gebruikslabels bewerkt voor gegevenssets en velden of wanneer u beleidsregels voor gegevensgebruik maakt.

<img src="../images/labels/add-custom-label.png" width="600" /><br>

## Volgende stappen

Nu u de etiketten van het gegevensgebruik op de dataset en gebiedsniveau hebt toegevoegd, kunt u beginnen om gegevens in te nemen [!DNL Experience Platform]. Voor meer informatie begint u met het lezen van de [gegevensinvoerdocumentatie](../../ingestion/home.md).

U kunt nu ook beleid voor gegevensgebruik definiëren op basis van de labels die u hebt toegepast. Zie het overzicht [van beleidsregels voor](../policies/overview.md)gegevensgebruik voor meer informatie.

## Aanvullende bronnen

De volgende video is bedoeld om uw begrip van te steunen, [!DNL Data Governance]en schetst hoe te om etiketten op een dataset en individuele gebieden toe te passen.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
