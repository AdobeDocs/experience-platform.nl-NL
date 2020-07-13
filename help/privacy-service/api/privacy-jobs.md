---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Taken
topic: developer guide
translation-type: tm+mt
source-git-commit: df36d88de8ac117206d8d744cfcdd7804fcec61e
workflow-type: tm+mt
source-wordcount: '1807'
ht-degree: 0%

---


# Privacytaken

In dit document wordt beschreven hoe u met privacytaken werkt met API-aanroepen. Het gaat specifiek over het gebruik van het `/job` eindpunt in de Privacy Service-API. Voordat u deze handleiding leest, raadpleegt u de sectie [Aan de](./getting-started.md#getting-started) slag voor belangrijke informatie die u moet weten om oproepen naar de API met succes te kunnen uitvoeren, inclusief vereiste headers en hoe u API-voorbeeldaanroepen kunt lezen.

## Alle taken weergeven {#list}

U kunt een lijst van alle beschikbare privacybanen binnen uw organisatie bekijken door een GET verzoek aan het `/jobs` eindpunt te doen.

**API-indeling**

Dit verzoekformaat gebruikt een `regulation` vraagparameter op het `/jobs` eindpunt, daarom begint het met een vraagteken (`?`) zoals hieronder getoond. De reactie wordt gepagineerd, toestaand u om andere vraagparameters (`page` en `size`) te gebruiken om de reactie te filtreren. U kunt meerdere parameters scheiden met ampersands (`&`).

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Parameter | Beschrijving |
| --- | --- |
| `{REGULATION}` | Het regulatietype waarvoor u een query wilt uitvoeren. Accepteerde waarden zijn `gdpr`, `ccpa`en `pdpa_tha`. |
| `{PAGE}` | De pagina met gegevens die moet worden weergegeven met een op 0 gebaseerde nummering. De standaardwaarde is `0`. |
| `{SIZE}` | Het aantal resultaten dat op elke pagina moet worden weergegeven. De standaardwaarde is `1` en het maximum is `100`. Als het maximum wordt overschreden, retourneert de API een fout van 400 code. |

**Verzoek**

Met het volgende verzoek wordt een gepagineerde lijst opgehaald van alle taken binnen een IMS-organisatie, te beginnen bij de derde pagina met een paginaformaat van 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwoord**

Een succesvolle reactie retourneert een lijst met taken, waarbij elke taak details zoals de taak `jobId`bevat. In dit voorbeeld bevat het antwoord een lijst met 50 taken, te beginnen op de derde pagina met resultaten.

### Volgende pagina&#39;s openen

Om de volgende reeks resultaten in een gepagineerde reactie te halen, moet u een andere API vraag aan het zelfde eindpunt maken terwijl het verhogen van de `page` vraagparameter door 1.

## Een privacytaak maken {#create-job}

Voordat u een nieuwe taakaanvraag maakt, moet u eerst identificatiegegevens verzamelen over de betrokkenen van wie u de gegevens wilt benaderen, verwijderen of niet wilt verkopen. Zodra u de vereiste gegevens hebt, moet het in de lading van een verzoek van de POST aan het `/jobs` eindpunt worden verstrekt.

>[!NOTE]
>
>Compatibele Adobe Experience Cloud-toepassingen gebruiken verschillende waarden voor het identificeren van betrokkenen. Raadpleeg de handleiding over [Privacy Service- en Experience Cloud-toepassingen](../experience-cloud-apps.md) voor meer informatie over de vereiste id&#39;s voor uw toepassing(en). Zie het document over [identiteitsgegevens in privacyverzoeken](../identity-data.md)voor meer algemene informatie over het bepalen van welke id&#39;s u naar de Privacy Service wilt verzenden.

De Privacy Service-API ondersteunt twee soorten taakaanvragen voor persoonlijke gegevens:

* [Toegang tot en/of verwijdering](#access-delete): Persoonsgegevens openen (lezen) of verwijderen.
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
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
| `companyContexts` **(Vereist)** | Een array met verificatiegegevens voor uw organisatie. Elke weergegeven id bevat de volgende kenmerken: <ul><li>`namespace`: De naamruimte van een id.</li><li>`value`: De waarde van de id.</li></ul>Het is **vereist** dat een van de id&#39;s `imsOrgId` als zijn `namespace`id gebruikt, met de unieke id `value` voor uw IMS-organisatie. <br/><br/>Aanvullende id&#39;s kunnen productspecifieke bedrijfsaanduidingen zijn (bijvoorbeeld `Campaign`) waarmee een integratie met een Adobe-toepassing van uw organisatie wordt aangegeven. Mogelijke waarden zijn accountnamen, clientcodes, gebruikers-id&#39;s of andere toepassings-id&#39;s. |
| `users` **(Vereist)** | Een array die een verzameling van ten minste één gebruiker bevat waarvan u de gegevens wilt openen of verwijderen. U kunt maximaal 1000 gebruikers-id&#39;s in één aanvraag opgeven. Elk gebruikersobject bevat de volgende informatie: <ul><li>`key`: Een id voor een gebruiker die wordt gebruikt om de afzonderlijke taak-id&#39;s in de reactiegegevens te kwalificeren. Het is aan te raden een unieke, gemakkelijk identificeerbare tekenreeks voor deze waarde te kiezen, zodat er later gemakkelijk naar kan worden verwezen of deze kan worden opgezocht.</li><li>`action`: Een array met de acties die moeten worden uitgevoerd op basis van de gegevens van de gebruiker. Afhankelijk van de handelingen die u wilt uitvoeren, moet deze array `access`, `delete`of beide bevatten.</li><li>`userIDs`: Een verzameling identiteiten voor de gebruiker. Het aantal identiteiten dat één gebruiker kan hebben, is beperkt tot negen. Elke identiteit bestaat uit een `namespace`, een `value`en een naamruimtekwalificatie (`type`). Zie de [bijlage](appendix.md) voor meer informatie over deze vereiste eigenschappen.</li></ul> Voor een meer gedetailleerde verklaring van `users` en `userIDs`, zie de [het oplossen van problemengids](../troubleshooting-guide.md#user-ids). |
| `include` **(Vereist)** | Een array met Adobe-producten die u wilt opnemen in de verwerking. Als deze waarde ontbreekt of anderszins leeg is, wordt het verzoek afgewezen. Omvat slechts producten die uw organisatie een integratie met heeft. Zie de paragraaf over [aanvaarde productwaarden](appendix.md) in de bijlage voor meer informatie. |
| `expandIDs` | Een optionele eigenschap die, wanneer ingesteld op `true`, een optimalisatie vertegenwoordigt voor het verwerken van de id&#39;s in de toepassingen (momenteel alleen ondersteund door Analytics). Als deze waarde wordt weggelaten, wordt deze standaard ingesteld op `false`. |
| `priority` | Een optionele eigenschap die wordt gebruikt door Adobe Analytics en die de prioriteit voor het verwerken van aanvragen instelt. Accepteerde waarden zijn `normal` en `low`. Als `priority` wordt weggelaten, is het standaardgedrag `normal`. |
| `analyticsDeleteMethod` | Een optionele eigenschap die aangeeft hoe Adobe Analytics de persoonlijke gegevens moet verwerken. Voor dit kenmerk worden twee mogelijke waarden geaccepteerd: <ul><li>`anonymize`: Alle gegevens waarnaar door de opgegeven verzameling gebruikers-id&#39;s wordt verwezen, worden anoniem gemaakt. Als `analyticsDeleteMethod` wordt weggelaten, is dit het standaardgedrag.</li><li>`purge`: Alle gegevens worden volledig verwijderd.</li></ul> |
| `regulation` **(Vereist)** | De verordening voor het verzoek. Moet een van de volgende drie waarden zijn: <ul><li>gdpr</li><li>ccpa</li><li>pdpa_tha</li></ul> |

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

Nadat de taakaanvraag is verzonden, kunt u doorgaan naar de volgende stap voor het [controleren van de status](#check-status)van de taak.

### Een opt-out-of-sales-taak maken {#opt-out}

In deze sectie wordt getoond hoe u met de API een aanvraag voor een opt-out-taak kunt uitvoeren.

**API-indeling**

```http
POST /jobs
```

**Verzoek**

Het volgende verzoek leidt tot een nieuw baanverzoek, dat door de attributen wordt gevormd die in de nuttige lading worden geleverd zoals hieronder beschreven.

```shell
curl -X POST \
  https://platform.adobe.io/data/privacy/gdpr/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["opt-out-of-sale"],
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
        "action": ["opt-out-of-sale"],
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
| `companyContexts` **(Vereist)** | Een array met verificatiegegevens voor uw organisatie. Elke weergegeven id bevat de volgende kenmerken: <ul><li>`namespace`: De naamruimte van een id.</li><li>`value`: De waarde van de id.</li></ul>Het is **vereist** dat een van de id&#39;s `imsOrgId` als zijn `namespace`id gebruikt, met de unieke id `value` voor uw IMS-organisatie. <br/><br/>Aanvullende id&#39;s kunnen productspecifieke bedrijfsaanduidingen zijn (bijvoorbeeld `Campaign`) waarmee een integratie met een Adobe-toepassing van uw organisatie wordt aangegeven. Mogelijke waarden zijn accountnamen, clientcodes, gebruikers-id&#39;s of andere toepassings-id&#39;s. |
| `users` **(Vereist)** | Een array die een verzameling van ten minste één gebruiker bevat waarvan u de gegevens wilt openen of verwijderen. U kunt maximaal 1000 gebruikers-id&#39;s in één aanvraag opgeven. Elk gebruikersobject bevat de volgende informatie: <ul><li>`key`: Een id voor een gebruiker die wordt gebruikt om de afzonderlijke taak-id&#39;s in de reactiegegevens te kwalificeren. Het is aan te raden een unieke, gemakkelijk identificeerbare tekenreeks voor deze waarde te kiezen, zodat er later gemakkelijk naar kan worden verwezen of deze kan worden opgezocht.</li><li>`action`: Een array met de acties die u wilt uitvoeren. Voor optieout-of-sale verzoeken, moet de serie slechts de waarde bevatten `opt-out-of-sale`.</li><li>`userIDs`: Een verzameling identiteiten voor de gebruiker. Het aantal identiteiten dat één gebruiker kan hebben, is beperkt tot negen. Elke identiteit bestaat uit een `namespace`, een `value`en een naamruimtekwalificatie (`type`). Zie de [bijlage](appendix.md) voor meer informatie over deze vereiste eigenschappen.</li></ul> Voor een meer gedetailleerde verklaring van `users` en `userIDs`, zie de [het oplossen van problemengids](../troubleshooting-guide.md#user-ids). |
| `include` **(Vereist)** | Een array met Adobe-producten die u wilt opnemen in de verwerking. Als deze waarde ontbreekt of anderszins leeg is, wordt het verzoek afgewezen. Omvat slechts producten die uw organisatie een integratie met heeft. Zie de paragraaf over [aanvaarde productwaarden](appendix.md) in de bijlage voor meer informatie. |
| `expandIDs` | Een optionele eigenschap die, wanneer ingesteld op `true`, een optimalisatie vertegenwoordigt voor het verwerken van de id&#39;s in de toepassingen (momenteel alleen ondersteund door Analytics). Als deze waarde wordt weggelaten, wordt deze standaard ingesteld op `false`. |
| `priority` | Een optionele eigenschap die wordt gebruikt door Adobe Analytics en die de prioriteit voor het verwerken van aanvragen instelt. Accepteerde waarden zijn `normal` en `low`. Als `priority` wordt weggelaten, is het standaardgedrag `normal`. |
| `analyticsDeleteMethod` | Een optionele eigenschap die aangeeft hoe Adobe Analytics de persoonlijke gegevens moet verwerken. Voor dit kenmerk worden twee mogelijke waarden geaccepteerd: <ul><li>`anonymize`: Alle gegevens waarnaar door de opgegeven verzameling gebruikers-id&#39;s wordt verwezen, worden anoniem gemaakt. Als `analyticsDeleteMethod` wordt weggelaten, is dit het standaardgedrag.</li><li>`purge`: Alle gegevens worden volledig verwijderd.</li></ul> |
| `regulation` **(Vereist)** | De verordening voor het verzoek. Moet een van de volgende drie waarden zijn: <ul><li>gdpr</li><li>ccpa</li><li>pdpa_tha</li></ul> |

**Antwoord**

Een succesvol antwoord geeft de details van de nieuwe banen terug.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd9vjs0",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bes0ewj2",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 2
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `jobId` | Een alleen-lezen, unieke door het systeem gegenereerde id voor een taak. Deze waarde wordt gebruikt om een specifieke taak op te zoeken in de volgende stap. |

Nadat de taakaanvraag is verzonden, kunt u doorgaan naar de volgende stap om de status van de taak te controleren.

## De status van een taak controleren {#check-status}

U kunt informatie over een specifieke baan, zoals zijn huidige verwerkingsstatus terugwinnen, door die baan `jobId` in de weg van een GET verzoek aan het `/jobs` eindpunt te omvatten.

>[!IMPORTANT]
>
>Gegevens voor eerder gemaakte taken kunnen alleen binnen 30 dagen na de einddatum van de taak worden opgehaald.

**API-indeling**

```http
GET /jobs/{JOB_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{JOB_ID}` | De id van de taak die u wilt opzoeken. Deze id wordt geretourneerd onder `jobId` succesvolle API-reacties voor het [maken van een taak](#create-job) en het [weergeven van alle taken](#list). |

**Verzoek**

Het volgende verzoek haalt de details van de baan terug waarvan in de verzoekweg `jobId` wordt verstrekt.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
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
| `productStatusResponse` | Elk object in de `productResponses` array bevat informatie over de huidige status van de taak ten opzichte van een specifieke [!DNL Experience Cloud] toepassing. |
| `productStatusResponse.status` | De huidige statuscategorie van de taak. Zie de onderstaande tabel voor een lijst met [beschikbare statuscategorieën](#status-categories) en de bijbehorende betekenissen. |
| `productStatusResponse.message` | De specifieke status van de taak, die overeenkomt met de statuscategorie. |
| `productStatusResponse.responseMsgCode` | Een standaardcode voor de berichten van de productreactie die door Privacy Service worden ontvangen. De details van het bericht worden onder verstrekt `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Een gedetailleerdere uitleg van de status van de baan. Berichten voor vergelijkbare statussen kunnen per product verschillen. |
| `productStatusResponse.results` | Voor bepaalde statussen kunnen sommige producten een `results` object retourneren dat aanvullende informatie biedt die niet door `responseMsgDetail`de status wordt gedekt. |
| `downloadURL` | Als de status van de taak `complete`is, verschaft dit kenmerk een URL waarmee de taakresultaten als een ZIP-bestand kunnen worden gedownload. Dit bestand kan 60 dagen nadat de taak is voltooid, worden gedownload. |

### Taakstatuscategorieën {#status-categories}

In de volgende tabel worden de verschillende mogelijke taakstatuscategorieën en de bijbehorende betekenis weergegeven:

| Statuscategorie | Betekenis |
| -------------- | -------- |
| Voltooid | De taak is voltooid en (indien vereist) worden bestanden vanuit elke toepassing geüpload. |
| Verwerking | Toepassingen hebben de taak erkend en worden momenteel verwerkt. |
| Verzonden | De taak wordt voorgelegd aan elke toepasselijke toepassing. |
| Fout | Er is iets misgegaan in de verwerking van de taak - er kan meer specifieke informatie worden verkregen door individuele taakdetails op te halen. |

>[!NOTE]
>
>Een voorgelegde baan kan in een verwerkingsstaat blijven als het een afhankelijke kindbaan heeft die nog wordt verwerkt.

## Volgende stappen

U weet nu hoe u privacytaken kunt maken en controleren met de Privacy Service-API. Voor informatie over hoe te om de zelfde taken uit te voeren gebruikend het gebruikersinterface, zie het overzicht [van de](../ui/overview.md)Privacy Service UI.
