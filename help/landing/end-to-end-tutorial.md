---
keywords: Experience Platform;thuis;populaire onderwerpen;CJA;reisanalyse;de analyse van de klantenreis;campagneorchestratie;orchestratie;klantenreis;reis;reis orchestratie;vermogen;regio
title: Adobe Experience Platform End-to-end voorbeeldworkflow
description: Leer op hoog niveau de standaard end-to-end workflow voor Adobe Experience Platform.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 0%

---

# Adobe Experience Platform end-to-end voorbeeldworkflow

Adobe Experience Platform is het krachtigste, meest flexibele en open systeem op de markt voor het ontwikkelen en beheren van volledige oplossingen die de ervaring van klanten stimuleren. Platform stelt organisaties in staat om klantgegevens en inhoud van elk systeem te centraliseren en te standaardiseren en datamateriaal en computerleren toe te passen om het ontwerp en de levering van rijke, gepersonaliseerde ervaringen drastisch te verbeteren.

Platform is gebaseerd op RESTful-API&#39;s en stelt de volledige functionaliteit van het systeem beschikbaar voor ontwikkelaars. Het ondersteunt de eenvoudige integratie van bedrijfsoplossingen met behulp van vertrouwde tools. Het platform laat u een holistische mening van uw klanten afleiden door uw klantengegevens in te voeren, uw gegevens te segmenteren aan het publiek u wilt richten, en deze publiek aan een externe bestemming te activeren. In de volgende zelfstudie wordt een end-to-end workflow getoond, waarin alle stappen worden getoond van opname via bronnen tot activering van het publiek via doelen.

