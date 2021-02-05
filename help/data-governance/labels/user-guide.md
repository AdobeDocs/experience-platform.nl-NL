---
keywords: Experience Platform;home;populaire onderwerpen;gegevensbeheer;label voor gegevensgebruik;beleidsservice;gebruikershandleiding voor labels voor gegevensgebruik
solution: Experience Platform
title: Labels voor gegevensgebruik beheren in de gebruikersinterface
topic: labels
description: In deze handleiding vindt u de stappen voor het werken met labels voor gegevensgebruik in de Adobe Experience Platform-gebruikersinterface.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 0%

---


# Labels voor gegevensgebruik beheren in de gebruikersinterface

In deze gebruikershandleiding worden de stappen beschreven voor het werken met labels voor gegevensgebruik in de gebruikersinterface [!DNL Experience Platform]. Voordat u de handleiding kunt gebruiken, raadpleegt u het [[!DNL Data Governance] overzicht](../home.md) voor een robuustere introductie van het [!DNL Data Governance]-framework.

## Labels beheren op het niveau van de gegevensset

Om de etiketten van het gegevensgebruik op het datasetniveau te beheren, moet u een bestaande dataset selecteren of nieuwe creëren. Nadat u zich hebt aangemeld bij Adobe Experience Platform, selecteert u **[!UICONTROL Datasets]** in de linkernavigatie om de **[!UICONTROL Datasets]**-werkruimte te openen. Deze pagina maakt een lijst van alle gecreeerde datasets die tot uw organisatie behoren, samen met nuttige details met betrekking tot elke dataset.

![Tabblad Gegevensset in werkruimte Gegevens](../images/labels/datasets.png)

