---
title: Opmerkingen bij de release Experience Platform
description: Een voorvertoning van de meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 76e8f0678c4634258170ca1161134dd1176c24e7
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 22%

---

# Opmerkingen bij de release Adobe Experience Platform

>[!IMPORTANT]
>
>Dit document is voorgenomen als a **voorproef** van de versienota&#39;s voor de huidige maand. Release-items kunnen worden gewijzigd en worden toegevoegd of verwijderd in de definitieve versie.

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/nl/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/nl/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/nl/docs/analytics-platform/using/releases/pre-release-notes)
>- [Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**Datum van de Versie: Januari 2026**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Bestemmingen](#destinations)
- [Realtime-klantenprofiel](#real-time-customer-profile)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

## Agent Orchestrator {#agent-orchestrator}

Met Agent Orchestrator kunt u op AI gebaseerde agents maken en implementeren die workflows kunnen automatiseren en op meerdere kanalen met klanten kunnen communiceren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Testbeweging voor Agent Orchestrator | Agent Orchestrator biedt nu een proefversie waarmee klanten de service kunnen verkennen en testen voordat ze een volledige aankoop doen. Met deze optie voor het begin van de aankoop kunnen organisaties in hun eigen omgeving de mogelijkheden van Agent Orchestrator evalueren, inclusief vaardigheden en functies voor het organiseren van projecten. De proef verstrekt hands-on ervaring met de bouw van AI-aangedreven agenten en het begrip hoe zij in bestaande werkschema&#39;s kunnen worden geïntegreerd. |

{style="table-layout:auto"}

Voor meer informatie, zie de [&#x200B; documentatie van Agent Orchestrator &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms waarmee gegevens uit Experience Platform naadloos kunnen worden geactiveerd. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| Kevel-bestemmingsconnector nu beschikbaar | [[!DNL Kevel] &#x200B;](https://www.kevel.com/) verstrekt de AI-Toegelaten technologie en deskundige begeleiding die innovatieve handelsleiders helpen lanceren, schrapen, en slagen in handelsmedia. De Retail Media Cloud-bevoegdheden van [!DNL Kevel] zijn gericht op, aanpasbare en aanpasbare advertentievormen voor on-site en off-site reclame. |
| De bestemmingsschakelaar van de Uitwisseling van de index nu beschikbaar | [!DNL Index] is een wereldwijd advertentieplatform dat media-eigenaars helpt de waarde van hun inhoud op elk scherm te maximaliseren. Met meer dan 20 jaar toonaangevend in de branche verbindt [!DNL Index] de grootste merken ter wereld met toonaangevende ervaren makers om hoogwaardige consumentenervaringen te bieden. |
| Regionale steun voor eindpunten voor verbindingen van het type Braze | Alle [&#x200B; gebied-specifieke eindpunten &#x200B;](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) die door [!DNL Braze] worden gesteund zijn nu beschikbaar voor selectie tijdens de stroom van de bestemmingsconfiguratie. Vraag uw [!DNL Braze] vertegenwoordiger welke eindpuntinstantie u zou moeten gebruiken. |
| Ondersteuning voor wekelijkse en maandelijkse planningen van Liveramp Onboarding | U kunt nu wekelijkse en maandelijkse exportschema&#39;s configureren voor de bestemming Liveramp aan boord. |
| AES256 encryptiesteun voor Amazon S3 bestemmingen | U kunt nu AES256-codering configureren voor uw Amazon S3-export. |
| Verbeterde activeringservaring voor de bestemmingen Trade Desk en Microsoft Bing | De handelsbureau en de bestemmingen van de Bing van Microsoft omvatten nu vooraf bepaalde verplichte afbeeldingen voor een geoptimaliseerde activeringservaring. |

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Bijgewerkte guardraillimieten voor Adobe Target-bestemming | Het maximumaantal doelgroepen dat aan één Adobe Target-bestemming kan worden toegewezen, is verhoogd van 50 naar 250. Hierdoor wordt Adobe Target uitgelijnd op de standaardpubliekslimiet voor andere doelen, waardoor workflows voor publieksactivering flexibeler worden. U kunt nu meer soorten publiek activeren naar Adobe Target-doelen zonder dat u meerdere gegevensstromen hoeft te maken. |
| [&#x200B; geeft bestemmingen &#x200B;](/help/destinations/ui/edit-destination.md) uit en [&#x200B; geeft marketing acties &#x200B;](/help/destinations/ui/edit-activation.md#edit-marketing-actions) algemene beschikbaarheid uit | De optie om bestemmingen en marketingacties te bewerken is nu beschikbaar voor alle gebruikers. |
| Veldweergavenamen in-/uitschakelen in toewijzingsstap | Wanneer u schemavelden toewijst aan een doel, kunt u nu schakelen tussen het weergeven van de volledige XDM-veldnaam en het weergeven van alleen de weergavenaam. |

{style="table-layout:auto"}

Voor meer informatie leest u het [overzicht van bestemmingen](../destinations/home.md).

## Real-Time Customer Profile {#real-time-customer-profile}

In real time het Profiel van de Klant laat u toe om een holistische mening van elke individuele klant te zien door gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens te combineren. Het profiel staat u toe om uw klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Handhaving van streaming capaciteit | Experience Platform dwingt nu streamingdoorvoer af voor realtime klantprofiel en identiteitsservice. Wanneer klanten hun gecontracteerde streamingcapaciteit overschrijden, worden de gegevens in de wachtrij geplaatst en verwerkt op een first-in-first-out manier. Dit zorgt voor voorspelbare systeemprestaties en voorkomt dat capaciteitsschendingen van invloed zijn op de kwaliteit van gegevensinvoer. Belangrijke opmerkingen: streamingupserts zijn niet beschikbaar op het datumpigment wanneer de capaciteit wordt overschreden, deze handhaving geldt niet voor klanten met Adobe Journey Optimizer-licenties en gegevens in de wachtrij worden opeenvolgend verwerkt zodra de capaciteit beschikbaar is. |
| Verouderde API-toegang voor Real-Time CDP Prime | API-toegang voor ervaringsgebeurtenissen is nu afgekeurd voor alle Real-Time CDP Prime-klanten. Deze wijziging is van invloed op de mogelijkheid om rechtstreeks via API query&#39;s uit te voeren op ervaringsgebeurtenissen. Real-Time CDP Ultimate-klanten kunnen een uitzondering aanvragen via een formeel uitzonderingsproces om toegang tot API-ervaringsgebeurtenissen mogelijk te maken als dat nodig is voor hun gebruiksscenario&#39;s. Deze afleiding helpt Real-Time CDP uit te lijnen met de licentiefunctionaliteit. |
| Monitorgegevensstroom | U kunt de vooruitgang en de bereidheid van dataflow looppas in Profiel nu controleren. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [[!DNL Real-Time Customer Profile] overzicht](../profile/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| TTL voor extern publiek vernieuwen | Externe doelgroepen (zoals CSV-uploads) ondersteunen nu een functie voor forceren vernieuwen voor instellingen voor tijd tot live (TTL). Met deze functie kunnen gebruikers de vervaldatum van de TTL handmatig vernieuwen voor externe doelgroepen, zodat ze meer controle hebben over het levenscyclusbeheer van de doelgroep. Dit is met name nuttig voor doelgroepen die na hun eerste TTL-periode moeten blijven of opnieuw moeten worden geactiveerd zonder de gegevens opnieuw te uploaden. |

Voor meer informatie raadpleegt u het [[!DNL Segmentation Service] overzicht](../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte bronnen**

| Bron | Beschrijving |
| --- | --- |
| [!DNL Oracle Eloqua] V2-bron | Er is nu een nieuwe [!DNL Oracle Eloqua] bronconnector beschikbaar, die de afgekeurde connector vervangt. Deze bijgewerkte connector biedt verbeterde functionaliteit en verbeterde betrouwbaarheid voor het opnemen van gegevens van [!DNL Oracle Eloqua] in Experience Platform. Klanten die de bestaande connector gebruiken, moeten migreren naar de nieuwe implementatie, omdat bestaande verbindingen niet meer werken. De nieuwe schakelaar steunt alle opstelling en configuratiestappen nodig om met [!DNL Oracle Eloqua] te verbinden en marketingautomatiseringsgegevens in te voeren. |
| [!DNL Salesforce Marketing Cloud] V2-bron | Er is nu een nieuwe [!DNL Salesforce Marketing Cloud] bronconnector beschikbaar, die de afgekeurde connector vervangt. Deze bijgewerkte connector biedt betere prestaties en extra mogelijkheden voor het opnemen van gegevens van [!DNL Salesforce Marketing Cloud] in Experience Platform. De klanten die de bestaande schakelaar gebruiken zouden overgang aan de nieuwe implementatie moeten. De nieuwe connector bevat uitgebreide installatie-instructies voor het maken van verbinding met [!DNL Salesforce Marketing Cloud] en het invoeren van gegevens over marketingautomatisering. |

Voor meer informatie raadpleegt u het [overzicht van bronnen](../sources/home.md).

