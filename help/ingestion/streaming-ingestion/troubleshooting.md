---
keywords: Experience Platform;home;populaire onderwerpen;streaming;streaming opname;problemen oplossen;streaming opname oplossen;streaming opname ophalen faq;faq;
solution: Experience Platform
title: Handleiding voor het oplossen van problemen met streaming-inname
topic: troubleshooting
description: In dit document worden antwoorden gegeven op veelgestelde vragen over het streamen van opname op Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---


# Handleiding voor het oplossen van problemen bij het streamen

In dit document worden antwoorden gegeven op veelgestelde vragen over het streamen van opname op Adobe Experience Platform. Raadpleeg de [handleiding voor het oplossen van Experience Platforms](../../landing/troubleshooting.md) voor vragen en problemen met betrekking tot andere [!DNL Platform]-services, inclusief de services die worden aangetroffen in alle [!DNL Platform]-API&#39;s.

Adobe Experience Platform [!DNL Data Ingestion] biedt RESTful-API&#39;s die u kunt gebruiken om gegevens in [!DNL Experience Platform] in te voeren. De opgenomen gegevens worden gebruikt om individuele klantenprofielen in bijna real time bij te werken, toestaand u om gepersonaliseerde, relevante ervaringen over veelvoudige kanalen te leveren. Lees het [Data Ingestie overview](../home.md) voor meer informatie over de service en de verschillende insluitingsmethoden. Lees het [streamingoverzicht](../streaming-ingestion/overview.md) voor informatie over het gebruik van streaming opname-API&#39;s.

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over streaming opname.

### Hoe weet ik dat de lading die ik verzend correct geformatteerd is?

[!DNL Data Ingestion] hefboomwerkings  [!DNL Experience Data Model] (XDM) schema&#39;s om het formaat van inkomende gegevens te bevestigen. Het verzenden van gegevens die niet in overeenstemming zijn met de structuur van een vooraf gedefinieerd XDM-schema zal ertoe leiden dat de invoer mislukt. Voor meer informatie over XDM en zijn gebruik in [!DNL Experience Platform], zie [XDM systeemoverzicht](../../xdm/home.md).

Streaming opname ondersteunt twee validatiemodi: synchroon en asynchroon. Elke validatiemethode verwerkt mislukte gegevens anders.

**De synchrone** bevestiging zou tijdens uw ontwikkelingsproces moeten worden gebruikt. Records die niet kunnen worden gevalideerd, worden verwijderd en er wordt een foutbericht geretourneerd met betrekking tot de vraag waarom deze zijn mislukt (bijvoorbeeld: &quot;Ongeldige XDM Message Format&quot;).

**Bij de productie moet asynchrone** validatie worden gebruikt. Eventuele beschadigde gegevens die geen validatie doorstaan, worden als een mislukt batchbestand verzonden naar [!DNL Data Lake], waar het later kan worden opgehaald voor verdere analyse.

Zie [Overzicht van streamingvalidatie](../quality/streaming-validation.md) voor meer informatie over synchrone en asynchrone validatie. Raadpleeg de handleiding bij [het ophalen van mislukte batches](../quality/retrieve-failed-batches.md) voor informatie over het weergeven van batches waarvoor validatie niet is gelukt.

### Kan ik een verzoeklading bevestigen alvorens het naar [!DNL Platform] te verzenden?

De nuttige ladingen van het verzoek kunnen slechts worden geëvalueerd nadat zij zijn verzonden naar [!DNL Platform]. Bij het uitvoeren van synchrone validatie retourneert een geldige payload gevulde JSON-objecten terwijl een ongeldige payload foutberichten retourneert. Tijdens asynchrone validatie detecteert de service beschadigde gegevens en verzendt deze naar de [!DNL Data Lake] waar deze later kunnen worden opgehaald voor analyse. Zie [Overzicht van streamingvalidatie](../quality/streaming-validation.md) voor meer informatie.

### Wat gebeurt er als synchrone validatie wordt aangevraagd voor een rand die deze niet ondersteunt?

Wanneer synchrone validatie niet wordt ondersteund voor de aangevraagde locatie, wordt een 501-foutreactie geretourneerd. Zie [Overzicht van streamingvalidatie](../quality/streaming-validation.md) voor meer informatie over synchrone validatie.

### Hoe kan ik ervoor zorgen dat gegevens alleen worden verzameld van vertrouwde bronnen?

[!DNL Experience Platform] ondersteunt beveiligde gegevensverzameling. Wanneer geverifieerde gegevensverzameling is ingeschakeld, moeten clients een JSON Web Token (JWT) en hun IMS-organisatie-id verzenden als aanvraagheaders. Voor meer informatie over hoe te om voor authentiek verklaarde gegevens naar [!DNL Platform] te verzenden, te zien gelieve de gids op [voor authentiek verklaarde gegevensinzameling](../tutorials/create-authenticated-streaming-connection.md).

### Wat is de latentie voor het stromen gegevens aan [!DNL Real-time Customer Profile]?

