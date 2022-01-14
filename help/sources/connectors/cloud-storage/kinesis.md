---
keywords: Experience Platform;home;populaire onderwerpen;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Amazon Kinesis Source Connector - overzicht
topic-legacy: overview
description: Leer hoe u Amazon Kinesis met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 5f4355a9d3ef39ee63581fc70dbf0f6e7d674814
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] connector

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform], en [!DNL Azure]. U kunt uw gegevens van deze systemen overbrengen naar [!DNL Platform].

Opslagbronnen in de cloud kunnen uw eigen gegevens overbrengen naar [!DNL Platform] zonder dat het downloaden, opmaken of uploaden nodig is. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema. [!DNL Platform] stelt u in staat gegevens over te brengen van [!DNL Amazon Kinesis] in real time.

>[!NOTE]
>
>De schaalfactor voor [!DNL Kinesis] moet worden verhoogd als u gegevens met een hoog volume moet innemen. Het maximale gegevensvolume dat u van uw [!DNL Kinesis] het account voor Platform is 4000 records per seconde. Neem contact op met uw Adobe als u de schaal wilt verhogen en meer gegevens over het volume wilt invoeren.

## Vereisten

In het volgende gedeelte vindt u meer informatie over de vereiste configuratie voordat u een [!DNL Kinesis] bronverbinding.

### Toegangsbeleid instellen

A [!DNL Kinesis] voor het maken van een bronverbinding zijn de volgende machtigingen vereist:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Deze machtigingen worden gerangschikt via de [!DNL Kinesis] -console en worden door het Platform gecontroleerd zodra u uw referenties hebt ingevoerd en uw gegevensstroom hebt geselecteerd.

In het onderstaande voorbeeld worden de minimale toegangsrechten weergegeven die vereist zijn om een [!DNL Kinesis] bronverbinding.

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

Voor meer informatie over het beheren van toegang voor [!DNL Kinesis] gegevensstromen, zie het volgende [[!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Type iterator configureren

[!DNL Kinesis] De volgende iteratortypen worden ondersteund, zodat u de volgorde kunt opgeven waarin de gegevens worden gelezen:

| Type iterator | Beschrijving |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | De gegevens worden gelezen vanaf een positie die wordt aangeduid met een specifiek volgnummer. |
| `AFTER_SEQUENCE_NUMBER` | De gegevens worden gelezen vanaf de positie die wordt bepaald door een specifiek volgnummer. |
| `AT_TIMESTAMP` | De gegevens worden gelezen vanaf een positie die wordt aangeduid met een specifiek tijdstempel. |
| `TRIM_HORIZON` | De gegevens worden gelezen vanaf de oudste gegevensrecord. |
| `LATEST` | De gegevens worden gelezen vanaf de meest recente gegevensrecord. |

A [!DNL Kinesis] UI-bron momenteel alleen ondersteund `TRIM_HORIZON`, terwijl de API beide ondersteunt `TRIM_HORIZON` en `LATEST` als modi om gegevens op te halen. De standaarditeratorwaarde die door het Platform wordt gebruikt voor de [!DNL Kinesis] bron is `TRIM_HORIZON`.

Raadpleeg de volgende secties voor meer informatie over iteratortypen [[!DNL Kinesis] document](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Verbinden [!DNL Amazon Kinesis] tot [!DNL Platform]

In de onderstaande documentatie vindt u informatie over het maken van een verbinding [!DNL Amazon Kinesis] tot [!DNL Platform] API&#39;s of de gebruikersinterface gebruiken:

### API&#39;s gebruiken

- [Een Amazon Kinesis-bronverbinding maken met de Flow Service API](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Streaming gegevens verzamelen met de Flow Service API](../../tutorials/api/collect/streaming.md)

### De gebruikersinterface gebruiken

- [Een Amazon Kinesis-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Een gegevensstroom configureren voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
