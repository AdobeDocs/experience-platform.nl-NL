---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zelfstudies voor gegevensinsluiting
topic: tutorial
translation-type: tm+mt
source-git-commit: 2020f4b88f81f2d4fe3cfbd91cd18119ae580f4f

---


# Gegevens verzamelen in Experience Platform

Met het Adobe Experience Platform worden gegevens uit meerdere bronnen bijeengebracht om marketers te helpen het gedrag van hun klanten beter te begrijpen. De Ingestie van de Gegevens van het Platform van de Ervaring van Adobe vertegenwoordigt de veelvoudige methodes waardoor Platform gegevens uit deze bronnen opneemt, evenals hoe die gegevens binnen het meer van Gegevens voor gebruik door de stroomafwaartse diensten van het Platform worden voortgeduurd. De Ingestie van gegevens omvat partijingestie, het stromen ingestie, en ingestie gebruikend bronschakelaars. Meer leren, lees het overzicht [van de Ingestie van](../ingestion/home.md) Gegevens of ga direct aan de [Brondocumentatie](../source-connectors/home.md)te werk.

## Een bronaansluiting maken in de gebruikersinterface en de API

De bron schakelaars staan u toe om gegevens van veelvoudige bronnen in te voeren, waar het dan kan worden geëtiketteerd, gestructureerd, en worden verbeterd gebruikend de diensten van het Platform. Ga naar het [maken van een bronaansluiting in het overzicht](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/sources-ui-tutorial.md)van de gebruikersinterface als u een aansluiting wilt maken met de gebruikersinterface. Als u bronconnectors wilt maken met de API, gaat u naar het [aanmaken van een bronaansluiting met behulp van het overzicht](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/sources-api-tutorial.md)van de Flow Service API.

## Gegevens van groep samenvoegen

Met het Adobe Experience Platform kunt u gegevens eenvoudig als batchbestanden importeren in Platform. Voorbeelden van gegevens die moeten worden opgenomen, kunnen profielgegevens bevatten van een plat bestand in een CRM-systeem (zoals een parketbestand) of gegevens die voldoen aan een bekend XDM-schema (Experience Data Model) in de Schemaregistratie. Ga om aan de slag te gaan naar de [inloggegevens in de zelfstudie](../ingestion/tutorials/ingest-batch-data.md)Platform.

## Een CSV-bestand toewijzen aan een XDM-schema

Als u CSV-gegevens wilt opnemen in het Adobe Experience Platform, moeten de gegevens worden toegewezen aan een XDM-schema (Experience Data Model). Voor stappen die tonen hoe te om een Csv- dossier aan een XDM- schema in kaart te brengen gebruikend het gebruikersinterface van het Platform van de Ervaring, volg de [kaart een Csv- dossier aan een XDM schemazelfstudie](../ingestion/tutorials/map-a-csv-file.md).

## Een streamingverbinding maken

Als u wilt beginnen met streamen van gegevens naar Experience Platform, moet u eerst een streaming HTTP-verbinding maken. Wanneer u een streamingverbinding maakt, moet u belangrijke details opgeven, zoals de bron van streaminggegevens, en of u gegevens wilt verzenden van een vertrouwde (geverifieerde) of niet-vertrouwde (niet-geverifieerde) bron. Dit kan worden gedaan gebruikend het de gebruikersinterface van het Platform of Ervaar Platform APIs. Voor meer informatie volgt u de zelfstudies voor het [maken van een streamingverbinding met de gebruikersinterface](../ingestion/tutorials/create-streaming-connection-ui.md) of het [maken van een streamingverbinding met API&#39;s](../ingestion/tutorials/create-streaming-connection.md).

## Een geverifieerde streamingverbinding maken

Met geverifieerde gegevensverzameling kunnen services van het Adobe Experience Platform, zoals Real-time klantprofiel en Identity, onderscheid maken tussen records die afkomstig zijn van vertrouwde bronnen en niet-vertrouwde bronnen. Volg de zelfstudie voor het [maken van een geverifieerde streamingverbinding](../ingestion/tutorials/create-authenticated-streaming-connection.md)om aan de slag te gaan.

## Gegevens van stroomrecord- en tijdreeksen

Met een dataset en het zwerven verbindingen op zijn plaats, kunt u verslag of tijdreeksgegevens in Platform stromen. Als u wilt beginnen met het streamen van recordgegevens, volgt u de [streamrecordgegevens in de zelfstudie](../ingestion/tutorials/streaming-record-data.md)Platform. Als u wilt beginnen met het streamen van tijdreeksgegevens, volgt u de tijdreeksgegevens van de [stream naar Platform](../ingestion/tutorials/streaming-time-series-data.md).

## Meerdere berichten streamen in één HTTP-aanvraag

Bij het streamen van gegevens naar het Adobe Experience Platform kan het maken van veel HTTP-oproepen duur zijn. Bijvoorbeeld, in plaats van het creëren van 200 HTTP- verzoeken met 1KB nuttige lading, is het veel efficiënter om 1 HTTP- verzoek met 200 berichten van 1KB elk, met één enkele lading van 200KB tot stand te brengen. Wanneer correct gebruikt, is het groeperen van veelvoudige berichten binnen één enkel verzoek een uitstekende manier om gegevens te optimaliseren die naar het Platform van de Ervaring worden verzonden. Leer hoe te om veelvoudige berichten naar het Platform van de Ervaring binnen één enkel HTTP- verzoek te verzenden gebruikend het stromen ingestie, volg het [verzenden van veelvoudige berichtzelfstudie](../ingestion/tutorials/streaming-multiple-messages.md).



