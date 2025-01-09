---
title: Amazon Kinesis Source Connector - Overzicht
description: Leer hoe u Amazon Kinesis met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 84d09038ded1f35269ebf67c6bc1a5dacaafe4ac
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] bron

>[!IMPORTANT]
>
>- De [!DNL Amazon Kinesis] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time CDP Ultimate hebben aangeschaft.
>
>- U kunt nu de [!DNL Amazon Kinesis] -bron gebruiken wanneer u Adobe Experience Platform uitvoert op Amazon Web Services (AWS). Experience Platform dat op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van het Experience Platform leren, zie het [ Experience Platform multi-cloud overzicht ](../../../landing/multi-cloud.md).


Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform] en [!DNL Azure] . U kunt uw gegevens van deze systemen overbrengen naar [!DNL Platform] .

Met bronnen voor cloudopslag kunt u uw eigen gegevens overbrengen naar [!DNL Platform] zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema. Met [!DNL Platform] kunt u gegevens van [!DNL Amazon Kinesis] in real-time invoeren.

>[!NOTE]
>
>De schaalfactor voor [!DNL Kinesis] moet worden verhoogd als u gegevens met een hoog volume wilt invoeren. Het maximale gegevensvolume dat u van uw [!DNL Kinesis] -account naar Platform kunt verzenden, is momenteel 4000 records per seconde. Neem contact op met uw Adobe als u de schaal wilt verhogen en meer gegevens over het volume wilt invoeren.

## Vereisten

In de volgende sectie vindt u meer informatie over de vereiste configuratie voordat u een [!DNL Kinesis] bronverbinding kunt maken.

### Toegangsbeleid instellen

Een [!DNL Kinesis] -stream vereist de volgende machtigingen om een bronverbinding te maken:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Deze machtigingen worden gerangschikt via de [!DNL Kinesis] -console en worden gecontroleerd door Platform nadat u uw referenties hebt ingevoerd en uw gegevensstroom hebt geselecteerd.

In het onderstaande voorbeeld worden de minimale toegangsrechten weergegeven die vereist zijn om een [!DNL Kinesis] bronverbinding te maken.

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

Voor meer informatie bij het controleren van toegang voor [!DNL Kinesis] gegevensstromen, zie het volgende [[!DNL Kinesis]  document ](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Type iterator configureren

[!DNL Kinesis] ondersteunt de volgende iteratortypen waarmee u de volgorde kunt opgeven waarin de gegevens worden gelezen:

| Type iterator | Beschrijving |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | De gegevens worden gelezen vanaf een positie die wordt aangeduid met een specifiek volgnummer. |
| `AFTER_SEQUENCE_NUMBER` | De gegevens worden gelezen vanaf de positie die wordt bepaald door een specifiek volgnummer. |
| `AT_TIMESTAMP` | De gegevens worden gelezen vanaf een positie die wordt aangeduid met een specifiek tijdstempel. |
| `TRIM_HORIZON` | De gegevens worden gelezen vanaf de oudste gegevensrecord. |
| `LATEST` | De gegevens worden gelezen vanaf de meest recente gegevensrecord. |

Een [!DNL Kinesis] UI-bron ondersteunt momenteel alleen `TRIM_HORIZON` , terwijl de API zowel `TRIM_HORIZON` als `LATEST` as-modi ondersteunt om gegevens op te halen. De standaardwaarde voor de iterator die Platform gebruikt voor de [!DNL Kinesis] -bron is `TRIM_HORIZON` .

Voor meer informatie over iteratortypes, zie het volgende [[!DNL Kinesis]  document ](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Verbinden [!DNL Amazon Kinesis] met [!DNL Platform]

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Amazon Kinesis] en [!DNL Platform] via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een Amazon Kinesis-bronverbinding maken met de Flow Service API](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Streaming gegevens verzamelen met de Flow Service API](../../tutorials/api/collect/streaming.md)

### UI gebruiken

- [Een Amazon Kinesis-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Een gegevensstroom configureren voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
