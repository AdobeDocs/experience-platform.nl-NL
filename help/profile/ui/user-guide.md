---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;enable profile;Enable profile
solution: Adobe Experience Platform
title: Gebruikershandleiding voor het profiel van de klant in realtime
topic: guide
description: Het profiel van de Klant in real time leidt tot een holistische mening van elk van uw individuele klanten, die gegevens van veelvoudige kanalen met inbegrip van online, off-line, CRM, en derdegegevens combineren. Dit document fungeert als richtlijn voor de interactie met Real-time klantprofiel in de Adobe Experience Platform-gebruikersinterface.
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] gebruikershandleiding

[!DNL Real-time Customer Profile] leidt tot een holistische mening van elk van uw individuele klanten, die gegevens van veelvoudige kanalen met inbegrip van online, off-line, CRM, en derdegegevens combineren.

Dit document fungeert als richtlijn voor interactie met [!DNL Real-time Customer Profile] de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze gebruikershandleiding vereist inzicht in de verschillende [!DNL Experience Platform] services die bij het beheer van de software betrokken zijn [!DNL Real-time Customer Profiles]. Lees de documentatie voor de volgende services voordat u deze gebruikershandleiding leest:

* [[!DNL Real-time klantprofiel]](../home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Identity Service]](../../identity-service/home.md): Schakelt [!DNL Real-time Customer Profile] het overbruggen van identiteiten uit verschillende gegevensbronnen in wanneer deze worden ingepakt [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Platform] georganiseerd.

## Overzicht

