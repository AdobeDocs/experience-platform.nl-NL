---
keywords: Experience Platform;home;popular topics; notifications
description: Met de Adobe I/O Events kunt u zich abonneren op gebeurtenissen en websites gebruiken om meldingen te ontvangen over de status van uw flowuitvoering. Deze berichten bevatten informatie over het succes van uw stroom of fouten die tot de mislukking van een looppas hebben bijgedragen.
solution: Experience Platform
title: Meldingen voor stroomuitvoering
topic: overview
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---


# Meldingen voor stroomuitvoering

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van [!DNL Platform] services. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

[[!DNL Adobe Experience Platform Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) wordt gebruikt om klantgegevens van diverse verschillende bronnen binnen te verzamelen en te centraliseren [!DNL Platform]. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Met Adobe I/O Events kunt u zich abonneren op gebeurtenissen en websites gebruiken om meldingen te ontvangen over de status van uw flowuitvoering. Deze berichten bevatten informatie over het succes van uw stroom of fouten die tot de mislukking van een looppas hebben bijgedragen.

In dit document worden stappen beschreven voor het abonneren op gebeurtenissen, het registreren van websites en het ontvangen van meldingen met informatie over de status van uw flowuitvoering.

## Aan de slag

In deze zelfstudie wordt ervan uitgegaan dat u al ten minste één bronverbinding hebt gemaakt waarvan u de stroom wilt controleren. Als u nog geen bronverbinding hebt gevormd, begin door het [bronoverzicht](./home.md) te bezoeken om de bron van uw keus te vormen alvorens aan deze gids terug te keren.

Dit document vereist ook een goed begrip van webhaken en hoe te om een webhaak van één toepassing aan een andere aan te sluiten. Raadpleeg de [[!DNL I/O Events] documentatie](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) voor een inleiding op websites.

## Webhaak registreren voor meldingen bij uitvoering van stroom

Als u meldingen over flowuitvoering wilt ontvangen, moet u Adobe Developer Console gebruiken om een webhaak voor uw [!DNL Experience Platform] integratie te registreren.

Volg de zelfstudie over het [abonneren van [!DNL I/O Event] toonmeldingen](../observability/notifications/subscribe.md) voor gedetailleerde stappen over hoe u dit kunt doen.

>[!IMPORTANT]
>
>Zorg er tijdens het abonnementsproces voor dat u **[!UICONTROL Platform-berichten]** als gebeurtenisprovider selecteert en selecteer de volgende abonnementen voor gebeurtenissen:
>
>* **[!UICONTROL Experience Platform Source&#39;s Flow Run geslaagd]**
>* **[!UICONTROL Doorloop van bron van Experience Platform is mislukt]**


## Meldingen ontvangen voor uitvoering van flow

Als uw webhaak is aangesloten en uw gebeurtenisabonnement is voltooid, kunt u meldingen over doorloop ontvangen via het dashboard van de webhaak.

Een melding retourneert informatie zoals het aantal taken dat wordt uitgevoerd, de bestandsgrootte en fouten. Een bericht keert ook een lading terug verbonden aan uw stroom in formaat JSON in werking stelt. De antwoordlading kan als `sources_flow_run_success` of `sources_flow_run_failure`worden geclassificeerd.

>[!IMPORTANT]
>
>Als gedeeltelijke ingestie tijdens het proces van de stroomverwezenlijking wordt toegelaten, zal een stroom die zowel succesvolle als ontbroken ingesties bevat `sources_flow_run_success` slechts worden gemerkt als het aantal fouten onder het foutendrempelpercentage is dat tijdens het proces van de stroomverwezenlijking wordt geplaatst. Als een geslaagde flowuitvoering fouten bevat, worden deze fouten nog steeds opgenomen in de geretourneerde lading.

### Succes

Een succesvolle reactie keert een reeks terug van `metrics` die eigenschappen van een specifieke stroomlooppas en `activities` die overzicht bepalen hoe het gegeven wordt getransformeerd.

```json
{
  "event_id": "aec55616-1715-487f-8044-ba648cc8ffee",
  "event": {
    "createdAt": 1597213529158,
    "updatedAt": 1597213530760,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "7127a4f0-def8-11e9-83ce-e79494b1c2a5",
    "sandboxName": "prod",
    "imsOrgId": "{IMS_ORG}",
    "id": "933cf9f4-cf01-4d75-bcf9-f4cf010d750a",
    "flowId": "1c6f1047-dcaf-48fe-af10-47dcaf08feaf",
    "providerRefId": "test1234",
    "etag": "\"5100ec97-0000-0200-0000-5f338b5b0000\"",
    "metrics": {
      "durationSummary": {
        "startedAtUTC": 1590512053,
        "completedAtUTC": 1590512053
      },
      "sizeSummary": {
        "inputBytes": 2048,
        "outputBytes": 1024
      },
      "recordSummary": {
        "inputRecordCount": 100,
        "outputRecordCount": 70
      },
      "fileSummary": {
        "inputFileCount": 10,
        "outputFileCount": 10
      },
      "statusSummary": {
        "status": "success"
      }
    },
    "activities": [
      {
        "id": "copyActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "startedAtUTC": 1590512053,
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 2048,
          "outputBytes": 1098
        },
        "recordSummary": {
          "inputRecordCount": 100,
          "outputRecordCount": 100
        },
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "adf/pipeline/id": "abcd",
            "adf/run/id": "1234"
          }
        },
        "sourceInfo": [
          {
            "id": "sourceConnectionId1",
            "type": "SourceConnection",
            "reference": {
              "type": "AdfRunId"
            }
          }
        ]
      },
      {
        "id": "promotionActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 1098,
          "outputBytes": 1024
        },
        "recordSummary": {},
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10,
          "extensions": {
            "manifest": {
              "fileInfo": "https://platform-int.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
            }
          }
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "batchId": "b1",
            "acp_request_id": "1234"
          }
        },
        "targetInfo": [
          {
            "id": "targetConnectionId1",
            "type": "TargetConnection",
            "reference": {
              "type": "batch"
            }
          }
        ]
      }
    ],
    "slaCreatedAt": 1597213531124,
    "processStartTime": 1597213531213,
    "header": {
      "_adobeio": {
        "imsOrgId": "{IMS_ORG}",
        "providerMetadata": "platform_notifications",
        "eventCode": "sources_flow_run_success"
      }
    },
    "transformedTime": 1597213531214
  }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `metrics` | Bepaalt kenmerken van de gegevens in de stroomlooppas. |
| `activities` | Hiermee definieert u de verschillende stappen en activiteiten die worden uitgevoerd om de gegevens te transformeren. |
| `durationSummary` | Definieert de begin- en eindtijd van de flowuitvoering. |
| `sizeSummary` | Definieert het volume van de gegevens in bytes. |
| `recordSummary` | Hiermee definieert u het recordaantal van de gegevens. |
| `fileSummary` | Hiermee definieert u het aantal bestanden van de gegevens. |
| `fileInfo` | Een URL die leidt tot een overzicht van de met succes opgenomen bestanden. |
| `statusSummary` | Bepaalt of de stroomlooppas een succes of een mislukking is. |

### Mislukt

De volgende reactie is een voorbeeld van een mislukte stroomuitvoering, waarbij een fout optreedt wanneer de gekopieerde gegevens worden verwerkt. Fouten kunnen ook optreden tijdens het kopiëren van gegevens uit de bron. Een mislukte stroomrun bevat informatie over de fouten die hebben bijgedragen aan de fout van de uitvoering, inclusief de fout en beschrijving ervan.

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{IMS_ORG}",
        "schema": {
          "name": "run-notification",
          "version": "1.0"
        },
        "provider": "FlowService",
        "_eventNotificationMeta": {
          "category": "Platform Notifications",
          "type": "sources_flow_run_failed"
        },
        "value": {
          "createdAt": 1597434147259,
          "updatedAt": 1597434157567,
          "createdBy": "{CREATED_BY}",
          "updatedBy": "{UPDATED_BY}",
          "createdClient": "{CREATED_CLIENT}",
          "updatedClient": "{UPDATED_CLIENT}",
          "sandboxId": "e49ebb00-d0fa-11e9-b164-ed6a398c8b35",
          "sandboxName": "prod",
          "imsOrgId": "{IMS_ORG}",
          "id": "d9024c32-2174-4271-824c-322174627101",
          "flowId": "cf4fce79-8822-456d-8fce-798822556dc6",
          "etag": "\"0c003dbf-0000-0200-0000-5f36e92d0000\"",
          "metrics": {
            "durationSummary": {
              "startedAtUTC": 1597434147190
            },
            "sizeSummary": {
              "inputBytes": -1
            },
            "fileSummary": {
              "inputFileCount": -1
            },
            "statusSummary": {
              "status": "failed",
              "errors": [
                {
                  "code": "CONNECTOR-2001-500",
                  "message": "Error in processing (parsing, validation or transformation) the copied data."
                }
              ]
            }
          },
          "activities": [
            {
              "id": "promotionActivity",
              "updatedAtUTC": 1597434157529,
              "durationSummary": {
                "startedAtUTC": 1597434147190,
                "completedAtUTC": 1597434157212
              },
              "sizeSummary": {
                "inputBytes": -1
              },
              "recordSummary": {},
              "fileSummary": {
                "inputFileCount": -1,
                "extensions": {
                  "manifest": {
                    "fileInfo": "https://platform-stage.adobe.io/data/foundation/export/batches/6f6a900f-e40d-4f0e-9bb9-b614436c3465/meta?path=input_files"
                  }
                }
              },
              "statusSummary": {
                "status": "failed",
                "errors": [
                  {
                    "code": "CONNECTOR-2001-500",
                    "message": "Error in processing (parsing, validation or transformation) the copied data."
                  }
                ],
                "extensions": {
                  "errors": [
                    {
                      "code": "133",
                      "message": "We are unable to locate any files uploaded for this batch. Please upload files to ingest."
                    }
                  ]
                }
              },
              "targetInfo": [
                {
                  "id": "e88737aa-27b8-4795-8737-aa27b8f7959e",
                  "type": "TargetConnection",
                  "reference": {
                    "type": "Batch",
                    "ids": [
                      "6f6a900f-e40d-4f0e-9bb9-b614436c3465"
                    ]
                  }
                }
              ]
            }
          ]
        }
      }
    ]
  }
]
```

| Eigenschap | Beschrijving |
| ---------- | ----------- |
| `fileInfo` | Een URL die leidt tot een overzicht van de dossiers die met succes en zonder succes werden opgenomen. |

>[!NOTE]
>
>Zie de [bijlage](#errors) voor meer informatie over foutenmeldingen.

## Volgende stappen

U kunt nu een abonnement nemen op gebeurtenissen waarmee u realtime meldingen kunt ontvangen over de status van uw flowuitvoering. Voor meer informatie over stroomlooppas en bronnen, zie het [bronoverzicht](./home.md).

## Aanhangsel

De volgende secties verstrekken extra informatie voor het werken met de berichten van de stroomlooppas.

### Foutberichten begrijpen {#errors}

Er kunnen inslikingsfouten optreden wanneer gegevens van de bron worden gekopieerd of wanneer de gekopieerde gegevens naar [!DNL Platform]de bron worden verwerkt. Zie de onderstaande tabel voor meer informatie over specifieke fouten.

| Fout | Beschrijving |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Er is een fout opgetreden tijdens het kopiëren van gegevens uit een bron. |
| `CONNECTOR-2001-500` | Er is een fout opgetreden tijdens het verwerken van gekopieerde gegevens naar [!DNL Platform]. Deze fout kan betrekking hebben op parseren, valideren of transformeren. |