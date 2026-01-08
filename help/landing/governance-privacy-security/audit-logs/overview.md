---
title: Overzicht controlelogboeken
description: Leer hoe u met auditlogboeken kunt zien wie welke acties in Adobe Experience Platform heeft uitgevoerd.
role: Admin,Developer
feature: Audits
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: d6575e44339ea41740fa18af07ce5b893f331488
workflow-type: tm+mt
source-wordcount: '1579'
ht-degree: 3%

---

# Controlelogboeken {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="Bovenste handelingen"
>abstract="Deze widget geeft de belangrijkste soorten acties weer die binnen de geselecteerde tijdlijn in Experience Platform zijn uitgevoerd. Om de volledige lijst van geregistreerde acties in Experience Platform te zien, selecteer **Controles** in de linkernavigatie."

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="Belangrijkste gebruikers"
>abstract="Deze widget toont de gebruikers die de meeste handelingen in Experience Platform binnen de geselecteerde tijdlijn hebben uitgevoerd. Om de volledige lijst van geregistreerde acties in Experience Platform te zien, selecteer **Controles** in de linkernavigatie."

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="Gebruikersactiviteiten in Experience Platform controleren"
>abstract="<h2>Beschrijving</h2><p>U kunt de gebruikersactiviteit voor diverse Experience Platform-services en -mogelijkheden in de vorm van auditlogboeken controleren. Deze logboeken vormen een controletraject dat <b> registreert die </b> <b> uitvoerde wat </b> actie en <b> wanneer </b>. De logboeken van de controle kunnen helpen bij het oplossen van problemenkwesties op Experience Platform en helpen uw zaken effectief voldoen aan het beleid van het collectieve gegevensbeheer en regelgevende vereisten.</p>"

Om de transparantie en zichtbaarheid van de in het systeem uitgevoerde activiteiten te vergroten, kunt u in Adobe Experience Platform gebruikersactiviteiten voor verschillende services en mogelijkheden controleren in de vorm van &quot;auditlogs&quot;. Deze logboeken vormen een auditspoor dat kan helpen met het oplossen van problemenkwesties op Experience Platform, en uw zaken helpen effectief aan het beleid en de regelgevende vereisten van het collectieve gegevensbeheer voldoen.

In een fundamentele betekenis, vertelt een controlelogboek **wie** **uitvoerde wat** actie, en **wanneer**. Elke actie die in een logboek wordt geregistreerd bevat meta-gegevens die op het actietype, datum en tijd, e-mailidentiteitskaart van de gebruiker die de actie, en extra attributen relevant voor het actietype uitvoerde.

Wanneer een gebruiker een actie uitvoert, worden twee soorten controlegebeurtenissen geregistreerd. Een kerngebeurtenis legt het machtigingsresultaat van de handeling vast, [!UICONTROL allow] of [!UICONTROL deny] , terwijl een verbeterde gebeurtenis het resultaat van de uitvoering vastlegt, [!UICONTROL success] of [!UICONTROL failure] . Meerdere verbeterde gebeurtenissen kunnen aan dezelfde kerngebeurtenis worden gekoppeld. Wanneer u bijvoorbeeld een doel activeert, registreert de kerngebeurtenis de toestemming voor de handeling [!UICONTROL Destination Update] , terwijl de verbeterde gebeurtenissen meerdere [!UICONTROL Segment Activate] -handelingen opnemen.

>[!NOTE]
>
> De meta-gegevens voor de acties **voegen gebruiker** toe en **verwijderen gebruiker** binnen het **5&rbrace; middel van de Rol zal niet e-mailidentiteitskaart van de gebruiker bevatten die de actie uitvoerde.** In plaats daarvan worden in de logboeken de door het systeem gegenereerde e-mailadressen-id (system@adobe.com) weergegeven.

Dit document behandelt controlelogboeken in Experience Platform, met inbegrip van hoe te om hen in UI of API te bekijken en te beheren.

## Gebeurtenistypen die zijn vastgelegd in auditlogboeken {#category}

In de volgende tabel wordt aangegeven op welke acties de middelen in de auditlogboeken worden vastgelegd:

