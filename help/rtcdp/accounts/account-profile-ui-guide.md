---
keywords: rtcdp-profiel;profielen rtcdp;rtcdp-identiteiten;rtcdp-samenvoegingsbeleid;realtime klantprofiel
title: Gebruikersgids voor accountprofiel
description: Via het gebruik van accountprofielen kunt u met Adobe Real-Time Customer Data Platform B2B edition accountgegevens uit meerdere bronnen verenigen. Deze handleiding bevat informatie over het werken met accountprofielen in de gebruikersinterface van Adobe Experience Platform.
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=nl-NL#rtcdp-editions" newtab=true
feature: Profiles, B2B
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 0%

---

# Gebruikersgids voor accountprofielen

>[!NOTE]
>
>Accountprofielen zijn alleen beschikbaar voor Real-Time Customer Data Platform B2B edition-klanten. Om meer over Real-Time CDP, met inbegrip van de eigenschappen en de functionaliteit beschikbaar aan elk vergunningstype te leren, gelieve te beginnen door het [&#x200B; overzicht van Real-Time CDP &#x200B;](../overview.md) te lezen.

Met accountprofielen kunt u accountgegevens uit meerdere bronnen verenigen. Deze verenigde mening van een rekening brengt gegevens van over uw vele marketing kanalen en de diverse systemen samen die uw organisatie momenteel gebruikt om de informatie van de klantenrekening op te slaan. Dit document biedt een handleiding voor interactie met accountprofielen met behulp van de Real-Time CDP- en B2B edition-mogelijkheden die beschikbaar zijn in de gebruikersinterface van Adobe Experience Platform (UI).

Om meer over te leren hoe de rekeningsprofielen als deel van het B2B- werkschema worden gecreeerd, te zien gelieve het [&#x200B; leerprogramma van begin tot eind &#x200B;](../b2b-tutorial.md).

## Overzicht van accountprofielen {#account-profiles-overview}

Selecteer **[!UICONTROL Profiles]** onder [!UICONTROL Accounts] in de linkernavigatie om het overzicht van accountprofielen weer te geven. Onder het tabblad [!UICONTROL Overview] ziet u op het dashboard een afbeelding of grafiek met widgets in één ingangspunt.

![&#x200B; het lusje van het Overzicht van de Profielen van de Rekening met Profielen in de linkernavigatie en benadrukt Overzicht.](images/b2b-account-profile-overview.png)

Raadpleeg de documentatie op het dashboard van [[!UICONTROL Account Profiles]](../../dashboards/guides/account-profiles.md) voor meer informatie. Zie de documentatie over [&#x200B; Real-time het gegevensmodel B2B edition &#x200B;](../../dashboards/data-models/cdp-insights-data-model-b2b.md) van de Gegevens van de Klant voor meer informatie over hoe uw modellen van inzichten gegevensmodellen kunnen worden gebruikt om douanegrafieken voor uw dashboards tot stand te brengen.

## Configureer lead in account matching {#configure-lead-to-account-matching}

>[!IMPORTANT]
>
> Alleen B2B AI-beheerders kunnen de &#39;lead to account matching&#39;-service inschakelen, uitschakelen en configureren. Wanneer u de service uitschakelt, worden de resultaten van de overeenkomst binnen 24 uur verwijderd.

Selecteer **[!UICONTROL Profiles]** onder [!UICONTROL Accounts] in de linkernavigatie om lead to account matching te configureren. Selecteer **[!UICONTROL Overview]** in de rechterbovenhoek op de tab **[!UICONTROL Settings]** .

![&#x200B; het lusje van het Overzicht van de Profielen van de Rekening met het Plaatsen benadrukte.](images/b2b-configuring-accounts-profile.png)

Het dialoogvenster **[!UICONTROL Account settings]** wordt geopend. Selecteer van hieruit de schakeloptie **[!UICONTROL Enable lead-to-account-matching]** om de functie in te schakelen. Selecteer in het vervolgkeuzemenu **[!UICONTROL Daily]** voor de instelling **[!UICONTROL Matching cadence]** . Selecteer ten slotte de relevante **[!UICONTROL Matching criteria]** -opties, gevolgd door **[!UICONTROL Save]** , om uw instellingen te bevestigen en terug te keren naar het **[!UICONTROL Account Profiles]** -scherm.

>[!NOTE]
>
> Het adres kan niet als enige passende criteria worden gebruikt. Een of meer andere criteria moeten worden geselecteerd.

![&#x200B; vorm de montages van de Rekening &#x200B;](images/b2b-configuring-account-settings.png)

Om meer over lood aan rekening aanpassing te leren, gelieve te verwijzen naar [&#x200B; Lood aan rekening die in het overzicht van Real-Time CDP B2B &#x200B;](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) past.

## Accountprofielen zoeken {#browse-account-profiles}

Als u door accountprofielen wilt bladeren, selecteert u eerst **[!UICONTROL Profiles]** onder [!UICONTROL Accounts] in de linkernavigatie.

Op het tabblad **[!UICONTROL Browse]** kunt u accountprofielen verkennen aan de hand van een account-id van een verbonden ondernemingsbron of door rechtstreeks brongegevens in te voeren.

![&#x200B; identiteitskaart van de Rekening van het Gebruik om profielen &#x200B;](images/b2b-account-browse-by.png) te onderzoeken

### Bladeren op [!UICONTROL Connected enterprise source] {#browse-by-connected-enterprise-source}

Als u door accountprofielen wilt bladeren op een verbonden ondernemingsbron, selecteert u **[!UICONTROL Connected enterprise source]** in het vervolgkeuzemenu **[!UICONTROL Browse by]** en kiest u vervolgens een verbonden bron met de selectieknop naast het veld **[!UICONTROL Source]** .

![&#x200B; doorblader rekeningsprofielen door verbonden ondernemingsbron &#x200B;](images/b2b-account-browse.png)

Hierdoor wordt het dialoogvenster **[!UICONTROL Select source]** geopend, waarin u een bron kunt selecteren op basis van de verbindingen die uw organisatie tot stand heeft gebracht.

>[!NOTE]
>
>Uw organisatie kan veelvoudige bronnen hebben die voor de zelfde dienstverlener (bijvoorbeeld, Marketo) worden gevormd, zodat is het belangrijk om de verbindingsnaam, het bronsysteem, en de instantie van het bronsysteem te herzien om ervoor te zorgen u door de correcte broninstantie zoekt.

Meer leren over het verbinden van ondernemingsbronnen, gelieve te verwijzen naar het [&#x200B; overzicht van bronnen &#x200B;](../sources/sources-overview.md).

U kunt een bron kiezen door het keuzerondje naast de naam van de verbinding te selecteren en vervolgens met **[!UICONTROL Select]** terug te keren naar het tabblad [!UICONTROL Browse] .

![&#x200B; Uitgezochte bronwerkschema &#x200B;](images/b2b-account-select-source.png)

Als er een bron is geselecteerd, moet u nu een **[!UICONTROL Account ID]** invoeren die betrekking heeft op de bron. Als u bijvoorbeeld een Salesforce-bron selecteert, moet u een account-id van het Salesforce-exemplaar invoeren om het aan die id gekoppelde accountprofiel weer te geven.

>[!NOTE]
>
>Voor Marketo-account-id&#39;s zijn er twee mogelijke accounttabellen waarnaar kan worden verwezen. Daarom moet u een specifieke syntaxis gebruiken om ervoor te zorgen dat u de juiste account weergeeft.
>
>De meest voorkomende, standaardsyntaxis is de Marketo-account-id die wordt toegevoegd door `.mkto_org` (bijvoorbeeld `1234567.mkto_org` ). Marketo Account-Based Marketing-klanten hebben mogelijk aanvullende waarden die u kunt vinden met de Marketo-account-id die is toegevoegd door `.mkto_account` . Neem contact op met uw Marketo-beheerder als u niet zeker weet welke syntaxis u moet gebruiken.

![&#x200B; selectie van identiteitskaart van de Rekening &#x200B;](images/b2b-account-browse-id.png)

### Bladeren op [!UICONTROL Others] {#browse-by-others}

Real-Time CDP, B2B edition ondersteunt de mogelijkheid om een directe zoekopdracht uit te voeren door u toe te staan een **[!UICONTROL Source name]** -, **[!UICONTROL Source instance]** - en **[!UICONTROL Account ID]** -account in te voeren voor een account dat u wilt bekijken. Door de bronnaam en -instantie rechtstreeks in te voeren, geeft u de context op die Experience Platform nodig heeft om de juiste accountprofielgegevens te zoeken en weer te geven.

De mogelijkheid om een directe zoekopdracht uit te voeren is handig in omstandigheden waarin een bronverbinding rechtstreeks met de gegevens niet mogelijk is. Als uw organisatie bijvoorbeeld een beleid voor gegevensbeheer heeft dat directe verbinding met een CRM voorkomt, kunt u die gegevens exporteren naar een systeem voor cloudopslag en deze vervolgens opnemen in Experience Platform.

Een ander voorbeeld is dat u de gegevens transformeert tussen het moment dat het systeem verlaat en Experience Platform binnengaat. U kunt de directe raadplegingsfunctionaliteit gebruiken om context voor de gegevens te verstrekken (zoals specificerend dat het gegevens van Marketo is, ondanks het feit dat het uit een emmertje van Amazon S3, bijvoorbeeld) komt zodat het systeem weet waar te zoeken, en hoe te om behoorlijk terug te geven, de gegevens.

Als u wilt beginnen met een directe zoekopdracht, selecteert u **[!UICONTROL Others]** in de vervolgkeuzelijst **[!UICONTROL Browse by]** en voert u vervolgens een **[!UICONTROL Source name]** , **[!UICONTROL Source instance]** en **[!UICONTROL Account ID]** in voor de account die u wilt weergeven.

![&#x200B; doorbladeren door anderen &#x200B;](images/b2b-account-browse-adhoc.png)

## Accountprofieldetails weergeven {#view-account-profile-details}

Als u op het tabblad **[!UICONTROL Browse]** een accountprofiel hebt gevonden en u **[!UICONTROL Profile ID]** selecteert, wordt het tabblad **[!UICONTROL Detail]** voor het accountprofiel geopend. De profielgegevens die op het tabblad **[!UICONTROL Detail]** worden weergegeven, zijn samengevoegd vanuit meerdere profielfragmenten tot één weergave van het individuele account. Dit omvat accountdetails zoals basiskenmerken en gegevens over sociale media.

De weergegeven standaardvelden kunnen ook op organisatorisch niveau worden gewijzigd om de voorkeurskenmerken van het accountprofiel weer te geven.

>[!NOTE]
>
>Er is een vergelijkbare functionaliteit beschikbaar voor klantprofielen en er is een stapsgewijze handleiding gemaakt met instructies voor het toevoegen en verwijderen van kenmerken, het wijzigen van het formaat van deelvensters, enzovoort. Gelieve te lezen de [&#x200B; gids van de profieldetail aanpassing &#x200B;](../../profile/ui/profile-customization.md) om meer te leren.

![&#x200B; de details van het rekeningsprofiel van de Mening &#x200B;](images/b2b-account-details.png)

U kunt aanvullende gegevens met betrekking tot de account weergeven door een andere beschikbare tabbladen te selecteren. Deze lusjes omvatten attributen, mensen, en het kansen lusje dat open en gesloten kansen met betrekking tot de rekening over uw ondernemingssystemen toont. Raadpleeg de volgende secties voor meer informatie over elk tabblad.

## Tabblad Kenmerken {#attributes-tab}

Op het tabblad **[!UICONTROL Attributes]** worden alle recordgegevens weergegeven die betrekking hebben op de account. Dit omvat kenmerkgegevens die afkomstig zijn van meerdere bronnen die samen zijn samengevoegd om één weergave van de account te vormen.

U kunt de gegevens niet alleen in een lijst weergeven, maar u kunt ook de zoekbalk gebruiken om te zoeken naar specifieke kenmerken of om de recordgegevens als JSON weer te geven.

![&#x200B; Attributen tabel &#x200B;](images/b2b-account-attributes.png)

## Het tabblad Personen {#people-tab}

Het tabblad **[!UICONTROL People]** bevat een lijst met individuele personen die aan het account zijn gekoppeld. Deze mensen kunnen contacten en leiders zijn van verschillende ondernemingssystemen die door verschillende teams binnen uw organisatie worden beheerd, maar in Real-Time CDP, B2B edition worden zij samen voorgesteld als één enkele lijst toelatend u om een meer holistische mening van uw rekeningscontacten te zien.

>[!NOTE]
>
>Op het tabblad [!UICONTROL People] wordt een lijst weergegeven met maximaal 25 personen die aan het account zijn gekoppeld. Voor rekeningen met meer dan 25 geassocieerde personen toont het systeem een willekeurige steekproef van 25 records.

Naast het tonen van u een momentopname van informatie voor het contact, omvat elke vermelde persoon ook een **[!UICONTROL Profile ID]**, die een klikbare verbinding is die u toestaat om het Real-Time Profiel van de Klant voor dat individu te onderzoeken. Om meer over het bekijken van individuele klantenprofielen met betrekking tot uw rekeningen te leren, te bezoeken gelieve de gids voor [&#x200B; het doorbladeren profielen in Real-Time CDP, B2B edition &#x200B;](../profile/profile-browse.md).

![&#x200B; Mensen tabel &#x200B;](images/b2b-account-people.png)

## Tabblad Kansen {#opportunities-tab}

Het tabblad **[!UICONTROL Opportunities]** bevat informatie over open en gesloten kansen voor de account. Deze mogelijkheden kunnen vanuit meerdere bronnen in Experience Platform worden benut, maar Real-Time CDP en B2B edition maken het voor de marketeers gemakkelijk om al deze mogelijkheden op één plaats samen te zien.

>[!NOTE]
>
>Op het tabblad [!UICONTROL Opportunities] wordt een lijst weergegeven met maximaal 25 mogelijkheden die aan het account zijn gekoppeld. Voor rekeningen met meer dan 25 bijbehorende kansen, toont het systeem een willekeurige steekproef van 25 verslagen.

Elke kans bevat informatie zoals de naam van de kans, de hoeveelheid kansen, het werkgebied en of de kans open, gesloten, gewonnen of verloren is.

![&#x200B; de kansen tabel van de Rekening &#x200B;](images/b2b-account-opportunities.png)

## Tabblad Verwante accounts {#related-accounts-tab}

Het tabblad **[!UICONTROL Related accounts]** bevat informatie over andere accounts die mogelijk verwant zijn aan de account waarin u bladert. Voor diepgaande informatie over de functionaliteit, lees het [&#x200B; verwante rekeningenoverzicht &#x200B;](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

>[!NOTE]
>
>* Een groep Verwante accounts kan maximaal 30 accountprofielen hebben. Als er meer dan 30 accountprofielen met elkaar zijn gevonden, worden deze willekeurig in meerdere groepen opgedeeld, elk met niet meer dan 30 leden. De groep Verwante accounts van een accountprofiel bevat altijd zichzelf.
>* Op het tabblad [!UICONTROL Related accounts] wordt momenteel een lijst weergegeven met maximaal 25 verwante accounts die zijn gekoppeld aan het account waarin u bladert. Dit is een beperking die in een toekomstige update zal worden aangepakt. Ondanks deze UI-beperking worden bij gebruik van verwante accounts in segmentdefinities voor groepen van 30 gerelateerde accountprofielen alle profielen gebruikt voor het opgeven van doelen.

Elke verwante rekening omvat informatie zoals de identiteitskaart en de naam van het rekeningsprofiel, zijn de sleutel van de rekeningsbron, en verdere informatie met betrekking tot homepage, adres, ouderrekening, telefoon, industrie, en jaarlijkse opbrengst.

![&#x200B; Verwante rekeningen tabel &#x200B;](images/b2b-account-related-accounts.png)

U kunt de verwante accounts in deze lijst gebruiken voor segmentatiedoeleinden. Zie a [&#x200B; segmentatievoorbeeld &#x200B;](/help/rtcdp/segmentation/b2b.md#related-account) om te begrijpen hoe te om verwante rekeningen te gebruiken om uw bereik in segmentdefinities uit te breiden.