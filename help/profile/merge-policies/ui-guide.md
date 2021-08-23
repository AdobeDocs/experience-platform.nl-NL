---
keywords: Experience Platform;profiel;realtime klantprofiel;samenvoegbeleid;UI;gebruikersinterface;geordende tijdstempel;prioriteit gegevensset
title: UI-gids voor samenvoegingsbeleid
type: Documentation
description: Wanneer het brengen van gegevens uit veelvoudige bronnen samen in Experience Platform, is het fusiebeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om de verenigde mening tot stand te brengen. Deze handleiding bevat stapsgewijze instructies voor het werken met samenvoegbeleidsregels via de Adobe Experience Platform-gebruikersinterface.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: a6a49b4cf9c89b5c6b4679f36daede93590ffb3c
workflow-type: tm+mt
source-wordcount: '2070'
ht-degree: 0%

---


# UI-gids voor samenvoegen

Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Wanneer het brengen van deze gegevens samen, zijn het fusiebeleid de regels die [!DNL Platform] gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om de verenigde mening tot stand te brengen.

Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Deze handleiding bevat stapsgewijze instructies voor het werken met samenvoegbeleidsregels via de gebruikersinterface van Adobe Experience Platform (UI).

Als u meer wilt weten over samenvoegingsbeleid en hun rol binnen het Experience Platform, begint u met het lezen van het [overzicht van het samenvoegbeleid](overview.md).

## Aan de slag

Deze gids vereist een werkend inzicht van verscheidene belangrijke [!DNL Experience Platform] eigenschappen. Lees de documentatie voor de volgende services voordat u deze handleiding volgt:

* [Klantprofiel](../home.md) in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Laat het Profiel van de Klant in real time toe door identiteiten van ongelijke gegevensbronnen te overbruggen die in worden opgenomen  [!DNL Platform].
* [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Platform] klantenervaring worden georganiseerd.

## Samenvoegbeleid weergeven {#view-merge-policies}

Binnen [!DNL Experience Platform] UI, kunt u beginnen werkend met fusiebeleid door **[!UICONTROL Profiles]** in de linkernavigatie te selecteren en dan **[!UICONTROL Merge Policies]** tabel te selecteren. Dit lusje omvat een lijst van al bestaand samenvoegingsbeleid voor uw organisatie, evenals details voor elk fusiebeleid met inbegrip van de beleidsnaam, al dan niet het fusiebeleid het standaardfusiebeleid is, en de schemaklasse waarop het fusiebeleid betrekking heeft.

![Landingspagina van beleid samenvoegen](../images/merge-policies/landing.png)

Als u wilt selecteren welke details zichtbaar zijn of extra kolommen aan de weergave wilt toevoegen, selecteert u **[!UICONTROL Configure columns]** en klikt u op een kolomnaam om deze toe te voegen aan of te verwijderen uit de weergave.

![](../images/merge-policies/adjust-view.png)

## Samenvoegbeleid maken {#create-a-merge-policy}

Als u een nieuw samenvoegbeleid wilt maken, selecteert u **[!UICONTROL Create merge policy]** op het tabblad Samenvoegbeleid om de nieuwe werkstroom voor samenvoegingsbeleid in te voeren.

![Het beleid van de fusie landende pagina met de Create benadrukte knoop.](../images/merge-policies/create-new.png)

Voor de **[!UICONTROL New merge policy]**-workflow moet u belangrijke informatie voor het nieuwe samenvoegbeleid opgeven via een reeks stappen met instructies. Deze stappen worden beschreven in de volgende secties.

![De nieuwe werkstroom voor samenvoegbeleid.](../images/merge-policies/create.png)

## [!UICONTROL Configure] {#configure}

De eerste stap in het werkschema staat u toe om uw samenvoegbeleid te vormen door basisinformatie te verstrekken. Deze informatie omvat:

