---
title: Aanbevolen procedures voor Privacy Service
description: Leer hoe u de verwerkingstijd en de kosten voor uw organisatie bij het invullen van privacyverzoeken kunt verminderen door deze richtlijnen voor optimaal gebruik te volgen.
exl-id: 1333d6c6-5ca0-41c1-9f9e-aa2a5a8b8a9c
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Aanbevolen procedures voor Privacy Service

Gebruik de Privacy Service om de naleving van de privacyregels voor gegevens te automatiseren wanneer klanten hun persoonlijke gegevens willen openen of verwijderen uit uw gegevensopslag. Om aan deze evoluerende bedrijfsbehoeften te voldoen, biedt de Privacy Service een RESTful API en UI aan om toegang en schrappingsverzoeken voor klantengegevens over de toepassingen van Adobe Experience Cloud voor te leggen.

In deze handleiding worden de aanbevolen procedures beschreven voor het efficiënt verwerken van privacyverzoeken en het optimaliseren van de responstijden bij het beheren van verzoeken om klantgegevens.

## Aan de slag {#getting-started}

Deze gids vereist een werkend begrip van [&#x200B; Privacy Service &#x200B;](./home.md) en hoe het u toestaat om toegang te beheren en verzoeken van uw gegevensproefpersonen (klanten) over de toepassingen van Adobe Experience Cloud te schrappen. U wordt ook geadviseerd om de gids te hebben gelezen op [&#x200B; creërend een verzoek van de privacybaan in UI &#x200B;](./ui/user-guide.md#create-a-new-privacy-job-request) of [&#x200B; API &#x200B;](./api/overview.md), en te begrijpen hoe te om deze verrichtingen programmatically uit te voeren.

## Vereisten {#prerequisites}

De toegang tot Adobe Experience Platform Privacy Service wordt gecontroleerd door granulaire op rol-gebaseerde toestemmingen in Adobe Admin Console. U hebt de relevante machtigingen in een productprofiel nodig om specifieke functies in de gebruikersinterface en de API van de Privacy Service te kunnen gebruiken. Neem contact op met de systeembeheerder als u aanvullende machtigingen nodig hebt.

De beheerders kunnen naar de gids op [&#x200B; verwijzen die toestemmingen voor Privacy Service &#x200B;](./permissions.md) voor meer informatie beheert.

## Richtlijnen voor het creëren van privacy-banen {#creation-guidelines}

Houd bij het maken van privacytaken rekening met de volgende richtlijnen om de verwerking van uw verzoek te stroomlijnen en de responstijden te verbeteren. Dit geldt voor zowel de API- als de UI-methoden.

1. **maximaliseer gegevensproefpersonen per verzoek:** omvat zo vele gegevensproefpersonen zoals mogelijk, tot 1000, per verzoek.
2. **Identiteitskaart van de Groep voor efficiency:** veelvoudige IDs van de Groep voor één enkel gegevenssubject (tot negen) in elk verzoek. **IDs kan uit de verschillende diensten van Adobe in het zelfde verzoek** komen.
3. **combineer toegang en schrap banen:** omvat zowel &quot;toegang&quot;als &quot;schrapt&quot;baantypes in één enkel verzoek indien vereist door de gegevenssubject.
4. **omvat slechts noodzakelijke producten:** omvat slechts producten die worden vereist of vergunning gegeven. De extra producten kunnen verwerkingstijd verlengen en kosten verhogen.

## Status van privacytaken controleren {#monitor-status}

Privacy Service biedt drie methoden om privacytaken effectief te controleren en de status ervan te controleren. De beschikbare methoden worden hieronder vermeld in volgorde van efficiëntie en productiviteit. Elke methode bevat richtlijnen voor de beste praktijken om uw ervaring te verbeteren, gevolgd door een ideaal scenario-voorbeeld waarin alle benaderingen worden gecombineerd.

### real-time meldingen ontvangen {#real-time-notifications}

**I/O Gebeurtenissen** bieden dichtbij statuscontrole in real time door statusgebeurtenissen aan. Dit is de meest efficiënte methode, omdat hierdoor de noodzaak om opiniepeilingsmechanismen in te voeren en extra API-verkeer te veroorzaken wordt vermeden.

**Recommendations:**

- **de opstelling van Webhaak:** opstelling webhooks om dupberichten te ontvangen wanneer de statusveranderingen voor voorgelegde banen voorkomen. Dit is een hulpmiddel bij realtimemonitoring.
- **Meldingen:** Gebruik berichten op zowel het baan als productniveau helpen de vooruitgang van verzoeken controleren.

Zie de documentatie op [&#x200B; het intekenen aan de gebeurtenissen van de Privacy Service &#x200B;](./privacy-events.md) voor instructies bij vestiging een gebeurtenisregistratie voor de berichten van de Privacy Service en hoe te om berichtlading te interpreteren.

### Alle taken ophalen op basis van filters {#retrieve-filtered-responses-for-all-jobs}

Om al uw gegevens van de privacybaan terug te winnen die op om het even welke gespecificeerde filters worden gebaseerd, **voert een verzoek van de GET aan het `/jobs` eindpunt** uit. Deze API-aanroep is handig om een weergave op hoog niveau te bieden van de huidige taakstatus voor grote sets met taak-id&#39;s met slechts één aanvraag. Het gebrek aan gedetailleerde productreacties, maar zij kunnen worden gevonden gebruikend het [`/jobs/{jobID}` eindpunt &#x200B;](#retrieve-detailed-responses-for-specific-jobs).

Een verzoek van de GET aan het `/jobs` eindpunt wordt best gebruikt om de statusgegevens van een grote reeks baan IDs te verzamelen of te vergelijken maar **&#x200B;**&#x200B;bedoeld niet voor regelmatige het opiniepeilingstype activiteiten.

**Recommendations:**

- **de parameters van de Vraag:** Gebruik specifieke filters om uw resultaten te versmallen, bijvoorbeeld: gegevenswaaiers, regelgevende types, en status (verwerking, volledig, etc.).

U kunt een lijst van alle huidige privacybanen in uw organisatie door de UI van de Privacy Service bekijken. Zie [&#x200B; het leiden privacybanen in de documentatie UI &#x200B;](./ui/user-guide.md#job-requests) voor informatie over hoe te om de lijst van het baanverzoek te filtreren. Alternatief, zie de documentatie over het [&#x200B; gebruik van het /job eindpunt in Privacy Service API &#x200B;](./api/privacy-jobs.md).

De Privacy Service API documentatie bevat details op [&#x200B; de beschikbare filters van de vraagparameter &#x200B;](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#tag/Privacy-jobs/operation/listPrivacyJobs).

### Gedetailleerde antwoorden ophalen voor één taak {#retrieve-detailed-responses-for-specific-jobs}

Om gedetailleerde reacties voor één enkele baan terug te winnen, **voer een verzoek van de GET aan het /jobs/{jobID} eindpunt** uit. Deze methode is bedoeld voor het verdiepen van informatie, zoals productspecifieke reacties en succesberichten. Een vraag aan dit eindpunt is de beste manier om te zien welke producten hebben gereageerd en die nog hangend zijn, hoewel het **&#x200B;**&#x200B;niet &lbrace;voor regelmatige opiniepeilingsactiviteit bedoeld is.

Zie de `/jobs/{JOB_ID}` eindpuntdocumentatie voor details op [&#x200B; hoe te om het statuut van een specifieke baan &#x200B;](./api/privacy-jobs.md#check-status) te controleren.

### Ideal-scenario-voorbeeld {#ideal-scenario}

Gebruik een webhaak zodat het systeem automatisch records kan bijwerken en meldingen of waarschuwingen kan verstrekken wanneer groepen van de id&#39;s van een aanvraag zijn voltooid. Als er nog taken openstaan, haalt het systeem deze taakstatus op met een aanvraag van de GET naar het eindpunt van de Privacy Service-API `/jobs` en wordt een update op hoog niveau van de lijst weergegeven.

Als een bepaalde baan nog hangend is, of een fout heeft teruggekeerd, kunt u de gedetailleerde reactie met een verzoek van de GET aan het `/job/{jobId}` eindpunt terugwinnen.

## Toegang tot aanvraaggegevens {#access-request-data}

Wanneer de gegevens-onderwerp informatie wordt gevraagd, keert elke dienst gegevens in een formaat terug dat met de manier verenigbaar is zij opslaan en die gegevens gebruiken. Nadat alle services de aanvraag hebben voltooid, wordt in de taakdetails een URL voor het ZIP-archiefbestand opgegeven, zodat deze gegevens kunnen worden gedownload. Zie de het oplossen van problemengids voor informatie over [&#x200B; hoe te om de resultaten van de privacybaan &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/privacy/troubleshooting-guide.html?lang=nl-NL#how-do-i-download-the-results-of-my-completed-privacy-jobs%3F) te downloaden.

Hieronder volgt een overzicht van de belangrijkste opmerkingen met betrekking tot het beheer van het gegevensarchief:

- Alle archiefbestanden worden na 30 dagen verwijderd van Experience Platform-servers. U kunt geen vragen stellen naar klantgegevens die ouder zijn dan 30 dagen.
- De structuur van het archiefbestand bevat mappen voor elk product dat in de aanvraag is opgenomen en de gegevensbestanden die daarin zijn opgenomen. Archiefbestanden of -mappen zijn mogelijk leeg als er geen gegevens zijn gevonden voor de opgegeven id.
- De gegevens voor eerder gecreëerde banen zijn slechts 30 dagen na de voltooiingsdatum toegankelijk. Daarna worden de gegevens uit het systeem verwijderd en moet een nieuw verzoek worden ingediend.

**Recommendations:**

- **de Archieven van Gegevens van Protect:** zowel zou het URL als .ZIP dossier moeten worden beschermd, aangezien zij persoonlijk identificeerbare informatie (PII) voor de gegevenssubject kunnen bevatten.

## Technische overwegingen {#technical-considerations}

Bij het invullen van een verzoek om Privacy Service moet u rekening houden met een aantal technische aspecten:

- **Periode van het Behoud van Gegevens:** de maximumterugblik periode is 60 dagen voor om het even welke groep banen, en de maximumtijdspanwijdte voor een vraag is 30 dagen (van/aan data).
- **onderbreking van de Gateway:** ben in gedachten dat uw verzoek van de gateway kan worden gelaten vallen als het 60 seconden overschrijdt.
- **de Behandeling van de Fout:** de foutenmeldingen van het overzicht grondig en leggen verzoeken waar nodig opnieuw voor. Privacy Service verwerkt taken niet automatisch na een fout.
- **Begrijpend HTTP 429 Fouten:** vertrouwt me met HTTP 429 foutenmeldingen en de noodzakelijke stappen om kwesties te verlichten. HTTP 429 fouten zijn het resultaat van &quot;Te veel verzoeken&quot;. Zie de [&#x200B; Gemeenschappelijke foutenmeldingen &#x200B;](./troubleshooting-guide.md#common-error-messages) sectie van de het oplossen van problemengids voor meer informatie over hoe te om de kwestie op te lossen.

## Volgende stappen

Door dit document te lezen beschikt u nu over de benodigde kennis en praktijken voor een efficiënt en doeltreffend gebruik van de Privacy Service. Daarna, zie de [&#x200B; het oplossen van problemengids &#x200B;](./troubleshooting-guide.md) voor antwoorden op vaak gestelde vragen over Privacy Service, en informatie over algemeen ondervonden fouten in API.
