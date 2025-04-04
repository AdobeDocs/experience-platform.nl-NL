---
title: Labels voor gegevensgebruik voor een schema beheren
description: Leer hoe u labels voor gegevensgebruik toevoegt aan XDM-schemavelden (Experience Data Model) in de gebruikersinterface van Adobe Experience Platform.
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# De labels voor gegevensgebruik voor een schema beheren

Alle gegevens die in Adobe Experience Platform worden gebracht worden beperkt door schema&#39;s van de Gegevens van de Ervaring van het Model (XDM). Deze gegevens zijn mogelijk onderworpen aan gebruiksbeperkingen die zijn gedefinieerd door uw organisatie of wettelijke voorschriften. Om van dit rekenschap te geven, staat Experience Platform u toe om het gebruik van bepaalde datasets en gebieden door het gebruik van [ etiketten van het gegevensgebruik ](../../data-governance/labels/overview.md) te beperken.

Een label dat wordt toegepast op een schemaveld, geeft het gebruiksbeleid aan dat van toepassing is op de gegevens in dat specifieke veld.

De etiketten kunnen op individuele schema&#39;s, en gebieden binnen die schema&#39;s worden toegepast. Wanneer de etiketten rechtstreeks op een schema worden toegepast, worden die etiketten verspreid aan alle bestaande en toekomstige datasets die op dat schema gebaseerd zijn.

Bovendien verspreidt om het even welk gebiedsetiket dat u in één schema toevoegt aan alle andere schema&#39;s die het zelfde gebied van een gedeelde klasse of een gebiedsgroep in dienst nemen. Zo zorgt u ervoor dat de gebruiksregels voor vergelijkbare velden consistent zijn in het gehele gegevensmodel.

Deze zelfstudie behandelt de stappen voor het toevoegen van labels aan een schema met behulp van de Schema-editor in de gebruikersinterface van Experience Platform.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt.
   * [ Redacteur van het Schema ](../ui/overview.md): Leer hoe te om schema&#39;s en andere middelen in Experience Platform UI tot stand te brengen en te beheren.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): biedt de infrastructuur voor het afdwingen van beperkingen voor gegevensgebruik voor Experience Platform-bewerkingen, waarbij beleidsregels worden gebruikt die definiëren welke marketingacties op gelabelde gegevens kunnen (of kunnen) worden uitgevoerd.

## Selecteer een schema of veld waaraan u labels wilt toevoegen {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="Regelgevingslabels bewerken"
>abstract="Pas een label toe op een schemaveld om het gebruiksbeleid aan te geven dat van toepassing is op de gegevens in dat specifieke veld."

Begin labels toe te voegen, moet u eerst [ een bestaand schema selecteren om uit te geven ](../ui/resources/schemas.md#edit) of [ een nieuw schema ](../ui/resources/schemas.md#create) creëren om zijn structuur in de Redacteur van het Schema te bekijken.

Als u de labels voor een afzonderlijk veld wilt bewerken, selecteert u het veld op het canvas en selecteert u vervolgens **[!UICONTROL Manage access]** in de rechtertrack.

>[!IMPORTANT]
>
>U kunt maximaal 300 labels toepassen op elk schema.

![ selecteer een gebied van het canvas van de Redacteur van het Schema ](../images/tutorials/labels/manage-access.png)

U kunt ook de tab **[!UICONTROL Labels]** selecteren, het gewenste veld in de lijst kiezen en **[!UICONTROL Apply Access and Data Governance Labels]** in de rechtertrack selecteren.

![ selecteer een gebied van het [!UICONTROL Labels] lusje ](../images/tutorials/labels/select-field-on-labels-tab.png)

Als u de labels voor het volledige schema wilt bewerken, schakelt u op het tabblad **[!UICONTROL Labels]** het selectievakje onder het filterpictogram in. Hiermee selecteert u elk beschikbaar veld in het schema. Selecteer vervolgens **[!UICONTROL Apply Access and Data Governance Labels]** in de rechtertrack.

![ selecteer de schemanaam van het [!UICONTROL Labels] lusje ](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>Een ontkenningsbericht verschijnt wanneer u eerst probeert om de etiketten voor een schema of een gebied uit te geven, verklarend hoe het etiketgebruik stroomafwaartse verrichtingen afhankelijk van het beleid van uw organisatie beïnvloedt. Selecteer **[!UICONTROL Proceed]** als u wilt doorgaan met bewerken.
>
>![ het gebruiksdisclaimer van het Etiket ](../images/tutorials/labels/disclaimer.png)

## De labels voor het schema of veld bewerken {#edit-labels}

Er wordt een dialoogvenster weergegeven waarin u de labels voor het geselecteerde veld kunt bewerken. Als u een afzonderlijk objecttype-veld hebt geselecteerd, worden in de rechterrail de subvelden weergegeven waarnaar de toegepaste labels zullen doorgeven.

![ toepassen de dialoog van de Etiketten van de Toegang en van het Beheer van Gegevens met de geselecteerde benadrukte gebieden.](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>Als u velden bewerkt voor het hele schema, worden de toepasselijke velden niet in de rechtertrack vermeld en wordt in plaats daarvan de schemanaam weergegeven.

Gebruik de weergegeven lijst om de labels te selecteren die u aan het schema of veld wilt toevoegen. Wanneer labels worden gekozen, wordt de sectie **[!UICONTROL Applied labels]** bijgewerkt en worden de labels weergegeven die tot nu toe zijn geselecteerd.

![ toepassen de dialoog van de Etiketten van de Toegang en van het Beheer van Gegevens met de toegepaste benadrukte etiketten.](../images/tutorials/labels/applied-labels.png)

Als u de weergegeven labels op type wilt filteren, selecteert u de gewenste categorie in de linkertrack. Als u een nieuw aangepast label wilt maken, selecteert u **[!UICONTROL Create label]** .

![ toepassen de dialoog van de Etiketten van de Toegang en van het Beleid van Gegevens met een toegepast filter van het etikettype en leidt etiket benadrukt.](../images/tutorials/labels/filter-and-create-custom.png)

Als u tevreden bent met de gekozen labels, selecteert u **[!UICONTROL Save]** om deze toe te passen op het veld of schema.

![ toepassen toegang en de dialoog van de Etiketten van het Beheer van Gegevens met sparen benadrukt.](../images/tutorials/labels/save-labels.png)

Het tabblad **[!UICONTROL Labels]** wordt weer weergegeven, met daarin de toegepaste labels voor het schema.

![ het lusje van Etiketten van de schemawerkruimte met de toegepaste benadrukte gebiedslabels.](../images/tutorials/labels/field-labels-added.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe u labels voor gegevensgebruik voor schema&#39;s en velden kunt beheren. Voor informatie bij het beheren van de etiketten van het gegevensgebruik, met inbegrip van hoe te om hen aan specifieke datasets eerder dan op het schemaniveau toe te voegen, zie de [ gids UI van de etiketten van het gegevensgebruik ](../../data-governance/labels/user-guide.md).
