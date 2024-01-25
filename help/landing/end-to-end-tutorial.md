---
keywords: Experience Platform;thuis;populaire onderwerpen;CJA;reisanalyse;de analyse van de klantenreis;campagneorchestratie;orchestratie;klantenreis;reis;reis orchestratie;vermogen;regio
title: Adobe Experience Platform End-to-end voorbeeldworkflow
description: Leer op hoog niveau de standaard end-to-end workflow voor Adobe Experience Platform.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: f9917d6a6de81f98b472cff9b41f1526ea51cdae
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 0%

---

# Adobe Experience Platform end-to-end voorbeeldworkflow

Adobe Experience Platform is het krachtigste, meest flexibele en open systeem op de markt voor het ontwikkelen en beheren van volledige oplossingen die de ervaring van klanten stimuleren. Platform stelt organisaties in staat om klantgegevens en inhoud van elk systeem te centraliseren en te standaardiseren en datamateriaal en computerleren toe te passen om het ontwerp en de levering van rijke, gepersonaliseerde ervaringen drastisch te verbeteren.

Platform is gebaseerd op RESTful-API&#39;s en stelt de volledige functionaliteit van het systeem beschikbaar voor ontwikkelaars. Het ondersteunt de eenvoudige integratie van bedrijfsoplossingen met behulp van vertrouwde tools. Het platform laat u een holistische mening van uw klanten afleiden door uw klantengegevens in te voeren, uw gegevens te segmenteren aan het publiek u wilt richten, en deze publiek aan een externe bestemming te activeren. In de volgende zelfstudie wordt een end-to-end workflow getoond, waarin alle stappen worden getoond van opname via bronnen tot activering van het publiek via doelen.

