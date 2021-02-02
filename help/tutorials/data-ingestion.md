---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Zelfstudies voor gegevensinsluiting
topic: tutorial
type: Tutorial
description: De Ingestie van gegevens omvat partijingestie, het stromen ingestie, en ingestie gebruikend bronschakelaars.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Gegevens opnemen in [!DNL Experience Platform]

Adobe Experience Platform brengt gegevens uit meerdere bronnen samen om marketers te helpen het gedrag van hun klanten beter te begrijpen. Adobe [!DNL Experience Platform Data Ingestion] vertegenwoordigt de veelvoudige methodes waardoor [!DNL Platform] gegevens uit deze bronnen inneemt, evenals hoe die gegevens binnen het meer van Gegevens voor gebruik door stroomafwaarts [!DNL Platform services] worden voortgeduurd. [!DNL Data Ingestion] omvat batch-opname, streaming opname en inname via bronconnectors. Lees voor meer informatie het [Data Ingestie overview](../ingestion/home.md) of ga direct naar de [Brondocumentatie](../sources/home.md).

## Een bronaansluiting maken in de gebruikersinterface en de API

De bronschakelaars staan u toe om gegevens van veelvoudige bronnen in te voeren, waar het dan kan worden geëtiketteerd, gestructureerd, en worden verbeterd gebruikend [!DNL Platform services]. Als u een bronaansluiting wilt maken, raadpleegt u het [overzicht van bronnen](../sources/home.md).

## Gegevens van groep samenvoegen

Met Adobe Experience Platform kunt u gegevens eenvoudig als batchbestanden importeren in [!DNL Platform]. Voorbeelden van gegevens die moeten worden opgenomen kunnen profielgegevens van een vlak dossier in een systeem van CRM (zoals een dossier van het Pakket) of gegevens omvatten die aan een bekend [!DNL Experience Data Model] (XDM) schema in de Registratie van het Schema in overeenstemming zijn. Ga om aan de slag te gaan naar de [inname-gegevens in de zelfstudie Platform](../ingestion/tutorials/ingest-batch-data.md).

## Een CSV-bestand toewijzen aan een XDM-schema

Als u CSV-gegevens in Adobe Experience Platform wilt invoeren, moeten de gegevens worden toegewezen aan een [!DNL Experience Data Model] (XDM)-schema. Voor stappen die tonen hoe te om een Csv- dossier aan een XDM- schema in kaart te brengen gebruikend [!DNL Experience Platform] gebruikersinterface, [kaart een Csv- dossier aan een XDM schemaleerprogramma ](../ingestion/tutorials/map-a-csv-file.md) in kaart brengen.

## Een streamingverbinding maken

Als u wilt beginnen met het streamen van gegevens naar [!DNL Experience Platform], moet u eerst een HTTP-eindpunt aanvragen. U hebt de optie om dit eindpunt te vormen om voor authentiek verklaard gedrag af te dwingen. Dit kan worden gedaan gebruikend [!DNL Platform] gebruikersinterface of [!DNL Experience Platform] APIs. Voor meer informatie volgt u de zelfstudies voor het maken van een streamingverbinding met de UI](../ingestion/tutorials/create-streaming-connection-ui.md) of [het maken van een streamingverbinding met behulp van API&#39;s](../ingestion/tutorials/create-streaming-connection.md).[

## Een geverifieerde streamingverbinding maken

Met geverifieerde gegevensverzameling kunnen Adobe Experience Platform-services, zoals [!DNL Real-time Customer Profile] en [!DNL Identity], onderscheid maken tussen records die afkomstig zijn van vertrouwde bronnen en niet-vertrouwde bronnen. Volg de zelfstudie voor [het maken van een geverifieerde streamingverbinding](../ingestion/tutorials/create-authenticated-streaming-connection.md) om aan de slag te gaan.

## Gegevens van stroomrecord- en tijdreeksen

Met een dataset en het zwerven verbindingen op zijn plaats, kunt u verslag of tijdreeksgegevens in [!DNL Platform] stromen. Als u wilt beginnen met het streamen van recordgegevens, volgt u de [streamrecordgegevens in de zelfstudie Platform](../ingestion/tutorials/streaming-record-data.md). Als u wilt beginnen met het streamen van tijdreeksgegevens, volgt u de [streamtijdreeksgegevens in Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Meerdere berichten streamen in één HTTP-aanvraag

Wanneer het stromen van gegevens aan Adobe Experience Platform, kan het maken van talrijke vraag van HTTP duur zijn. Bijvoorbeeld, in plaats van het creëren van 200 HTTP- verzoeken met 1KB nuttige lading, is het veel efficiënter om 1 HTTP- verzoek met 200 berichten van 1KB elk, met één enkele lading van 200KB tot stand te brengen. Wanneer correct gebruikt, is het groeperen van veelvoudige berichten binnen één enkel verzoek een uitstekende manier om gegevens te optimaliseren die naar [!DNL Experience Platform] worden verzonden. Om te leren hoe te om veelvoudige berichten naar [!DNL Experience Platform] binnen één enkel HTTP- verzoek te verzenden gebruikend het stromen opname, volg [verzendend veelvoudige berichtzelfstudie](../ingestion/tutorials/streaming-multiple-messages.md).



