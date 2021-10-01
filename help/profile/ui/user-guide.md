---
keywords: Experience Platform;profiel;real-time klantprofiel;problemen;API;verenigd profiel;verenigd profiel;verenigd profiel;profiel;rtcp;inschakelen profiel;Inschakelen profiel;Unieschema;UNION-PROFIEL;vakbondsprofiel
title: Gebruikershandleiding voor gebruikersprofiel in realtime
topic-legacy: guide
description: Het profiel van de Klant in real time leidt tot een holistische mening van elk van uw individuele klanten, die gegevens van veelvoudige kanalen met inbegrip van online, off-line, CRM, en derdegegevens combineren. Dit document fungeert als richtlijn voor de interactie met Real-time klantprofiel in de Adobe Experience Platform-gebruikersinterface.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 771be1f5939066295c01eb573a13dbb740e8c776
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] UI-hulplijn

[!DNL Real-time Customer Profile] leidt tot een holistische mening van elk van uw individuele klanten, die gegevens van veelvoudige kanalen met inbegrip van online, off-line, CRM, en derdegegevens combineren. Dit document fungeert als richtlijn voor interactie met [!DNL Real-time Customer Profile]-gegevens in de gebruikersinterface van Adobe Experience Platform (UI).

## Aan de slag

Deze UI-gids vereist inzicht in de verschillende [!DNL Experience Platform] services betrokken bij het beheer van [!DNL Real-time Customer Profiles]. Voordat u deze handleiding leest of in de gebruikersinterface werkt, raadpleegt u de documentatie voor de volgende services:

* [[!DNL Real-time Customer Profile] overzicht](../home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Identity Service]](../../identity-service/home.md): Schakelt  [!DNL Real-time Customer Profile] door het overbruggen van identiteiten uit verschillende gegevensbronnen in terwijl ze worden opgenomen in  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Platform] klantenervaring worden georganiseerd.

## [!UICONTROL Overview]

Selecteer **[!UICONTROL Profiles]** in de linkernavigatie in de interface van het Experience Platform om het tabblad **[!UICONTROL Overview]** met het profieldashboard te openen.

>[!NOTE]
>
>Als uw organisatie nieuw aan Platform is en nog geen actieve datasets van het Profiel of gecreeerd samenvoegbeleid heeft, is [!UICONTROL Profiles] dashboard niet zichtbaar. In plaats daarvan bevat het tabblad [!UICONTROL Overview] koppelingen en documentatie waarmee u aan de slag kunt gaan met het realtime profiel van de klant.

### Profieldashboard {#profile-dashboard}

Het profieldashboard bevat een overzicht van de belangrijkste maatstaven die betrekking hebben op de profielgegevens van uw organisatie.

Voor meer informatie gaat u naar de [dashboardgids voor profielen](../../dashboards/guides/profiles.md).

![](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL Browse] tabmetriek

Selecteer het tabblad **[!UICONTROL Browse]** om verschillende metriek weer te geven die betrekking hebben op de profielgegevens van uw organisatie. U kunt dit tabblad ook gebruiken om door de profielopslag te bladeren met behulp van een samenvoegbeleid of een identiteit, zoals beschreven in de volgende sectie van deze handleiding.

