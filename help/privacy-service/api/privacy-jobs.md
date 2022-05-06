---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: API-eindpunt voor privacytaken
topic-legacy: developer guide
description: Leer hoe u privacytaken voor Experience Cloud-toepassingen beheert met de Privacy Service-API.
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 0%

---

# Het eindpunt van privacytaken

In dit document wordt beschreven hoe u met privacytaken werkt met API-aanroepen. Het betreft met name het gebruik van de `/job` in de [!DNL Privacy Service] API. Raadpleeg voordat u deze handleiding leest de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

>[!NOTE]
>
>Als u toestemmings- of opt-outverzoeken van klanten wilt beheren, raadpleegt u de [leidraad voor het eindpunt van de overeenkomst](./consent.md).

## Alle taken weergeven {#list}

U kunt een lijst weergeven met alle beschikbare privacytaken binnen uw organisatie door een aanvraag in te dienen bij de GET `/jobs` eindpunt.

**API-indeling**

Deze aanvraagindeling gebruikt een `regulation` queryparameter voor de `/jobs` eindpunt, daarom begint het met een vraagteken (`?`) zoals hieronder weergegeven. De reactie wordt gepagineerd, toestaand u om andere vraagparameters te gebruiken (`page` en `size`) om de reactie te filteren. U kunt meerdere parameters scheiden met ampersands (`&`).

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Parameter | Beschrijving |
| --- | --- |
| `{REGULATION}` | Het regulatietype waarvoor u een query wilt uitvoeren. Tot de geaccepteerde waarden behoren: <ul><li>`gdpr` (Europese Unie)</li><li>`ccpa` (Californië)</li><li>`lgpd_bra` (Brazilië)</li><li>`nzpa_nzl` (Nieuw-Zeeland)</li><li>`pdpa_tha` (Thailand)</li></ul> |
| `{PAGE}` | De pagina met gegevens die moet worden weergegeven met een op 0 gebaseerde nummering. De standaardwaarde is `0`. |
| `{SIZE}` | Het aantal resultaten dat op elke pagina moet worden weergegeven. De standaardwaarde is `1` en het maximum `100`. Als het maximum wordt overschreden, retourneert de API een fout van 400 code. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met het volgende verzoek wordt een gepagineerde lijst opgehaald van alle taken binnen een IMS-organisatie, te beginnen bij de derde pagina met een paginaformaat van 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwoord**

Een succesvol antwoord retourneert een lijst met taken, waarbij elke taak details bevat zoals de taak `jobId`. In dit voorbeeld bevat het antwoord een lijst met 50 taken, te beginnen op de derde pagina met resultaten.

### Volgende pagina&#39;s openen

Om de volgende reeks resultaten in een gepagineerde reactie te halen, moet u een andere API vraag aan het zelfde eindpunt maken terwijl het verhogen van `page` query parameter by 1.

## Een privacytaak maken {#create-job}

Voordat u een nieuwe taakaanvraag maakt, moet u eerst identificatiegegevens verzamelen over de betrokkenen van wie u de gegevens wilt benaderen, verwijderen of niet wilt verkopen. Zodra u de vereiste gegevens hebt, moet het in de lading van een verzoek van de POST aan `/jobs` eindpunt.

>[!NOTE]
>
>Compatibele Adobe Experience Cloud-toepassingen gebruiken verschillende waarden voor het identificeren van betrokkenen. Zie de handleiding op [Privacy Service- en Experience Cloud-toepassingen](../experience-cloud-apps.md) voor meer informatie over vereiste id&#39;s voor uw toepassing(en). Meer algemene richtlijnen voor het bepalen van welke id&#39;s u wilt verzenden naar [!DNL Privacy Service], zie het document op [identiteitsgegevens in privacyverzoeken](../identity-data.md).

De [!DNL Privacy Service] API ondersteunt twee soorten taakaanvragen voor persoonlijke gegevens:

