---
title: Kevel-verbinding
description: Gebruik het Kevel-streamingdoel om het publiek rechtstreeks in de API's van UserDB en Segmentbeheer van Kevel te activeren en realtime gericht op de beslissingstijd te ondersteunen.
source-git-commit: d820485fd81efd08d8626f8476338558c4585c20
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 1%

---


# [!DNL Kevel]-verbinding {#kevel}

## Overzicht {#overview}

[[!DNL Kevel] &#x200B;](https://www.kevel.com/) verstrekt de AI-Toegelaten technologie en deskundige begeleiding die innovatieve handelsleiders helpen lanceren, schrapen, en slagen in handelsmedia. De Retail Media Cloud-bevoegdheden van [!DNL Kevel] zijn gericht op, aanpasbare en aanpasbare advertentievormen voor on-site en off-site reclame.

Met de [!DNL Kevel] streamingbestemming voor Adobe Experience Platform kunnen klanten Adobe-doelgroepen rechtstreeks activeren in de gebruikersdatabase- en segmentbeheerAPI&#39;s van [!DNL Kevel] voor ondersteuning van realtime doelwitten tijdens de besluitvorming.

>[!IMPORTANT]
> 
>Als u vragen hebt of een update betreffende de [!DNL Kevel] bestemming of zijn documentatie zou willen verzoeken, gelieve het [!DNL Kevel] team in [&#x200B; support@kevel.com &#x200B;](mailto:support@kevel.com) te e-mailen.

## Gebruiksscenario’s {#use-cases}

U kunt een rijk toonaangevend publiek met gedragingen in al uw mediabelessen in de detailhandel activeren voor meer relevante advertenties en betere prestaties. In Experience Platform maakt u een publiek met hoge waarden en intenties, zoals veelvuldige categorieconcerns of gebruikers met recent productbelang, en synchroniseert u deze abonnementen in realtime met [!DNL Kevel] . [!DNL Kevel] maakt deze segmenten onmiddellijk beschikbaar voor ad-hocbesluitvorming, zodat u ze exact kunt richten op gesponsorde producten en andere indelingen voor alle zoekacties, browsers en apps. Zodra de gebruikers kwalificeren, kunt u op deze signalen in werking stellen om relevantere beelden, beter te richten, en betere meting en ROAS te drijven.

## Vereisten {#prerequisites}

Als u zich wilt voorbereiden op het gebruik van het [!DNL Kevel] -doel, moet aan de volgende voorwaarden worden voldaan:

- U moet een actieve **[!DNL Kevel]netwerk** en API toegang hebben.
- U hebt een **[!DNL Kevel]API sleutel** met toestemmingen nodig om segmenten tot stand te brengen en verslagen bij te werken UserDB.
- U moet naamruimten in Experience Platform configureren die zijn toegewezen aan de identiteiten die uw site of toepassing tijdens [!DNL Kevel] -advertentieverzoeken verzendt (bijvoorbeeld ECID, GAID, IDFA, loyalty-id, enz.).
- Adobe-klanten dienen alleen identiteiten toe te wijzen die tijdens realtime-advertentieverzoeken worden gebruikt, aangezien elke identiteit resulteert in een UserDB-record.

## Ondersteunde identiteiten {#supported-identities}

Het doel van [!DNL Kevel] ondersteunt activering voor elke identiteit die uw toepassing kan gebruiken bij het verzenden van advertentieverzoeken naar [!DNL Kevel] . U kunt maximaal drie naamruimten toewijzen om overeenkomstige UserDB-records te genereren.

[!DNL Kevel] ondersteunt de volgende Experience Platform-naamruimten:

| Naamruimte identiteit | Beschrijving | Normaal gebruik |
|--------------------|---------------------------------|----------------------------------------------------------------|
| **ECID** | Experience Cloud-id | Wordt gebruikt voor onsite personalisatie en cross-Adobe-identificatie. |
| **GAID** | GOOGLE ADVERTISING ID | Wordt gebruikt voor Android-app/apparaatverkeer. |
| **IDFA** | APPLE ADVERTISING ID | Wordt gebruikt voor iOS-app/apparaatverkeer (afhankelijk van ATT-toestemming). |
| **EXTERNAL_ID** | Externe id (aangepaste id) | Geeft gedeponeerde of door back-end gegenereerde id&#39;s door. |

{style="table-layout:auto"}

### Ondersteuning voor aangepaste naamruimten

De [!DNL Kevel] bestemming **keurt ook douane namespaces** goed, zoals die in uw implementatie van Experience Platform wordt bepaald.

Dit betekent:

- U kunt **klant-specifieke identiteitsnamespaces** in kaart brengen (bijvoorbeeld: `loyalty_id`, `gigya_id`, of om het even welke douaneidentiteit u in de Dienst van de Identiteit hebt bepaald).
- Deze naamruimten kunnen op dezelfde manier worden toegewezen aan `kevel_user_key1` , `kevel_user_key2` of `kevel_user_key3` als algemene naamruimten.
- [!DNL Kevel] zal **één verslag UserDB per geval van elke in kaart gebrachte identiteit** produceren, toestaand aanpassing in real time bij ad-beslissingstijd voor elk herkenningsteken uw systemen verzenden.

### Identiteitskaartgedrag

- U kunt **tot drie** identiteitsnamespaces van Experience Platform aan [!DNL Kevel] drie identiteitsgroeven in kaart brengen.
- Voor elk geactiveerd profiel, [!DNL Kevel] ontvangt **één verslag UserDB per geval van elke in kaart gebrachte identiteit**.
- Klanten dienen alleen identiteiten toe te wijzen die ze daadwerkelijk verzenden en aanvragen naar [!DNL Kevel] om onnodige opslag van de UserDB te voorkomen.

![&#x200B; het Voorbeeld van de Afbeelding voor KevelBestemming &#x200B;](/help/destinations/assets/catalog/advertising/kevel-destination-mappings.png)

## Ondersteunde doelgroepen {#supported-audiences}

| Oorsprong publiek | Ondersteund | Beschrijving |
|-----------------------|-----------|---------------------------------------------------------- |
| Segmentatieservice | Ja | Adobe Profile publiek dat door de segmenteringsmotor wordt geëvalueerd. |
| Aangepaste uploads | Nee | Momenteel niet ondersteund. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

| Item | Type | Notities |
|------|------|-------|
| Exporttype | **de uitvoer van het Segment** | [!DNL Kevel] ontvangt een update wanneer een profiel in aanmerking komt voor een publiek of dit sluit. |
| Exportfrequentie | **Streaming** | Updates worden in real-time verzonden via het Destination SDK-streamingframework. |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

Volg standaardExperience Platform [&#x200B; verbinden een bestemmings &#x200B;](../../ui/connect-destination.md) werkschema.

>[!IMPORTANT]
> 
>U moet **Doelen van de Mening** hebben en **leidt de toestemmingen van Doelen**.

### Verifiëren voor bestemming {#authenticate}

Geef het volgende veld op wanneer u verbinding maakt met [!DNL Kevel] :

- **het teken van de Drager** - Uw [!DNL Kevel] API sleutel.

![&#x200B; de opties van de Authentificatie voor KevelBestemming &#x200B;](/help/destinations/assets/catalog/advertising/kevel-destination-authentication.png)

### Doelgegevens invullen {#destination-details}

Na verificatie configureren:

- **Naam** — Een etiket om deze bestemmingsinstantie te identificeren.
- **Beschrijving** — Facultatieve tekst om deze bestemmingsinstantie te beschrijven.
- **[!DNL Kevel]Netwerk-id** — Uw [!DNL Kevel] netwerk-id.

![&#x200B; de details van de Bestemming voor KevelBestemming &#x200B;](/help/destinations/assets/catalog/advertising/kevel-destination-details.png)

## Segmenten naar dit doel activeren {#activate}

Als u een publiek naar [!DNL Kevel] wilt sturen, volgt u de workflow in\
[&#x200B; activeer profielen en segmenten aan het stromen segment de uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Deactivering van het publiek {#deactivate}

Wanneer een publiek in Experience Platform wordt gedeactiveerd of verwijderd van het [!DNL Kevel] -doel, stopt Experience Platform met het verzenden van verdere kwalificatieupdates voor profielen voor dat publiek. Bestaande segmenten die in [!DNL Kevel] zijn gemaakt, blijven beschikbaar en worden niet automatisch verwijderd.

Als het [!DNL Kevel] -segment momenteel wordt gebruikt in een actieve campagne, voorkomt [!DNL Kevel] verwijdering om onderbreking van de live levering te voorkomen. In dit geval leidt deactivering in Experience Platform tot het volgende:

- De Experience Platform-gegevensstroom wordt gestopt
- Het segment [!DNL Kevel] blijft bestaan en blijft mogelijk gekoppeld aan campagnes totdat u de campagne handmatig verwijdert of bijwerkt

Als u het afwijzen van doelen in [!DNL Kevel] volledig wilt beëindigen, moet u ervoor zorgen dat het segment wordt verwijderd uit actieve campagnes in het campagnebeheersysteem van [!DNL Kevel] .

### Kenmerken en identiteiten toewijzen {#map}

[!DNL Kevel] vereist:

- **Identiteitsnaamruimten** - tot drie identiteitsnaamruimten in kaart gebracht aan [!DNL Kevel] identiteitsgroeven.
- **lidmaatschap van het Segment** — Geen handmatige vereiste afbeelding; Experience Platform gaat automatisch de herkenningstekens en aliassen van het segmentlidmaatschap over.

Selecteer tijdens de activering de naamruimten waarvoor u [!DNL Kevel] hebt geconfigureerd. Elke identiteit zal zijn eigen de updatevraag van UserDB produceren.

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Wanneer een profiel in aanmerking komt voor of een publiek verlaat, verzendt Experience Platform een streamingupdate naar [!DNL Kevel] .

### Voorbeeld ontvangen door [!DNL Kevel] UserDB

```json
PUT /udb/{networkId}/segments?userKey=ECID-12345
{
  "segments": [1723, 3344, 9988]
}
```

| Parameter | Beschrijving |
|-----------|-------------|
| **userKey** | Voortgekomen uit de toegewezen Adobe-identiteit. |
| **segmenten** | De set met [!DNL Kevel] segment-id&#39;s die overeenkomen met het Adobe-publiek waarvoor het profiel momenteel wordt uitgevoerd. |

{style="table-layout:auto"}

### Voorbeeld van Experience Platform-profiel dat tijdens exporteren wordt gebruikt {#sample-profile}

Wanneer het activeren van publiek aan de [!DNL Kevel] bestemming, verzendt Experience Platform profielfragmenten die zowel **segmentkwalificaties** en **identiteiten bevatten die door de klant** aan [!DNL Kevel] de identiteitsgroeven van de klant worden in kaart gebracht.

Hieronder ziet u een voorbeeld van een geëxporteerd profiel met:

- Meerdere naamruimten toegewezen aan `kevel_user_key1` , `kevel_user_key2` en `kevel_user_key3`
- Eén geactiveerd segment in de naamruimte `ups`

```json
{
  "segmentMembership": {
    "ups": {
      "9d161bbb-c785-474a-965b-7d7bc2adf879": {
        "status": "realized",
        "lastQualificationTime": "2025-12-10T21:43:38.541076Z"
      }
    }
  },
  "identityMap": {
    "kevel_user_key1": [
      {
        "id": "ECID-fN1zo"
      },
      {
        "id": "ECID-9Xr2p"
      }
    ],
    "kevel_user_key2": [
      {
        "id": "GAID-4oic4"
      }
    ],
    "kevel_user_key3": [
      {
        "id": "IDFA-nB5fU"
      }
    ]
  }
}
```

#### Hoe [!DNL Kevel] dit profiel interpreteert

Met de [!DNL Kevel] doelconfiguratie genereert elke toegewezen identiteit een afzonderlijke UserDB-record, wat betekent dat [!DNL Kevel] ontvangt:

- Eén update voor `ECID-fN1zo`
- Eén update voor `ECID-9Xr2p`
- Eén update voor `GAID-4oic4`
- Eén update voor `IDFA-nB5fU`

Hierdoor kan dezelfde persoon op het tijdstip van de beslissing worden erkend met behulp van een van zijn beschikbare identiteiten, waarbij elke identiteit een identieke reeks segmentlidmaatschappen heeft.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

- [[!DNL Kevel]  Referentie UserDB &#x200B;](https://dev.kevel.com/reference/userdb)
- [[!DNL Kevel]  Doelgericht Gebruikerssegment &#x200B;](https://dev.kevel.com/docs/segment-targeting)
