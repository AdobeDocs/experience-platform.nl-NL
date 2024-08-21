---
title: Opmerkingen bij de release van Adobe Experience Platform, augustus 2024
description: De release van augustus 2024 bevat opmerkingen over Adobe Experience Platform.
source-git-commit: 67152524c9448ad1c6cd1f25437e5ed69900ef84
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: woensdag 20 augustus 2024**

>[!TIP]
>
>Bekijk een [ overzicht van de gevallendocumentatie van het steekproefgebruik ](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/use-cases/overview) om over diverse gebruiksgevallen zoals het prospecteren, de verwerving, en meer te leren die uw organisatie met Real-Time CDP kan bereiken.

Updates van bestaande functies en documentatie in Experience Platform:

- [Toegangsbeheer op basis van kenmerken](#abac)
- [Doelen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identiteitsservice](#identity-service)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Toegangsbeheer op basis van kenmerken {#abac}

Toegangsbeheer op basis van kenmerken is een mogelijkheid van Adobe Experience Platform die privacybewuste merken meer flexibiliteit biedt om gebruikerstoegang te beheren. Afzonderlijke objecten zoals schemavelden en segmenten kunnen worden toegewezen aan gebruikersrollen. Met deze functie kunt u toegang tot afzonderlijke objecten verlenen of intrekken voor specifieke platformgebruikers in uw organisatie.

Via attribuut-gebaseerde toegangscontrole, kunnen de beheerders van uw organisatie gebruikers&#39; toegang tot gevoelige persoonlijke gegevens (SPD) controleren, persoonlijk identificeerbare informatie (PII), en ander aangepast type van gegevens over alle werkschema&#39;s en middelen van het Platform. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die overeenkomen met die velden.

**Nieuwe eigenschap**

| Functie-update | Beschrijving |
| --- | --- |
| Nieuwe functie voor machtigingenbeheer | U kunt [ Manager van de Toestemming ](../../access-control/abac/permission-manager/overview.md) nu gebruiken om rapporten te produceren gebruikend eenvoudige vragen, die u toegangsbeheer zullen begrijpen en tijd zullen bewaren controlerend toegangstoestemmingen over verscheidene werkschema&#39;s en granulariteitsniveaus. Voor meer informatie bij het creëren van rapporten voor gebruikers en rollen, zie de [ gebruikersgids van de Manager van de Toestemming ](../../access-control/abac/permission-manager/permissions.md). ![ gebruikersinterface die van het Experience Platform van het Beeld de Manager van de Toestemming in linkernav benadrukt.](../2024/assets/august/permission-manager-rn.png " Manager van de Toestemming in het gebruikersinterface."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Voor meer informatie over op attribuut-gebaseerde toegangsbeheer, zie het [ op attributen-gebaseerde toegangsbeheeroverzicht ](../../access-control/abac/overview.md). Voor een uitvoerige gids over het op attribuut-gebaseerde toegangsbeheerwerkschema, lees de [ op attribuut-gebaseerde gids van begin tot eind van de toegangscontrole ](../../access-control/abac/end-to-end-guide.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| ----------- | ----------- |
| Het exporteren van bestanden op aanvraag naar batchbestemmingen is nu over het algemeen beschikbaar. | De optie om dossiers op bestelling naar partijbestemmingen uit te voeren is nu beschikbaar aan alle klanten. Zie de [ specifieke documentatie ](../../destinations/ui/export-file-now.md) voor meer details. |
| Bewerk de uitvoerprogramma&#39;s voor veelvoudige uitgevoerde publiek in [ het plannen stap ](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | De optie om de exportschema&#39;s voor meerdere geëxporteerde doelgroepen rechtstreeks vanuit de planningsstap van de workflow voor publieksactivering te bewerken, is nu beschikbaar voor alle klanten. ![ Beeld van het gebruikersinterface van het Experience Platform die de Edit planningsoptie in de het plannen stap benadrukt.](../2024/assets/august/edit-schedule.png " geef programmaoptie in de het plannen stap uit."){width="250" align="center" zoomable="yes"} |
| Bewerk dossiernamen voor veelvoudige uitgevoerde publiek in [ plannend stap ](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | De optie om de namen van meerdere geëxporteerde bestanden rechtstreeks te bewerken vanuit de planningsstap van de workflow voor publieksactivering is nu beschikbaar voor alle klanten. ![ Beeld van het gebruikersinterface van het Experience Platform die de Edit dossiernaamoptie in de het plannen stap benadrukt.](../2024/assets/august/edit-file-name.png " geef dossier - noem optie in het plannen stap uit."){width="250" align="center" zoomable="yes"} |
| Verwijder veelvoudige publiek uit een dataflow van de [ pagina van de Details van de Bestemming ](../../destinations/ui/destination-details-page.md#bulk-remove). | De optie om meerdere soorten publiek te verwijderen uit bestaande gegevensstromen van de pagina **[!UICONTROL Destination Details]** is nu beschikbaar voor alle klanten. ![ Beeld van het gebruikersinterface van het Experience Platform die de Remove publieksoptie in de pagina van de Details van de Bestemming benadrukt.](../2024/assets/august/bulk-remove-audiences.png " verwijder publieksoptie in de pagina van de Details van de Bestemming."){width="250" align="center" zoomable="yes"} |
| De uitvoer veelvoudige dossiers op bestelling aan partijbestemmingen van de [ pagina van de Details van de Bestemming ](../../destinations/ui/destination-details-page.md#bulk-export). | De optie om meerdere bestanden op aanvraag naar batchbestemmingen te exporteren vanaf de pagina **[!UICONTROL Destination Details]** is nu beschikbaar voor alle klanten. ![ Beeld van het gebruikersinterface van het Experience Platform die het dossier van de Uitvoer nu optie in de pagina van de Details van de Bestemming benadrukt.](../2024/assets/august/bulk-export-file-now.png " het dossier van de Uitvoer nu optie in de pagina van de Details van de Bestemming."){width="250" align="center" zoomable="yes"} |
| Bewerk dossiernamen voor veelvoudige uitgevoerde publiek van de [ pagina van de Details van de Bestemming ](../../destinations/ui/destination-details-page.md#bulk-edit-file-names). | U kunt de namen van meerdere geëxporteerde bestanden nu rechtstreeks vanaf de pagina **[!UICONTROL Destination Details]** bewerken. ![ Beeld van het gebruikersinterface van het Experience Platform die de Edit optie van de dossiernaam in de pagina van bestemmingsdetails benadrukt.](../2024/assets/august/edit-file-name-destination-details.png " geef dossier - noem optie in de pagina van bestemmingsdetails uit."){width="250" align="center" zoomable="yes"} |
| Verwijder veelvoudige datasets uit een dataflow van de [ pagina van de Details van de Bestemming ](../../destinations/ui/export-datasets.md#remove-dataset). | De optie om veelvoudige datasets uit een dataflow te verwijderen is nu beschikbaar aan alle klanten. ![ Beeld van het gebruikersinterface van het Experience Platform die de Remove datasetoptie in de pagina van bestemmingsdetails benadrukt.](../2024/assets/august/bulk-remove-datasets.png " verwijder datasetoptie in de pagina van bestemmingsdetails."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Voor meer informatie, lees het [ overzicht van bestemmingen ](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Maken van een ML-ondersteund schema | Gebruik geavanceerde computerleeralgoritmen om uw voorbeeld-CSV-gegevensbestanden te analyseren en automatisch geoptimaliseerde schema&#39;s te maken met standaard- en aangepaste velden.<br> Zeer belangrijke Eigenschappen:<br><ul><li>Sneller schema maken: Genereer schema&#39;s rechtstreeks vanuit voorbeeldgegevensbestanden met behulp van door ML aanbevolen en gegenereerde XDM-velden.</li><li>Flexibele evolutie van schema: voeg gemakkelijk gebieden in het geproduceerde schema toe of werk gebieden bij.</li><li>Naadloze integratie: volledig geïntegreerd met de stroom van het kernschema creëren in het Schema Ul, die een vlotte en samenhangende gebruikerservaring verzekert.</li><li>Efficiënte revisie en bewerking: bekijk en werk uw schema snel bij met de Platte weergave-editor, zodat het ontwerpproces efficiënter en gebruiksvriendelijker wordt.</li></ul> |

{style="table-layout:auto"}

Om meer te leren, lees het [ ML-Bijgewerkte overzicht van de schemaverwezenlijking ](../../xdm/ui/ml-assisted-schema-creation.md)

Voor meer informatie over XDM in Platform, zie het [ XDM overzicht van het Systeem ](../../xdm/home.md).

## Identiteitsservice {#identity-service}

Gebruik Adobe Experience Platform Identity Service om een uitgebreide weergave van uw klanten en hun gedrag te maken door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte documentatie**

| Functie | Beschrijving |
| --- | --- |
| Hulplijn voor grafiekconfiguraties | Lees de [ gids van de grafiekconfiguraties ](../../identity-service/identity-graph-linking-rules/example-configurations.md) voor informatie over gemeenschappelijke grafiekscenario&#39;s die u terwijl het werken met identiteitsgrafiek zou kunnen ontmoeten die regels en identiteitsgegevens verbindt. De handleiding voor grafiekconfiguraties biedt voorbeelden, variërend van eenvoudige grafiekscenario&#39;s voor één persoon tot complexe en hiërarchische grafiekscenario&#39;s voor meerdere personen. U kunt de gids voor voorbeelden van gebeurtenissen en algoritmeconfiguraties ook gebruiken die u in de [ grafieksimulatie UI ](../../identity-service/identity-graph-linking-rules/graph-simulation.md) kunt invoeren, evenals onderverdelingen van hoe de primaire identiteiten op bepaalde grafiekscenario&#39;s worden geselecteerd. |

{style="table-layout:auto"}

Voor meer informatie over de Dienst van de Identiteit, lees het [ overzicht van de Dienst van de Identiteit ](../../identity-service/home.md).

## Segmenteringsservice {#segmentation}

Met [!DNL Segmentation Service] kunt u gegevens die zijn opgeslagen in [!DNL Experience Platform] en die betrekking hebben op personen (zoals klanten, vooruitzichten, gebruikers of organisaties) segmenteren naar het publiek. U kunt een publiek maken via segmentdefinities of andere bronnen op basis van uw [!DNL Real-Time Customer Profile] -gegevens. Deze soorten publiek worden centraal geconfigureerd en onderhouden op [!DNL Platform] en zijn gemakkelijk toegankelijk voor elke Adobe.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Inktdetails | Voor publiek met de Aangepaste upload oorsprong, kunt u vollediger details van de opname van het publiek binnen de pagina van publieksdetails bekijken. Bovendien kunt u labels toepassen op de payload-kenmerken door het schema te selecteren en de gewenste kenmerken voor de labels te selecteren. Meer informatie over de sectie van de ingangsdetails kan in de [ Poortgids van het Poortaal van het Publiek ](../../segmentation/ui/audience-portal.md#ingestion-details) worden gevonden. |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service], gelieve te zien het [ overzicht van de Segmentatie ](../../segmentation/home.md).

## Bronnen

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

Gebruik bronnen in Experience Platform om gegevens van een Adobe of een gegevensbron van derden in te voeren.

**Bijgewerkte documentatie**

| Bijgewerkte documentatie | Beschrijving |
| --- | --- |
| Uitgebreide documentatie over het bijwerken van gegevensstromen | De gids bij [ het bijwerken van bestaande brondataflows in UI ](../../sources/tutorials/ui/update-dataflows.md) is bijgewerkt om meer informatie over de verscheidenheid van configuraties te verstrekken u aan een bestaande dataflow kunt maken. De handleiding is ook bijgewerkt om het verwachte gedrag te verduidelijken wanneer een uitgeschakelde gegevensstroom opnieuw wordt ingeschakeld. |

{style="table-layout:auto"}

Voor meer informatie, lees het [ overzicht van bronnen ](../../sources/home.md).
