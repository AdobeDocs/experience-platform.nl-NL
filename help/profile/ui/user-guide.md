---
keywords: Experience Platform;profiel;real-time klantprofiel;problemen;API;verenigd profiel;verenigd profiel;verenigd profiel;profiel;rtcp;inschakelen profiel;Inschakelen profiel;Unieschema;UNION-PROFIEL;vakbondsprofiel
title: Gebruikersgids voor realtime gebruikersprofiel
description: Het profiel van de Klant in real time leidt tot een holistische mening van elk van uw individuele klanten, die gegevens van veelvoudige kanalen met inbegrip van online, off-line, CRM, en derdegegevens combineren. Dit document fungeert als richtlijn voor de interactie met Real-Time Klantprofiel in de Adobe Experience Platform-gebruikersinterface.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: d9fc1fa6a1bbc6b13b2600a5ec9400a0b488056a
workflow-type: tm+mt
source-wordcount: '2135'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] UI-hulplijn

[!DNL Real-Time Customer Profile] maakt een holistische weergave van elk van uw individuele klanten, waarbij gegevens van meerdere kanalen worden gecombineerd, waaronder online-, offline-, CRM- en gegevens van derden. Dit document fungeert als richtlijn voor interactie met [!DNL Real-Time Customer Profile] -gegevens in de gebruikersinterface van Adobe Experience Platform (UI).

## Aan de slag

Deze UI-gids vereist inzicht in de verschillende [!DNL Experience Platform] -services die bij het beheren van [!DNL Real-Time Customer Profiles] betrokken zijn. Voordat u deze handleiding leest of in de gebruikersinterface werkt, raadpleegt u de documentatie voor de volgende services:

* [[!DNL Real-Time Customer Profile]  overzicht ](../home.md): Verstrekt een verenigd, in real time consumentenprofiel dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Identity Service]](../../identity-service/home.md): schakelt [!DNL Real-Time Customer Profile] in door identiteiten te overbruggen van verschillende gegevensbronnen terwijl ze worden ingesloten in [!DNL Experience Platform] .
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt.

## [!UICONTROL Overview]

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Profiles]** in de linkernavigatie om het tabblad **[!UICONTROL Overview]** met het profieldashboard te openen.

>[!NOTE]
>
>Als uw organisatie nieuw is voor Experience Platform en nog geen actieve profielgegevenssets of samenvoegbeleid heeft gemaakt, is het dashboard van [!UICONTROL Profiles] niet zichtbaar. In plaats daarvan geeft het tabblad [!UICONTROL Overview] koppelingen en documentatie weer om u te helpen aan de slag te gaan met Real-Time Klantprofiel.

### Profieldashboard {#profile-dashboard}

Het profieldashboard bevat een overzicht van de belangrijkste maatstaven die betrekking hebben op de profielgegevens van uw organisatie.

Meer leren, bezoek de [ gids van het profieldashboard ](../../dashboards/guides/profiles.md).

![ het dashboard van het Profiel wordt getoond.](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL Browse] tabmetriek

Selecteer het tabblad **[!UICONTROL Browse]** om verschillende metrische gegevens weer te geven die betrekking hebben op de profielgegevens van uw organisatie. U kunt dit lusje ook gebruiken om de opslag van het Profiel te doorbladeren gebruikend een samenvoegbeleid of een identiteit, zoals geschetst in de volgende sectie van deze gids.

