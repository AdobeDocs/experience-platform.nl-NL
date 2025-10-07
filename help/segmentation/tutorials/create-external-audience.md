---
title: Een extern publiek maken en activeren
type: Tutorial
description: Leer hoe u een extern publiek in Adobe Experience Platform kunt maken met de Experience Platform API's.
source-git-commit: 0a37ef2f5fc08eb515c7c5056936fd904ea6d360
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 0%

---


# Een extern publiek maken en activeren met de API

In deze zelfstudie worden de stappen doorlopen die nodig zijn om een extern publiek te maken met de Adobe Experience Platform API&#39;s.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de verschillende Experience Platform-services die betrokken zijn bij het creëren van een extern publiek. Lees vóór het begin van deze zelfstudie de documentatie voor de volgende services:

- [&#x200B; Bronnen &#x200B;](../../sources/home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): hiermee kunt u een publiek maken op basis van de externe gegevens.
- [&#x200B; Doelen &#x200B;](../../destinations/home.md): De bestemmingen zijn pre-gebouwde integratie met algemeen gebruikte toepassingen die voor de naadloze activering van gegevens van Experience Platform voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en meer toestaan.

### Vereiste koppen

Dit leerprogramma vereist u ook om het [&#x200B; authentificatieleerprogramma &#x200B;](https://www.adobe.com/go/platform-api-authentication-en) te voltooien om vraag aan [!DNL Experience Platform] APIs met succes te maken. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Voor aanvragen van [!DNL Experience Platform] API&#39;s is een header vereist die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Experience Platform], zie de [&#x200B; documentatie van het zandbakoverzicht &#x200B;](../../sandboxes/home.md).

Voor alle POST-, PUT- en PATCH-aanvragen is een extra header vereist:

- Inhoudstype: application/json

## Het externe publiek voorbereiden {#prepare}

Voordat u een extern publiek kunt maken in Experience Platform, moet u een bestand voorbereiden dat de publieksgegevens bevat.

In dit voorbeeld moet u een CSV-bestand gebruiken. Verzeker uw Csv- dossier **minstens** één kolom met een identiteitswaarde zoals ECID, e-mailidentiteitskaart, of identiteitskaart van CRM bevat. Bovendien, zorg ervoor bevat alle verrijkingsattributen u voor segmentatie en activering zult nodig hebben.

U moet er ook voor zorgen dat het bestand voldoet aan de vereisten van uw Experience Platform-schema. Voor meer informatie bij het creëren van een schema, lees of de [&#x200B; leerprogramma bij het creëren van een schema gebruikend API &#x200B;](/help/xdm/tutorials/create-schema-api.md) of [&#x200B; leerprogramma bij het creëren van een schema gebruikend UI &#x200B;](/help/xdm/tutorials/create-schema-ui.md).

Nadat u hebt bevestigd dat uw CSV-bestand alle benodigde informatie bevat en voldoet aan het schema, moet u het CSV-bestand uploaden naar uw leverancier van cloudopslag, zodat u bronnen kunt gebruiken om de gegevens in Experience Platform in te voeren. Voor meer informatie bij het gebruiken van een bron van de wolkenopslag, lees of het [&#x200B; leerprogramma bij het onderzoeken van de opties van de wolkenopslag gebruikend API &#x200B;](/help/sources/tutorials/api/explore/cloud-storage.md) of het [&#x200B; overzicht van bronnen &#x200B;](/help/sources/home.md#cloud-storage).

## Een extern publiek maken {#create}

Nadat u het CSV-bestand hebt voorbereid, kunt u nu beginnen met het maken van het externe publiek.

U kunt een extern publiek maken door een POST-aanvraag in te dienen bij het eindpunt van `/external-audience/` .

Wanneer u dit verzoek indient, moet u de volgende informatie opgeven:

- De naam van het publiek
- Een beschrijving voor het publiek
- De overeenkomstige gebieden tussen CSV en het schema
- De bronspecificatiegegevens
   - Dit omvat het bestandspad van het CSV-bestand voor inname
      - De dossierweg **kan** geen ruimten bevatten. Als het pad bijvoorbeeld `activation/sample-source/Example CSV File.csv` is, stelt u het pad in op `activation/sample-source/ExampleCSVFile.csv` .

Voor meer gedetailleerde informatie over hoe te om dit eindpunt te gebruiken, lees de [&#x200B; externe gids van het kijkeindpunt &#x200B;](/help/segmentation/api/external-audiences.md#create-audience).

+++Verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

+++

Nadat u deze aanvraag hebt ingediend, controleert u of u de `operationId` hebt ontvangen van de reactie zodat u de gebruikers-id kunt ophalen.

## Hpubliek-id ophalen {#retrieve-audience-id}

Nu u het externe publiek hebt gemaakt, moet u de gebruikers-id ophalen zodat u het publiek in Experience Platform kunt opnemen.

U kunt de publieks-id ophalen door een GET-aanvraag in te dienen bij het `/external-audiences/operations` -eindpunt en de id op te geven van de bewerking die u eerder hebt ontvangen vanuit de methode voor het maken van externe reacties van het publiek.

Voor meer gedetailleerde informatie over hoe te om dit eindpunt te gebruiken, lees de [&#x200B; externe gids van het publiekseindpunt &#x200B;](/help/segmentation/api/external-audiences.md#retrieve-status).

+++ Verzoek

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/{OPERATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

Nadat u deze aanvraag hebt ingediend, controleert u of u nota neemt van `audienceId` u van de reactie ontvangt zodat kunt u de innametaak voor het publiek teweegbrengen.

## Beginnen met publiek starten {#start-ingestion}

Aangezien u uw `audienceId` hebt, kunt u nu de opname van uw externe publiek in Experience Platform activeren.

U kunt een publieksopname beginnen door een POST- verzoek aan het volgende eindpunt te doen terwijl het verstrekken van publiekidentiteitskaart Daarnaast moet u de begintijd opgeven om te bepalen welke bestanden worden verwerkt.

Voor meer gedetailleerde informatie over hoe te om dit eindpunt te gebruiken, lees de [&#x200B; externe gids van het publiek eindpunt &#x200B;](/help/segmentation/api/external-audiences.md#start-audience-ingestion)

+++ Verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

+++

Nadat u deze aanvraag hebt ingediend, controleert u de `runId` die u van het antwoord ontvangt, zodat u de innamestatus kunt controleren.

## Status van opname controleren {#monitor-ingestion}

Nadat u de publieksopname hebt geactiveerd, kunt u nu de voortgang van de opname controleren om het succes van de opname te bevestigen en de beschikbaarheid van het publiek voor downstreamactivering te valideren.

U kunt de status van een publieksinvoer terugwinnen door een GET- verzoek aan het volgende eindpunt te doen terwijl het verstrekken van zowel het publiek als looppas IDs.

Voor meer gedetailleerde informatie over hoe te om dit eindpunt te gebruiken, lees de [&#x200B; externe gids van het publiekseindpunt &#x200B;](/help/segmentation/api/external-audiences.md#retrieve-ingestion-status).

+++ Verzoek

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs/{RUN_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

## Volgende stappen {#next-steps}

>[!IMPORTANT]
>
>Om het extern geproduceerde publiek te gebruiken, moet u **&#x200B;**&#x200B;wachten tot de dagelijkse segmentatietaak is voltooid.

Zodra u hebt bevestigd dat het externe publiek met succes is opgenomen, kunt u het in het Portaal van het Publiek zien en het gebruiken in stroomafwaartse diensten zoals bestemmingen.

Voor meer informatie over het Portaal van het Publiek, lees de [&#x200B; gids UI van het Portaal van het Publiek &#x200B;](/help/segmentation/ui/audience-portal.md). Voor meer informatie over bestemmingen, lees het [&#x200B; overzicht van bestemmingen &#x200B;](/help/destinations/home.md).

