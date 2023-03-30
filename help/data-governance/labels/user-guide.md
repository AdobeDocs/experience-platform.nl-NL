---
keywords: Experience Platform;home;populaire onderwerpen;gegevensbeheer;label voor gegevensgebruik;beleidsservice;gebruikershandleiding voor labels voor gegevensgebruik
solution: Experience Platform
title: Labels voor gegevensgebruik beheren in de gebruikersinterface
description: In deze handleiding vindt u de stappen voor het werken met labels voor gegevensgebruik in de Adobe Experience Platform-gebruikersinterface.
exl-id: aa44d5cc-416a-4ef2-be14-b4f32aec162c
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 0%

---

# Labels voor gegevensgebruik beheren in de gebruikersinterface {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_description"
>title="Gegevensgebruik in Platform beheren"
>abstract="<h2>Beschrijving</h2><p>Met het gegevensbeheerkader in Experience Platform kunt u kenmerken en gegevenssets labelen op basis van beperkingen voor gegevensgebruik en beleidsregels instellen die deze beperkingen voor specifieke marketingacties identificeren en naleven.</p>"

In deze gebruikershandleiding worden de stappen beschreven voor het werken met labels voor gegevensgebruik in de [!DNL Experience Platform] gebruikersinterface.

## Labels beheren op het niveau van de gegevensset

>[!IMPORTANT]
>
>Het toepassen van labels op gegevenssetniveau wordt alleen ondersteund voor gevallen waarin gegevens worden beheerd. Als u probeert toegangsbeleid voor de gegevens tot stand te brengen, moet u [labels toepassen op het schema](../../xdm/tutorials/labels.md) dat de gegevensset op die gegevens is gebaseerd. Zie het overzicht op [attribuut-based toegangsbeheer](../../access-control/abac/overview.md) voor meer informatie .

Om de etiketten van het gegevensgebruik op het datasetniveau te beheren, moet u een bestaande dataset selecteren of nieuwe creëren. Nadat u zich hebt aangemeld bij Adobe Experience Platform, selecteert u **[!UICONTROL Datasets]** op de linkernavigatie om de **[!UICONTROL Datasets]** werkruimte. Deze pagina maakt een lijst van alle gecreeerde datasets die tot uw organisatie behoren, samen met nuttige details met betrekking tot elke dataset.

![Tabblad Gegevensset in werkruimte Gegevens](../images/labels/datasets-tab.png)

