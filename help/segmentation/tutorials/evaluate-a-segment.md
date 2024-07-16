---
solution: Experience Platform
title: Evalueer en de Resultaten van het Segment van de Toegang
type: Tutorial
description: Volg deze zelfstudie om te leren hoe u segmentatiedefinities en toegangssegmenteringsresultaten kunt evalueren met de Adobe Experience Platform Segmentation Service API.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 0%

---

# Evalueer en open de resultaten van de segmentdefinitie

Dit document bevat een zelfstudie voor het evalueren van segmentdefinities en het openen van deze resultaten met de [[!DNL Segmentation API]](../api/getting-started.md) .

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende [!DNL Adobe Experience Platform] -services die betrokken zijn bij het maken van een publiek. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, klantprofiel in real-time op basis van geaggregeerde gegevens van meerdere bronnen.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): hiermee kunt u soorten publiek maken op basis van [!DNL Real-Time Customer Profile] -gegevens.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee Platform gegevens voor klantervaring organiseert. Om het beste gebruik van Segmentatie te maken, gelieve te verzekeren uw gegevens als profielen en gebeurtenissen volgens de [ beste praktijken voor gegevens modellering ](../../xdm/schema/best-practices.md) worden opgenomen.
- [ Sandboxen ](../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Vereiste koppen

Dit leerprogramma vereist u ook om het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) te voltooien om vraag aan [!DNL Platform] APIs met succes te maken. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Voor aanvragen van [!DNL Platform] API&#39;s is een header vereist die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

Alle POST, PUT, en PATCH verzoeken vereisen een extra kopbal:

- Inhoudstype: application/json

## Een segmentdefinitie evalueren {#evaluate-a-segment}

Zodra u hebt ontwikkeld, getest en uw segmentdefinitie bewaard, kunt u de segmentdefinitie door of geplande evaluatie of op bestelling evaluatie dan evalueren.

