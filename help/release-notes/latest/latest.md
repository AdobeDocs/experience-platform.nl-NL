---
title: 'Aanvullende informatie van januari 2026 voor Adobe Experience Platform '
description: Aanvullende informatie van januari 2026 voor Adobe Experience Platform.
source-git-commit: 905c8853fadc08bb7e357f43f358844b560b3097
workflow-type: tm+mt
source-wordcount: '1529'
ht-degree: 18%

---


# Aanvullende informatie voor Adobe Experience Platform

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/nl/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/nl/docs/journey-optimizer-b2b/user/release-notes)
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
| Gebruiksgebonden proefversie van Adobe Experience Platform Agents | **Uitgezochte klanten hebben nu een gratis proeftoegang tot de Agenten van Adobe Experience Platform**. U kunt de proef gebruiken om met Agenten door de AI Hulp interface te onderzoeken en in wisselwerking te staan die door Adobe Experience Platform Agent Orchestrator wordt aangedreven. De proef biedt hands-on ervaring met AI Agenten die binnen de context van de bestaande producten en milieu&#39;s van Experience Cloud van klanten werken, die teams toestaan om waarde te evalueren alvorens aan een volledige aankoop te verbinden. Adobe Experience Platform Agents worden begeleid door gebruikersinvoer en -toezicht en respecteren bestaande toegangscontroles op productniveau, zodat gebruikers alleen handelingen kunnen uitvoeren of gegevens kunnen bekijken waarvoor ze zijn geautoriseerd in de onderliggende Experience Cloud-toepassingen. Lees het [&#x200B; gebruik-gebonden proefoverzicht van de Agenten van Experience Platform &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/agents/trial) voor informatie over hoe te begonnen worden. |

{style="table-layout:auto"}

