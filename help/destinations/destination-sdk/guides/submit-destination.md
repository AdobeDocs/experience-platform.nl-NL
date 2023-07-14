---
description: Deze pagina verstrekt alle informatie u voor overzicht een geproduceerde bestemming moet voorleggen die gebruikend Destination SDK wordt authored.
title: Ter controle een productiebestemming verzenden die is geschreven in Destination SDK
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# Ter controle een productiebestemming verzenden die is geschreven in Destination SDK

## Overzicht {#overview}

>[!IMPORTANT]
>
>* Het hier gedocumenteerde proces wordt slechts vereist voor partners die geproduceerde (openbare) bestemmingen voorleggen. Als u een privé bestemming voor uw eigen gebruik creeert, te hoeven u niet om deze materialen te produceren en te delen met Adobe.
>
>* Publicatietijd Adobe is vijf werkdagen.
>
>* Als het team van de Adobe u vraagt om het even welke updates aan uw configuraties na uw aanvankelijke voorlegging aan te brengen, moet u een ander bestemmingspublicatieverzoek voorleggen nadat u de updates aanbrengt.
>
>* Zelfs nadat uw bestemming in de catalogus van het Experience Platform levend is, als u om het even welke updates aan uw configuraties moet maken, moet u een nieuw doel voorleggen publicatieverzoek voor de updates die in de configuraties moeten worden weerspiegeld.

Voordat uw bestemming kan worden gepubliceerd naar de [Catalogus Experience Platform doelen](/help/destinations/catalog/overview.md), moet u Adobe bepaalde informatie geven over de bestemming en de uitgevoerde tests om ervoor te zorgen dat gebruikers de best mogelijke ervaring hebben met het activeren van gegevens op uw platform.

Deze pagina bevat alle informatie die u moet opgeven wanneer u een bestemming verzendt of bijwerkt die u met Adobe Experience Platform Destination SDK hebt gemaakt. Als u een bestemming in Adobe Experience Platform wilt verzenden, stuurt u een e-mail naar <aepdestsdk@adobe.com> waaronder:

* Een beschrijving van de gebruiksgevallen die uw bestemming oplost. Dit wordt slechts vereist als u een nieuwe bestemmingsconfiguratie voorlegt.
* Een beschrijving van de reden voor het verzenden van uw bestemming. Dit wordt slechts vereist als u een bestaande bestemmingsconfiguratie bijwerkt.
* De resultaten van de test na het gebruiken van het bestemmingsAPI eindpunt om een vraag van HTTP aan uw bestemming uit te voeren. Gelieve te delen met Adobe een API vraag die aan uw bestemmingshindpunt wordt gemaakt en de API reactie die van uw bestemmingshindpunt wordt ontvangen.
* Aanvullende vereisten voor bestandsgebaseerde doelen:
   * Een aanvraag en een reactievoorbeeld delen nadat de API voor testen is gebruikt [Bestandsgebaseerde bestemming testen met voorbeeldprofielen](../testing-api/batch-destinations/file-based-destination-testing-api.md).
   * Koppel een voorbeeldbestand dat door uw bestemming is gegenereerd en dat naar uw opslaglocatie is geëxporteerd.
   * Verzend een of andere vorm van bewijs dat u het geëxporteerde bestand van de opslaglocatie naar uw systeem hebt ingevoerd.
* Het bewijs dat u een bestemmings het publiceren verzoek voor uw bestemming gebruikend hebt voorgelegd [doel-publicatie-API](../publishing-api/create-publishing-request.md).
* Een documentatie PR (trekkingsverzoek), volgens de instructies die in de [zelfbedieningsdocumentatie](../docs-framework/documentation-instructions.md).
* Een afbeeldingsbestand dat wordt weergegeven als een logo voor uw doelkaart in de catalogus met bestemmingen voor het Experience Platform.

In de onderstaande secties vindt u gedetailleerde informatie over elk onderdeel:

## Omschrijving hoofdletter gebruiken {#use-case-description}

Verstrek een beschrijving van de gebruiksgevallen die uw bestemming voor klanten van het Experience Platform oplost. Uw beschrijvingen kunnen gelijkaardig zijn aan gebruiksgevallen van bestaande partners:

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): Maak een publiek op basis van uw klantlijsten, personen die uw site hebben bezocht of personen die al met uw inhoud hebben gewerkt op Pinterest.
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases): DataX-API&#39;s zijn beschikbaar voor adverteerders die een specifieke doelgroep willen aanwijzen met e-mailadressen die zijn uitgeschakeld in VMG (Verizon Media), zodat ze snel een nieuw publiek kunnen maken en de gewenste doelgroep kunnen duwen met de bijna-real-time API van VMG.