De volgende sectie verstrekt stappen voor het creëren van een nieuwe dataset om etiketten op toe te passen. Als u etiketten voor een bestaande dataset wilt uitgeven, selecteer de dataset van de lijst en ga vooruit naar [toevoegend de etiketten van het gegevensgebruik aan dataset](#add-labels).

### Een nieuwe gegevensset maken

>[!NOTE]
>
>In dit voorbeeld, wordt een dataset gecreeerd gebruikend een vooraf gevormd [!DNL Experience Data Model] (XDM) schema. Voor meer informatie over schema&#39;s XDM, zie [XDM systeemoverzicht](../../xdm/home.md) en [grondbeginselen van schemacompositie](../../xdm/schema/composition.md).

Als u een nieuwe gegevensset wilt maken, selecteert u **[!UICONTROL Dataset maken]** in de rechterbovenhoek van de werkruimte **[!UICONTROL Datasets]**.

![](../images/labels/create_dataset.png)

Het scherm **[!UICONTROL Gegevensset maken]** wordt weergegeven. Van hier, uitgezochte **[!UICONTROL Create Dataset van Schema]**.

![Dataset maken van schema](../images/labels/dataset_create.png)

Het **[!UICONTROL Uitgezochte Schema]** scherm verschijnt, dat van alle beschikbare schema&#39;s een lijst maakt die u voor het creëren van een dataset kunt gebruiken. Selecteer het keuzerondje naast een schema om het te selecteren. In de sectie **[!UICONTROL Schemas]** rechts ziet u aanvullende details over het geselecteerde schema. Nadat u een schema hebt geselecteerd, selecteert u **[!UICONTROL Volgende]**.

![Datasetschema selecteren](../images/labels/dataset_schema.png)

Het scherm **[!UICONTROL Gegevensset configureren]** wordt weergegeven. Geef een naam (vereist) en beschrijving (optioneel, maar aanbevolen) voor de nieuwe gegevensset op en selecteer **[!UICONTROL Voltooien]**.

![Gegevensset configureren met naam en beschrijving](../images/labels/dataset_configure.png)

De **[!UICONTROL Dataset Activity]** pagina verschijnt, tonend informatie over de pas gecreëerde dataset. In dit voorbeeld krijgt de dataset de naam &quot;Loyalty-leden&quot;, daarom toont de top-navigation **Datasets > Loyalty-leden**.

![Pagina Gegevensactiviteit](../images/labels/dataset_activity.png)

### Gegevensgebruikslabels toevoegen aan de gegevensset {#add-labels}

Nadat u een nieuwe gegevensset hebt gemaakt of een bestaande gegevensset hebt geselecteerd in de lijst in de werkruimte **[!UICONTROL Datasets]**, selecteert u **[!UICONTROL Gegevensbeheer]** om de werkruimte **[!UICONTROL Gegevensbeheer]** te openen. De werkruimte staat u toe om de etiketten van het gegevensgebruik op het datasetniveau en gebiedsniveau te beheren.

![Tabblad Gegevensbeheer gegevensset](../images/labels/dataset_data_governance.png)

Om de etiketten van het gegevensgebruik op het datasetniveau uit te geven, begin door het potloodpictogram naast de naam van de dataset te selecteren.

![Labels op gegevensniveau bewerken](../images/labels/dataset_labels_edit_button.png)

Het dialoogvenster **[!UICONTROL Regellabels bewerken]** wordt geopend. Controleer in het dialoogvenster de vakken naast de labels die u op de gegevensset wilt toepassen. Herinner dat deze etiketten door alle gebieden binnen de dataset zullen worden geërft. De **[!UICONTROL Toegepaste labels]** kopbal werkt bij aangezien u elk vakje controleert, tonend de etiketten u hebt gekozen. Als u de gewenste labels hebt geselecteerd, selecteert u **[!UICONTROL Wijzigingen opslaan]**.

<img alt="Regelgevingslabels toepassen op datumniveau" src="../images/labels/apply-labels-dataset.png" width="700"><br>

De werkruimte **[!UICONTROL Gegevensbeheer]** wordt opnieuw weergegeven en toont de labels die u hebt toegepast op het niveau van de gegevensset. U kunt ook zien dat de labels onderaan elk van de velden in de gegevensset worden overgeërfd.

![Labels voor gegevenssets die zijn overgeërfd door velden](../images/labels/dataset_inherited_labels.png)

U ziet dat een &quot;x&quot; wordt weergegeven naast de labels op datasetniveau, zodat u de labels kunt verwijderen. De overgeërfde labels naast elk veld hebben geen &quot;x&quot; en worden &quot;grijs&quot; weergegeven zonder dat u deze kunt verwijderen of bewerken. Dit komt omdat **overgeërfde gebieden read-only** zijn, betekenend kunnen zij niet op het gebiedsniveau worden verwijderd.

De schakeloptie **[!UICONTROL Overerfde labels tonen]** is standaard ingeschakeld, zodat u alle labels kunt zien die zijn overgeërfd van de gegevensset naar de bijbehorende velden. Als u de schakeloptie uitschakelt, worden alle overgeërfde labels in de gegevensset verborgen.

![Overerfde labels verbergen](../images/labels/hide_inherited_labels.png)

## Labels op veldniveau beheren

Als u doorgaat met de workflow voor [het toevoegen en bewerken van labels voor gegevensgebruik op gegevenssetniveau](#add-labels), kunt u ook labels op veldniveau beheren in de werkruimte **[!UICONTROL Gegevensbeheer]** voor die gegevensset.

Als u gegevensgebruikslabels wilt toepassen op een afzonderlijk veld, schakelt u het selectievakje naast de veldnaam in en selecteert u **[!UICONTROL Regellabels bewerken]**.

![Veldlabels bewerken](../images/labels/fields_single_field.png)

Het dialoogvenster **[!UICONTROL Regellabels bewerken]** wordt weergegeven. In het dialoogvenster worden kopteksten weergegeven met de geselecteerde velden, toegepaste labels en overgeërfde labels. De overgeërfde labels (C2 en C5) worden grijs weergegeven in het dialoogvenster. Zij zijn read-only etiketten die van het datasetniveau worden geërft en zijn daarom slechts editable op het datasetniveau.

<img alt="Regellabels bewerken voor een afzonderlijk veld" src="../images/labels/field-label-inheritance.png" width="700"><br>

Selecteer labels op veldniveau door het selectievakje naast elk label dat u wilt gebruiken in te schakelen. Terwijl u labels selecteert, wordt de koptekst **[!UICONTROL Toegepaste labels]** bijgewerkt om labels weer te geven die zijn toegepast op de velden die worden weergegeven in de koptekst **[!UICONTROL Geselecteerde velden]**. Als u klaar bent met het selecteren van labels op veldniveau, selecteert u **[!UICONTROL Wijzigingen opslaan]**.

<img alt="Labels op veldniveau toepassen" src="../images/labels/apply-labels-field.png" width="700"><br>

De werkruimte **[!UICONTROL Gegevensbeheer]** wordt opnieuw weergegeven. In deze werkruimte worden nu de geselecteerde labels op veldniveau in de rij naast de veldnaam weergegeven. Het label op veldniveau heeft een &#39;x&#39; naast het label, zodat u het label kunt verwijderen.

![Veld dat labels op veldniveau weergeeft](../images/labels/fields_show_field_level_labels.png)

U kunt deze stappen herhalen om door te gaan met het toevoegen en bewerken van labels op veldniveau voor extra velden, waaronder het selecteren van meerdere velden om labels op veldniveau tegelijk toe te passen.

![Selecteer meerdere velden om labels op veldniveau tegelijk toe te passen.](../images/labels/fields_select_multiple.png)

Het is belangrijk om te herinneren dat de overerving zich van top-level slechts (dataset → gebieden) beweegt, betekenend dat de etiketten die op het gebiedsniveau worden toegepast niet aan andere gebieden of datasets worden verspreid.

## Aangepaste labels beheren

U kunt uw eigen etiketten van het douanegebruik binnen **[!UICONTROL Beleid]** werkruimte in [!DNL Experience Platform] UI tot stand brengen. Selecteer **[!UICONTROL Beleid]** in de linkernavigatie, dan uitgezocht **[!UICONTROL Etiketten]** om een lijst van bestaande etiketten te bekijken. Selecteer **[!UICONTROL Label maken]**.

![](../images/labels/create-label-btn.png)

Het dialoogvenster **[!UICONTROL Label maken]** wordt weergegeven. Geef vanaf hier de volgende informatie op voor het nieuwe label:

* **[!UICONTROL Id]**: Een unieke id voor het label. Deze waarde wordt gebruikt voor opzoekdoeleinden en moet daarom kort en beknopt zijn.
* **[!UICONTROL Naam]**: Een vriendelijke weergavenaam voor het label.
* **[!UICONTROL Omschrijving]**: (Optioneel) Een beschrijving van het label voor verdere context.

Selecteer **[!UICONTROL Maken]** als u klaar bent.

![](../images/labels/create-label.png)

Het dialoogvenster wordt gesloten en het nieuwe aangepaste label wordt weergegeven in de lijst onder het tabblad **[!UICONTROL Labels]**.

![](../images/labels/label-created.png)

Het label kan nu worden geselecteerd onder **[!UICONTROL Eigen labels]** wanneer u gebruikslabels voor gegevenssets en velden bewerkt of wanneer u beleidsregels voor gegevensgebruik maakt.

<img src="../images/labels/add-custom-label.png" width="600" /><br>

## Volgende stappen

Nu u de etiketten van het gegevensgebruik op het dataset en gebiedsniveau hebt toegevoegd, kunt u beginnen om gegevens in [!DNL Experience Platform] in te nemen. Als u meer wilt weten, begint u met het lezen van de [documentatie voor gegevensinvoer](../../ingestion/home.md).

U kunt nu ook beleid voor gegevensgebruik definiëren op basis van de labels die u hebt toegepast. Voor meer informatie, zie [beleidsoverzicht van het gegevensgebruik](../policies/overview.md).

## Aanvullende bronnen

De volgende video is bedoeld om uw begrip van [!DNL Data Governance] te steunen, en schetst hoe te om etiketten op een dataset en individuele gebieden toe te passen.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
