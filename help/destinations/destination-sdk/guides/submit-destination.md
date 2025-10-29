---
description: Op deze pagina vindt u alle informatie die u nodig hebt om een gebruiksklaar doel ter controle te verzenden wanneer u dit met Destination SDK hebt gemaakt.
title: Verzenden als productiebestemming voor revisie
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---

# Verzenden als productiebestemming voor revisie

## Overzicht {#overview}

>[!IMPORTANT]
>
>* Het hier gedocumenteerde proces wordt slechts vereist voor partners die geproduceerde (openbare) bestemmingen voorleggen. Als u een privébestemming voor eigen gebruik maakt, hoeft u deze materialen niet te maken en te delen met Adobe.
>
>* De standaard Adobe-responstijd voor het controleren van publicatieverzoeken voor doelen is vijf werkdagen.
>
>* Als het Adobe-team u vraagt of u na uw eerste verzending updates voor uw configuraties wilt uitvoeren, moet u een ander publicatieverzoek voor het doel verzenden nadat u de updates hebt uitgevoerd.
>
>* Zelfs nadat uw bestemming in de catalogus van Experience Platform levend is, als u om het even welke updates aan uw configuraties moet maken, moet u een nieuw doel voorleggen publicatieverzoek om de updates worden weerspiegeld in de configuraties.
>
>* De tijdlijn van de revisie en de vereiste artefacten zijn het zelfde voor nieuwe bestemmingen en bestaande bestemmingen die u bijwerkt.

Alvorens uw bestemming aan de [ de bestemmingscatalogus van Experience Platform ](/help/destinations/catalog/overview.md) kan worden gepubliceerd, moet u Adobe van bepaalde informatie over de bestemming en het testen voorzien u uitvoerde, om ervoor te zorgen dat de gebruikers van de beste mogelijke ervaring wanneer het activeren van gegevens aan uw platform genieten.

Deze pagina bevat alle informatie die u moet opgeven wanneer u een bestemming verzendt of bijwerkt die u met Adobe Experience Platform Destination SDK hebt gemaakt. Als u een doel in Adobe Experience Platform wilt verzenden, stuurt u een e-mail naar <aepdestsdk@adobe.com> met daarin:

* Een beschrijving van de gebruiksgevallen die uw bestemming oplost. Dit wordt slechts vereist als u een nieuwe bestemmingsconfiguratie voorlegt.
* Een beschrijving van de reden voor het verzenden van uw bestemming. Dit wordt slechts vereist als u een bestaande bestemmingsconfiguratie bijwerkt.
* De resultaten van de test na het gebruiken van het bestemmingsAPI eindpunt om een vraag van HTTP aan uw bestemming uit te voeren. Deel met Adobe een API-aanroep naar het eindpunt van de bestemming en de API-reactie die u van het eindpunt van de bestemming hebt ontvangen.
* Een schermopname die de gebruikerservaring toont voor iemand die verbinding maakt met uw bestemming en de activeringsstappen doorloopt.
* Aanvullende vereisten voor bestandsgebaseerde doelen:
   * Deel een verzoek en een reactiesteekproef na het gebruiken van het testen API aan [ test uw op dossier-gebaseerde bestemming met steekproefprofielen ](../testing-api/batch-destinations/file-based-destination-testing-api.md).
   * Koppel een voorbeeldbestand dat door uw bestemming is gegenereerd en dat naar uw opslaglocatie is geëxporteerd.
   * Verzend een of andere vorm van bewijs dat u het geëxporteerde bestand van de opslaglocatie naar uw systeem hebt ingevoerd.
* Het bewijs dat u een bestemmings het publiceren verzoek voor uw bestemming gebruikend [ bestemmings het publiceren API ](../publishing-api/create-publishing-request.md) hebt voorgelegd.
* Een documentatie PR (trekkingsverzoek), die de instructies volgen in het [ worden beschreven zelfbediening documentatieproces ](../docs-framework/documentation-instructions.md).
* Een afbeeldingsbestand dat wordt weergegeven als een logo voor uw doelkaart in de catalogus met Experience Platform-doelen.

In de onderstaande secties vindt u gedetailleerde informatie over elk onderdeel:

## Omschrijving hoofdletter gebruiken {#use-case-description}

Geef een beschrijving van de gebruiksgevallen die uw bestemming oplost voor Experience Platform-klanten. Uw beschrijvingen kunnen gelijkaardig zijn aan gebruiksgevallen van bestaande partners:

