---
title: Overzicht controlelogboeken
description: Leer hoe u met auditlogboeken kunt zien wie welke acties in Adobe Experience Platform heeft uitgevoerd.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: 7ae5e9dc79b4e1f08d2bf98876b02db1967ccbe1
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 4%

---

# Controlelogboeken {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="Bovenste handelingen"
>abstract="Deze widget toont de belangrijkste soorten acties die in het Experience Platform zijn uitgevoerd binnen het geselecteerde tijdkader. Om de volledige lijst van geregistreerde acties in Platform te zien, selecteer **Controles** in de linkernavigatie."

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="Belangrijkste gebruikers"
>abstract="Deze widget geeft de gebruikers weer die de meeste handelingen in het Experience Platform binnen de geselecteerde tijdlijn hebben uitgevoerd. Om de volledige lijst van geregistreerde acties in Platform te zien, selecteer **Controles** in de linkernavigatie."

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="Gebruikersactiviteiten in het platform bewaken"
>abstract="<h2>Beschrijving</h2><p>U kunt gebruikersactiviteit voor diverse diensten en mogelijkheden van het Platform in de vorm van controlelogboeken controleren. Deze logboeken vormen een controletraject dat <b> registreert die </b> <b> uitvoerde wat </b> actie en <b> wanneer </b>. De logboeken van de controle kunnen helpen bij het oplossen van problemenkwesties op Platform en helpen uw zaken effectief voldoen aan het beleid van het collectieve gegevensbeheer en regelgevende vereisten.</p>"

Om de transparantie en zichtbaarheid van de in het systeem uitgevoerde activiteiten te vergroten, kunt u in Adobe Experience Platform gebruikersactiviteiten voor verschillende services en mogelijkheden controleren in de vorm van &quot;auditlogs&quot;. Deze logboeken vormen een auditspoor dat met het oplossen van problemenkwesties op Platform kan helpen, en uw zaken helpen effectief aan het beleid van het collectieve gegevensbeheer en regelgevende vereisten voldoen.

In een fundamentele betekenis, vertelt een controlelogboek **wie** **uitvoerde wat** actie, en **wanneer**. Elke actie die in een logboek wordt geregistreerd bevat meta-gegevens die op het actietype, datum en tijd, e-mailidentiteitskaart van de gebruiker die de actie, en extra attributen relevant voor het actietype uitvoerde.

Dit document behandelt controlelogboeken in Platform, met inbegrip van hoe te om hen in UI of API te bekijken en te beheren.

## Gebeurtenistypen die zijn vastgelegd in auditlogboeken {#category}

In de volgende tabel wordt aangegeven op welke acties de middelen in de auditlogboeken worden vastgelegd:

