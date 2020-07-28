---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zelfstudies voor gegevensinsluiting
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---


# Gegevens verzamelen in [!DNL Experience Platform]

Adobe Experience Platform brengt gegevens uit meerdere bronnen samen, zodat marketers het gedrag van hun klanten beter kunnen begrijpen. Adobe vertegenwoordigt de veelvoudige methodes waardoor gegevens uit deze bronnen [!DNL Experience Platform Data Ingestion] opnemen, evenals hoe die gegevens binnen het meer van Gegevens voor gebruik door stroomafwaartse [!DNL Platform] [!DNL Platform services]. [!DNL Data Ingestion] omvat batch-opname, streaming opname en inname via bronconnectors. Meer leren, lees het overzicht [van de Ingestie van](../ingestion/home.md) Gegevens of ga direct aan de [Brondocumentatie](../sources/home.md)te werk.

## Een bronaansluiting maken in de gebruikersinterface en de API

De bron schakelaars staan u toe om gegevens van veelvoudige bronnen in te voeren, waar het dan kan worden geëtiketteerd, gestructureerd, en het verbeterde gebruiken [!DNL Platform services]. Beginnen creërend een bronschakelaar, zie het [bronoverzicht](../sources/home.md).

## Gegevens van groep samenvoegen

Met Adobe Experience Platform kunt u gegevens gemakkelijk importeren in [!DNL Platform] de vorm van batchbestanden. Voorbeelden van gegevens die moeten worden opgenomen, kunnen profielgegevens bevatten van een plat bestand in een CRM-systeem (zoals een parketbestand) of gegevens die in overeenstemming zijn met een bekend [!DNL Experience Data Model] (XDM) schema in de Schemaregistratie. Ga om te beginnen naar de [innamegegevens in de zelfstudie](../ingestion/tutorials/ingest-batch-data.md)Platform.

## Een CSV-bestand toewijzen aan een XDM-schema

Om CSV-gegevens in Adobe Experience Platform in te voeren, moeten de gegevens worden toegewezen aan een [!DNL Experience Data Model] (XDM) schema. Voor stappen die tonen hoe te om een Csv- dossier aan een schema toe te wijzen XDM gebruikend het [!DNL Experience Platform] gebruikersinterface, volg de [kaart een Csv- dossier aan een XDM schemazelfstudie](../ingestion/tutorials/map-a-csv-file.md).

## Een streamingverbinding maken

Wanneer u wilt beginnen met streamen van gegevens, moet u eerst een HTTP-eindpunt aanvragen. [!DNL Experience Platform] U hebt de optie om dit eindpunt te vormen om voor authentiek verklaard gedrag af te dwingen. Dit kan worden gedaan gebruikend het [!DNL Platform] gebruikersinterface of [!DNL Experience Platform] APIs. Voor meer informatie volgt u de zelfstudies voor het [maken van een streamingverbinding met de gebruikersinterface](../ingestion/tutorials/create-streaming-connection-ui.md) of het [maken van een streamingverbinding met API&#39;s](../ingestion/tutorials/create-streaming-connection.md).

## Een geverifieerde streamingverbinding maken

De voor authentiek verklaarde Inzameling van Gegevens staat de diensten van het Adobe Experience Platform, zoals [!DNL Real-time Customer Profile] en [!DNL Identity], toe om tussen verslagen te onderscheiden die uit vertrouwde op bronnen en onbetrouwbare bronnen komen. Volg de zelfstudie voor het [maken van een geverifieerde streamingverbinding](../ingestion/tutorials/create-authenticated-streaming-connection.md)om aan de slag te gaan.

## Gegevens van stroomrecord- en tijdreeksen

Met een dataset en het zwerven verbindingen op zijn plaats, kunt u verslag of tijdreeksgegevens in stromen [!DNL Platform]. Als u wilt beginnen met het streamen van recordgegevens, volgt u de [streamrecordgegevens in de zelfstudie](../ingestion/tutorials/streaming-record-data.md)Platform. Als u wilt beginnen met het streamen van tijdreeksgegevens, volgt u de gegevens van de [streaming tijdreeks in het Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Meerdere berichten streamen in één HTTP-aanvraag

Wanneer het stromen van gegevens aan Adobe Experience Platform, kan het maken van talrijke vraag van HTTP duur zijn. Bijvoorbeeld, in plaats van het creëren van 200 HTTP- verzoeken met 1KB nuttige lading, is het veel efficiënter om 1 HTTP- verzoek met 200 berichten van 1KB elk, met één enkele lading van 200KB tot stand te brengen. Wanneer correct gebruikt, is het groeperen van veelvoudige berichten binnen één enkel verzoek een uitstekende manier om gegevens te optimaliseren die worden verzonden naar [!DNL Experience Platform]. Leer hoe te om veelvoudige berichten naar [!DNL Experience Platform] binnen één enkele HTTP- verzoek te verzenden gebruikend het stromen opname, volg het [verzenden van veelvoudige berichtzelfstudie](../ingestion/tutorials/streaming-multiple-messages.md).



