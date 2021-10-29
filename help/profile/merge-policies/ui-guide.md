---
keywords: Experience Platform;profiel;realtime klantprofiel;samenvoegbeleid;UI;gebruikersinterface;geordende tijdstempel;prioriteit gegevensset
title: UI-gids voor samenvoegingsbeleid
type: Documentation
description: Wanneer het brengen van gegevens uit veelvoudige bronnen samen in Experience Platform, is het fusiebeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om de verenigde mening tot stand te brengen. Deze handleiding bevat stapsgewijze instructies voor het werken met samenvoegbeleidsregels via de Adobe Experience Platform-gebruikersinterface.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: e0a75a75e5dbb0318ec8785d887d7a156d28f5bd
workflow-type: tm+mt
source-wordcount: '2191'
ht-degree: 0%

---


# UI-gids voor samenvoegen

Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Bij het samenvoegen van deze gegevens gelden als samenvoegbeleid de regels die [!DNL Platform] gebruikt om te bepalen hoe aan gegevens voorrang zal worden gegeven en welke gegevens zullen worden gecombineerd om de verenigde mening tot stand te brengen.

Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Deze handleiding bevat stapsgewijze instructies voor het werken met samenvoegbeleidsregels via de gebruikersinterface van Adobe Experience Platform (UI).

Als u meer wilt weten over samenvoegingsbeleid en deze rol binnen het Experience Platform, leest u eerst de [overzicht van samenvoegbeleid](overview.md).

## Aan de slag

Deze gids vereist een goed begrip van verscheidene belangrijke [!DNL Experience Platform] functies. Lees de documentatie voor de volgende services voordat u deze handleiding volgt:

