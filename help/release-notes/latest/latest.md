---
title: 'Aanvullende informatie van januari 2026 voor Adobe Experience Platform '
description: Aanvullende informatie van januari 2026 voor Adobe Experience Platform.
source-git-commit: 9a3fbe281195041cf7444c5b6ec185395ff5ad23
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 24%

---


# Aanvullende informatie voor Adobe Experience Platform

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/nl/docs/analytics-platform/using/releases/pre-release-notes)
>- [Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: woensdag 27 januari 2026**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

<!-- - [Agent Orchestrator](#agent-orchestrator) -->

- [Bestemmingen](#destinations)
- [Real-Time Customer Profile](#real-time-customer-profile)
- [Schema&#39;s](#schemas)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

<!-- ## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator enables you to build and deploy AI-powered agents that can automate workflows and interact with customers across multiple channels.

**New or updated features**

| Feature | Description |
| --- | --- |
| Trial motion for Adobe Experience Platform Agents | **Select customers now have access to Adobe Experience Platform Agents for a complimentary trial**, enabling them to explore and interact with these Agents through the AI Assistant interface powered by Adobe Experience Platform Agent Orchestrator. The trial offers hands-on experience with AI Agents that operate within the context of customers' existing Experience Cloud products and environments, allowing teams to evaluate value before committing to a full purchase. Adobe Experience Platform Agents are guided by user input and oversight and respect existing product-level access controls, ensuring users can only perform actions or view data for which they are authorized within the underlying Experience Cloud applications.|

{style="table-layout:auto"}

For more information, see the [Agent Orchestrator documentation](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator). -->

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms waarmee gegevens uit Experience Platform naadloos kunnen worden geactiveerd. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| Kevel-bestemmingsconnector nu beschikbaar | Met de [!DNL Kevel] streamingbestemming voor Adobe Experience Platform kunnen klanten Adobe-doelgroepen rechtstreeks activeren in de gebruikersdatabase- en segmentbeheerAPI&#39;s van [!DNL Kevel] voor ondersteuning van realtime doelwitten tijdens de besluitvorming. [[!DNL Kevel] &#x200B;](https://www.kevel.com/) verstrekt de AI-Toegelaten technologie en deskundige begeleiding die innovatieve handelsleiders helpen lanceren, schrapen, en slagen in handelsmedia. De Retail Media Cloud-bevoegdheden van [!DNL Kevel] zijn gericht op, aanpasbare en aanpasbare advertentievormen voor on-site en off-site reclame. |
| De bestemmingsschakelaar van de Uitwisseling van de index nu beschikbaar | Gebruik deze bestemmingsschakelaar om publiekssegmenten van Adobe Experience Platform rechtstreeks naar het programmatic reclameplatform van [!DNL Index Exchange] uit te voeren. [!DNL Index] is een wereldwijd advertentieplatform dat media-eigenaars helpt de waarde van hun inhoud op elk scherm te maximaliseren. Met meer dan 20 jaar toonaangevend in de branche verbindt [!DNL Index] de grootste merken ter wereld met toonaangevende ervaren makers om hoogwaardige consumentenervaringen te bieden. |
| Regionale steun voor eindpunten voor verbindingen van het type Braze | Alle [&#x200B; gebied-specifieke eindpunten &#x200B;](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) die door [!DNL Braze] worden gesteund zijn nu beschikbaar voor selectie tijdens de stroom van de bestemmingsconfiguratie. Vraag uw [!DNL Braze] vertegenwoordiger welke eindpuntinstantie u zou moeten gebruiken. |
| Wekelijks en maandelijkse het plannen steun voor [&#x200B; Liveramp Onboarding &#x200B;](../../destinations/catalog/advertising/liveramp-onboarding.md#scheduling) | U kunt nu wekelijkse en maandelijkse exportschema&#39;s configureren voor de bestemming Liveramp aan boord. <br> Deze release wordt geleidelijk uitgevoerd en is op 30 januari voltooid. |
| Verbeterde activeringservaring voor [&#x200B; de Commerciële Desk &#x200B;](../../destinations/catalog/advertising/tradedesk.md) en [&#x200B; Microsoft Bing &#x200B;](../../destinations/catalog/advertising/bing.md) bestemmingen | De handelsbureau en de bestemmingen van de Bing van Microsoft omvatten nu vooraf bepaalde verplichte afbeeldingen voor een geoptimaliseerde activeringservaring.  <br> Deze release wordt geleidelijk uitgevoerd en is op 30 januari voltooid. |

<!-- |AES256 encryption support for [Amazon S3](../../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) destinations | You can now configure AES256 encryption for your Amazon S3 exports. Two options are available: <br><br>**[!UICONTROL Default]**: If you don't have any custom policies applied on your buckets, data will be encrypted at rest when it lands in S3 with the AES256 algorithm. However, if you have custom policies applied, Experience Platform will respect those policies and Amazon S3 will continue to apply whichever custom encryption policies you have configured.<br><br>**[!UICONTROL SSE-S3/AES256]**: Experience Platform adds the `s3:x-amz-server-side-encryption": "AES256` header in the export and data will be encrypted at rest when it lands in S3 with the AES256 algorithm. | -->


**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Bijgewerkte guardrailgrenzen voor [&#x200B; Adobe Target &#x200B;](../../destinations/catalog/personalization/adobe-target-connection.md) bestemmingen | Het maximumaantal doelgroepen dat aan één Adobe Target-bestemming kan worden toegewezen, is verhoogd van 50 naar 250. Hierdoor wordt Adobe Target uitgelijnd op de standaardpubliekslimiet voor andere doelen, waardoor workflows voor publieksactivering flexibeler worden. U kunt nu meer soorten publiek activeren naar Adobe Target-doelen zonder dat u meerdere gegevensstromen hoeft te maken. |
| [&#x200B; geeft bestemmingen &#x200B;](/help/destinations/ui/edit-destination.md) uit en [&#x200B; geeft marketing acties &#x200B;](/help/destinations/ui/edit-activation.md#edit-marketing-actions) algemene beschikbaarheid uit | De optie om bestemmingen en marketingacties te bewerken is nu beschikbaar voor alle gebruikers. |
| De namen van de gebiedsvertoning van de knevel in de Afbeelding [&#x200B; stap &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) | Wanneer u schemavelden toewijst aan een doel, kunt u nu schakelen tussen het weergeven van de volledige XDM-veldnaam en het weergeven van alleen de weergavenaam. <br> ![&#x200B; opname van het Scherm die de knevel van de vertoningsnaam tonen.](/help/release-notes/2026/assets/january/show-display-names.gif) |

{style="table-layout:auto"}

Voor meer informatie leest u het [overzicht van bestemmingen](../../destinations/home.md).

## Real-Time Customer Profile {#real-time-customer-profile}

In real time het Profiel van de Klant laat u toe om een holistische mening van elke individuele klant te zien door gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens te combineren. Het profiel staat u toe om uw klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [&#x200B; het stromen capaciteit &#x200B;](/help/landing/license-usage-and-guardrails/capacity.md) handhaving | Experience Platform dwingt nu streamingdoorvoer af voor realtime klantprofiel en identiteitsservice. Wanneer klanten hun gecontracteerde streamingcapaciteit overschrijden, worden de gegevens in de wachtrij geplaatst en verwerkt op een first-in-first-out manier. Dit zorgt voor voorspelbare systeemprestaties en voorkomt dat capaciteitsschendingen van invloed zijn op de kwaliteit van gegevensinvoer. Belangrijke opmerkingen: <ul><li>Streaming upserts zijn niet beschikbaar op het datumpomeer wanneer de capaciteit wordt overschreden</li><li>Deze handhaving geldt niet voor klanten met Adobe Journey Optimizer-licenties</li><li>Gegevens in de wachtrij worden opeenvolgend verwerkt zodra capaciteit beschikbaar is.</li></ul> Voor meer informatie, lees het [&#x200B; capaciteitsoverzicht &#x200B;](/help/landing/license-usage-and-guardrails/capacity.md). |
| Afstand van opzoekopdracht door entiteit | Het gebruik van de zoekAPI voor entiteiten voor ervaringsgebeurtenissen is nu afgekeurd voor alle Real-Time CDP Prime-klanten. Deze afleiding helpt Real-Time CDP uit te lijnen met de licentiefunctionaliteit. Real-Time CDP Ultimate-klanten die van plan zijn deze functionaliteit te gebruiken, kunnen contact opnemen met de klantenservice van Adobe om deze functie opnieuw in te schakelen.  Voor meer informatie, lees de [&#x200B; entiteiten API gids &#x200B;](/help/profile/api/entities.md). |
| Taakstatus van het opnemen van profielen controleren | U kunt nu het voortgangspercentage op taakniveau controleren voor het invoeren van batch-profielen na uitvoering. Deze functie biedt realtime zichtbaarheid in de huidige voortgang van taken voor batchinvoer, inclusief kritieke controlepunten die aangeven of de opname gereed is voor segmentatie van klanten en Adobe Journey Optimizer-opzoekingen. Voor grote ingesties die verscheidene uren kunnen vergen om te verwerken, helpt deze vooruitgangstransparantie u begrijpen of de baan normaal of het ontmoeten kwesties vordert, die onzekerheid tijdens gegevensverwerking verminderen.Voor meer informatie, lees de [&#x200B; gids van monitorprofielen &#x200B;](/help/dataflows/ui/monitor-profiles.md). |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [[!DNL Real-Time Customer Profile] overzicht](../../profile/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Vernieuwen van externe publieksgegevens | Extern publiek (zoals CSV-uploads) ondersteunt nu een functie voor forceren vernieuwen voor instellingen voor gegevensvervaldatum. Met deze functie kunnen gebruikers de gegevensvervaldatum voor externe doelgroepen handmatig vernieuwen, zodat ze meer controle hebben over het levenscyclusbeheer van de doelgroep. Dit is met name handig voor doelgroepen die langer moeten blijven dan hun oorspronkelijke gegevensvervaldatum of die opnieuw moeten worden geactiveerd zonder dat de gegevens opnieuw moeten worden geüpload. Voor meer informatie over deze eigenschap, lees het [&#x200B; Poortoverzicht van het Poortpubliek van het publiek &#x200B;](../../segmentation/ui/audience-portal.md#audience-summary). |

Voor meer informatie raadpleegt u het [[!DNL Segmentation Service] overzicht](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte bronnen**

| Bron | Beschrijving |
| --- | --- |
| [[!DNL Oracle Eloqua]](/help/sources/connectors/marketing-automation/eloqua.md) V2-bron | Een nieuwe [!DNL Oracle Eloqua] bronschakelaar is nu beschikbaar, die [&#x200B; vervangen schakelaar &#x200B;](/help/sources/connectors/marketing-automation/oracle-eloqua.md). Deze bijgewerkte connector biedt verbeterde functionaliteit en verbeterde betrouwbaarheid voor het opnemen van gegevens van [!DNL Oracle Eloqua] in Experience Platform. Klanten die de bestaande connector gebruiken, moeten migreren naar de nieuwe implementatie, omdat bestaande verbindingen niet meer werken. De nieuwe schakelaar steunt alle opstelling en configuratiestappen nodig om met [!DNL Oracle Eloqua] te verbinden en marketingautomatiseringsgegevens in te voeren. |
| [[!DNL Salesforce Marketing Cloud]](/help/sources/connectors/marketing-automation/sfmc.md) V2-bron | Een nieuwe [!DNL Salesforce Marketing Cloud] bronschakelaar is nu beschikbaar, die [&#x200B; vervangen schakelaar &#x200B;](/help/sources/connectors/marketing-automation/salesforce-marketing-cloud.md). Deze bijgewerkte connector biedt betere prestaties en extra mogelijkheden voor het opnemen van gegevens van [!DNL Salesforce Marketing Cloud] in Experience Platform. De klanten die de bestaande schakelaar gebruiken zouden overgang aan de nieuwe implementatie moeten. De nieuwe connector bevat uitgebreide installatie-instructies voor het maken van verbinding met [!DNL Salesforce Marketing Cloud] en het invoeren van gegevens over marketingautomatisering. |

Voor meer informatie raadpleegt u het [overzicht van bronnen](../../sources/home.md).

