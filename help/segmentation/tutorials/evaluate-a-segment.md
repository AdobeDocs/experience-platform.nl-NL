---
keywords: Experience Platform;huis;populaire onderwerpen;segmentbeoordeling;Segmenteringsdienst;segmentatie;segmentatie;evalueer een segment;toegangssegmentresultaten;evalueer en toegangssegment;
solution: Experience Platform
title: Evalueer en de Resultaten van het Segment van de Toegang
topic: tutorial
type: Tutorial
description: Volg deze zelfstudie om te leren hoe u segmenten en toegangssegmentresultaten kunt evalueren met de Adobe Experience Platform Segmentation Service API.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
translation-type: tm+mt
source-git-commit: 87729e4996b0b2ac26e1a0abaa80af717825f9e6
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# Evalueer en open segmentresultaten

Dit document biedt een zelfstudie voor het evalueren van segmenten en het benaderen van segmentresultaten met behulp van [[!DNL Segmentation API]](../api/getting-started.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende [!DNL Adobe Experience Platform] services die betrokken zijn bij het maken van publiekssegmenten. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Staat u toe om publiekssegmenten van  [!DNL Real-time Customer Profile] gegevens te bouwen.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert.
- [Sandboxen](../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Vereiste koppen

Deze zelfstudie vereist ook dat u de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) hebt voltooid om aanroepen van [!DNL Platform] API&#39;s te kunnen uitvoeren. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Voor aanvragen voor [!DNL Platform] API&#39;s is een header vereist die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie [sandbox-overzicht](../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

Alle POST, PUT, en PATCH verzoeken vereisen een extra kopbal:

- Inhoudstype: application/json

## Een segment evalueren

Zodra u hebt ontwikkeld, getest, en uw segmentdefinitie bewaard, kunt u het segment door of geplande evaluatie of op bestelling evaluatie dan evalueren.

[De geplande evaluatie](#scheduled-evaluation)  (die ook als &quot;geplande segmentatie&quot;wordt bekend) staat u toe om een terugkomende planning voor het runnen van een uitvoerbaan in een specifieke tijd tot stand te brengen, terwijl de  [op bestelling ](#on-demand-evaluation) evaluatie het creëren van een segmentbaan impliceert om het publiek onmiddellijk te bouwen. De stappen voor elk worden hieronder geschetst.

Als u [nog geen segment gebruikend de Segmentatie API](./create-a-segment.md) leerprogramma hebt gecreeerd of een segmentdefinitie gebruikend [de Bouwer van het Segment ](../ui/overview.md) gecreeerd, te doen gelieve dit alvorens met dit leerprogramma te werk te gaan.

## Geplande evaluatie {#scheduled-evaluation}

Via een geplande evaluatie kan uw IMS-organisatie een terugkerend schema maken om exporttaken automatisch uit te voeren.

>[!NOTE]
>
>De geplande evaluatie kan voor zandbakken met een maximum van vijf (5) fusiebeleid voor [!DNL XDM Individual Profile] worden toegelaten. Als uw organisatie meer dan vijf samenvoegingsbeleid voor [!DNL XDM Individual Profile] binnen één enkele zandbakmilieu heeft, zult u geen geplande evaluatie kunnen gebruiken.

### Een schema maken

Door een verzoek van de POST aan het `/config/schedules` eindpunt te doen, kunt u een programma tot stand brengen en de specifieke tijd omvatten wanneer het programma zou moeten worden teweeggebracht.

Meer gedetailleerde informatie over het gebruiken van dit eindpunt kan in [planningseindpuntgids](../api/schedules.md#create) worden gevonden

### Een schema inschakelen

Door gebrek, is een programma inactief wanneer gecreeerd tenzij het `state` bezit aan `active` in creeer (POST) verzoeklichaam wordt geplaatst. U kunt een programma toelaten (plaats `state` aan `active`) door een verzoek van PATCH aan het `/config/schedules` eindpunt en met inbegrip van identiteitskaart van het programma in de weg in te dienen.

Meer gedetailleerde informatie over het gebruiken van dit eindpunt kan in [planningseindpuntgids](../api/schedules.md#update-state) worden gevonden

### Werk de planningstijd bij

De timing van het programma kan worden bijgewerkt door een verzoek van de PATCH aan het `/config/schedules` eindpunt en met inbegrip van identiteitskaart van het programma in de weg te doen.

Meer gedetailleerde informatie over het gebruiken van dit eindpunt kan in [planningseindpuntgids](../api/schedules.md#update-schedule) worden gevonden

## Evaluatie op aanvraag

De evaluatie op bestelling staat u toe om een segmentbaan tot stand te brengen om een publiekssegment te produceren wanneer u het vereist. In tegenstelling tot geplande evaluatie, zal dit slechts gebeuren wanneer gevraagd en niet terugkerend.

### Een segmenttaak maken

Een segmentbaan is een asynchroon proces dat tot een nieuw publiekssegment leidt. Het verwijst naar een segmentdefinitie, evenals naar elk samenvoegbeleid dat bepaalt hoe [!DNL Real-time Customer Profile] overlappende kenmerken over uw profielfragmenten samenvoegt. Wanneer een segmentbaan met succes voltooit, kunt u diverse informatie over het segment, zoals om het even welke fouten verzamelen die tijdens verwerking en de uiteindelijke grootte van uw publiek kunnen zijn voorgekomen.

U kunt een nieuwe segmentbaan tot stand brengen door een verzoek van de POST aan het `/segment/jobs` eindpunt in [!DNL Real-time Customer Profile] API te doen.

Meer gedetailleerde informatie over het gebruiken van dit eindpunt kan in [segmentbaaneindpunt gids](../api/segment-jobs.md#create) worden gevonden


### Status segmenttaak opzoeken

U kunt `id` voor een specifieke segmentbaan gebruiken om een raadplegingsverzoek (GET) uit te voeren om de huidige status van de baan te bekijken.

Meer gedetailleerde informatie over het gebruiken van dit eindpunt kan in [segmentbaaneindpunt gids](../api/segment-jobs.md#get) worden gevonden

## Segmentresultaten interpreteren

Wanneer de segmentbanen met succes in werking worden gesteld, wordt de kaart `segmentMembership` bijgewerkt voor elk profiel inbegrepen binnen het segment. `segmentMembership` slaat ook om het even welke vooraf beoordeelde publiekssegmenten op die in worden opgenomen  [!DNL Platform], die voor integratie met andere oplossingen zoals  [!DNL Adobe Audience Manager]toestaan.

In het volgende voorbeeld wordt getoond hoe het kenmerk `segmentMembership` eruit ziet voor elke afzonderlijke profielrecord:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `lastQualificationTime` | De tijdstempel op het moment dat de bevestiging van het segmentlidmaatschap werd uitgevoerd en het profiel het segment inging of verlaat. |
| `status` | De status van segmentdeelname als onderdeel van het huidige verzoek. Moet gelijk zijn aan een van de volgende bekende waarden: <ul><li>`existing`: Entiteit blijft deel uitmaken van het segment.</li><li>`realized`: De entiteit gaat het segment in.</li><li>`exited`: Entiteit verlaat het segment.</li></ul> |

## Resultaten van toegangssegmenten

De resultaten van een segmentbaan kunnen op één van twee manieren worden betreden: u kunt tot individuele profielen toegang hebben of een volledig publiek naar een dataset uitvoeren.

In de volgende secties worden deze opties gedetailleerder beschreven.

## Een profiel opzoeken

Als u het specifieke profiel kent waartoe u toegang wilt hebben, kunt u dit doen gebruikend [!DNL Real-time Customer Profile] API. De volledige stappen voor toegang tot individuele profielen zijn beschikbaar in de [Toegang tot gegevens van het Profiel van de Klant in real time gebruikend het Profiel API](../../profile/api/entities.md) leerprogramma.

## Een segment {#export} exporteren

Nadat een segmentatietaak met succes is voltooid (de waarde van het `status` attribuut is &quot;SUCCEEDED&quot;), kunt u uw publiek naar een dataset uitvoeren waar het kan worden betreden en worden gehandeld.

De volgende stappen zijn vereist om uw publiek te exporteren:

- [Creeer een doeldataset](#create-a-target-dataset)  - creeer de dataset om publieksleden te houden.
- [Produceer publieksprofielen in de dataset](#generate-profiles-for-audience-members)  - bevolk de dataset met Individuele Profielen XDM die op de resultaten van een segmentbaan worden gebaseerd.
- [Voortgang](#monitor-export-progress)  export controleren - De huidige voortgang van het exportproces controleren.
- [Lees publieksgegevens](#next-steps)  - Haal de resulterende afzonderlijke XDM-profielen op die de leden van uw publiek vertegenwoordigen.

### Een doelgegevensset maken

Wanneer het uitvoeren van een publiek, moet een doeldataset eerst worden gecreeerd. Het is belangrijk dat de dataset correct wordt gevormd om de uitvoer succesvol te verzekeren.

Één van de belangrijkste overwegingen is het schema waarop de dataset (`schemaRef.id` in het API steekproefverzoek hieronder) wordt gebaseerd. Als u een segment wilt exporteren, moet de gegevensset zijn gebaseerd op [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Een verenigingsschema is een systeem-geproduceerd, read-only schema dat de gebieden van schema&#39;s samenvoegt die de zelfde klasse delen, in dit geval dat de Individuele klasse van het Profiel XDM is. Voor meer informatie over de schema&#39;s van de verenigingsmening, te zien gelieve [sectie van het Profiel van de Klant in real time van de Ontwikkelaar van het Registratie van het Schema gids](../../xdm/api/getting-started.md).

Er zijn twee manieren om de noodzakelijke dataset tot stand te brengen:

- **Het gebruiken APIs:** de stappen die in deze zelfstudie volgen schetsen hoe te om een dataset tot stand te brengen die verwijzingen  [!DNL XDM Individual Profile Union Schema] gebruikend  [!DNL Catalog] API.
- **Gebruikend UI:** om het  [!DNL Adobe Experience Platform] gebruikersinterface te gebruiken om een dataset tot stand te brengen die verwijzingen het unieschema, de stappen in het  [UI ](../ui/overview.md) leerprogramma volgen en dan aan dit leerprogramma terugkeren om met de stappen te werk te gaan voor het  [produceren van publieksprofielen](#generate-xdm-profiles-for-audience-members).

Als u reeds een compatibele dataset hebt en zijn identiteitskaart kent, kunt u aan de stap voor [het produceren van publieksprofielen](#generate-xdm-profiles-for-audience-members) direct te werk gaan.

**API-indeling**

```http
POST /dataSets
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe dataset, die configuratieparameters in de lading verstrekken.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true
    }
}'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | Een beschrijvende naam voor de gegevensset. |
| `schemaRef.id` | Identiteitskaart van de verenigingsmening (schema) dat de dataset zal worden geassocieerd met. |
| `fileDescription.persisted` | Een Booleaanse waarde; als de waarde is ingesteld op `true`, kan de gegevensset blijven staan in de samenvoegweergave. |

**Antwoord**

Een succesvolle reactie keert een serie terug die read-only, systeem-geproduceerde unieke identiteitskaart van de pas gecreëerde dataset bevat. Een behoorlijk gevormde dataset identiteitskaart wordt vereist om publieksleden met succes uit te voeren.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Profielen genereren voor publieksleden {#generate-profiles}

Zodra u een unie-persisterende dataset hebt, kunt u een uitvoerbaan creëren om de publieksleden aan de dataset door een verzoek van de POST aan het `/export/jobs` eindpunt in [!DNL Real-time Customer Profile] API voort te zetten en dataset ID en de segmentinformatie voor de segmenten te verstrekken die u wenst om uit te voeren.

Meer gedetailleerde informatie over het gebruiken van dit eindpunt kan in [de gids van het de baaneindpunt van de uitvoer](../api/export-jobs.md#create) worden gevonden

### Exportvoortgang volgen

Als processen van de uitvoerbaan, kunt u zijn status controleren door een verzoek van de GET aan het `/export/jobs` eindpunt en met inbegrip van `id` van de uitvoerbaan in de weg te richten. De exporttaak is voltooid wanneer het veld `status` de waarde &quot;SUCCEEDED&quot; retourneert.

Meer gedetailleerde informatie over het gebruiken van dit eindpunt kan in [de gids van het de baaneindpunt van de uitvoer](../api/export-jobs.md#get) worden gevonden

## Volgende stappen

Nadat het exporteren is voltooid, zijn uw gegevens beschikbaar in [!DNL Data Lake] in [!DNL Experience Platform]. U kunt [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) dan gebruiken om tot de gegevens toegang te hebben gebruikend `batchId` verbonden aan de uitvoer. Afhankelijk van de grootte van het segment, kunnen de gegevens in brokken zijn en de partij kan uit verscheidene dossiers bestaan.

Voor geleidelijke instructies op hoe te om [!DNL Data Access] API te gebruiken om tot partijdossiers toegang te hebben en te downloaden, volg [de zelfstudie van de Toegang van Gegevens](../../data-access/tutorials/dataset-data.md).

U kunt geëxporteerde segmentgegevens ook benaderen met [!DNL Adobe Experience Platform Query Service]. Met de UI of RESTful API kunt u [!DNL Query Service] query&#39;s schrijven, valideren en uitvoeren op gegevens binnen [!DNL Data Lake].

Voor meer informatie over hoe te om publieksgegevens te vragen, te herzien gelieve de documentatie op [[!DNL Query Service]](../../query-service/home.md).
