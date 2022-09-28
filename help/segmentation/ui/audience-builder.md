---
keywords: Experience Platform;thuis;populaire onderwerpen;Segmenteringsdienst;segmentatie;segmenteringsservice;gebruikershandleiding;ui-gids;gebruikershandleiding;publiek ontwerper;publiek ontwikkelaar;publiek;publiek;publiek ui-gids; publiek
solution: Experience Platform
title: UI-gids voor soorten publiek
topic-legacy: ui guide
description: De Audience Builder in de gebruikersinterface van Adobe Experience Platform biedt een rijke werkruimte die u in staat stelt te werken met de gegevenselementen van het Profiel. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van soorten publiek voor uw organisatie.
hide: true
hidefromtoc: true
source-git-commit: f71d49b576059e687c337cbacd6dd3d525e97834
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# Handleiding voor de gebruikersinterface van Audience Builder

>[!IMPORTANT]
>
>De Audience Builder is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De Audience Builder biedt een werkruimte voor het maken en bewerken van soorten publiek, met behulp van blokken die worden gebruikt om verschillende acties te vertegenwoordigen.

![De interface van Audience Builder.](../images/ui/audience-builder/audience-builder.png)

Het canvas van de publiekssamenstelling bestaat uit vijf verschillende types van blokken: **[[!UICONTROL Audience]](#audience-block)**, **[[!UICONTROL Exclude]](#exclude-block)**, **[[!UICONTROL Join]](#join-block)**, **[[!UICONTROL Rank]](#rank-block)**, en **[[!UICONTROL Split]](#split-block)**.

## [!UICONTROL Audience] {#audience-block}

De **[!UICONTROL Audience]** met bloktype kunt u de subdoelgroepen toevoegen die u wilt samenstellen voor een groter publiek. Standaard kunt u een **[!UICONTROL Audience]** blok is inbegrepen bij de bovenkant van het samenstellingscanvas.

Wanneer u **[!UICONTROL Audience]** blok, de juiste spoorstaaf toont controles voor etikettering en toevoegend publiek aan het blok.

![De het blokdetails van het Publiek worden getoond.](../images/ui/audience-builder/select-audience.png)

Na het selecteren **[!UICONTROL Add Audience]**, wordt een lijst met doelgroepen weergegeven. Selecteer het publiek dat u wilt opnemen, gevolgd door **[!UICONTROL Add]** om ze toe te voegen aan uw publieksblok.

![Er wordt een lijst met doelgroepen weergegeven. In dit dialoogvenster kunt u selecteren welk publiek u wilt toevoegen.](../images/ui/audience-builder/select-audience.png)

Uw geselecteerde publiek verschijnt nu binnen de juiste spoorlijn wanneer **[!UICONTROL Audience]** wordt geselecteerd. Vanaf hier kunt u het samenvoegingstype van het gecombineerde publiek wijzigen.

![De mogelijke samenvoegingstypen voor het publiek worden gemarkeerd.](../images/ui/audience-builder/merge-types.png)

| Type samenvoegen | Beschrijving |
| ---------- | ----------- |
| [!UICONTROL Union] | Het publiek wordt in één publiek samengevoegd. Dit zou het equivalent van een OF verrichting zijn. |
| [!UICONTROL Intersection] | Het publiek wordt gecombineerd, met alleen het publiek dat wordt gedeeld in **alles** van de toegevoegde waarden. Dit zou het equivalent van een EN verrichting zijn. |
| [!UICONTROL Exclude overlap] | Het publiek wordt gecombineerd, met alleen het publiek dat wordt gedeeld in **één, maar niet alle** van de toegevoegde waarden. Dit is het equivalent van een XOR-bewerking. |

## [!UICONTROL Exclude] {#exclude-block}

De **[!UICONTROL Exclude]** met bloktype kunt u opgegeven deelsoorten of kenmerken uitsluiten van uw nieuwe grotere publiek.

Om een **[!UICONTROL Exclude]** blok, selecteer **+** pictogram, gevolgd door **[!UICONTROL Exclude]**.

![De optie Uitsluiten is geselecteerd.](../images/ui/audience-builder/add-exclude-block.png)

De **[!UICONTROL Exclude]** wordt toegevoegd. Wanneer dit blok wordt geselecteerd, verschijnen de details over de uitsluiting in het juiste spoor. Dit geldt ook voor het label en uitsluitingstype van het blok. U kunt uitsluiten [op publiek](#exclude-audience) of [by, kenmerk](#exclude-attribute).

![Het blok van de Uitsluiting, die de twee verschillende beschikbare uitsluitingstypes benadrukken.](../images/ui/audience-builder/exclude.png)

### Uitsluiten door publiek {#exclude-audience}

Als u uitsluiting door het publiek toepast, kunt u selecteren welk publiek u wilt uitsluiten door **[!UICONTROL Add Audience]**.

![De knop voor het publiek toevoegen is geselecteerd, zodat u kunt kiezen welk publiek u wilt uitsluiten.](../images/ui/audience-builder/add-excluded-audience.png)

Er wordt een lijst met doelgroepen weergegeven. Selecteren **[!UICONTROL Add]** om het publiek toe te voegen u aan uw exclusief blok wilt uitsluiten.

![Er wordt een lijst met doelgroepen weergegeven. In dit dialoogvenster kunt u selecteren welk publiek u wilt toevoegen.](../images/ui/audience-builder/select-audience.png)

### Uitsluiten op kenmerk {#exclude-attribute}

Als u per kenmerk uitschakelt, kunt u selecteren welke kenmerken u wilt uitsluiten door de optie ![filter](../images/ui/audience-builder/filter-attribute.png) pictogram in de **[!UICONTROL Exclusion rule]** sectie.

![De kenmerkensectie wordt gemarkeerd en u ziet waar u wilt selecteren om het kenmerk te kiezen dat u wilt uitsluiten.](../images/ui/audience-builder/exclude-attribute.png)

Er wordt een lijst met profielkenmerken weergegeven. Selecteer het kenmerktype dat u wilt uitsluiten, gevolgd door **[!UICONTROL Select]** om deze aan uw uitsluitingsblok toe te voegen.

![Er wordt een lijst met kenmerken weergegeven.](../images/ui/audience-builder/select-attribute.png)

## [!UICONTROL Join] {#join-block}

De **[!UICONTROL Join]** het bloktype staat u toe om in extern publiek van datasets toe te voegen die nog niet door Adobe Experience Platform zijn verwerkt.

Als u een **[!UICONTROL Join]** blok, selecteer **+** pictogram, gevolgd door **[!UICONTROL Join]**.

![De optie Verbinden is geselecteerd.](../images/ui/audience-builder/add-join-block.png)

Wanneer u het blok selecteert, worden de details over de verbinding getoond in het juiste spoor, met inbegrip van het etiket van het blok en de optie om publiek aan de verrijkingsdataset toe te voegen.

![Het verbindingsblok wordt gemarkeerd, inclusief details over het blok join.](../images/ui/audience-builder/join.png)

Na het selecteren **[!UICONTROL Add Audience]**, wordt een lijst met doelgroepen weergegeven. Selecteer het publiek dat u wilt opnemen, gevolgd door **[!UICONTROL Add]** om hen aan uw te toevoegen toetreedt blok.

![Er wordt een lijst met doelgroepen weergegeven. In dit dialoogvenster kunt u selecteren welk publiek u wilt toevoegen.](../images/ui/audience-builder/select-audience.png)

Uw geselecteerde publiek verschijnt nu binnen de juiste spoorlijn wanneer **[!UICONTROL Join]** wordt geselecteerd.

![Het publiek dat is toegevoegd als onderdeel van de verbinding, wordt weergegeven.](../images/ui/audience-builder/selected-audiences.png)

## [!UICONTROL Rank] {#rank-block}

De **[!UICONTROL Rank]** met bloktype kunt u het publiek rangschikken en sorteren voordat het nieuwe publiek wordt gepubliceerd.

Als u een **[!UICONTROL Rank]** blok, selecteer **+** pictogram, gevolgd door **[!UICONTROL Rank]**.

![De optie Rank is geselecteerd.](../images/ui/audience-builder/add-rank-block.png)

Wanneer u het blok selecteert, worden de details over het rangschikken getoond in de juiste spoorstaaf, met inbegrip van het etiket van het blok, het attribuut aan rangschikking, de rangschikking, en een knevel om het aantal profielen te beperken tot rangschikking.

![De rank blok wordt gemarkeerd, evenals de details van de rank blok.](../images/ui/audience-builder/rank.png)

Als u wilt selecteren op welk kenmerk het publiek moet worden geplaatst, selecteert u de optie ![filter](../images/ui/audience-builder/filter-attribute.png) pictogram.

![Het filterpictogram wordt gemarkeerd en geeft aan wat u moet selecteren om het selectiescherm voor profielkenmerken te openen.](../images/ui/audience-builder/select-rank-attribute.png)

Er wordt een lijst met profielkenmerken weergegeven. Op deze popover, kunt u het attributentype selecteren u uw publiek door wilt rangschikken. Selecteren **[!UICONTROL Select]** om het aan uw rangschikkingsblok toe te voegen. Let op: het geselecteerde kenmerk kan **alleen** van het type `int`.

![Er wordt een lijst met kenmerken weergegeven.](../images/ui/audience-builder/select-attribute.png)

Na het selecteren van de attributen, kunt u de orde selecteren om het door te rangschikken. Dit gebeurt in oplopende (van laagste naar hoogste) of aflopende (van hoogste naar laagste) volgorde.

Bovendien, kunt u het aantal teruggekeerde publiek beperken door toe te laten **[!UICONTROL Add profile limit]** schakelen. Wanneer deze schakeloptie is ingeschakeld, kunt u het maximale aantal keren instellen dat binnen het **[!UICONTROL Included profiles]** veld.

![De schakeloptie voor het toevoegen van profiellimieten wordt gemarkeerd. Hiermee kunt u het aantal geretourneerde soorten publiek beperken.](../images/ui/audience-builder/add-profile-limit.png)

## [!UICONTROL Split] {#split-block}

De **[!UICONTROL Split]** met bloktype kunt u het nieuwe publiek opsplitsen in verschillende deelsoorten. U kunt dit publiek splitsen op basis van een percentage of op basis van een kenmerk.

Als u een **[!UICONTROL Split]** blok, selecteer **+** pictogram, gevolgd door **[!UICONTROL Split]**.

![De optie Splitsen is geselecteerd.](../images/ui/audience-builder/add-split-block.png)

### Splitsen op percentage {#split-percentage}

Bij het splitsen naar percentage worden de doelgroepen willekeurig gesplitst op basis van het aantal beschikbare paden en percentages.

U kunt bijvoorbeeld drie paden hebben, elk met een ander percentage profielen.

![De uitsplitsing in aantal opgeslagen soorten publiek en percentages wordt weergegeven.](../images/ui/audience-builder/percentages.png)

Bovendien, kunt u één van de gespleten publiek merken om de controlegroep te zijn.

![De knevel van de controlegroep wordt toegelaten. Hiermee kunt u een van de gesplitste doelgroepen markeren als een controlegroep.](../images/ui/audience-builder/control-group.png)

### Splitsen op kenmerk {#split-attribute}

Bij splitsen op kenmerk wordt het publiek gesplitst op basis van de opgegeven kenmerken. Selecteer het kenmerk waarop u wilt splitsen **[!UICONTROL Split]** blok, gevolgd door de ![filter](../images/ui/audience-builder/filter-attribute.png) pictogram.

![De filterknop wordt geselecteerd en geeft aan hoe u op kenmerk moet filteren.](../images/ui/audience-builder/select-attribute-split.png)

Er wordt een lijst met profielkenmerken weergegeven. Selecteer het kenmerktype, gevolgd door **[!UICONTROL Select]** om het toe te voegen aan uw gesplitste blok.

![Er wordt een lijst met kenmerken weergegeven.](../images/ui/audience-builder/select-attribute.png)

Nadat u het kenmerk hebt geselecteerd, kunt u kiezen tot welke profielen u wilt behoren door de waarden in het deelvenster **[!UICONTROL Values]** veld.

![De waarden waarop u de kenmerken wilt splitsen, worden toegevoegd.](../images/ui/audience-builder/attribute-split-values.png)

Daarnaast kunt u de opdracht **[!UICONTROL Other profiles]** Schakel deze optie in om een subpubliek te maken dat uit alle niet-geselecteerde profielen bestaat.

![De schakeloptie Andere profielen wordt gemarkeerd.](../images/ui/audience-builder/attribute-split-other-profiles.png)

## Uw publiek publiceren

Nadat u de doelgroep hebt samengesteld, kunt u deze opslaan en publiceren door **[!UICONTROL Publish]**.

![De knop Publiceren is gemarkeerd en geeft aan hoe u uw publiek kunt opslaan en publiceren.](../images/ui/audience-builder/publish-audience.png)

Als er fouten optreden bij het maken van het publiek, verschijnt er een waarschuwing met de informatie over het oplossen van het probleem.

![De knop Publiceren is gemarkeerd en geeft aan hoe u uw publiek kunt opslaan en publiceren.](../images/ui/audience-builder/audience-alert.png)

## Volgende stappen

De Audience Builder biedt een rijke workflow waarmee u een publiek kunt maken van de verschillende bloktypen. Meer over andere delen van de Dienst UI van de Segmentatie leren, gelieve te lezen [Gebruikershandleiding voor segmentatieservice](./overview.md).