Op de rechterkant van het **[!UICONTROL Browse]** lusje is de [ profieltelling ](#profile-count) evenals een lijst van [ profielen door namespace ](#profiles-by-namespace).

>[!NOTE]
>
>Deze profielmetriek kan van de metriek variëren die op het [ profiel dashboard ](#profile-dashboard) wordt getoond omdat zij gebruikend het standaardsamenvoegbeleid van uw organisatie worden geëvalueerd. Voor meer informatie bij het werken met fusiebeleid, met inbegrip van hoe te om een standaardfusiebeleid te bepalen, zie het [ overzicht van het samenvoegingsbeleid ](../merge-policies/overview.md).

Naast deze metriek, verstrekt deze sectie een laatste bijgewerkte datum en tijd, die tonen wanneer de metriek het laatst werden geëvalueerd.

![ de metriek van het Profiel wordt getoond en benadrukt.](../images/user-guide/browse-metrics.png)

### Aantal profielen {#profile-count}

Het aantal profielen geeft het totale aantal profielen weer dat uw organisatie in Experience Platform heeft, nadat het standaardsamenvoegbeleid van uw organisatie profielfragmenten heeft samengevoegd tot één profiel voor elke afzonderlijke klant. Met andere woorden, uw organisatie kan veelvoudige profielfragmenten met betrekking tot één enkele klant hebben die met uw merk over verschillende kanalen interactie heeft, maar deze fragmenten zouden samen (volgens het standaard fusiebeleid) worden samengevoegd en een telling van &quot;1&quot;profiel terugkeren omdat zij allen met het zelfde individu verwant zijn.

Het aantal profielen omvat ook zowel profielen met kenmerken (recordgegevens) als profielen die alleen tijdreeksgegevens (gebeurtenisgegevens) bevatten, zoals Adobe Analytics-profielen. Het aantal profielen wordt regelmatig vernieuwd om een up-to-date totaal aantal profielen in Experience Platform te bieden.

#### De metrische waarde voor het aantal profielen bijwerken

Wanneer de opname van records in de [!DNL Profile] store de telling met meer dan 3% verhoogt of verlaagt, wordt een baan teweeggebracht om de telling bij te werken. Voor het stromen gegevenswerkschema&#39;s, wordt een controle uitgevoerd op uurbasis om te bepalen als de 3% verhoging of dalingsdrempel is voldaan. Als dit het geval is, wordt er automatisch een taak geactiveerd om het aantal profielen bij te werken. Voor batch-opname wordt binnen 15 minuten na het correct innemen van een batch in de profielopslag een taak uitgevoerd om het aantal profielen bij te werken als aan de drempel voor 3% verhoging of verlaging is voldaan.

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

De metrische waarde **[!UICONTROL Profiles by namespace]** geeft het totale aantal en de totale verdeling van naamruimten over alle samengevoegde profielen in uw archief Profiel weer. Het totale aantal profielen per naamruimte (d.w.z. het optellen van de waarden voor elke naamruimte) zal altijd hoger zijn dan de metrische waarde van het aantal profielen, omdat aan één profiel meerdere naamruimten kunnen zijn gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

#### De metrische waarde van [!UICONTROL Profiles by namespace] bijwerken

Gelijkaardig aan de [ profieltelling ](#profile-count) metrisch, wanneer het opnemen van verslagen in de [!DNL Profile] opslag de telling met meer dan 5% verhoogt of vermindert, wordt een baan teweeggebracht om de namespacemetriek bij te werken. Voor het stromen gegevenswerkschema&#39;s, wordt een controle uitgevoerd op uurbasis om te bepalen als de 5% verhoging of dalingsdrempel is voldaan. Als dit het geval is, wordt er automatisch een taak geactiveerd om het aantal profielen bij te werken. Voor batch-opname wordt binnen 15 minuten nadat een batch in de [!DNL Profile] store is opgenomen, een taak uitgevoerd om de metriek bij te werken als aan de drempel van 5% verhoging of verlaging is voldaan.

## Tabblad [!UICONTROL Browse] gebruiken om profielen weer te geven

Op het tabblad **[!UICONTROL Browse]** kunt u voorbeeldprofielen weergeven met behulp van een samenvoegbeleid of specifieke profielen opzoeken met behulp van een naamruimte en waarde voor identiteit.

![ de Profielen die tot de organisatie behoren worden getoond.](../images/user-guide/none-selected.png)

### Bladeren op [!UICONTROL Merge policy]

Het tabblad **[!UICONTROL Browse]** is standaard ingesteld op het standaardsamenvoegbeleid voor uw organisatie. Als u een ander samenvoegbeleid wilt kiezen, selecteert u de `X` naast de naam van het samenvoegbeleid en opent u het dialoogvenster **[!UICONTROL Select merge policy]** met de kiezer.

>[!NOTE]
>
>Als er geen samenvoegbeleid is geselecteerd, opent u het selectiedialoogvenster met de selectieknop naast het veld **[!UICONTROL Merge policy]** .

![ de selecteur van het beleid van de Fusie wordt benadrukt.](../images/user-guide/browse-by-merge-policy.png)

Als u een samenvoegbeleid wilt kiezen in het dialoogvenster **[!UICONTROL Select merge policy]** , selecteert u het keuzerondje naast de naam van het beleid en gebruikt u **[!UICONTROL Select]** om terug te keren naar het tabblad [!UICONTROL Browse] . Vervolgens kunt u **[!UICONTROL View]** selecteren om de voorbeeldprofielen te vernieuwen en een voorbeeld van profielen weer te geven waarop het nieuwe samenvoegbeleid is toegepast.

![ dialoog A waar u het fusiebeleid kunt selecteren door wordt getoond te filtreren.](../images/user-guide/select-merge-policy.png)

De profielen die worden getoond vertegenwoordigen een steekproef van maximaal 20 profielen van de opslag van het Profiel van uw organisatie, nadat het geselecteerde samenvoegbeleid is toegepast. De voorbeeldprofielen voor het geselecteerde samenvoegbeleid worden vernieuwd wanneer nieuwe gegevens worden toegevoegd aan de profielopslag van uw organisatie.

Selecteer **[!UICONTROL Profile ID]** als u de details van een van de voorbeeldprofielen wilt weergeven. Voor meer informatie, zie de sectie later in deze gids op [ het bekijken van profieldetails ](#profile-detail).

![ de profielen van de Steekproef die het fusiebeleid aanpassen worden getoond.](../images/user-guide/sample-profiles.png)

Meer over samenvoegingsbeleid en hun rol binnen Experience Platform leren, zie het [ overzicht van het fusiebeleid ](../merge-policies/overview.md).

### Bladeren op [!UICONTROL Identity] {#browse-identity}

Op het tabblad **[!UICONTROL Browse]** kunt u een naamruimte voor identiteiten gebruiken om een specifiek profiel op te zoeken aan de hand van een identiteitswaarde. Als u bladert op basis van een identiteit, moet u een samenvoegbeleid, een naamruimte voor identiteit en een identiteitswaarde opgeven.

![ de selecteur van het fusiebeleid wordt benadrukt.](../images/user-guide/browse-by-merge-policy.png)

Gebruik indien nodig de kiezer van **[!UICONTROL Merge policy]** om het dialoogvenster **[!UICONTROL Select merge policy]** te openen en kies het samenvoegbeleid dat u wilt gebruiken.

![ dialoog A waar u het fusiebeleid kunt selecteren door wordt getoond te filtreren.](../images/user-guide/select-merge-policy.png)

Vervolgens opent u het dialoogvenster **[!UICONTROL Identity namespace]** met de kiezer van **[!UICONTROL Select identity namespace]** en kiest u de naamruimte waarin u wilt zoeken. Als uw organisatie veel naamruimten heeft, kunt u de zoekbalk in het dialoogvenster gebruiken om de naam van een naamruimte te typen.

U kunt een naamruimte selecteren om aanvullende details weer te geven of het keuzerondje selecteren om een naamruimte te kiezen. Vervolgens kunt u **[!UICONTROL Select]** gebruiken om door te gaan.

![ dialoog A waar u de identiteit kunt selecteren namespace aan filter door wordt getoond.](../images/user-guide/select-identity-namespace.png)

Nadat u een [!UICONTROL Identity namespace] hebt geselecteerd en terugkeert naar de tab [!UICONTROL Browse] , kunt u een **[!UICONTROL Identity value]** invoeren die betrekking heeft op de naamruimte die u hebt geselecteerd.

>[!NOTE]
>
>Deze waarde is specifiek voor een individueel klantprofiel en moet een geldige waarde zijn voor de opgegeven naamruimte. Als u bijvoorbeeld de naamruimte E-mail selecteert, hebt u een identiteitswaarde nodig in de vorm van een geldig e-mailadres.

![ de identiteitswaarde die u wilt filtreren door wordt benadrukt.](../images/user-guide/filter-identity-value.png)

Wanneer een waarde is ingevoerd, selecteert u **[!UICONTROL View]** en geeft u één profiel dat overeenkomt met de waarde. Selecteer **[!UICONTROL Profile ID]** om de profieldetails te bekijken.

![ het profiel dat de identiteitswaarde aanpast wordt benadrukt.](../images/user-guide/filtered-identity-value.png)

## Profieldetails weergeven {#profile-detail}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_201001_404"
>title="Entiteit niet gevonden"
>abstract="Dit betekent dat Experience Platform de gevraagde entiteit niet kon vinden. Probeer een van de volgende oplossingen om deze fout op te lossen:<ul><li>Controleer of de juiste profiel-id wordt vermeld in de URL van de entiteit waartoe u toegang probeert te krijgen.</li><li>Zorg ervoor dat u beschikt over de juiste organisatie- en sandboxcombinatie voor de entiteit waartoe u toegang probeert te krijgen.</li></ul>"

Nadat u een **[!UICONTROL Profile ID]** -tab hebt geselecteerd, wordt het tabblad **[!UICONTROL Detail]** geopend. De profielgegevens die op het tabblad **[!UICONTROL Detail]** worden weergegeven, zijn samengevoegd vanuit meerdere profielfragmenten en vormen één weergave van de individuele klant. Dit omvat klantgegevens zoals basiskenmerken, gekoppelde identiteiten en kanaalvoorkeuren.

De weergegeven standaardvelden kunnen ook op organisatorisch niveau worden gewijzigd om de voorkeursprofielkenmerken weer te geven. Meer leren over het aanpassen van deze gebieden, met inbegrip van geleidelijke instructies voor het toevoegen van en het verwijderen van attributen en het resizing van dashboardpanelen, te lezen gelieve de [ gids van de profieldetail aanpassing ](profile-customization.md).

![ het lusje van Details wordt benadrukt. De profieldetails worden getoond.](../images/user-guide/profile-detail-row-name.png)

U kunt ook schakelen tussen het weergeven van de kenmerknamen als hun weergavenamen en hun padnamen voor velden. Als u wilt schakelen tussen deze twee weergaven, selecteert u de schakeloptie **[!UICONTROL Show display names]** .

![ de knevel van vertoningsnamen van de Show wordt benadrukt, en de vertoningsnamen worden getoond onder de attributen.](../images/user-guide/profile-detail.png)

Selecteer een van de andere beschikbare tabbladen om aanvullende informatie over het profiel van de individuele klant weer te geven. Deze lusjes omvatten attributen, gebeurtenissen, en het lusje van het publiekslidmaatschap dat het publiek toont waarvoor het profiel momenteel gekwalificeerd is.

### Tabblad Kenmerken

Het tabblad **[!UICONTROL Attributes]** bevat een lijstweergave met een overzicht van alle kenmerken die betrekking hebben op één profiel, nadat het opgegeven samenvoegbeleid is toegepast.

Deze kenmerken kunnen ook als een JSON-object worden weergegeven door op **[!UICONTROL View JSON]** te selecteren. Dit is handig voor gebruikers die beter willen begrijpen hoe de profielkenmerken in Experience Platform worden ingevoerd.

![ het lusje van Attributen wordt benadrukt. De profielkenmerken worden weergegeven.](../images/user-guide/attributes.png)

Als u de kenmerken wilt weergeven die beschikbaar zijn op de Edge, selecteert u **[!UICONTROL Edge]** in de kiezer voor de gegevenslocatie.

![ de selecteur van de gegevensplaats binnen het attributenlusje wordt benadrukt.](../images/user-guide/attributes-select.png)

Voor meer informatie over randprofielen, te lezen gelieve de [ documentatie van randprofielen ](../edge-profiles.md).

### Het tabblad Gebeurtenissen

Het tabblad **[!UICONTROL Events]** bevat gegevens van de 100 meest recente ExperienceEvents die aan de klant zijn gekoppeld. Deze gegevens kunnen het openen van e-mail, winkelwagentjes en paginaweergaven omvatten. Als u **[!UICONTROL View all]** selecteert voor een afzonderlijke gebeurtenis, worden aanvullende velden en waarden vastgelegd als onderdeel van de gebeurtenis.

Gebeurtenissen kunnen ook als een JSON-object worden weergegeven door op **[!UICONTROL View JSON]** te klikken. Dit is handig om te begrijpen hoe gebeurtenissen worden vastgelegd in Experience Platform.

![ het lusje van Gebeurtenissen wordt benadrukt. De profielgebeurtenissen worden getoond.](../images/user-guide/events.png)

### Tabblad Poortlidmaatschap

Op het tabblad **[!UICONTROL Audience membership]** wordt een lijst weergegeven met de naam en beschrijving van het publiek waartoe het individuele klantprofiel momenteel behoort. Deze lijst wordt automatisch bijgewerkt wanneer het profiel in aanmerking komt of vervalt bij het publiek. Het totale aantal soorten publiek waarvoor het profiel momenteel is gekwalificeerd, wordt aan de rechterkant van het tabblad weergegeven.

Voor meer informatie over segmentatie in Experience Platform, gelieve te verwijzen naar de [ documentatie van de Dienst van de Segmentatie van Adobe Experience Platform ](../../segmentation/home.md).

![ het lusje van het lidmaatschap van de Publiek wordt benadrukt. De details van het publiekslidmaatschap van het profiel worden getoond.](../images/user-guide/audience-membership.png)

Selecteer **[!UICONTROL Edge]** in de kiezer voor de gegevenslocatie om het publiekslidmaatschap van de profielen op de Edge weer te geven. Meer informatie over randsegmentatie kan in de [ gids van de randsegmentatie ](../../segmentation/methods/edge-segmentation.md) worden gevonden.

![ de selecteur van de gegevensplaats binnen het lusje van het publiekslidmaatschap wordt benadrukt.](../images/user-guide/audience-membership-select.png)

## Beleid samenvoegen

Selecteer in het hoofdmenu **[!UICONTROL Profiles]** de tab **[!UICONTROL Merge Policies]** om een lijst weer te geven met samenvoegbeleidsregels die bij uw organisatie horen. Elk vermeld beleid toont zijn naam, al dan niet het standaardsamenvoegbeleid, en de schemaklasse die het op van toepassing is.

Voor meer informatie over fusiebeleid, zie het [ overzicht van het fusiebeleid ](../merge-policies/overview.md).

![ het lusje van het Beleid van de Fusie wordt benadrukt. Het beleid van de fusie dat tot de organisatie behoort wordt getoond.](../images/user-guide/merge-policies.png)

## Unieschema {#union-schema}

Selecteer in het hoofdmenu **[!UICONTROL Profiles]** het tabblad **[!UICONTROL Union Schema]** om de beschikbare samenvoegingsschema&#39;s voor uw opgenomen gegevens weer te geven. Een samenvoegingsschema is een samenvoeging van alle [!DNL Experience Data Model] (XDM) gebieden onder de zelfde klasse, waarvan schema&#39;s voor gebruik in [!DNL Real-Time Customer Profile] zijn toegelaten.

Voor meer informatie over verenigingsschema&#39;s, gelieve te bezoeken de [ gids UI van het uniesschema ](union-schema.md).

![ het lusje van het Schema van de Unie wordt benadrukt. De schema&#39;s van de unie die tot de organisatie behoren worden getoond.](../images/user-guide/union-schema.png)

## Berekende kenmerken {#computed-attributes}

Selecteer in het hoofdmenu **[!UICONTROL Profiles]** het tabblad **[!UICONTROL Computed attributes]** om een lijst weer te geven met berekende kenmerken die bij uw organisatie horen.

![ het Berekende attributenlusje wordt benadrukt.](../images/user-guide/computed-attributes.png)

Voor meer informatie over gegevens verwerkte attributen, te lezen gelieve [ gegevens verwerkt attributenoverzicht ](../computed-attributes/overview.md). Voor meer informatie over hoe te om gegevens verwerkte attributen binnen Experience Platform UI te gebruiken, te lezen gelieve de [ gegevens verwerkte gids UI van attributen ](../computed-attributes/ui.md).

## Volgende stappen

Door deze handleiding te lezen, weet u hoe u de profielgegevens van uw organisatie kunt bekijken en beheren met de gebruikersinterface van Experience Platform. Voor informatie over hoe te met profielgegevens werken gebruikend Experience Platform APIs, gelieve te verwijzen naar de [ Realtime gids van het Profiel van de Klant API ](../api/overview.md).
