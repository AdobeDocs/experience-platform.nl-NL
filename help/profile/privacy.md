---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Privacy-aanvraagverwerking in realtime-klantprofiel
type: Documentation
description: Adobe Experience Platform Privacy Service verwerkt verzoeken van klanten om toegang te krijgen, te weigeren of hun persoonlijke gegevens te verwijderen, zoals gedefinieerd in een groot aantal privacyregels. Dit document behandelt essentiële concepten met betrekking tot de verwerking van privacyverzoeken voor Real-time Klantprofiel.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: a713245f3228ed36f262fa3c2933d046ec8ee036
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 0%

---

# Behandeling van privacyverzoek in [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] verwerkt verzoeken van klanten om toegang tot hun persoonsgegevens, om te weigeren deze te verkopen of om hun persoonsgegevens te verwijderen, zoals bepaald in privacyvoorschriften zoals de algemene gegevensbeschermingsverordening (GDPR), en [!DNL California Consumer Privacy Act] (CCPA).

In dit document worden de belangrijkste concepten besproken die betrekking hebben op de verwerking van verzoeken om privacy voor [!DNL Real-time Customer Profile] in Adobe Experience Platform.

>[!NOTE]
>
>In deze handleiding wordt alleen uitgelegd hoe u privacyverzoeken voor de profielgegevensopslag in Experience Platform kunt indienen. Als u ook privacyverzoeken wilt maken voor het Platform Data Lake, raadpleegt u de handleiding over [verwerking van privacyverzoeken in het Data Lake](../catalog/privacy.md) in aanvulling op deze zelfstudie.
>
>Raadpleeg voor meer informatie over het indienen van privacyverzoeken voor andere Adobe Experience Cloud-toepassingen de [Privacy Service](../privacy-service/experience-cloud-apps.md).

## Aan de slag

U wordt aangeraden het volgende goed te begrijpen: [!DNL Experience Platform] services vóór het lezen van deze handleiding:

