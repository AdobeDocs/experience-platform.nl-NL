---
keywords: Experience Platform;home;populaire onderwerpen;gegevensbeheer;label voor gegevensgebruik;beleidsservice;gebruikershandleiding voor labels voor gegevensgebruik
solution: Experience Platform
title: Labels voor gegevensgebruik beheren in de gebruikersinterface
description: In deze handleiding vindt u de stappen voor het werken met labels voor gegevensgebruik in de Adobe Experience Platform-gebruikersinterface.
exl-id: aa44d5cc-416a-4ef2-be14-b4f32aec162c
source-git-commit: 1690a73cf709594b82469e95aba64231cf216d96
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 0%

---

# Labels voor gegevensgebruik beheren in de gebruikersinterface {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_description"
>title="Gegevensgebruik in Platform beheren"
>abstract="<h2>Beschrijving</h2><p>Met het gegevensbeheerkader in Experience Platform kunt u kenmerken en schema&#39;s labelen op basis van beperkingen voor gegevensgebruik en beleidsregels instellen die deze beperkingen voor specifieke marketingacties identificeren en naleven.</p>"

In deze gebruikershandleiding worden de stappen beschreven voor het werken met labels voor gegevensgebruik in de [!DNL Experience Platform] gebruikersinterface.

## Labels beheren {#manage-labels}

Als u labels op uw gegevens wilt toepassen, hebt u de opdracht **[!UICONTROL Manage Usage Labels]** toestemming voor gebruik in de productiesandbox. Als u een aangepast label wilt maken, moet u ook over beheerdersrechten voor het productprofiel beschikken. Elke organisatie heeft slechts één lijst van toepasselijke etiketten, en momenteel, wordt het schrappen van etiketten niet gesteund.

Zie de handleiding over hoe u [machtigingen configureren](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html) of de [toegangsbeheeroverzicht](../../access-control/home.md) voor meer informatie over hoe te om een toestemming toe te wijzen. Neem contact op met de beheerder van uw organisatie als u geen toegang hebt tot de Admin Console voor uw organisatie.

## Labels op schemaniveau beheren

U kunt labels rechtstreeks toevoegen aan een schema of aan velden binnen dat schema. Om het even welke gebieden die op het schemaniveau worden toegepast zullen aan alle datasets verspreiden die op dat schema worden gebaseerd.

Als u labels voor gegevensgebruik op schemaniveau wilt beheren, moet u een bestaand schema selecteren of een nieuw schema maken. Nadat u zich hebt aangemeld bij Adobe Experience Platform, selecteert u **[!UICONTROL Schemas]** op de linkernavigatie om de **[!UICONTROL Schemas]** werkruimte. Deze pagina bevat een overzicht van alle gemaakte schema&#39;s die tot uw organisatie behoren, samen met nuttige details over elk schema.

![De gebruikersinterface van Adobe Experience Platform met het tabblad Schema gemarkeerd.](../images/labels/schema-tab.png)

