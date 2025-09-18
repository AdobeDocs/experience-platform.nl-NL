---
solution: Experience Platform
title: Een segmentdefinitie maken met de segmentatieservice-API
type: Tutorial
description: Volg deze zelfstudie om te leren hoe u een segmentdefinitie kunt ontwikkelen, testen, voorvertonen en opslaan met de Adobe Experience Platform Segmentation Service API.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: a374d261e3b34b30869f1a9e8486d52f5bd658cb
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 0%

---

# Creeer een segmentdefinitie gebruikend de Dienst API van de Segmentatie

Dit document biedt een zelfstudie voor het ontwikkelen, testen, voorvertonen en opslaan van een segmentdefinitie met de [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md) .

Voor informatie over hoe te om segmentdefinities te bouwen gebruikend het gebruikersinterface, gelieve de [ gids van de Bouwer van het Segment ](../ui/segment-builder.md) te zien.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende [!DNL Adobe Experience Platform] -services die betrokken zijn bij het maken van segmentdefinities. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Staat u toe om publiek te bouwen gebruikend segmentdefinities of andere externe bronnen van gegevens van het Profiel van de Klant in real time.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt. Om het beste gebruik van Segmentatie te maken, gelieve te verzekeren uw gegevens als profielen en gebeurtenissen volgens de [ beste praktijken voor gegevens modellering ](../../xdm/schema/best-practices.md) worden opgenomen.

De volgende secties bevatten aanvullende informatie die u moet weten om aanroepen naar de API&#39;s van [!DNL Experience Platform] te kunnen uitvoeren.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Experience Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Een segmentdefinitie ontwikkelen

De eerste stap in segmentatie is een segmentdefinitie te bepalen. Een segmentdefinitie is een object dat een query omvat die is geschreven in [!DNL Profile Query Language] (PQL). Dit object wordt ook wel een PQL-voorspelling genoemd. PQL voorspelt de regels voor de segmentdefinitie op basis van voorwaarden die gerelateerd zijn aan record- of tijdreeksgegevens die u aan [!DNL Real-Time Customer Profile] opgeeft. Zie de [ gids van PQL ](../pql/overview.md) voor meer informatie bij het schrijven van de vragen van PQL.

U kunt een nieuwe segmentdefinitie maken door een POST-aanvraag in te dienen bij het eindpunt `/segment/definitions` in de [!DNL Segmentation] API. Het volgende voorbeeld schetst hoe te om een definitieverzoek te formatteren, die welke informatie wordt vereist opdat een segmentdefinitie met succes wordt bepaald.

