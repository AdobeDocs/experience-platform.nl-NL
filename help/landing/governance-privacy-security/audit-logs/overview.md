---
title: Overzicht controlelogboeken
description: Leer hoe u met auditlogboeken kunt zien wie welke acties in Adobe Experience Platform heeft uitgevoerd.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: f9917d6a6de81f98b472cff9b41f1526ea51cdae
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 3%

---

# Controlelogboeken {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="Bovenste handelingen"
>abstract="Deze widget geeft de belangrijkste soorten acties weer die binnen de geselecteerde tijdlijn in het Experience Platform zijn uitgevoerd. Als u de volledige lijst met opgenomen acties wilt weergeven in Platform, selecteert u **Audits** in de linkernavigatie."

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="Belangrijkste gebruikers"
>abstract="Deze widget geeft de gebruikers weer die de meeste handelingen in het Experience Platform binnen de geselecteerde tijdlijn hebben uitgevoerd. Als u de volledige lijst met opgenomen acties wilt weergeven in Platform, selecteert u **Audits** in de linkernavigatie."

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="Gebruikersactiviteiten in het platform bewaken"
>abstract="<h2>Beschrijving</h2><p>U kunt gebruikersactiviteit voor diverse diensten en mogelijkheden van het Platform in de vorm van controlelogboeken controleren. Deze logboeken vormen een auditspoor dat registreert <b>wie</b> uitgevoerd <b>wat</b> actie en <b>wanneer</b>. De logboeken van de controle kunnen helpen bij het oplossen van problemenkwesties op Platform en helpen uw zaken effectief voldoen aan het beleid van het collectieve gegevensbeheer en regelgevende vereisten.</p>"

Om de transparantie en zichtbaarheid van de in het systeem uitgevoerde activiteiten te vergroten, kunt u in Adobe Experience Platform gebruikersactiviteiten voor verschillende services en mogelijkheden controleren in de vorm van &quot;auditlogs&quot;. Deze logboeken vormen een auditspoor dat met het oplossen van problemenkwesties op Platform kan helpen, en uw zaken helpen effectief aan het beleid van het collectieve gegevensbeheer en regelgevende vereisten voldoen.

In wezen vertelt een controlelogboek **wie** uitgevoerd **wat** actie, en **wanneer**. Elke actie die in een logboek wordt geregistreerd bevat meta-gegevens die op het actietype, datum en tijd, e-mailidentiteitskaart van de gebruiker die de actie, en extra attributen relevant voor het actietype uitvoerde.

Dit document behandelt controlelogboeken in Platform, met inbegrip van hoe te om hen in UI of API te bekijken en te beheren.

## Gebeurtenistypen die zijn vastgelegd in auditlogboeken {#category}

In de volgende tabel wordt aangegeven op welke acties de middelen in de auditlogboeken worden vastgelegd:

