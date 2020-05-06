---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Problemen met streaming opname oplossen
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 0eecd802fc8d0ace3a445f3f188a7f095b97d0c8
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 0%

---


# Handleiding voor het oplossen van problemen bij het streamen

In dit document worden antwoorden gegeven op veelgestelde vragen over het streamen van opname via het Adobe Experience Platform. Voor vragen en het oplossen van problemen met betrekking tot andere diensten van het Platform, met inbegrip van die die over alle Platform APIs worden ontmoet, gelieve te verwijzen naar de het oplossen van problemengids [van het Platform van de](../../landing/troubleshooting.md)Ervaring.

De Opname van de Gegevens van het Platform van de Ervaring van Adobe verstrekt RESTful APIs die u kunt gebruiken om gegevens in het Platform van de Ervaring op te nemen. De opgenomen gegevens worden gebruikt om individuele klantenprofielen in bijna real time bij te werken, toestaand u om gepersonaliseerde, relevante ervaringen over veelvoudige kanalen te leveren. Lees het overzicht [van de](../home.md) gegevensinname voor meer informatie over de service en de verschillende innamemethoden. Lees het [overzicht](../streaming-ingestion/overview.md)van de streamingopname voor informatie over het gebruik van API&#39;s voor het opnemen van streaming.

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over streaming opname.

### Hoe weet ik dat de lading die ik verzend correct geformatteerd is?

De schema&#39;s van het Model van de Gegevens van de Ervaring van het Gegevensmodel (XDM) om het formaat van inkomende gegevens te bevestigen. Het verzenden van gegevens die niet in overeenstemming zijn met de structuur van een vooraf gedefinieerd XDM-schema zal ertoe leiden dat de invoer mislukt. Voor meer informatie over XDM en zijn gebruik in het Platform van de Ervaring, zie het [Overzicht](../../xdm/home.md)van het Systeem XDM.

Streaming opname ondersteunt twee validatiemodi: synchroon en asynchroon. Elke validatiemethode verwerkt mislukte gegevens anders.

**De synchrone bevestiging** zou tijdens uw ontwikkelingsproces moeten worden gebruikt. Records die niet kunnen worden gevalideerd, worden verwijderd en er wordt een foutbericht geretourneerd met betrekking tot de vraag waarom deze zijn mislukt (bijvoorbeeld: &quot;Ongeldige XDM Message Format&quot;).

**Bij de productie moet asynchrone validatie** worden gebruikt. Eventuele misvormde gegevens die geen validatie doorstaan, worden naar het Data Lake verzonden als een mislukt batchbestand, waar het later kan worden opgehaald voor verdere analyse.

Zie het [streamingvalidatieoverzicht](../quality/streaming-validation.md)voor meer informatie over synchrone en asynchrone validatie. Raadpleeg de handleiding bij het [ophalen van mislukte batches](../quality/retrieve-failed-batches.md)voor informatie over het weergeven van batches waarvoor validatie niet is gelukt.

### Kan ik een aanvraaglading bevestigen alvorens het naar Platform te verzenden?

De nuttige ladingen van het verzoek kunnen slechts worden geëvalueerd nadat zij naar Platform zijn verzonden. Bij het uitvoeren van synchrone validatie retourneert een geldige payload gevulde JSON-objecten terwijl een ongeldige payload foutberichten retourneert. Tijdens asynchrone bevestiging, ontdekt de dienst en verzendt om het even welke misvormde gegevens naar het meer van Gegevens waar het later voor analyse kan worden teruggewonnen. Zie het [streamingvalidatieoverzicht](../quality/streaming-validation.md) voor meer informatie.

### Wat gebeurt er als synchrone validatie wordt aangevraagd voor een rand die deze niet ondersteunt?

Wanneer synchrone validatie niet wordt ondersteund voor de aangevraagde locatie, wordt een 501-foutreactie geretourneerd. Zie het [streamingvalidatieoverzicht](../quality/streaming-validation.md) voor meer informatie over synchrone validatie.

### Hoe kan ik ervoor zorgen dat gegevens alleen worden verzameld van vertrouwde bronnen?

Experience Platform ondersteunt beveiligde gegevensverzameling. Wanneer geverifieerde gegevensverzameling is ingeschakeld, moeten clients een JSON Web Token (JWT) en hun IMS-organisatie-id verzenden als aanvraagheaders. Voor meer informatie over hoe te om voor authentiek verklaarde gegevens naar Platform te verzenden, te zien gelieve de gids over [voor authentiek verklaarde gegevensinzameling](../tutorials/create-authenticated-streaming-connection.md).

### Wat is de latentie voor het stromen gegevens aan het Profiel van de Klant in real time?

