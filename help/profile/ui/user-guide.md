---
keywords: Experience Platform;profiel;real-time klantprofiel;problemen;API;verenigd profiel;verenigd profiel;verenigd profiel;profiel;rtcp;inschakelen profiel;Inschakelen profiel;Unieschema;UNION-PROFIEL;vakbondsprofiel
title: Gebruikershandleiding voor gebruikersprofiel in realtime
topic-legacy: guide
description: Het profiel van de Klant in real time leidt tot een holistische mening van elk van uw individuele klanten, die gegevens van veelvoudige kanalen met inbegrip van online, off-line, CRM, en derdegegevens combineren. Dit document fungeert als richtlijn voor de interactie met Real-time klantprofiel in de Adobe Experience Platform-gebruikersinterface.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] UI-hulplijn

[!DNL Real-time Customer Profile] leidt tot een holistische mening van elk van uw individuele klanten, die gegevens van veelvoudige kanalen met inbegrip van online, off-line, CRM, en derdegegevens combineren. Dit document fungeert als richtlijn voor interactie met [!DNL Real-time Customer Profile]-gegevens in de gebruikersinterface van Adobe Experience Platform (UI).

## Aan de slag

Deze UI-gids vereist inzicht in de verschillende [!DNL Experience Platform] services betrokken bij het beheer van [!DNL Real-time Customer Profiles]. Voordat u deze handleiding leest of in de gebruikersinterface werkt, raadpleegt u de documentatie voor de volgende services:

* [[!DNL Real-time Customer Profile]](../home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Identity Service]](../../identity-service/home.md): Schakelt  [!DNL Real-time Customer Profile] door het overbruggen van identiteiten uit verschillende gegevensbronnen in terwijl ze worden opgenomen in  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Platform] klantenervaring worden georganiseerd.

## Overzicht

Selecteer **[!UICONTROL Profiles]** in de linkernavigatie in de interface van het Experience Platform om het tabblad **[!UICONTROL Overview]** te openen. Op dit tabblad vindt u koppelingen naar documentatie en video&#39;s die u helpen bij het begrijpen van profielen en het werken met profielen.

![](../images/user-guide/profiles-overview.png)

### (Alfa) Profieldashboard

>[!IMPORTANT]
>
>De dashboardfunctionaliteit bevindt zich momenteel in alfa en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Voor sommige gebruikers bevat het selecteren van **[!UICONTROL Profiles]** in de linkernavigatie en het openen van het tabblad **[!UICONTROL Overview]** een dashboard met een overzicht van de belangrijkste maatstaven voor de profielgegevens.

Voor meer informatie gaat u naar de [dashboardhulplijn van het profiel](profile-dashboard.md).

## Bladeren

Selecteer het tabblad **[!UICONTROL Browse]** om door profielen te bladeren op identiteit.

![](../images/user-guide/profiles-browse.png)

### Profielmetriek {#profile-metrics}

