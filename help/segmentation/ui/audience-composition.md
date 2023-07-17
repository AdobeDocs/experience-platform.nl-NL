---
solution: Experience Platform
title: UI-gids voor soorten publiek
description: De Samenstelling van het publiek in Adobe Experience Platform UI verstrekt een rijke werkruimte die u toestaat om met de gegevenselementen van het Profiel in wisselwerking te staan. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van soorten publiek voor uw organisatie.
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 13492b90552d16334030792323956ea18ca928dc
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 0%

---

# Handleiding voor compositie van publiek

De Samenstelling van het publiek verstrekt een werkruimte om publiek te bouwen en uit te geven, gebruikend blokken die worden gebruikt om verschillende acties te vertegenwoordigen.

![De interface Audience Composition.](../images/ui/audience-composition/audience-composition.png)

Als u de details van de compositie wilt wijzigen, inclusief de titel en beschrijving, selecteert u de optie ![schuifregelaars](../images/ui/audience-composition/sliders.png) knop.

De **[!UICONTROL Composition properties]** wordt weergegeven. U kunt hier details van uw samenstelling, met inbegrip van de titel en beschrijving opnemen.

![De keuzelijst Compositie-eigenschappen wordt weergegeven.](../images/ui/audience-composition/composition-properties.png)

>[!NOTE]
>
>Als u **niet** Als u de compositie een titel geeft, krijgt deze de titel &quot;Compositie&quot;, gevolgd door de datum en tijd waarop de compositie wordt gemaakt.

Nadat u de details van uw compositie hebt bijgewerkt, selecteert u **[!UICONTROL Save]** om deze updates te bevestigen. Het canvas van de publiekscompositie verschijnt opnieuw.

