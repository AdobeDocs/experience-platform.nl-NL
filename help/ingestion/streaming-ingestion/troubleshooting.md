---
keywords: Experience Platform;home;populaire onderwerpen;streaming;streaming opname;problemen oplossen;streaming opname oplossen;streaming opname ophalen faq;faq;
solution: Experience Platform
title: Handleiding voor het oplossen van problemen met streaming-inname
topic-legacy: troubleshooting
description: In dit document worden antwoorden gegeven op veelgestelde vragen over het streamen van opname op Adobe Experience Platform.
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# Handleiding voor het oplossen van problemen bij het streamen

In dit document worden antwoorden gegeven op veelgestelde vragen over het streamen van opname op Adobe Experience Platform. Voor vragen en problemen met betrekking tot andere problemen [!DNL Platform] services, inclusief services die overal worden aangetroffen [!DNL Platform] API&#39;s, raadpleeg de [Handleiding voor het oplossen van problemen met Experience Platforms](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] biedt RESTful-API&#39;s die u kunt gebruiken om gegevens in te voeren [!DNL Experience Platform]. De opgenomen gegevens worden gebruikt om individuele klantenprofielen in bijna real time bij te werken, toestaand u om gepersonaliseerde, relevante ervaringen over veelvoudige kanalen te leveren. Lees de [Overzicht van gegevensinname](../home.md) voor meer informatie over de dienst en de verschillende innamemethoden. Voor stappen over het gebruik van streaming opname-API&#39;s leest u de [overzicht van streaming opname](../streaming-ingestion/overview.md).

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over streaming opname.

### Hoe weet ik dat de lading die ik verzend correct geformatteerd is?

[!DNL Data Ingestion] hefboomwerkingen [!DNL Experience Data Model] (XDM) schema&#39;s om het formaat van inkomende gegevens te bevestigen. Het verzenden van gegevens die niet in overeenstemming zijn met de structuur van een vooraf gedefinieerd XDM-schema zal ertoe leiden dat de invoer mislukt. Voor meer informatie over XDM en het gebruik ervan in [!DNL Experience Platform], zie de [XDM System, overzicht](../../xdm/home.md).

Streaming opname ondersteunt twee validatiemodi: synchroon en asynchroon. Elke validatiemethode verwerkt mislukte gegevens anders.

**Synchrone validatie** moet worden gebruikt tijdens uw ontwikkelingsproces. Records die niet kunnen worden gevalideerd, worden verwijderd en er wordt een foutbericht geretourneerd met betrekking tot de vraag waarom deze zijn mislukt (bijvoorbeeld: &quot;Ongeldige XDM Message Format&quot;).

**Asynchrone validatie** worden gebruikt bij de productie. Eventuele beschadigde gegevens die geen validatie doorstaan, worden verzonden naar de [!DNL Data Lake] als een mislukt batchbestand, waar het later kan worden opgehaald voor verdere analyse.

Raadpleeg voor meer informatie over synchrone en asynchrone validatie de [overzicht van streamingvalidatie](../quality/streaming-validation.md). Raadpleeg de handleiding voor informatie over hoe u batches die niet zijn gevalideerd kunt bekijken. [ophalen van mislukte batches](../quality/retrieve-failed-batches.md).

### Kan ik een aanvraaglading bevestigen alvorens het te verzenden naar [!DNL Platform]?

De lading van het verzoek kan slechts worden geëvalueerd nadat zij zijn verzonden naar [!DNL Platform]. Bij het uitvoeren van synchrone validatie retourneert een geldige payload gevulde JSON-objecten terwijl een ongeldige payload foutberichten retourneert. Tijdens asynchrone bevestiging, ontdekt de dienst en verzendt om het even welke misvormde gegevens naar [!DNL Data Lake] waar het later voor analyse kan worden opgehaald. Zie de [overzicht van streamingvalidatie](../quality/streaming-validation.md) voor meer informatie .

### Wat gebeurt er als synchrone validatie wordt aangevraagd voor een rand die deze niet ondersteunt?

Wanneer synchrone validatie niet wordt ondersteund voor de aangevraagde locatie, wordt een 501-foutreactie geretourneerd. Zie de [overzicht van streamingvalidatie](../quality/streaming-validation.md) voor meer informatie over synchrone validatie.

### Hoe kan ik ervoor zorgen dat gegevens alleen worden verzameld van vertrouwde bronnen?

[!DNL Experience Platform] ondersteunt beveiligde gegevensverzameling. Wanneer geverifieerde gegevensverzameling is ingeschakeld, moeten clients een JSON Web Token (JWT) en hun IMS-organisatie-id verzenden als aanvraagheaders. Voor meer informatie over hoe te om voor authentiek verklaarde gegevens te verzenden naar [!DNL Platform], raadpleeg de handleiding op [geverifieerde gegevensverzameling](../tutorials/create-authenticated-streaming-connection.md).

### Wat is de latentie voor het stromen gegevens aan [!DNL Real-time Customer Profile]?

