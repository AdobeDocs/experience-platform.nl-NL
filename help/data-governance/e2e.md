---
title: End-to-end handleiding voor gegevensbeheer
description: Volg het volledige proces voor het afdwingen van beperkingen van het gegevensgebruik voor gebieden en datasets in Adobe Experience Platform.
exl-id: f18ae032-027a-4c97-868b-e04753237c81
source-git-commit: 9f3fa696ed60ce85fa93515e39716d89ec80f1ec
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 0%

---

# End-to-end handleiding voor gegevensbeheer

Als u wilt bepalen welke marketingacties op bepaalde gegevenssets en velden in Adobe Experience Platform kunnen worden uitgevoerd, moet u het volgende instellen:

1. [Labels toepassen](#labels) aan de schemagebieden of volledige datasets, het waarvan gebruik wilt beperken u.
1. [Beleid voor gegevensbeheer configureren en inschakelen](#policy) die bepalen welke soorten geëtiketteerde gegevens voor bepaalde marketing acties kunnen worden gebruikt.
1. [Marketing-acties toepassen op uw doelen](#destinations) om aan te geven welk beleid van toepassing is op gegevens die naar die bestemmingen worden verzonden.

Als u klaar bent met het configureren van uw labels, beheerbeleid en marketingacties, kunt u [uw beleidshandhaving testen](#test) ervoor te zorgen dat het naar behoren functioneert.

Deze gids doorloopt het volledige proces om een beleid van het gegevensbeheer in het Platform UI te vormen en af te dwingen. Voor meer gedetailleerde informatie over de eigenschappen die in deze gids worden gebruikt, verwijs naar de overzichtsdocumentatie over de volgende onderwerpen:

* [Adobe Experience Platform Data Governance](./home.md)
* [Labels voor gegevensgebruik](./labels/overview.md)
* [Beleid voor gegevensgebruik](./policies/overview.md)
* [Beleidshandhaving](./enforcement/overview.md)

>[!NOTE]
>
>Deze gids concentreert zich op hoe te opstelling en beleid te handhaven voor hoe de gegevens in Experience Platform worden gebruikt of worden geactiveerd. Als u probeert te beperken **toegang** aan de gegevens zelf voor bepaalde gebruikers van het Platform binnen uw organisatie, zie de gids van begin tot eind op [attribuut-based toegangsbeheer](../access-control/abac/end-to-end-guide.md) in plaats daarvan. Op attributen-gebaseerde toegangscontrole gebruikt ook etiketten en beleid, maar voor een verschillend gebruiksgeval dan gegevensbeheer.

## Labels toepassen {#labels}

>[!IMPORTANT]
>
>Labels kunnen niet langer op afzonderlijke velden op het niveau van de gegevensset worden toegepast. Deze workflow is vervangen door labels op schemaniveau. Nochtans, kunt u nog een volledige dataset etiketteren. Alle labels die eerder op afzonderlijke gegevenssetvelden zijn toegepast, worden tot 31 mei 2024 nog steeds ondersteund via de interface van het platform. Om ervoor te zorgen dat uw etiketten over alle schema&#39;s verenigbaar zijn, moeten om het even welke etiketten die eerder aan gebieden op het datasetniveau worden vastgemaakt door u over het komende jaar worden gemigreerd aan het schemaniveau. Zie de sectie over [eerder toegepaste labels migreren](#migrate-labels) voor instructies over hoe te om dit te doen.

U kunt [labels toepassen op een schema](#schema-labels) zodat alle datasets die op dat schema worden gebaseerd de zelfde etiketten erven. Hierdoor kunt u de labels voor gegevensbeheer, toestemming en toegangsbeheer op één locatie beheren. Door beperkingen van het gegevensgebruik op het schemaniveau af te dwingen, verspreidt het effect zich stroomafwaarts aan alle datasets die op dat schema gebaseerd zijn. De etiketten die op het niveau van de schemagebied worden toegepast steunen het gebruikscituaties van het Beleid van Gegevens en zijn ontdekt in de werkruimte Datasets [!UICONTROL Data Governance] onder de [!UICONTROL Field Name] kolom als alleen-lezen labels.

Als er een specifieke dataset is die u beperkingen van het gegevensgebruik wilt afdwingen, kunt u [labels rechtstreeks toepassen op die gegevensset](#dataset-labels) of specifieke velden binnen die gegevensset.

U kunt ook [labels toepassen op een schema](#schema-labels) zodat alle datasets die op dat schema worden gebaseerd de zelfde etiketten erven.

>[!NOTE]
>
>Raadpleeg voor meer informatie over de verschillende labels voor gegevensgebruik en het beoogde gebruik de [gegevensgebruikslabels, verwijzing](./labels/reference.md). Als de beschikbare kernlabels niet op alle gewenste gebruiksgevallen betrekking hebben, kunt u [uw eigen aangepaste labels definiëren](./labels/user-guide.md#manage-custom-labels) ook.

### Labels toepassen op een volledige gegevensset {#dataset-labels}

Selecteren **[!UICONTROL Datasets]** in de linkernavigatie, dan selecteer de naam van de dataset u etiketten op wilt toepassen. U kunt optioneel het onderzoeksgebied gebruiken om onderaan de lijst van getoonde datasets te versmallen.

![De werkruimte van Datasets doorbladert lusje met Datasets en een benadrukte datasetrij.](./images/e2e/select-dataset.png)

De detailweergave voor de gegevensset wordt weergegeven. Selecteer de **[!UICONTROL Data governance]** om een lijst van de gebieden van de dataset en om het even welke etiketten te bekijken die reeds op hen zijn toegepast. Selecteer het potloodpictogram om de labels van gegevenssets te bewerken.

![Het tabblad Gegevensbeheer voor de gegevensset Loyalty-leden met het potloodpictogram gemarkeerd.](./images/e2e/edit-dataset-labels.png)

De [!UICONTROL Edit governance labels] wordt weergegeven. Selecteer het juiste governancelabel en selecteer **[!UICONTROL Save]**.

![Het dialoogvenster Beheerslabels bewerken met het selectievakje Label en de optie Opslaan gemarkeerd.](./images/e2e/edit-dataset-governance-labels.png)

### Labels toepassen op een schema {#schema-labels}

Selecteren **[!UICONTROL Schemas]** in de linkernavigatie, dan selecteer het schema dat u etiketten aan van de lijst wilt toevoegen.

>[!TIP]
>
>Als u niet zeker bent welk schema op een bepaalde dataset van toepassing is, selecteer **[!UICONTROL Datasets]** in de linkernavigatie, dan selecteer de verbinding onder **[!UICONTROL Schema]** kolom voor de gewenste dataset. Selecteer de schemanaam in popover die lijkt om het schema in de Redacteur van het Schema te openen.
>
>![Beeld dat een verbinding aan het schema van een dataset toont](./images/e2e/schema-from-dataset.png)

De structuur van het schema wordt weergegeven in de Schema-editor. Selecteer van hieruit de **[!UICONTROL Labels]** om een lijstmening van de gebieden van het schema en de etiketten te tonen die reeds op hen zijn toegepast. Schakel de selectievakjes in naast de velden waaraan u labels wilt toevoegen en selecteer vervolgens **[!UICONTROL Apply access and data governance labels]** in het rechterspoor.

![Het tabblad Labels van de werkruimte Schema met één schemaveld geselecteerd en de labels voor toegang en gegevensbeheer toegepast gemarkeerd.](./images/e2e/schema-field-label.png)

>[!NOTE]
>
>Als u labels wilt toevoegen aan alle velden in het schema, selecteert u het potloodpictogram op de bovenste rij.
>
>![Afbeelding waarin het potloodpictogram wordt weergegeven dat in de weergave Schema-labels wordt geselecteerd](./images/e2e/label-whole-schema.png)

De [!UICONTROL Apply access and data governance labels] wordt weergegeven. Selecteer de labels die u wilt toepassen op het gekozen schemaveld. Selecteer **[!UICONTROL Save]**.

![Het dialoogvenster Toegangs- en gegevensbeheerlabels toepassen waarin meerdere labels worden weergegeven die aan een schemaveld worden toegevoegd.](./images/e2e/save-schema-labels.png)

Ga als volgt te werk om labels toe te passen op verschillende velden (of verschillende schema&#39;s). Als u klaar bent, kunt u doorgaan naar de volgende stap van [beleid inzake gegevensbeheer inschakelen](#policy).

### Labels migreren die eerder zijn toegepast op het niveau van de gegevensset {#migrate-labels}

Selecteren **[!UICONTROL Dataset]** in de linkernavigatie, dan selecteer de naam van de dataset u etiketten van wilt migreren. U kunt optioneel het onderzoeksgebied gebruiken om onderaan de lijst van getoonde datasets te versmallen.

![Het tabblad Bladeren van de werkruimte Datasets met de Dataset Loyalty-leden gemarkeerd.](./images/e2e/select-dataset.png)

De detailweergave voor de gegevensset wordt weergegeven. Selecteer de **[!UICONTROL Data governance]** om een lijst van de gebieden van de dataset en om het even welke etiketten te bekijken die reeds op hen zijn toegepast. Selecteer het pictogram Annuleren naast een label dat u uit een veld wilt verwijderen. Er verschijnt een bevestigingsvenster. Selecteer [!UICONTROL Remove label] om je keuzes te bevestigen.

![Het tabblad Gegevensbeheer van de werkruimte Datasets bevat een label voor een veld dat is gemarkeerd voor verwijdering.](./images/e2e/remove-label.png)

Nadat u het etiket van uw datasetgebied hebt verwijderd, navigeer aan de Redacteur van het Schema om het etiket aan het schema toe te voegen. Instructies over hoe u dit kunt doen vindt u in de [sectie over het toepassen van labels op een schema](#schema-labels).

>[!TIP]
>
>U kunt de schemanaam in het juiste spoor selecteren, die door de verbinding in de dialoog wordt gevolgd die lijkt om aan het aangewezen schema te navigeren.
>![Het tabblad Gegevensbeheer van de werkruimte Datasets met de schemanaam in de zijbalk en dialoogkoppeling gemarkeerd.](./images/e2e/navigate-to-schema.png)

Nadat u de benodigde labels hebt gemigreerd, controleert u of u de juiste labels hebt [beleid voor gegevensbeheer ingeschakeld](#policy).

## Beleid voor gegevensbeheer inschakelen {#policy}

Nadat u etiketten op uw schema&#39;s en/of datasets hebt toegepast, kunt u het beleid van het gegevensbeheer tot stand brengen dat de marketing acties beperkt waarvoor bepaalde etiketten kunnen worden gebruikt.

Selecteren **[!UICONTROL Policies]** in de linkernavigatie om een lijst van kernbeleid te bekijken dat door Adobe wordt bepaald, evenals om het even welk douanebeleid dat eerder door uw organisatie wordt gecreeerd.

Elk kernetiket heeft een bijbehorend kernbeleid dat, wanneer toegelaten, de aangewezen activeringsbeperkingen op om het even welke gegevens afdwingt die dat etiket bevatten. Als u een kernbeleid wilt inschakelen, selecteert u dit in de lijst en selecteert u vervolgens de optie **[!UICONTROL Policy status]** schakelen naar **[!UICONTROL Enabled]**.

![Afbeelding met een kernbeleid dat wordt ingeschakeld in de gebruikersinterface](./images/e2e/enable-core-policy.png)

Als het beschikbare kernbeleid niet al uw gebruiksgevallen (zoals wanneer u douaneetiketten aanwendt die u onder uw organisatie hebt bepaald) behandelt, kunt u een douanebeleid in plaats daarvan bepalen. Van de **[!UICONTROL Policies]** werkruimte, selecteert u **[!UICONTROL Create policy]**.

![Afbeelding die de [!UICONTROL Create policy] knop die wordt geselecteerd in de gebruikersinterface](./images/e2e/create-policy.png)

Er verschijnt een pop-up waarin u wordt gevraagd het type beleid te selecteren dat u wilt maken. Selecteren **[!UICONTROL Data governance policy]** selecteert u vervolgens **[!UICONTROL Continue]**.

![Afbeelding die de [!UICONTROL Data governance policy] optie geselecteerd](./images/e2e/governance-policy.png)

Geef op het volgende scherm een **[!UICONTROL Name]** en optioneel **[!UICONTROL Description]** voor het beleid. Selecteer in de onderstaande tabel de labels waarop dit beleid moet controleren. Met andere woorden, dit zijn de labels die door het beleid niet kunnen worden gebruikt voor de marketingactie(s) die u in de volgende stap opgeeft.

Als u meerdere labels selecteert, kunt u de opties in het rechterspoor gebruiken om te bepalen of alle labels aanwezig moeten zijn om te zorgen dat het beleid gebruiksbeperkingen afdwingt, of dat slechts een van de labels aanwezig moet zijn. Selecteer **[!UICONTROL Next]**.

![Beeld dat de basisconfiguratie van het beleid toont die in UI wordt voltooid](./images/e2e/configure-policy.png)

Selecteer in het volgende scherm de marketingacties waarvoor dit beleid de eerder geselecteerde labels beperkt. Selecteren **[!UICONTROL Next]** om door te gaan.

![Afbeelding die een marketingactie toont die wordt toegewezen aan een beleid in de gebruikersinterface](./images/e2e/select-marketing-action.png)

Het definitieve scherm toont een samenvatting van de details van het beleid en de acties het zal beperken waarvoor etiketten. Selecteren **[!UICONTROL Finish]** om het beleid te creëren.

![Beeld dat het beleid dat in UI wordt bevestigd toont wordt gevormd](./images/e2e/confirm-policy.png)

Het beleid wordt gemaakt, maar is ingesteld op [!UICONTROL Disabled] standaard. Selecteer het beleid in de lijst en stel de optie **[!UICONTROL Policy status]** schakelen naar **[!UICONTROL Enabled]** om het beleid mogelijk te maken.

![Afbeelding die het gemaakte beleid weergeeft dat in de gebruikersinterface wordt ingeschakeld](./images/e2e/enable-created-policy.png)

Ga verder met de bovenstaande stappen om het gewenste beleid te maken en in te schakelen voordat u verdergaat met de volgende stap.

## Marketing-acties voor doelen beheren {#destinations}

Als uw toegelaten beleid nauwkeurig om te bepalen welke gegevens aan een bestemming kunnen worden geactiveerd, moet u specifieke marketing acties aan die bestemming toewijzen.

Neem bijvoorbeeld een ingeschakeld beleid dat voorkomt dat gegevens een `C2` label dat niet voor de marketingactie wordt gebruikt &quot;[!UICONTROL Export to Third Party]&quot;. Wanneer het activeren van gegevens aan een bestemming, controleert het beleid welke marketing acties op de bestemming aanwezig zijn. Als &quot;[!UICONTROL Export to Third Party]&quot; aanwezig is, gegevens proberen te activeren met een `C2` resulteert in een beleidsovertreding. Als &quot;[!UICONTROL Export to Third Party]&quot; niet aanwezig is, wordt het beleid niet afgedwongen voor de bestemming en gegevens met `C2` etiketten kunnen vrij worden geactiveerd.

Wanneer [verbinding maken met een doel in de UI](../destinations/ui/connect-destination.md)de **[!UICONTROL Governance]** stap in het werkschema staat u toe om de marketing acties te selecteren die op deze bestemming van toepassing zijn, die uiteindelijk bepalen welk beleid van gegevensbeheer voor de bestemming wordt afgedwongen.

![Afbeelding met marketingacties die zijn geselecteerd voor een doel](./images/e2e/destination-marketing-actions.png)

## Beleidshandhaving testen {#test}

Zodra u uw gegevens hebt geëtiketteerd, gegevens toegelaten beleid, en marketing acties aan uw bestemmingen toegewezen, kunt u testen of uw beleid wordt afgedwongen zoals verwacht.

Als u dingen opstelling correct, wanneer u probeert om gegevens te activeren die door uw beleid worden beperkt, wordt de activering automatisch ontkend en een bericht van de beleidsschending verschijnt, schetterend gedetailleerde informatie van de gegevenslijn over wat de schending veroorzaakte.

Document weergeven op [automatische beleidshandhaving](./enforcement/auto-enforcement.md) voor details over hoe te om de berichten van de beleidsschending te interpreteren.

## Volgende stappen

Deze handleiding bevatte de vereiste stappen voor het configureren en afdwingen van beleidsregels voor gegevensbeheer in uw activeringsworkflows. Raadpleeg de volgende documentatie voor meer informatie over de componenten voor gegevensbeheer die bij deze handleiding betrokken zijn:

* [Labels voor gegevensgebruik](./labels/overview.md)
* [Beleid voor gegevensgebruik](./policies/overview.md)
* [Beleidshandhaving](./enforcement/overview.md)
