---
keywords: Experience Platform;huis;populaire onderwerpen;segment;Segment;creeer segment;segmentatie;creeer een segment;Segmenteringsdienst;
solution: Experience Platform
title: Een segment maken
topic: tutorial
type: Tutorial
description: Dit document biedt een zelfstudie voor het ontwikkelen, testen, voorvertonen en opslaan van een segmentdefinitie met de Adobe Experience Platform Segmentation Service API.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---


# Een segment maken

Dit document biedt een zelfstudie voor het ontwikkelen, testen, voorvertonen en opslaan van een segmentdefinitie met de [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Voor informatie over hoe te om segmenten te bouwen gebruikend het gebruikersinterface, te zien gelieve [de gids van de Bouwer van het Segment](../ui/overview.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende [!DNL Adobe Experience Platform] services die betrokken zijn bij het maken van publiekssegmenten. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Staat u toe om publiekssegmenten van de gegevens van het Profiel van de Klant in real time te bouwen.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Platform] klantenervaring worden georganiseerd.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan [!DNL Platform] APIs te maken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie [sandbox-overzicht](../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Een segmentdefinitie ontwikkelen

De eerste stap in segmentatie is een segment te bepalen, dat in een constructie wordt vertegenwoordigd genoemd een segmentdefinitie. Een segmentdefinitie is een voorwerp dat een vraag inkapselt die in [!DNL Profile Query Language] (PQL) wordt geschreven. Dit object wordt ook wel een PQL-voorspelling genoemd. In PQL worden de regels voor het segment gedefinieerd op basis van voorwaarden die gerelateerd zijn aan record- of tijdreeksgegevens die u verschaft aan [!DNL Real-time Customer Profile]. Zie [PQL gids](../pql/overview.md) voor meer informatie bij het schrijven van vragen PQL.

U kunt een nieuwe segmentdefinitie tot stand brengen door een verzoek van de POST aan het `/segment/definitions` eindpunt in [!DNL Segmentation] API te doen. Het volgende voorbeeld schetst hoe te om een definitieverzoek te formatteren, die welke informatie wordt vereist opdat een segment met succes wordt bepaald.

Lees voor een gedetailleerde uitleg van het definiëren van een segment de [segmentdefinitiehandleiding](../api/segment-definitions.md#create).

## Een publiek schatten en voorvertonen {#estimate-and-preview-an-audience}

Terwijl u de segmentdefinitie ontwikkelt, kunt u de schatting- en voorvertoningsgereedschappen in [!DNL Real-time Customer Profile] gebruiken om informatie op overzichtsniveau weer te geven, zodat u zeker weet dat u het verwachte publiek isoleert. Schattingen verschaffen statistische informatie over een segmentdefinitie, zoals de geprojecteerde publieksgrootte en het betrouwbaarheidsinterval. De voorproeven verstrekken gepagineerde lijsten van kwalificerende profielen voor een segmentdefinitie, die u toestaat om de resultaten tegen te vergelijken wat u verwacht.

Door uw publiek te schatten en te previewing, kunt u uw predikaten testen en optimaliseren PQL tot zij een wenselijk resultaat veroorzaken, waar zij dan in een bijgewerkte segmentdefinitie kunnen worden gebruikt.

Er zijn twee vereiste stappen om een voorvertoning van uw segment te bekijken of een schatting van uw segment te krijgen:

1. [Een voorbeeldtaak maken](#create-a-preview-job)
2. [Schatting of ](#view-an-estimate-or-preview) voorvertoning weergeven met de id van de voorvertoningstaak

### Hoe schattingen worden gegenereerd

Gegevenssteekproeven worden gebruikt om segmenten te evalueren en het aantal kwalificerende profielen te schatten. De nieuwe gegevens worden geladen in geheugen elke ochtend (tussen 12AM-2AM PT, die 7-9AM UTC is), en alle segmenteringsvragen worden geschat gebruikend de steekproefgegevens van die dag. Bijgevolg zullen nieuwe toegevoegde velden of verzamelde aanvullende gegevens de volgende dag in schattingen worden weergegeven.

De voorbeeldgrootte is afhankelijk van het totale aantal entiteiten in het profielarchief. Deze steekproefgrootte wordt vertegenwoordigd in de volgende lijst:

| Entiteiten in profielopslag | Voorbeeldformaat |
| ------------------------- | ----------- |
| Minder dan 1 miljoen | Volledige gegevensset |
| 1 tot 20 miljoen | 1 miljoen |
| Meer dan 20 miljoen | 5% van het totaal |

De schattingen lopen over het algemeen over 10-15 seconden, beginnend met een ruwe schatting en raffinage aangezien meer verslagen worden gelezen.

### Een voorbeeldtaak maken

U kunt een nieuwe voorproefbaan tot stand brengen door een verzoek van de POST aan het `/preview` eindpunt te doen.

Gedetailleerde instructies over het maken van een voorbeeldtaak vindt u in de [handleiding voor voorvertoningen en schattingen van eindpunten](../api/previews-and-estimates.md#create-preview).

### Een schatting of voorvertoning weergeven

De schattings- en voorvertoningsprocessen worden asynchroon uitgevoerd, omdat verschillende query&#39;s verschillende tijdsduur kunnen duren. Nadat een query is gestart, kunt u API-aanroepen gebruiken om de huidige status van de schatting of voorvertoning tijdens het uitvoeren op te halen (GET).

Met de API [!DNL Segmentation Service] kunt u de huidige status van een voorvertoningstaak opzoeken aan de hand van de id. Als de status &quot;RESULT_READY&quot; is, kunt u de resultaten bekijken. Als u de huidige status van een voorvertoningstaak wilt opzoeken, leest u de sectie over [het ophalen van een voorbeeldtaaksectie](../api/previews-and-estimates.md#get-preview) in de handleiding voor voorvertoningen en geschatte eindpunten. Als u de huidige status van een geschatte taak wilt opzoeken, leest u de sectie over [het ophalen van een geschatte taak](../api/previews-and-estimates.md#get-estimate) in de handleiding voor voorvertoningen en geschatte eindpunten.


## Volgende stappen

Nadat u de segmentdefinitie hebt ontwikkeld, getest en opgeslagen, kunt u een segmenttaak maken om een publiek op te bouwen met de API [!DNL Segmentation Service]. Zie de zelfstudie op [het evalueren van en het toegang tot van segmentresultaten](./evaluate-a-segment.md) voor gedetailleerde stappen op hoe te om dit te verwezenlijken.