Voor meer informatie, zie de [&#x200B; documentatie van Agent Orchestrator &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms waarmee gegevens uit Experience Platform naadloos kunnen worden geactiveerd. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [&#x200B; Kevel bestemmings &#x200B;](/help/destinations/catalog/advertising/kevel.md) schakelaar nu beschikbaar | Met de [!DNL Kevel] streamingbestemming voor Adobe Experience Platform kunnen klanten Adobe-doelgroepen rechtstreeks activeren in de gebruikersdatabase- en segmentbeheerAPI&#39;s van [!DNL Kevel] voor ondersteuning van realtime doelwitten tijdens de besluitvorming. [[!DNL Kevel] &#x200B;](https://www.kevel.com/) verstrekt de AI-Toegelaten technologie en deskundige begeleiding die innovatieve handelsleiders helpen lanceren, schrapen, en slagen in handelsmedia. De Retail Media Cloud-bevoegdheden van [!DNL Kevel] zijn gericht op, aanpasbare en aanpasbare advertentievormen voor on-site en off-site reclame. |
| [&#x200B; nu beschikbare schakelaar van de bestemmingsUitwisseling van de 0&rbrace; Index](/help/destinations/catalog/advertising/index-exchange.md) | Gebruik deze bestemmingsschakelaar om publiekssegmenten van Adobe Experience Platform rechtstreeks naar het programmatic reclameplatform van [!DNL Index Exchange] uit te voeren. [!DNL Index] is een wereldwijd advertentieplatform dat media-eigenaars helpt de waarde van hun inhoud op elk scherm te maximaliseren. Met meer dan 20 jaar toonaangevend in de branche verbindt [!DNL Index] de grootste merken ter wereld met toonaangevende ervaren makers om hoogwaardige consumentenervaringen te bieden. |
| Regionale steun voor eindpunten voor verbindingen van het type Braze | Alle [&#x200B; gebied-specifieke eindpunten &#x200B;](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) die door [!DNL Braze] worden gesteund zijn nu beschikbaar voor selectie tijdens de stroom van de bestemmingsconfiguratie. Vraag uw [!DNL Braze] vertegenwoordiger welke eindpuntinstantie u zou moeten gebruiken. |
| Wekelijks en maandelijkse het plannen steun voor [&#x200B; Liveramp Onboarding &#x200B;](../../destinations/catalog/advertising/liveramp-onboarding.md#scheduling) | U kunt nu wekelijkse en maandelijkse exportschema&#39;s configureren voor de bestemming Liveramp aan boord. <br> Deze release wordt geleidelijk uitgevoerd en is op 30 januari voltooid. |
| Verbeterde activeringservaring voor [&#x200B; de Commerciële Desk &#x200B;](../../destinations/catalog/advertising/tradedesk.md) en [&#x200B; Microsoft Bing &#x200B;](../../destinations/catalog/advertising/bing.md) bestemmingen | De handelsbureau en de bestemmingen van de Bing van Microsoft omvatten nu vooraf bepaalde verplichte afbeeldingen voor een geoptimaliseerde activeringservaring.  <br> Deze release wordt geleidelijk uitgevoerd en is op 30 januari voltooid. ![&#x200B; Beeld die vooraf bepaalde afbeeldingen voor de Handelsplaats tonen &#x200B;](../2026/assets/january/mandatory-mappings-ttd.png) {width="150" align="center" zoomable="yes"} <br> ![&#x200B; Beeld die vooraf bepaalde afbeeldingen voor het Bing van Microsoft tonen &#x200B;](../2026/assets/january/mandatory-mappings-bing.png) {width="150" align="center" zoomable="yes"} |
| AES256 encryptiesteun voor [&#x200B; Amazon S3 &#x200B;](../../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) bestemmingen | U kunt nu AES256-codering configureren voor uw Amazon S3-export. Er zijn twee opties beschikbaar: <ul><li>**[!UICONTROL Default]**: gegevens worden in rust gecodeerd met het standaardversleutelingsalgoritme dat op uw emmertje is ingesteld.</li><li>**[!UICONTROL SSE-S3/AES256]**: Experience Platform voegt de `s3:x-amz-server-side-encryption": "AES256` -header in de export toe en gegevens worden in rust gecodeerd met het AES256-algoritme wanneer het land in S3 ligt. **Deze optie neemt belangrijkheid over om het even welk standaard encryptiealgoritme dat op uw S3 emmertje** wordt gevormd.</li></ul> Deze release wordt geleidelijk ingevoerd en zal op 30 januari zijn voltooid. |
| De steun van de activering van het aantal van de telefoon voor [&#x200B; de Trade Desk - CRM &#x200B;](../../destinations/catalog/advertising/tradedesk-emails.md#phone-hashing) verbinding | De plaats van de Handel - bestemming CRM steunt nu telefoonnummeractivering naast e-mailadressen. U kunt zowel unhashed telefoonaantallen in formaat E.164 als gehakt telefoonaantallen (formaat SHA256_E.164) aan uw rekening van het Bureau van de Handel voor publiek activeren richtend en onderdrukking die op de gegevens van CRM wordt gebaseerd. Telefoonnummers moeten worden genormaliseerd naar E.164-indeling voordat ze kunnen worden geactiveerd. |
| [&#x200B; bestemmingsupdates van de Partij van 0&rbrace; Snowflake &lbrace;](../../destinations/catalog/warehouses/snowflake-batch.md) | De Snowflake Batch-bestemming bevat nu mogelijkheden voor het selecteren van gebieden tijdens de doelconfiguratie. U kunt nu de specifieke Snowflake-regio selecteren waar uw exemplaar is ingericht, zodat u verzekerd bent van optimale gegevensoverdracht en de regionale vereisten kunt naleven. Bovendien, is de standaardbeperking van het fusiebeleid verwijderd, toestaand u om publiek uit te voeren dat aan om het even welk fusiebeleid in kaart wordt gebracht. <br> De batchbestemming [!DNL Snowflake] is momenteel alleen beschikbaar voor Real-Time CDP-klanten die zijn ingericht in het Experience Platform VA7-gebied. |

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