Aan de rechterkant van het tabblad **[!UICONTROL Browse]** is het [aantal profielen](#profile-count) en een lijst met [profielen door naamruimte](#profiles-by-namespace).

>[!NOTE]
>
>Deze profielmetriek kan van de metriek variëren die op [profiel dashboard](#profile-dashboard) wordt getoond omdat zij gebruikend het standaardsamenvoegbeleid van uw organisatie worden geëvalueerd. Voor meer informatie bij het werken met fusiebeleid, met inbegrip van hoe te om een standaard fusiebeleid te bepalen, zie [overzicht van het fusiebeleid](../merge-policies/overview.md).

Naast deze metriek, verstrekt deze sectie een laatste bijgewerkte datum en tijd, die tonen wanneer de metriek het laatst werden geëvalueerd.

![](../images/user-guide/profiles-browse-metrics.png)

### Aantal profielen {#profile-count}

Het aantal profielen geeft het totale aantal profielen weer dat uw organisatie binnen het Experience Platform heeft, nadat het standaardsamenvoegbeleid van uw organisatie profielfragmenten heeft samengevoegd tot één profiel voor elke individuele klant. Met andere woorden, uw organisatie kan veelvoudige profielfragmenten met betrekking tot één enkele klant hebben die met uw merk over verschillende kanalen interactie heeft, maar deze fragmenten zouden samen (volgens het standaard fusiebeleid) worden samengevoegd en een telling van &quot;1&quot;profiel terugkeren omdat zij allen met het zelfde individu verwant zijn.

Het aantal profielen omvat ook zowel profielen met kenmerken (recordgegevens) als profielen die alleen tijdreeksgegevens (gebeurtenisgegevens) bevatten, zoals Adobe Analytics-profielen. Het aantal profielen wordt regelmatig vernieuwd om een up-to-date totaal aantal profielen binnen Platform te verstrekken.

#### De metrische waarde voor het aantal profielen bijwerken

Wanneer de opname van verslagen in [!DNL Profile] opslag de telling met meer dan 5% verhoogt of vermindert, wordt een baan teweeggebracht om de telling bij te werken. Voor het stromen gegevenswerkschema&#39;s, wordt een controle uitgevoerd op uurbasis om te bepalen als de 5% verhoging of dalingsdrempel is voldaan. Als dit het geval is, wordt er automatisch een taak geactiveerd om het aantal profielen bij te werken. Voor batch-opname wordt binnen 15 minuten na het correct innemen van een batch in de profielopslag een taak uitgevoerd om het aantal profielen bij te werken als aan de drempel van 5% verhoging of afname is voldaan.

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

De metrische **[!UICONTROL Profiles by namespace]** toont het totale aantal en de verdeling van namespaces over alle samengevoegde profielen in uw Opslag van het Profiel. Het totale aantal profielen per naamruimte (d.w.z. het optellen van de waarden voor elke naamruimte) zal altijd hoger zijn dan de metrische waarde van het aantal profielen, omdat aan één profiel meerdere naamruimten kunnen zijn gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

#### De metrische [!UICONTROL Profiles by namespace] bijwerken

Vergelijkbaar met de [profieltelling](#profile-count) metrisch, wanneer de opname van verslagen in [!DNL Profile] opslag de telling met meer dan 5% verhoogt of vermindert, wordt een baan teweeggebracht om de namespacemetriek bij te werken. Voor het stromen gegevenswerkschema&#39;s, wordt een controle uitgevoerd op uurbasis om te bepalen als de 5% verhoging of dalingsdrempel is voldaan. Als dit het geval is, wordt er automatisch een taak geactiveerd om het aantal profielen bij te werken. Voor batch-opname wordt binnen 15 minuten nadat een batch in de [!DNL Profile]-winkel is opgenomen, een taak uitgevoerd om de metriek bij te werken als aan de drempel van 5% verhoging of verlaging is voldaan.

## Tabblad [!UICONTROL Browse] gebruiken om profielen weer te geven

Op het tabblad **[!UICONTROL Browse]** kunt u voorbeeldprofielen weergeven met behulp van een samenvoegbeleid of specifieke profielen opzoeken met behulp van een naamruimte en waarde voor identiteit.

![](../images/user-guide/browse-by-none-selected.png)

### Bladeren op [!UICONTROL Merge policy]

Het tabblad **[!UICONTROL Browse]** is standaard ingesteld op het standaardsamenvoegbeleid voor uw organisatie. Als u een ander samenvoegbeleid wilt kiezen, selecteert u `X` naast de naam van het samenvoegbeleid en opent u het dialoogvenster **[!UICONTROL Select merge policy]** met de kiezer.

>[!NOTE]
>
>Als er geen samenvoegbeleid is geselecteerd, gebruikt u de selectieknop naast het veld **[!UICONTROL Merge policy]** om het selectiedialoogvenster te openen.

![](../images/user-guide/browse-by-merge-policy.png)

Als u een samenvoegbeleid wilt kiezen in het dialoogvenster **[!UICONTROL Select merge policy]**, selecteert u het keuzerondje naast de naam van het beleid en gebruikt u **[!UICONTROL Select]** om terug te keren naar het tabblad [!UICONTROL Browse]. U kunt **[!UICONTROL View]** dan selecteren om de steekproefprofielen te verfrissen en een steekproef van profielen met het nieuwe toegepaste samenvoegingsbeleid te zien.

![](../images/user-guide/select-merge-policy-dialog.png)

De profielen die worden getoond vertegenwoordigen een steekproef van maximaal 20 profielen van de het profielopslag van uw organisatie, nadat het geselecteerde samenvoegbeleid is toegepast. De voorbeeldprofielen voor het geselecteerde samenvoegbeleid worden vernieuwd wanneer nieuwe gegevens worden toegevoegd aan de profielopslag van uw organisatie.

Als u de details van een van de voorbeeldprofielen wilt weergeven, selecteert u **[!UICONTROL Profile ID]**. Zie de sectie verderop in deze handleiding op [Informatie over het weergaveprofiel](#profile-detail) voor meer informatie.

![](../images/user-guide/sample-profiles.png)

Meer over fusiebeleid en hun rol binnen Platform leren, zie [overzicht van fusiebeleid](../merge-policies/overview.md).


### Bladeren op [!UICONTROL Identity] {#browse-identity}

Op het tabblad **[!UICONTROL Browse]** kunt u een naamruimte gebruiken om een specifiek profiel op te zoeken aan de hand van een identiteitswaarde. Als u bladert op basis van een identiteit, moet u een samenvoegbeleid, een naamruimte voor identiteit en een identiteitswaarde opgeven.

![](../images/user-guide/browse-by-identity.png)

Gebruik indien nodig de kiezer **[!UICONTROL Merge policy]** om het dialoogvenster **[!UICONTROL Select merge policy]** te openen en kies het samenvoegbeleid dat u wilt gebruiken.

![](../images/user-guide/select-merge-policy-dialog.png)

Vervolgens gebruikt u de kiezer **[!UICONTROL Identity namespace]** om het dialoogvenster **[!UICONTROL Select identity namespace]** te openen en de naamruimte te kiezen waarmee u wilt zoeken. Als uw organisatie veel naamruimten heeft, kunt u de zoekbalk in het dialoogvenster gebruiken om de naam van een naamruimte te typen.

U kunt een naamruimte selecteren om aanvullende details weer te geven of het keuzerondje selecteren om een naamruimte te kiezen. U kunt **[!UICONTROL Select]** dan gebruiken om verder te gaan.

![](../images/user-guide/profiles-select-identity-namespace.png)

Nadat u een [!UICONTROL Identity namespace] hebt geselecteerd en terugkeert naar het tabblad [!UICONTROL Browse], kunt u een **[!UICONTROL Identity value]** invoeren die betrekking heeft op de naamruimte die u hebt geselecteerd.

>[!NOTE]
>
>Deze waarde is specifiek voor een individueel klantprofiel en moet een geldige waarde zijn voor de opgegeven naamruimte. Als u bijvoorbeeld de naamruimte E-mail selecteert, hebt u een identiteitswaarde nodig in de vorm van een geldig e-mailadres.

![](../images/user-guide/browse-by-identity-values.png)

Wanneer een waarde is ingevoerd, selecteert u **[!UICONTROL View]** en geeft u één profiel dat overeenkomt met de waarde. Selecteer **[!UICONTROL Profile ID]** om de profieldetails te bekijken.

![](../images/user-guide/browse-by-identity-profile.png)

## Profieldetails weergeven {#profile-detail}

Nadat u een **[!UICONTROL Profile ID]** hebt geselecteerd, wordt het tabblad **[!UICONTROL Detail]** geopend. De profielgegevens die op het tabblad **[!UICONTROL Detail]** worden weergegeven, zijn samengevoegd vanuit meerdere profielfragmenten en vormen één weergave van de individuele klant. Dit omvat klantgegevens zoals basiskenmerken, gekoppelde identiteiten en kanaalvoorkeuren.

De weergegeven standaardvelden kunnen ook op organisatorisch niveau worden gewijzigd om de voorkeursprofielkenmerken weer te geven. Lees de [handleiding voor het aanpassen van profieldetails](profile-customization.md) voor meer informatie over het aanpassen van deze velden, inclusief stapsgewijze instructies voor het toevoegen en verwijderen van kenmerken en het wijzigen van het formaat van dashboarddeelvensters.

![](../images/user-guide/profiles-profile-detail.png)

U kunt aanvullende informatie met betrekking tot het individuele klantenprofiel bekijken door een andere beschikbare lusjes te selecteren. Deze lusjes omvatten attributen, gebeurtenissen, en het lusje van het segmentlidmaatschap dat de segmenten toont waarvoor het profiel momenteel gekwalificeerd is.

![](../images/user-guide/profiles-attributes-events-segments.png)

### Tabblad Kenmerken

Het tabblad **[!UICONTROL Attributes]** bevat een lijstweergave met een overzicht van alle kenmerken die betrekking hebben op één profiel, nadat het opgegeven samenvoegbeleid is toegepast.

Deze kenmerken kunnen ook als een JSON-object worden weergegeven door op **[!UICONTROL View JSON]** te klikken. Dit is handig voor gebruikers die beter willen begrijpen hoe de profielkenmerken in het Platform worden ingevoerd.

![](../images/user-guide/profiles-attributes.png)

### Het tabblad Gebeurtenissen

Het tabblad **[!UICONTROL Events]** bevat gegevens die betrekking hebben op ExperienceEvents die aan de klant zijn gekoppeld. Dit kan e-mails openen, winkelwagentjes, paginaweergaven en meer zijn. Als u **[!UICONTROL View all]** selecteert voor een afzonderlijke gebeurtenis, worden aanvullende velden en waarden weergegeven als onderdeel van de gebeurtenis.

Gebeurtenissen kunnen ook als een JSON-object worden weergegeven door op **[!UICONTROL View JSON]** te klikken. Dit is handig om te begrijpen hoe gebeurtenissen in het Platform worden vastgelegd.

![](../images/user-guide/profiles-events.png)

### Tabblad Segmentlidmaatschap

Op het tabblad **[!UICONTROL Segment membership]** wordt een lijst weergegeven met de naam en beschrijving van de segmenten waartoe het individuele klantprofiel momenteel behoort. Deze lijst wordt automatisch bijgewerkt wanneer het profiel in aanmerking komt of vervalt vanuit segmenten. Het totale aantal segmenten waarvoor het profiel momenteel is gekwalificeerd, wordt aan de rechterkant van het tabblad weergegeven.

Voor meer informatie over segmentatie in Experience Platform, gelieve te verwijzen naar [de documentatie van de Dienst van de Segmentatie van het Experience Platform van Adobe](../../segmentation/home.md).

![](../images/user-guide/profiles-segment-membership.png)

## Beleid samenvoegen

Selecteer in het hoofdmenu **[!UICONTROL Profiles]** het tabblad **[!UICONTROL Merge Policies]** om een lijst weer te geven met samenvoegbeleidsregels die bij uw organisatie horen. Elk vermeld beleid toont zijn naam, al dan niet het standaardsamenvoegbeleid, en de schemaklasse die het op van toepassing is.

Zie [Overzicht van samenvoegingsbeleid](../merge-policies/overview.md) voor meer informatie over samenvoegingsbeleid.

![](../images/user-guide/profiles-merge-policies.png)

## Unieschema {#union-schema}

Selecteer in het hoofdmenu **[!UICONTROL Profiles]** het tabblad **[!UICONTROL Union Schema]** om de beschikbare samenvoegingsschema&#39;s voor uw opgenomen gegevens weer te geven. Een samenvoegingsschema is een samenvoeging van alle [!DNL Experience Data Model] (XDM) gebieden onder de zelfde klasse, de waarvan schema&#39;s voor gebruik in [!DNL Real-time Customer Profile] zijn toegelaten.

Voor meer informatie over verenigingsschema&#39;s, gelieve te bezoeken [verenigingsschema UI gids](union-schema.md).

![](../images/user-guide/profiles-union-schema.png)

## Volgende stappen

Door deze gids te lezen, weet u hoe te om de het profielgegevens van uw organisatie te bekijken en te beheren gebruikend de UI van het Experience Platform. Raadpleeg de handleiding [Real-time Customer Profile API](../api/overview.md) voor informatie over het werken met profielgegevens met Experience Platform-API&#39;s.
