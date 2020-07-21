---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Amazon Kinesis-connector
topic: overview
translation-type: tm+mt
source-git-commit: 340f5d0611e9e9eb4676018ee10c8a8aa08dbb2d
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# (Beta) [!DNL Amazon Kinesis] -connector

>[!NOTE]
>De [!DNL Amazon Kinesis] connector is in bèta. Zie het [Bronoverzicht](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform]en [!DNL Azure]. U kunt uw gegevens van deze systemen in brengen [!DNL Platform].

Met bronnen voor cloudopslag kunt u uw eigen gegevens overbrengen [!DNL Platform] zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema. [!DNL Platform] kunt u gegevens in real-time [!DNL Amazon Kinesis] inbrengen.

## IP adres lijst van gewenste personen

De volgende IP adressen moeten aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen.

### Oost-Amerikaanse regio

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### West-Europa

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australië - oost

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

In de onderstaande documentatie vindt u informatie over het maken van een verbinding [!DNL Amazon Kinesis] [!DNL Platform] met API&#39;s of de gebruikersinterface:

## Verbinding maken [!DNL Amazon Kinesis] met API&#39; [!DNL Platform] s

- [Een Amazon Kinesis-connector maken met de Flow Service API](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Een systeem voor cloudopslag verkennen met de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Gegevens voor cloudopslag verzamelen met de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

## Verbinding maken [!DNL Amazon Kinesis] met [!DNL Platform] de gebruikersinterface

- [Een Amazon Kinesis-bronconnector maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Een gegevensstroom configureren voor een aansluiting voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/streaming/cloud-storage.md)