![ werkschema van begin tot eind van het Experience Platform ](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## Aan de slag

Voor deze end-to-end workflow worden meerdere Adobe Experience Platform-services gebruikt. Hieronder volgt een lijst met services die in deze workflow worden gebruikt en koppelingen bevatten naar de bijbehorende overzichten:

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Platform] gegevens voor de klantervaring indeelt. Om het beste gebruik van Segmentatie te maken, gelieve te verzekeren uw gegevens als profielen en gebeurtenissen volgens de [ beste praktijken voor gegevens modellering ](../xdm/schema/best-practices.md) worden opgenomen.
- [[!DNL Identity Service]](../identity-service/home.md): biedt u een uitgebreide weergave van uw klanten en hun gedrag door identiteiten te overbruggen tussen apparaten en systemen.
- [ Bronnen ](../sources/home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
- [[!DNL Segmentation Service]](../segmentation/home.md) [!DNL Segmentation Service] : hiermee kunt u gegevens die zijn opgeslagen in [!DNL Experience Platform] en die betrekking hebben op individuen (zoals klanten, vooruitzichten, gebruikers of organisaties), opsplitsen in kleinere groepen.
- [[!DNL Real-Time Customer Profile]](../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
- [ Datasets ](../catalog/datasets/overview.md): De opslag en beheersconstructie voor gegevenspersistentie in [!DNL Experience Platform].
- [ Doelen ](../destinations/home.md): De bestemmingen zijn pre-gebouwde integratie met algemeen gebruikte toepassingen die voor de naadloze activering van gegevens van Platform voor dwars-kanaal marketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen toestaan.

## Een XDM-schema maken

Voordat u gegevens in Platform invoert, moet u eerst een XDM-schema maken om de structuur van die gegevens te beschrijven. Wanneer u uw gegevens in de volgende stap opneemt, zult u uw inkomende gegevens aan dit schema in kaart brengen. Leren hoe te om een voorbeeldXDM schema tot stand te brengen, te lezen gelieve het leerprogramma op [ creërend een schema gebruikend de Redacteur van het Schema ](../xdm/tutorials/create-schema-ui.md).

De bovenstaande zelfstudie laat zien hoe u identiteitsvelden kunt instellen voor uw schema&#39;s. Een identiteitsveld vertegenwoordigt een veld dat kan worden gebruikt om een individuele persoon te identificeren die gerelateerd is aan een record- of tijdreeksgebeurtenis. Identiteitsvelden zijn een cruciale component in de manier waarop identiteitsgrafieken van klanten worden samengesteld in Platform. Dit beïnvloedt uiteindelijk de manier waarop in realtime-klantprofiel afzonderlijke gegevensfragmenten worden samengevoegd om een volledig beeld van de klant te krijgen. Voor meer details op hoe te om identiteitsgrafieken in Platform te bekijken, zie het leerprogramma op [ hoe te om de kijker van de identiteitsgrafiek te gebruiken ](../identity-service/features/identity-graph-viewer.md).

U moet uw schema voor gebruik in het Profiel van de Klant in real time toelaten zodat de klantenprofielen van de gegevens kunnen worden geconstrueerd die op uw schema worden gebaseerd. Zie de sectie op [ toelatend een schema voor Profiel ](../xdm/ui/resources/schemas.md#profile) in de schema&#39;s UI gids voor meer informatie.

## Uw gegevens opnemen in platform

Nadat u een XDM-schema hebt gemaakt, kunt u uw gegevens in het systeem opnemen.

Alle gegevens die in Platform worden gebracht worden opgeslagen aan individuele datasets bij opname. Een dataset is een inzameling van gegevensverslagen die aan een specifiek schema XDM in kaart brengen. Voordat uw gegevens door [!DNL Real-Time Customer Profile] kunnen worden gebruikt, moet de desbetreffende gegevensset specifiek zijn geconfigureerd. Voor volledige instructies op hoe te om een dataset voor Profiel toe te laten, zie de [ gids UI van Datasets ](../catalog/datasets/user-guide.md#enable-profile) en het [ leerprogramma van de datasetconfiguratie API ](../profile/tutorials/dataset-configuration.md). Zodra de dataset is gevormd, kunt u beginnen gegevens in het op te nemen.

Het platform laat gegevens toe om van externe bronnen worden opgenomen terwijl het voorzien u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere. Bijvoorbeeld, kunt u uw gegevens opnemen door [ Amazon S3 ](../sources/tutorials/api/create/cloud-storage/s3.md) te gebruiken. Een volledige lijst van beschikbare bronnen kan in het [ overzicht van bronschakelaars ](../sources/home.md) worden gevonden.

Als u Amazon S3 als uw bronschakelaar gebruikt, kunt u de instructies in of het API leerprogramma volgen op [ het creëren van een schakelaar van Amazon S3 ](../sources/tutorials/api/create/cloud-storage/s3.md) of het leerprogramma UI op [ het creëren van een schakelaar van Amazon S3 ](../sources/tutorials/ui/create/cloud-storage/s3.md) om te leren hoe te om, met, en gegevens binnen de schakelaar tot stand te brengen te verbinden.

Voor meer gedetailleerde instructies op bronschakelaars, te lezen gelieve het [ overzicht van bronschakelaars ](../sources/home.md). Om meer over de Dienst van de Stroom te leren, API die de bronnen van zijn gebaseerd, te lezen gelieve de [ Verwijzing van de Dienst API van de Stroom ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Zodra uw gegevens in Platform door de bronschakelaar worden gebracht en in uw profiel-Toegelaten dataset worden opgeslagen, worden de klantenprofielen automatisch gecreeerd gebaseerd op de identiteitsgegevens u in uw schema XDM vormde.

Wanneer het uploaden van gegevens aan een nieuwe dataset voor het eerst, of wanneer het opzetten van een nieuw proces ETL of een gegevensbron, wordt geadviseerd om de gegevens zorgvuldig te controleren om ervoor te zorgen het correct is geupload en dat de geproduceerde profielen de gegevens bevatten u verwacht. Voor meer informatie over hoe te om tot klantenprofielen in het Platform UI toegang te hebben, zie de [ Realtime gids UI van het Profiel van de Klant ](../profile/ui/user-guide.md). Voor de details op hoe te om tot profielen toegang te hebben die Real-Time API van het Profiel van de Klant gebruiken, zie de gids op [ gebruikend het entiteitseindpunt ](../profile/api/entities.md).

## Uw gegevens evalueren

Nadat de gegenereerde profielen zijn gegenereerd op basis van de gegevens die u hebt ingevoerd, kunt u de gegevens evalueren met behulp van segmentatie. De segmentatie is het proces om specifieke attributen of gedrag te bepalen die door een ondergroep van individuen van uw opslag van het Profiel worden gedeeld, om een verhandelbare groep mensen van uw klantenbasis te onderscheiden. Om meer over segmentatie te leren, te lezen gelieve het [ overzicht van de segmentatiedienst ](../segmentation/home.md).

### Een segmentdefinitie maken

Om te beginnen, moet u een segmentdefinitie creëren om uw klanten te groeperen om uw doelpubliek tot stand te brengen. Een segmentdefinitie is een inzameling van regels die u kunt gebruiken om het publiek te bepalen u wilt richten. Om een segmentdefinitie tot stand te brengen, kunt u de instructies in of UI gids volgen bij het gebruiken van [ de Bouwer van het Segment ](../segmentation/ui/segment-builder.md) of het API leerprogramma op [ creërend een segment ](../segmentation/tutorials/create-a-segment.md).

Zodra u een segmentdefinitie hebt gecreeerd, zorg ervoor dat u nota van identiteitskaart van de segmentdefinitie houdt.

### Uw segmentdefinitie evalueren

Na het creëren van uw segmentdefinitie, kunt u of een segmentbaan tot stand brengen om het segment als éénmalige instantie te evalueren of een programma tot stand te brengen om het segment op een aan de gang zijnde basis te evalueren.

Om een segmentdefinitie op bestelling te evalueren, kunt u een segmentbaan tot stand brengen. Een segmentbaan is een asynchroon proces dat tot een nieuw publiekssegment leidt dat op de waarnaar wordt verwezen segmentdefinitie en samenvoegbeleid wordt gebaseerd. Een samenvoegingsbeleid is een reeks regels die het Platform gebruikt om te bepalen welke gegevens zullen worden gebruikt om klantenprofielen tot stand te brengen, en welke gegevens voorrang zullen krijgen wanneer er discrepanties tussen bronnen zijn. Leren hoe te met samenvoegbeleid te werken, zie de [ gids UI van het samenvoegingsbeleid ](../profile/merge-policies/ui-guide.md).

Zodra de segmentbaan wordt gecreeerd en geëvalueerd, kunt u informatie over het segment, zoals de grootte van uw publiek of fouten krijgen die tijdens verwerking kunnen zijn voorgekomen. Leren hoe te om een segmentbaan tot stand te brengen, met inbegrip van alle details u moet verstrekken, te lezen gelieve de [ gids van de de baanontwikkelaar van het segment ](../segmentation/api/segment-jobs.md).

Om een segmentdefinitie op een aan de gang zijnde basis te evalueren, kunt u een programma tot stand brengen en toelaten. Een schema is een hulpmiddel dat kan worden gebruikt om een segmentbaan eens per dag op een gespecificeerde tijd automatisch in werking te stellen. Leren om een programma tot stand te brengen en toe te laten, kunt u de instructies in de API gids op het [ planneneindpunt ](../segmentation/api/schedules.md) volgen.

## Uw geëvalueerde gegevens exporteren

Na het creëren van uw eenmalig segmentbaan of uw aan de gang zijnde programma, kunt u of een baan van de segmentuitvoer tot stand brengen om de resultaten naar een dataset uit te voeren of de resultaten naar een bestemming uit te voeren. In de volgende secties vindt u een overzicht van beide opties.

### Uw geëvalueerde gegevens exporteren naar een gegevensset

Nadat u een eenmalige segmenttaak of uw doorlopende planning hebt gemaakt, kunt u de resultaten exporteren door een segmentexporttaak te maken. Een segmentexporttaak is een asynchrone taak die informatie over het geëvalueerde publiek naar een dataset verzendt.

Voordat u een exporttaak maakt, moet u eerst een gegevensset maken waarin u de gegevens wilt exporteren. Leren hoe te om een dataset tot stand te brengen, te lezen gelieve de sectie op [ creërend een doeldataset ](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) in het leerprogramma bij het evalueren van een segment, die u nota neemt van dataset identiteitskaart na verwezenlijking. Nadat u een gegevensset hebt gemaakt, kunt u een exporttaak maken. Leren hoe te om een uitvoerbaan tot stand te brengen, kunt u de instructies in de API gids op het [ eindpunt van de de uitvoerbanen ](../segmentation/api/export-jobs.md) volgen.

### Uw geëvalueerde gegevens exporteren naar een bestemming

Alternatief, na het creëren van uw eenmalig segmentbaan of uw aan de gang zijnde programma, kunt u de resultaten naar een bestemming uitvoeren. Een bestemming is een eindpunt, zoals een toepassing van de Adobe op de externe dienst, waar een publiek kan worden geactiveerd en worden geleverd. Een volledige lijst van beschikbare bestemmingen kan in de [ catalogus van bestemmingen ](../destinations/catalog/overview.md) worden gevonden.

Voor instructies op hoe te om gegevens aan partij of e-mail marketing bestemmingen te activeren, zie het leerprogramma op [ hoe te om publieksgegevens aan de uitvoer van het partijprofiel bestemmingen te activeren gebruikend Platform UI ](../destinations/ui/activate-batch-profile-destinations.md) en de [ gids op hoe te met partijbestemmingen te verbinden en gegevens te activeren gebruikend de Dienst API van de Stroom ](../destinations/api/connect-activate-batch-destinations.md).

## De gegevensactiviteiten van uw platform controleren

Met Platform kunt u bijhouden hoe gegevens worden verwerkt met behulp van gegevensstromen. Dit zijn weergaven van taken die gegevens over de verschillende componenten van het platform verplaatsen. Deze gegevensstromen worden gevormd over de verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, waar het dan door [!DNL Identity Service] en [!DNL Real-Time Customer Profile] wordt gebruikt alvorens uiteindelijk aan bestemmingen wordt geactiveerd. Het controledashboard voorziet u van een visuele vertegenwoordiging van de reis van een gegevensstroom. Leren hoe te om dataflows binnen het Platform UI te controleren, de leerprogramma&#39;s op [ controlerende dataflows voor bronnen ](../dataflows/ui/monitor-sources.md) en [ controledataflows voor bestemmingen ](../dataflows/ui/monitor-destinations.md) zien.

U kunt de activiteiten van het Platform ook controleren door statistische metriek en gebeurtenisberichten te gebruiken door [!DNL Observability Insights] te gebruiken. U kunt zich abonneren op waarschuwingsmeldingen via de gebruikersinterface van het platform of deze verzenden naar een geconfigureerde webhaak. Voor meer details op hoe te om te bekijken, toelaten, onbruikbaar maken en aan beschikbare alarm van het Experience Platform UI intekenen, zie de [[!UICONTROL Alerts] gids UI ](../observability/alerts/ui.md). Voor details op hoe te om alarm door websites te ontvangen, zie de gids bij [ het intekenen aan de berichten van de Gebeurtenis van Adobe I/O ](../observability/alerts/subscribe.md).

## Volgende stappen

Door dit leerprogramma te lezen, hebt u een basisinleiding aan een eenvoudige stroom van begin tot eind voor Platform gekregen. Meer over Adobe Experience Platform leren, gelieve het [ overzicht van het Platform ](./home.md) te lezen. Om meer over het gebruiken van het Platform UI en het Platform API te leren, te lezen gelieve de [ gids UI van het Platform ](./ui-guide.md) en de [ gids API van het Platform ](./api-guide.md) respectievelijk.
