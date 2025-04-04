---
title: End-to-end handleiding voor gegevensbeheer
description: Volg het volledige proces voor het afdwingen van beperkingen van het gegevensgebruik voor gebieden en datasets in Adobe Experience Platform.
exl-id: f18ae032-027a-4c97-868b-e04753237c81
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1814'
ht-degree: 0%

---

# End-to-end handleiding voor gegevensbeheer

Als u wilt bepalen welke marketingacties op bepaalde gegevenssets en velden in Adobe Experience Platform kunnen worden uitgevoerd, moet u het volgende instellen:

1. [ pas etiketten ](#labels) op de schemagebieden of volledige datasets toe, het waarvan gebruik u wilt beperken.
1. [ vormt en laat het beleid van het gegevensbeheer ](#policy) toe dat bepaalt welke soorten geëtiketteerde gegevens voor bepaalde marketing acties kunnen worden gebruikt.
1. [ pas marketing acties op uw bestemmingen ](#destinations) toe om op te wijzen welk beleid op gegevens van toepassing is die naar die bestemmingen worden verzonden.

Zodra u klaar bent met het vormen van uw etiketten, governancebeleid, en marketing acties, kunt u [ uw beleidshandhaving ](#test) testen om ervoor te zorgen het zoals verwacht werkt.

Deze gids doorloopt het volledige proces om een beleid van het gegevensbeheer in Experience Platform UI te vormen en te handhaven. Voor meer gedetailleerde informatie over de eigenschappen die in deze gids worden gebruikt, verwijs naar de overzichtsdocumentatie over de volgende onderwerpen:

* [Adobe Experience Platform Data Governance](./home.md)
* [Labels voor gegevensgebruik](./labels/overview.md)
* [Beleid voor gegevensgebruik](./policies/overview.md)
* [Beleidshandhaving](./enforcement/overview.md)

>[!NOTE]
>
>Deze handleiding is vooral gericht op het instellen en afdwingen van beleid voor het gebruik of activeren van gegevens in Experience Platform. Als u probeert om **toegang** tot de gegevens zelf voor bepaalde gebruikers van Experience Platform binnen uw organisatie te beperken, zie in plaats daarvan de gids van begin tot eind op [ op attribuut-gebaseerde toegangsbeheer ](../access-control/abac/end-to-end-guide.md). Op attributen-gebaseerde toegangscontrole gebruikt ook etiketten en beleid, maar voor een verschillend gebruiksgeval dan gegevensbeheer.

## Labels toepassen {#labels}

>[!IMPORTANT]
>
>Labels kunnen niet langer op afzonderlijke velden op het niveau van de gegevensset worden toegepast. Deze workflow is vervangen door labels op schemaniveau. Nochtans, kunt u nog een volledige dataset etiketteren. Alle labels die eerder op afzonderlijke gegevenssetvelden zijn toegepast, worden tot 31 mei 2024 nog steeds ondersteund via de gebruikersinterface van Experience Platform. Om ervoor te zorgen dat uw etiketten over alle schema&#39;s verenigbaar zijn, moeten om het even welke etiketten die eerder aan gebieden op het datasetniveau worden vastgemaakt door u over het komende jaar worden gemigreerd aan het schemaniveau. Zie de sectie op [ migrerend eerder toegepaste etiketten ](#migrate-labels) voor instructies op hoe te om dit te doen.

U kunt [ etiketten op een schema ](#schema-labels) toepassen zodat alle datasets die op dat schema worden gebaseerd de zelfde etiketten erven. Hierdoor kunt u de labels voor gegevensbeheer, toestemming en toegangsbeheer op één locatie beheren. Door beperkingen van het gegevensgebruik op het schemaniveau af te dwingen, verspreidt het effect zich stroomafwaarts aan alle datasets die op dat schema gebaseerd zijn. Labels die worden toegepast op het niveau van het schemaveld ondersteunen het gebruik van Data Governance en zijn te vinden op het tabblad Datasets [!UICONTROL Data Governance] onder de kolom [!UICONTROL Field Name] als alleen-lezen labels.

Als er een specifieke dataset is die u beperkingen van het gegevensgebruik wilt afdwingen, kunt u [ etiketten rechtstreeks op die dataset ](#dataset-labels) of specifieke gebieden binnen die dataset toepassen.

Alternatief, kunt u [ etiketten op een schema ](#schema-labels) toepassen zodat alle datasets die op dat schema worden gebaseerd de zelfde etiketten erven.

>[!NOTE]
>
>Voor meer informatie over de verschillende etiketten van het gegevensgebruik en hun voorgenomen gebruik, zie de [ de etiketverwijzing van het gegevensgebruik ](./labels/reference.md). Als de beschikbare kernetiketten niet alle gewenste gebruiksgevallen behandelen, kunt u [ uw eigen douanelabels ](./labels/user-guide.md#manage-custom-labels) eveneens bepalen.

### Labels toepassen op een volledige gegevensset {#dataset-labels}

Selecteer **[!UICONTROL Datasets]** in de linkernavigatie, dan selecteer de naam van de dataset u etiketten op wilt toepassen. U kunt optioneel het onderzoeksgebied gebruiken om onderaan de lijst van getoonde datasets te versmallen.

![ de werkruimte van Datasets doorbladert lusje met Datasets en een benadrukte datasetrij.](./images/e2e/select-dataset.png)

De detailweergave voor de gegevensset wordt weergegeven. Selecteer het tabblad **[!UICONTROL Data governance]** om een lijst weer te geven met de velden van de gegevensset en eventuele labels die er al op zijn toegepast. Selecteer het potloodpictogram om de labels van gegevenssets te bewerken.

![ het beheer lusje van Gegevens voor de dataset van de Leden van de Loyalty met het benadrukte potloodpictogram.](./images/e2e/edit-dataset-labels.png)

Het dialoogvenster [!UICONTROL Edit governance labels] wordt weergegeven. Selecteer het juiste governancelabel en selecteer **[!UICONTROL Save]** .

![ Edit governance etiketteert dialoog met label checkbox en sparen benadrukte.](./images/e2e/edit-dataset-governance-labels.png)

### Labels toepassen op een schema {#schema-labels}

Selecteer **[!UICONTROL Schemas]** in de linkernavigatie en selecteer vervolgens het schema waaraan u labels wilt toevoegen in de lijst.

>[!TIP]
>
>Als u niet zeker bent welk schema op een bepaalde dataset van toepassing is, selecteer **[!UICONTROL Datasets]** in de linkernavigatie, dan de verbinding onder de **[!UICONTROL Schema]** kolom voor de gewenste dataset. Selecteer de schemanaam in popover die lijkt om het schema in de Redacteur van het Schema te openen.
>
>![ Beeld dat een verbinding aan het schema van een dataset toont ](./images/e2e/schema-from-dataset.png)

De structuur van het schema wordt weergegeven in de Schema-editor. Van hier, selecteer het **[!UICONTROL Labels]** lusje om een lijstmening van de gebieden van het schema en de etiketten te tonen die reeds op hen zijn toegepast. Selecteer de selectievakjes naast de velden waaraan u labels wilt toevoegen en selecteer vervolgens **[!UICONTROL Apply access and data governance labels]** in de rechtertrack.

![ het lusje van Etiketten van de werkruimte van het Schema met één enkel die schemagebied wordt geselecteerd en toegang en de benadrukte etiketten van het gegevensbeheer toepast.](./images/e2e/schema-field-label.png)

>[!NOTE]
>
>Als u labels wilt toevoegen aan alle velden in het schema, selecteert u het potloodpictogram op de bovenste rij.
>
>![ Beeld dat het potloodpictogram toont dat van de mening van schemalabels wordt geselecteerd ](./images/e2e/label-whole-schema.png)

Het dialoogvenster [!UICONTROL Apply access and data governance labels] wordt weergegeven. Selecteer de labels die u wilt toepassen op het gekozen schemaveld. Selecteer **[!UICONTROL Save]** als u klaar bent.

![ toepassen toegang en de etiketten van het gegevensbeheer die veelvoudige etiketten tonen die aan een schemagebied worden toegevoegd.](./images/e2e/save-schema-labels.png)

Ga als volgt te werk om labels toe te passen op verschillende velden (of verschillende schema&#39;s). Wanneer gebeëindigd, kunt u aan de volgende stap van [ verdergaan toelatend beleid van het gegevensbeheer ](#policy).

### Labels migreren die eerder zijn toegepast op het niveau van de gegevensset {#migrate-labels}

Selecteer **[!UICONTROL Dataset]** in de linkernavigatie, dan selecteer de naam van de dataset u etiketten van wilt migreren. U kunt optioneel het onderzoeksgebied gebruiken om onderaan de lijst van getoonde datasets te versmallen.

![ het Browse lusje van de werkruimte van Datasets met de benadrukt Dataset van de Leden van de Loyalty.](./images/e2e/select-dataset.png)

De detailweergave voor de gegevensset wordt weergegeven. Selecteer het tabblad **[!UICONTROL Data governance]** om een lijst weer te geven met de velden van de gegevensset en eventuele labels die er al op zijn toegepast. Selecteer het pictogram Annuleren naast een label dat u uit een veld wilt verwijderen. Er verschijnt een bevestigingsvenster. Selecteer [!UICONTROL Remove label] om uw opties te bevestigen.

![ het lusje van het Beheer van Gegevens van de werkruimte Datasets met een etiket voor een gebied dat voor verwijdering wordt benadrukt.](./images/e2e/remove-label.png)

Nadat u het etiket van uw datasetgebied hebt verwijderd, navigeer aan de Redacteur van het Schema om het etiket aan het schema toe te voegen. De instructies op hoe te om dit te doen, kunnen in de [ sectie worden gevonden bij het toepassen van etiketten op een schema ](#schema-labels).

>[!TIP]
>
>U kunt de schemanaam in het juiste spoor selecteren, die door de verbinding in de dialoog wordt gevolgd die lijkt om aan het aangewezen schema te navigeren.
>![Het lusje van het Beheer van Gegevens van de werkruimte Datasets met de schemanaam in de benadrukte sidebar en dialoogverbinding.](./images/e2e/navigate-to-schema.png)

Nadat u de noodzakelijke etiketten hebt gemigreerd, zorg ervoor dat u het correcte [ toegelaten beleid van het gegevensbeheer ](#policy) hebt.

## Beleid voor gegevensbeheer inschakelen {#policy}

Nadat u etiketten op uw schema&#39;s en/of datasets hebt toegepast, kunt u het beleid van het gegevensbeheer tot stand brengen dat de marketing acties beperkt waarvoor bepaalde etiketten kunnen worden gebruikt.

Selecteer **[!UICONTROL Policies]** in de linkernavigatie om een lijst van kernbeleid te bekijken dat door Adobe wordt bepaald, evenals om het even welk douanebeleid dat eerder door uw organisatie wordt gecreeerd.

Elk kernetiket heeft een bijbehorend kernbeleid dat, wanneer toegelaten, de aangewezen activeringsbeperkingen op om het even welke gegevens afdwingt die dat etiket bevatten. Als u een kernbeleid wilt inschakelen, selecteert u dit in de lijst en selecteert u de **[!UICONTROL Policy status]** -schakeloptie naar **[!UICONTROL Enabled]** .

![ Beeld dat een kernbeleid toont dat in UI ](./images/e2e/enable-core-policy.png) wordt toegelaten

Als het beschikbare kernbeleid niet al uw gebruiksgevallen (zoals wanneer u douaneetiketten aanwendt die u onder uw organisatie hebt bepaald) behandelt, kunt u een douanebeleid in plaats daarvan bepalen. Selecteer in de **[!UICONTROL Policies]** -werkruimte de optie **[!UICONTROL Create policy]** .

![ Beeld dat de [!UICONTROL Create policy] knoop toont die in UI ](./images/e2e/create-policy.png) wordt geselecteerd

Er verschijnt een pop-up waarin u wordt gevraagd het type beleid te selecteren dat u wilt maken. Selecteer **[!UICONTROL Data governance policy]** en selecteer vervolgens **[!UICONTROL Continue]** .

![ Beeld dat de [!UICONTROL Data governance policy] optie toont die ](./images/e2e/governance-policy.png) wordt geselecteerd

Geef op het volgende scherm een **[!UICONTROL Name]** en optioneel **[!UICONTROL Description]** voor het beleid op. Selecteer in de onderstaande tabel de labels waarop dit beleid moet controleren. Met andere woorden, dit zijn de labels die door het beleid niet kunnen worden gebruikt voor de marketingactie(s) die u in de volgende stap opgeeft.

Als u meerdere labels selecteert, kunt u de opties in het rechterspoor gebruiken om te bepalen of alle labels aanwezig moeten zijn om te zorgen dat het beleid gebruiksbeperkingen afdwingt, of dat slechts een van de labels aanwezig moet zijn. Selecteer **[!UICONTROL Next]** als u klaar bent.

![ Beeld dat de basisconfiguratie van het beleid toont in UI wordt voltooid ](./images/e2e/configure-policy.png)

Selecteer in het volgende scherm de marketingacties waarvoor dit beleid de eerder geselecteerde labels beperkt. Selecteer **[!UICONTROL Next]** om door te gaan.

![ Beeld dat een marketing actie toont die aan een beleid in UI ](./images/e2e/select-marketing-action.png) wordt toegewezen

Het definitieve scherm toont een samenvatting van de details van het beleid en de acties het zal beperken waarvoor etiketten. Selecteer **[!UICONTROL Finish]** om het beleid te maken.

![ Beeld die het beleid tonen dat in UI wordt bevestigd ](./images/e2e/confirm-policy.png)

Het beleid wordt gemaakt, maar is standaard ingesteld op [!UICONTROL Disabled] . Selecteer het beleid in de lijst en stel **[!UICONTROL Policy status]** toggle in op **[!UICONTROL Enabled]** om het beleid in te schakelen.

![ Beeld dat het gecreeerde beleid toont dat in UI ](./images/e2e/enable-created-policy.png) wordt toegelaten

Ga verder met de bovenstaande stappen om het gewenste beleid te maken en in te schakelen voordat u verdergaat met de volgende stap.

## Marketing-acties voor doelen beheren {#destinations}

Als uw toegelaten beleid nauwkeurig om te bepalen welke gegevens aan een bestemming kunnen worden geactiveerd, moet u specifieke marketing acties aan die bestemming toewijzen.

Bijvoorbeeld, overweeg een toegelaten beleid dat om het even welk gegeven verhindert dat een `C2` etiket voor de marketing actie &quot; [!UICONTROL Export to Third Party] wordt gebruikt. Wanneer het activeren van gegevens aan een bestemming, controleert het beleid welke marketing acties op de bestemming aanwezig zijn. Als &quot;[!UICONTROL Export to Third Party]&quot; aanwezig is, leidt het activeren van gegevens met een `C2` -label tot een schending van het beleid. Als &quot;[!UICONTROL Export to Third Party]&quot; niet aanwezig is, wordt het beleid niet afgedwongen voor de bestemming en kunnen gegevens met `C2` -labels vrij worden geactiveerd.

Wanneer [ verbindend een bestemming in UI ](../destinations/ui/connect-destination.md), staat de **[!UICONTROL Governance]** stap in het werkschema u toe om de marketing acties te selecteren die op deze bestemming van toepassing zijn, die uiteindelijk bepalen welk beleid van gegevensbeheer voor de bestemming wordt afgedwongen.

![ Beeld dat marketing acties toont die voor een bestemming ](./images/e2e/destination-marketing-actions.png) worden geselecteerd

## Beleidshandhaving testen {#test}

Zodra u uw gegevens hebt geëtiketteerd, gegevens toegelaten beleid, en marketing acties aan uw bestemmingen toegewezen, kunt u testen of uw beleid wordt afgedwongen zoals verwacht.

Als u dingen opstelling correct, wanneer u probeert om gegevens te activeren die door uw beleid worden beperkt, wordt de activering automatisch ontkend en een bericht van de beleidsschending verschijnt, schetterend gedetailleerde informatie van de gegevenslijn over wat de schending veroorzaakte.

Zie het document op [ automatische beleidshandhaving ](./enforcement/auto-enforcement.md) voor details op hoe te om de berichten van de beleidsschending te interpreteren.

## Volgende stappen

Deze handleiding bevatte de vereiste stappen voor het configureren en afdwingen van beleidsregels voor gegevensbeheer in uw activeringsworkflows. Raadpleeg de volgende documentatie voor meer informatie over de componenten voor gegevensbeheer die bij deze handleiding betrokken zijn:

* [Labels voor gegevensgebruik](./labels/overview.md)
* [Beleid voor gegevensgebruik](./policies/overview.md)
* [Beleidshandhaving](./enforcement/overview.md)