Klik in [[!DNL Experience Platform UI]](http://platform.adobe.com)op **[!UICONTROL Profielen]** in de linkernavigatie om het tabblad **[!UICONTROL Overzicht]** te openen. Op dit tabblad vindt u koppelingen naar documentatie en video&#39;s die u helpen bij het begrijpen van profielen en het werken met profielen.

![](../images/user-guide/profiles-overview.png)

## Bladeren

Selecteer het tabblad **[!UICONTROL Bladeren]** om door profielen te bladeren op basis van identiteit.

![](../images/user-guide/profiles-browse.png)

### Profielafmetingen {#profile-metrics}

Aan de rechterkant van het tabblad **[!UICONTROL Bladeren]** staan verschillende belangrijke metingen voor uw profielgegevens, zoals het totale aantal [](#profile-count) profielen en een lijst met [profielen per naamruimte](#profiles-by-namespace).

Deze profielmetriek worden geëvalueerd gebruikend het standaardsamenvoegbeleid van uw organisatie. Voor meer informatie bij het werken met fusiebeleid, met inbegrip van hoe te om een standaardfusiebeleid te bepalen, zie de de gebruikersgids [van het Beleid van de](merge-policies.md)Fusie.

Naast deze metriek, verstrekt de sectie van profielmetriek ook een *Laatst bijgewerkte* datum en tijd, die tonen wanneer de metriek het laatst werden geëvalueerd.

![](../images/user-guide/profiles-profile-metrics.png)

### Aantal profielen {#profile-count}

Het aantal profielen geeft het totale aantal profielen weer dat uw organisatie binnen heeft [!DNL Experience Platform], nadat het standaardsamenvoegbeleid van uw organisatie profielfragmenten heeft samengevoegd tot één profiel voor elke individuele klant. Met andere woorden, uw organisatie kan veelvoudige profielfragmenten met betrekking tot één enkele klant hebben die met uw merk over verschillende kanalen interactie heeft, maar deze fragmenten zouden samen (volgens het standaard fusiebeleid) worden samengevoegd en een telling van &quot;1&quot;profiel terugkeren omdat zij allen met het zelfde individu verwant zijn.

Het aantal profielen omvat ook zowel profielen met kenmerken (recordgegevens) als profielen die alleen tijdreeksgegevens (gebeurtenisgegevens) bevatten, zoals Adobe Analytics-profielen. Het aantal profielen wordt regelmatig vernieuwd om een up-to-date totaal aantal profielen binnen Platform te verstrekken.

Wanneer de opname van records in de [!DNL Profile Store] telling met meer dan 5% verhoogt of verlaagt, wordt een baan teweeggebracht om de telling bij te werken. Voor het stromen gegevenswerkschema&#39;s, wordt een controle uitgevoerd op uurbasis om te bepalen als de 5% verhoging of dalingsdrempel is voldaan. Als dit het geval is, wordt er automatisch een taak geactiveerd om het aantal profielen bij te werken. Voor batch-opname wordt binnen 15 minuten na het correct innemen van een batch in de profielopslag een taak uitgevoerd om het aantal profielen bij te werken als aan de drempel van 5% verhoging of verlaging is voldaan.

### Profielen op naamruimte {#profiles-by-namespace}

Met de metrische waarde **[!UICONTROL Profielen op naamruimte]** worden het totale aantal naamruimten en de totale verdeling daarvan over alle samengevoegde profielen in uw profielarchief weergegeven. Het totale aantal profielen per naamruimte (d.w.z. het optellen van de waarden voor elke naamruimte) zal altijd hoger zijn dan de metrische waarde van het aantal profielen, omdat aan één profiel meerdere naamruimten kunnen zijn gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

Vergelijkbaar met de metrische waarde van het [profielaantal](#profile-count) , wanneer de opname van verslagen in de [!DNL Profile Store] toename of daling de telling met meer dan 5% verhoogt, wordt een baan teweeggebracht om de namespacemetriek bij te werken. Voor het stromen gegevenswerkschema&#39;s, wordt een controle uitgevoerd op uurbasis om te bepalen als de 5% verhoging of dalingsdrempel is voldaan. Als dit het geval is, wordt er automatisch een taak geactiveerd om het aantal profielen bij te werken. Voor batch-opname wordt binnen 15 minuten na het correct innemen van een batch in de batch een taak uitgevoerd [!DNL Profile Store]als aan de drempel van 5% voor verhogen of verlagen is voldaan, om de metriek bij te werken.

### Samenvoegbeleid

Met de **[!UICONTROL optie Samenvoegbeleid]** selecteren wordt automatisch het standaardsamenvoegbeleid voor uw organisatie geselecteerd. Als u dat samenvoegbeleid niet wilt gebruiken, kunt u het `X` naast het standaardsamenvoegbeleid selecteren om een dialoogvenster **[!UICONTROL Samenvoegbeleid]** selecteren te openen waarin u een ander samenvoegingsbeleid kunt kiezen. Raadpleeg de gebruikershandleiding [Beleid](merge-policies.md)samenvoegen voor meer informatie over samenvoegingsbeleid.

![](../images/user-guide/profiles-search-merge-policy.png)

### Naamruimte identiteit

Met de naamruimte **[!UICONTROL -kiezer]** Identiteit wordt een dialoogvenster geopend waarin u de naamruimte kunt kiezen waarmee u wilt zoeken. U kunt de kenmerken die worden weergegeven in de zoekopdracht aanpassen door het filterpictogram te selecteren en te kiezen welke kenmerken u wilt toevoegen of verwijderen.

![](../images/user-guide/profiles-search-filter.png)

Kies in het dialoogvenster Naamruimte **** selecteren de naamruimte waarin u wilt zoeken of gebruik de **[!UICONTROL zoekbalk]** in het dialoogvenster om de naam van een naamruimte te typen. U kunt een naamruimte selecteren om aanvullende details weer te geven. Nadat u de naamruimte hebt gevonden waarnaar u wilt zoeken, kunt u het keuzerondje selecteren en op **[!UICONTROL Selecteren]** drukken om door te gaan.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Identiteitswaarde

Nadat u een naamruimte **** Identiteit hebt geselecteerd, gaat u terug naar het tabblad **[!UICONTROL Bladeren]** waar u een waarde **** Identiteit kunt invoeren. Deze waarde is specifiek voor een individueel klantprofiel en moet een geldige waarde zijn voor de opgegeven naamruimte. Als u bijvoorbeeld de naamruimte **** Identiteit &quot;E-mail&quot; selecteert, hebt u een **[!UICONTROL identiteitswaarde]** nodig in de vorm van een geldig e-mailadres.

![](../images/user-guide/profiles-show-profile.png)

Nadat een waarde is ingevoerd, selecteert u Profiel **** tonen en geeft u één profiel weer dat overeenkomt met de waarde. Selecteer de **[!UICONTROL profiel-id]** om de profieldetails weer te geven.

![](../images/user-guide/profiles-display-profile.png)

### Profieldetails {#profile-detail}

Als u de **[!UICONTROL profiel-id]** selecteert, wordt het tabblad **[!UICONTROL Details]** geopend. Deze pagina bevat informatie over het geselecteerde profiel, zoals basiskenmerken, gekoppelde identiteiten en beschikbare contactkanalen. De weergegeven profielgegevens zijn samengevoegd vanuit meerdere profielfragmenten en vormen één weergave van de individuele klant.

![](../images/user-guide/profiles-profile-detail.png)

U kunt aanvullende informatie over het profiel weergeven, zoals **[!UICONTROL Kenmerken]**, **[!UICONTROL Gebeurtenissen]** en **[!UICONTROL Segmenten]** waarbij het profiel een lid is.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Beleid samenvoegen

Selecteer het tabblad **[!UICONTROL Samenvoegen van beleidsregels]** om een lijst weer te geven met samenvoegingsbeleid dat tot uw organisatie behoort. Elk vermeld beleid toont zijn naam, al dan niet het standaardsamenvoegbeleid, en het schema dat het op van toepassing is.

Voor meer informatie over fusiebeleid, zie de de gebruikersgids [van het Beleid van de](merge-policies.md)Fusie.

![](../images/user-guide/profiles-merge-policies.png)

## Unieschema

Selecteer het tabblad *Unieschema* om de samenvoegingsschema&#39;s voor uw [!DNL Profile Store]. Een verenigingsschema is een samenvoeging van alle [!DNL Experience Data Model] (XDM) gebieden onder de zelfde klasse, de waarvan schema&#39;s voor gebruik binnen zijn toegelaten [!DNL Real-time Customer Profile]. Selecteer een klasse in de linkerlijst om de structuur van zijn unieschema in het canvas te bekijken.

Als u bijvoorbeeld &quot;[!DNL XDM Profile]&quot; selecteert, wordt het samenvoegingsschema voor de [!DNL XDM Individual Profile] klasse weergegeven.

Zie de sectie over verenigingsschema&#39;s in de [schemacompositie gids](../../xdm/schema/composition.md) voor meer informatie over verenigingsschema&#39;s en hun rol in [!DNL Real-time Customer Profile].

![](../images/user-guide/profiles-union-schema.png)

## Volgende stappen

Door deze gids te lezen, weet u nu hoe te om uw [!DNL Profile] gegevens te bekijken en te beheren gebruikend [!DNL Experience Platform] UI. Voor informatie over hoe te hefboomwerking [!DNL Real-time Customer Profile] gegevens om publiekssegmenten te produceren, zie de documentatie [van de](../../segmentation/home.md)Segmentatie.