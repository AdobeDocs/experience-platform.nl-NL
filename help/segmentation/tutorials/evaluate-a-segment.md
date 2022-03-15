---
keywords: Experience Platform;huis;populaire onderwerpen;segmentbeoordeling;Segmenteringsdienst;segmentatie;segmentatie;evalueer een segment;toegangssegmentresultaten;evalueer en toegangssegment;
solution: Experience Platform
title: Evalueer en de Resultaten van het Segment van de Toegang
topic-legacy: tutorial
type: Tutorial
description: Volg deze zelfstudie om te leren hoe u segmenten en toegangssegmentresultaten kunt evalueren met de Adobe Experience Platform Segmentation Service API.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 885ebbcae223229f4614acd5b50266ea11bcf906
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 0%

---

# Evalueer en open segmentresultaten

Dit document biedt een zelfstudie voor het evalueren van segmenten en het benaderen van segmentresultaten met behulp van [[!DNL Segmentation API]](../api/getting-started.md).

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende [!DNL Adobe Experience Platform] de diensten betrokken bij het creëren van publiekssegmenten. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Hiermee kunt u publiekssegmenten maken op basis van [!DNL Real-time Customer Profile] gegevens.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor het Platform gegevens van de klantenervaring organiseert. Als u de segmentatie het beste wilt gebruiken, moet u ervoor zorgen dat uw gegevens als profielen en gebeurtenissen worden opgenomen volgens de [best practices voor gegevensmodellering](../../xdm/schema/best-practices.md).
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Vereiste koppen

Voor deze zelfstudie hebt u ook het volgende nodig: [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) om met succes vraag te maken aan [!DNL Platform] API&#39;s. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Verzoeken om [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle POST, PUT, en PATCH verzoeken vereisen een extra kopbal:

- Inhoudstype: application/json

## Een segment evalueren

Zodra u hebt ontwikkeld, getest, en uw segmentdefinitie bewaard, kunt u het segment door of geplande evaluatie of op bestelling evaluatie dan evalueren.