De volgende sectie verstrekt stappen voor het creëren van een nieuwe dataset om etiketten op toe te passen. Als u labels voor een bestaande gegevensset wilt bewerken, selecteert u de gegevensset in de lijst en gaat u verder met [gegevensgebruikslabels toevoegen aan de gegevensset](#add-labels).

### Een nieuwe gegevensset maken

>[!NOTE]
>
>In dit voorbeeld, wordt een dataset gecreeerd gebruikend pre-gevormde [!DNL Experience Data Model] (XDM) schema. Voor meer informatie over XDM- schema&#39;s, zie [XDM System, overzicht](../../xdm/home.md) en [grondbeginselen van de schemacompositie](../../xdm/schema/composition.md).

Als u een nieuwe gegevensset wilt maken, selecteert u **[!UICONTROL Create Dataset]** in de rechterbovenhoek van het dialoogvenster **[!UICONTROL Datasets]** werkruimte.

![](../images/labels/create-dataset.png)

De **[!UICONTROL Create Dataset]** wordt weergegeven. Selecteer **[!UICONTROL Create Dataset from Schema]**.

![Dataset maken van schema](../images/labels/create-from-dataset.png)

De **[!UICONTROL Select Schema]** het scherm verschijnt, dat van alle beschikbare schema&#39;s een lijst maakt die u voor het creëren van een dataset kunt gebruiken. Selecteer het keuzerondje naast een schema om het te selecteren. De **[!UICONTROL Schemas]** aan de rechterkant worden aanvullende details over het geselecteerde schema weergegeven. Als u een schema hebt geselecteerd, selecteert u **[!UICONTROL Next]**.

![Datasetschema selecteren](../images/labels/select-schema.png)

De **[!UICONTROL Configure Dataset]** wordt weergegeven. Geef een naam (vereist) en beschrijving (optioneel, maar aanbevolen) op voor de nieuwe gegevensset en selecteer vervolgens **[!UICONTROL Finish]**.

![Gegevensset configureren met naam en beschrijving](../images/labels/configure-dataset.png)

De **[!UICONTROL Dataset Activity]** pagina verschijnt, tonend informatie over de pas gecreëerde dataset. In dit voorbeeld krijgt de dataset de naam &quot;Leden van de Waardigheid&quot;, daarom toont de top-navigation **Datasets > Loyalty-leden**.

![Pagina Gegevensactiviteit](../images/labels/dataset-created.png)

### Gegevensgebruikslabels toevoegen aan de gegevensset {#add-labels}

Nadat u een nieuwe gegevensset hebt gemaakt of een bestaande gegevensset hebt geselecteerd in de lijst in het dialoogvenster **[!UICONTROL Datasets]** werkruimte, selecteert u **[!UICONTROL Data Governance]** om de **[!UICONTROL Data Governance]** werkruimte. De werkruimte staat u toe om de etiketten van het gegevensgebruik op het datasetniveau en gebiedsniveau te beheren.

![Tabblad Gegevensbeheer gegevensset](../images/labels/dataset-governance.png)

Om de etiketten van het gegevensgebruik op het datasetniveau uit te geven, begin door het potloodpictogram naast de naam van de dataset te selecteren.

![Labels op gegevensniveau bewerken](../images/labels/dataset-level-edit.png)

De **[!UICONTROL Edit Governance Labels]** wordt geopend. Controleer in het dialoogvenster de vakken naast de labels die u op de gegevensset wilt toepassen. Herinner dat deze etiketten door alle gebieden binnen de dataset zullen worden geërft. De **[!UICONTROL Applied Labels]** de koptekst wordt bijgewerkt terwijl u elk selectievakje inschakelt en de labels die u hebt gekozen, worden weergegeven. Als u de gewenste labels hebt geselecteerd, selecteert u **[!UICONTROL Save Changes]**.

![Regelgevingslabels toepassen op datumniveau](../images/labels/apply-labels-dataset.png)

De **[!UICONTROL Data Governance]** werkruimte opnieuw wordt weergegeven, met de labels die u op datasetniveau hebt toegepast. U kunt ook zien dat de labels onderaan elk van de velden in de gegevensset worden overgeërfd.

![Labels voor gegevenssets die zijn overgeërfd door velden](../images/labels/dataset-labels-applied.png)

U ziet dat een &quot;x&quot; wordt weergegeven naast de labels op datasetniveau, zodat u de labels kunt verwijderen. De overgeërfde labels naast elk veld hebben geen &#39;x&#39; en worden &#39;grijs weergegeven&#39; zonder mogelijkheid om te verwijderen of te bewerken. Dit komt omdat **overgeërfde velden zijn alleen-lezen**, wat betekent dat ze niet op veldniveau kunnen worden verwijderd.

De **[!UICONTROL Show Inherited Labels]** de knevel is door gebrek, dat u toestaat om het even welke etiketten te zien die neer van de dataset aan zijn gebieden worden geërft. Als u de schakeloptie uitschakelt, worden alle overgeërfde labels in de gegevensset verborgen.

![Overerfde labels verbergen](../images/labels/inherited-labels.png)

## Labels beheren op het niveau van het gegevenssetveld {#manage-labels-at-dataset-field-level}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_instructions"
>title="Instructies"
>abstract="<ul><li>Selecteren <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/user-guide.html">Gegevenssets</a> in de linkernavigatie, dan selecteer de dataset waarvan gegevens u wilt beperken.</li><li>Selecteer in de weergave Gegevens van de gegevensset de <b>Gegevensbeheer</b> tab.</li><li>Selecteer de gegevenssetvelden die u wilt beperken en selecteer vervolgens <b>Regelgevingslabels bewerken</b> om de gegevens te etiketteren die op gebruiksbeperkingen worden gebaseerd.</li><li>Nadat u de gegevens van een label hebt voorzien, selecteert u <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html">Beleid</a> in de linkernavigatie selecteert u vervolgens <b>Beleid maken</b>.</li><li>Maak een <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html#create-governance-policy">Beleid inzake gegevensbeheer</a>Selecteer vervolgens de labels voor gegevensgebruik die het beleid op het beleid toepast.</li><li>Selecteer de marketingactie(s) die het beleid zal weigeren voor gegevens die deze labels bevatten. Nadat het beleid is gemaakt, selecteert u het in de lijst en schakelt u het in met de schakeloptie in het rechterspoor.</li><li>Voor elk toegelaten beleid, verhindert het Platform om het even welke gegevens die de gespecificeerde etiketten bevatten voor de bepaalde marketing actie(s) worden gebruikt. Deze handhaving vindt automatisch plaats wanneer u probeert om geëtiketteerde gegevens aan een bestemming met bijbehorende marketing acties (gebruiksgevallen) te activeren.</li></ul>"

>[!IMPORTANT]
>
>Het toepassen van labels op gegevenssetveldniveau wordt alleen ondersteund voor gevallen waarin gebruik wordt gemaakt van gegevensbeheer. Als u probeert toegangsbeleid voor de gegevens tot stand te brengen, moet u [labels toepassen op het schema](../../xdm/tutorials/labels.md) dat de gegevensset op die gegevens is gebaseerd. Zie het overzicht op [attribuut-based toegangsbeheer](../../access-control/abac/overview.md) voor meer informatie .

Doorgaan met de workflow voor [gegevensgebruikslabels toevoegen en bewerken op gegevenssetniveau](#add-labels)kunt u ook labels op veldniveau beheren in het dialoogvenster **[!UICONTROL Data Governance]** werkruimte voor die dataset.

Als u gegevensgebruikslabels op een afzonderlijk veld wilt toepassen, schakelt u het selectievakje naast de veldnaam in en selecteert u vervolgens **[!UICONTROL Edit Governance Labels]**.

![Veldlabels bewerken](../images/labels/field-label-edit.png)

De **[!UICONTROL Edit Governance Labels]** wordt weergegeven. In het dialoogvenster worden kopteksten weergegeven met de geselecteerde velden, toegepaste labels en overgeërfde labels. De overgeërfde labels (C2 en C5) worden grijs weergegeven in het dialoogvenster. Zij zijn read-only etiketten die van het datasetniveau worden geërft en zijn daarom slechts editable op het datasetniveau.

![Regellabels bewerken voor een afzonderlijk veld](../images/labels/field-label-inheritance.png)

Selecteer labels op veldniveau door het selectievakje naast elk label dat u wilt gebruiken in te schakelen. Terwijl u labels selecteert, worden de **[!UICONTROL Applied Labels]** koptekst wordt bijgewerkt met labels die zijn toegepast op de velden die worden weergegeven in het dialoogvenster **[!UICONTROL Selected Fields]** header. Als u klaar bent met het selecteren van labels op veldniveau, selecteert u **[!UICONTROL Save Changes]**.

![Labels op veldniveau toepassen](../images/labels/apply-labels-field.png)

De **[!UICONTROL Data Governance]** wordt de werkruimte opnieuw weergegeven. De geselecteerde labels op veldniveau worden nu in de rij naast de veldnaam weergegeven. Het label op veldniveau heeft een &#39;x&#39; naast het label, zodat u het label kunt verwijderen.

![Veld dat labels op veldniveau weergeeft](../images/labels/field-labels-applied.png)

U kunt deze stappen herhalen om door te gaan met het toevoegen en bewerken van labels op veldniveau voor extra velden, waaronder het selecteren van meerdere velden om labels op veldniveau tegelijk toe te passen.

![Selecteer meerdere velden om labels op veldniveau tegelijk toe te passen.](../images/labels/multiple-fields.png)

Het is belangrijk om te herinneren dat de overerving zich van top-level slechts (dataset → gebieden) beweegt, betekenend dat de etiketten die op het gebiedsniveau worden toegepast niet aan andere gebieden of datasets worden verspreid.

## Labels op schemaniveau beheren

U kunt labels rechtstreeks toevoegen aan een schema of aan velden binnen dat schema. Om het even welke gebieden die op het schemaniveau worden toegepast zullen aan alle datasets verspreiden die op dat schema worden gebaseerd.

Zie de zelfstudie aan [beheren, labels op schemaniveau](../../xdm/tutorials/labels.md) voor meer informatie .

## Aangepaste labels beheren {#manage-custom-labels}

>[!CONTEXTUALHELP]
>id="platform_governance_createlabels"
>title="Labels maken"
>abstract="Met labels kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Platform biedt een standaardset labels die u kunt gebruiken, maar u kunt ook aangepaste labels maken die specifiek zijn voor uw organisatie."

U kunt uw eigen labels voor aangepast gebruik maken in het dialoogvenster **[!UICONTROL Policies]** werkruimte in de [!DNL Experience Platform] UI. Selecteren **[!UICONTROL Policies]** in de linkernavigatie, dan selecteren **[!UICONTROL Labels]** om een lijst met bestaande labels weer te geven. Selecteer **[!UICONTROL Create label]**.

![](../images/labels/create-label-btn.png)

De **[!UICONTROL Create label]** wordt weergegeven. Geef vanaf hier de volgende informatie op voor het nieuwe label:

* **[!UICONTROL Identifier]**: Een unieke id voor het label. Deze waarde wordt gebruikt voor opzoekdoeleinden en moet daarom kort en beknopt zijn.
* **[!UICONTROL Name]**: Een vriendelijke weergavenaam voor het label.
* **[!UICONTROL Description]**: (Optioneel) Een beschrijving van het label voor verdere context.

Als u klaar bent, selecteert u **[!UICONTROL Create]**.

![](../images/labels/create-label.png)

Het dialoogvenster wordt gesloten en het nieuwe aangepaste label wordt weergegeven in de lijst onder het tabblad **[!UICONTROL Labels]** tab.

![](../images/labels/label-created.png)

Het label kan nu onder **[!UICONTROL Custom Labels]** wanneer het uitgeven van gebruiksetiketten voor datasets en gebieden, of wanneer het creëren van het beleid van het gegevensgebruik.

<img src="../images/labels/add-custom-label.png" width="600" /><br>

## Volgende stappen

Nu u de etiketten van het gegevensgebruik op de dataset en het gebiedsniveau hebt toegevoegd, kunt u beginnen gegevens in te nemen [!DNL Experience Platform]. Als u meer wilt weten, begint u met het lezen van de [documentatie over gegevensinvoer](../../ingestion/home.md).

U kunt nu ook beleid voor gegevensgebruik definiëren op basis van de labels die u hebt toegepast. Zie voor meer informatie de [overzicht van beleidsregels voor gegevensgebruik](../policies/overview.md).

## Aanvullende bronnen

De volgende video is bedoeld om uw begrip van het Beleid van Gegevens te steunen, en schetst hoe te om etiketten op een dataset en individuele gebieden toe te passen.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
