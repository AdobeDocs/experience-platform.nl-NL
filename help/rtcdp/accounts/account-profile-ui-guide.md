---
keywords: rtcdp-profiel;profielen rtcdp;rtcdp-identiteiten;rtcdp-samenvoegingsbeleid;realtime klantprofiel
title: Gebruikersgids voor accountprofiel
description: Door het gebruik van accountprofielen kunt u met Adobe Real-time Customer Data Platform B2B Edition rekeninggegevens uit meerdere bronnen verenigen. Deze handleiding bevat informatie over het werken met accountprofielen in de gebruikersinterface van Adobe Experience Platform.
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
feature: Profiles, B2B
exl-id: a05e8b84-026e-4482-a288-aa25b441bd69
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 0%

---

# Gebruikersgids voor accountprofielen

>[!NOTE]
>
>Accountprofielen zijn alleen beschikbaar voor Real-time Customer Data Platform B2B Edition-klanten. Als u meer wilt weten over Real-Time CDP, inclusief de functies en functionaliteit die beschikbaar zijn voor elk type licentie, leest u eerst de [Real-Time CDP-overzicht](../overview.md).

Met accountprofielen kunt u accountgegevens uit meerdere bronnen verenigen. Deze verenigde mening van een rekening brengt gegevens van over uw vele marketing kanalen en de diverse systemen samen die uw organisatie momenteel gebruikt om de informatie van de klantenrekening op te slaan. Dit document biedt een gids voor interactie met accountprofielen met behulp van de Real-Time CDP- en B2B Edition-mogelijkheden die beschikbaar zijn in de gebruikersinterface van Adobe Experience Platform (UI).

Als u meer wilt weten over de manier waarop accountprofielen worden gemaakt als onderdeel van de B2B-workflow, raadpleegt u de [end-to-end zelfstudie](../b2b-tutorial.md).

## Overzicht van accountprofielen {#account-profiles-overview}

Selecteren **[!UICONTROL Profiles]** krachtens [!UICONTROL Accounts] in de linkernavigatie om het overzicht van accountprofielen weer te geven. Onder de [!UICONTROL Overview] op het dashboard wordt een afbeelding of diagram weergegeven waarin widgets in één ingangspunt worden weergegeven.

![Tabblad Overzicht waarin widgets worden weergegeven](images/b2b-account-profile-overview.png)

Zie de documentatie op de [[!UICONTROL Account Profiles]](../../dashboards/guides/account-profiles.md) dashboard voor meer informatie.

## Configureer lead in account matching {#configure-lead-to-account-matching}

>[!IMPORTANT]
>
> Alleen B2B AI-beheerders kunnen de &#39;lead to account matching&#39;-service inschakelen, uitschakelen en configureren. Wanneer u de service uitschakelt, worden de resultaten van de overeenkomst binnen 24 uur verwijderd.

Selecteer **[!UICONTROL Profiles]** krachtens [!UICONTROL Accounts] in de linkernavigatie. Op de **[!UICONTROL Overview]** tab, selecteert u **[!UICONTROL Settings]** rechtsboven.

![Instellingen selecteren](images/b2b-configuring-accounts-profile.png)

De **[!UICONTROL Account settings]** wordt geopend. Selecteer hier de **[!UICONTROL Enable lead-to-account-matching]** schakelen om de functie in te schakelen. Gebruik het vervolgkeuzemenu om **[!UICONTROL Daily]** voor de **[!UICONTROL Matching cadence]** instellen. Selecteer ten slotte de relevante **[!UICONTROL Matching criteria]** opties gevolgd door **[!UICONTROL Save]** om uw instellingen te bevestigen en terug te keren naar de **[!UICONTROL Account Profiles]** scherm.

>[!NOTE]
>
> Het adres kan niet als enige passende criteria worden gebruikt. Een of meer andere criteria moeten worden geselecteerd.

![Accountinstellingen configureren](images/b2b-configuring-account-settings.png)