[Geplande evaluatie](#scheduled-evaluation) (ook wel &#39;geplande segmentatie&#39; genoemd) kunt u een terugkerend schema maken voor het uitvoeren van een exporttaak op een bepaald moment, terwijl [evaluatie op aanvraag](#on-demand-evaluation) betekent dat u een segmenttaak maakt om het publiek direct op te bouwen. De stappen voor elk worden hieronder geschetst.

Als u nog niet de [een segment maken met de segmentatie-API](./create-a-segment.md) zelfstudie of definitie van segment maken met [Segment Builder](../ui/overview.md), doe dit voordat u verdergaat met deze zelfstudie.

## Geplande evaluatie {#scheduled-evaluation}

Via een geplande evaluatie kan uw IMS-organisatie een terugkerend schema maken om exporttaken automatisch uit te voeren.

>[!NOTE]
>
>De geplande evaluatie kan voor zandbakken met een maximum van vijf (5) fusiebeleid voor worden toegelaten [!DNL XDM Individual Profile]. Als uw organisatie meer dan vijf samenvoegbeleidsregels heeft voor [!DNL XDM Individual Profile] binnen één sandboxomgeving kunt u geen geplande evaluatie gebruiken.

### Een schema maken

Door een POST aan de `/config/schedules` eindpunt, kunt u een programma tot stand brengen en de specifieke tijd omvatten wanneer het programma zou moeten worden teweeggebracht.

Meer gedetailleerde informatie over het gebruik van dit eindpunt vindt u in de [plannings eindgids](../api/schedules.md#create)

### Een schema inschakelen

Een schema is standaard inactief wanneer het wordt gemaakt, tenzij het `state` eigenschap is ingesteld op `active` in de create (POST) aanvraaginstantie. U kunt een programma inschakelen (stel de `state` tot `active`) door een PATCH-verzoek aan de `/config/schedules` en met inbegrip van identiteitskaart van het programma in de weg.

Meer gedetailleerde informatie over het gebruik van dit eindpunt vindt u in de [plannings eindgids](../api/schedules.md#update-state)

### Werk de planningstijd bij

De timing van het programma kan worden bijgewerkt door een verzoek van de PATCH aan het `/config/schedules` en met inbegrip van identiteitskaart van het programma in de weg.

Meer gedetailleerde informatie over het gebruik van dit eindpunt vindt u in de [plannings eindgids](../api/schedules.md#update-schedule)

## Evaluatie op aanvraag

De evaluatie op bestelling staat u toe om een segmentbaan tot stand te brengen om een publiekssegment te produceren wanneer u het vereist. In tegenstelling tot geplande evaluatie, zal dit slechts gebeuren wanneer gevraagd en niet terugkerend.

### Een segmenttaak maken

Een segmentbaan is een asynchroon proces dat tot een publiekssegment op bestelling leidt. Het verwijst naar een segmentdefinitie evenals om het even welk samenvoegbeleid dat controleert hoe [!DNL Real-time Customer Profile] Hiermee voegt u overlappende kenmerken samen in uw profielfragmenten. Wanneer een segmentbaan met succes voltooit, kunt u diverse informatie over het segment, zoals om het even welke fouten verzamelen die tijdens verwerking en de uiteindelijke grootte van uw publiek kunnen zijn voorgekomen. Een segmentbaan moet in werking worden gesteld telkens als u het publiek wilt verfrissen dat momenteel voor de segmentdefinitie kwalificeert.

U kunt een nieuwe segmentbaan tot stand brengen door een verzoek van de POST aan `/segment/jobs` in de [!DNL Real-time Customer Profile] API.

Meer gedetailleerde informatie over het gebruik van dit eindpunt vindt u in de [eindgids voor segmenttaken](../api/segment-jobs.md#create)

### Status segmenttaak opzoeken

U kunt de `id` voor een specifieke segmentbaan om een raadplegingsverzoek (GET) uit te voeren om de huidige status van de baan te bekijken.

Meer gedetailleerde informatie over het gebruik van dit eindpunt vindt u in de [eindgids voor segmenttaken](../api/segment-jobs.md#get)

## Segmentresultaten interpreteren

Wanneer segmenttaken correct worden uitgevoerd, wordt `segmentMembership` De kaart wordt bijgewerkt voor elk profiel inbegrepen binnen het segment. `segmentMembership` slaat ook om het even welke vooraf beoordeelde publiekssegmenten op die in worden opgenomen [!DNL Platform], waardoor integratie met andere oplossingen zoals [!DNL Adobe Audience Manager].

In het volgende voorbeeld wordt getoond wat de `segmentMembership` Het kenmerk ziet er zo uit voor elke afzonderlijke profielrecord:

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

Als u het specifieke profiel kent waartoe u toegang wilt hebben, kunt u dit doen door [!DNL Real-time Customer Profile] API. De volledige stappen voor toegang tot individuele profielen zijn beschikbaar in het dialoogvenster [Toegang tot gegevens in realtime klantprofiel met de profiel-API](../../profile/api/entities.md) zelfstudie.

## Een segment exporteren {#export}

Nadat een segmentatietaak is voltooid (de waarde van de opdracht `status` attribuut is &quot;SUCCEEDED&quot;), kunt u uw publiek naar een dataset uitvoeren waar het kan worden betreden en op gehandeld.

De volgende stappen zijn vereist om uw publiek te exporteren:

- [Een doelgegevensset maken](#create-a-target-dataset) - Maak de dataset om publieksleden te houden.
- [Profielen voor het publiek genereren in de gegevensset](#generate-profiles) - Vul de dataset met Individuele Profielen XDM die op de resultaten van een segmentbaan worden gebaseerd.
- [Exportvoortgang volgen](#monitor-export-progress) - Controleer de huidige voortgang van het exportproces.
- [Lees de publieksgegevens](#next-steps) - Haal de resulterende afzonderlijke XDM-profielen op die de leden van uw publiek vertegenwoordigen.

### Een doelgegevensset maken {#create-dataset}

Wanneer het uitvoeren van een publiek, moet een doeldataset eerst worden gecreeerd. Het is belangrijk dat de dataset correct wordt gevormd om de uitvoer succesvol te verzekeren.

Één van de belangrijkste overwegingen is het schema waarop de dataset wordt gebaseerd (`schemaRef.id` in de API voorbeeldaanvraag hieronder). Voor het exporteren van een segment moet de gegevensset gebaseerd zijn op de [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Een verenigingsschema is een systeem-geproduceerd, read-only schema dat de gebieden van schema&#39;s samenvoegt die de zelfde klasse delen, in dit geval dat de Individuele klasse van het Profiel XDM is. Voor meer informatie over de schema&#39;s van de uniview, gelieve te zien [Het gedeelte Klantprofiel in realtime van de handleiding voor ontwikkelaars van het schemaregister](../../xdm/api/getting-started.md).

Er zijn twee manieren om de noodzakelijke dataset tot stand te brengen:

- **API&#39;s gebruiken:** De stappen die in deze zelfstudie volgen schetsen hoe te om een dataset tot stand te brengen die verwijzingen [!DNL XDM Individual Profile Union Schema] met de [!DNL Catalog] API.
- **De interface gebruiken:** Als u de opdracht [!DNL Adobe Experience Platform] gebruikersinterface om een dataset tot stand te brengen die verwijzingen het unieschema, de stappen in [UI-zelfstudie](../ui/overview.md) en ga vervolgens terug naar deze zelfstudie om door te gaan met de stappen voor [profielen voor publiek genereren](#generate-profiles).

Als u reeds een compatibele dataset hebt en zijn identiteitskaart kent, kunt u aan de stap rechtstreeks te werk gaan voor [profielen voor publiek genereren](#generate-profiles).

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
    }
}'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `name` | Een beschrijvende naam voor de gegevensset. |
| `schemaRef.id` | Identiteitskaart van de verenigingsmening (schema) dat de dataset zal worden geassocieerd met. |

**Antwoord**

Een succesvolle reactie keert een serie terug die read-only, systeem-geproduceerde unieke identiteitskaart van de pas gecreëerde dataset bevat. Een behoorlijk gevormde dataset identiteitskaart wordt vereist om publieksleden met succes uit te voeren.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Profielen genereren voor publieksleden {#generate-profiles}

Zodra u een unie-persisterende dataset hebt, kunt u een uitvoerbaan tot stand brengen om de publieksleden aan de dataset voort te zetten door een verzoek van de POST aan het `/export/jobs` in de [!DNL Real-time Customer Profile] API en het verstrekken van dataset identiteitskaart en de segmentinformatie voor de segmenten die u wenst om uit te voeren.

Meer gedetailleerde informatie over het gebruik van dit eindpunt vindt u in de [eindgebruikershandleiding exporttaken](../api/export-jobs.md#create)

### Exportvoortgang volgen

Als exporttaakprocessen kunt u de status controleren door een GET-aanvraag in te dienen bij de `/export/jobs` en met inbegrip van de `id` van de exporttaak in het pad. De exporttaak is voltooid zodra de `status` retourneert de waarde &quot;SUCCEEDED&quot;.

Meer gedetailleerde informatie over het gebruik van dit eindpunt vindt u in de [eindgebruikershandleiding exporttaken](../api/export-jobs.md#get)

## Volgende stappen

Nadat het exporteren is voltooid, zijn uw gegevens beschikbaar in het dialoogvenster [!DNL Data Lake] in [!DNL Experience Platform]. U kunt dan de [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) om toegang te krijgen tot de gegevens met de `batchId` die aan de export zijn gekoppeld. Afhankelijk van de grootte van het segment, kunnen de gegevens in brokken zijn en de partij kan uit verscheidene dossiers bestaan.

Voor stapsgewijze instructies over het gebruik van de [!DNL Data Access] API voor toegang tot en download batchbestanden [Zelfstudie over gegevenstoegang](../../data-access/tutorials/dataset-data.md).

U hebt ook toegang tot geëxporteerde segmentgegevens met [!DNL Adobe Experience Platform Query Service]. Gebruikend UI of RESTful API, [!DNL Query Service] staat u toe om, vragen over gegevens te schrijven te bevestigen en in werking te stellen binnen [!DNL Data Lake].

Voor meer informatie over het vragen van publieksgegevens raadpleegt u de documentatie over [[!DNL Query Service]](../../query-service/home.md).
