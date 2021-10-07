---
keywords: Experience Platform;home;populaire onderwerpen;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Amazon Kinesis Source Connector - overzicht
topic-legacy: overview
description: Leer hoe u Amazon Kinesis met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 481f72c5c630f6dbcbbfd3eee11c91787e780f3f
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] connector

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform] en [!DNL Azure]. U kunt uw gegevens van deze systemen naar [!DNL Platform] brengen.

Opslagbronnen in de cloud kunnen uw eigen gegevens naar [!DNL Platform] brengen zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema. [!DNL Platform] kunt u gegevens  [!DNL Amazon Kinesis] in real-time invoeren.

## Vereisten

In de volgende sectie vindt u meer informatie over de vereiste configuratie voordat u een [!DNL Kinesis]-bronverbinding kunt maken.

### Toegangsbeleid instellen

Een [!DNL Kinesis] stroom vereist de volgende toestemmingen om een bronverbinding tot stand te brengen:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Deze toestemmingen worden geschikt door de [!DNL Kinesis] console en door Platform gecontroleerd zodra u uw geloofsbrieven ingaat en uw gegevensstroom selecteert.

In het onderstaande voorbeeld worden de minimale toegangsrechten weergegeven die vereist zijn om een [!DNL Kinesis]-bronverbinding te maken.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:GetShardIterator",
                "kinesis:GetRecords",
                "kinesis:DescribeStream",
                "kinesis:ListStreams"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `kinesis:GetShardIterator` | Een handeling die is vereist om records te doorlopen. |
| `kinesis:GetRecords` | Een handeling die is vereist om records op te halen van een specifieke offset- of gedeelde id. |
| `kinesis:DescribeStream` | Een actie die informatie betreffende de stroom met inbegrip van de kaart terugkeert, die nodig is om een gedeelde identiteitskaart te produceren. |
| `kinesis:ListStreams` | Een handeling die is vereist om beschikbare streams weer te geven die u kunt selecteren in de gebruikersinterface. |

Raadpleeg het volgende [[!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html) voor meer informatie over het beheren van toegang voor [!DNL Kinesis] gegevensstromen.

### Type iterator configureren

[!DNL Kinesis] De volgende iteratortypen worden ondersteund, zodat u de volgorde kunt opgeven waarin de gegevens worden gelezen:

| Type iterator | Beschrijving |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | De gegevens worden gelezen vanaf een positie die wordt aangeduid met een specifiek volgnummer. |
| `AFTER_SEQUENCE_NUMBER` | De gegevens worden gelezen vanaf de positie die wordt bepaald door een specifiek volgnummer. |
| `AT_TIMESTAMP` | De gegevens worden gelezen vanaf een positie die wordt aangeduid met een specifiek tijdstempel. |
| `TRIM_HORIZON` | De gegevens worden gelezen vanaf de oudste gegevensrecord. |
| `LATEST` | De gegevens worden gelezen vanaf de meest recente gegevensrecord. |

Een [!DNL Kinesis] UI-bron ondersteunt momenteel alleen `TRIM_HORIZON`, terwijl de API zowel `TRIM_HORIZON` als `LATEST` ondersteunt als modi om gegevens op te halen. De standaardwaarde voor de iterator die Platform gebruikt voor de bron [!DNL Kinesis] is `TRIM_HORIZON`.

Zie het volgende [[!DNL Kinesis] document](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax) voor meer informatie over iteratortypen.

## [!DNL Amazon Kinesis] verbinden met [!DNL Platform]

In de onderstaande documentatie vindt u informatie over hoe u [!DNL Amazon Kinesis] kunt verbinden met [!DNL Platform] via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een Amazon Kinesis-bronverbinding maken met de Flow Service API](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Streaming gegevens verzamelen met de Flow Service API](../../tutorials/api/collect/streaming.md)

### De gebruikersinterface gebruiken

- [Een Amazon Kinesis-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Een gegevensstroom configureren voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