Gestroomde gebeurtenissen worden over het algemeen weerspiegeld in [!DNL Real-time Customer Profile] in minder dan 60 seconden. De daadwerkelijke latentie kan door gegevensvolume, berichtgrootte, en bandbreedtebeperkingen variëren.

### Kan ik meerdere berichten opnemen in dezelfde API-aanvraag?

U kunt veelvoudige berichten binnen één enkele verzoeklading groeperen en hen stromen aan [!DNL Platform]. Als de gegevens correct worden gebruikt, is het groeperen van meerdere berichten binnen één aanvraag een uitstekende manier om uw gegevensbewerkingen te optimaliseren. Lees de zelfstudie op [het verzenden van veelvoudige berichten in een verzoek](../tutorials/streaming-multiple-messages.md) voor meer informatie .

### Hoe weet ik of de gegevens die ik verstuur, worden ontvangen?

Alle gegevens waarnaar wordt verzonden [!DNL Platform] (met succes of anders) wordt opgeslagen als partijdossiers alvorens in datasets wordt voortgeduurd. De verwerkingsstatus van batches wordt weergegeven in de gegevensset waarnaar ze zijn verzonden.

U kunt verifiëren of de gegevens met succes zijn opgenomen door datasetactiviteit te controleren gebruikend [Gebruikersinterface Experience Platform](https://platform.adobe.com). Klikken **[!UICONTROL Datasets]** in de linkernavigatie om een lijst van datasets te tonen. Selecteer de dataset u aan van de getoonde lijst stroomt om zijn te openen **[!UICONTROL Dataset activity]** pagina, met daarin alle batches die tijdens een geselecteerde tijdsperiode zijn verzonden. Voor meer informatie over het gebruik [!DNL Experience Platform] om gegevensstromen te controleren, zie de gids op [streaming gegevensstromen controleren](../quality/monitor-data-ingestion.md).

Als uw gegevens niet zijn ingevoerd en u wilt deze herstellen van [!DNL Platform], kunt u de mislukte batches ophalen door hun id&#39;s naar de [!DNL Data Access API]. Zie de handleiding op [ophalen van mislukte batches](../quality/retrieve-failed-batches.md) voor meer informatie .

### Waarom zijn mijn streaminggegevens niet beschikbaar in het Data Lake?

Er zijn diverse redenen waarom het niet mogelijk is dat de ingestie van de partij de [!DNL Data Lake], zoals ongeldige opmaak, ontbrekende gegevens of systeemfouten. Om te bepalen waarom de batch is mislukt, moet u de batch ophalen met de [!DNL Data Ingestion Service API] en bekijk de details. Voor gedetailleerde stappen bij het terugwinnen van een ontbroken partij, zie de gids op [ophalen van mislukte batches](../quality/retrieve-failed-batches.md).

### Hoe parseer ik de reactie die voor het API verzoek is teruggekeerd?

U kunt een reactie parseren door eerst de antwoordcode van de server te controleren om te bepalen of uw verzoek werd goedgekeurd. Als een geslaagde antwoordcode wordt geretourneerd, kunt u de `responses` matrixobject om de status van de ingangstaak te bepalen.

Een geslaagde API-aanvraag voor één bericht retourneert statuscode 200. Een geslaagde (of gedeeltelijk succesvolle) API-aanvraag voor berichten in batches retourneert statuscode 207.

De volgende JSON is een voorbeeld van een reactieobject voor een API-aanvraag met twee berichten: één succesvol en één mislukt. Berichten die succesvol streamen retourneren een `xactionId` eigenschap. Berichten die er niet in slagen om een stream te retourneren `statusCode` eigenschap en een reactie `message` met meer informatie.

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
                imsOrgId: [{ORG_ID}] 
                Message has unknown xdm format"
        }
    ]
}
```

### Waarom worden mijn verzonden berichten niet ontvangen door [!DNL Real-time Customer Profile]?

Indien [!DNL Real-time Customer Profile] Hiermee wordt een bericht afgewezen. Dit is vooral te wijten aan onjuiste identiteitsgegevens. Dit kan het resultaat zijn van het opgeven van een ongeldige waarde of naamruimte voor een identiteit.

Er zijn twee typen naamruimten: standaard en aangepast. Wanneer u aangepaste naamruimten gebruikt, moet u ervoor zorgen dat de naamruimte is geregistreerd binnen [!DNL Identity Service]. Zie de [Overzicht van naamruimte in identiteit](../../identity-service/namespaces.md) voor meer informatie over het gebruik van standaard- en aangepaste naamruimten.

U kunt de [[!DNL Experience Platform UI]](https://platform.adobe.com) om meer informatie te zien over waarom een bericht ontbrak het opnemen. Klikken **[!UICONTROL Monitoring]** in de linkernavigatie, dan bekijk **[!UICONTROL Streaming end-to-end]** om berichtenbatches te bekijken die tijdens een geselecteerde tijdsperiode zijn gestreamd.