| Bron | Acties |
| --- | --- |
| [ het controlebeleid van de Toegang (attribuut gebaseerd toegangsbeheer) ](../../../access-control/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [ Rekening (Adobe) ](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [ instantie van de Attribution AI ](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen</li><li>Uitschakelen</li></ul> |
| [ Logboeken van de Controle ](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>Exporteren</li></ul> |
| [ Klasse ](../../../xdm/schema/composition.md#class) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| Berekend kenmerk | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [ de instantie van AI van de Klant ](../../../intelligent-services/customer-ai/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen</li><li>Uitschakelen</li></ul> |
| [ Dataset ](../../../catalog/datasets/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Laat voor [ in real time het Profiel van de Klant ](../../../profile/home.md) toe</li><li>Uitschakelen voor profiel</li><li>Gegevens toevoegen</li><li>Batch verwijderen</li></ul> |
| [ DataStream ](../../../datastreams/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen</li><li>Uitschakelen</li><li>[ geef Toewijzing ](../../../datastreams/data-prep.md) uit</li></ul> |
| [Datatypen](../../../xdm/schema/composition.md#data-type) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [ Doel ](../../../destinations/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen</li><li>Uitschakelen</li><li>Gegevensset activeren</li><li>Gegevensset verwijderen</li><li>Profiel activeren</li><li>Profiel verwijderen</li></ul> |
| [ de groep van het Gebied ](../../../xdm/schema/composition.md#field-group) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [ grafiek van de Identiteit ](../../../identity-service/features/identity-graph-viewer.md) | <ul><li>Weergave</li></ul> |
| [ Identiteitsnaamruimte ](../../../identity-service/features/namespaces.md) | <ul><li>Maken</li><li>Bijwerken</li></ul> |
| [ beleid van de Fusie ](../../../profile/merge-policies/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [ Profiel van het Product ](../../../access-control/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Query](../../../query-service/ui/overview.md) | <ul><li>Uitvoeren</li></ul> |
| [ malplaatje van de Vraag ](../../../query-service/ui/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [ Rol (attribuut gebaseerd toegangsbeheer) ](../../../access-control/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Gebruiker toevoegen</li><li>Gebruiker verwijderen</li></ul> |
| [ Sandbox ](../../../sandboxes/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Herstellen</li><li>Verwijderen</li></ul> |
| [ Geplande vraag ](../../../query-service/ui/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [ Schema ](../../../xdm/schema/composition.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen voor profiel</li></ul> |
| [ Segment ](../../../segmentation/home.md) | <ul><li>Maken</li><li>Verwijderen</li><li>Segment activeren</li><li>Segment verwijderen</li></ul> |
| [ de gegevensstroom van Source ](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen</li><li>Uitschakelen</li><li>Dataset activeren</li><li>Gegevensset verwijderen</li><li>Profiel activeren</li><li>Profiel verwijderen</li></ul> |
| [ orde van het Werk ](../../../hygiene/home.md) | <ul><li>Maken</li></ul> |

## Toegang tot auditlogboeken

Wanneer de eigenschap voor uw organisatie wordt toegelaten, worden de controlelogboeken automatisch verzameld aangezien de activiteit voorkomt. U te hoeven niet om logboekinzameling manueel toe te laten.

Als u controlelogboeken wilt weergeven en exporteren, moet u de toegangsbeheermachtiging van **[!UICONTROL View User Activity Log]** hebben (deze kunt u vinden onder de categorie [!UICONTROL Data Governance] ). Leren hoe te om individuele toestemmingen voor de eigenschappen van het Platform te beheren, gelieve te verwijzen naar de [ documentatie van de toegangscontrole ](../../../access-control/home.md).

## Het beheren van controlelogboeken in UI {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="Instructies"
>abstract="<ul><li>Selecteer <b> Controles </b> in de linkernavigatie. De werkruimte Audits toont een lijst van geregistreerde logboeken, door gebrek dat van meest recente aan minst recente wordt gesorteerd.</li>   <li> OPMERKING: auditlogboeken worden 365 dagen bewaard waarna ze uit het systeem worden verwijderd. Daarom kun je slechts 365 dagen teruggaan. Als u terug op gegevens moet kijken ouder dan 365 dagen, zou u logboeken bij een regelmatige kring moeten uitvoeren om aan uw interne beleidsvereisten te voldoen. </li><li>Selecteer een gebeurtenis in de lijst om de details in de rechtertrack weer te geven. </li><li>Selecteer het trechter-pictogram om een lijst met filterbesturingselementen weer te geven om de resultaten te beperken. Alleen de laatste 1000 records worden weergegeven, ongeacht de geselecteerde filters. </li><li>Om de huidige lijst van controlelogboeken uit te voeren, selecteer **logboek van de Download**.</li><li>Voor meer hulp met deze eigenschap, zie het <a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html"> overzicht van controlelogboeken </a> op Experience League.</li></ul>"

U kunt controlelogboeken voor verschillende eigenschappen van het Experience Platform bekijken binnen de **[!UICONTROL Audits]** werkruimte in de UI van het Platform. De werkruimte bevat een lijst met opgenomen logbestanden, die standaard van de meest recente naar de minst recente logbestanden worden gesorteerd.

![ het dashboard van Audits die Audits in het linkermenu benadrukken.](../../images/audit-logs/audits.png)

Auditlogboeken worden 365 dagen bewaard waarna ze uit het systeem worden verwijderd. Daarom kun je slechts 365 dagen teruggaan. Als u gegevens van meer dan 365 dagen vereist, zou u logboeken bij een regelmatige kast moeten uitvoeren om aan uw interne beleidsvereisten te voldoen.

Selecteer een gebeurtenis in de lijst om de details in de rechtertrack weer te geven.

![ het logboeklusje van de Activiteit van het dashboard van Audits met het benadrukte paneel van gebeurtenisdetails.](../../images/audit-logs/select-event.png)

### Controllerlogboeken filteren

>[!NOTE]
>
>Aangezien dit een nieuwe eigenschap is, gaan de getoonde gegevens slechts terug tot maart 2022. Afhankelijk van de geselecteerde bron kunnen eerdere gegevens beschikbaar zijn vanaf januari 2022.


Selecteer het kanaalpictogram (![ pictogram van de Filter ](/help/images/icons/filter.png)) om een lijst van filtercontroles te tonen om smalle resultaten te helpen. Alleen de laatste 1000 records worden weergegeven, ongeacht de verschillende geselecteerde filters.

![ het dashboard van Audits met het gefiltreerde benadrukte activiteitenlogboek.](../../images/audit-logs/filters.png)

De volgende filters zijn beschikbaar voor controlegebeurtenissen in UI:

| Filter | Beschrijving |
| --- | --- |
| [!UICONTROL Category] | Gebruik dropdown menu aan filter getoonde resultaten door [ categorie ](#category). |
| [!UICONTROL Action] | Filteren op handeling. De acties beschikbaar voor elke dienst kunnen in de middellijst hierboven worden gezien. |
| [!UICONTROL User] | Voer de volledige gebruikers-id in (bijvoorbeeld `johndoe@acme.com` ) om te filteren op gebruiker. |
| [!UICONTROL Status] | Filter door of de actie werd toegestaan (voltooid) of wegens gebrek aan [ toegangsbeheer ](../../../access-control/home.md) toestemmingen ontkend. |
| [!UICONTROL Date] | Selecteer een begindatum en/of een einddatum om een datumbereik te definiëren waarop de resultaten moeten worden gefilterd. De gegevens kunnen met een raadplegingsperiode van 90 dagen worden uitgevoerd (bijvoorbeeld, 2021-12-15 aan 2022-03-15). Dit kan per gebeurtenistype verschillen. |

Als u een filter wilt verwijderen, selecteert u de &quot;X&quot; op het vulpictogram voor het desbetreffende filter of selecteert u **[!UICONTROL Clear all]** om alle filters te verwijderen.

![ het dashboard van Audits met duidelijke benadrukte filter.](../../images/audit-logs/clear-filters.png)

De teruggekeerde gegevens van het controlelogboek bevatten de volgende informatie over alle vragen die aan uw gekozen filtercriteria voldoen.

| Kolomnaam | Beschrijving |
|---|---|
| [!UICONTROL Timestamp] | De exacte datum en tijd van de actie die in een `month/day/year hour:minute AM/PM` -indeling wordt uitgevoerd. |
| [!UICONTROL Asset Name] | De waarde voor het veld [!UICONTROL Asset Name] is afhankelijk van de categorie die als filter is gekozen. |
| [!UICONTROL Category] | Dit veld komt overeen met de categorie die is geselecteerd in de vervolgkeuzelijst met filters. |
| [!UICONTROL Action] | Welke acties beschikbaar zijn, is afhankelijk van de categorie die als filter is gekozen. |
| [!UICONTROL User] | Dit veld bevat de gebruikers-id die de query heeft uitgevoerd. |

![ het dashboard van Audits met het gefilterde benadrukte activiteitenlogboek.](../../images/audit-logs/filtered.png)

### Controleverslagen exporteren

Selecteer **[!UICONTROL Download log]** als u de huidige lijst met auditlogs wilt exporteren.

![ het dashboard van Audits met [!UICONTROL Download log] benadrukte.](../../images/audit-logs/download.png)

Selecteer in het dialoogvenster dat wordt weergegeven de gewenste indeling (**[!UICONTROL CSV]** of **[!UICONTROL JSON]** ) en selecteer vervolgens **[!UICONTROL Download]** . De browser downloadt het gegenereerde bestand en slaat het op uw computer op.

![ de dialoog van de dossierformaatselectie met [!UICONTROL Download] benadrukt.](../../images/audit-logs/select-download-format.png)

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

Selecteer in de lijst de gewenste waarschuwing om u te abonneren op de ontvangst van berichten. Voor meer informatie over alarm, zie de gids op [ het intekenen aan alarm gebruikend UI ](../../../observability/alerts/ui.md).

## Controlelogbestanden beheren in de API

Alle acties die u in UI kunt uitvoeren kunnen ook worden gedaan gebruikend API vraag. Zie het [ API verwijzingsdocument ](https://www.adobe.io/experience-platform-apis/references/audit-query/) voor meer informatie.

## Controlelogbestanden voor Adobe Admin Console beheren

Leren hoe te om controlelogboeken voor activiteiten in Adobe Admin Console te beheren, verwijs naar het volgende [ document ](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Volgende stappen en extra bronnen

Deze gids besprak hoe te om controlelogboeken in Experience Platform te beheren. Voor meer informatie over hoe te om de activiteiten van het Platform te controleren, zie de documentatie over [ de Inzichten van de Waarneming ](../../../observability/home.md) en [ controle gegevensopname ](../../../ingestion/quality/monitor-data-ingestion.md).

Bekijk de volgende video om uw inzicht in auditlogs in Experience Platform te versterken:

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
