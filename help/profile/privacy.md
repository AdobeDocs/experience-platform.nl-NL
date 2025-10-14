---
keywords: Experience Platform;startpagina;populaire onderwerpen
solution: Experience Platform
title: Privacy-aanvraagverwerking in realtime-klantprofiel
type: Documentation
description: Adobe Experience Platform Privacy Service verwerkt verzoeken van klanten om toegang te krijgen, te weigeren of hun persoonlijke gegevens te verwijderen, zoals gedefinieerd in een groot aantal privacyregels. Dit document behandelt essentiële concepten met betrekking tot de verwerking van privacyverzoeken voor Real-Time Klantprofiel.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: 6eaa384feb1b84e6081f03cb4de9687ad26f437d
workflow-type: tm+mt
source-wordcount: '1746'
ht-degree: 0%

---

# Behandeling van privacyaanvraag in [!DNL Real-Time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] verwerkt verzoeken van klanten om toegang te krijgen tot, zich uit de verkoop te sluiten van of hun persoonsgegevens te verwijderen, zoals is vastgelegd in privacyregels zoals de General Data Protection Regulation (GDPR) en [!DNL California Consumer Privacy Act] (CCPA).

In dit document worden de belangrijkste concepten besproken die betrekking hebben op het verwerken van privacyverzoeken voor [!DNL Real-Time Customer Profile] in Adobe Experience Platform.

