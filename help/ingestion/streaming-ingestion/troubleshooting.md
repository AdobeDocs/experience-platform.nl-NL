---
keywords: Experience Platform;home;populaire onderwerpen;streaming;streaming opname;problemen oplossen;streaming opname problemen;streaming opname faq;faq;
solution: Experience Platform
title: Handleiding voor het oplossen van problemen met streaming-inname
description: In dit document worden antwoorden gegeven op veelgestelde vragen over het streamen van opname op Adobe Experience Platform.
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# Handleiding voor het oplossen van problemen bij het streamen

In dit document worden antwoorden gegeven op veelgestelde vragen over het streamen van opname op Adobe Experience Platform. Voor vragen en het oplossen van problemen met betrekking tot andere [!DNL Experience Platform] diensten, met inbegrip van die die over alle [!DNL Experience Platform] APIs worden ontmoet, gelieve te verwijzen naar de [&#x200B; het oplossen van problemengids van Experience Platform &#x200B;](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] biedt RESTful-API&#39;s die u kunt gebruiken om gegevens in [!DNL Experience Platform] in te voeren. De opgenomen gegevens worden gebruikt om individuele klantenprofielen in bijna real time bij te werken, toestaand u om gepersonaliseerde, relevante ervaringen over veelvoudige kanalen te leveren. Gelieve te lezen het [&#x200B; overzicht van de Ingestie van Gegevens &#x200B;](../home.md) voor meer informatie over de dienst en de verschillende inspraakmethodes. Voor stappen op hoe te om het stromen ingestie APIs te gebruiken, te lezen gelieve [&#x200B; het stromen ingestitieoverzicht &#x200B;](../streaming-ingestion/overview.md).

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over streaming opname.

### Hoe weet ik dat de lading die ik verzend correct geformatteerd is?

[!DNL Data Ingestion] gebruikt [!DNL Experience Data Model] -schema&#39;s (XDM) om de indeling van binnenkomende gegevens te valideren. Het verzenden van gegevens die niet in overeenstemming zijn met de structuur van een vooraf gedefinieerd XDM-schema zal ertoe leiden dat de invoer mislukt. Voor meer informatie over XDM en zijn gebruik in [!DNL Experience Platform], zie het [&#x200B; XDM overzicht van het Systeem &#x200B;](../../xdm/home.md).

Streaming opname ondersteunt twee validatiemodi: synchroon en asynchroon. Elke validatiemethode verwerkt mislukte gegevens anders.

**synchrone bevestiging** zou tijdens uw ontwikkelingsproces moeten worden gebruikt. Records die niet kunnen worden gevalideerd, worden verwijderd en er wordt een foutbericht geretourneerd met betrekking tot de vraag waarom deze zijn mislukt (bijvoorbeeld: &quot;Ongeldige XDM Message Format&quot;).

**Asynchrone bevestiging** zou in productie moeten worden gebruikt. Eventuele onjuiste gegevens die geen validatie doorstaan, worden als een mislukt batchbestand naar de [!DNL Data Lake] verzonden, waar het later kan worden opgehaald voor verdere analyse.

Voor meer informatie over synchrone en asynchrone bevestiging, zie het [&#x200B; stromen bevestigingsoverzicht &#x200B;](../quality/streaming-validation.md). Voor stappen op hoe te om partijen te bekijken die bevestiging ontbreken, te verwijzen gelieve naar de gids op [&#x200B; terugwinnend ontbroken partijen &#x200B;](../quality/retrieve-failed-batches.md).

### Kan ik een aanvraaglading bevestigen alvorens het naar [!DNL Experience Platform] te verzenden?

Aanvraagladingen kunnen alleen worden geëvalueerd nadat ze naar [!DNL Experience Platform] zijn verzonden. Bij het uitvoeren van synchrone validatie retourneert een geldige payload gevulde JSON-objecten terwijl een ongeldige payload foutberichten retourneert. Tijdens asynchrone validatie detecteert de service beschadigde gegevens en verzendt deze naar de [!DNL Data Lake] waar deze later kunnen worden opgehaald voor analyse. Zie [&#x200B; het stromen bevestigingsoverzicht &#x200B;](../quality/streaming-validation.md) voor meer informatie.

### Wat gebeurt er als synchrone validatie wordt aangevraagd voor een rand die deze niet ondersteunt?

Wanneer synchrone validatie niet wordt ondersteund voor de aangevraagde locatie, wordt een 501-foutreactie geretourneerd. Gelieve te zien het [&#x200B; stromen bevestigingsoverzicht &#x200B;](../quality/streaming-validation.md) voor meer informatie over synchrone bevestiging.

### Hoe kan ik ervoor zorgen dat gegevens alleen worden verzameld van vertrouwde bronnen?

[!DNL Experience Platform] ondersteunt beveiligde gegevensverzameling. Wanneer de voor authentiek verklaarde gegevensinzameling wordt toegelaten, moeten de cliënten een Token van het Web JSON (JWT) en hun organisatie-identiteitskaart als verzoekkopballen verzenden. Voor meer informatie over hoe te om voor authentiek verklaarde gegevens naar [!DNL Experience Platform] te verzenden, te zien gelieve de gids over [&#x200B; voor authentiek verklaarde gegevensinzameling &#x200B;](../tutorials/create-authenticated-streaming-connection.md).

### Wat is de latentie voor het stromen gegevens aan [!DNL Real-Time Customer Profile]?

Gestroomde gebeurtenissen worden over het algemeen weerspiegeld in [!DNL Real-Time Customer Profile] in minder dan 60 seconden. De daadwerkelijke latentie kan door gegevensvolume, berichtgrootte, en bandbreedtebeperkingen variëren.

### Kan ik meerdere berichten opnemen in dezelfde API-aanvraag?

U kunt meerdere berichten groeperen binnen één aanvraaglading en deze streamen naar [!DNL Experience Platform] . Als de gegevens correct worden gebruikt, is het groeperen van meerdere berichten binnen één aanvraag een uitstekende manier om uw gegevensbewerkingen te optimaliseren. Gelieve te lezen het leerprogramma op [&#x200B; verzendend veelvoudige berichten in een verzoek &#x200B;](../tutorials/streaming-multiple-messages.md) voor meer informatie.

### Hoe weet ik of de gegevens die ik verstuur, worden ontvangen?

Alle gegevens die naar [!DNL Experience Platform] (met succes of anders) worden verzonden, worden opgeslagen als batchbestanden voordat ze in gegevenssets worden gecontinueerd. De verwerkingsstatus van batches wordt weergegeven in de gegevensset waarnaar ze zijn verzonden.

U kunt verifiëren als het gegeven met succes is opgenomen door datasetactiviteit te controleren gebruikend het [&#x200B; gebruikersinterface van Experience Platform &#x200B;](https://platform.adobe.com). Klik op **[!UICONTROL Datasets]** in de linkernavigatie om een lijst met gegevenssets weer te geven. Selecteer de dataset u van de getoonde lijst aan om zijn **[!UICONTROL Dataset activity]** pagina te openen, die alle partijen toont die tijdens een geselecteerde tijdspanne worden verzonden. Voor meer informatie over het gebruiken van [!DNL Experience Platform] om gegevensstromen te controleren, zie de gids bij [&#x200B; controle het stromen gegevensstromen &#x200B;](../quality/monitor-data-ingestion.md).

Als uw gegevens niet zijn ingevoerd en u wilt deze herstellen vanuit [!DNL Experience Platform] , kunt u de mislukte batches ophalen door hun id&#39;s naar de [!DNL Data Access API] te verzenden. Zie de gids bij [&#x200B; het terugwinnen ontbroken partijen &#x200B;](../quality/retrieve-failed-batches.md) voor meer informatie.

### Waarom zijn mijn streaminggegevens niet beschikbaar in het Data Lake?

Er zijn verschillende redenen waarom het invoeren van batch de [!DNL Data Lake] mogelijk niet bereikt, zoals ongeldige opmaak, ontbrekende gegevens of systeemfouten. Om te bepalen waarom de batch is mislukt, moet u de batch ophalen met de [!DNL Data Ingestion Service API] -code en de details ervan bekijken. Voor gedetailleerde stappen bij het terugwinnen van een ontbroken partij, zie de gids bij [&#x200B; terugwinnen ontbroken partijen &#x200B;](../quality/retrieve-failed-batches.md).

### Hoe parseer ik de reactie die voor het API verzoek is teruggekeerd?

U kunt een reactie parseren door eerst de antwoordcode van de server te controleren om te bepalen of uw verzoek werd goedgekeurd. Als er een geslaagde antwoordcode wordt geretourneerd, kunt u het `responses` -arrayobject bekijken om de status van de gebruikerstaak te bepalen.

Een geslaagde API-aanvraag voor één bericht retourneert statuscode 200. Een geslaagde (of gedeeltelijk succesvolle) API-aanvraag voor berichten in batches retourneert statuscode 207.

De volgende JSON is een voorbeeld van een reactieobject voor een API-aanvraag met twee berichten: één succesvol en één mislukt. Berichten die succesvol streamen, retourneren een eigenschap `xactionId` . Berichten die er niet in slagen om een `statusCode` eigenschap en een reactie `message` met meer informatie te stromen, retourneren.

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

### Waarom worden mijn verzonden berichten niet ontvangen door [!DNL Real-Time Customer Profile]?

Als [!DNL Real-Time Customer Profile] een bericht afwijst, is dit waarschijnlijk te wijten aan onjuiste identiteitsgegevens. Dit kan het resultaat zijn van het opgeven van een ongeldige waarde of naamruimte voor een identiteit.

Er zijn twee typen naamruimten: standaard en aangepast. Wanneer u aangepaste naamruimten gebruikt, moet u ervoor zorgen dat de naamruimte is geregistreerd binnen [!DNL Identity Service] . Zie het [&#x200B; overzicht van identiteitsnamespace &#x200B;](../../identity-service/features/namespaces.md) voor meer informatie bij het gebruiken van gebrek en douane namespaces.

U kunt [[!DNL Experience Platform UI] gebruiken &#x200B;](https://platform.adobe.com) om meer informatie te zien over waarom een bericht ontbrak het opnemen. Klik op **[!UICONTROL Monitoring]** in de linkernavigatie en bekijk vervolgens het tabblad **[!UICONTROL Streaming end-to-end]** om berichtenbatches die tijdens een geselecteerde tijdsperiode zijn gestreamd, weer te geven.