Rechts op het tabblad **[!UICONTROL Browse]** staan verschillende belangrijke metriek voor uw profielgegevens, zoals het totale aantal [profielen](#profile-count) en een lijst met [profielen door naamruimte](#profiles-by-namespace).

Deze profielmetriek worden geëvalueerd gebruikend het standaardsamenvoegbeleid van uw organisatie. Voor meer informatie bij het werken met fusiebeleid, met inbegrip van hoe te om een standaard fusiebeleid te bepalen, zie [de gebruikersgids van het Beleid van de Fusie](merge-policies.md).

Naast deze metriek, verstrekt de sectie van profielmetriek ook een laatste bijgewerkte datum en tijd, die tonen wanneer de metriek het laatst werden geëvalueerd.

![](../images/user-guide/profiles-profile-metrics.png)

### Aantal profielen {#profile-count}

Het aantal profielen geeft het totale aantal profielen weer dat uw organisatie binnen [!DNL Experience Platform] heeft, nadat het standaardsamenvoegbeleid van uw organisatie profielfragmenten heeft samengevoegd tot één enkel profiel voor elke individuele klant. Met andere woorden, uw organisatie kan veelvoudige profielfragmenten met betrekking tot één enkele klant hebben die met uw merk over verschillende kanalen interactie heeft, maar deze fragmenten zouden samen (volgens het standaard fusiebeleid) worden samengevoegd en een telling van &quot;1&quot;profiel terugkeren omdat zij allen met het zelfde individu verwant zijn.

Het aantal profielen omvat ook zowel profielen met kenmerken (recordgegevens) als profielen die alleen tijdreeksgegevens (gebeurtenisgegevens) bevatten, zoals Adobe Analytics-profielen. Het aantal profielen wordt regelmatig vernieuwd om een up-to-date totaal aantal profielen binnen Platform te verstrekken.

Wanneer de opname van verslagen in [!DNL Profile] opslag de telling met meer dan 5% verhoogt of vermindert, wordt een baan teweeggebracht om de telling bij te werken. Voor het stromen gegevenswerkschema&#39;s, wordt een controle uitgevoerd op uurbasis om te bepalen als de 5% verhoging of dalingsdrempel is voldaan. Als dit het geval is, wordt er automatisch een taak geactiveerd om het aantal profielen bij te werken. Voor batch-opname wordt binnen 15 minuten na het correct innemen van een batch in de profielopslag een taak uitgevoerd om het aantal profielen bij te werken als aan de drempel van 5% verhoging of afname is voldaan.

### Profielen op naamruimte {#profiles-by-namespace}

De metrische **[!UICONTROL Profiles by namespace]** toont het totale aantal en de verdeling van namespaces over alle samengevoegde profielen in uw Opslag van het Profiel. Het totale aantal profielen per naamruimte (d.w.z. het optellen van de waarden voor elke naamruimte) zal altijd hoger zijn dan de metrische waarde van het aantal profielen, omdat aan één profiel meerdere naamruimten kunnen zijn gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

Vergelijkbaar met de [profieltelling](#profile-count) metrisch, wanneer de opname van verslagen in [!DNL Profile] opslag de telling met meer dan 5% verhoogt of vermindert, wordt een baan teweeggebracht om de namespacemetriek bij te werken. Voor het stromen gegevenswerkschema&#39;s, wordt een controle uitgevoerd op uurbasis om te bepalen als de 5% verhoging of dalingsdrempel is voldaan. Als dit het geval is, wordt er automatisch een taak geactiveerd om het aantal profielen bij te werken. Voor batch-opname wordt binnen 15 minuten nadat een batch in de [!DNL Profile]-winkel is opgenomen, een taak uitgevoerd om de metriek bij te werken als aan de drempel van 5% verhoging of verlaging is voldaan.

### Samenvoegbeleid

Met de kiezer **[!UICONTROL Merge policy]** wordt automatisch het standaardsamenvoegbeleid voor uw organisatie geselecteerd. Als u dat samenvoegbeleid niet wilt gebruiken, kunt u `X` naast het standaardsamenvoegbeleid selecteren om het **[!UICONTROL Select merge policy]** dialoogvenster te openen waarin u een ander samenvoegbeleid kunt kiezen.

Meer over samenvoegingsbeleid en hun rol binnen Platform leren, zie [beleidsgids UI](merge-policies.md) samenvoegen.

![](../images/user-guide/profiles-search-merge-policy.png)

### Naamruimte identiteit

Met de kiezer **[!UICONTROL Identity namespace]** wordt een dialoogvenster geopend waarin u de naamruimte kunt kiezen waarmee u wilt zoeken. U kunt de kenmerken die worden weergegeven in de zoekopdracht aanpassen door het filterpictogram te selecteren en te kiezen welke kenmerken u wilt toevoegen of verwijderen.

![](../images/user-guide/profiles-search-filter.png)

Kies in het dialoogvenster **[!UICONTROL Select identity namespace]** de naamruimte waarin u wilt zoeken of gebruik de zoekbalk in het dialoogvenster om de naam van een naamruimte te typen. U kunt een naamruimte selecteren om aanvullende details weer te geven. Nadat u de naamruimte hebt gevonden die u wilt gebruiken, kunt u het keuzerondje selecteren en op **[!UICONTROL Select]** drukken om door te gaan.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Identiteitswaarde

Nadat u een naamruimte voor identiteit hebt geselecteerd, gaat u terug naar het tabblad **[!UICONTROL Browse]** waar u een **[!UICONTROL Identity value]** kunt invoeren. Deze waarde is specifiek voor een individueel klantprofiel en moet een geldige waarde zijn voor de opgegeven naamruimte. Als u bijvoorbeeld de naamruimte E-mail selecteert, hebt u een identiteitswaarde nodig in de vorm van een geldig e-mailadres.

![](../images/user-guide/profiles-show-profile.png)

Wanneer een waarde is ingevoerd, selecteert u **[!UICONTROL Show profile]** en geeft u één profiel dat overeenkomt met de waarde. Selecteer **[!UICONTROL Profile ID]** om de profieldetails te bekijken.

![](../images/user-guide/profiles-display-profile.png)

### Profieldetails {#profile-detail}

Als u **[!UICONTROL Profile ID]** selecteert, wordt het tabblad **[!UICONTROL Detail]** geopend. De profielgegevens die op het tabblad **[!UICONTROL Detail]** worden weergegeven, zijn samengevoegd vanuit meerdere profielfragmenten en vormen één weergave van de individuele klant. Dit omvat klantgegevens zoals basiskenmerken, gekoppelde identiteiten en kanaalvoorkeuren. De weergegeven standaardvelden kunnen ook op organisatorisch niveau worden gewijzigd om de voorkeursprofielkenmerken weer te geven. Lees de [handleiding voor het aanpassen van profieldetails](profile-customization.md) voor meer informatie over het aanpassen van deze velden, inclusief stapsgewijze instructies voor het toevoegen en verwijderen van kenmerken en het wijzigen van het formaat van dashboarddeelvensters.

![](../images/user-guide/profiles-profile-detail.png)

U kunt aanvullende informatie over het afzonderlijke profiel weergeven door een andere beschikbare tabbladen te selecteren. Deze lusjes omvatten attributen, gebeurtenissen, en segmentlidmaatschap, die de segmenten tonen waarvoor het profiel momenteel gekwalificeerd is.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Beleid samenvoegen

Selecteer in het hoofdmenu **[!UICONTROL Profiles]** het tabblad **[!UICONTROL Merge Policies]** om een lijst weer te geven met samenvoegbeleidsregels die bij uw organisatie horen. Elk vermeld beleid toont zijn naam, al dan niet het standaardsamenvoegbeleid, en de schemaklasse die het op van toepassing is.

Voor meer informatie over fusiebeleid, zie [beleidsgids UI](merge-policies.md) samenvoegen.

Meer over het werken met fusiebeleid gebruikend Real-time het Profiel van de Klant API, gelieve te verwijzen naar [de gids ](../api/merge-policies.md) van het de eindpunt van samenvoegingsbeleid.

![](../images/user-guide/profiles-merge-policies.png)

## Unieschema {#union-schema}

Selecteer in het hoofdmenu **[!UICONTROL Profiles]** het tabblad **[!UICONTROL Union Schema]** om de beschikbare samenvoegingsschema&#39;s voor uw opgenomen gegevens weer te geven. Een samenvoegingsschema is een samenvoeging van alle [!DNL Experience Data Model] (XDM) gebieden onder de zelfde klasse, de waarvan schema&#39;s voor gebruik in [!DNL Real-time Customer Profile] zijn toegelaten.

Voor meer informatie over verenigingsschema&#39;s, gelieve te bezoeken [verenigingsschema UI gids](union-schema.md).

![](../images/user-guide/profiles-union-schema.png)

## Volgende stappen

Door deze gids te lezen, weet u nu hoe te om uw [!DNL Profile] gegevens te bekijken en te beheren gebruikend [!DNL Experience Platform] UI. Raadpleeg de [Handleiding voor ontwikkelaars van profielen](../api/overview.md) voor informatie over het werken met profielgegevens met de Real-time Customer Profile API.
