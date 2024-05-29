---
keywords: Experience Platform;profiel;real-time klantprofiel;problemen;API;verenigd profiel;verenigd profiel;verenigd profiel;profiel;rtcp;inschakelen profiel;Inschakelen profiel;Unieschema;UNION-PROFIEL;vakbondsprofiel
title: Gebruikersgids voor realtime gebruikersprofiel
description: Het profiel van de Klant in real time leidt tot een holistische mening van elk van uw individuele klanten, die gegevens van veelvoudige kanalen met inbegrip van online, off-line, CRM, en derdegegevens combineren. Dit document fungeert als richtlijn voor de interactie met Real-Time Klantprofiel in de Adobe Experience Platform-gebruikersinterface.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '2027'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] UI-hulplijn

[!DNL Real-Time Customer Profile] leidt tot een holistische mening van elk van uw individuele klanten, die gegevens van veelvoudige kanalen met inbegrip van online, off-line, CRM, en derdegegevens combineren. Dit document fungeert als richtlijn voor interactie met [!DNL Real-Time Customer Profile] gegevens in de gebruikersinterface van Adobe Experience Platform (UI).

## Aan de slag

Deze UI-gids vereist inzicht in de verschillende [!DNL Experience Platform] diensten die betrokken zijn bij het beheer [!DNL Real-Time Customer Profiles]. Voordat u deze handleiding leest of in de gebruikersinterface werkt, raadpleegt u de documentatie voor de volgende services:

