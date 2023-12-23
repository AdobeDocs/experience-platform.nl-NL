---
title: Aanbevolen procedures voor Privacy Service
description: Leer hoe u de verwerkingstijd en de kosten voor uw organisatie bij het invullen van privacyverzoeken kunt verminderen door deze richtlijnen voor optimaal gebruik te volgen.
source-git-commit: c6507a39ba5ae5ca6aa2bf02cf8844a4592152ac
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Aanbevolen procedures voor Privacy Service

Gebruik de Privacy Service om de naleving van de privacyregels voor gegevens te automatiseren wanneer klanten hun persoonlijke gegevens willen openen of verwijderen uit uw gegevensopslag. Om aan deze evoluerende bedrijfsbehoeften te voldoen, biedt de Privacy Service een RESTful API en UI aan om toegang en schrappingsverzoeken voor klantengegevens over de toepassingen van Adobe Experience Cloud voor te leggen.

In deze handleiding worden de aanbevolen procedures beschreven voor het efficiënt verwerken van privacyverzoeken en het optimaliseren van de responstijden bij het beheren van verzoeken om klantgegevens.

## Aan de slag {#getting-started}

Deze handleiding vereist een goed begrip van [Privacy Service](./home.md) en hoe u hiermee toegang kunt beheren en aanvragen van uw betrokkenen (klanten) kunt verwijderen voor alle Adobe Experience Cloud-toepassingen. U wordt ook aangeraden de handleiding te hebben gelezen op [het creëren van een privacybaanverzoek in UI](./ui/user-guide.md#create-a-new-privacy-job-request) of [de API](./api/overview.md)en begrijpen hoe u deze bewerkingen programmatisch kunt uitvoeren.

## Vereisten {#prerequisites}

De toegang tot Adobe Experience Platform Privacy Service wordt gecontroleerd door granulaire op rol-gebaseerde toestemmingen in Adobe Admin Console. U hebt de relevante machtigingen in een productprofiel nodig om specifieke functies in de gebruikersinterface en de API van de Privacy Service te kunnen gebruiken. Neem contact op met de systeembeheerder als u aanvullende machtigingen nodig hebt.

Beheerders kunnen de handleiding raadplegen op [machtigingen voor Privacy Service beheren](./permissions.md) voor meer informatie .

## Richtlijnen voor het creëren van privacy-banen {#creation-guidelines}

Houd bij het maken van privacytaken rekening met de volgende richtlijnen om de verwerking van uw verzoek te stroomlijnen en de responstijden te verbeteren. Dit geldt voor zowel de API- als de UI-methoden.

1. **Gegevenssubjecten maximaliseren per aanvraag:** Neem zoveel mogelijk betrokkenen op, tot 1000 per aanvraag.
2. **Groeps-id&#39;s voor efficiëntie:** Groepeer meerdere id&#39;s voor één gegevenssubject (maximaal negen) in elke aanvraag. De **ID&#39;s kunnen afkomstig zijn van verschillende Adobe-services in dezelfde aanvraag**.
3. **Toegang combineren en taken verwijderen:** U kunt zowel taaktypen &quot;access&quot; als &quot;delete&quot; in één aanvraag opnemen als dat door de betrokkene is vereist.
4. **Alleen noodzakelijke producten opnemen:** Omvat slechts producten die worden vereist of vergunning gegeven. De extra producten kunnen verwerkingstijd verlengen en kosten verhogen.

## Status van privacytaken controleren {#monitor-status}

Privacy Service biedt drie methoden om privacytaken effectief te controleren en de status ervan te controleren. De beschikbare methoden worden hieronder vermeld in volgorde van efficiëntie en productiviteit. Elke methode bevat richtlijnen voor de beste praktijken om uw ervaring te verbeteren, gevolgd door een ideaal scenario-voorbeeld waarin alle benaderingen worden gecombineerd.

### real-time meldingen ontvangen {#real-time-notifications}

**I/O-gebeurtenissen** bieden vrijwel realtime statuscontrole via statusgebeurtenissen aan. Dit is de meest efficiënte methode, omdat hierdoor de noodzaak om opiniepeilingsmechanismen in te voeren en extra API-verkeer te veroorzaken wordt vermeden.

**Recommendations:**

- **Webhaak instellen:** Websites instellen om pushmeldingen te ontvangen wanneer statuswijzigingen optreden voor verzonden taken. Dit is een hulpmiddel bij realtimemonitoring.
- **Meldingen:** Gebruik meldingen op zowel taakniveau als productniveau om de voortgang van aanvragen te volgen.

Zie de documentatie op [abonneren op Privacy Service-gebeurtenissen](./privacy-events.md) voor instructies voor het instellen van een gebeurtenisregistratie voor meldingen van Privacys Service en voor het interpreteren van berichtladingen.

### Alle taken ophalen op basis van filters {#retrieve-filtered-responses-for-all-jobs}

Om al uw gegevens van de privacybaan terug te winnen die op om het even welke gespecificeerde filters worden gebaseerd, **voert een verzoek van de GET uit aan `/jobs` eindpunt**. Deze API-aanroep is handig om een weergave op hoog niveau te bieden van de huidige taakstatus voor grote sets met taak-id&#39;s met slechts één aanvraag. Het ontbreekt aan gedetailleerde productreacties, maar deze zijn te vinden met de [`/jobs/{jobID}` eindpunt](#retrieve-detailed-responses-for-specific-jobs).

Een verzoek van de GET aan `/jobs` het eindpunt wordt het best gebruikt om de statusgegevens van een grote reeks baan IDs te verzamelen of te vergelijken maar is **niet** bedoeld voor reguliere opiniepeilingactiviteiten.

**Recommendations:**

- **Parameters query:** Gebruik specifieke filters om uw resultaten te beperken, bijvoorbeeld: gegevensbereiken, regeltypen en status (verwerking, voltooid, enzovoort).

U kunt een lijst van alle huidige privacybanen in uw organisatie door de UI van de Privacy Service bekijken. Zie de [privacytaken beheren in de UI-documentatie](./ui/user-guide.md#job-requests) voor informatie over het filteren van de lijst met taakaanvragen. U kunt ook de documentatie op het tabblad [gebruik van het /job eindpunt in Privacy Service API](./api/privacy-jobs.md).

De Privacy Service API-documentatie bevat informatie over [de beschikbare filters van de vraagparameter](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#tag/Privacy-jobs/operation/listPrivacyJobs).

### Gedetailleerde antwoorden ophalen voor één taak {#retrieve-detailed-responses-for-specific-jobs}

Om gedetailleerde reacties voor één enkele baan terug te winnen, **voer een verzoek van de GET aan /job/ uit{jobID} eindpunt**. Deze methode is bedoeld voor het verdiepen van informatie, zoals productspecifieke reacties en succesberichten. Een vraag aan dit eindpunt is de beste manier om te zien welke producten hebben gereageerd en die nog hangende zijn, hoewel het is **niet** bedoeld voor reguliere opiniepeilingen.

Zie de `/jobs/{JOB_ID}` eindpuntdocumentatie voor details over [hoe de status van een specifieke baan kan worden gecontroleerd](./api/privacy-jobs.md#check-status).

### Ideal-scenario-voorbeeld {#ideal-scenario}

Gebruik een webhaak zodat het systeem automatisch records kan bijwerken en meldingen of waarschuwingen kan verstrekken wanneer groepen van de id&#39;s van een aanvraag zijn voltooid. Als er nog taken uitstaan, haalt het systeem deze taakstatus op met een aanvraag van een GET naar de Privacy Service-API `/jobs` en biedt een update op hoog niveau van de lijst.

Als een bepaalde taak nog in behandeling is of een fout heeft geretourneerd, kunt u de gedetailleerde reactie ophalen met een verzoek van de GET aan de `/job/{jobId}` eindpunt.

## Toegang tot aanvraaggegevens {#access-request-data}

Wanneer de gegevens-onderwerp informatie wordt gevraagd, keert elke dienst gegevens in een formaat terug dat met de manier verenigbaar is zij opslaan en die gegevens gebruiken. Nadat alle services de aanvraag hebben voltooid, wordt in de taakdetails een URL voor het ZIP-archiefbestand opgegeven, zodat deze gegevens kunnen worden gedownload. Zie de gids voor het oplossen van problemen voor informatie over [hoe te om privacybaanresultaten te downloaden](https://experienceleague.adobe.com/docs/experience-platform/privacy/troubleshooting-guide.html?lang=en#how-do-i-download-the-results-of-my-completed-privacy-jobs%3F).

Hieronder volgt een overzicht van de belangrijkste opmerkingen met betrekking tot het beheer van het gegevensarchief:

- Alle archiefbestanden worden na 30 dagen verwijderd van Experience Platform-servers. U kunt geen vragen stellen naar klantgegevens die ouder zijn dan 30 dagen.
- De structuur van het archiefbestand bevat mappen voor elk product dat in de aanvraag is opgenomen en de gegevensbestanden die daarin zijn opgenomen. Archiefbestanden of -mappen zijn mogelijk leeg als er geen gegevens zijn gevonden voor de opgegeven id.
- De gegevens voor eerder gecreëerde banen zijn slechts 30 dagen na de voltooiingsdatum toegankelijk. Daarna worden de gegevens uit het systeem verwijderd en moet een nieuw verzoek worden ingediend.

**Recommendations:**

- **Protect-gegevensarchieven:** Zowel het URL- als het ZIP-bestand moeten worden beschermd, omdat het persoonlijk identificeerbare gegevens (PII) voor de betrokkene kan bevatten.

## Technische overwegingen {#technical-considerations}

Bij het invullen van een verzoek om Privacy Service moet u rekening houden met een aantal technische aspecten:

- **Bewaarperiode gegevens:** De maximale terugkijkperiode is 60 dagen voor om het even welke groep banen, en de maximumtijdspanwijdte voor een vraag is 30 dagen (van/aan data).
- **Time-out gateway:** Houd er rekening mee dat uw verzoek van de gateway kan worden neergezet als het langer is dan 60 seconden.
- **Foutverwerking:** Controleer de foutberichten grondig en verzend verzoeken waar nodig opnieuw. Privacy Service verwerkt taken niet automatisch na een fout.
- **HTTP 429-fouten begrijpen:** Verken uzelf met HTTP 429-foutberichten en de noodzakelijke stappen om problemen te verhelpen. HTTP 429 fouten zijn het resultaat van &quot;Te veel verzoeken&quot;. Zie de [Algemene foutberichten](./troubleshooting-guide.md#common-error-messages) in de gids voor probleemoplossing vindt u meer informatie over het oplossen van dit probleem.

## Volgende stappen

Door dit document te lezen beschikt u nu over de benodigde kennis en praktijken voor een efficiënt en doeltreffend gebruik van de Privacy Service. Zie de [gids voor problemen](./troubleshooting-guide.md) voor antwoorden op veelgestelde vragen over Privacy Service, en informatie over algemeen ondervonden fouten in API.