Gestroomde gebeurtenissen worden over het algemeen weerspiegeld in [!DNL Real-time Customer Profile] in minder dan 60 seconden. De daadwerkelijke latentie kan door gegevensvolume, berichtgrootte, en bandbreedtebeperkingen variëren.

### Kan ik meerdere berichten opnemen in dezelfde API-aanvraag?

U kunt veelvoudige berichten binnen één enkele verzoeklading groeperen en hen stromen aan [!DNL Platform]. Als de gegevens correct worden gebruikt, is het groeperen van meerdere berichten binnen één aanvraag een uitstekende manier om uw gegevensbewerkingen te optimaliseren. Lees de zelfstudie over [het verzenden van meerdere berichten in een aanvraag](../tutorials/streaming-multiple-messages.md) voor meer informatie.

### Hoe weet ik of de gegevens die ik verstuur, worden ontvangen?

Alle gegevens die naar [!DNL Platform] (met succes of anders) worden verzonden worden opgeslagen als partijdossiers alvorens in datasets worden voortgeduurd. De verwerkingsstatus van batches wordt weergegeven in de gegevensset waarnaar ze zijn verzonden.

U kunt controleren of gegevens met succes zijn opgenomen door datasetactiviteit te controleren gebruikend [Experience Platform gebruikersinterface](https://platform.adobe.com). Klik **[!UICONTROL Datasets]** in de linkernavigatie om een lijst van datasets te tonen. Selecteer de dataset u aan van de getoonde lijst stroomt om zijn **[!UICONTROL Dataset activiteit]** pagina te openen, tonend alle partijen die tijdens een geselecteerde tijdspanne worden verzonden. Zie de handleiding over [het bewaken van streaming gegevensstromen](../quality/monitor-data-ingestion.md) voor meer informatie over het gebruik van [!DNL Experience Platform] voor het controleren van gegevensstromen.

Als uw gegevens niet kunnen worden ingevoerd en u wilt het van [!DNL Platform] terugkrijgen, kunt u de ontbroken partijen terugwinnen door hun IDs naar [!DNL Data Access API] te verzenden. Zie de handleiding bij [het ophalen van mislukte batches](../quality/retrieve-failed-batches.md) voor meer informatie.

### Waarom zijn mijn streaminggegevens niet beschikbaar in het Data Lake?

Er zijn verschillende redenen waarom het invoeren van batch de [!DNL Data Lake] mogelijk niet bereikt, zoals ongeldige opmaak, ontbrekende gegevens of systeemfouten. Om te bepalen waarom de batch is mislukt, moet u de batch ophalen met de [!DNL Data Ingestion Service API] en de details ervan bekijken. Zie de handleiding op [het ophalen van mislukte batches](../quality/retrieve-failed-batches.md) voor gedetailleerde stappen bij het ophalen van een mislukte batch.

### Hoe parseer ik de reactie die voor het API verzoek is teruggekeerd?

U kunt een reactie parseren door eerst de antwoordcode van de server te controleren om te bepalen of uw verzoek werd goedgekeurd. Als een succesvolle antwoordcode is teruggekeerd, kunt u `responses` serievoorwerp dan herzien om de status van de ingangstaak te bepalen.

Een geslaagde API-aanvraag voor één bericht retourneert statuscode 200. Een geslaagde (of gedeeltelijk succesvolle) API-aanvraag voor berichten in batches retourneert statuscode 207.

De volgende JSON is een voorbeeld van een reactieobject voor een API-aanvraag met twee berichten: één succesvol en één mislukt. Berichten die met succes stromen terugkeren een `xactionId` bezit. Berichten die er niet in slagen om een `statusCode` bezit en een reactie `message` met meer informatie te stromen.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a
                79b25e9421ea127f5] 
                imsOrgId: [{IMS_ORG}] 
                Message has unknown xdm format"
        }
    ]
}
```

### Waarom worden mijn verzonden berichten niet ontvangen door [!DNL Real-time Customer Profile]?

Als [!DNL Real-time Customer Profile] een bericht verwerpt, is het hoogstwaarschijnlijk toe te schrijven aan onjuiste identiteitsinformatie. Dit kan het resultaat zijn van het opgeven van een ongeldige waarde of naamruimte voor een identiteit.

Er zijn twee typen naamruimten: standaard en aangepast. Wanneer u aangepaste naamruimten gebruikt, moet u ervoor zorgen dat de naamruimte is geregistreerd binnen [!DNL Identity Service]. Zie [Naamruimte overzicht](../../identity-service/namespaces.md) voor meer informatie over het gebruik van standaard- en aangepaste naamruimten.

U kunt [[!DNL Experience Platform UI]](https://platform.adobe.com) gebruiken om meer informatie te zien over waarom een bericht mislukte opname. Klik **[!UICONTROL Controle]** in de linkernavigatie, dan bekijk **[!UICONTROL het stromen van begin tot eind]** lusje om berichtpartijen te zien die tijdens een geselecteerde tijdspanne worden gestroomd.