Voor een gedetailleerde verklaring op hoe te om een segmentdefinitie te bepalen, te lezen gelieve de [ gids van de de ontwikkelaar van de segmentdefinitie ](../api/segment-definitions.md#create).

## Een publiek schatten en voorvertonen {#estimate-and-preview-an-audience}

Terwijl u de segmentdefinitie ontwikkelt, kunt u de schatting- en voorvertoningsgereedschappen in [!DNL Real-Time Customer Profile] gebruiken om informatie op overzichtsniveau weer te geven, zodat u zeker weet dat u het verwachte publiek isoleert. Schattingen verschaffen statistische informatie over een segmentdefinitie, zoals de geprojecteerde publieksgrootte en het betrouwbaarheidsinterval. De voorproeven verstrekken gepagineerde lijsten van kwalificerende profielen voor een segmentdefinitie, die u toestaat om de resultaten tegen te vergelijken wat u verwacht.

Door een schatting en voorvertoning van uw publiek te maken, kunt u uw PQL-voorspellingen testen en optimaliseren totdat ze een gewenste uitkomst opleveren. Vervolgens kunt u deze gebruiken in een bijgewerkte segmentdefinitie.

Er zijn twee vereiste stappen om een voorvertoning van uw segmentdefinitie weer te geven of een schatting van uw segmentdefinitie te krijgen:

1. [Een voorbeeldtaak maken](#create-a-preview-job)
2. [ de schatting of voorproef van de Mening ](#view-an-estimate-or-preview) gebruikend identiteitskaart van de voorproefbaan

### Hoe schattingen worden gegenereerd

Aangezien gegevens die voor het Profiel van de Klant in real time worden toegelaten in Experience Platform worden opgenomen, wordt het opgeslagen binnen de gegevensopslag van het Profiel. Wanneer de opname van records in het archief Profiel het totale aantal profielen met meer dan 3% verhoogt of verlaagt, wordt een samplingtaak geactiveerd om het aantal bij te werken. Als het aantal profielen niet met meer dan 3% verandert, wordt de samplingtaak automatisch wekelijks uitgevoerd.

De wijze waarop het monster wordt geactiveerd, hangt af van het type inname dat wordt gebruikt:

- Voor het stromen gegevenswerkschema&#39;s, wordt een controle uitgevoerd op uurbasis om te bepalen als de 3% verhoging of dalingsdrempel is voldaan. Als aan deze drempel is voldaan, wordt automatisch een voorbeeldtaak geactiveerd om de telling bij te werken.
- Voor batch-opname wordt binnen 15 minuten na het correct innemen van een batch in de profielopslag een taak uitgevoerd om het aantal bij te werken als aan de drempel voor 3% verhoging of verlaging is voldaan. Met behulp van de profiel-API kunt u een voorvertoning weergeven van de meest recente voorbeeldtaak en de distributie van het lijstprofiel via gegevensset en naamruimte op naam.

De voorbeeldgrootte is afhankelijk van het totale aantal entiteiten in de profielopslag. Deze steekproefgrootte wordt vertegenwoordigd in de volgende lijst:

| Entiteiten in de profielopslag | Voorbeeldformaat |
| ------------------------- | ----------- |
| Minder dan 1 miljoen | Volledige gegevensset |
| 1 tot 20 miljoen | 1 miljoen |
| Meer dan 20 miljoen | 5% van het totaal |

De schattingen lopen over het algemeen over 10-15 seconden, beginnend met een ruwe schatting en raffinage aangezien meer verslagen worden gelezen.

### Een voorbeeldtaak maken

U kunt een nieuwe voorvertoningstaak maken door een POST-aanvraag in te dienen bij het eindpunt van `/preview` .

De gedetailleerde instructies bij het creëren van een voorproefbaan kunnen in de [ voorproeven en de gids van ramingen eindpunten ](../api/previews-and-estimates.md#create-preview) worden gevonden.

### Een schatting of voorvertoning weergeven

De schattings- en voorvertoningsprocessen worden asynchroon uitgevoerd, omdat verschillende query&#39;s verschillende tijdsduur kunnen duren. Zodra een vraag is in werking gesteld, kunt u API vraag gebruiken om (GET) de huidige staat van de raming terug te winnen of voorproef aangezien het vordert.

Met de API [!DNL Segmentation Service] kunt u de huidige status van een voorbeeldtaak opzoeken aan de hand van de id. Als de status &quot;RESULT_READY&quot; is, kunt u de resultaten bekijken. Om omhoog de huidige staat van een voorproefbaan te kijken, te lezen gelieve de sectie op [ het terugwinnen van een sectie van de voorproefbaan ](../api/previews-and-estimates.md#get-preview) in de voorproeven en de gids van ramingen eindpunten. Om omhoog de huidige staat van een geschatte baan te kijken, te lezen gelieve de sectie over [ het terugwinnen van een geschatte baan ](../api/previews-and-estimates.md#get-estimate) in de voorproeven en de gids van schattingen eindpunten.


## Volgende stappen

Nadat u de segmentdefinitie hebt ontwikkeld, getest en opgeslagen, kunt u een segmenttaak maken om een publiek op te bouwen met de API [!DNL Segmentation Service] . Zie het leerprogramma op [ beoordelend en tot segmentresultaten ](./evaluate-a-segment.md) voor gedetailleerde stappen op hoe te om dit te verwezenlijken.