>[!NOTE]
>
>In deze handleiding wordt alleen uitgelegd hoe u privacyaanvragen kunt indienen voor de profielgegevensopslag in Experience Platform. Als u ook van plan bent om privacyverzoeken voor het de gegevensmeer van Experience Platform te maken, verwijs naar de gids over [&#x200B; verwerking van het privacyverzoek in het gegevens meer &#x200B;](../catalog/privacy.md) naast dit leerprogramma.
>
>Voor stappen op hoe te om privacyverzoeken voor andere toepassingen van Adobe Experience Cloud te maken, verwijs naar de [&#x200B; documentatie van Privacy Service &#x200B;](../privacy-service/experience-cloud-apps.md).

>[!IMPORTANT]
>
>Het privacyverzoek in deze gids **&#x200B;**&#x200B;behandelt geen B2B niet-persoonentiteiten.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende [!DNL Experience Platform] -componenten:

* [[!DNL Privacy Service]](../privacy-service/home.md): Beheert verzoeken van klanten om toegang te krijgen tot, uit de verkoop te stappen of hun persoonlijke gegevens te verwijderen in Adobe Experience Cloud-toepassingen.
* [[!DNL Identity Service]](../identity-service/home.md): lost de fundamentele uitdaging op die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.
* [[!DNL Real-Time Customer Profile]](home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

## Naamruimten voor identiteiten {#namespaces}

Adobe Experience Platform [!DNL Identity Service] biedt een brug tussen identiteitsgegevens van klanten op systemen en apparaten. [!DNL Identity Service] gebruikt **identiteit namespaces** om context aan identiteitswaarden te verstrekken door hen op hun systeem van oorsprong met elkaar in verband te brengen. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;E-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

De Dienst van de identiteit handhaaft een opslag van globaal bepaalde (standaard) en user-defined (douane) identiteitsnamespaces. Standaard naamruimten zijn beschikbaar voor alle organisaties (bijvoorbeeld E-mail en ECID), terwijl uw organisatie aangepaste naamruimten kan maken die aan de specifieke behoeften voldoen.

Voor meer informatie over identiteit namespaces in [!DNL Experience Platform], zie het [&#x200B; overzicht van identiteitskaart namespace &#x200B;](../identity-service/features/namespaces.md).

## Verzoeken indienen {#submit}

In de onderstaande secties wordt beschreven hoe u privacyverzoeken voor [!DNL Real-Time Customer Profile] kunt indienen met de API of UI van [!DNL Privacy Service] . Alvorens deze secties te lezen, zou u moeten herzien, of zich bewust zijn van, [&#x200B; Privacy Service API &#x200B;](../privacy-service/api/getting-started.md) of [&#x200B; Privacy Service UI &#x200B;](../privacy-service/ui/overview.md) documentatie. Deze documenten bevatten volledige stappen voor het verzenden van een privacytaak, waaronder het correct indelen van verzonden identiteitsgegevens van gebruikers in aanvragen voor nuttige taken.

>[!IMPORTANT]
>
>Privacy Service kan [!DNL Profile] -gegevens alleen verwerken met behulp van een samenvoegbeleid dat geen identiteitsstitching uitvoert. Zie de sectie over [&#x200B; de beperkingen van het samenvoegingsbeleid &#x200B;](#merge-policy-limitations) voor meer informatie.
>
>Merk op dat de privacyverzoeken asynchroon binnen de regelgevende vereisten worden verwerkt, en de hoeveelheid tijd die zij om nemen te voltooien kan variëren. Als er wijzigingen optreden in uw [!DNL Profile] -gegevens terwijl een aanvraag nog wordt verwerkt, is het niet zeker dat die inkomende records ook in dat verzoek worden verwerkt. Alleen profielen die zich op het moment dat de privacytaak wordt aangevraagd in het archief met gegevens of profielen bevinden, kunnen worden verwijderd. Als u profielgegevens opgeeft die betrekking hebben op het onderwerp van een verwijderingsverzoek tijdens de verwijdertaak, is het niet gegarandeerd dat alle profielfragmenten worden verwijderd.
>Het is uw verantwoordelijkheid om op de hoogte te zijn van binnenkomende gegevens in Experience Platform of de Dienst van het Profiel op het tijdstip van een verwijderingsverzoek, aangezien die gegevens in uw verslagopslag zullen worden opgenomen. U moet voorzichtig zijn met het opnemen van gegevens die zijn verwijderd of worden verwijderd.

### De API gebruiken

Bij het maken van taakaanvragen in de API moeten alle id&#39;s in `userIDs` een specifieke `namespace` en `type` gebruiken. Een geldige [&#x200B; identiteitskaart namespace &#x200B;](#namespaces) die door [!DNL Identity Service] wordt erkend moet voor de `namespace` waarde worden verstrekt, terwijl `type` of `standard` of `unregistered` (voor standaard en douanenaamruimten, respectievelijk) moet zijn.

>[!NOTE]
>
>U moet mogelijk meer dan één id opgeven voor elke klant, afhankelijk van de identiteitsgrafiek en de manier waarop uw profielfragmenten worden gedistribueerd in Experience Platform-gegevenssets. Zie de volgende sectie [&#x200B; profielfragmenten &#x200B;](#fragments) voor meer informatie.

Bovendien moet de `include` -array van de payload van de aanvraag de productwaarden voor de verschillende gegevensopslagruimten bevatten waarnaar de aanvraag wordt verzonden. Als u de profielgegevens wilt verwijderen die aan een identiteit zijn gekoppeld, moet de array de waarde `ProfileService` bevatten. Als u de identiteitsgrafiekkoppelingen van de klant wilt verwijderen, moet de array de waarde `identity` bevatten.

>[!NOTE]
>
>Zie de sectie over [&#x200B; profielverzoeken en identiteitsverzoeken &#x200B;](#profile-v-identity) later in dit document voor meer gedetailleerde informatie over de gevolgen van het gebruiken van `ProfileService` en `identity` binnen de `include` serie.

Met de volgende aanvraag wordt een nieuwe privacytaak gemaakt voor de gegevens van één klant in de [!DNL Profile] Store. Er worden twee identiteitswaarden opgegeven voor de klant in de array `userIDs` ; een die de standaardnaamruimte `Email` identity gebruikt en een andere die een aangepaste naamruimte `Customer_ID` gebruikt. De methode bevat ook de productwaarde voor [!DNL Profile] (`ProfileService`) in de array `include` :

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "Email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "Customer_ID",
            "value": "12345678",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService","identity"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>Experience Platform verwerkt privacyverzoeken over alle [&#x200B; zandbakken &#x200B;](../sandboxes/home.md) die tot uw organisatie behoren. Als gevolg hiervan wordt elke `x-sandbox-name` -header die in de aanvraag is opgenomen, genegeerd door het systeem.

**reactie van het Product**

Als de privacytaak eenmaal is voltooid, wordt een antwoord in JSON-indeling geretourneerd met informatie over de aangevraagde gebruikers-id&#39;s.

```json
{
    "privacyResponse": {
        "jobId": "7467850f-9698-11ed-8635-355435552164",
        "response": [
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "female"           
                    },
                    "personalEmail": {
                        "address": "ajones@acme.com",
                    },
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "5b7db37a-bc7a-46a2-a63e-2cfe7e1cc068"
                            }
                        ]
                    }
                }
            },
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "male"
                    },
                    "id": 12345678,
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "e9d439f2-f5e4-4790-ad67-b13dbd89d52e"
                            }
                        ]
                    }
                }
            }
        ]
    }
}
```

### UI gebruiken

Wanneer u taakaanvragen maakt in de gebruikersinterface, moet u **[!UICONTROL AEP Data Lake]** en/of **[!UICONTROL Profile]** under **[!UICONTROL Products]** selecteren om taken te verwerken voor respectievelijk gegevens die in het gegevenspeer of [!DNL Real-Time Customer Profile] zijn opgeslagen.

![&#x200B; een verzoek van de toegangstaak die in UI, met de optie van het Profiel wordt gecreeerd onder Producten &#x200B;](./images/privacy/product-value.png) wordt geselecteerd

## Profielfragmenten in privacyverzoeken {#fragments}

In de [!DNL Profile] gegevensopslag, zullen de persoonlijke gegevens voor een individuele klant vaak van veelvoudige profielfragmenten bestaan, die met de persoon door de identiteitsgrafiek worden geassocieerd. Wanneer u een privacyaanvraag indient bij de [!DNL Profile] -winkel, is het belangrijk om te weten dat aanvragen alleen op profielfragmentniveau worden verwerkt en niet op het hele profiel.

Bijvoorbeeld, overweeg een situatie waar u de gegevens van de klantenattributen in drie afzonderlijke datasets opslaat, die verschillende herkenningstekens gebruiken om die gegevens met individuele klanten te associëren:

| Naam gegevensset | Primair identiteitsveld | Opgeslagen kenmerken |
| --- | --- | --- |
| Dataset 1 | `customer_id` | `address` |
| Gegevensset 2 | `email_id` | `firstName`, `lastName` |
| Gegevensset 3 | `email_id` | `mlScore` |

Een van de gegevenssets gebruikt `customer_id` als primaire id, terwijl de andere twee `email_id` gebruiken. Als u een privacyaanvraag (access or delete) alleen met `email_id` als waarde voor de gebruikers-id wilt verzenden, worden alleen de kenmerken `firstName` , `lastName` en `mlScore` verwerkt, terwijl `address` niet wordt beïnvloed.

Om ervoor te zorgen dat uw privacyverzoeken alle relevante klantenattributen verwerken, moet u de primaire identiteitswaarden voor alle toepasselijke datasets verstrekken waar die attributen (tot een maximum van negen IDs per klant) kunnen worden opgeslagen. Zie de sectie over identiteitsgebieden in de [&#x200B; grondbeginselen van schemacompositie &#x200B;](../xdm/schema/composition.md#identity) voor meer informatie over gebieden die algemeen als identiteiten worden gemerkt.

## Verzoek om verwerking verwijderen {#delete}

Wanneer [!DNL Experience Platform] een verwijderaanvraag ontvangt van [!DNL Privacy Service] , stuurt [!DNL Experience Platform] een bevestiging naar [!DNL Privacy Service] dat de aanvraag is ontvangen en de desbetreffende gegevens zijn gemarkeerd voor verwijdering. De records worden vervolgens verwijderd nadat de privacytaak is voltooid.

>[!IMPORTANT]
>
>De verzoeken om privacy te schrappen zijn niet onmiddellijk en kunnen variëren afhankelijk van de betrokken diensten en andere beïnvloedende factoren zoals geografische plaats. De termijn voor het voltooien van privacytaken kan variëren van 15 tot 45 dagen, maar wordt niet gegarandeerd.

Afhankelijk van of u ook de Dienst van de Identiteit (`identity`) en het gegevens meer (`aepDataLake`) als producten in uw privacyverzoek voor Profiel (`ProfileService`) omvatte, worden de verschillende reeksen gegevens met betrekking tot het profiel verwijderd uit het systeem op potentieel verschillende tijden:

| Producten inbegrepen | Effecten |
| --- | --- |
| alleen `ProfileService` | Het profiel wordt onmiddellijk als verwijderd beschouwd zodra Privacy Service de bevestiging verzendt dat het verwijderingsverzoek is voltooid. De identiteitsgrafiek van het profiel blijft echter ongewijzigd en het profiel kan mogelijk opnieuw worden samengesteld als nieuwe gegevens met dezelfde identiteiten worden opgenomen. De niet-persoonlijk identificeerbare gegevens verbonden aan het profiel blijven ook in het gegevensmeer. |
| `ProfileService` en `identity` | Het profiel en de bijbehorende identiteitsgrafiek worden onmiddellijk verwijderd zodra Privacy Service de bevestiging verzendt dat het verwijderingsverzoek is voltooid. De niet-persoonlijk identificeerbare gegevens verbonden aan het profiel blijven ook in het gegevensmeer. |
| `ProfileService` en `aepDataLake` | Het profiel wordt onmiddellijk verwijderd zodra Privacy Service de bevestiging verzendt dat het verwijderingsverzoek is voltooid. De identiteitsgrafiek van het profiel blijft echter ongewijzigd en het profiel kan mogelijk opnieuw worden samengesteld als nieuwe gegevens met dezelfde identiteiten worden opgenomen.<br><br> wanneer het product van het gegevensmeerproduct antwoordt dat het verzoek werd ontvangen en momenteel verwerkt, worden de gegevens verbonden aan het profiel soft-deleted en daarom niet toegankelijk door om het even welke [!DNL Experience Platform] dienst. Zodra de baan wordt voltooid, worden de gegevens volledig verwijderd uit het gegevens meer. |
| `ProfileService` , `identity` en `aepDataLake` | Het profiel en de bijbehorende identiteitsgrafiek worden onmiddellijk verwijderd zodra Privacy Service de bevestiging verzendt dat het verwijderingsverzoek is voltooid.<br><br> wanneer het product van het gegevensmeerproduct antwoordt dat het verzoek werd ontvangen en momenteel verwerkt, worden de gegevens verbonden aan het profiel soft-deleted en daarom niet toegankelijk door om het even welke [!DNL Experience Platform] dienst. Zodra de baan wordt voltooid, worden de gegevens volledig verwijderd uit het gegevens meer. |

Verwijs naar de [[!DNL Privacy Service]  documentatie &#x200B;](../privacy-service/home.md#monitor) voor meer informatie bij het volgen van baanstatussen.

### Profielaanvragen versus identiteitsverzoeken {#profile-v-identity}

Als een schrappingsverzoek voor Profiel (`ProfileService`) maar niet de Dienst van de Identiteit (`identity`) wordt gemaakt, verwijdert de resulterende baan de verzamelde attributengegevens voor een klant (of reeks klanten) maar verwijdert niet de verenigingen die in de identiteitsgrafiek worden gevestigd.

Een verwijderingsaanvraag die de namen `email_id` en `customer_id` van een klant gebruikt, verwijdert bijvoorbeeld alle kenmerkgegevens die onder die id&#39;s zijn opgeslagen. Gegevens die daarna onder dezelfde `customer_id` worden ingevoerd, worden echter nog steeds gekoppeld aan de juiste `email_id` , omdat de koppeling nog steeds bestaat.

Om het profiel en alle identiteitskoppelingen voor een bepaalde klant te verwijderen, zorg ervoor om zowel de Dienst van het Profiel als van de Identiteit als doelproducten in uw schrappingsverzoeken te omvatten.

### Beleidsbeperkingen samenvoegen {#merge-policy-limitations}

Privacy Service kan [!DNL Profile] -gegevens alleen verwerken met behulp van een samenvoegbeleid dat geen identiteitsstitching uitvoert. Als u de interface gebruikt om te bevestigen of uw privacyverzoeken worden verwerkt, controleert u of u een beleid gebruikt met **[!DNL None]** als [!UICONTROL ID stitching] -type. Met andere woorden, u kunt geen samenvoegbeleid gebruiken waarbij [!UICONTROL ID stitching] is ingesteld op [!UICONTROL Private graph] .

>![&#x200B; ID het stitching van het fusiebeleid wordt geplaatst aan niets &#x200B;](./images/privacy/no-id-stitch.png)

## Volgende stappen

Door dit document te lezen, hebt u kennis genomen van de belangrijke concepten voor het verwerken van privacyverzoeken in [!DNL Experience Platform] . Als u meer inzicht wilt in de manier waarop u identiteitsgegevens kunt beheren en privacytaken kunt maken, blijft u de documentatie in deze handleiding lezen.

Voor informatie bij de behandeling van privacyverzoeken voor [!DNL Experience Platform] middelen die niet door [!DNL Profile] worden gebruikt, zie het document over [&#x200B; verwerking van de privacyaanvraag in het gegevens meer &#x200B;](../catalog/privacy.md).