## Reden voor update {#reason-for-update}

>[!NOTE]
>
>Deze sectie is alleen vereist wanneer u een bestaande configuratie bijwerkt.

Geef een korte beschrijving van de kwestie die door uw verzending wordt opgelost voor de bestaande bestemming. Als u bijvoorbeeld een bericht verzendt, worden de naam, beschrijving en het logo van uw bestemming mogelijk bijgewerkt wanneer u overschakelt van bèta naar algemene beschikbaarheid. Of, zou uw voorlegging een insect kunnen bevestigen dat in uw bestemmingsconfiguratie wordt ontdekt.

## Testresultaten na gebruik van de API voor testbestemming {#testing-api-response}

Geef testresultaten op nadat u de [doel-API testen](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) eindpunt om een vraag van HTTP aan uw bestemming uit te voeren. Dit omvat:

* De volledige API-aanvraag (headers en body) die met de API voor testen is ingediend bij het eindpunt van de bestemming.
* De API reactie die van uw bestemmingshindpunt wordt ontvangen.

Uw verzoek en antwoord kunnen bijvoorbeeld lijken op de onderstaande voorbeelden:

**Verzoek**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**Antwoord**

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

## Aanvullende eisen voor op bestanden gebaseerde bestemmingen {#additional-file-based-destination-requirements}

Voor op dossier-gebaseerde bestemmingen, moet u extra bewijs verstrekken dat u correct opstelling uw bestemming hebt. Zorg ervoor dat je de onderstaande objecten opneemt:

### API-reactie testen {#testing-api-response-file-based}

Neem een aanvraag en een reactievoorbeeld op nadat u de API voor testen hebt gebruikt om [Bestandsgebaseerde bestemming testen met voorbeeldprofielen](../testing-api/batch-destinations/file-based-destination-testing-api.md).

### Geëxporteerd bestand bijvoegen {#attach-exported-file}

In uw [verzending-e-mail](#download-sample-email)voegt u een CSV-bestand toe dat naar uw opslaglocatie is geëxporteerd door het doel dat u hebt ingesteld.

### Bewijs van geslaagde inname {#proof-of-successful-ingestion}

Tot slot moet u een of andere vorm van bewijs verstrekken dat de gegevens met succes in uw systeem zijn opgenomen nadat het werd uitgevoerd naar de opslagplaats u verstrekte. Geef hieronder een of meer van de volgende objecten op:

* Screenshots of een korte video van het schermvangst waar u het dossier manueel van de opslagplaats neemt en het in uw systeem opneemt.
* Screenshots of een korte video van het schermvangst waar UI van uw systeem bevestigt dat filename die door Experience Platform wordt geproduceerd met succes in uw systeem werd opgenomen.
* Loglijnen van uw systeem die Adobe met of filename of met de gegevens kan correleren die van Experience Platform worden geproduceerd.

## Bewijs dat u een bestemmings het publiceren verzoek hebt ingediend {#destination-publishing-request-proof}

Nadat u de bestemming hebt getest, moet u de opdracht [doel-publicatie-API](../publishing-api/create-publishing-request.md) om de bestemming voor overzicht en publicatie naar Adobe te verzenden.

Geef de id van de publicatieaanvraag voor uw doel op. Voor informatie over het ophalen van de id van de publicatieaanvraag leest u hoe u [doel-publicatieverzoeken ophalen](../publishing-api/retrieve-publishing-request.md).

## Doeldocumentatie PR (pull-request) voor productieve integratie {#documentation-pr}

Als u een Onafhankelijke Verkoper van de Software (ISV) of Integrator van het Systeem (SI) creeert [productievere integratie](../overview.md#productized-custom-integrations), moet u de [zelfbedieningsdocumentatie](../docs-framework/documentation-instructions.md) om een pagina van de productdocumentatie voor uw bestemming tot stand te brengen. Geef als onderdeel van het verzendproces de pull request (PR) voor de doeldocumentatie op.

## Logo voor uw doel {#logo}

De doelcatalogus bevat een logo voor elke doelkaart. Neem in uw e-mailbericht een afbeelding op met het logo voor uw bestemming.

De afbeeldingsvereisten zijn:
* **Indeling**: `SVG`
* **Grootte**: minder dan 2 MB

## Voorbeeldmail downloaden {#download-sample-email}

[Downloaden](../assets/guides/sample-email-submit-destination.rtf) een voorbeeld-e-mail met alle informatie die u aan Adobe moet verstrekken.