* [Klantprofiel in realtime](../home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Laat het Profiel van de Klant in real time toe door identiteiten van verschillende gegevensbronnen te overbruggen die in worden opgenomen [!DNL Platform].
* [Experience Data Model (XDM)](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Platform] organiseert de gegevens van de klantenervaring.

## Samenvoegbeleid weergeven {#view-merge-policies}

Binnen de [!DNL Experience Platform] UI, kunt u beginnen werkend met samenvoegbeleid door te selecteren **[!UICONTROL Profiles]** in de linkernavigatie en selecteer vervolgens de **[!UICONTROL Merge Policies]** tab. Dit lusje omvat een lijst van al bestaand samenvoegingsbeleid voor uw organisatie, evenals details voor elk fusiebeleid met inbegrip van de beleidsnaam, al dan niet het fusiebeleid het standaardfusiebeleid is, en de schemaklasse waarop het fusiebeleid betrekking heeft.

![Landingspagina van beleid samenvoegen](../images/merge-policies/landing.png)

Als u wilt selecteren welke details zichtbaar zijn of extra kolommen aan de weergave wilt toevoegen, selecteert u **[!UICONTROL Configure columns]** en klik op een kolomnaam om deze toe te voegen aan of te verwijderen uit de weergave.

![](../images/merge-policies/adjust-view.png)

## Samenvoegbeleid maken {#create-a-merge-policy}

Als u een nieuw samenvoegbeleid wilt maken, selecteert u **[!UICONTROL Create merge policy]** op het tabblad Samenvoegbeleid om de nieuwe werkstroom voor samenvoegbeleid in te voeren.

![Het beleid van de fusie landende pagina met de Create benadrukte knoop.](../images/merge-policies/create-new.png)

De **[!UICONTROL New merge policy]** vereist dat u belangrijke informatie voor het nieuwe samenvoegbeleid opgeeft via een reeks instructies. Deze stappen worden beschreven in de volgende secties.

![De nieuwe werkstroom voor samenvoegbeleid.](../images/merge-policies/create.png)

## [!UICONTROL Configure] {#configure}

De eerste stap in het werkschema staat u toe om uw samenvoegbeleid te vormen door basisinformatie te verstrekken. Deze informatie omvat:

* **[!UICONTROL Name]**: De naam van uw samenvoegingsbeleid moet beschrijvend maar beknopt zijn.
* **[!UICONTROL Schema class]**: De XDM-schemaklasse die aan het samenvoegbeleid is gekoppeld. This specifies the schema class for which this merge policy is created. Organisaties kunnen meerdere samenvoegbeleidsregels per schemaklasse maken. Alleen de [!UICONTROL XDM Individual Profile] is beschikbaar in de UI. U kunt een voorbeeld van het samenvoegingsschema voor de schemaklasse bekijken door te selecteren **[!UICONTROL View Union Schema]**. Zie de sectie over [weergeven, verenigingsschema](#view-union-schema) dat volgt .
* **[!UICONTROL ID stitching]**: In dit veld wordt gedefinieerd hoe de verwante identiteiten van een klant worden bepaald. Er zijn twee mogelijke waarden voor identiteitsstitching, en het is belangrijk om te begrijpen hoe het type van identiteitsstitching dat u selecteert uw gegevens zal beïnvloeden. Voor meer informatie raadpleegt u de [overzicht van samenvoegbeleid](overview.md).
   * **[!UICONTROL None]**: Geen identiteitsstitching uitvoeren.
   * **[!UICONTROL Private Graph]**: Identiteitsstitching uitvoeren op basis van uw persoonlijke identiteitsgrafiek.
* **[!UICONTROL Default merge policy]**: Een schakelknop waarmee u kunt bepalen of dit samenvoegbeleid al dan niet de standaardinstelling voor uw organisatie is. Als de kiezer is ingeschakeld, wordt een waarschuwing weergegeven met de vraag of u het standaardsamenvoegbeleid van uw organisatie wilt wijzigen. Zie de [overzicht van samenvoegbeleid](overview.md) voor meer informatie over standaardbeleid voor samenvoegen.
   ![](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Active-On-Edge Merge Policy]**: Een schakelknop waarmee u kunt bepalen of dit samenvoegbeleid aan de rand actief is. Om ervoor te zorgen dat alle profielgebruikers met dezelfde weergave aan de randen werken, kan het samenvoegbeleid als actief aan de rand worden gemarkeerd. Als u wilt dat een segment aan de rand wordt geactiveerd (gemarkeerd als een randsegment), moet het segment zijn gekoppeld aan een samenvoegingsbeleid dat is gemarkeerd als actief aan de rand. Als een segment **niet** gekoppeld aan een samenvoegbeleid dat aan de rand is gemarkeerd als actief, wordt het segment niet gemarkeerd als actief aan de rand en wordt het gemarkeerd als een streaming segment. Bovendien kan elke IMS-organisatie alleen **één** samenvoegbeleid dat op rand actief is.

Nadat de vereiste velden zijn voltooid, kunt u **[!UICONTROL Next]** om door te gaan met de workflow.

![Een volledig Configure scherm met de Volgende benadrukte knoop.](../images/merge-policies/create-complete.png)

## [!UICONTROL View Union Schema] {#view-union-schema}

Wanneer u een samenvoegbeleid maakt of bewerkt, kunt u het samenvoegingsschema voor de gekozen schema-klasse bekijken door **[!UICONTROL View Union Schema]**.

![](../images/merge-policies/view-union-schema.png)

Hierdoor wordt het [!UICONTROL View Union Schema] dialoog, die alle bijdragende schema&#39;s, identiteiten, en verhoudingen toont verbonden aan het unieschema. U kunt de dialoog gebruiken om het verenigingsschema te onderzoeken op de zelfde manier u door tot [!UICONTROL Union Schema] in de [!UICONTROL Profiles] van de gebruikersinterface van het Platform.

Voor gedetailleerde informatie over unieschema&#39;s, met inbegrip van hoe met hen in interactie te staan in [!UICONTROL Union Schema] of de [!UICONTROL View Union Schema] in de workflow voor het samenvoegen van beleidsregels. Ga naar [UI-hulplijn verenigingsschema](../ui/union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Select Profile datasets] {#select-profile-datasets}

Op de **[!UICONTROL Select Profile datasets]** scherm, moet u selecteren **[!UICONTROL Merge method]** die u wilt gebruiken voor het samenvoegbeleid. Ook weergegeven op het scherm is het totale aantal [!UICONTROL Profile datasets] in uw organisatie die betrekking hebben op de schemaklasse die op het vorige scherm werd geselecteerd.

Afhankelijk van de samenvoegmethode die u kiest, zullen alle datasets van het Profiel door de orde worden samengevoegd waarin zij (timestamp bevolen) laatst werden bijgewerkt of u zult moeten selecteren welke datasets van het Profiel in het fusiebeleid en de orde omvatten waarin om hen (datasetbelangrijkheid) samen te voegen.

Raadpleeg voor meer informatie over samenvoegmethoden de [overzicht van samenvoegbeleid](overview.md).

### Tijdstempel geordend {#timestamp-ordered-profile}

Selecteren **[!UICONTROL Timestamp ordered]** aangezien de fusiemethode betekent dat de attributen van de onlangs bijgewerkte datasets belangrijkheid zullen nemen. Dit geldt voor alle profielgegevenssets.

>[!NOTE]
>
>Het getal tussen haakjes naast **[!UICONTROL Profile datasets]** (bijvoorbeeld `(37)` in het getoonde beeld) toont het totale aantal profieldatasets die zullen worden omvat.

![](../images/merge-policies/timestamp-ordered.png)

### Dataset-prioriteit {#dataset-precedence-profile}

Selecteren **[!UICONTROL Dataset precedence]** aangezien de fusiemethode vereist u om de datasets van het Profiel te selecteren en hen manueel voorrang te geven. Elke vermelde dataset omvat ook de status van de laatste partij die wordt opgenomen of toont een bericht dat geen partijen in die dataset zijn opgenomen.

U kunt tot 50 datasets van de datasetlijst selecteren om in het fusiebeleid te omvatten.

>[!NOTE]
>
>Het getal tussen haakjes naast **[!UICONTROL Profile datasets]** (bijvoorbeeld `(37)` in de getoonde afbeelding) toont het totale aantal profielgegevenssets dat beschikbaar is voor selectie.

Aangezien de datasets worden geselecteerd, worden zij toegevoegd aan **[!UICONTROL Select datasets]** sectie, die u toestaat om de datasets te slepen en te laten vallen en hen volgens uw gewenste belangrijkheid te ordenen. Aangezien de datasets in de lijst worden aangepast, zal rangschikken (1, 2, 3, enz.) naast de dataset bijwerken, tonend prioriteit (1 die de hoogste prioriteit wordt gegeven, dan 2, en verder).

Als u een gegevensset selecteert, worden ook de **[!UICONTROL Union schema]** sectie, die de gebieden in het unieschema tonen waaraan elke dataset gegevens bijdraagt. Voor meer informatie over unieschema&#39;s, zoals hoe te met de visualisaties in UI in wisselwerking te staan, gelieve te verwijzen naar [UI-hulplijn verenigingsschema](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL Select ExperienceEvent datasets] {#select-experienceevent-datasets}

De volgende stap in het werkschema vereist u om datasets te selecteren ExperienceEvent. Dit scherm wordt beïnvloed door de samenvoegmethode die u op het [[!UICONTROL Select Profile datasets]](#select-profile-datasets) scherm.

### Tijdstempel geordend {#timestamp-ordered-experienceevent}

Als u **[!UICONTROL Timestamp ordered]** als de fusiemethode voor de datasets van het Profiel, zullen de attributen van de onlangs bijgewerkte datasets ExperienceEvent ook hier belangrijkheid nemen.

>[!NOTE]
>
>Het getal tussen haakjes naast **[!UICONTROL ExperienceEvent datasets]** (bijvoorbeeld `(20)` in het getoonde beeld) toont het totale aantal datasets ExperienceEvent die door uw organisatie worden gecreeerd die op de schemaklasse betrekking hebben die u op het scherm van de de configuratieconfiguratie van het samenvoegingsbeleid selecteerde.

![](../images/merge-policies/timestamp-experienceevent.png)

### Dataset-prioriteit {#dataset-precedence-experienceevent}

Als u **[!UICONTROL Dataset precedence]** als de fusiemethode voor de datasets van het Profiel, zult u moeten selecteren ExperienceEvent datasets om te omvatten. U kunt tot 50 datasets ExperienceEvent van de datasetlijst selecteren.

>[!NOTE]
>
>Het getal tussen haakjes naast **[!UICONTROL ExperienceEvent datasets]** (bijvoorbeeld `(20)` in het getoonde beeld) toont het totale aantal datasets ExperienceEvent die door uw organisatie worden gecreeerd die op de schemaklasse betrekking hebben die u op het scherm van de de configuratieconfiguratie van het samenvoegingsbeleid selecteerde.

Als datasets zijn geselecteerd, worden deze weergegeven in de [!UICONTROL Select datasets] sectie.

De datasets van ExperienceEvent kunnen niet manueel worden bevolen, in plaats daarvan worden de attributen in de datasets ExperienceEvent toegevoegd aan de datasets van het Profiel als zij deel van het zelfde profielfragment uitmaken.

Net als bij het selecteren van profielgegevenssets wordt door het selecteren van een ExperienceEvent-gegevensset ook het dialoogvenster **[!UICONTROL Union schema]** sectie, die de gebieden in het unieschema tonen waaraan elke dataset gegevens bijdraagt. Voor meer informatie over unieschema&#39;s, zoals hoe te met de visualisaties in UI in wisselwerking te staan, gelieve te verwijzen naar [UI-hulplijn verenigingsschema](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL Review] {#review}

De laatste stap in de workflow is het controleren van het samenvoegbeleid. De **[!UICONTROL Review]** het scherm toont informatie over uw samenvoegbeleid, met inbegrip van de identiteitskaart die methode stitching selecteerde, geselecteerde fusiemethode, en de datasets inbegrepen. (Als u alle meegeleverde profiel- of ExperienceEvent-gegevenssets wilt weergeven, selecteert u het aantal gegevenssets waarmee u de vervolgkeuzelijst wilt uitvouwen.)

Wordt ook op het revisiescherm weergegeven: **[!UICONTROL Preview data]** tabel met voorbeeldprofielrecords die uw samenvoegbeleid gebruiken. Zo kunt u een voorvertoning weergeven van een klantprofiel voordat u het samenvoegbeleid opslaat.

Controleer of u de configuratie van het samenvoegbeleid en de voorbeeldgegevens zorgvuldig controleert voordat u selecteert **[!UICONTROL Finish]** om de aanmaakworkflow te voltooien.

### Tijdstempel geordend {#timestamp-ordered-review}

Als u **[!UICONTROL Timestamp ordered]** als fusiemethode voor uw samenvoegingsbeleid, omvat de lijst van de datasets van het Profiel alle datasets die door uw organisatie met betrekking tot de schemaklasse, in volgorde van timestamp zijn gecreeerd. De lijst van datasets ExperienceEvent omvat alle datasets die uw organisatie voor de gekozen schemaklasse heeft gecreeerd en aan de datasets van het Profiel zal worden toegevoegd.

De **[!UICONTROL Preview data]** de lijst toont de verslagen van het steekproefprofiel die op een timestamp opdracht geven tot van de datasets worden gebaseerd. Zo kunt u een voorvertoning weergeven van een klantprofiel voordat u het samenvoegbeleid opslaat.

![](../images/merge-policies/timestamp-review.png)

### Dataset-prioriteit {#dataset-precedence-review}

Als u **[!UICONTROL Dataset precedence]** als samenvoegmethode voor uw samenvoegbeleid, omvatten de lijsten van Profiel en de datasets ExperienceEvent slechts de datasets van het Profiel en van de ExperienceEvent die u tijdens het creatiewerkschema selecteerde, respectievelijk. De orde van de datasets van het Profiel zou de belangrijkheid moeten aanpassen die u tijdens verwezenlijking specificeerde. Als dat niet het geval is, gebruikt u de [!UICONTROL Back] om terug te keren naar de vorige workflowstappen en de prioriteit aan te passen.

De **[!UICONTROL Preview data]** de lijst toont de verslagen van het steekproefprofiel gebruikend de geselecteerde datasets. Zo kunt u een voorvertoning weergeven van een klantprofiel voordat u het samenvoegbeleid opslaat.

![](../images/merge-policies/dataset-precedence-review.png)

### Bijgewerkte lijst van samenvoegingsbeleid {#updated-list}

Nadat u de workflow hebt voltooid om een nieuw samenvoegbeleid te maken, gaat u terug naar de map **[!UICONTROL Merge Policies]** tab. De lijst met samenvoegingsbeleid voor uw organisatie moet nu het samenvoegbeleid bevatten dat u zojuist hebt gemaakt.

![](../images/merge-policies/new-merge-policy-created.png)

## Een samenvoegingsbeleid bewerken

Van de [!UICONTROL Merge Policies] kunt u een bestaand samenvoegbeleid wijzigen dat is gemaakt voor de [!DNL XDM Individual Profile] door de **[!UICONTROL Policy name]** voor het samenvoegbeleid dat u wilt bewerken.

![Landingspagina van beleid samenvoegen](../images/merge-policies/select-edit.png)

Wanneer de **[!UICONTROL Edit merge policy]** wordt weergegeven, kunt u de naam wijzigen en [!UICONTROL ID stitching] methode, evenals verandering al dan niet dit beleid het standaardfusiebeleid voor uw organisatie is.

Selecteren **[!UICONTROL Next]** om door het werkschema van het fusiebeleid verder te gaan om de fusiemethode en datasets inbegrepen in het fusiebeleid bij te werken.

![](../images/merge-policies/edit-screen.png)

Nadat u de benodigde wijzigingen hebt aangebracht, controleert u het samenvoegbeleid en selecteert u **[!UICONTROL Finish]** om uw wijzigingen op te slaan en terug te keren naar de [!UICONTROL Merge policies] tab.

>[!WARNING]
>
>Het wijzigen van een samenvoegbeleid kan invloed hebben op segmentatie en profielresultaten, omdat dit de manier wijzigt waarop gegevensconflicten worden opgelost. Controleer de wijzigingen in het samenvoegbeleid zorgvuldig voordat u ze opslaat.

![](../images/merge-policies/edit-review.png)

## Schendingen van het beleid inzake gegevensbeheer

Wanneer het creëren van of het bijwerken van een samenvoegbeleid, wordt een controle uitgevoerd om te bepalen als het fusiebeleid om het even welk beleid van het gegevensgebruik schendt dat door uw organisatie wordt bepaald. Beleid voor gegevensgebruik maakt deel uit van Adobe Experience Platform [!DNL Data Governance] en zijn regels die het soort marketingacties beschrijven dat u mag uitvoeren op of mag uitvoeren op specifieke [!DNL Platform] gegevens. Bijvoorbeeld, als een samenvoegbeleid werd gebruikt om een segment tot stand te brengen dat aan een derdebestemming activeerde, en uw organisatie een beleid van het gegevensgebruik had dat de uitvoer van specifieke gegevens naar derden verhindert, zou u een **[!UICONTROL Data governance policy violation detected]** melding wanneer wordt geprobeerd uw samenvoegbeleid op te slaan.

Deze melding bevat een lijst met beleidsregels voor gegevensgebruik die zijn overtreden. U kunt de details van de schending bekijken door een beleid in de lijst te selecteren. Bij het selecteren van een overtreden beleid, **[!UICONTROL Data lineage]** bevat de reden voor de schending en de betrokken activering, die elk meer details verstrekken over hoe het beleid van het gegevensgebruik is overtreden.

Als u meer wilt weten over de manier waarop gegevensbeheer in Adobe Experience Platform wordt uitgevoerd, leest u eerst de [Overzicht van gegevensbeheer](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Volgende stappen

Nu u en gevormd samenvoegbeleid voor uw organisatie hebt gecreeerd, kunt u hen gebruiken om de mening van klantenprofielen binnen Platform aan te passen en publiekssegmenten van uw gegevens van het Profiel tot stand te brengen. Zie de [segmentatieoverzicht](../../segmentation/home.md) voor meer informatie over het maken van segmenten en het werken met segmenten gebruikt u de opdracht [!DNL Experience Platform] UI en API&#39;s.
