---
title: Labels voor gegevensgebruik voor een schema beheren
description: Leer hoe u labels voor gegevensgebruik toevoegt aan XDM-schemavelden (Experience Data Model) in de gebruikersinterface van Adobe Experience Platform.
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: c35c270afca57cb96228cea29fd5a39ec6615332
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# De labels voor gegevensgebruik voor een schema beheren

>[!IMPORTANT]
>
>Etikettering op basis van schema maakt deel uit van [attribuut-based toegangsbeheer](../../access-control/abac/overview.md), die momenteel in een beperkte versie beschikbaar is voor in de VS gevestigde zorgklanten. Deze mogelijkheid is beschikbaar voor alle Adobe Real-time Customer Data Platform-klanten zodra deze volledig is vrijgegeven.

Alle gegevens die in Adobe Experience Platform worden gebracht worden beperkt door schema&#39;s van de Gegevens van de Ervaring van het Model (XDM). Deze gegevens zijn mogelijk onderworpen aan gebruiksbeperkingen die zijn gedefinieerd door uw organisatie of wettelijke voorschriften. Om dit te verklaren, staat het Platform u toe om het gebruik van bepaalde datasets en gebieden door het gebruik van te beperken [gegevensgebruikslabels](../../data-governance/labels/overview.md).

Een label dat wordt toegepast op een schemaveld, geeft het gebruiksbeleid aan dat van toepassing is op de gegevens in dat specifieke veld.

Labels kunnen worden toegepast op afzonderlijke schema&#39;s en op velden binnen die schema&#39;s. Wanneer de etiketten rechtstreeks op een schema worden toegepast, worden die etiketten verspreid aan alle bestaande en toekomstige datasets die op dat schema gebaseerd zijn.

Bovendien verspreidt om het even welk gebiedsetiket dat u in één schema toevoegt aan alle andere schema&#39;s die het zelfde gebied van een gedeelde klasse of een gebiedsgroep in dienst nemen. Zo zorgt u ervoor dat de gebruiksregels voor vergelijkbare velden consistent zijn in het gehele gegevensmodel.

Deze zelfstudie behandelt de stappen voor het toevoegen van labels aan een schema met behulp van de Schema-editor in de interface van het platform.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Het gestandaardiseerde kader waarbinnen [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Schema-editor](../ui/overview.md): Leer om schema&#39;s en andere middelen in Platform UI tot stand te brengen en te beheren.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Biedt de infrastructuur voor het afdwingen van beperkingen voor gegevensgebruik op platformbewerkingen, met behulp van beleid dat definieert welke marketingacties op gelabelde gegevens kunnen (of kunnen) worden uitgevoerd.

## Selecteer een schema of veld waaraan u labels wilt toevoegen {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="Regelgevingslabels bewerken"
>abstract="Pas een label toe op een schemaveld om het gebruiksbeleid aan te geven dat van toepassing is op de gegevens in dat specifieke veld."

Als u wilt beginnen met het toevoegen van labels, moet u eerst [een bestaand schema selecteren om te bewerken](../ui/resources/schemas.md#edit) of [een nieuw schema maken](../ui/resources/schemas.md#create) om de structuur ervan weer te geven in de Schema-editor.

Als u de labels voor een afzonderlijk veld wilt bewerken, selecteert u het veld op het canvas en selecteert u vervolgens **[!UICONTROL Manage access]** in het rechterspoor.

![Een veld selecteren in het canvas van de Schema-editor](../images/tutorials/labels/manage-access.png)

U kunt ook de optie **[!UICONTROL Labels]** kiest u het gewenste veld in de lijst en selecteert u **[!UICONTROL Apply Access and Data Governance Labels]** in het rechterspoor.

![Selecteer een veld in het menu [!UICONTROL Labels] tab](../images/tutorials/labels/select-field-on-labels-tab.png)

Als u de labels voor het volledige schema wilt bewerken, gaat u in het dialoogvenster **[!UICONTROL Labels]** selecteert u het selectievakje onder het filterpictogram. Hiermee selecteert u elk beschikbaar veld in het schema. Selecteer vervolgens **[!UICONTROL Apply Access and Data Governance Labels]** in het rechterspoor.

![Selecteer de naam van het schema in het menu [!UICONTROL Labels] tab](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>Een ontkenningsbericht verschijnt wanneer u eerst probeert om de etiketten voor een schema of een gebied uit te geven, verklarend hoe het etiketgebruik stroomafwaartse verrichtingen afhankelijk van het beleid van uw organisatie beïnvloedt. Selecteren **[!UICONTROL Proceed]** om verder te gaan met bewerken.
>
>![Label-gebruiksdisclaimer](../images/tutorials/labels/disclaimer.png)

## De labels voor het schema of veld bewerken {#edit-labels}

Er wordt een dialoogvenster weergegeven waarin u de labels voor het geselecteerde veld kunt bewerken. Als u een afzonderlijk objecttype-veld hebt geselecteerd, worden in de rechterrail de subvelden weergegeven waarnaar de toegepaste labels zullen doorgeven.

![Het dialoogvenster Labels voor toegang en gegevensbeheer toepassen met de geselecteerde velden gemarkeerd.](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>Als u velden bewerkt voor het hele schema, worden de toepasselijke velden niet in de rechtertrack vermeld en wordt in plaats daarvan de schemanaam weergegeven.

Gebruik de weergegeven lijst om de labels te selecteren die u aan het schema of veld wilt toevoegen. Als labels worden gekozen, wordt de **[!UICONTROL Applied labels]** -sectie wordt bijgewerkt om de labels weer te geven die tot nu toe zijn geselecteerd.

![Het dialoogvenster Labels voor toegang en gegevensbeheer toepassen met de toegepaste labels gemarkeerd.](../images/tutorials/labels/applied-labels.png)

Als u de weergegeven labels op type wilt filteren, selecteert u de gewenste categorie in de linkertrack. Als u een nieuw aangepast label wilt maken, selecteert u **[!UICONTROL Create label]**.

![Het dialoogvenster Labels voor toegang en gegevensbeheer toepassen waarop een filter voor labeltype is toegepast en het label Maken is gemarkeerd.](../images/tutorials/labels/filter-and-create-custom.png)

Als u tevreden bent met de gekozen labels, selecteert u **[!UICONTROL Save]** om deze toe te passen op het veld of schema.

![Het dialoogvenster Labels voor toegang en gegevensbeheer toepassen met Opslaan gemarkeerd.](../images/tutorials/labels/save-labels.png)

De **[!UICONTROL Labels]** opnieuw wordt weergegeven, met de toegepaste labels voor het schema.

![Het tabblad Labels van de werkruimte Schema&#39;s met de toegepaste veldlabels gemarkeerd.](../images/tutorials/labels/field-labels-added.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe u labels voor gegevensgebruik voor schema&#39;s en velden kunt beheren. Voor informatie over het beheren van de etiketten van het gegevensgebruik, met inbegrip van hoe te om hen aan specifieke datasets eerder dan op het schemaniveau toe te voegen, zie [UI-handleiding voor gegevensgebruikslabels](../../data-governance/labels/user-guide.md).
