---
keywords: Experience Platform;startpagina;populaire onderwerpen
solution: Experience Platform
title: API-eindpunt voor privacytaken
description: Leer hoe u privacytaken voor Experiencen Cloud-toepassingen beheert met de Privacy Service-API.
role: Developer
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: 02a95212ff8a018b2b7f0a06978307d08a6915af
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 0%

---

# Het eindpunt van privacytaken

In dit document wordt beschreven hoe u met privacytaken werkt met API-aanroepen. Het gaat specifiek over het gebruik van het eindpunt `/job` in de API van [!DNL Privacy Service] . Alvorens deze gids te lezen, verwijs naar [ begonnen gids ](./getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

>[!NOTE]
>
>Als u om toestemmings of opt-out verzoeken van klanten probeert te beheren, verwijs naar de [ gids van het toestemmingspunten ](./consent.md).

## Alle taken weergeven {#list}

U kunt een lijst van alle beschikbare privacybanen binnen uw organisatie bekijken door een verzoek van de GET tot het `/jobs` eindpunt te richten.

**API formaat**

Deze verzoekformaat gebruikt een `regulation` vraagparameter op het `/jobs` eindpunt, daarom begint het met een vraagteken (`?`) zoals hieronder getoond. Wanneer het vermelden van middelen, keert Privacy Service API tot 1000 banen terug en pagineert de reactie. Gebruik andere queryparameters (`page` , `size` en datumfilters) om de reactie te filteren. U kunt veelvoudige parameters scheiden gebruikend ampersands (`&`).

>[!TIP]
>
>Gebruik extra vraagparameters aan verdere filterresultaten voor specifieke vragen. U kunt bijvoorbeeld zien hoeveel privacytaken gedurende een bepaalde periode zijn verzonden en wat hun status is met de queryparameters `status` , `fromDate` en `toDate` .

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
GET /jobs?regulation={REGULATION}&fromDate={FROMDATE}&toDate={TODATE}&status={STATUS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{REGULATION}` | Het regulatietype waarvoor u een query wilt uitvoeren. Tot de geaccepteerde waarden behoren: <ul><li>`apa_aus`</li><li>`cpa_usa`</li><li>`cpra_usa`</li><li>`ctdpa_usa`</li><li>`fdbr_usa`</li><li>`gdpr` - Nota: Dit wordt ook gebruikt voor verzoeken met betrekking tot **ccpa** verordeningen.</li><li>`hipaa_usa`</li><li>`icdpa_usa`</li><li>`lgpd_bra`</li><li>`mcdpa_usa`</li><li>`mhmda_usa`</li><li>`ndpa_usa`</li><li>`nhpa_usa`</li><li>`njdpa_usa`</li><li>`nzpa_nzl`</li><li>`ocpa_usa`</li><li>`pdpa_tha`</li><li>`tdpsa_usa`</li><li>`ucpa_usa`</li><li>`vcdpa_usa`</li></ul><br> zie het overzicht op [ gesteunde verordeningen ](../regulations/overview.md) voor meer informatie over de privacyverordeningen die de bovengenoemde waarden vertegenwoordigen. |
| `{PAGE}` | De pagina met gegevens die moet worden weergegeven met een op 0 gebaseerde nummering. De standaardwaarde is `0` . |
| `{SIZE}` | Het aantal resultaten dat op elke pagina moet worden weergegeven. De standaardwaarde is `100` en het maximum is `1000` . Als het maximum wordt overschreden, retourneert de API een fout van 400 code. |
| `{status}` | Standaard worden alle statussen opgenomen. Als u een statustype opgeeft, worden alleen privacytaken geretourneerd die overeenkomen met dat statustype. De toegestane waarden zijn onder meer: <ul><li>`processing`</li><li>`complete`</li><li>`error`</li></ul> |
| `{toDate}` | Deze parameter beperkt de resultaten tot de resultaten die vóór een opgegeven datum zijn verwerkt. Vanaf de datum van het verzoek kan het systeem 45 dagen terugkijken. Het bereik mag echter niet langer dan 30 dagen zijn.<br> het keurt het formaat YYYY-MM-DD goed. De datum die u opgeeft, wordt geïnterpreteerd als de beëindigingsdatum uitgedrukt in Greenwich Mean Time (GMT).<br> als u deze parameter (en een overeenkomstige `fromDate`) niet verstrekt, keert het standaardgedrag banen terug die gegevens de afgelopen zeven dagen terug. Als u `toDate` gebruikt, moet u ook de parameter `fromDate` query gebruiken. Als u niet allebei gebruikt, keert de vraag een fout 400 terug. |
| `{fromDate}` | Deze parameter beperkt de resultaten tot de resultaten die na een opgegeven datum worden verwerkt. Vanaf de datum van het verzoek kan het systeem 45 dagen terugkijken. Het bereik mag echter niet langer dan 30 dagen zijn.<br> het keurt het formaat YYYY-MM-DD goed. De datum die u opgeeft, wordt geïnterpreteerd als de datum van oorsprong van het verzoek, uitgedrukt in Greenwich Mean Time (GMT).<br> als u deze parameter (en een overeenkomstige `toDate`) niet verstrekt, keert het standaardgedrag banen terug die gegevens de afgelopen zeven dagen terug. Als u `fromDate` gebruikt, moet u ook de parameter `toDate` query gebruiken. Als u niet allebei gebruikt, keert de vraag een fout 400 terug. |
| `{filterDate}` | Deze parameter beperkt de resultaten tot de resultaten die op een bepaalde datum worden verwerkt. De notatie YYYY-MM-DD wordt geaccepteerd. Het systeem kan de afgelopen 45 dagen terugkijken. |

{style="table-layout:auto"}

**Verzoek**

Met het volgende verzoek wordt een gepagineerde lijst opgehaald van alle taken binnen een organisatie, te beginnen bij de derde pagina met een paginaformaat van 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Reactie**

Een geslaagde reactie retourneert een lijst met taken, waarbij elke taak details bevat zoals de `jobId` . In dit voorbeeld bevat het antwoord een lijst met 50 taken, te beginnen op de derde pagina met resultaten.

### Volgende pagina&#39;s openen

Om de volgende reeks resultaten in een gepagineerde reactie te halen, moet u een andere API vraag aan het zelfde eindpunt maken terwijl het verhogen van de `page` vraagparameter door 1.

## Een privacytaak maken {#create-job}

>[!IMPORTANT]
>
>Privacy Service is alleen bedoeld voor betrokkenen en verzoeken om consumentenrechten. Elk ander gebruik van Privacy Service voor het opschonen of onderhouden van gegevens wordt niet ondersteund of toegestaan. Adobe is wettelijk verplicht deze tijdig te vervullen. Als zodanig is het testen van belasting op Privacy Service niet toegestaan, omdat dit een productieomgeving is en een onnodige achterstand oplevert bij geldige privacyverzoeken.
>
>Er is nu een vaste uploadlimiet voor dagelijks gebruik om misbruik van de service te voorkomen. Gebruikers die misbruik van het systeem kunnen maken, hebben toegang tot de service uitgeschakeld. Daarna zal er een vergadering met hen worden gehouden om hun acties te bespreken en te bespreken of Privacy Service aanvaardbaar is.

Voordat u een nieuwe taakaanvraag maakt, moet u eerst identificatiegegevens verzamelen over de betrokkenen van wie u de gegevens wilt benaderen, verwijderen of niet wilt verkopen. Zodra u de vereiste gegevens hebt, moet het in de lading van een verzoek van de POST aan het `/jobs` eindpunt worden verstrekt.

>[!NOTE]
>
>Compatibele Adobe Experience Cloud-toepassingen gebruiken verschillende waarden voor het identificeren van betrokkenen. Zie de gids op [ Privacy Service en de toepassingen van het Experience Cloud ](../experience-cloud-apps.md) voor meer informatie over vereiste herkenningstekens voor uw toepassing(en). Voor meer algemene begeleiding bij het bepalen van welke IDs naar [!DNL Privacy Service] te verzenden, zie het document op [ identiteitsgegevens in privacyverzoeken ](../identity-data.md).

De API van [!DNL Privacy Service] ondersteunt twee soorten taakaanvragen voor persoonlijke gegevens:

* [ toegang en/of schrapping ](#access-delete): Toegang (lees) of schrap persoonlijke gegevens.
* [ Opt uit verkoop ](#opt-out): Teken persoonlijke gegevens als niet te verkopen.

>[!IMPORTANT]
>
>Terwijl toegang en schrappingsverzoeken als één enkele API vraag kunnen worden gecombineerd, opt-out verzoeken moeten afzonderlijk worden gemaakt.

### Een toegangs-/verwijdertaak maken {#access-delete}

In deze sectie ziet u hoe u een aanvraag voor een toegangs-/verwijdertaak uitvoert met de API.

**API formaat**

```http
POST /jobs
```

**Verzoek**

Het volgende verzoek leidt tot een nieuw baanverzoek, dat door de attributen wordt gevormd die in de nuttige lading worden geleverd zoals hieronder beschreven.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager","profileService"],
    "expandIds": false,
    "priority": "normal",
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `companyContexts` **(Required)** | Een array met verificatiegegevens voor uw organisatie. Elke weergegeven id bevat de volgende kenmerken: <ul><li>`namespace`: De naamruimte van een id.</li><li>`value`: De waarde van de id.</li></ul>Het wordt **vereist** dat één van de herkenningstekens `imsOrgId` als zijn `namespace` gebruikt, met zijn `value` die unieke identiteitskaart voor uw organisatie bevatten. <br/><br/> de Extra herkenningstekens kunnen product-specifieke bedrijfkwalificfiers (bijvoorbeeld, `Campaign`) zijn, die een integratie met een toepassing van de Adobe identificeren die tot uw organisatie behoort. Mogelijke waarden zijn accountnamen, clientcodes, gebruikers-id&#39;s of andere toepassings-id&#39;s. |
| `users` **(Required)** | Een array die een verzameling van ten minste één gebruiker bevat waarvan u de gegevens wilt openen of verwijderen. Een maximum van 1000 gebruikers kan in één enkel verzoek worden verstrekt. Elk gebruikersobject bevat de volgende informatie: <ul><li>`key`: Een id voor een gebruiker die wordt gebruikt om de afzonderlijke taak-id&#39;s in de reactiegegevens te kwalificeren. Het is aan te raden een unieke, gemakkelijk identificeerbare tekenreeks voor deze waarde te kiezen, zodat er later gemakkelijk naar kan worden verwezen of deze kan worden opgezocht.</li><li>`action`: Een array met de acties die moeten worden uitgevoerd op basis van de gegevens van de gebruiker. Afhankelijk van de handelingen die u wilt uitvoeren, moet deze array `access` , `delete` of beide bevatten.</li><li>`userIDs`: Een verzameling identiteiten voor de gebruiker. Het aantal identiteiten dat één gebruiker kan hebben, is beperkt tot negen. Elke identiteit bestaat uit een `namespace` , een `value` , en een namespace kwalificfier (`type`). Zie [ bijlage ](appendix.md) voor meer details over deze vereiste eigenschappen.</li></ul> Voor een meer gedetailleerde verklaring van `users` en `userIDs`, zie de [ het oplossen van problemengids ](../troubleshooting-guide.md#user-ids). |
| `include` **(Required)** | Een array met producten van de Adobe die in de verwerking moeten worden opgenomen. Als deze waarde ontbreekt of anderszins leeg is, wordt het verzoek afgewezen. Omvat slechts producten die uw organisatie een integratie met heeft. Zie de sectie op [ erkende productwaarden ](appendix.md) in het bijlage voor meer informatie. |
| `expandIDs` | Een optionele eigenschap die, indien ingesteld op `true`, een optimalisatie vertegenwoordigt voor het verwerken van de id&#39;s in de toepassingen (momenteel alleen ondersteund door [!DNL Analytics] ). Als deze waarde wordt weggelaten, wordt deze standaard ingesteld op `false` . |
| `priority` | Een optionele eigenschap die door Adobe Analytics wordt gebruikt en die de prioriteit voor het verwerken van aanvragen instelt. Geaccepteerde waarden zijn `normal` en `low`. Wanneer `priority` wordt weggelaten, is het standaardgedrag `normal` . |
| `mergePolicyId` | Wanneer het maken van privacyverzoeken voor het Profiel van de Klant in real time (`profileService`), kunt u naar keuze identiteitskaart van het specifieke [ fusiebeleid ](../../profile/merge-policies/overview.md) verstrekken dat u voor identiteitskaart het stitching wilt gebruiken. Door een samenvoegbeleid te specificeren, kunnen de privacyverzoeken publieksinformatie omvatten wanneer het terugkeren van gegevens over een klant. Per aanvraag kan slechts één samenvoegbeleid worden opgegeven. Als er geen samenvoegingsbeleid is opgegeven, wordt segmenteringsinformatie niet opgenomen in de reactie. |
| `regulation` **(Required)** | De verordening voor de privacybaan. De volgende waarden worden geaccepteerd: <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br> zie het overzicht op [ gesteunde verordeningen ](../regulations/overview.md) voor meer informatie over de privacyverordeningen die de bovengenoemde waarden vertegenwoordigen. |

{style="table-layout:auto"}

**Reactie**

Een succesvol antwoord geeft de details van de nieuwe banen terug.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076be029f3",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd023j1",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "delete"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 3
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `jobId` | Een alleen-lezen, unieke door het systeem gegenereerde id voor een taak. Deze waarde wordt gebruikt in de volgende stap van het opzoeken van een specifieke taak. |

{style="table-layout:auto"}

Zodra u met succes het baanverzoek hebt voorgelegd, kunt u aan de volgende stap van [ te werk gaan controlerend de status van de baan ](#check-status).

## De status van een taak controleren {#check-status}

U kunt informatie over een specifieke baan, zoals zijn huidige verwerkingsstatus terugwinnen, door de baan `jobId` in de weg van een verzoek van de GET aan het `/jobs` eindpunt te omvatten.

>[!IMPORTANT]
>
>Gegevens voor eerder gemaakte taken kunnen alleen binnen 30 dagen na de einddatum van de taak worden opgehaald.

**API formaat**

```http
GET /jobs/{JOB_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{JOB_ID}` | De id van de taak die u wilt opzoeken. Deze identiteitskaart is teruggekeerd onder `jobId` in succesvolle API reacties voor [ creërend een baan ](#create-job) en [ die van alle banen ](#list) een lijst maken. |

{style="table-layout:auto"}

**Verzoek**

Met het volgende verzoek worden de details opgehaald van de taak waarvan `jobId` is opgegeven in het aanvraagpad.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Reactie**

Een geslaagde reactie retourneert de details van de opgegeven taak.

```json
{
    "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "complete",
    "submittedBy": "{ACCOUNT_ID}",
    "createdDate": "10/02/2019 08:25 PM GMT",
    "lastModifiedDate": "10/02/2019 08:25 PM GMT",
    "userIds": [
        {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard",
            "namespaceId": 6,
            "isDeletedClientSide": false
        },
        {
            "namespace": "ECID",
            "value": "1123A4D5690B32A",
            "type": "standard",
            "namespaceId": 4,
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Analytics",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Finished successfully."
            }
        },
        {
            "product": "Profile",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Success dataSetIds = [5dbb87aad37beb18a96feb61], Failed dataSetIds = []"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6054-200",
                "responseMsgDetail": "PARTIALLY COMPLETED- Data not found for some requests, check results for more info.",
                "results": {
                  "processed": ["1123A4D5690B32A"],
                  "ignored": ["dsmith@acme.com"]
                }
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `productStatusResponse` | Elk object in de array `productResponses` bevat informatie over de huidige status van de taak ten opzichte van een specifieke [!DNL Experience Cloud] -toepassing. |
| `productStatusResponse.status` | De huidige statuscategorie van de taak. Zie de lijst hieronder voor een lijst van [ beschikbare statuscategorieën ](#status-categories) en hun overeenkomstige betekenissen. |
| `productStatusResponse.message` | De specifieke status van de taak, die overeenkomt met de statuscategorie. |
| `productStatusResponse.responseMsgCode` | Een standaardcode voor productresponsberichten die worden ontvangen door [!DNL Privacy Service] . De details van het bericht worden onder `responseMsgDetail` verstrekt. |
| `productStatusResponse.responseMsgDetail` | Een gedetailleerdere uitleg van de status van de baan. Berichten voor vergelijkbare statussen kunnen per product verschillen. |
| `productStatusResponse.results` | Voor bepaalde statussen kunnen sommige producten een `results` -object retourneren dat aanvullende informatie biedt die niet door `responseMsgDetail` wordt gedekt. |
| `downloadURL` | Als de status van de taak `complete` is, verschaft dit kenmerk een URL waarmee de taakresultaten als een ZIP-bestand kunnen worden gedownload. Dit bestand kan 60 dagen nadat de taak is voltooid, worden gedownload. |

{style="table-layout:auto"}

### Taakstatuscategorieën {#status-categories}

In de volgende tabel worden de verschillende mogelijke taakstatuscategorieën en de bijbehorende betekenis weergegeven:

| Status categorie | Betekenis |
| -------------- | -------- |
| `complete` | De taak is voltooid en (indien vereist) worden bestanden vanuit elke toepassing geüpload. |
| `processing` | Toepassingen hebben de taak erkend en worden momenteel verwerkt. |
| `submitted` | De taak wordt voorgelegd aan elke toepasselijke toepassing. |
| `error` | Er is iets misgegaan in de verwerking van de taak - er kan meer specifieke informatie worden verkregen door individuele taakdetails op te halen. |

{style="table-layout:auto"}

>[!NOTE]
>
>Een verzonden taak kan in de status `processing` blijven als deze een afhankelijke onderliggende taak heeft die nog wordt verwerkt.

## Volgende stappen

U weet nu hoe u met de API [!DNL Privacy Service] privacytaken kunt maken en controleren. Voor informatie over hoe te om de zelfde taken uit te voeren gebruikend het gebruikersinterface, zie het [ overzicht van de Privacy Service UI ](../ui/overview.md).