* [[!DNL Real-Time Customer Profile] overzicht](../home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [[!DNL Identity Service]](../../identity-service/home.md): Schakelt in [!DNL Real-Time Customer Profile] door identiteiten van verschillende gegevensbronnen te overbruggen aangezien zij worden opgenomen in [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Platform] organiseert de gegevens van de klantenervaring.

## [!UICONTROL Overview]

Selecteer in de gebruikersinterface van het Experience Platform de optie **[!UICONTROL Profiles]** in de linkernavigatie om de **[!UICONTROL Overview]** tabblad met het profieldashboard.

>[!NOTE]
>
>Als uw organisatie nieuw aan Platform is en nog geen actieve datasets van het Profiel of gecreeerd samenvoegbeleid heeft, [!UICONTROL Profiles] het dashboard is niet zichtbaar. In plaats daarvan [!UICONTROL Overview] op het tabblad vindt u koppelingen en documentatie om u te helpen aan de slag te gaan met Real-Time Klantprofiel.

### Profieldashboard {#profile-dashboard}

Het profieldashboard bevat een overzicht van de belangrijkste maatstaven die betrekking hebben op de profielgegevens van uw organisatie.

Ga voor meer informatie naar de [Handleiding voor profieldashboard](../../dashboards/guides/profiles.md).

![Het dashboard Profiel wordt weergegeven.](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL Browse] tabmetriek

Selecteer de **[!UICONTROL Browse]** om verschillende metriek weer te geven die betrekking hebben op de profielgegevens van uw organisatie. U kunt dit lusje ook gebruiken om de opslag van het Profiel te doorbladeren gebruikend een samenvoegbeleid of een identiteit, zoals geschetst in de volgende sectie van deze gids.

Aan de rechterkant van het **[!UICONTROL Browse]** tab is [aantal profielen](#profile-count) alsmede een lijst van [profielen op naamruimte](#profiles-by-namespace).

>[!NOTE]
>
>Deze profielwaarden kunnen afwijken van de maatstaven die worden weergegeven op het tabblad [profieldashboard](#profile-dashboard) omdat zij gebruikend het standaardsamenvoegbeleid van uw organisatie worden geëvalueerd. Voor meer informatie bij het werken met fusiebeleid, met inbegrip van hoe te om een standaard fusiebeleid te bepalen, zie [overzicht van samenvoegbeleid](../merge-policies/overview.md).

Naast deze metriek, verstrekt deze sectie een laatste bijgewerkte datum en tijd, die tonen wanneer de metriek het laatst werden geëvalueerd.

![De maatstaven van het Profiel worden weergegeven en gemarkeerd.](../images/user-guide/browse-metrics.png)

### Aantal profielen {#profile-count}

Het aantal profielen geeft het totale aantal profielen weer dat uw organisatie binnen het Experience Platform heeft, nadat het standaardsamenvoegbeleid van uw organisatie profielfragmenten heeft samengevoegd tot één profiel voor elke individuele klant. Met andere woorden, uw organisatie kan veelvoudige profielfragmenten met betrekking tot één enkele klant hebben die met uw merk over verschillende kanalen interactie heeft, maar deze fragmenten zouden samen (volgens het standaard fusiebeleid) worden samengevoegd en een telling van &quot;1&quot;profiel terugkeren omdat zij allen met het zelfde individu verwant zijn.

Het aantal profielen omvat ook zowel profielen met kenmerken (recordgegevens) als profielen die alleen tijdreeksgegevens (gebeurtenisgegevens) bevatten, zoals Adobe Analytics-profielen. Het aantal profielen wordt regelmatig vernieuwd om een up-to-date totaal aantal profielen binnen Platform te bieden.

#### De metrische waarde voor het aantal profielen bijwerken

Wanneer de opname van records in de [!DNL Profile] de opslag verhoogt of vermindert de telling met meer dan 5%, wordt een baan teweeggebracht om de telling bij te werken. Voor het stromen gegevenswerkschema&#39;s, wordt een controle uitgevoerd op uurbasis om te bepalen als de 5% verhoging of dalingsdrempel is voldaan. Als dit het geval is, wordt er automatisch een taak geactiveerd om het aantal profielen bij te werken. Voor batch-opname wordt binnen 15 minuten na het correct innemen van een batch in de profielopslag een taak uitgevoerd om het aantal profielen bij te werken als aan de drempel van 5% verhoging of afname is voldaan.

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

De **[!UICONTROL Profiles by namespace]** metrisch toont het totale aantal en de verdeling van namespaces over alle samengevoegde profielen in uw opslag van het Profiel. Het totale aantal profielen per naamruimte (d.w.z. het optellen van de waarden voor elke naamruimte) zal altijd hoger zijn dan de metrische waarde van het aantal profielen, omdat aan één profiel meerdere naamruimten kunnen zijn gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

#### De [!UICONTROL Profiles by namespace] metrisch

Vergelijkbaar met de [aantal profielen](#profile-count) metrisch, wanneer de inname van verslagen in [!DNL Profile] de opslag verhoogt of vermindert de telling met meer dan 5%, wordt een baan teweeggebracht om de namespacemetriek bij te werken. Voor het stromen gegevenswerkschema&#39;s, wordt een controle uitgevoerd op uurbasis om te bepalen als de 5% verhoging of dalingsdrempel is voldaan. Als dit het geval is, wordt er automatisch een taak geactiveerd om het aantal profielen bij te werken. Voor batch-inname, binnen 15 minuten na het met succes innemen van een batch in de [!DNL Profile] slaan, als aan de 5% verhoging of daling drempel wordt voldaan, wordt een baan in werking gesteld om de metriek bij te werken.

## Gebruiken [!UICONTROL Browse] tabblad to view profiles

Op de **[!UICONTROL Browse]** kunt u voorbeeldprofielen weergeven met behulp van een samenvoegbeleid of specifieke profielen opzoeken met behulp van een naamruimte en waarde voor identiteit.

![De profielen die bij de organisatie horen, worden weergegeven.](../images/user-guide/none-selected.png)

### Bladeren op [!UICONTROL Merge policy]

De **[!UICONTROL Browse]** wordt standaard ingesteld op het standaardsamenvoegbeleid voor uw organisatie. Als u een ander samenvoegbeleid wilt kiezen, selecteert u de `X` naast de naam van het samenvoegbeleid en open vervolgens de kiezer **[!UICONTROL Select merge policy]** in.

>[!NOTE]
>
>Als er geen samenvoegbeleid is geselecteerd, gebruikt u de selectieknop naast de knop **[!UICONTROL Merge policy]** om het dialoogvenster Selectie te openen.

![De kiezer voor samenvoegbeleid wordt gemarkeerd.](../images/user-guide/browse-by-merge-policy.png)

Als u een samenvoegbeleid wilt kiezen in het menu **[!UICONTROL Select merge policy]** selecteert u het keuzerondje naast de naam van het beleid en gebruikt u **[!UICONTROL Select]** om terug te keren naar de [!UICONTROL Browse] tab. U kunt vervolgens **[!UICONTROL View]** om de steekproefprofielen te verfrissen en een steekproef van profielen te zien met het nieuwe toegepaste samenvoegbeleid.

![Er wordt een dialoogvenster weergegeven waarin u het samenvoegbeleid kunt selecteren waarop u wilt filteren.](../images/user-guide/select-merge-policy.png)

De profielen die worden getoond vertegenwoordigen een steekproef van maximaal 20 profielen van de opslag van het Profiel van uw organisatie, nadat het geselecteerde samenvoegbeleid is toegepast. De voorbeeldprofielen voor het geselecteerde samenvoegbeleid worden vernieuwd wanneer nieuwe gegevens worden toegevoegd aan de profielopslag van uw organisatie.

Als u de details van een van de voorbeeldprofielen wilt weergeven, selecteert u de optie **[!UICONTROL Profile ID]**. Zie de sectie verderop in deze handleiding voor meer informatie [profieldetails weergeven](#profile-detail).

![Voorbeeldprofielen die overeenkomen met het samenvoegbeleid worden weergegeven.](../images/user-guide/sample-profiles.png)

Als u meer wilt weten over samenvoegingsbeleid en hun rol in Platform, raadpleegt u de [overzicht van samenvoegbeleid](../merge-policies/overview.md).

### Bladeren op [!UICONTROL Identity] {#browse-identity}

Op de **[!UICONTROL Browse]** kunt u een naamruimte gebruiken om een specifiek profiel op te zoeken aan de hand van een identiteitswaarde. Als u bladert op basis van een identiteit, moet u een samenvoegbeleid, een naamruimte voor identiteit en een identiteitswaarde opgeven.

![De kiezer voor het samenvoegbeleid wordt gemarkeerd.](../images/user-guide/browse-by-merge-policy.png)

Gebruik indien nodig de **[!UICONTROL Merge policy]** om de **[!UICONTROL Select merge policy]** en kiest u het samenvoegbeleid dat u wilt gebruiken.

![Er wordt een dialoogvenster weergegeven waarin u het samenvoegbeleid kunt selecteren waarop u wilt filteren.](../images/user-guide/select-merge-policy.png)

Gebruik vervolgens de **[!UICONTROL Identity namespace]** om de **[!UICONTROL Select identity namespace]** en kiest u de naamruimte waarin u wilt zoeken. Als uw organisatie veel naamruimten heeft, kunt u de zoekbalk in het dialoogvenster gebruiken om de naam van een naamruimte te typen.

U kunt een naamruimte selecteren om aanvullende details weer te geven of het keuzerondje selecteren om een naamruimte te kiezen. U kunt vervolgens **[!UICONTROL Select]** om door te gaan.

![Er wordt een dialoogvenster weergegeven waarin u de naamruimte kunt selecteren waarnaar u wilt filteren.](../images/user-guide/select-identity-namespace.png)

Nadat u een [!UICONTROL Identity namespace] en terugkeren naar de [!UICONTROL Browse] kunt u een **[!UICONTROL Identity value]** heeft betrekking op de naamruimte die u hebt geselecteerd.

>[!NOTE]
>
>Deze waarde is specifiek voor een individueel klantprofiel en moet een geldige waarde zijn voor de opgegeven naamruimte. Als u bijvoorbeeld de naamruimte E-mail selecteert, hebt u een identiteitswaarde nodig in de vorm van een geldig e-mailadres.

![De identiteitswaarde waarop u wilt filteren, wordt gemarkeerd.](../images/user-guide/filter-identity-value.png)

Nadat een waarde is ingevoerd, selecteert u **[!UICONTROL View]** en er wordt één profiel geretourneerd dat overeenkomt met de waarde. Selecteer de **[!UICONTROL Profile ID]** om de profieldetails te bekijken.

![Het profiel dat overeenkomt met de identiteitswaarde wordt gemarkeerd.](../images/user-guide/filtered-identity-value.png)

## Profieldetails weergeven {#profile-detail}

Nadat u een **[!UICONTROL Profile ID]** de **[!UICONTROL Detail]** wordt geopend. De profielgegevens die worden weergegeven op de **[!UICONTROL Detail]** tab is samengevoegd vanuit meerdere profielfragmenten en vormt zo één weergave van de individuele klant. Dit omvat klantgegevens zoals basiskenmerken, gekoppelde identiteiten en kanaalvoorkeuren.

De weergegeven standaardvelden kunnen ook op organisatorisch niveau worden gewijzigd om de voorkeursprofielkenmerken weer te geven. Als u meer wilt weten over het aanpassen van deze velden, inclusief stapsgewijze instructies voor het toevoegen en verwijderen van kenmerken en het wijzigen van het formaat van dashboarddeelvensters, leest u de [handleiding voor het aanpassen van profieldetails](profile-customization.md).

![Het tabblad Details is gemarkeerd. De profieldetails worden getoond.](../images/user-guide/profile-detail.png)

U kunt aanvullende informatie met betrekking tot het individuele klantenprofiel bekijken door een andere beschikbare lusjes te selecteren. Deze lusjes omvatten attributen, gebeurtenissen, en het lusje van het publiekslidmaatschap dat het publiek toont waarvoor het profiel momenteel gekwalificeerd is.

### Tabblad Kenmerken

De **[!UICONTROL Attributes]** bevat een lijstweergave waarin een overzicht wordt gegeven van alle kenmerken die betrekking hebben op één profiel, nadat het opgegeven samenvoegbeleid is toegepast.

Deze kenmerken kunnen ook als een JSON-object worden weergegeven door **[!UICONTROL View JSON]**. Dit is handig voor gebruikers die beter willen begrijpen hoe de profielkenmerken worden opgenomen in Platform.

![Het tabblad Kenmerken is gemarkeerd. De profielkenmerken worden weergegeven.](../images/user-guide/attributes.png)

Selecteer **[!UICONTROL Edge]** op de gegevenslocatieselector.

![De gegevenslocatieselector op het tabblad Kenmerken wordt gemarkeerd.](../images/user-guide/attributes-select.png)

Lees voor meer informatie over randprofielen de [documentatie over Edge-profielen](../edge-profiles.md).

### Het tabblad Gebeurtenissen

De **[!UICONTROL Events]** bevat gegevens van de 100 meest recente ExperienceEvents die aan de klant zijn gekoppeld. Deze gegevens kunnen het openen van e-mail, winkelwagentjes en paginaweergaven omvatten. Selecteren **[!UICONTROL View all]** voor elke afzonderlijke gebeurtenis worden aanvullende velden en waarden vastgelegd als onderdeel van de gebeurtenis.

Gebeurtenissen kunnen ook als een JSON-object worden weergegeven door **[!UICONTROL View JSON]**. Dit is handig als u wilt begrijpen hoe gebeurtenissen worden vastgelegd in Platform.

![Het tabblad Gebeurtenissen is gemarkeerd. De profielgebeurtenissen worden weergegeven.](../images/user-guide/events.png)

### Tabblad Poortlidmaatschap

De **[!UICONTROL Audience membership]** wordt een lijst weergegeven met de naam en beschrijving van het publiek waartoe het individuele klantprofiel momenteel behoort. Deze lijst wordt automatisch bijgewerkt wanneer het profiel in aanmerking komt of vervalt bij het publiek. Het totale aantal soorten publiek waarvoor het profiel momenteel is gekwalificeerd, wordt aan de rechterkant van het tabblad weergegeven.

Raadpleeg voor meer informatie over segmentering in Experience Platform de [Documentatie Adoben Experience Platform Segmentation Service](../../segmentation/home.md).

![Het tabblad Poortlidmaatschap is gemarkeerd. De lidmaatschapsdetails voor het publiek van het profiel worden weergegeven.](../images/user-guide/audience-membership.png)

Selecteer **[!UICONTROL Edge]** in de gegevenslocatieselector. Meer informatie over de segmentatie van de randen vindt u in de [hulplijn voor randsegmentatie](../../segmentation/ui/edge-segmentation.md).

![De kiezer voor de gegevenslocatie op het tabblad voor het publiekslidmaatschap wordt gemarkeerd.](../images/user-guide/audience-membership-select.png)

## Beleid samenvoegen

Van de belangrijkste **[!UICONTROL Profiles]** , selecteert u de **[!UICONTROL Merge Policies]** om een lijst weer te geven met samenvoegbeleid dat tot uw organisatie behoort. Elk vermeld beleid toont zijn naam, al dan niet het standaardsamenvoegbeleid, en de schemaklasse die het op van toepassing is.

Zie voor meer informatie over samenvoegingsbeleid de [overzicht van samenvoegbeleid](../merge-policies/overview.md).

![Het tabblad Samenvoegen wordt gemarkeerd. Het samenvoegingsbeleid dat bij de organisatie hoort, wordt weergegeven.](../images/user-guide/merge-policies.png)

## Unieschema {#union-schema}

Van de belangrijkste **[!UICONTROL Profiles]** , selecteert u de **[!UICONTROL Union Schema]** tabblad om beschikbare samenvoegingsschema&#39;s voor uw opgenomen gegevens weer te geven. Een samenvoegingsschema is een samenvoeging van alle [!DNL Experience Data Model] (XDM) velden onder dezelfde klasse, waarvan de schema&#39;s zijn ingeschakeld voor gebruik in [!DNL Real-Time Customer Profile].

Ga voor meer informatie over vakbondsschema&#39;s naar de [UI-hulplijn verenigingsschema](union-schema.md).

![Het tabblad Unieschema wordt gemarkeerd. Unieregelingen die tot de organisatie behoren, worden weergegeven.](../images/user-guide/union-schema.png)

## Berekende kenmerken {#computed-attributes}

Van de belangrijkste **[!UICONTROL Profiles]** , selecteert u de **[!UICONTROL Computed attributes]** om een lijst weer te geven met berekende kenmerken die bij uw organisatie horen.

![Het tabblad Berekende kenmerken is gemarkeerd.](../images/user-guide/computed-attributes.png)

Lees voor meer informatie over berekende kenmerken de [overzicht van berekende kenmerken](../computed-attributes/overview.md). Lees voor meer informatie over het gebruik van berekende kenmerken in de interface van het platform de [UI-gids voor berekende kenmerken](../computed-attributes/ui.md).

## Volgende stappen

Door deze gids te lezen, weet u hoe te om de het profielgegevens van uw organisatie te bekijken en te beheren gebruikend de UI van het Experience Platform. Voor informatie over het werken met profielgegevens met Experience Platform-API&#39;s raadpleegt u de [Handleiding voor realtime gebruikersprofiel-API](../api/overview.md).