* [ Pinterest ](/help/destinations/catalog/advertising/pinterest.md): Creeer publiek van uw klantenlijsten, mensen die uw plaats of mensen hebben bezocht die reeds met uw inhoud op Pinterest in wisselwerking staan.
* [ Gegevens X van Yahoo ](/help/destinations/catalog/advertising/datax.md#use-cases): DataX APIs is beschikbaar voor adverteerders die een specifieke publieksgroep willen richten die van e-mailadressen in de Media van de Verizon (VMG) wordt gehouden kan snel een nieuw publiek tot stand brengen en de gewenste publieksgroep duwen gebruikend VMG&#39;s dichtbij-real-time API.

## Reden voor update {#reason-for-update}

>[!NOTE]
>
>Deze sectie is alleen vereist wanneer u een bestaande configuratie bijwerkt.

Geef een korte beschrijving van de kwestie die door uw verzending wordt opgelost voor de bestaande bestemming. Als u bijvoorbeeld een bericht verzendt, worden de naam, beschrijving en het logo van uw bestemming mogelijk bijgewerkt wanneer u overschakelt van bèta naar algemene beschikbaarheid. Of, zou uw voorlegging een insect kunnen bevestigen dat in uw bestemmingsconfiguratie wordt ontdekt.

## Testresultaten na gebruik van de API voor testbestemming {#testing-api-response}

Verstrek testresultaten na het gebruiken van het [ doelAPI ](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) eindpunt om een vraag van HTTP aan uw bestemming uit te voeren. Dit omvat het volgende:

* De volledige API-aanvraag (headers en body) die met de API voor testen is ingediend bij het eindpunt van de bestemming.
* De API reactie die van uw bestemmingshindpunt wordt ontvangen.

Uw verzoek en antwoord zien er bijvoorbeeld ongeveer hetzelfde uit als de onderstaande voorbeelden:

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

**Reactie**

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

Omvat een verzoek en een reactiesteekproef na het gebruiken van het testen API aan [ test uw op dossier-gebaseerde bestemming met steekproefprofielen ](../testing-api/batch-destinations/file-based-destination-testing-api.md).

### Geëxporteerd bestand bijvoegen {#attach-exported-file}

In uw [ voorleggingsE-mail ](#download-sample-email), maak een Csv- dossier vast dat in uw opslagplaats door de bestemming werd uitgevoerd die u opstelling.

### Bewijs van geslaagde inname {#proof-of-successful-ingestion}

Tot slot moet u een of andere vorm van bewijs verstrekken dat de gegevens met succes in uw systeem zijn opgenomen nadat het werd uitgevoerd naar de opslagplaats u verstrekte. Geef hieronder een of meer van de volgende objecten op:

* Screenshots of een korte video van het schermvangst waar u het dossier manueel van de opslagplaats neemt en het in uw systeem opneemt.
* Screenshots of een korte video van het schermvangst waar UI van uw systeem bevestigt dat filename die door Experience Platform wordt geproduceerd met succes in uw systeem werd opgenomen.
* Loglijnen van uw systeem die Adobe kan correleren met de bestandsnaam of met de gegevens die zijn gegenereerd vanuit Experience Platform.

## Bewijs dat u een bestemmings het publiceren verzoek hebt ingediend {#destination-publishing-request-proof}

Na met succes het testen van uw bestemming, moet u [ bestemmings het publiceren API ](../publishing-api/create-publishing-request.md) gebruiken om de bestemming voor overzicht en het publiceren naar Adobe voor te leggen.

Geef de id van de publicatieaanvraag voor uw doel op. Voor informatie over hoe te om te terugwinnen publiceer verzoekidentiteitskaart, leest hoe te [ bestemming terugwinnen publicatieverzoeken ](../publishing-api/retrieve-publishing-request.md).

## Doeldocumentatie PR (pull-request) voor productieve integratie {#documentation-pr}

Als u een Onafhankelijke Verkoper van de Software (ISV) of Integrator van het Systeem (SI) creërend a [ geproduceerde integratie ](../overview.md#productized-custom-integrations) bent, moet u het [ zelfbedienings documentatieproces ](../docs-framework/documentation-instructions.md) gebruiken om een pagina van de productdocumentatie voor uw bestemming tot stand te brengen. Geef als onderdeel van het verzendproces de pull request (PR) voor de doeldocumentatie op.

## Logo voor uw doel {#logo}

De doelcatalogus bevat een logo voor elke doelkaart. Neem in uw e-mailbericht een afbeelding op met het logo voor uw bestemming.

De afbeeldingsvereisten zijn:

* **Formaat**: `SVG`
* **Grootte**: minder dan 2MB

## Voorbeelde-mail downloaden {#download-sample-email}

[ Download ](../assets/guides/sample-email-submit-destination.rtf) een steekproefe-mail met alle informatie die u aan Adobe moet verstrekken.