| Bron | Acties |
| --- | --- |
| [&#x200B; het controlebeleid van de Toegang (attribuut gebaseerd toegangsbeheer) &#x200B;](../../../access-control/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [&#x200B; Rekening (Adobe) &#x200B;](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [&#x200B; instantie van AI van de Attributie &#x200B;](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen</li><li>Uitschakelen</li></ul> |
| [&#x200B; Logboeken van de Controle &#x200B;](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>Exporteren</li></ul> |
| [&#x200B; Klasse &#x200B;](../../../xdm/schema/composition.md#class) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| Berekend kenmerk | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [&#x200B; de instantie van AI van de Klant &#x200B;](../../../intelligent-services/customer-ai/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen</li><li>Uitschakelen</li></ul> |
| [&#x200B; Dataset &#x200B;](../../../catalog/datasets/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Laat voor [&#x200B; in real time het Profiel van de Klant &#x200B;](../../../profile/home.md) toe</li><li>Uitschakelen voor profiel</li><li>Gegevens toevoegen</li><li>Batch verwijderen</li></ul> |
| [&#x200B; DataStream &#x200B;](../../../datastreams/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen</li><li>Uitschakelen</li><li>[&#x200B; geef Toewijzing &#x200B;](../../../datastreams/data-prep.md) uit</li></ul> |
| [Datatypen](../../../xdm/schema/composition.md#data-type) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [&#x200B; Doel &#x200B;](../../../destinations/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen</li><li>Uitschakelen</li><li>Gegevensset activeren</li><li>Gegevensset verwijderen</li><li>Profiel activeren</li><li>Profiel verwijderen</li></ul> |
| [&#x200B; de groep van het Gebied &#x200B;](../../../xdm/schema/composition.md#field-group) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [&#x200B; grafiek van de Identiteit &#x200B;](../../../identity-service/features/identity-graph-viewer.md) | <ul><li>Weergave</li></ul> |
| [&#x200B; Identiteitsnaamruimte &#x200B;](../../../identity-service/features/namespaces.md) | <ul><li>Maken</li><li>Bijwerken</li></ul> |
| [&#x200B; beleid van de Fusie &#x200B;](../../../profile/merge-policies/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [&#x200B; profiel van het Product &#x200B;](../../../access-control/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Query](../../../query-service/ui/overview.md) | <ul><li>Uitvoeren</li></ul> |
| [&#x200B; malplaatje van de Vraag &#x200B;](../../../query-service/ui/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [&#x200B; Rol (attribuut gebaseerd toegangsbeheer) &#x200B;](../../../access-control/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Gebruiker toevoegen</li><li>Gebruiker verwijderen</li></ul> |
| [&#x200B; Sandbox &#x200B;](../../../sandboxes/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Herstellen</li><li>Verwijderen</li></ul> |
| [&#x200B; Geplande vraag &#x200B;](../../../query-service/ui/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [&#x200B; Schema &#x200B;](../../../xdm/schema/composition.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen voor profiel</li></ul> |
| [&#x200B; Segment &#x200B;](../../../segmentation/home.md) | <ul><li>Maken</li><li>Verwijderen</li><li>Segment activeren</li><li>Segment verwijderen</li></ul> |
| [&#x200B; de gegevensstroom van Source &#x200B;](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen</li><li>Uitschakelen</li><li>Dataset activeren</li><li>Gegevensset verwijderen</li><li>Profiel activeren</li><li>Profiel verwijderen</li></ul> |
| [&#x200B; orde van het Werk &#x200B;](../../../hygiene/home.md) | <ul><li>Maken</li></ul> |

## Toegang tot auditlogboeken

Wanneer de eigenschap voor uw organisatie wordt toegelaten, worden de controlelogboeken automatisch verzameld aangezien de activiteit voorkomt. U te hoeven niet om logboekinzameling manueel toe te laten.

Als u controlelogboeken wilt weergeven en exporteren, moet u de toegangsbeheermachtiging van **[!UICONTROL View User Activity Log]** hebben (deze kunt u vinden onder de categorie [!UICONTROL Data Governance] ). Leren hoe te om individuele toestemmingen voor de eigenschappen van Experience Platform te beheren, gelieve te verwijzen naar de [&#x200B; documentatie van de toegangscontrole &#x200B;](../../../access-control/home.md).

## Het beheren van controlelogboeken in UI {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="Instructies"
>abstract="<ul><li>Selecteer <b> Controles </b> in de linkernavigatie. De werkruimte Audits toont een lijst van geregistreerde logboeken, door gebrek dat van meest recente aan minst recente wordt gesorteerd.</li>   <li> OPMERKING: auditlogboeken worden 365 dagen bewaard waarna ze uit het systeem worden verwijderd. Daarom kun je slechts 365 dagen teruggaan. Als u terug op gegevens moet kijken ouder dan 365 dagen, zou u logboeken bij een regelmatige kring moeten uitvoeren om aan uw interne beleidsvereisten te voldoen. </li><li>Selecteer een gebeurtenis in de lijst om de details in de rechtertrack weer te geven. </li><li>Selecteer het funnel-pictogram om een lijst met filterbesturingselementen weer te geven om de resultaten te beperken. Alleen de laatste 1000 records worden weergegeven, ongeacht de geselecteerde filters. </li><li>Om de huidige lijst van controlelogboeken uit te voeren, selecteer **logboek van de Download**.</li><li>Voor meer hulp met deze eigenschap, zie het <a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=nl-NL"> overzicht van controlelogboeken </a> op Experience League.</li></ul>"

U kunt controlelogboeken voor verschillende Experience Platform-functies weergeven in de **[!UICONTROL Audits]** -werkruimte in de Experience Platform-gebruikersinterface. De werkruimte bevat een lijst met opgenomen logbestanden, die standaard van de meest recente naar de minst recente logbestanden worden gesorteerd.

![&#x200B; het dashboard van Audits die Audits in het linkermenu benadrukken.](../../images/audit-logs/audits.png)

Auditlogboeken worden 365 dagen bewaard waarna ze uit het systeem worden verwijderd. Als u gegevens van meer dan 365 dagen vereist, zou u logboeken bij een regelmatige kast moeten uitvoeren om aan uw interne beleidsvereisten te voldoen.

Uw methode om controlelogboeken te verzoeken verandert de toegestane tijdspanne en het aantal verslagen u toegang tot zult hebben. [&#x200B; het Uitvoeren logboeken &#x200B;](#export-audit-logs) staat u toe om terug 365 dagen (in 90 dagintervallen) naar een maximum van 10.000 controlelogboeken (of kern of verbeterd) te gaan, waar aangezien [&#x200B; activiteitenlogboek UI &#x200B;](#filter-audit-logs) in Experience Platform de afgelopen 90 dagen aan een maximum van 1000 kerngebeurtenissen toont, elk van hen met de overeenkomstige verbeterde gebeurtenissen.

Selecteer een gebeurtenis in de lijst om de details in de rechtertrack weer te geven.

![&#x200B; het logboeklusje van de Activiteit van het dashboard van Audits met het benadrukte paneel van gebeurtenisdetails.](../../images/audit-logs/select-event.png)

### Controllerlogboeken filteren

Selecteer het pictogram van funnel (![&#x200B; pictogram van de Filter &#x200B;](/help/images/icons/filter.png)) om een lijst van filtercontroles te tonen om smalle resultaten te helpen.

>[!NOTE]
>
>In de gebruikersinterface van Experience Platform worden alleen de afgelopen 90 dagen maximaal 1000 kerngebeurtenissen weergegeven, elk met de bijbehorende verbeterde gebeurtenissen, ongeacht de toegepaste filters. Als u logboeken voorbij nodig hebt dat (tot een maximum van 365 dagen), zult u uw controlelogboeken [&#x200B; moeten uitvoeren &#x200B;](#export-audit-logs).

![&#x200B; het dashboard van Audits met het gefiltreerde benadrukte activiteitenlogboek.](../../images/audit-logs/filters.png)

De volgende filters zijn beschikbaar voor controlegebeurtenissen in UI:

| Filter | Beschrijving |
| --- | --- |
| [!UICONTROL Category] | Gebruik dropdown menu aan filter getoonde resultaten door [&#x200B; categorie &#x200B;](#category). |
| [!UICONTROL Action] | Filteren op handeling. De acties beschikbaar voor elke dienst kunnen in de middellijst hierboven worden gezien. |
| [!UICONTROL User] | Voer de volledige gebruikersnaam in (bijvoorbeeld `johndoe@acme.com` ) om te filteren op gebruiker. |
| [!UICONTROL Status] | De controlegebeurtenissen van de filter door resultaat: succesvol, ontbroken, toegestaan of ontkend toe te schrijven aan gebrek aan [&#x200B; toegangsbeheer &#x200B;](../../../access-control/home.md) toestemmingen. Voor een uitgevoerde actie, tonen de kerngebeurtenissen [!UICONTROL Allow] of [!UICONTROL Deny]. Wanneer de kerngebeurtenis [!UICONTROL Allow] is, heeft deze mogelijk een of meer verbeterde gebeurtenissen met **[!UICONTROL Success]** of **[!UICONTROL Failure]** gekoppeld. Een geslaagde actie toont bijvoorbeeld [!UICONTROL Allow] op de kerngebeurtenis en [!UICONTROL Success] op de bijgevoegde verbeterde gebeurtenis. |
| [!UICONTROL Date] | Selecteer een begindatum en/of een einddatum om een datumbereik te definiëren waarop de resultaten moeten worden gefilterd. De gegevens kunnen met een raadplegingsperiode van 90 dagen worden uitgevoerd (bijvoorbeeld, 2021-12-15 aan 2022-03-15). Dit kan per gebeurtenistype verschillen. |

Als u een filter wilt verwijderen, selecteert u de &quot;X&quot; op het vulpictogram voor het desbetreffende filter of selecteert u **[!UICONTROL Clear all]** om alle filters te verwijderen.

![&#x200B; het dashboard van Audits met duidelijke benadrukte filter.](../../images/audit-logs/clear-filters.png)

De teruggekeerde gegevens van het controlelogboek bevatten de volgende informatie over alle vragen die aan uw gekozen filtercriteria voldoen.

| Kolomnaam | Beschrijving |
|---|---|
| [!UICONTROL Timestamp] | De exacte datum en tijd van de actie die in een `month/day/year hour:minute AM/PM` -indeling wordt uitgevoerd. |
| [!UICONTROL Asset Name] | De waarde voor het veld [!UICONTROL Asset Name] is afhankelijk van de categorie die als filter is gekozen. |
| [!UICONTROL Category] | Dit veld komt overeen met de categorie die is geselecteerd in de vervolgkeuzelijst met filters. |
| [!UICONTROL Action] | Welke acties beschikbaar zijn, is afhankelijk van de categorie die u als filter hebt gekozen. |
| [!UICONTROL User] | Dit veld bevat de gebruikersnaam die de query heeft uitgevoerd. |

![&#x200B; het dashboard van Audits met het gefiltreerde benadrukte activiteitenlogboek.](../../images/audit-logs/filtered.png)

### Controleverslagen exporteren {#export-audit-logs}

Selecteer **[!UICONTROL Download log]** als u de huidige lijst met auditlogs wilt exporteren.

>[!NOTE]
>
>Logbestanden kunnen in het verleden worden aangevraagd met tussenpozen van 90 dagen tot 365 dagen. Nochtans, is de maximumhoeveelheid logboeken die tijdens één enkele uitvoer kan zijn teruggekeerd 10.000 controlegebeurtenissen (of kern of verbeterd).

![&#x200B; het dashboard van Audits met [!UICONTROL Download log] benadrukte.](../../images/audit-logs/download.png)

Selecteer in het dialoogvenster dat wordt weergegeven de gewenste indeling (**[!UICONTROL CSV]** of **[!UICONTROL JSON]** ) en selecteer vervolgens **[!UICONTROL Download]** . De browser downloadt het gegenereerde bestand en slaat het op uw computer op.

![&#x200B; de dialoog van de dossierformaatselectie met [!UICONTROL Download] benadrukt.](../../images/audit-logs/select-download-format.png)

## Waarschuwingen inschakelen {#enable-alerts}

U kunt controlealarm toelaten om berichten voor de volgende regels te ontvangen:

* Doelgroep maken
* Doelgroep bijwerken
* Doelgroep verwijderen
* Dataset maken
* Dataset bijwerken
* Dataset verwijderen
* Schema maken
* Schema bijwerken
* Schema verwijderen

Selecteer in de lijst de gewenste waarschuwing om u te abonneren op de ontvangst van berichten. Voor meer informatie over alarm, zie de gids op [&#x200B; het intekenen aan alarm gebruikend UI &#x200B;](../../../observability/alerts/ui.md).

## Controlelogbestanden beheren in de API

Alle acties die u in UI kunt uitvoeren kunnen ook worden gedaan gebruikend API vraag. Zie het [&#x200B; API verwijzingsdocument &#x200B;](https://www.adobe.io/experience-platform-apis/references/audit-query/) voor meer informatie.

## Controlelogbestanden voor Adobe Admin Console beheren

Leren hoe te om controlelogboeken voor activiteiten in Adobe Admin Console te beheren, verwijs naar het volgende [&#x200B; document &#x200B;](https://helpx.adobe.com/nl/enterprise/using/audit-logs.html).

## Volgende stappen en extra bronnen

In deze handleiding wordt beschreven hoe u de auditlogs in Experience Platform kunt beheren. Voor meer informatie over hoe te om de activiteiten van Experience Platform te controleren, zie de documentatie over [&#x200B; de Inzichten van de Waarneming &#x200B;](../../../observability/home.md) en [&#x200B; controle gegevensopname &#x200B;](../../../ingestion/quality/monitor-data-ingestion.md).

Bekijk de volgende video om meer inzicht te krijgen in auditlogs in Experience Platform:

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