[ Geplande evaluatie ](#scheduled-evaluation) (ook genoemd geworden &quot;geplande segmentatie&quot;wordt bekend) staat u toe om een terugkomende planning voor het runnen van een uitvoerbaan in een specifieke tijd tot stand te brengen, terwijl [ op bestelling evaluatie ](#on-demand-evaluation) impliceert het creëren van een segmentbaan om het publiek onmiddellijk te bouwen. De stappen voor elk worden hieronder geschetst.

Als u nog niet [ hebt voltooid creeer een segmentdefinitie gebruikend de Segmentatie API ](./create-a-segment.md) leerprogramma of creeerde een segmentdefinitie gebruikend [ de Bouwer van het Segment ](../ui/segment-builder.md), gelieve dit te doen alvorens met dit leerprogramma te werk te gaan.

## Geplande evaluatie {#scheduled-evaluation}

Door geplande evaluatie, kan uw organisatie een terugkomende planning tot stand brengen om de uitvoerbanen automatisch in werking te stellen.

>[!NOTE]
>
>Een geplande evaluatie kan worden ingeschakeld voor sandboxen met maximaal vijf (5) samenvoegbeleidsregels voor [!DNL XDM Individual Profile] . Als uw organisatie meer dan vijf samenvoegbeleidsregels voor [!DNL XDM Individual Profile] heeft binnen één sandbox-omgeving, kunt u geen geplande evaluatie gebruiken.

### Een schema maken

Door een verzoek van de POST aan het `/config/schedules` eindpunt te doen, kunt u een programma tot stand brengen en de specifieke tijd omvatten wanneer het programma zou moeten worden teweeggebracht.

Meer gedetailleerde informatie over het gebruiken van dit eindpunt kan in de [ gids van het planningseindpunt ](../api/schedules.md#create) worden gevonden

### Een schema inschakelen

Een schema is standaard niet actief wanneer het wordt gemaakt, tenzij de eigenschap `state` is ingesteld op `active` in de aanvraagtekst (POST) create. U kunt een schema inschakelen (stel `state` in op `active` ) door een PATCH-aanvraag in te dienen bij het `/config/schedules` -eindpunt en de id van het schema op te nemen in het pad.

Meer gedetailleerde informatie over het gebruiken van dit eindpunt kan in de [ gids van het planningseindpunt ](../api/schedules.md#update-state) worden gevonden

### Werk de planningstijd bij

De timing van het programma kan worden bijgewerkt door een verzoek van de PATCH aan het `/config/schedules` eindpunt en met inbegrip van identiteitskaart van het programma in de weg te doen.

Meer gedetailleerde informatie over het gebruiken van dit eindpunt kan in de [ gids van het planningseindpunt ](../api/schedules.md#update-schedule) worden gevonden

## Evaluatie op aanvraag

De evaluatie op bestelling staat u toe om een segmentbaan tot stand te brengen om een publiek te produceren wanneer u het vereist. In tegenstelling tot geplande evaluatie, zal dit slechts gebeuren wanneer gevraagd en niet terugkerend.

### Een segmenttaak maken

Een segmentbaan is een asynchroon proces dat tot een publiekssegment op bestelling leidt. Het verwijst naar een segmentdefinitie en naar elk samenvoegbeleid dat bepaalt hoe [!DNL Real-Time Customer Profile] overlappende kenmerken in uw profielfragmenten samenvoegt. Wanneer een segmentbaan met succes voltooit, kunt u diverse informatie over de segmentdefinitie, zoals om het even welke fouten verzamelen die tijdens verwerking en de uiteindelijke grootte van uw publiek kunnen zijn voorgekomen. Een segmentbaan moet in werking worden gesteld telkens als u het publiek wilt verfrissen dat de segmentdefinitie momenteel kwalificeert.

U kunt een nieuwe segmenttaak maken door een aanvraag voor een POST in te dienen bij het eindpunt `/segment/jobs` in de [!DNL Real-Time Customer Profile] API.

De meer gedetailleerde informatie over het gebruiken van dit eindpunt kan in de [ gids van het segmentbaneneindpunt ](../api/segment-jobs.md#create) worden gevonden

### Status segmenttaak opzoeken

U kunt `id` voor een specifieke segmentbaan gebruiken om een raadplegingsverzoek (GET) uit te voeren om de huidige status van de baan te bekijken.

De meer gedetailleerde informatie over het gebruiken van dit eindpunt kan in de [ gids van het segmentbaneneindpunt ](../api/segment-jobs.md#get) worden gevonden

## Resultaten van segmenttaken interpreteren

Wanneer segmenttaken zijn uitgevoerd, wordt de `segmentMembership` -kaart bijgewerkt voor elk profiel dat is opgenomen in de segmentdefinitie. `segmentMembership` slaat ook vooraf beoordeelde soorten publiek op die in [!DNL Platform] worden opgenomen, zodat deze kunnen worden geïntegreerd met andere oplossingen, zoals [!DNL Adobe Audience Manager] .

In het volgende voorbeeld wordt getoond hoe het kenmerk `segmentMembership` er uitziet voor elke afzonderlijke profielrecord:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "realized"
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
| `lastQualificationTime` | Het tijdstempel waarin de bevestiging van segmentlidmaatschap werd gemaakt en het profiel de segmentdefinitie inging of verwierp. |
| `status` | De deelnamestatus van de segmentdefinitie als onderdeel van de huidige aanvraag. Moet gelijk zijn aan een van de volgende bekende waarden: <ul><li>`realized`: entiteit komt in aanmerking voor de segmentdefinitie.</li><li>`exited`: entiteit sluit de segmentdefinitie af.</li></ul> |

>[!NOTE]
>
>Elk segmentlidmaatschap dat meer dan 30 dagen in de `exited` -status is, gebaseerd op `lastQualificationTime` , wordt verwijderd.

## Resultaten van segmenttaken openen

De resultaten van een segmentbaan kunnen op één van twee manieren worden betreden: u kunt tot individuele profielen toegang hebben of een volledig publiek naar een dataset uitvoeren.

In de volgende secties worden deze opties gedetailleerder beschreven.

## Een profiel opzoeken

Als u het specifieke profiel kent waartoe u toegang wilt hebben, kunt u dit doen door de [!DNL Real-Time Customer Profile] API te gebruiken. De volledige stappen voor de toegang tot van individuele profielen zijn beschikbaar in de [ Realtime gegevens van het Profiel van de Klant van de Toegang gebruikend het profiel API ](../../profile/api/entities.md) leerprogramma.

## Een segment exporteren {#export}

Nadat een segmentatietaak is voltooid (de waarde van het kenmerk `status` is &quot;SUCCEEDED&quot;), kunt u uw publiek exporteren naar een dataset waar toegang tot de taak mogelijk is en waarop u kunt reageren.

De volgende stappen zijn vereist om uw publiek te exporteren:

- [ creeer een doeldataset ](#create-a-target-dataset) - creeer de dataset om publieksleden te houden.
- [ produceer publieksprofielen in de dataset ](#generate-profiles) - bevolkt de dataset met Individuele Profielen XDM die op de resultaten van een segmentbaan worden gebaseerd.
- [ de uitvoervooruitgang van de Monitor ](#monitor-export-progress) - controleer de huidige vooruitgang van het uitvoerproces.
- [ leest publieksgegevens ](#next-steps) - verkrijg de resulterende Individuele Profielen XDM die de leden van uw publiek vertegenwoordigen.

### Een doelgegevensset maken {#create-dataset}

Wanneer het uitvoeren van een publiek, moet een doeldataset eerst worden gecreeerd. Het is belangrijk dat de dataset correct wordt gevormd om de uitvoer succesvol te verzekeren.

Één van de belangrijkste overwegingen is het schema waarop de dataset (`schemaRef.id` in het API steekproefverzoek hieronder) wordt gebaseerd. Om een segmentdefinitie uit te voeren, moet de dataset op [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`) worden gebaseerd. Een verenigingsschema is een systeem-geproduceerd, read-only schema dat de gebieden van schema&#39;s samenvoegt die de zelfde klasse delen, in dit geval dat de Individuele klasse van het Profiel XDM is. Voor meer informatie over de schema&#39;s van de verenigingsmening, zie gelieve de [ sectie van het Profiel van de Klant in real time van de Ontwikkelaar van het Registratie van het Schema gids ](../../xdm/api/getting-started.md).

Er zijn twee manieren om de noodzakelijke dataset tot stand te brengen:

- **Gebruikend APIs:** de stappen die in dit leerprogramma volgen schetsen hoe te om een dataset tot stand te brengen die [!DNL XDM Individual Profile Union Schema] verwijzingen gebruikend [!DNL Catalog] API.
- **Gebruikend UI:** om het [!DNL Adobe Experience Platform] gebruikersinterface te gebruiken om een dataset tot stand te brengen die verwijzingen het unieschema, de stappen in het [ UI leerprogramma ](../ui/overview.md) volgen en dan op dit leerprogramma terugkeren om met de stappen voor [ te werk te gaan producerend publieksprofielen ](#generate-profiles).

Als u reeds een compatibele dataset hebt en zijn identiteitskaart kent, kunt u aan de stap voor [ direct te werk gaan die publieksprofielen ](#generate-profiles) produceert.

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | Een beschrijvende naam voor de gegevensset. |
| `schemaRef.id` | Identiteitskaart van de verenigingsmening (schema) dat de dataset zal worden geassocieerd met. |

**Reactie**

Een succesvolle reactie keert een serie terug die read-only, systeem-geproduceerde unieke identiteitskaart van de pas gecreëerde dataset bevat. Een behoorlijk gevormde dataset identiteitskaart wordt vereist om publieksleden met succes uit te voeren.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Profielen genereren voor publieksleden {#generate-profiles}

Zodra u een unie-persisterende dataset hebt, kunt u een de uitvoerbaan tot stand brengen om de publieksleden aan de dataset door een verzoek van de POST aan het `/export/jobs` eindpunt in [!DNL Real-Time Customer Profile] API voort te zetten en de dataset ID en de informatie van de segmentdefinitie voor de segmentdefinities te verstrekken die u wenst uit te voeren.

De meer gedetailleerde informatie over het gebruiken van dit eindpunt kan in de [ gids van het de baneneindpunt van de uitvoertaken ](../api/export-jobs.md#create) worden gevonden

### Exportvoortgang volgen

Tijdens het uitvoeren van een exporttaak kunt u de status controleren door een aanvraag voor een GET in te dienen bij het eindpunt van `/export/jobs` en de `id` van de exporttaak op te nemen in het pad. De exporttaak is voltooid wanneer het veld `status` de waarde &quot;SUCCEEDED&quot; retourneert.

De meer gedetailleerde informatie over het gebruiken van dit eindpunt kan in de [ gids van het de baneneindpunt van de uitvoertaken ](../api/export-jobs.md#get) worden gevonden

## Volgende stappen

Nadat het exporteren is voltooid, zijn uw gegevens beschikbaar in de map [!DNL Data Lake] in [!DNL Experience Platform] . U kunt [[!DNL Data Access API] dan gebruiken ](https://www.adobe.io/experience-platform-apis/references/data-access/) om tot de gegevens toegang te hebben gebruikend `batchId` verbonden aan de uitvoer. Afhankelijk van de grootte van de segmentdefinitie, kunnen de gegevens in brokken zijn en de partij kan uit verscheidene dossiers bestaan.

Voor geleidelijke instructies op hoe te om [!DNL Data Access] API te gebruiken om tot partijdossiers toegang te hebben en te downloaden, volg het [ leerprogramma van de Toegang van Gegevens ](../../data-access/tutorials/dataset-data.md).

U kunt geëxporteerde segmentdefinitiegegevens ook benaderen met [!DNL Adobe Experience Platform Query Service] . Met de UI of RESTful API kunt u in [!DNL Query Service] query&#39;s schrijven, valideren en uitvoeren op gegevens binnen [!DNL Data Lake] .

Raadpleeg de documentatie bij [[!DNL Query Service]](../../query-service/home.md) voor meer informatie over het uitvoeren van query&#39;s op publieksgegevens.