![end-to-end workflow voor Experience Platforms](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## Aan de slag

Voor deze end-to-end workflow worden meerdere Adobe Experience Platform-services gebruikt. Hieronder volgt een lijst met services die in deze workflow worden gebruikt en koppelingen bevatten naar de bijbehorende overzichten:

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Platform] organiseert de gegevens van de klantenervaring. Als u de segmentatie het beste wilt gebruiken, moet u ervoor zorgen dat uw gegevens als profielen en gebeurtenissen worden opgenomen volgens de [best practices voor gegevensmodellering](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md): Biedt u een uitgebreide weergave van uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
- [Bronnen](../sources/home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service] staat u toe om gegevens te verdelen die in worden opgeslagen [!DNL Experience Platform] dat betrekking heeft op individuen (zoals klanten, vooruitzichten, gebruikers, of organisaties) in kleinere groepen.
- [[!DNL Real-Time Customer Profile]](../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
- [Gegevenssets](../catalog/datasets/overview.md): De opslag- en beheerconstructie voor gegevenspersistentie in [!DNL Experience Platform].
- [Doelen](../destinations/home.md): De bestemmingen zijn pre-gebouwde integratie met algemeen gebruikte toepassingen die voor de naadloze activering van gegevens van Platform voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen toestaan.

## Een XDM-schema maken

Voordat u gegevens in Platform invoert, moet u eerst een XDM-schema maken om de structuur van die gegevens te beschrijven. Wanneer u uw gegevens in de volgende stap opneemt, zult u uw inkomende gegevens aan dit schema in kaart brengen. Lees de zelfstudie voor meer informatie over het maken van een voorbeeld-XDM-schema [een schema maken met de Schema-editor](../xdm/tutorials/create-schema-ui.md).

De bovenstaande zelfstudie laat zien hoe u identiteitsvelden kunt instellen voor uw schema&#39;s. Een identiteitsveld vertegenwoordigt een veld dat kan worden gebruikt om een individuele persoon te identificeren die gerelateerd is aan een record- of tijdreeksgebeurtenis. Identiteitsvelden zijn een cruciale component in de manier waarop identiteitsgrafieken van klanten worden samengesteld in Platform. Dit beïnvloedt uiteindelijk de manier waarop in realtime-klantprofiel afzonderlijke gegevensfragmenten worden samengevoegd om een volledig beeld van de klant te krijgen. Raadpleeg de zelfstudie voor meer informatie over het weergeven van identiteitsgrafieken in Platform. [gebruiken van de viewer voor identiteitsgrafieken](../identity-service/features/identity-graph-viewer.md).

U moet uw schema voor gebruik in het Profiel van de Klant in real time toelaten zodat de klantenprofielen van de gegevens kunnen worden geconstrueerd die op uw schema worden gebaseerd. Zie de sectie over [een schema inschakelen voor profiel](../xdm/ui/resources/schemas.md#profile) in de gids van schema&#39;s UI voor meer informatie.

## Uw gegevens opnemen in platform

Nadat u een XDM-schema hebt gemaakt, kunt u uw gegevens in het systeem opnemen.

Alle gegevens die in Platform worden gebracht worden opgeslagen aan individuele datasets bij opname. Een dataset is een inzameling van gegevensverslagen die aan een specifiek schema XDM in kaart brengen. Voordat uw gegevens kunnen worden gebruikt door [!DNL Real-Time Customer Profile], moet de betrokken gegevensset specifiek worden geconfigureerd. Voor volledige instructies over hoe te om een dataset voor Profiel toe te laten, zie [UI-gids voor gegevensbestanden](../catalog/datasets/user-guide.md#enable-profile) en de [API-zelfstudie voor gegevenssetconfiguratie](../profile/tutorials/dataset-configuration.md). Zodra de dataset is gevormd, kunt u beginnen gegevens in het op te nemen.

Het platform laat gegevens toe om van externe bronnen worden opgenomen terwijl het voorzien u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere. U kunt bijvoorbeeld uw gegevens invoeren met [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). Een volledige lijst van beschikbare bronnen is te vinden in de [overzicht van bronconnectors](../sources/home.md).

Als u Amazon S3 als bronaansluiting gebruikt, kunt u de instructies in de API-zelfstudie volgen op [een Amazon S3-connector maken](../sources/tutorials/api/create/cloud-storage/s3.md) of de UI-zelfstudie ingeschakeld [een Amazon S3-connector maken](../sources/tutorials/ui/create/cloud-storage/s3.md) om te leren om tot stand te brengen, met, en gegevens binnen de schakelaar aan te sluiten.

Voor meer gedetailleerde instructies op bronschakelaars, gelieve te lezen [overzicht van bronconnectors](../sources/home.md). Lees voor meer informatie over Flow Service, de API waarvan bronnen zijn gebaseerd op [Referentie voor de Flow Service API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Zodra uw gegevens in Platform door de bronschakelaar worden gebracht en in uw profiel-Toegelaten dataset worden opgeslagen, worden de klantenprofielen automatisch gecreeerd gebaseerd op de identiteitsgegevens u in uw schema XDM vormde.

Wanneer het uploaden van gegevens aan een nieuwe dataset voor het eerst, of wanneer het opzetten van een nieuw proces ETL of een gegevensbron, wordt geadviseerd om de gegevens zorgvuldig te controleren om ervoor te zorgen het correct is geupload en dat de geproduceerde profielen de gegevens bevatten u verwacht. Voor meer informatie over hoe te om tot klantenprofielen in Platform UI toegang te hebben, zie [Gebruikershandleiding voor realtime gebruikersprofiel van klanten](../profile/ui/user-guide.md). Raadpleeg de handleiding voor meer informatie over het gebruik van de Real-Time Customer Profile API voor toegang tot profielen [het gebruiken van het entiteitseindpunt](../profile/api/entities.md).

## Uw gegevens evalueren

Nadat de gegenereerde profielen zijn gegenereerd op basis van de gegevens die u hebt ingevoerd, kunt u de gegevens evalueren met behulp van segmentatie. De segmentatie is het proces om specifieke attributen of gedrag te bepalen die door een ondergroep van individuen van uw profielopslag worden gedeeld, om een verhandelbare groep mensen van uw klantenbasis te onderscheiden. Voor meer informatie over segmentatie leest u de [overzicht van segmentatieservice](../segmentation/home.md).

### Een segmentdefinitie maken

Om te beginnen, moet u een segmentdefinitie creëren om uw klanten te groeperen om uw doelpubliek tot stand te brengen. Een segmentdefinitie is een inzameling van regels die u kunt gebruiken om het publiek te bepalen u wilt richten. Om een segmentdefinitie tot stand te brengen, kunt u de instructies in of UI gids volgen bij het gebruiken van [Segment Builder](../segmentation/ui/segment-builder.md) of de API-zelfstudie aan [een segment maken](../segmentation/tutorials/create-a-segment.md).

Zodra u een segmentdefinitie hebt gecreeerd, zorg ervoor dat u nota van identiteitskaart van de segmentdefinitie houdt.

### Uw segmentdefinitie evalueren

Na het creëren van uw segmentdefinitie, kunt u of een segmentbaan tot stand brengen om het segment als éénmalige instantie te evalueren of een programma tot stand te brengen om het segment op een aan de gang zijnde basis te evalueren.

Om een segmentdefinitie op bestelling te evalueren, kunt u een segmentbaan tot stand brengen. Een segmentbaan is een asynchroon proces dat tot een nieuw publiekssegment leidt dat op de waarnaar wordt verwezen segmentdefinitie en samenvoegbeleid wordt gebaseerd. Een samenvoegingsbeleid is een reeks regels die het Platform gebruikt om te bepalen welke gegevens zullen worden gebruikt om klantenprofielen tot stand te brengen, en welke gegevens voorrang zullen krijgen wanneer er discrepanties tussen bronnen zijn. Als u wilt leren werken met samenvoegingsbeleid, raadpleegt u de [UI-hulplijn voor samenvoegbeleid](../profile/merge-policies/ui-guide.md).

Zodra de segmentbaan wordt gecreeerd en geëvalueerd, kunt u informatie over het segment, zoals de grootte van uw publiek of fouten krijgen die tijdens verwerking kunnen zijn voorgekomen. Als u wilt leren hoe u een segmenttaak maakt, inclusief alle details die u moet opgeven, leest u de [segmenttaakontwikkelaarshandleiding](../segmentation/api/segment-jobs.md).

Om een segmentdefinitie op een aan de gang zijnde basis te evalueren, kunt u een programma tot stand brengen en toelaten. Een schema is een hulpmiddel dat kan worden gebruikt om een segmentbaan eens per dag op een gespecificeerde tijd automatisch in werking te stellen. Als u wilt leren hoe u een schema kunt maken en inschakelen, volgt u de instructies in de API-handleiding op het tabblad [planningeindpunt](../segmentation/api/schedules.md).

## Uw geëvalueerde gegevens exporteren

Na het creëren van uw eenmalig segmentbaan of uw aan de gang zijnde programma, kunt u of een baan van de segmentuitvoer tot stand brengen om de resultaten naar een dataset uit te voeren of de resultaten naar een bestemming uit te voeren. In de volgende secties vindt u een overzicht van beide opties.

### Uw geëvalueerde gegevens exporteren naar een gegevensset

Nadat u een eenmalige segmenttaak of uw doorlopende planning hebt gemaakt, kunt u de resultaten exporteren door een segmentexporttaak te maken. Een segmentexporttaak is een asynchrone taak die informatie over het geëvalueerde publiek naar een dataset verzendt.

Voordat u een exporttaak maakt, moet u eerst een gegevensset maken waarin u de gegevens wilt exporteren. Om te leren hoe te om een dataset tot stand te brengen, te lezen gelieve de sectie over [het creëren van een doeldataset](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) in de zelfstudie over het evalueren van een segment, waarbij u zorgt dat u na het maken een notitie maakt van de id van de gegevensset. Nadat u een gegevensset hebt gemaakt, kunt u een exporttaak maken. Als u wilt leren hoe u een exporttaak maakt, volgt u de instructies in de API-handleiding op het tabblad [eindpunt exporttaken](../segmentation/api/export-jobs.md).

### Uw geëvalueerde gegevens exporteren naar een bestemming

Alternatief, na het creëren van uw eenmalig segmentbaan of uw aan de gang zijnde programma, kunt u de resultaten naar een bestemming uitvoeren. Een bestemming is een eindpunt, zoals een toepassing van de Adobe op de externe dienst, waar een publiek kan worden geactiveerd en worden geleverd. Een volledige lijst van beschikbare bestemmingen is te vinden in [doelcatalogus](../destinations/catalog/overview.md).

Voor instructies over hoe te om gegevens aan partij of e-mail marketing bestemmingen te activeren, zie de zelfstudie op [hoe te om publieksgegevens aan de bestemmingen van de de uitvoer van het partijprofiel te activeren gebruikend Platform UI](../destinations/ui/activate-batch-profile-destinations.md) en de [handleiding voor het maken van verbinding met batchbestemmingen en het activeren van gegevens met behulp van de Flow Service API](../destinations/api/connect-activate-batch-destinations.md).

## De gegevensactiviteiten van uw platform controleren

Met Platform kunt u bijhouden hoe gegevens worden verwerkt met behulp van gegevensstromen. Dit zijn weergaven van taken die gegevens over de verschillende componenten van het platform verplaatsen. Deze dataflows worden gevormd over de verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, waar het dan door wordt gebruikt [!DNL Identity Service] en [!DNL Real-Time Customer Profile] alvorens uiteindelijk aan bestemmingen worden geactiveerd. Het controledashboard voorziet u van een visuele vertegenwoordiging van de reis van een gegevensstroom. Leer hoe te om gegevensstromen binnen UI van het Platform te controleren, zie de leerprogramma&#39;s op [gegevensstromen controleren voor bronnen](../dataflows/ui/monitor-sources.md) en [dataflow voor bestemmingen controleren](../dataflows/ui/monitor-destinations.md).

U kunt de activiteiten van het Platform door het gebruik van statistische metriek en gebeurtenisberichten ook controleren door te gebruiken [!DNL Observability Insights]. U kunt zich abonneren op waarschuwingsmeldingen via de gebruikersinterface van het platform of deze verzenden naar een geconfigureerde webhaak. Voor meer informatie over het bekijken, toelaten, onbruikbaar maken, en intekenen aan beschikbare alarm van het Experience Platform UI, zie [[!UICONTROL Alerts] UI-hulplijn](../observability/alerts/ui.md). Zie de handleiding voor meer informatie over het ontvangen van waarschuwingen via websites [abonneren op Adobe I/O Event-berichten](../observability/alerts/subscribe.md).

## Volgende stappen

Door dit leerprogramma te lezen, hebt u een basisinleiding aan een eenvoudige stroom van begin tot eind voor Platform gekregen. Lees voor meer informatie over Adobe Experience Platform de [Overzicht van platform](./home.md). Voor meer informatie over het gebruik van de platforminterface en de platform-API leest u de [Handleiding voor platforminterface](./ui-guide.md) en de [Platform API-handleiding](./api-guide.md) respectievelijk.
