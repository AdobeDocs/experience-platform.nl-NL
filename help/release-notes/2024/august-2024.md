---
title: Aanvullende informatie voor Adobe Experience Platform van augustus 2024
description: Aanvullende informatie van augustus 2024 voor Adobe Experience Platform.
exl-id: 153891e9-fd82-4894-a047-c8d82f214fef
source-git-commit: 4fecb47084a522b4eb9808dc317e0d70e7ef42c6
workflow-type: ht
source-wordcount: '1553'
ht-degree: 100%

---

# Aanvullende informatie voor Adobe Experience Platform.

**Releasedatum: 20 augustus 2024**

>[!TIP]
>
>Bekijk een [overzicht van documentatie met voorbeelden van gebruiksscenario&#39;s](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/use-cases/overview) en ontdek welke verschillende gebruiksscenario&#39;s uw organisatie met real time CDP kan bereiken, zoals prospectie, acquisitie en meer.

Updates van bestaande functies en documentatie in Experience Platform:

- [Kenmerkgebaseerde toegangscontrole](#abac)
- [Gegevensopname](#data-ingestion)
- [Bestemmingen](#destinations)
- [Experience-datamodel (XDM)](#xdm)
- [Identiteitsservice](#identity-service)
- [Segmentatieservice](#segmentation)
- [Bronnen](#sources)

## Kenmerkgebaseerde toegangscontrole {#abac}

Toegangscontrole op basis van kenmerken is een functionaliteit van Adobe Experience Platform waarmee merken die aandacht hebben voor privacy, meer flexibiliteit krijgen bij toegangsbeheer voor gebruikers. Inviduele objecten, zoals schemavelden en segmenten, kunnen aan gebruikersrollen worden toegewezen. Met deze functie kunt u toegang tot individuele objecten verlenen of intrekken voor specifieke platformgebruikers in uw organisatie.

Met op kenmerken gebaseerde toegangscontrole kunnen beheerders van uw organisatie de toegang van gebruikers tot gevoelige persoonlijke gegevens (SPD), persoonlijk identificeerbare informatie (PII) en andere aangepaste typen gegevens in alle platformworkflows en -bronnen beheren. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die bij die velden horen.

**Nieuwe functie**

| Functie-update | Beschrijving |
| --- | --- |
| Nieuwe functie voor Permission Manager | U kunt nu [Permission Manager](../../access-control/abac/permission-manager/overview.md) gebruiken om rapporten te genereren met behulp van eenvoudige query&#39;s. Hiermee krijgt u inzicht in toegangsbeheer en bespaart u tijd bij het verifiëren van toegangsrechten in verschillende workflows en op verschillende granulariteitsniveaus. Raadpleeg het [handboek voor Permission Manager](../../access-control/abac/permission-manager/permissions.md) voor meer informatie over het maken van rapporten voor gebruikers en rollen. ![Afbeelding Experience Platform-gebruikersinterface met Permission Manager in het linkernavigatiedeelvenster gemarkeerd.](assets/august/permission-manager-rn.png "Permission Manager in de gebruikersinterface."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Zie het [overzicht van op kenmerken gebaseerde toegangscontrole](../../access-control/abac/overview.md) voor meer informatie over op kenmerken gebaseerde toegangscontrole. Voor een uitgebreide handleiding over de workflow voor toegangscontrole op basis van kenmerken leest u de [end-to-end handleiding voor toegangscontrole op basis van kenmerken](../../access-control/abac/end-to-end-guide.md).

## Gegevensinname (bijgewerkt op 23 augustus) {#data-ingestion}

Adobe Experience Platform biedt een uitgebreide reeks functies voor het invoeren van elk type en elke latentie van gegevens. U kunt gegevens opnemen via batch- of streaming-API&#39;s, via door Adobe gemaakte bronnen, via gegevensintegratiepartners of via de gebruikersinterface van Adobe Experience Platform.

**Update van datumnotatieverwerking bij batchgegevensopname**

In deze release wordt een probleem opgelost met de *datumnotatieverwerking* bij batchgegevensopname. Vroeger transformeerde het systeem datumvelden die door klanten waren ingevoegd `Date` in `DateTime`-indeling. Dit betekende dat de tijdzone automatisch aan velden werd toegevoegd en dat leverde problemen op voor gebruikers die de `Date`-indeling wensten of nodig hadden. Vanaf nu wordt de tijdzone niet meer automatisch toegevoegd aan velden van het type `Date`. Deze update zorgt ervoor dat de geëxporteerde indeling van gegevens overeenkomt met de indeling die op verzoek van klanten wordt weergegeven in het profiel voor dat veld.

`Date`-velden vóór de release: `"birthDate": "2018-01-12T00:00:00Z"`
`Date`-velden na de release: `"birthDate": "2018-01-12"`

Meer informatie over [batchopname](/help/ingestion/batch-ingestion/overview.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms die zorgen voor de naadloze activering van gegevens van Adobe Experience Platform. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s te activeren.

**Nieuwe of bijgewerkte bestemmingen** {#new-updated-destinations}

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [Braze](/help/destinations/catalog/mobile-engagement/braze.md) | [!UICONTROL Braze] beheert een aantal verschillende instanties voor hun dashboard en REST-eindpunten. [!UICONTROL Braze]-klanten moeten het juiste REST-eindpunt gebruiken op basis van de instantie waarvoor ze zijn ingericht. Deze versie voegt een nieuw US-07-eindpunt toe dat u kunt selecteren wanneer u verbinding maakt met [!UICONTROL Braze]. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functie | Beschrijving |
| ----------- | ----------- |
| Het exporteren van bestanden op aanvraag naar batchbestemmingen is nu algemeen beschikbaar. | De optie om bestanden op aanvraag te exporteren naar batchbestemmingen is nu beschikbaar voor alle klanten. Raadpleeg de [specifieke documentatie](../../destinations/ui/export-file-now.md) voor meer informatie. |
| Bewerk exportschema&#39;s voor meerdere geëxporteerde doelgroepen in de [planningsstap](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | De optie om de exportschema&#39;s voor meerdere geëxporteerde doelgroepen rechtstreeks vanuit de planningsstap van de workflow voor doelgroepactivering te bewerken, is nu beschikbaar voor alle klanten. ![Afbeelding van de gebruikersinterface van Experience Platform met de optie Planning bewerken in de planningsstap gemarkeerd.](assets/august/edit-schedule.png "De optie Planning bewerken in de planningsstap."){width="250" align="center" zoomable="yes"} |
| Bestandsnamen bewerken voor meerdere geëxporteerde doelgroepen in de [planningsstap](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | De optie om de namen van meerdere geëxporteerde bestanden rechtstreeks te bewerken vanuit de planningsstap van de workflow voor doelgroepactivering is nu voor alle klanten beschikbaar. ![Afbeelding van de gebruikersinterface van Experience Platform met de optie Bestandsnaam bewerken gemarkeerd in de planningsstap.](assets/august/edit-file-name.png "De optie Bestandsnaam bewerken in de planningsstap."){width="250" align="center" zoomable="yes"} |
| Meerdere doelgroepen uit een gegevensstroom verwijderen via de pagina [Bestemmingsgegevens](../../destinations/ui/destination-details-page.md#bulk-remove). | De optie om meerdere doelgroepen uit bestaande gegevensstromen te verwijderen vanaf de pagina **[!UICONTROL Destination Details]** is nu beschikbaar voor alle klanten. ![Afbeelding van de gebruikersinterface van Experience Platform met de optie Doelgroepen verwijderen op de pagina Bestemmingsgegevens.](assets/august/bulk-remove-audiences.png "De optie Doelgroepen verwijderen op de pagina Bestemmingsgegevens."){width="250" align="center" zoomable="yes"} |
| Meerdere bestanden op aanvraag exporteren naar batchbestemmingen vanaf de pagina [Bestemmingsgegevens](../../destinations/ui/destination-details-page.md#bulk-export). | De optie om meerdere bestanden op aanvraag naar batchbestemmingen te exporteren vanaf de pagina **[!UICONTROL Destination Details]** is nu beschikbaar voor alle klanten. ![Afbeelding van de gebruikersinterface van Experience Platform met de optie Bestand nu exporteren gemarkeerd op de pagina Bestemmingsgegevens.](assets/august/bulk-export-file-now.png "De optie Bestand nu exporteren op de pagina Bestemmingsgegevens."){width="250" align="center" zoomable="yes"} |
| Bestandsnamen bewerken voor meerdere geëxporteerde doelgroepen vanaf de pagina [Bestemmingsgegevens](../../destinations/ui/destination-details-page.md#bulk-edit-file-names). | U kunt de namen van meerdere geëxporteerde bestanden nu rechtstreeks vanaf de pagina **[!UICONTROL Destination Details]** bewerken. ![Afbeelding van de gebruikersinterface van Experience Platform met de optie Bestandsnaam bewerken gemarkeerd op de pagina Bestemmingsgegevens.](assets/august/edit-file-name-destination-details.png "De optie Bestandsnaam bewerken op de pagina Bestemmingsgegevens."){width="250" align="center" zoomable="yes"} |
| Meerdere datasets uit een gegevensstroom verwijderen vanaf de pagina [Bestemmingsgegevens](../../destinations/ui/export-datasets.md#remove-dataset). | De optie om meerdere datasets uit een gegevensstroom te verwijderen is nu beschikbaar voor alle klanten. ![Afbeelding van de gebruikersinterface van Experience Platform met de optie Datasets verwijderen gemarkeerd op de pagina Bestemmingsgegevens.](assets/august/bulk-remove-datasets.png "De optie Datasets verwijderen op de pagina Bestemmingsgegevens."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Voor meer informatie leest u het [overzicht van bestemmingen](../../destinations/home.md).

## Experience-datamodel (XDM) {#xdm}

XDM is een open-sourcespecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Adobe Experience Platform worden geïmporteerd. Door de normen van XDM te volgen kunnen alle gegevens van de klantervaring in een algemene weergave worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Workflow voor het maken van een ML-ondersteund schema | Gebruik geavanceerde computerleeralgoritmen om uw bestanden met voorbeeldgegevens te analyseren en automatisch geoptimaliseerde schema&#39;s te maken met standaard- en aangepaste velden.<br>Belangrijkste functies:<br><ul><li>Sneller schema&#39;s maken: genereer schema&#39;s rechtstreeks vanuit voorbeeldgegevensbestanden met behulp van door ML aanbevolen en gegenereerde XDM-velden.</li><li>Flexibele evolutie van schema&#39;s: voeg eenvoudig velden toe of werk ze bij in het gegenereerde schema.</li><li>Naadloze integratie: volledig geïntegreerd met de workflow voor het maken van schema&#39;s in de Schema-gebruikersinterface, wat leidt tot een vlotte en samenhangende gebruikerservaring.</li><li>Efficiënt beoordelen en bewerken: bekijk en update uw schema snel met de Flat View-editor, waardoor het ontwerpproces efficiënter en gebruiksvriendelijker wordt.</li></ul><br>Lees de [handleiding voor de workflow voor het maken van schema&#39;s met behulp van ML](../../xdm/ui/ml-assisted-schema-creation.md) voor meer informatie. |

{style="table-layout:auto"}

Raadpleeg het [XDM-systeemoverzicht](../../xdm/home.md) voor meer informatie over XDM in Platform.

## Identiteitsservice {#identity-service}

Met Adobe Experience Platform Identity Service krijgt u een uitgebreid beeld van uw klanten en hun gedrag door identiteiten op verschillende apparaten en systemen te koppelen, zodat u in real time een impactvolle, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte documentatie**

| Functie | Beschrijving |
| --- | --- |
| Handleiding voor grafiekconfiguraties | Lees de [handleiding voor grafiekconfiguraties](../../identity-service/identity-graph-linking-rules/example-configurations.md) voor informatie over veelvoorkomende grafiekscenario&#39;s die u kunt tegenkomen bij het werken met identiteitsgrafiekkoppelingsregels en identiteitsgegevens. De handleiding voor grafiekconfiguraties bevat voorbeelden die variëren van eenvoudige grafiekscenario&#39;s voor één persoon tot complexe en hiërarchische grafiekscenario&#39;s voor meerdere personen. U kunt de handleiding ook gebruiken om voorbeelden van gebeurtenissen en algoritmeconfiguraties te verkrijgen die u kunt invoeren in de [gebruikersinterface van de grafieksimulatie](../../identity-service/identity-graph-linking-rules/graph-simulation.md), evenals een overzicht van hoe primaire identiteiten in bepaalde grafiekscenario&#39;s worden geselecteerd. |

{style="table-layout:auto"}

Voor meer informatie over Identity Service leest u het [Identity Service-overzicht](../../identity-service/home.md).

## Segmentatieservice {#segmentation}

Met [!DNL Segmentation Service] kunt u gegevens die zijn opgeslagen in [!DNL Experience Platform] en die betrekking hebben op personen (zoals klanten, prospects, gebruikers of organisaties), segmenteren in doelgroepen. U kunt een doelgroep maken via segmentdefinities of andere bronnen op basis van uw [!DNL Real-Time Customer Profile]-gegevens. Deze soorten doelgroepen worden centraal geconfigureerd en bijgehouden in [!DNL Platform], en zijn gemakkelijk toegankelijk via elke Adobe-toepassing.

**Bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Opnamegegevens | Voor doelgroepen met de oorsprong Aangepaste upload kunt u uitgebreidere details over de doelgroepopname bekijken op de pagina Doelgroepgegevens. Bovendien kunt u labels toepassen op de payload-kenmerken door het schema te selecteren en de gewenste kenmerken voor de labels te selecteren. Voor meer informatie over de sectie Opnamegegevens raadpleegt u de [Handleiding voor Audience Portal](../../segmentation/ui/audience-portal.md#ingestion-details). |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service] raadpleegt u het [Segmentatieoverzicht](../../segmentation/home.md).

## Bronnen

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

Gebruik bronnen in Experience Platform om gegevens uit een Adobe-toepassing of een gegevensbron van derden op te nemen.

**Bijgewerkte functie**

| Functie | Beschrijving |
| --- | --- |
| Updates voor de Adobe Analytics-bronaansluiting | Op de pagina met datasetactiviteiten wordt geen informatie over batches weergegeven, omdat de Analytics Source-bronaansluiting volledig door Adobe wordt beheerd. U kunt de gegevensstroom controleren door de statistieken van de opgenomen records te bekijken. Lees de handleiding over het maken van een [bronverbinding voor Analytics-gegevens](../../sources/tutorials/ui/create/adobe-applications/analytics.md) voor meer informatie. |

**Bijgewerkte documentatie**

| Bijgewerkte documentatie | Beschrijving |
| --- | --- |
| Uitgebreide documentatie over het bijwerken van gegevensstromen | De handleiding over het [bijwerken van bestaande brongegevensstromen in de gebruikersinterface](../../sources/tutorials/ui/update-dataflows.md) is bijgewerkt om meer informatie te geven over de verschillende configuraties die u kunt maken voor een bestaande gegevensstroom. De handleiding is ook bijgewerkt om het verwachte gedrag te verduidelijken wanneer een uitgeschakelde gegevensstroom opnieuw wordt ingeschakeld. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [ overzicht van bronnen ](../../sources/home.md).
