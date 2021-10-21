---
keywords: Experience Platform;huis;populaire onderwerpen;segment;Segment;creeer segment;segmentatie;creeer een segment;Segmenteringsdienst;
solution: Experience Platform
title: Een segment maken met de segmentatieservice-API
topic-legacy: tutorial
type: Tutorial
description: Volg deze zelfstudie om te leren hoe u een segmentdefinitie kunt ontwikkelen, testen, voorvertonen en opslaan met de Adobe Experience Platform Segmentation Service API.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: 8325ae6fd7d0013979e80d56eccd05b6ed6f5108
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# Creeer een segment gebruikend de Dienst API van de Segmentatie

Dit document bevat een zelfstudie voor het ontwikkelen, testen, voorvertonen en opslaan van een segmentdefinitie met behulp van de [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Voor informatie over hoe te om segmenten te bouwen gebruikend het gebruikersinterface, gelieve te zien [Handleiding Segment Builder](../ui/overview.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende [!DNL Adobe Experience Platform] de diensten betrokken bij het creëren van publiekssegmenten. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Staat u toe om publiekssegmenten van de gegevens van het Profiel van de Klant in real time te bouwen.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Platform] organiseert de gegevens van de klantenervaring. Als u de segmentatie het beste wilt gebruiken, moet u ervoor zorgen dat uw gegevens als profielen en gebeurtenissen worden opgenomen volgens de [best practices voor gegevensmodellering](../../xdm/schema/best-practices.md).

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan te maken [!DNL Platform] API&#39;s.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Een segmentdefinitie ontwikkelen

De eerste stap in segmentatie is een segment te bepalen, dat in een constructie wordt vertegenwoordigd genoemd een segmentdefinitie. Een segmentdefinitie is een object waarin een query is opgenomen [!DNL Profile Query Language] (PQL). Dit object wordt ook wel een PQL-voorspelling genoemd. PQL bepaalt de regels voor het segment die op voorwaarden met betrekking tot om het even welke verslag of tijdreeksgegevens worden gebaseerd u verstrekt aan [!DNL Real-time Customer Profile]. Zie de [PQL-hulplijn](../pql/overview.md) voor meer informatie over het schrijven van vragen PQL.

U kunt een nieuwe segmentdefinitie tot stand brengen door een verzoek van de POST aan `/segment/definitions` in de [!DNL Segmentation] API. Het volgende voorbeeld schetst hoe te om een definitieverzoek te formatteren, die welke informatie wordt vereist opdat een segment met succes wordt bepaald.

Lees voor een gedetailleerde uitleg van de manier waarop u een segment definieert de [segmentdefinitiehandleiding](../api/segment-definitions.md#create).

## Een publiek schatten en voorvertonen {#estimate-and-preview-an-audience}

Terwijl u de segmentdefinitie ontwikkelt, kunt u de schatting- en voorvertoningsgereedschappen gebruiken binnen [!DNL Real-time Customer Profile] om informatie op overzichtsniveau weer te geven om ervoor te zorgen dat u het verwachte publiek isoleert. Schattingen verschaffen statistische informatie over een segmentdefinitie, zoals de geprojecteerde publieksgrootte en het betrouwbaarheidsinterval. De voorproeven verstrekken gepagineerde lijsten van kwalificerende profielen voor een segmentdefinitie, die u toestaat om de resultaten tegen te vergelijken wat u verwacht.

Door uw publiek te schatten en te previewing, kunt u uw predikaten testen en optimaliseren PQL tot zij een wenselijk resultaat veroorzaken, waar zij dan in een bijgewerkte segmentdefinitie kunnen worden gebruikt.

Er zijn twee vereiste stappen om een voorvertoning van uw segment te bekijken of een schatting van uw segment te krijgen:

1. [Een voorbeeldtaak maken](#create-a-preview-job)
2. [Schatting of voorvertoning weergeven](#view-an-estimate-or-preview) gebruiken van identiteitskaart van de voorproefbaan

### Hoe schattingen worden gegenereerd

Gegevenssteekproeven worden gebruikt om segmenten te evalueren en het aantal kwalificerende profielen te schatten. De nieuwe gegevens worden geladen in geheugen elke ochtend (tussen 12AM-2AM PT, die 7-9AM UTC is), en alle segmenteringsvragen worden geschat gebruikend de steekproefgegevens van die dag. Dientengevolge zullen nieuwe toegevoegde velden of extra verzamelde gegevens de volgende dag in schattingen worden weerspiegeld.

De voorbeeldgrootte is afhankelijk van het totale aantal entiteiten in het profielarchief. Deze steekproefgrootte wordt vertegenwoordigd in de volgende lijst:

| Entiteiten in profielopslag | Voorbeeldformaat |
| ------------------------- | ----------- |
| Minder dan 1 miljoen | Volledige gegevensset |
| 1 tot 20 miljoen | 1 miljoen |
| Meer dan 20 miljoen | 5% van het totaal |

De schattingen lopen over het algemeen over 10-15 seconden, beginnend met een ruwe schatting en raffinage aangezien meer verslagen worden gelezen.

### Een voorbeeldtaak maken

U kunt een nieuwe voorvertoningstaak maken door een POST aan te vragen bij de `/preview` eindpunt.

Gedetailleerde instructies over het maken van een voorbeeldtaak vindt u in het gedeelte [handleiding voor voorvertoningen en schattingen van eindpunten](../api/previews-and-estimates.md#create-preview).

### Een schatting of voorvertoning weergeven

De schattings- en voorvertoningsprocessen worden asynchroon uitgevoerd, omdat verschillende query&#39;s verschillende tijdsduur kunnen duren. Nadat een query is gestart, kunt u API-aanroepen gebruiken om de huidige status van de schatting of voorvertoning tijdens het uitvoeren op te halen (GET).

Met de [!DNL Segmentation Service] API, kunt u de huidige status van een voorvertoningstaak opzoeken aan de hand van de bijbehorende id. Als de status &quot;RESULT_READY&quot; is, kunt u de resultaten bekijken. Als u de huidige status van een voorbeeldtaak wilt opzoeken, leest u de sectie op [een sectie met een voorbeeldtaak ophalen](../api/previews-and-estimates.md#get-preview) in de leidraad voor voorvertoningen en schattingen van eindpunten. Als u de huidige status van een geschatte taak wilt opzoeken, leest u de sectie over [een geschatte taak ophalen](../api/previews-and-estimates.md#get-estimate) in de leidraad voor voorvertoningen en schattingen van eindpunten.


## Volgende stappen

Nadat u de segmentdefinitie hebt ontwikkeld, getest en opgeslagen, kunt u een segmenttaak maken om een publiek te maken met de opdracht [!DNL Segmentation Service] API. Zie de zelfstudie aan [evalueren en tot segmentresultaten toegang hebben](./evaluate-a-segment.md) voor gedetailleerde stappen over hoe te om dit te verwezenlijken.