* **[!UICONTROL Name]**: De naam van uw samenvoegingsbeleid moet beschrijvend maar beknopt zijn.
* **[!UICONTROL Schema class]**: De XDM-schemaklasse die aan het samenvoegbeleid is gekoppeld. This specifies the schema class for which this merge policy is created. Organisaties kunnen meerdere samenvoegbeleidsregels per schemaklasse maken. Momenteel is alleen de klasse [!UICONTROL XDM Individual Profile] beschikbaar in de gebruikersinterface. U kunt een voorbeeld van het samenvoegingsschema voor de schemaklasse bekijken door **[!UICONTROL View Union Schema]** te selecteren. Voor meer informatie, zie de sectie over [het bekijken van verenigingsschema](#view-union-schema) die volgt.
* **[!UICONTROL ID stitching]**: In dit veld wordt gedefinieerd hoe de verwante identiteiten van een klant worden bepaald. Er zijn twee mogelijke waarden voor identiteitsstitching, en het is belangrijk om te begrijpen hoe het type van identiteitsstitching dat u selecteert uw gegevens zal beïnvloeden. Voor meer informatie raadpleegt u het [overzicht van het samenvoegbeleid](overview.md).
   * **[!UICONTROL None]**: Geen identiteitsstitching uitvoeren.
   * **[!UICONTROL Private Graph]**: Identiteitsstitching uitvoeren op basis van uw persoonlijke identiteitsgrafiek.
* **[!UICONTROL Default merge policy]**: Een schakelknop waarmee u kunt bepalen of dit samenvoegbeleid al dan niet de standaardinstelling voor uw organisatie is. Als de kiezer is ingeschakeld, wordt een waarschuwing weergegeven met de vraag of u het standaardsamenvoegbeleid van uw organisatie wilt wijzigen. Zie [overzicht van samenvoegingsbeleid](overview.md) om meer over standaardsamenvoegbeleid te leren.
   ![](../images/merge-policies/create-make-default.png)

Nadat de vereiste velden zijn voltooid, kunt u **[!UICONTROL Next]** selecteren om door te gaan met de workflow.

![Een volledig Configure scherm met de Volgende benadrukte knoop.](../images/merge-policies/create-complete.png)

## [!UICONTROL View Union Schema] {#view-union-schema}

Wanneer u een samenvoegbeleid maakt of bewerkt, kunt u het samenvoegingsschema voor de gekozen schema-klasse weergeven door **[!UICONTROL View Union Schema]** te selecteren.

![](../images/merge-policies/view-union-schema.png)

Dit opent de [!UICONTROL View Union Schema] dialoog, die alle bijdragende schema&#39;s, identiteiten, en verhoudingen verbonden aan het unieschema toont. U kunt de dialoog gebruiken om het verenigingsschema te onderzoeken op de zelfde manier dat u door tot het [!UICONTROL Union Schema] lusje in [!UICONTROL Profiles] sectie van het Platform UI toegang te hebben.

Voor gedetailleerde informatie over unieschema&#39;s, met inbegrip van hoe te met hen in het [!UICONTROL Union Schema] lusje of [!UICONTROL View Union Schema] dialoog in het werkschema van het fusiebeleid wordt getoond, te bezoeken gelieve [de gids UI van het unieschema](../ui/union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Select Profile datasets] {#select-profile-datasets}

Op het **[!UICONTROL Select Profile datasets]** scherm, moet u **[!UICONTROL Merge method]** selecteren die u voor uw fusiebeleid wenst te gebruiken. Ook weergegeven op het scherm is het totale aantal [!UICONTROL Profile datasets] in uw organisatie dat betrekking heeft op de schemaklasse die is geselecteerd op het vorige scherm.

Afhankelijk van de samenvoegmethode die u kiest, zullen alle datasets van het Profiel door de orde worden samengevoegd waarin zij (timestamp bevolen) laatst werden bijgewerkt of u zult moeten selecteren welke datasets van het Profiel in het fusiebeleid en de orde omvatten waarin om hen (datasetbelangrijkheid) samen te voegen.

Voor meer informatie over fusiemethodes, gelieve te verwijzen naar [overzicht van fusiebeleid](overview.md).

### Tijdstempel geordend {#timestamp-ordered-profile}

Als u **[!UICONTROL Timestamp ordered]** selecteert als samenvoegmethode, hebben kenmerken van de meest recente bijgewerkte datasets voorrang. Dit geldt voor alle profielgegevenssets.

>[!NOTE]
>
>Het getal tussen haakjes naast **[!UICONTROL Profile datasets]** (bijvoorbeeld `(37)` in de getoonde afbeelding) geeft het totale aantal profielgegevenssets weer dat wordt opgenomen.

![](../images/merge-policies/timestamp-ordered.png)

### Dataset-prioriteit {#dataset-precedence-profile}

Als u **[!UICONTROL Dataset precedence]** selecteert als samenvoegmethode, moet u de gegevenssets Profiel selecteren en handmatig voorrang geven aan de gegevenssets. Elke vermelde dataset omvat ook de status van de laatste partij die wordt opgenomen of toont een bericht dat geen partijen in die dataset zijn opgenomen.

U kunt tot 50 datasets van de datasetlijst selecteren om in het fusiebeleid te omvatten.

>[!NOTE]
>
>Het aantal tussen haakjes naast **[!UICONTROL Profile datasets]** (bijvoorbeeld `(37)` in de getoonde afbeelding) toont het totale aantal profieldatasets beschikbaar voor selectie.

Aangezien datasets worden geselecteerd, worden zij toegevoegd aan **[!UICONTROL Select datasets]** sectie, die u toestaat om de datasets te slepen en te laten vallen en hen volgens uw gewenste belangrijkheid te plaatsen. Aangezien de datasets in de lijst worden aangepast, zal rangschikken (1, 2, 3, enz.) naast de dataset bijwerken, tonend prioriteit (1 die de hoogste prioriteit wordt gegeven, dan 2, en verder).

Als u een gegevensset selecteert, wordt ook de sectie **[!UICONTROL Union schema]** bijgewerkt en worden de velden in het samenvoegingsschema weergegeven waaraan elke gegevensset gegevens bijdraagt. Voor meer informatie over verenigingsschema&#39;s, met inbegrip van hoe te met de visualisaties in UI in wisselwerking te staan, gelieve te verwijzen [verenigingsschema UI gids](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL Select ExperienceEvent datasets] {#select-experienceevent-datasets}

De volgende stap in het werkschema vereist u om datasets te selecteren ExperienceEvent. Dit scherm wordt beïnvloed door de fusiemethode die u op het [[!UICONTROL Select Profile datasets]](#select-profile-datasets) scherm selecteerde.

### Tijdstempel geordend {#timestamp-ordered-experienceevent}

Als u **[!UICONTROL Timestamp ordered]** als fusiemethode voor de datasets van het Profiel selecteerde, zullen de attributen van de onlangs bijgewerkte datasets ExperienceEvent ook hier belangrijkheid nemen.

>[!NOTE]
>
>Het aantal tussen haakjes naast **[!UICONTROL ExperienceEvent datasets]** (bijvoorbeeld, `(20)` in het getoonde beeld) toont het totale aantal datasets ExperienceEvent die door uw organisatie worden gecreeerd die op de schemaklasse betrekking hebben die u op het scherm van de de configuratieconfiguratie van het fusiebeleid selecteerde.

![](../images/merge-policies/timestamp-experienceevent.png)

### Dataset-prioriteit {#dataset-precedence-experienceevent}

Als u **[!UICONTROL Dataset precedence]** als fusiemethode voor de datasets van het Profiel selecteerde, zult u de datasets moeten selecteren ExperienceEvent om te omvatten. U kunt tot 50 datasets ExperienceEvent van de datasetlijst selecteren.

>[!NOTE]
>
>Het aantal tussen haakjes naast **[!UICONTROL ExperienceEvent datasets]** (bijvoorbeeld, `(20)` in het getoonde beeld) toont het totale aantal datasets ExperienceEvent die door uw organisatie worden gecreeerd die op de schemaklasse betrekking hebben die u op het scherm van de de configuratieconfiguratie van het fusiebeleid selecteerde.

Aangezien datasets worden geselecteerd, verschijnen zij in [!UICONTROL Select datasets] sectie.

De datasets van ExperienceEvent kunnen niet manueel worden bevolen, in plaats daarvan worden de attributen in de datasets ExperienceEvent toegevoegd aan de datasets van het Profiel als zij deel van het zelfde profielfragment uitmaken.

Vergelijkbaar met het selecteren van de datasets van het Profiel, werkt het selecteren van een dataset ExperienceEvent ook de **[!UICONTROL Union schema]** sectie bij, die de gebieden in het unieschema toont waaraan elke dataset gegevens bijdraagt. Voor meer informatie over verenigingsschema&#39;s, met inbegrip van hoe te met de visualisaties in UI in wisselwerking te staan, gelieve te verwijzen [verenigingsschema UI gids](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL Review] {#review}

De laatste stap in de workflow is het controleren van het samenvoegbeleid. Het **[!UICONTROL Review]** scherm toont informatie over uw samenvoegbeleid, met inbegrip van geselecteerde identiteitskaart het stitching methode, geselecteerde fusiemethode, en de datasets inbegrepen. (Als u alle meegeleverde profiel- of ExperienceEvent-gegevenssets wilt weergeven, selecteert u het aantal gegevenssets waarmee u de vervolgkeuzelijst wilt uitvouwen.)

Ook inbegrepen op het overzichtsscherm is de **[!UICONTROL Preview data]** lijst die de verslagen van het steekproefprofiel toont gebruikend uw samenvoegbeleid. Zo kunt u een voorvertoning weergeven van een klantprofiel voordat u het samenvoegbeleid opslaat.

Controleer of u de configuratie van het samenvoegbeleid en de voorbeeldgegevens zorgvuldig controleert voordat u **[!UICONTROL Finish]** selecteert om de aanmaakworkflow te voltooien.

### Tijdstempel geordend {#timestamp-ordered-review}

Als u **[!UICONTROL Timestamp ordered]** als fusiemethode voor uw samenvoegbeleid selecteerde, omvat de lijst van de datasets van het Profiel alle datasets die door uw organisatie met betrekking tot de schemacategorie, in volgorde van timestamp zijn gecreeerd. De lijst van datasets ExperienceEvent omvat alle datasets die uw organisatie voor de gekozen schemaklasse heeft gecreeerd en aan de datasets van het Profiel zal worden toegevoegd.

In de tabel **[!UICONTROL Preview data]** worden voorbeeldprofielrecords weergegeven die zijn gebaseerd op een tijdstempelvolgorde van de gegevenssets. Zo kunt u een voorvertoning weergeven van een klantprofiel voordat u het samenvoegbeleid opslaat.

![](../images/merge-policies/timestamp-review.png)

### Dataset-prioriteit {#dataset-precedence-review}

Als u **[!UICONTROL Dataset precedence]** als fusiemethode voor uw samenvoegbeleid selecteerde, omvatten de lijsten van Profiel en datasets ExperienceEvent slechts de datasets van het Profiel en van de ExperienceEvent die u tijdens het creatiewerkschema selecteerde, respectievelijk. De orde van de datasets van het Profiel zou de belangrijkheid moeten aanpassen die u tijdens verwezenlijking specificeerde. Als dit niet het geval is, gebruikt u de knop [!UICONTROL Back] om terug te keren naar de vorige workflowstappen en de prioriteit aan te passen.

In de tabel **[!UICONTROL Preview data]** worden voorbeeldprofielrecords weergegeven die de geselecteerde datasets gebruiken. Zo kunt u een voorvertoning weergeven van een klantprofiel voordat u het samenvoegbeleid opslaat.

![](../images/merge-policies/dataset-precedence-review.png)

### Bijgewerkte lijst van samenvoegingsbeleid {#updated-list}

Nadat u de workflow hebt voltooid om een nieuw samenvoegbeleid te maken, gaat u terug naar het tabblad **[!UICONTROL Merge Policies]**. De lijst met samenvoegingsbeleid voor uw organisatie moet nu het samenvoegbeleid bevatten dat u zojuist hebt gemaakt.

![](../images/merge-policies/new-merge-policy-created.png)

## Een samenvoegingsbeleid bewerken

Vanuit het tabblad [!UICONTROL Merge Policies] kunt u een bestaand samenvoegbeleid wijzigen dat voor de klasse [!DNL XDM Individual Profile] is gemaakt door **[!UICONTROL Policy name]** te selecteren voor het samenvoegbeleid dat u wilt bewerken.

![Landingspagina van beleid samenvoegen](../images/merge-policies/select-edit.png)

Wanneer het **[!UICONTROL Edit merge policy]** scherm verschijnt, kunt u veranderingen in de naam en [!UICONTROL ID stitching] methode aanbrengen, evenals veranderen of dit beleid al dan niet het standaardfusiebeleid voor uw organisatie is.

Selecteer **[!UICONTROL Next]** om door het werkschema van het fusiebeleid verder te gaan om de fusiemethode en datasets inbegrepen in het fusiebeleid bij te werken.

![](../images/merge-policies/edit-screen.png)

Nadat u de benodigde wijzigingen hebt aangebracht, controleert u het samenvoegbeleid en selecteert u **[!UICONTROL Finish]** om de wijzigingen op te slaan en terug te keren naar het tabblad [!UICONTROL Merge policies].

>[!WARNING]
>
>Het wijzigen van een samenvoegbeleid kan invloed hebben op segmentatie en profielresultaten, omdat dit de manier wijzigt waarop gegevensconflicten worden opgelost. Controleer de wijzigingen in het samenvoegbeleid zorgvuldig voordat u ze opslaat.

![](../images/merge-policies/edit-review.png)

## Schendingen van het beleid inzake gegevensbeheer

Wanneer het creëren van of het bijwerken van een samenvoegbeleid, wordt een controle uitgevoerd om te bepalen als het fusiebeleid om het even welk beleid van het gegevensgebruik schendt dat door uw organisatie wordt bepaald. Het beleid voor gegevensgebruik maakt deel uit van Adobe Experience Platform [!DNL Data Governance] en is een regel die het soort marketingacties beschrijft dat u mag uitvoeren of waarvan u een beperking hebt opgelegd voor specifieke [!DNL Platform]-gegevens. Bijvoorbeeld, als een fusiebeleid werd gebruikt om een segment tot stand te brengen dat aan een derdebestemming activeerde, en uw organisatie een beleid van het gegevensgebruik had dat de uitvoer van specifieke gegevens naar derden verhindert, zou u een **[!UICONTROL Data governance policy violation detected]** bericht wanneer het proberen om uw fusiebeleid te bewaren ontvangen.

Deze melding bevat een lijst met beleidsregels voor gegevensgebruik die zijn overtreden. U kunt de details van de schending bekijken door een beleid in de lijst te selecteren. Bij het selecteren van een overtreden beleid, verstrekt het **[!UICONTROL Data lineage]** lusje de reden voor de schending en de beïnvloede activeringen, elk die meer detail verstrekken in hoe het beleid van het gegevensgebruik is overtreden.

Als u meer wilt weten over de manier waarop gegevensbeheer in Adobe Experience Platform wordt uitgevoerd, leest u eerst het [Overzicht gegevensbeheer](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Volgende stappen

Nu u en gevormd samenvoegbeleid voor uw organisatie hebt gecreeerd, kunt u hen gebruiken om de mening van klantenprofielen binnen Platform aan te passen en publiekssegmenten van uw gegevens van het Profiel tot stand te brengen. Zie [segmentatieoverzicht](../../segmentation/home.md) voor meer informatie over om tot stand te brengen en met segmenten te werken gebruikend [!DNL Experience Platform] UI en APIs.