* [[!DNL Privacy Service]](../privacy-service/home.md): Beheert verzoeken van klanten om hun persoonlijke gegevens in Adobe Experience Cloud-toepassingen te openen, uit de handel te nemen of te verwijderen.
* [[!DNL Identity Service]](../identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.
* [[!DNL Real-time Customer Profile]](home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## Naamruimten voor identiteiten {#namespaces}

Adobe Experience Platform [!DNL Identity Service] brugt de gegevens van de klantenidentiteit over systemen en apparaten. [!DNL Identity Service] gebruik **naamruimten** context te verschaffen aan identiteitswaarden door deze te koppelen aan hun systeem van oorsprong. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;e-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

De Dienst van de identiteit handhaaft een opslag van globaal bepaalde (standaard) en user-defined (douane) identiteitsnamespaces. Standaard naamruimten zijn beschikbaar voor alle organisaties (bijvoorbeeld E-mail en ECID), terwijl uw organisatie aangepaste naamruimten kan maken die aan de specifieke behoeften voldoen.

Voor meer informatie over naamruimten in [!DNL Experience Platform], zie de [Overzicht van naamruimte in identiteit](../identity-service/namespaces.md).

## Verzoeken indienen {#submit}

In de volgende secties wordt beschreven hoe u privacyverzoeken kunt indienen voor [!DNL Real-time Customer Profile] met de [!DNL Privacy Service] API of UI. Voordat u deze secties leest, wordt u ten zeerste aangeraden de [Privacy Service-API](../privacy-service/api/getting-started.md) of [UI Privacy Service](../privacy-service/ui/overview.md) documentatie voor volledige stappen over hoe te om een privacybaan voor te leggen, met inbegrip van hoe te om ingediende gegevens van de gebruikersidentiteit in verzoek te formatteren lading.

>[!IMPORTANT]
>
>Privacy Service kan alleen verwerken [!DNL Profile] gegevens die een samenvoegbeleid gebruiken dat geen identiteitsstitching uitvoert. Zie de sectie over [beleidsbeperkingen samenvoegen](#merge-policy-limitations) voor meer informatie .
>
>Het is ook belangrijk om op te merken dat de hoeveelheid tijd die een privacyverzoek kan duren om te voltooien niet kan worden gewaarborgd. Als er wijzigingen optreden in uw [!DNL Profile] terwijl een verzoek nog wordt verwerkt, kan ook niet worden gegarandeerd of die gegevens al dan niet worden verwerkt.

### De API gebruiken

Bij het maken van taakaanvragen in de API, alle id&#39;s die binnen `userIDs` moet een specifieke `namespace` en `type`. Een geldige [naamruimte identity](#namespaces) erkend door [!DNL Identity Service] moet worden voorzien in `namespace` waarde, terwijl de `type` moet ofwel `standard` of `unregistered` (voor respectievelijk standaard- en aangepaste naamruimten).

>[!NOTE]
>
>Afhankelijk van de identiteitsgrafiek en de manier waarop uw profielfragmenten in gegevenssets van Platforms worden gedistribueerd, moet u mogelijk meer dan één id opgeven voor elke klant. Zie de volgende sectie [profielfragmenten](#fragments) voor meer informatie .

Bovendien `include` array van de aanvraag payload moet de productwaarden voor de verschillende gegevensopslagruimten bevatten waarnaar de aanvraag wordt verzonden. Als u de profielgegevens wilt verwijderen die aan een identiteit zijn gekoppeld, moet de array de waarde bevatten `ProfileService`. Om de verenigingen van de identiteitsgrafiek van de klant te schrappen, moet de serie de waarde omvatten `identity`.

>[!NOTE]
>
>Zie de sectie over [profielaanvragen en identiteitsverzoeken](#profile-v-identity) later in dit document vindt u gedetailleerde informatie over de effecten van het gebruik van `ProfileService` en `identity` binnen de `include` array.

Met het volgende verzoek wordt een nieuwe privacytaak gemaakt voor de gegevens van één klant in het dialoogvenster [!DNL Profile] opslaan. Er zijn twee identiteitswaarden voor de klant in de `userIDs` array; één met de norm `Email` naamruimte identiteit en de andere naamruimte met behulp van een aangepaste naamruimte `Customer_ID` naamruimte. Het omvat ook de productwaarde voor [!DNL Profile] (`ProfileService`) in de `include` array:

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
>Platform verwerkt privacyverzoeken voor alle [sandboxen](../sandboxes/home.md) die deel uitmaken van uw organisatie. Dientengevolge, om het even welke `x-sandbox-name` header die in de aanvraag is opgenomen, wordt genegeerd door het systeem.

### De gebruikersinterface gebruiken

Zorg ervoor dat u bij het maken van taakaanvragen in de gebruikersinterface **[!UICONTROL AEP Data Lake]** en/of **[!UICONTROL Profile]** krachtens **[!UICONTROL Products]** om taken te verwerken voor gegevens die zijn opgeslagen in de [!DNL Data Lake] of [!DNL Real-time Customer Profile], respectievelijk.

![Een verzoek van de toegangstaak die in UI wordt gecreeerd, met de optie van het Profiel die onder Producten wordt geselecteerd](./images/privacy/product-value.png)

## Profielfragmenten in privacyverzoeken {#fragments}

In de [!DNL Profile] gegevensopslag, de persoonlijke gegevens voor een individuele klant zullen vaak van veelvoudige profielfragmenten bestaan, die met de persoon door de identiteitsgrafiek worden geassocieerd. Bij het indienen van privacyverzoeken bij de [!DNL Profile] Opslaan, is het belangrijk om op te merken dat verzoeken slechts op profiel-fragment niveau, eerder dan het volledige profiel worden verwerkt.

Bijvoorbeeld, overweeg een situatie waar u de gegevens van de klantenattributen in drie afzonderlijke datasets opslaat, die verschillende herkenningstekens gebruiken om die gegevens met individuele klanten te associëren:

| Naam gegevensset | Primair identiteitsveld | Opgeslagen kenmerken |
| --- | --- | --- |
| Dataset 1 | `customer_id` | `address` |
| Gegevensset 2 | `email_id` | `firstName`, `lastName` |
| Gegevensset 3 | `email_id` | `mlScore` |

Een van de gegevenssets gebruikt `customer_id` als primair identificatiemiddel, terwijl de andere twee `email_id`. Als u een privacyverzoek (toegang of verwijdering) alleen wilt verzenden met `email_id` als de gebruiker-id-waarde, alleen de `firstName`, `lastName`, en `mlScore` kenmerken worden verwerkt, terwijl `address` niet worden beïnvloed.

Om ervoor te zorgen dat uw privacyverzoeken alle relevante klantenattributen verwerken, moet u de primaire identiteitswaarden voor alle toepasselijke datasets verstrekken waar die attributen (tot een maximum van negen IDs per klant) kunnen worden opgeslagen. Zie de sectie over identiteitsvelden in de [grondbeginselen van de schemacompositie](../xdm/schema/composition.md#identity) voor meer informatie over velden die algemeen als identiteiten zijn gemarkeerd.

## Verzoek om verwerking verwijderen {#delete}

Wanneer [!DNL Experience Platform] ontvangt een verwijderingsverzoek van [!DNL Privacy Service], [!DNL Platform] stuurt bevestiging naar [!DNL Privacy Service] dat het verzoek is ontvangen en de betrokken gegevens zijn gemarkeerd voor verwijdering. De records worden vervolgens verwijderd uit de [!DNL Data Lake] of [!DNL Profile] opslaan nadat de privacytaak is voltooid. Hoewel de verwijdertaak nog steeds wordt verwerkt, worden de gegevens via de elektronische weg verwijderd en zijn ze daarom door niemand toegankelijk [!DNL Platform] service. Zie de [[!DNL Privacy Service] documentatie](../privacy-service/home.md#monitor) voor meer informatie over het bijhouden van de taakstatus.

In toekomstige versies [!DNL Platform] stuurt bevestiging naar [!DNL Privacy Service] nadat de gegevens fysiek zijn verwijderd.

### Profielaanvragen versus identiteitsverzoeken {#profile-v-identity}

Als een verwijderaanvraag is ingediend voor Profiel (`ProfileService`) maar niet identiteitsdienst (`identity`), verwijdert de resulterende baan de verzamelde kenmerkgegevens voor een klant (of een reeks klanten) maar verwijdert niet de verenigingen die in de identiteitsgrafiek worden gevestigd.

Bijvoorbeeld, een schrappingsverzoek dat een klant gebruikt `email_id` en `customer_id` verwijdert alle kenmerkgegevens die onder die id&#39;s zijn opgeslagen. Gegevens die daarna onder dezelfde `customer_id` nog steeds in verband worden gebracht met `email_id`, aangezien de associatie nog steeds bestaat.

Om het profiel en alle identiteitskoppelingen voor een bepaalde klant te verwijderen, zorg ervoor om zowel de Dienst van het Profiel als van de Identiteit als doelproducten in uw schrappingsverzoeken te omvatten.

### Beleidsbeperkingen samenvoegen {#merge-policy-limitations}

Privacy Service kan alleen verwerken [!DNL Profile] gegevens die een samenvoegbeleid gebruiken dat geen identiteitsstitching uitvoert. Als u de UI gebruikt om te bevestigen of uw privacyverzoeken worden verwerkt, zorg ervoor dat u een beleid gebruikt met **[!DNL None]** als [!UICONTROL ID stitching] type. Met andere woorden, u kunt geen samenvoegbeleid gebruiken waarbij [!UICONTROL ID stitching] is ingesteld op [!UICONTROL Private graph].
>![De ID-instelling van het samenvoegbeleid is ingesteld op Geen](./images/privacy/no-id-stitch.png)
>
## Volgende stappen

Door dit document te lezen, hebt u kennis gemaakt met de belangrijke concepten voor het verwerken van privacyverzoeken in [!DNL Experience Platform]. U wordt aangeraden de documentatie in deze handleiding te blijven lezen om meer inzicht te krijgen in de manier waarop u identiteitsgegevens kunt beheren en privacytaken kunt maken.

Voor informatie over het verwerken van privacyverzoeken voor [!DNL Platform] middelen die niet worden gebruikt door [!DNL Profile], zie het document op [verwerking van privacyverzoeken in het Data Lake](../catalog/privacy.md).