In de volgende sectie vindt u stappen voor het maken van een nieuw schema waarop labels moeten worden toegepast. Als u labels voor een bestaand schema wilt bewerken, selecteert u het schema in de lijst en gaat u verder met [gegevensgebruikslabels toevoegen aan het schema](#add-labels).

### Een nieuw schema maken

Als u een nieuw schema wilt maken, selecteert u **[!UICONTROL Create schema]** in de rechterbovenhoek van het dialoogvenster **[!UICONTROL Schemas]** werkruimte. Zie de handleiding op [hoe te om een schema tot stand te brengen gebruikend de Redacteur van het Schema](../../xdm/tutorials/create-schema-ui.md#create) voor volledige instructies. U kunt ook [een schema maken met de API voor het schemaregister](../../xdm/tutorials/create-schema-api.md) indien nodig.

### Gegevensgebruikslabels toevoegen aan een schema {#add-labels-to-schema}

Nadat u een nieuw schema hebt gemaakt of een bestaand schema hebt geselecteerd in de lijst in het dialoogvenster [!UICONTROL Browse] tabblad van het dialoogvenster [!UICONTROL Schemas] in de werkruimte selecteert u een veld in uw schema in de Schema-editor. In de [!UICONTROL Field properties] zijbalk, selecteren **[!UICONTROL Apply Access and Data Governance Labels]**.

![Het tabblad Structuur van de werkruimte Schema geeft de visualisatie van uw schema weer met de gemarkeerde labels voor toegang en gegevensbeheer.](../images/labels/schema-label-governance.png)

Er wordt een dialoogvenster weergegeven waarin u labels voor gegevensgebruik op schemaniveau en veldniveau kunt toepassen en beheren. Zie de XDM-zelfstudie voor volledige instructies op [hoe u gegevensgebruikslabels voor XDM-schema&#39;s toevoegt of bewerkt](../../xdm/tutorials/labels.md#select-schema-field).

### Gegevensgebruikslabels toevoegen aan een specifieke gegevensset {#add-labels-to-dataset}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_instructions"
>title="Instructies"
>abstract="<ol><li>Selecteren <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/user-guide.html">Gegevenssets</a> in de linkernavigatie, dan selecteer de dataset waarvan gegevens u wilt beperken.</li><li>Selecteer in de weergave Gegevens van de gegevensset de <b>Gegevensbeheer</b> tab.</li><li>Selecteer de gegevenssetvelden die u wilt beperken en selecteer vervolgens <b>Regelgevingslabels bewerken</b> om de gegevens te etiketteren die op gebruiksbeperkingen worden gebaseerd.</li><li>Nadat u de gegevens van een label hebt voorzien, selecteert u <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html">Beleid</a> in de linkernavigatie selecteert u vervolgens <b>Beleid maken</b>.</li><li>Maak een <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html#create-governance-policy">Beleid inzake gegevensbeheer</a>Selecteer vervolgens de labels voor gegevensgebruik die het beleid op het beleid toepast.</li><li>Selecteer de marketingactie(s) die het beleid zal weigeren voor gegevens die deze labels bevatten. Nadat het beleid is gemaakt, selecteert u het in de lijst en schakelt u het in met de schakeloptie in het rechterspoor.</li><li>Voor elk toegelaten beleid, verhindert het Platform om het even welke gegevens die de gespecificeerde etiketten bevatten voor de bepaalde marketing actie(s) worden gebruikt. Deze handhaving vindt automatisch plaats wanneer u probeert om geëtiketteerde gegevens aan een bestemming met bijbehorende marketing acties (gebruiksgevallen) te activeren.</li></ol>"

>[!IMPORTANT]
>
>Labels kunnen niet meer worden toegepast op velden op het niveau van de gegevensset. Deze workflow is vervangen door labels op schemaniveau. Alle labels die eerder op het niveau van gegevenssetobjecten zijn toegepast, worden tot 31 mei 2024 nog steeds ondersteund via de gebruikersinterface van het Platform. Om ervoor te zorgen dat uw etiketten over alle schema&#39;s verenigbaar zijn, moeten om het even welke etiketten die eerder aan gebieden op het datasetniveau worden vastgemaakt door u over het komende jaar worden gemigreerd aan het schemaniveau. Zie de documentatie voor instructies op [hoe te om eerder toegepaste etiketten van de dataset aan het schemaniveau te migreren](../e2e.md#migrate-labels).

De etiketten kunnen op de volledige dataset van worden toegepast **[!UICONTROL Data Governance]** tabblad van het dialoogvenster **[!UICONTROL Datasets]** werkruimte. De werkruimte staat u toe om de etiketten van het gegevensgebruik op het datasetniveau te beheren.

![De [!UICONTROL Data Governance] tabblad van het dialoogvenster [!UICONTROL Datasets] werkruimte met gegevensbeheer gemarkeerd.](../images/labels/dataset-governance.png)

Als u labels voor gegevensgebruik wilt bewerken op het niveau van de gegevensset, selecteert u eerst het potloodpictogram (![Een potloodpictogram.](../images/labels/edit-icon.png)) in de rij van de naam van de gegevensset.

![De [!UICONTROL Data Governance] tabblad van het dialoogvenster [!UICONTROL Datasets] werkruimte met het pictogram Potlood bewerken gemarkeerd.](../images/labels/dataset-level-edit.png)

De **[!UICONTROL Edit Governance Labels]** wordt geopend. Controleer in het dialoogvenster de vakken naast de labels die u op de gegevensset wilt toepassen. Herinner dat deze etiketten door alle gebieden binnen de dataset zullen worden geërft. De **[!UICONTROL Applied Labels]** de koptekst wordt bijgewerkt terwijl u elk selectievakje inschakelt en de labels die u hebt gekozen, worden weergegeven. Als u de gewenste labels hebt geselecteerd, selecteert u **[!UICONTROL Save Changes]**.

![Het dialoogvenster Governance-labels bewerken met selectievakjes en gemarkeerde wijzigingen opslaan.](../images/labels/apply-labels-dataset.png)

De **[!UICONTROL Data Governance]** werkruimte wordt opnieuw weergegeven en hierin worden de labels weergegeven die u hebt toegepast op het niveau van de gegevensset in de eerste rij van de tabel. U kunt de etiketten ook zien, die door individuele kaarten worden vermeld, die neer aan elk van de gebieden binnen de dataset worden geërft.

![De [!UICONTROL Data Governance] tabblad van het dialoogvenster [!UICONTROL Datasets] werkruimte met toegepaste labels op gegevenssetniveau en geërfte labels voor gegevenssetvelden gemarkeerd.](../images/labels/applied-dataset-labels.png)

### Labels uit een gegevensset verwijderen {#remove-labels-from-a-dataset}

De etiketten die op het datasetniveau worden toegevoegd hebben &quot;x&quot;naast hun kaart. Dit staat u toe om de etiketten uit de volledige dataset te verwijderen. Overerfde labels naast elk veld hebben geen &quot;x&quot; en verschijnen &quot;grijs&quot;. Deze **overgeërfde labels zijn alleen-lezen**, wat betekent dat ze niet kunnen worden verwijderd of bewerkt op veldniveau.

<!-- ## View labels at the dataset field level {#view-labels-at-dataset-field-level} -->

<!-- To view labels inherited by the dataset from the schema level, select **[!UICONTROL Datasets]** to navigate to the datasets workspace and select the relevant dataset from the list. 

![The Browse tab of the Datasets workspace with Datasets highlighted in the left sidebar.](../images/labels/dataset-navigation.png)

Next, select the **[!UICONTROL Data Governance]** tab to show the labels that have been applied to the dataset. You can also see that the labels are inherited down to each of the fields within the dataset.

![Dataset Labels inherited by fields](../images/labels/dataset-labels-applied.png)

The inherited labels beside each field do not have an "x" next to them and appear "greyed out" with no ability to remove or edit. This is because **inherited fields are read-only**, meaning they cannot be removed at the field level. -->

<!--Beleive can cut above here  -->

De **[!UICONTROL Show Inherited Labels]** de knevel is door gebrek, dat u toestaat om het even welke etiketten te zien die neer van het schema aan zijn gebieden worden geërft. Als u de schakeloptie uitschakelt, worden alle overgeërfde labels in de gegevensset verborgen.

![Het tabblad Gegevensbeheer van de werkruimte Datasets met de schakeloptie Geërfde labels tonen gemarkeerd.](../images/labels/inherited-labels.png)

<!-- Labels applied to the dataset appear in read-only form within the **[!UICONTROL Data Governance]** view for that dataset. 

![The Data Governance tab of the Datasets workspace with labels highlighted.](../images/labels/read-only-governance-labels.png) -->

>[!NOTE]
>
>De etiketten die werden toegepast alvorens de eigenschap van de datasetetikettering werd afgekeurd kunnen uit de dataset worden verwijderd door de relevante dataset te vinden en het annuleringspictogram op het etiket te selecteren.
>![Het tabblad Gegevensbeheer van de werkruimte Datasets met een label voor de delabel gemarkeerd.](../images/labels/remove-governance-labels.png)
>Zie de documentatie voor instructies op [hoe te om eerder toegepaste etiketten van de dataset aan het schemaniveau te migreren](../e2e.md#migrate-labels).

## Aangepaste labels beheren {#manage-custom-labels}

>[!CONTEXTUALHELP]
>id="platform_governance_createlabels"
>title="Labels maken"
>abstract="Met labels kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Platform biedt een standaardset labels die u kunt gebruiken, maar u kunt ook aangepaste labels maken die specifiek zijn voor uw organisatie."

U kunt uw eigen labels voor aangepast gebruik maken in het dialoogvenster **[!UICONTROL Policies]** werkruimte in de [!DNL Experience Platform] UI. Selecteren **[!UICONTROL Policies]** in de linkernavigatie, dan selecteren **[!UICONTROL Labels]** om een lijst met bestaande labels weer te geven. Selecteer **[!UICONTROL Create label]**.

![De werkruimte Beleid waarin beleid wordt gemaakt, wordt gemarkeerd.](../images/labels/create-label-btn.png)

De **[!UICONTROL Create label]** wordt weergegeven. Geef vanaf hier de volgende informatie op voor het nieuwe label:

* **[!UICONTROL Name]**: Een unieke id voor het label. Deze waarde wordt gebruikt voor opzoekdoeleinden en moet daarom kort en beknopt zijn.
* **[!UICONTROL Friendly name]**: Een vriendelijke weergavenaam voor het label.
* **[!UICONTROL Description]**: (Optioneel) Een beschrijving van het label voor verdere context.

Als u klaar bent, selecteert u **[!UICONTROL Create]**.

![Het dialoogvenster Label maken van de werkruimte Beleid met de optie Maken gemarkeerd.](../images/labels/create-label-dialog.png)

Het dialoogvenster wordt gesloten en het nieuwe aangepaste label wordt weergegeven in de lijst onder het tabblad **[!UICONTROL Labels]** tab.

![Het tabblad Labels van de werkruimte Beleid met het nieuwe aangepaste label gemarkeerd.](../images/labels/label-created.png)

Het label kan nu onder **[!UICONTROL Custom Labels]** wanneer het uitgeven van gebruiksetiketten voor datasets en gebieden, of wanneer het creëren van het beleid van het gegevensgebruik.

![Het dialoogvenster Labels voor toegang en gegevensbeheer toepassen met de gemarkeerde aangepaste labels.](../images/labels/add-custom-label.png)

## Volgende stappen

Nu u de etiketten van het gegevensgebruik op de dataset en het gebiedsniveau hebt toegevoegd, kunt u beginnen gegevens in te nemen [!DNL Experience Platform]. Als u meer wilt weten, begint u met het lezen van de [documentatie over gegevensinvoer](../../ingestion/home.md).

U kunt nu ook beleid voor gegevensgebruik definiëren op basis van de labels die u hebt toegepast. Zie voor meer informatie de [overzicht van beleidsregels voor gegevensgebruik](../policies/overview.md).

<!-- The workflow of this video is now outdated. This can be enabled once the video has been updated

## Additional resources

The following video is intended to support your understanding of Data Governance, and outlines how to apply labels to a dataset and individual fields.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on) -->