Gestroomde gebeurtenissen worden over het algemeen weerspiegeld in het Real-time profiel van de Klant binnen 60 seconden. De daadwerkelijke latentie kan door gegevensvolume, berichtgrootte, en bandbreedtebeperkingen variëren.

### Kan ik meerdere berichten opnemen in dezelfde API-aanvraag?

U kunt veelvoudige berichten binnen één enkele verzoeklading groeperen en hen stromen aan Platform. Als de gegevens correct worden gebruikt, is het groeperen van meerdere berichten binnen één aanvraag een uitstekende manier om uw gegevensbewerkingen te optimaliseren. Lees de zelfstudie over het [verzenden van meerdere berichten in een aanvraag](../tutorials/streaming-multiple-messages.md) voor meer informatie.

### Hoe weet ik of de gegevens die ik verstuur, worden ontvangen?

Alle gegevens die naar Platform (met succes of anders) worden verzonden worden opgeslagen als partijdossiers alvorens in datasets worden voortgeduurd. De verwerkingsstatus van batches wordt weergegeven in de gegevensset waarnaar ze zijn verzonden.

U kunt verifiëren of de gegevens met succes zijn opgenomen door datasetactiviteit te controleren gebruikend het de gebruikersinterface [van het Platform van de](https://platform.adobe.com)Ervaring. Klik **Datasets** in de linkernavigatie om een lijst van datasets te tonen. Selecteer de dataset u aan van de getoonde lijst stroomt om zijn de activiteitenpagina *van de* Dataset te openen, tonend alle partijen die tijdens een geselecteerde tijdspanne worden verzonden. Zie de handleiding voor het [controleren van streaming gegevensstromen](../quality/monitor-data-flows.md)voor meer informatie over het gebruik van Experience Platform voor het controleren van gegevensstromen.

Als uw gegevens niet kunnen worden ingevoerd en u wilt het van Platform terugkrijgen, kunt u de ontbroken partijen terugwinnen door hun IDs naar de Toegang API [van][Data Access Service API]Gegevens te verzenden. Zie de handleiding over het [ophalen van mislukte batches](../quality/retrieve-failed-batches.md) voor meer informatie.

### Waarom zijn mijn streaminggegevens niet beschikbaar in het Data Lake?

Er zijn verschillende redenen waarom het opnemen van batches het Data Lake mogelijk niet bereikt, zoals ongeldige opmaak, ontbrekende gegevens of systeemfouten. Om te bepalen waarom uw partij ontbrak, moet u de partij terugwinnen gebruikend de Dienst API [van de Ingestie van][Data Ingestion Service] Gegevens en zijn details bekijken. Zie de handleiding over het [ophalen van mislukte batches](../quality/retrieve-failed-batches.md)voor gedetailleerde stappen over het ophalen van een mislukte batch.

### Hoe parseer ik de reactie die voor het API verzoek is teruggekeerd?

U kunt een reactie parseren door eerst de antwoordcode van de server te controleren om te bepalen of uw verzoek werd goedgekeurd. Als een geslaagde antwoordcode wordt geretourneerd, kunt u het `responses` matrixobject bekijken om de status van de ingstaak te bepalen.

Een geslaagde API-aanvraag voor één bericht retourneert statuscode 200. Een geslaagde (of gedeeltelijk succesvolle) API-aanvraag voor berichten in batches retourneert statuscode 207.

De volgende JSON is een voorbeeld van een reactieobject voor een API-aanvraag met twee berichten: één succesvol en één mislukt. Berichten die een `xactionId` eigenschap hebben gestreamd, retourneren deze. De berichten die er niet in slagen om een `statusCode` bezit en een reactie `message` met meer informatie te stromen.

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

### Waarom worden mijn verzonden berichten niet ontvangen door het Profiel van de Klant in real time?

Als het Profiel van de Klant in real time een bericht verwerpt, is het hoogstwaarschijnlijk toe te schrijven aan onjuiste identiteitsinformatie. Dit kan het resultaat zijn van het opgeven van een ongeldige waarde of naamruimte voor een identiteit.

Er zijn twee typen naamruimten: standaard en aangepast. Wanneer het gebruiken van douanenaamruimten, zorg ervoor namespace binnen de Dienst van de Identiteit is geregistreerd. Zie het overzicht [van naamruimte](../../identity-service/namespaces.md) voor identiteiten voor meer informatie over het gebruik van standaard- en aangepaste naamruimten.

U kunt de UI [van het Platform van de](https://platform.adobe.com) Ervaring gebruiken om meer informatie te zien over waarom een bericht ontbrak het opnemen. Klik op **Controle** in de linkernavigatie en bekijk het tabblad _Streaming end-to-end_ om de berichtbatches te zien die tijdens een geselecteerde tijdsperiode worden gestreamd.