| Bron | Acties |
| --- | --- |
| [Toegangsbeheerbeleid (op kenmerken gebaseerd toegangsbeheer)](../../../access-control/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Account (Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Attribution AI-instantie](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen</li><li>Uitschakelen</li></ul> |
| [Controlelogboeken](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>Exporteren</li></ul> |
| [Klasse](../../../xdm/schema/composition.md#class) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| Berekend kenmerk | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [AI-exemplaar van klant](../../../intelligent-services/customer-ai/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen</li><li>Uitschakelen</li></ul> |
| [Gegevensset](../../../catalog/datasets/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen voor [Klantprofiel in realtime](../../../profile/home.md)</li><li>Uitschakelen voor profiel</li><li>Gegevens toevoegen</li><li>Batch verwijderen</li></ul> |
| [DataStream](../../../datastreams/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen</li><li>Uitschakelen</li><li>[Toewijzing bewerken](../../../datastreams/data-prep.md)</li></ul> |
| [Datatypen](../../../xdm/schema/composition.md#data-type) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Bestemming](../../../destinations/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen</li><li>Uitschakelen</li><li>Gegevensset activeren</li><li>Gegevensset verwijderen</li><li>Profiel activeren</li><li>Profiel verwijderen</li></ul> |
| [Veldgroep](../../../xdm/schema/composition.md#field-group) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Identiteitsgrafiek](../../../identity-service/features/identity-graph-viewer.md) | <ul><li>Weergave</li></ul> |
| [Naamruimte identiteit](../../../identity-service/features/namespaces.md) | <ul><li>Maken</li><li>Bijwerken</li></ul> |
| [Samenvoegbeleid](../../../profile/merge-policies/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Productprofiel](../../../access-control/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Query](../../../query-service/ui/overview.md) | <ul><li>Uitvoeren</li></ul> |
| [Zoekopdrachtsjabloon](../../../query-service/ui/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Rol (op attributen gebaseerd toegangsbeheer)](../../../access-control/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Gebruiker toevoegen</li><li>Gebruiker verwijderen</li></ul> |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Herstellen</li><li>Verwijderen</li></ul> |
| [Geplande query](../../../query-service/ui/overview.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li></ul> |
| [Schema](../../../xdm/schema/composition.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen voor profiel</li></ul> |
| [Segment](../../../segmentation/home.md) | <ul><li>Maken</li><li>Verwijderen</li><li>Segment activeren</li><li>Segment verwijderen</li></ul> |
| [Gegevensstroom bron](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Maken</li><li>Bijwerken</li><li>Verwijderen</li><li>Inschakelen</li><li>Uitschakelen</li><li>Dataset activeren</li><li>Gegevensset verwijderen</li><li>Profiel activeren</li><li>Profiel verwijderen</li></ul> |
| [Werkorder](../../../hygiene/home.md) | <ul><li>Maken</li></ul> |

## Toegang tot auditlogboeken

Wanneer de eigenschap voor uw organisatie wordt toegelaten, worden de controlelogboeken automatisch verzameld aangezien de activiteit voorkomt. U te hoeven niet om logboekinzameling manueel toe te laten.

Als u controlelogboeken wilt weergeven en exporteren, moet u beschikken over **[!UICONTROL View User Activity Log]** toegangsbeheermachtiging verleend (gevonden onder [!UICONTROL Data Governance] categorie). Raadpleeg voor meer informatie over het beheren van individuele machtigingen voor platformfuncties de [toegangsbeheerdocumentatie](../../../access-control/home.md).

## Het beheren van controlelogboeken in UI {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="Instructies"
>abstract="<ul><li>Selecteren <b>Audits</b> in de linkernavigatie. De werkruimte Audits toont een lijst van geregistreerde logboeken, door gebrek dat van meest recente aan minst recente wordt gesorteerd.</li>   <li> OPMERKING: auditlogboeken worden 365 dagen bewaard waarna ze uit het systeem worden verwijderd. Daarom kun je slechts 365 dagen teruggaan. Als u terug op gegevens moet kijken ouder dan 365 dagen, zou u logboeken bij een regelmatige kring moeten uitvoeren om aan uw interne beleidsvereisten te voldoen. </li><li>Selecteer een gebeurtenis in de lijst om de details in de rechtertrack weer te geven. </li><li>Selecteer het trechter-pictogram om een lijst met filterbesturingselementen weer te geven om de resultaten te beperken. Alleen de laatste 1000 records worden weergegeven, ongeacht de geselecteerde filters. </li><li>Selecteer **Logbestand downloaden**.</li><li>Voor meer hulp bij deze functie raadpleegt u de <a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html">overzicht van auditlogboeken</a> op Experience League.</li></ul>"

U kunt controlelogboeken voor verschillende eigenschappen van het Experience Platform binnen bekijken **[!UICONTROL Audits]** in de gebruikersinterface van het platform. De werkruimte bevat een lijst met opgenomen logbestanden, die standaard van de meest recente naar de minst recente logbestanden worden gesorteerd.

![Het dashboard Audits markeert Audits in het linkermenu.](../../images/audit-logs/audits.png)

Auditlogboeken worden 365 dagen bewaard waarna ze uit het systeem worden verwijderd. Daarom kun je slechts 365 dagen teruggaan. Als u gegevens van meer dan 365 dagen vereist, zou u logboeken bij een regelmatige kast moeten uitvoeren om aan uw interne beleidsvereisten te voldoen.

Selecteer een gebeurtenis in de lijst om de details in de rechtertrack weer te geven.

![Hiermee wordt het tabblad Activiteit van het dashboard gecontroleerd, waarbij het deelvenster met gebeurtenisdetails is gemarkeerd.](../../images/audit-logs/select-event.png)

### Controllerlogboeken filteren

>[!NOTE]
>
>Aangezien dit een nieuwe eigenschap is, gaan de getoonde gegevens slechts terug tot maart 2022. Afhankelijk van de geselecteerde bron kunnen eerdere gegevens beschikbaar zijn vanaf januari 2022.


Selecteer het trechter-pictogram (![Filterpictogram](../../images/audit-logs/icon.png)) om een lijst met filterbesturingselementen weer te geven om de resultaten te beperken. Alleen de laatste 1000 records worden weergegeven, ongeacht de verschillende geselecteerde filters.

![Het dashboard van Audits met het gefiltreerde activiteitenlogboek benadrukte.](../../images/audit-logs/filters.png)

De volgende filters zijn beschikbaar voor controlegebeurtenissen in UI:

| Filter | Beschrijving |
| --- | --- |
| [!UICONTROL Category] | Gebruik het vervolgkeuzemenu om de weergegeven resultaten te filteren op [categorie](#category). |
| [!UICONTROL Action] | Filteren op handeling. De acties beschikbaar voor elke dienst kunnen in de middellijst hierboven worden gezien. |
| [!UICONTROL User] | Voer de volledige gebruikersnaam in (bijvoorbeeld `johndoe@acme.com`) om te filteren op gebruiker. |
| [!UICONTROL Status] | Filteren op de vraag of de handeling is toegestaan (voltooid) of geweigerd vanwege een gebrek aan [toegangsbeheer](../../../access-control/home.md) machtigingen. |
| [!UICONTROL Date] | Selecteer een begindatum en/of een einddatum om een datumbereik te definiëren waarop de resultaten moeten worden gefilterd. De gegevens kunnen met een raadplegingsperiode van 90 dagen worden uitgevoerd (bijvoorbeeld, 2021-12-15 aan 2022-03-15). Dit kan per gebeurtenistype verschillen. |

Als u een filter wilt verwijderen, selecteert u de X op het vulpictogram voor het desbetreffende filter of selecteert u **[!UICONTROL Clear all]** alle filters verwijderen.

![Het dashboard Audits met duidelijk benadrukt filter.](../../images/audit-logs/clear-filters.png)

De teruggekeerde gegevens van het controlelogboek bevatten de volgende informatie over alle vragen die aan uw gekozen filtercriteria voldoen.

| Kolomnaam | Beschrijving |
|---|---|
| [!UICONTROL Timestamp] | De exacte datum en tijd van de actie die in een `month/day/year hour:minute AM/PM` gebruiken. |
| [!UICONTROL Asset Name] | De waarde voor de [!UICONTROL Asset Name] wordt bepaald door de categorie die als filter wordt gekozen. |
| [!UICONTROL Category] | Dit veld komt overeen met de categorie die is geselecteerd in de vervolgkeuzelijst met filters. |
| [!UICONTROL Action] | Welke acties beschikbaar zijn, is afhankelijk van de categorie die u als filter hebt gekozen. |
| [!UICONTROL User] | Dit veld bevat de gebruikersnaam die de query heeft uitgevoerd. |

![Het dashboard van Audits met het gefiltreerde activiteitenlogboek benadrukte.](../../images/audit-logs/filtered.png)

### Controleverslagen exporteren

Selecteer **[!UICONTROL Download log]**.

![Het dashboard Audits met het [!UICONTROL Download log] gemarkeerd.](../../images/audit-logs/download.png)

Selecteer in het dialoogvenster dat wordt weergegeven de gewenste indeling (een van de **[!UICONTROL CSV]** of **[!UICONTROL JSON]**), selecteert u vervolgens **[!UICONTROL Download]**. De browser downloadt het gegenereerde bestand en slaat het op uw computer op.

![Het dialoogvenster Bestandsindeling selecteren met [!UICONTROL Download] gemarkeerd.](../../images/audit-logs/select-download-format.png)

## Controlelogbestanden beheren in de API

Alle acties die u in UI kunt uitvoeren kunnen ook worden gedaan gebruikend API vraag. Zie de [API-naslagdocument](https://www.adobe.io/experience-platform-apis/references/audit-query/) voor meer informatie .

## Controlelogbestanden voor Adobe Admin Console beheren

Raadpleeg het volgende voor meer informatie over het beheren van auditlogs voor activiteiten in Adobe Admin Console [document](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Volgende stappen en extra bronnen

Deze gids besprak hoe te om controlelogboeken in Experience Platform te beheren. Raadpleeg de documentatie over voor meer informatie over het bewaken van platformactiviteiten [Waarnembaarheidsinzichten](../../../observability/home.md) en [controle van gegevensinvoer](../../../ingestion/quality/monitor-data-ingestion.md).

Bekijk de volgende video om uw inzicht in auditlogs in Experience Platform te versterken:

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
