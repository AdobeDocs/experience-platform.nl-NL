---
title: 'Aanvullende informatie van januari 2026 voor Adobe Experience Platform '
description: Aanvullende informatie van januari 2026 voor Adobe Experience Platform.
source-git-commit: 1761acbcab12acf1596daf5461476d5b91bb0e9b
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 22%

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

- [Agent Orchestrator](#agent-orchestrator)
- [Bestemmingen](#destinations)
- [Real-Time Customer Profile](#real-time-customer-profile)
- [Schema&#39;s](#schemas)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

## Agent Orchestrator {#agent-orchestrator}

Met Agent Orchestrator kunt u op AI gebaseerde agents maken en implementeren die workflows kunnen automatiseren en op meerdere kanalen met klanten kunnen communiceren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Gebruiksgebonden proefversie van Adobe Experience Platform Agents | **Uitgezochte klanten hebben nu een gratis proeftoegang tot de Agenten van Adobe Experience Platform**. U kunt de proef gebruiken om met Agenten door de AI Hulp interface te onderzoeken en in wisselwerking te staan die door Adobe Experience Platform Agent Orchestrator wordt aangedreven. De proef biedt hands-on ervaring met AI Agenten die binnen de context van de bestaande producten en milieu&#39;s van Experience Cloud van klanten werken, die teams toestaan om waarde te evalueren alvorens aan een volledige aankoop te verbinden. Adobe Experience Platform Agents worden begeleid door gebruikersinvoer en -toezicht en respecteren bestaande toegangscontroles op productniveau, zodat gebruikers alleen handelingen kunnen uitvoeren of gegevens kunnen bekijken waarvoor ze zijn geautoriseerd in de onderliggende Experience Cloud-toepassingen. Lees het [ gebruik-gebonden proefoverzicht van de Agenten van Experience Platform ](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/trial) voor informatie over hoe te begonnen worden. |

{style="table-layout:auto"}

Voor meer informatie, zie de [ documentatie van Agent Orchestrator ](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms waarmee gegevens uit Experience Platform naadloos kunnen worden geactiveerd. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [ Kevel bestemmings ](/help/destinations/catalog/advertising/kevel.md) schakelaar nu beschikbaar | Met de [!DNL Kevel] streamingbestemming voor Adobe Experience Platform kunnen klanten Adobe-doelgroepen rechtstreeks activeren in de gebruikersdatabase- en segmentbeheerAPI&#39;s van [!DNL Kevel] voor ondersteuning van realtime doelwitten tijdens de besluitvorming. [[!DNL Kevel] ](https://www.kevel.com/) verstrekt de AI-Toegelaten technologie en deskundige begeleiding die innovatieve handelsleiders helpen lanceren, schrapen, en slagen in handelsmedia. De Retail Media Cloud-bevoegdheden van [!DNL Kevel] zijn gericht op, aanpasbare en aanpasbare advertentievormen voor on-site en off-site reclame. |
| [ de bestemmingsschakelaar van de Uitwisseling van de Index 10} nu beschikbaar](/help/destinations/catalog/advertising/index-exchange.md) | Gebruik deze bestemmingsschakelaar om publiekssegmenten van Adobe Experience Platform rechtstreeks naar het programmatic reclameplatform van [!DNL Index Exchange] uit te voeren. [!DNL Index] is een wereldwijd advertentieplatform dat media-eigenaars helpt de waarde van hun inhoud op elk scherm te maximaliseren. Met meer dan 20 jaar toonaangevend in de branche verbindt [!DNL Index] de grootste merken ter wereld met toonaangevende ervaren makers om hoogwaardige consumentenervaringen te bieden. |
| Regionale steun voor eindpunten voor verbindingen van het type Braze | Alle [ gebied-specifieke eindpunten ](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) die door [!DNL Braze] worden gesteund zijn nu beschikbaar voor selectie tijdens de stroom van de bestemmingsconfiguratie. Vraag uw [!DNL Braze] vertegenwoordiger welke eindpuntinstantie u zou moeten gebruiken. |
| Wekelijks en maandelijkse het plannen steun voor [ Liveramp Onboarding ](../../destinations/catalog/advertising/liveramp-onboarding.md#scheduling) | U kunt nu wekelijkse en maandelijkse exportschema&#39;s configureren voor de bestemming Liveramp aan boord. <br> Deze release wordt geleidelijk uitgevoerd en is op 30 januari voltooid. |
| Verbeterde activeringservaring voor [ de Commerciële Desk ](../../destinations/catalog/advertising/tradedesk.md) en [ Microsoft Bing ](../../destinations/catalog/advertising/bing.md) bestemmingen | De handelsbureau en de bestemmingen van de Bing van Microsoft omvatten nu vooraf bepaalde verplichte afbeeldingen voor een geoptimaliseerde activeringservaring.  <br> Deze release wordt geleidelijk uitgevoerd en is op 30 januari voltooid. ![ Beeld die vooraf bepaalde afbeeldingen voor de Handelsplaats tonen ](assets/january/mandatory-mappings-ttd.png) {width="150" align="center" zoomable="yes"} <br> ![ Beeld die vooraf bepaalde afbeeldingen voor het Bing van Microsoft tonen ](assets/january/mandatory-mappings-bing.png) {width="150" align="center" zoomable="yes"} |
| De steun van de activering van het aantal van de telefoon voor [ de Trade Desk - CRM ](../../destinations/catalog/advertising/tradedesk-emails.md#phone-hashing) verbinding | De plaats van de Handel - bestemming CRM steunt nu telefoonnummeractivering naast e-mailadressen. U kunt zowel unhashed telefoonaantallen in formaat E.164 als gehakt telefoonaantallen (formaat SHA256_E.164) aan uw rekening van het Bureau van de Handel voor publiek activeren richtend en onderdrukking die op de gegevens van CRM wordt gebaseerd. Telefoonnummers moeten worden genormaliseerd naar E.164-indeling voordat ze kunnen worden geactiveerd. |
| [ bestemmingsupdates van de Partij van 0} Snowflake {](../../destinations/catalog/warehouses/snowflake-batch.md) | De Snowflake Batch-bestemming bevat nu mogelijkheden voor het selecteren van gebieden tijdens de doelconfiguratie. U kunt nu de specifieke Snowflake-regio selecteren waar uw exemplaar is ingericht, zodat u verzekerd bent van optimale gegevensoverdracht en de regionale vereisten kunt naleven. Bovendien, is de standaardbeperking van het fusiebeleid verwijderd, toestaand u om publiek uit te voeren dat aan om het even welk fusiebeleid in kaart wordt gebracht. <br> De batchbestemming [!DNL Snowflake] is momenteel alleen beschikbaar voor Real-Time CDP-klanten die zijn ingericht in het Experience Platform VA7-gebied. |


<!-- |AES256 encryption support for [Amazon S3](../../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) destinations | You can now configure AES256 encryption for your Amazon S3 exports. Two options are available: <ul><li>**[!UICONTROL Default]**: Data will be encrypted at rest with the default encryption algorithm set on your bucket.</li><li>**[!UICONTROL SSE-S3/AES256]**: Experience Platform adds the `s3:x-amz-server-side-encryption": "AES256` header in the export and data will be encrypted at rest with the AES256 algorithm when it lands in S3. **This option takes precedence over any default encryption algorithm configured on your S3 bucket**.</li></ul> This release is being rolled out gradually and will be complete by January 30th.| -->

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Bijgewerkte guardrailgrenzen voor [ Adobe Target ](../../destinations/catalog/personalization/adobe-target-connection.md) bestemmingen | Het maximumaantal doelgroepen dat aan één Adobe Target-bestemming kan worden toegewezen, is verhoogd van 50 naar 250. Hierdoor wordt Adobe Target uitgelijnd op de standaardpubliekslimiet voor andere doelen, waardoor workflows voor publieksactivering flexibeler worden. U kunt nu meer soorten publiek activeren naar Adobe Target-doelen zonder dat u meerdere gegevensstromen hoeft te maken. |
| [ geeft bestemmingen ](/help/destinations/ui/edit-destination.md) uit en [ geeft marketing acties ](/help/destinations/ui/edit-activation.md#edit-marketing-actions) algemene beschikbaarheid uit | De optie om bestemmingen en marketingacties te bewerken is nu beschikbaar voor alle gebruikers. |
| De namen van de gebiedsvertoning van de knevel in de Afbeelding [ stap ](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) | Wanneer u schemavelden toewijst aan een doel, kunt u nu schakelen tussen het weergeven van de volledige XDM-veldnaam en het weergeven van alleen de weergavenaam. <br> ![ opname van het Scherm die de knevel van de vertoningsnaam tonen.](/help/release-notes/2026/assets/january/show-display-names.gif) |

{style="table-layout:auto"}

Voor meer informatie leest u het [overzicht van bestemmingen](../../destinations/home.md).

## Real-Time Customer Profile {#real-time-customer-profile}

In real time het Profiel van de Klant laat u toe om een holistische mening van elke individuele klant te zien door gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens te combineren. Het profiel staat u toe om uw klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [ het stromen capaciteit ](/help/landing/license-usage-and-guardrails/capacity.md) handhaving | Experience Platform dwingt nu streamingdoorvoer af voor realtime klantprofiel en identiteitsservice. Wanneer klanten hun gecontracteerde streamingcapaciteit overschrijden, worden de gegevens in de wachtrij geplaatst en verwerkt op een first-in-first-out manier. Dit zorgt voor voorspelbare systeemprestaties en voorkomt dat capaciteitsschendingen van invloed zijn op de kwaliteit van gegevensinvoer. Belangrijke opmerkingen: <ul><li>Streaming upserts zijn niet beschikbaar op het datumpomeer wanneer de capaciteit wordt overschreden</li><li>Deze handhaving geldt niet voor klanten met Adobe Journey Optimizer-licenties</li><li>Gegevens in de wachtrij worden opeenvolgend verwerkt zodra capaciteit beschikbaar is.</li></ul> Voor meer informatie, lees het [ capaciteitsoverzicht ](/help/landing/license-usage-and-guardrails/capacity.md). |
| Afstand van opzoekopdracht door entiteit | Het gebruik van de zoekAPI voor entiteiten voor ervaringsgebeurtenissen is nu afgekeurd voor alle Real-Time CDP Prime-klanten. Deze afleiding helpt Real-Time CDP uit te lijnen met de licentiefunctionaliteit. Real-Time CDP Ultimate-klanten die van plan zijn deze functionaliteit te gebruiken, kunnen contact opnemen met de klantenservice van Adobe om deze functie opnieuw in te schakelen.  Voor meer informatie, lees de [ entiteiten API gids ](/help/profile/api/entities.md). |
| Taakstatus van het opnemen van profielen controleren | U kunt nu het voortgangspercentage op taakniveau controleren voor het invoeren van batch-profielen na uitvoering. Deze functie biedt realtime zichtbaarheid in de huidige voortgang van taken voor batchinvoer, inclusief kritieke controlepunten die aangeven of de opname gereed is voor segmentatie van klanten en Adobe Journey Optimizer-opzoekingen. Voor grote ingesties die verscheidene uren kunnen vergen om te verwerken, helpt deze vooruitgangstransparantie u begrijpen of de baan normaal of het ontmoeten kwesties vordert, die onzekerheid tijdens gegevensverwerking verminderen.Voor meer informatie, lees de [ gids van monitorprofielen ](/help/dataflows/ui/monitor-profiles.md). |
| Verbeteringen voor profielviewer (GA) | De volgende verbeteringen in de profielviewer zijn nu over het algemeen beschikbaar. <ul><li>**Gecombineerde weergave**: kenmerken, gebeurtenissen, en inzichten zijn gecombineerd in één enkele weergave.</li><li>**Door AI gegenereerde inzichten**: op de pagina met profielgegevens worden nu door AI gegenereerde inzichten weergegeven, zodat u weet welke gegevens uit uw profiel zijn gegenereerd. Deze inzichten kunnen informatie omvatten zoals propensity-scores en trendanalyse.</li><li>**Stijlupdate**: de pagina met profielgegevens is visueel vernieuwd.</li><li>**Bladeren**: u kunt nu uw profielen verkennen via een interactieve, op kaarten gebaseerde carrousel met zoek- en aanpassingsmogelijkheden.</li></ul> Voor meer informatie, lees de [ gids van de profielkijker ](/help/profile/ui/user-guide.md). |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [[!DNL Real-Time Customer Profile] overzicht](../../profile/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Vernieuwen van externe publieksgegevens | Extern publiek (zoals CSV-uploads) ondersteunt nu een functie voor forceren vernieuwen voor instellingen voor gegevensvervaldatum. Met deze functie kunnen gebruikers de gegevensvervaldatum voor externe doelgroepen handmatig vernieuwen, zodat ze meer controle hebben over het levenscyclusbeheer van de doelgroep. Dit is met name handig voor doelgroepen die langer moeten blijven dan hun oorspronkelijke gegevensvervaldatum of die opnieuw moeten worden geactiveerd zonder dat de gegevens opnieuw moeten worden geüpload. Voor meer informatie over deze eigenschap, lees het [ Poortoverzicht van het Poortpubliek van het publiek ](../../segmentation/ui/audience-portal.md#audience-summary). |
| Validatie van publiek | Experience Platform biedt nu ingebouwde validaties om ervoor te zorgen dat uw publiek nauwkeurig, stabiel en schaalbaar is. Deze controles worden automatisch in real time in werking gesteld terwijl u uw publieksdefinities creeert. Voor meer informatie, lees het [ overzicht van de publieksbevestiging ](/help/segmentation/validation.md). |

Voor meer informatie raadpleegt u het [[!DNL Segmentation Service] overzicht](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte bronnen**

| Bron | Beschrijving |
| --- | --- |
| [[!DNL Oracle Eloqua]](/help/sources/connectors/marketing-automation/eloqua.md) V2-bron | Een nieuwe [!DNL Oracle Eloqua] bronschakelaar is nu beschikbaar, die [ vervangen schakelaar ](/help/sources/connectors/marketing-automation/oracle-eloqua.md). Deze bijgewerkte connector biedt verbeterde functionaliteit en verbeterde betrouwbaarheid voor het opnemen van gegevens van [!DNL Oracle Eloqua] in Experience Platform. Klanten die de bestaande connector gebruiken, moeten migreren naar de nieuwe implementatie, omdat bestaande verbindingen niet meer werken. De nieuwe schakelaar steunt alle opstelling en configuratiestappen nodig om met [!DNL Oracle Eloqua] te verbinden en marketingautomatiseringsgegevens in te voeren. |
| [[!DNL Salesforce Marketing Cloud]](/help/sources/connectors/marketing-automation/sfmc.md) V2-bron | Een nieuwe [!DNL Salesforce Marketing Cloud] bronschakelaar is nu beschikbaar, die [ vervangen schakelaar ](/help/sources/connectors/marketing-automation/salesforce-marketing-cloud.md). Deze bijgewerkte connector biedt betere prestaties en extra mogelijkheden voor het opnemen van gegevens van [!DNL Salesforce Marketing Cloud] in Experience Platform. De klanten die de bestaande schakelaar gebruiken zouden overgang aan de nieuwe implementatie moeten. De nieuwe connector bevat uitgebreide installatie-instructies voor het maken van verbinding met [!DNL Salesforce Marketing Cloud] en het invoeren van gegevens over marketingautomatisering. |

Voor meer informatie raadpleegt u het [overzicht van bronnen](../../sources/home.md).