* [Toegang en/of verwijderen](#access-delete): Persoonsgegevens openen (lezen) of verwijderen.
* [Uitschakelen](#opt-out): Persoonlijke gegevens markeren als niet te verkopen gegevens.

>[!IMPORTANT]
>
>Terwijl toegang en schrappingsverzoeken als één enkele API vraag kunnen worden gecombineerd, opt-out verzoeken moeten afzonderlijk worden gemaakt.

### Een toegangs-/verwijdertaak maken {#access-delete}

In deze sectie ziet u hoe u een aanvraag voor een toegangs-/verwijdertaak uitvoert met de API.

**API-indeling**

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
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `companyContexts` **(Vereist)** | Een array met verificatiegegevens voor uw organisatie. Elke weergegeven id bevat de volgende kenmerken: <ul><li>`namespace`: De naamruimte van een id.</li><li>`value`: De waarde van de id.</li></ul>Het is **vereist** dat een van de id&#39;s gebruikt `imsOrgId` als `namespace`, met `value` met de unieke id voor uw IMS-organisatie. <br/><br/>Aanvullende id&#39;s kunnen productspecifieke bedrijfsaanduidingen zijn (bijvoorbeeld `Campaign`), die een integratie met een toepassing van de Adobe van uw organisatie identificeren. Mogelijke waarden zijn accountnamen, clientcodes, gebruikers-id&#39;s of andere toepassings-id&#39;s. |
| `users` **(Vereist)** | Een array die een verzameling van ten minste één gebruiker bevat waarvan u de gegevens wilt openen of verwijderen. U kunt maximaal 1000 gebruikers-id&#39;s in één aanvraag opgeven. Elk gebruikersobject bevat de volgende informatie: <ul><li>`key`: Een id voor een gebruiker die wordt gebruikt om de afzonderlijke taak-id&#39;s in de reactiegegevens te kwalificeren. Het is aan te raden een unieke, gemakkelijk identificeerbare tekenreeks voor deze waarde te kiezen, zodat er later gemakkelijk naar kan worden verwezen of deze kan worden opgezocht.</li><li>`action`: Een array met de acties die moeten worden uitgevoerd op basis van de gegevens van de gebruiker. Afhankelijk van de handelingen die u wilt uitvoeren, moet deze array `access`, `delete`, of beide.</li><li>`userIDs`: Een verzameling identiteiten voor de gebruiker. Het aantal identiteiten dat één gebruiker kan hebben, is beperkt tot negen. Elke identiteit bestaat uit een `namespace`, `value`en een naamruimtekwalificatie (`type`). Zie de [aanhangsel](appendix.md) voor meer informatie over deze vereiste eigenschappen.</li></ul> Voor een meer gedetailleerde uitleg van `users` en `userIDs`, zie de [gids voor problemen](../troubleshooting-guide.md#user-ids). |
| `include` **(Vereist)** | Een array met Adobe-producten die in de verwerking moeten worden opgenomen. Als deze waarde ontbreekt of anderszins leeg is, wordt het verzoek afgewezen. Omvat slechts producten die uw organisatie een integratie met heeft. Zie de sectie over [aanvaarde productwaarden](appendix.md) in het aanhangsel voor meer informatie. |
| `expandIDs` | Een optionele eigenschap die, wanneer ingesteld op `true`, is een optimalisatie voor het verwerken van de id&#39;s in de toepassingen (momenteel alleen ondersteund door [!DNL Analytics]). Indien weggelaten, wordt deze waarde standaard ingesteld op `false`. |
| `priority` | An optional property used by Adobe Analytics that sets the priority for processing request. Accepteerde waarden zijn `normal` en `low`. Indien `priority` wordt weggelaten, is het standaardgedrag `normal`. |
| `analyticsDeleteMethod` | Een optionele eigenschap die aangeeft hoe Adobe Analytics de persoonlijke gegevens moet verwerken. Voor dit kenmerk worden twee mogelijke waarden geaccepteerd: <ul><li>`anonymize`: Alle gegevens waarnaar door de opgegeven verzameling gebruikers-id&#39;s wordt verwezen, worden anoniem gemaakt. Indien `analyticsDeleteMethod` wordt weggelaten, is dit het standaardgedrag.</li><li>`purge`: Alle gegevens worden volledig verwijderd.</li></ul> |
| `regulation` **(Vereist)** | De verordening voor de privacybaan. De volgende waarden worden geaccepteerd: <ul><li>`gdpr` (Europese Unie)</li><li>`ccpa` (Californië)</li><li>`lgpd_bra` (Brazilië)</li><li>`nzpa_nzl` (Nieuw-Zeeland)</li><li>`pdpa_tha` (Thailand)</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

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

{style=&quot;table-layout:auto&quot;}

Nadat de taakaanvraag is verzonden, kunt u verdergaan met de volgende stap van [de status van de taak controleren](#check-status).

## De status van een taak controleren {#check-status}

U kunt informatie over een specifieke taak ophalen, zoals de huidige verwerkingsstatus, door de betreffende taak op te nemen `jobId` op het pad van een verzoek van de GET aan de `/jobs` eindpunt.

>[!IMPORTANT]
>
>Gegevens voor eerder gemaakte taken kunnen alleen binnen 30 dagen na de einddatum van de taak worden opgehaald.

**API-indeling**

```http
GET /jobs/{JOB_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{JOB_ID}` | De id van de taak die u wilt opzoeken. Deze id is geretourneerd onder `jobId` in geslaagde API-reacties voor [een taak maken](#create-job) en [aanbieden, alle taken](#list). |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met het volgende verzoek worden de gegevens opgehaald van de taak waarvan `jobId` wordt opgegeven in het aanvraagpad.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwoord**

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
| `productStatusResponse` | Elk object in het dialoogvenster `productResponses` array bevat informatie over de huidige status van de taak ten opzichte van een specifieke [!DNL Experience Cloud] toepassing. |
| `productStatusResponse.status` | De huidige statuscategorie van de taak. Zie de onderstaande tabel voor een lijst met [beschikbare statuscategorieën](#status-categories) en hun overeenkomstige betekenis. |
| `productStatusResponse.message` | De specifieke status van de taak, die overeenkomt met de statuscategorie. |
| `productStatusResponse.responseMsgCode` | Een standaardcode voor productresponsberichten die worden ontvangen door [!DNL Privacy Service]. De details van het bericht worden verstrekt onder `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Een gedetailleerdere uitleg van de status van de baan. Berichten voor vergelijkbare statussen kunnen per product verschillen. |
| `productStatusResponse.results` | Voor bepaalde statussen kunnen sommige producten a `results` object dat aanvullende informatie biedt die niet wordt gedekt door `responseMsgDetail`. |
| `downloadURL` | Als de status van de taak `complete`, biedt dit kenmerk een URL om de taakresultaten te downloaden als een ZIP-bestand. Dit bestand kan 60 dagen nadat de taak is voltooid, worden gedownload. |

{style=&quot;table-layout:auto&quot;}

### Taakstatuscategorieën {#status-categories}

In de volgende tabel worden de verschillende mogelijke taakstatuscategorieën en de bijbehorende betekenis weergegeven:

| Statuscategorie | Betekenis |
| -------------- | -------- |
| `complete` | De taak is voltooid en (indien vereist) worden bestanden vanuit elke toepassing geüpload. |
| `processing` | Toepassingen hebben de taak erkend en worden momenteel verwerkt. |
| `submitted` | De taak wordt voorgelegd aan elke toepasselijke toepassing. |
| `error` | Er is iets misgegaan in de verwerking van de taak - er kan meer specifieke informatie worden verkregen door individuele taakdetails op te halen. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Een ingediende baan kan in een `processing` staat als het een afhankelijke kindbaan heeft die nog verwerkt.

## Volgende stappen

U weet nu hoe u met de [!DNL Privacy Service] API. Voor informatie over hoe te om de zelfde taken uit te voeren gebruikend het gebruikersinterface, zie [Overzicht van de gebruikersinterface voor Privacys Service](../ui/overview.md).