Het canvas van de publiekssamenstelling bestaat uit vier verschillende types van blokken: **[[!UICONTROL Audience]](#audience-block)**, **[[!UICONTROL Exclude]](#exclude-block)**, **[[!UICONTROL Rank]](#rank-block)**, en **[[!UICONTROL Split]](#split-block)**.

## [!UICONTROL Audience] {#audience-block}

De **[!UICONTROL Audience]** met bloktype kunt u de subdoelgroepen toevoegen die u wilt samenstellen voor een groter publiek. Standaard kunt u een **[!UICONTROL Audience]** blok is inbegrepen bij de bovenkant van het samenstellingscanvas.

Wanneer u **[!UICONTROL Audience]** blok, de juiste spoorvertoningen controles voor het etiketteren van het publiek, toevoegend publiek aan het blok, en bouwend douaneregels voor het publieksblok.

>[!NOTE]
>
>U kunt een publiek toevoegen **of** een aangepaste regel maken. Deze twee functies **kan** samen worden gebruikt.

![De het blokdetails van het Publiek worden getoond.](../images/ui/audience-composition/audience-block.png)

### [!UICONTROL Add audience] {#add-audience}

Om publiek aan het blok van het Publiek toe te voegen. selecteren **[!UICONTROL Add Audience]**.

![De knop voor het publiek toevoegen is gemarkeerd.](../images/ui/audience-composition/add-audience.png)

Er wordt een lijst met doelgroepen weergegeven. Selecteer het publiek dat u wilt opnemen, gevolgd door **[!UICONTROL Add]** om ze toe te voegen aan uw publieksblok.

![Er wordt een lijst met doelgroepen weergegeven. In dit dialoogvenster kunt u selecteren welk publiek u wilt toevoegen.](../images/ui/audience-composition/select-audience.png)

Uw geselecteerde publiek verschijnt nu binnen de juiste spoorlijn wanneer **[!UICONTROL Audience]** wordt geselecteerd. Vanaf hier kunt u het samenvoegingstype van het gecombineerde publiek wijzigen.

![De mogelijke samenvoegingstypen voor het publiek worden gemarkeerd.](../images/ui/audience-composition/merge-types.png)

| Type samenvoegen | Beschrijving |
| ---------- | ----------- |
| [!UICONTROL Union] | Het publiek wordt in één publiek samengevoegd. Dit zou het equivalent van een OF verrichting zijn. |
| [!UICONTROL Intersection] | Het publiek wordt gecombineerd, met alleen het publiek dat wordt gedeeld in **alles** van de toegevoegde waarden. Dit zou het equivalent van een EN verrichting zijn. |
| [!UICONTROL Exclude overlap] | Het publiek wordt gecombineerd, met alleen het publiek dat wordt gedeeld in **één, maar niet alle** van de toegevoegde waarden. Dit is het equivalent van een XOR-bewerking. |

### [!UICONTROL Build rule] {#build-rule}

Als u een aangepaste regel wilt toevoegen aan het blok Publiek, selecteert u **[!UICONTROL Build rule]**.

![De knop Build rule is gemarkeerd.](../images/ui/audience-composition/build-rule.png)

De Segment Builder wordt weergegeven. U kunt de Bouwer van het Segment gebruiken om een douaneregel tot stand te brengen voor het publiek te volgen. Meer informatie over het gebruik van de Segment Builder vindt u in de [Handleiding Segment Builder](./segment-builder.md).

![De gebruikersinterface van Segment Builder wordt weergegeven.](../images/ui/audience-composition/segment-builder.png)

Nadat u een aangepaste regel hebt toegevoegd, selecteert u **[!UICONTROL Save]** om de regel aan uw publiek toe te voegen.

![](../images/ui/audience-composition/custom-rule.png)

## [!UICONTROL Exclude] {#exclude-block}

De **[!UICONTROL Exclude]** met bloktype kunt u opgegeven deelsoorten of kenmerken uitsluiten van uw nieuwe grotere publiek.

Om een **[!UICONTROL Exclude]** blok, selecteer **+** pictogram, gevolgd door **[!UICONTROL Exclude]**.

![De optie Uitsluiten is geselecteerd.](../images/ui/audience-composition/add-exclude-block.png)

De **[!UICONTROL Exclude]** wordt toegevoegd. Wanneer dit blok wordt geselecteerd, verschijnen de details over de uitsluiting in het juiste spoor. Dit geldt ook voor het label en uitsluitingstype van het blok. U kunt uitsluiten [op publiek](#exclude-audience) of [by, kenmerk](#exclude-attribute).

![Het blok van de Uitsluiting, die de twee verschillende beschikbare uitsluitingstypes benadrukken.](../images/ui/audience-composition/exclude.png)

### Uitsluiten door publiek {#exclude-audience}

Als u uitsluiting door het publiek toepast, kunt u selecteren welk publiek u wilt uitsluiten door **[!UICONTROL Add Audience]**.

![De [!UICONTROL Add audience] is geselecteerd, waarmee u kunt kiezen welk publiek u wilt uitsluiten.](../images/ui/audience-composition/add-excluded-audience.png)

Er wordt een lijst met doelgroepen weergegeven. Selecteren **[!UICONTROL Add]** om het publiek toe te voegen u aan uw exclusief blok wilt uitsluiten.

![Er wordt een lijst met doelgroepen weergegeven. In dit dialoogvenster kunt u selecteren welk publiek u wilt toevoegen.](../images/ui/audience-composition/select-audience.png)

### Uitsluiten op kenmerk {#exclude-attribute}

Als u per kenmerk uitschakelt, kunt u selecteren welke kenmerken u wilt uitsluiten door de optie ![filter](../images/ui/audience-composition/filter-attribute.png) pictogram in de **[!UICONTROL Exclusion rule]** sectie.

![De kenmerkensectie wordt gemarkeerd en u ziet waar u wilt selecteren om het kenmerk te kiezen dat u wilt uitsluiten.](../images/ui/audience-composition/exclude-attribute.png)

Er wordt een lijst met profielkenmerken weergegeven. Selecteer het kenmerktype dat u wilt uitsluiten, gevolgd door **[!UICONTROL Select]** om deze aan uw uitsluitingsblok toe te voegen.

![Er wordt een lijst met kenmerken weergegeven.](../images/ui/audience-composition/select-attribute-exclude.png)

<!-- ## [!UICONTROL Join] {#join-block}

The **[!UICONTROL Join]** block type allows you to add in external audiences from datasets that have not yet been processed by Adobe Experience Platform.

To add a **[!UICONTROL Join]** block, select the **+** icon, followed by **[!UICONTROL Join]**.

![The Join option is selected.](../images/ui/audience-composition/add-join-block.png)

When you select the block, details about the join are shown in the right rail, including the block's label and the option to add audiences to the enrichment dataset.

![The join block is highlighted, including details about the join block.](../images/ui/audience-composition/join.png)

After selecting **[!UICONTROL Add Audience]**, a list of audiences appears. Select the audiences you want to include, followed by **[!UICONTROL Add]** to add them to your join block.

![A list of audiences appears. You can select which audience you want to add from this dialog.](../images/ui/audience-composition/select-audience.png)

Your selected audiences now appear within the right rail when the **[!UICONTROL Join]** block is selected. 

![The audiences that were added as part of the Join are shown.](../images/ui/audience-composition/selected-audiences.png) -->

## [!UICONTROL Rank] {#rank-block}

De **[!UICONTROL Rank]** het bloktype staat u toe om profielen te rangschikken en te sorteren die op een gespecificeerd attribuut worden gebaseerd en deze gerangschikte profielen aan uw samenstelling te omvatten.

Als u een **[!UICONTROL Rank]** blok, selecteer **+** pictogram, gevolgd door **[!UICONTROL Rank]**.

![De optie Rank is geselecteerd.](../images/ui/audience-composition/add-rank-block.png)

Wanneer u het blok selecteert, worden de details over het rangschikken getoond in de juiste spoorstaaf, met inbegrip van het etiket van het blok, het attribuut aan rangschikking, de rangschikking, en een knevel om het aantal profielen te beperken tot rangschikking.

![De rank blok wordt gemarkeerd, evenals de details van de rank blok.](../images/ui/audience-composition/rank.png)

Als u wilt selecteren op welk kenmerk het publiek moet worden geplaatst, selecteert u de optie ![filter](../images/ui/audience-composition/filter-attribute.png) pictogram.

![Het filterpictogram wordt gemarkeerd en geeft aan wat u moet selecteren om het selectiescherm voor profielkenmerken te openen.](../images/ui/audience-composition/select-rank-attribute.png)

Er wordt een lijst met profielkenmerken weergegeven. Op deze popover, kunt u het attributentype selecteren u uw publiek door wilt rangschikken. Selecteren **[!UICONTROL Select]** om het aan uw rangschikkingsblok toe te voegen. Let op: het geselecteerde kenmerk kan **alleen** zijn getallen.

![Er wordt een lijst met kenmerken weergegeven.](../images/ui/audience-composition/select-attribute-rank.png)

Na het selecteren van de attributen, kunt u de orde selecteren om het door te rangschikken. Dit gebeurt in oplopende (van laagste naar hoogste) of aflopende (van hoogste naar laagste) volgorde.

Bovendien, kunt u het aantal teruggekeerde publiek beperken door toe te laten **[!UICONTROL Add profile limit]** schakelen. Wanneer deze schakeloptie is ingeschakeld, kunt u het maximale aantal keren instellen dat binnen het **[!UICONTROL Included profiles]** veld.

![De schakeloptie voor het toevoegen van profiellimieten wordt gemarkeerd. Hiermee kunt u het aantal geretourneerde soorten publiek beperken.](../images/ui/audience-composition/add-profile-limit.png)

## [!UICONTROL Split] {#split-block}

De **[!UICONTROL Split]** met bloktype kunt u het nieuwe publiek opsplitsen in verschillende deelsoorten. U kunt dit publiek splitsen op basis van een percentage of op basis van een kenmerk.

Als u een **[!UICONTROL Split]** blok, selecteer **+** pictogram, gevolgd door **[!UICONTROL Split]**.

![De optie Splitsen is geselecteerd.](../images/ui/audience-composition/add-split-block.png)

### Splitsen op percentage {#split-percentage}

Bij het splitsen naar percentage worden de doelgroepen willekeurig gesplitst op basis van het aantal beschikbare paden en percentages.

U kunt bijvoorbeeld drie paden hebben, elk met een ander percentage profielen.

![De uitsplitsing in aantal opgeslagen soorten publiek en percentages wordt weergegeven.](../images/ui/audience-composition/percentages.png)

### Splitsen op kenmerk {#split-attribute}

Bij splitsen op kenmerk wordt het publiek gesplitst op basis van de opgegeven kenmerken. Selecteer het kenmerk waarop u wilt splitsen **[!UICONTROL Split]** blok, gevolgd door de ![filter](../images/ui/audience-composition/filter-attribute.png) pictogram.

![De filterknop wordt geselecteerd en geeft aan hoe u op kenmerk moet filteren.](../images/ui/audience-composition/select-split-attribute.png)

Er wordt een lijst met profielkenmerken weergegeven. Selecteer het kenmerktype, gevolgd door **[!UICONTROL Select]** om het toe te voegen aan uw gesplitste blok.

![Er wordt een lijst met kenmerken weergegeven.](../images/ui/audience-composition/select-attribute-exclude.png)

Nadat u het kenmerk hebt geselecteerd, kunt u kiezen tot welke profielen u wilt behoren door de waarden in het deelvenster **[!UICONTROL Values]** veld.

![De waarden waarop u de kenmerken wilt splitsen, worden toegevoegd.](../images/ui/audience-composition/attribute-split-values.png)

Daarnaast kunt u de opdracht **[!UICONTROL Other profiles]** Schakel deze optie in om een subpubliek te maken dat uit alle niet-geselecteerde profielen bestaat.

![De schakeloptie Andere profielen wordt gemarkeerd.](../images/ui/audience-composition/split-other-profiles.png)

## Uw publiek publiceren

Nadat u de doelgroep hebt samengesteld, kunt u deze opslaan en publiceren door **[!UICONTROL Publish]**.

![De knop Publiceren is gemarkeerd en geeft aan hoe u uw publiek kunt opslaan en publiceren.](../images/ui/audience-composition/publish.png)

Als er fouten optreden bij het maken van het publiek, verschijnt er een waarschuwing met de informatie over het oplossen van het probleem.

![De knop Publiceren is gemarkeerd en geeft aan hoe u uw publiek kunt opslaan en publiceren.](../images/ui/audience-composition/audience-alert.png)

## Volgende stappen

De Samenstelling van het publiek verstrekt een rijke werkschema toelatend u om publiek van de verschillende bloktypes tot stand te brengen. Meer over andere delen van de Dienst UI van de Segmentatie leren, gelieve te lezen [Gebruikershandleiding voor segmentatieservice](./overview.md).