Als u meer wilt weten over het maken van overeenkomsten met accounts, raadpleegt u de [Lood-aan-rekeningsovereenkomsten in Real-Time CDP B2B-overzicht](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

## Accountprofielen zoeken {#browse-account-profiles}

Als u door accountprofielen wilt bladeren, selecteert u eerst **[!UICONTROL Profiles]** krachtens [!UICONTROL Accounts] in de linkernavigatie.

Op de **[!UICONTROL Browse]** kunt u accountprofielen verkennen aan de hand van een account-id van een verbonden onderneming of door de brongegevens rechtstreeks in te voeren.

![Gebruik account-id om profielen te verkennen](images/b2b-account-browse-by.png)

### Bladeren op [!UICONTROL Connected enterprise source] {#browse-by-connected-enterprise-source}

Selecteer **[!UICONTROL Connected enterprise source]** van de **[!UICONTROL Browse by]** en vervolgens een verbonden bron kiezen met de selectieknop naast het dialoogvenster **[!UICONTROL Source]** veld.

![Door accountprofielen bladeren op basis van een verbonden ondernemingsbron](images/b2b-account-browse.png)

Hierdoor wordt het **[!UICONTROL Select source]** , waarin u een bron kunt selecteren op basis van de verbindingen die uw organisatie heeft gemaakt.

>[!NOTE]
>
>Uw organisatie kan veelvoudige bronnen hebben die voor de zelfde dienstverlener (bijvoorbeeld, Marketo) worden gevormd, zodat is het belangrijk om de verbindingsnaam, het bronsysteem, en de instantie van het bronsysteem te herzien om ervoor te zorgen u door de correcte broninstantie zoekt.

Raadpleeg voor meer informatie over het verbinden van bedrijfsbronnen de [overzicht van bronnen](../sources/sources-overview.md).

U kunt een bron kiezen door het keuzerondje naast de naam van de verbinding te selecteren en vervolgens **[!UICONTROL Select]** om terug te keren naar de [!UICONTROL Browse] tab.

![Bronworkflow selecteren](images/b2b-account-select-source.png)

Als er een bron is geselecteerd, moet u nu een **[!UICONTROL Account ID]** met betrekking tot de bron. Als u bijvoorbeeld een Salesforce-bron selecteert, moet u een account-id invoeren in de Salesforce-instantie om het accountprofiel weer te geven dat aan die id is gekoppeld.

>[!NOTE]
>
>Voor Marketo-account-id&#39;s zijn er twee mogelijke accounttabellen waarnaar kan worden verwezen. Daarom moet u een specifieke syntaxis gebruiken om ervoor te zorgen dat u de juiste account weergeeft.
>
>De meest voorkomende, standaardsyntaxis is de Marketo-account-id die wordt toegevoegd door `.mkto_org` (bijvoorbeeld `1234567.mkto_org`). Marketo Account-Based Marketing-klanten kunnen aanvullende waarden vinden met de Marketo-account-id die is toegevoegd door `.mkto_account`. Neem contact op met uw Marketo-beheerder als u niet zeker weet welke syntaxis u moet gebruiken.

![Selectie van account-id](images/b2b-account-browse-id.png)

### Bladeren op [!UICONTROL Others] {#browse-by-others}

Real-Time CDP, B2B Edition ondersteunt de mogelijkheid om een directe zoekopdracht uit te voeren door u toe te staan een **[!UICONTROL Source name]**, **[!UICONTROL Source instance]**, en **[!UICONTROL Account ID]** voor een account dat u wilt bekijken. Door de bronnaam en -instantie rechtstreeks in te voeren, geeft u de context op die Experience Platform nodig heeft om de juiste accountprofielgegevens te zoeken en weer te geven.

De mogelijkheid om een directe zoekopdracht uit te voeren is handig in omstandigheden waarin een bronverbinding rechtstreeks met de gegevens niet mogelijk is. Als uw organisatie bijvoorbeeld een beleid voor gegevensbeheer heeft dat directe verbinding met een CRM verhindert, kunt u die gegevens exporteren naar een systeem voor cloudopslag en deze vervolgens in Experience Platform opnemen.

Een ander voorbeeld zou kunnen zijn dat u een transformatie op de gegevens tussen de tijd uitvoert het een systeem verlaat en Platform ingaat. U kunt de directe raadplegingsfunctionaliteit gebruiken om context voor de gegevens te verstrekken (zoals specificerend dat het gegevens van Marketo is, ondanks het feit dat het uit een emmertje van Amazon S3, bijvoorbeeld) komt zodat het systeem weet waar te zoeken, en hoe te om behoorlijk terug te geven, de gegevens.

Als u een directe zoekopdracht wilt starten, selecteert u **[!UICONTROL Others]** van de **[!UICONTROL Browse by]** vervolgkeuzelijst, voert u vervolgens een **[!UICONTROL Source name]**, **[!UICONTROL Source instance]**, en **[!UICONTROL Account ID]** voor de account die u wilt bekijken.

![Bladeren door anderen](images/b2b-account-browse-adhoc.png)

## Accountprofieldetails weergeven {#view-account-profile-details}

Nadat u de **[!UICONTROL Browse]** om een accountprofiel te zoeken, selecteert u de optie **[!UICONTROL Profile ID]** opent de **[!UICONTROL Detail]** voor het accountprofiel. De profielgegevens die worden weergegeven op de **[!UICONTROL Detail]** tabblad is samengevoegd vanuit meerdere profielfragmenten om een enkele weergave van de afzonderlijke account te vormen. Dit omvat accountdetails zoals basiskenmerken en gegevens over sociale media.

De weergegeven standaardvelden kunnen ook op organisatorisch niveau worden gewijzigd om de voorkeurskenmerken van het accountprofiel weer te geven.

>[!NOTE]
>
>Er is een vergelijkbare functionaliteit beschikbaar voor klantprofielen en er is een stapsgewijze handleiding gemaakt met instructies voor het toevoegen en verwijderen van kenmerken, het wijzigen van het formaat van deelvensters, enzovoort. Lees de [handleiding voor het aanpassen van profieldetails](../../profile/ui/profile-customization.md) voor meer informatie.

![Accountprofieldetails weergeven](images/b2b-account-details.png)

U kunt aanvullende gegevens met betrekking tot de account weergeven door een andere beschikbare tabbladen te selecteren. Deze lusjes omvatten attributen, mensen, en het kansen lusje dat open en gesloten kansen met betrekking tot de rekening over uw ondernemingssystemen toont. Raadpleeg de volgende secties voor meer informatie over elk tabblad.

## Tabblad Kenmerken {#attributes-tab}

De **[!UICONTROL Attributes]** worden alle recordgegevens weergegeven die betrekking hebben op de account. Dit omvat kenmerkgegevens die afkomstig zijn van meerdere bronnen die samen zijn samengevoegd om één weergave van de account te vormen.

U kunt de gegevens niet alleen in een lijst weergeven, maar u kunt ook de zoekbalk gebruiken om te zoeken naar specifieke kenmerken of om de recordgegevens als JSON weer te geven.

![Tabblad Kenmerken](images/b2b-account-attributes.png)

## Het tabblad Personen {#people-tab}

De **[!UICONTROL People]** bevat een lijst met individuele personen die aan het account zijn gekoppeld. Deze mensen kunnen contacten en leiders van verschillende ondernemingssystemen zijn die door verschillende teams binnen uw organisatie worden beheerd, maar in Real-Time CDP, B2B Edition worden zij samen voorgesteld als één enkele lijst toelatend om een holistische mening van uw rekeningscontacten te zien.

>[!NOTE]
>
>De [!UICONTROL People] wordt een lijst weergegeven met maximaal 25 personen die zijn gekoppeld aan het account. Voor rekeningen met meer dan 25 geassocieerde personen toont het systeem een willekeurige steekproef van 25 records.

Naast het tonen van u een momentopname van informatie voor het contact, omvat elke vermelde persoon ook een **[!UICONTROL Profile ID]**, wat een klikbare verbinding is die u toestaat om het Profiel van de Klant in real time voor dat individu te onderzoeken. Voor meer informatie over het bekijken van individuele klantenprofielen met betrekking tot uw rekeningen, gelieve de gids voor [browserprofielen in Real-Time CDP, B2B Edition](../profile/profile-browse.md).

![Het tabblad Personen](images/b2b-account-people.png)

## Tabblad Kansen {#opportunities-tab}

De **[!UICONTROL Opportunities]** bevat informatie over open en afgesloten mogelijkheden met betrekking tot de account. Deze kansen kunnen in Experience Platform van veelvoudige bronnen worden opgenomen, nochtans maakt de Real-Time CDP, B2B Uitgave het voor marketers gemakkelijk om al deze kansen samen te zien op één plaats.

>[!NOTE]
>
>De [!UICONTROL Opportunities] wordt een lijst weergegeven met maximaal 25 mogelijkheden die aan de account zijn gekoppeld. Voor rekeningen met meer dan 25 bijbehorende kansen, toont het systeem een willekeurige steekproef van 25 verslagen.

Elke kans bevat informatie zoals de naam van de kans, de hoeveelheid kansen, het werkgebied en of de kans open, gesloten, gewonnen of verloren is.

![Tabblad Accountmogelijkheden](images/b2b-account-opportunities.png)

## Tabblad Verwante accounts {#related-accounts-tab}

De **[!UICONTROL Related accounts]** bevat informatie over andere accounts die mogelijk gerelateerd zijn aan de account waarin u bladert. Voor uitgebreide informatie over de functionaliteit leest u de [overzicht van verwante accounts](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

>[!NOTE]
>
>* Een groep Verwante accounts kan maximaal 30 accountprofielen hebben. Als er meer dan 30 accountprofielen met elkaar zijn gevonden, worden deze willekeurig in meerdere groepen opgedeeld, elk met niet meer dan 30 leden. De groep Verwante accounts van een accountprofiel bevat altijd zichzelf.
>* De [!UICONTROL Related accounts] wordt momenteel een lijst weergegeven met maximaal 25 verwante accounts die zijn gekoppeld aan het account waarin u bladert. Dit is een beperking die in een toekomstige update zal worden aangepakt. Ondanks deze UI-beperking worden bij gebruik van verwante accounts in segmentdefinities voor groepen van 30 gerelateerde accountprofielen alle profielen gebruikt voor het opgeven van doelen.

Elke verwante rekening omvat informatie zoals de identiteitskaart en de naam van het rekeningsprofiel, zijn de sleutel van de rekeningsbron, en verdere informatie met betrekking tot homepage, adres, ouderrekening, telefoon, industrie, en jaarlijkse opbrengst.

![Tabblad Verwante accounts](images/b2b-account-related-accounts.png)

U kunt de verwante accounts in deze lijst gebruiken voor segmentatiedoeleinden. Zie een [segmenteringsvoorbeeld](/help/rtcdp/segmentation/b2b.md#related-account) om te begrijpen hoe te om verwante rekeningen te gebruiken om uw bereik in segmentdefinities uit te breiden.