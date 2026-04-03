---
title: Verenigde identiteitssteun in de Inzameling van Gegevens
description: Leer hoe de verenigde identiteitssteun eerste-partijpersistentie en gesteunde activering van derde samen in Webgegevensinzameling brengt.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 32c2565d31eed4eda28195afaf82aac6f04a6f8a
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 2%

---

# Verenigde identiteitssteun in de Inzameling van Gegevens

>[!AVAILABILITY]
>
>Deze functie is momenteel in bèta. De beschikbaarheid, het gedrag en de documentatie kunnen veranderen.

Met Unified Identity Support kan de Edge Network zowel in de context van de identiteit van de eerste partij als van derden werken. Het combineert een duurzame identificatie van de eerste partij op uw bezittingen met de werkschema&#39;s van de derde activering in browsers die derdekoekjes steunen. Voor achtergrond op hoe het Web SDK ECIDs, FPIDs, en andere identiteitssignalen behandelt, zie [&#x200B; Identiteit in de Inzameling van Gegevens &#x200B;](./overview.md).

Met de verenigde identiteitssteun, kunt u:

* **maximaliseer publieksbereik**: Activeer uw publiek van Experience Platform op derdebestemmingen (DSPs, SSPs, en netwerken) voor een groter aandeel van uw verkeer.
* **handhaaf metingsnauwkeurigheid**: Houd verenigbare bezoekersidentificatie over uw bezeten eigenschappen en reclameplatforms.
* **Toekomstbestendig uw implementatie**: Gebruik eerstepartijapparaat IDs als uw stichting terwijl het handhaven van verenigbaarheid met derdeactiveringswerkschema&#39;s.

Wanneer een bezoeker op uw site arriveert, evalueert de Edge Network automatisch beschikbare identiteitssignalen: context van eerste en derde partijen koppelen wanneer de omstandigheden dit toestaan. Browsers die cookies van derden blokkeren, blijven in de modus van de eerste partij werken zonder dat de implementatie wordt onderbroken.

## Werking

De Edge Network genereert ECID&#39;s door de beschikbare identiteitssignalen in de volgende prioriteitsvolgorde te evalueren:

| Prioriteit | Bron | Context | Gedrag |
| --- | --- | --- | --- |
| 1 | **Identiteitskaart van de Demping** | Derden | Als er een demdex-id aanwezig is, wordt de ECID ervan afgevoerd. Dit zaad veroorzaakt verenigbare ECID over domeinen die het zelfde derdekoekje delen. |
| 2 | **FPID** | Eerste partij | Als er geen demdex-id aanwezig is maar er wel een FPID bestaat, wordt de ECID van de FPID afgevoerd en wordt er een demdex-id van afgeleid. |
| 3 | **Random** | Eerste partij | Als noch een demdex-id noch een FPID beschikbaar is, wordt een nieuwe willekeurige ECID gegenereerd en wordt er een demdex-id uit afgeleid. |

ECID&#39;s en demdex-id&#39;s zijn cryptografisch gekoppeld via een deterministisch algoritme, wat betekent dat het ene kan worden afgeleid van het andere. Deze relatie maakt het de Edge Network mogelijk om tussen identiteitscontexten van eerste en van derde partijen te vertalen zonder dat u in uw implementatie aparte logica voor het afhandelen van bezoekers hoeft te gebruiken.

Omdat de relatie deterministisch is, kunnen publiek dat op eerste-partij ECIDs wordt voortgebouwd door derdeinfrastructuur worden geactiveerd wanneer overeenkomstige identiteitskaart van de Index beschikbaar is.

Voor bezoekers die al een door FPID afgeleide ECID hebben, kan de Edge Network hun identiteit van de eerste partij automatisch koppelen aan de context van de externe identiteit. Dit gebeurt transparant wanneer browser derdekoekjes steunt en geen veranderingen in uw implementatie vereist. Wanneer er sprake is van automatische koppelingen:

1. De Edge Network detecteert dat de ECID van de bezoeker niet is afgeleid van een demdex-id.
1. Als de browser van de bezoeker cookies van derden ondersteunt, wordt een lichte synchronisatie van de identiteit geactiveerd.
1. Het systeem maakt een koppeling tussen de eerste-partij-ECID van de bezoeker en hun identiteit van derden.
1. De koppeling wordt opgeslagen in het identiteitsarchief, zodat het publiek zich kan activeren op andere bestemmingen.

Bij automatische koppelingen blijven bestaande ECID&#39;s behouden en wordt het knippen van bezoekers voorkomen. In de loop der tijd komt een groter deel van het publiek geleidelijk in aanmerking voor activering door derden wanneer bezoekers terugkeren en een koppeling tot stand brengen.

De activering van het publiek van derden is afhankelijk van ID-synchronisatie (id-synchronisatie). Wanneer de Edge Network een identiteit van een derde vaststelt of vernieuwt, worden in de reactie instructies voor het synchroniseren van de id geretourneerd. Deze instructies leiden browser om de identiteit van de bezoeker met partnerdomeinen (DSPs, en netwerken, en andere activeringsplatforms) te synchroniseren, zodat uw publiek van Experience Platform op die platforms kan worden aangepast en worden geleverd.

## Vereisten

De verenigde identiteitssteun vereist elk van het volgende:

* Uw plaats gebruikt de inzameling van eerste-partijgegevens op een domein u controleert.
* Uw implementatie gebruikt FPID&#39;s of een andere persistentiestrategie van een eerste partij als basis.
* Cookies van andere leveranciers worden ingeschakeld in uw Web SDK-configuratie.
* Identiteitssynchronisatie van derden is ingeschakeld voor de gegevensstroom.
* De bezoeker gebruikt browser die derdekoekjes toestaat (zie [&#x200B; hieronder Browserverenigbaarheid 0&rbrace;).](#browser-compatibility)

## Configuratie

1. **laat derdekoekjes in SDK van het Web** toe: Laat **de derdekoekjes van het Gebruik** plaatsen in uw implementatie van SDK van het Web toe. Als het gebruiken van de markeringsuitbreiding, laat **[!UICONTROL Use third-party cookies]** in [&#x200B; de configuratiemontages van de Identiteit &#x200B;](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies) toe. Als u de JavaScript-bibliotheek gebruikt, stelt u [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md) in op `true` .

1. **laat de synchronisatie van derdeidentiteitskaart in de datastream** toe: laat de **[!UICONTROL Third-Party ID Sync]** optie in de geavanceerde montages van uw gegevensstroom toe. Zie [&#x200B; gegevensstromen &#x200B;](/help/datastreams/configure.md#advanced-options) creëren en vormen.

1. **zorg ervoor dat de persistentie van de eerste partij op zijn plaats** is: bevestig dat uw strategie van de eerste-partijpersistentie (zoals FPIDs) reeds op uw bezeten domein wordt opgesteld. Zie [&#x200B; Eerste partij apparaat IDs in de Inzameling van Gegevens &#x200B;](fpid.md).

## Validatie

Controleren of Unified Identity-ondersteuning werkt:

1. Open de de ontwikkelaarshulpmiddelen van uw browser en navigeer aan het **Netwerk** lusje.
1. Wis bestaande verzoeken en activeer een gebeurtenis van SDK van het Web (paginading of douanegebeurtenis) in een nieuwe of incognitozitting.
1. Vind de reactie van Edge Network (zoek vraag aan `adobedc.demdex.net` en uw eerste-partijinzamelingseindpunt).
1. Controleer de payload van de reactie op ID-synchronisatieinstructies.

Wanneer ID-synchronisatieinstructies aanwezig zijn, bevat de reactie een `identity:exchange` -greep die vergelijkbaar is met het volgende:

```json
{
  "handle": [
    {
      "type": "identity:exchange",
      "payload": [
        {
          "type": "url",
          "id": 411,
          "spec": {
            "url": "https://example.com/...",
            "hideReferrer": false,
            "ttlMinutes": 10080
          }
        },
        {
          "type": "url",
          "id": 89,
          "spec": {
            "url": "https://example.org/...",
            "hideReferrer": true,
            "ttlMinutes": 10080
          }
        }
      ]
    }
  ]
}
```

| Element | Beschrijving |
| --- | --- |
| `type: "identity:exchange"` | Geeft aan dat er instructies voor ID-synchronisatie aanwezig zijn. |
| `payload` array | Lijst met URL&#39;s voor synchronisatie van partner-id. |
| `url` waarden | Omleiden URLs aan partnerdomeinen voor de synchronisatie van identiteitskaart |
| `id` waarden | Partner-id&#39;s. |

>[!TIP]
>
>Als u de `identity:exchange` -greep niet ziet in het antwoord:
>
>* Zorg ervoor dat u test met een nieuwe of incognito-browsersessie. Bestaande identiteiten activeren geen nieuwe syncs.
>* Verifieer dat zowel de gegevensstroom als de montages van SDK van het Web correct worden gevormd.
>* Bevestig dat u browser gebruikt die derdekoekjes steunt (zie de lijst hieronder).

Na bevestiging van ID synchronisatieactiviteit, bevestig dat:

* De identiteit van de eerste partij blijft zoals verwacht bij het laden van de pagina op uw eigen domein.
* De activerings- en rapportstromen gedragen zich zoals u had verwacht in de omgevingen die u ondersteunt.

## Browsercompatibiliteit {#browser-compatibility}

Identiteitsfuncties van derden zijn afhankelijk van browserondersteuning voor cookies van andere leveranciers. De volgende tabel geeft een overzicht van het verwachte gedrag:

| Browser | Ondersteuning voor cookies van andere bedrijven | Demdex beschikbaar | Identiteitsgedrag |
| --- | --- | --- | --- |
| Google Chrome | Ondersteund | Ja | Demdex → ECID (consistent in verschillende domeinen) |
| Microsoft Edge | Standaard ondersteund | Ja | Demdex → ECID (consistent in verschillende domeinen) |
| Mozilla Firefox | Standaard geblokkeerd (ETP) | Nee (standaard) | FPID → ECID (per domein) |
| Apple Safari | Geblokkeerd (ITP) | Nee | FPID → ECID (per domein) |

Voor browsers die cookies van derden blokkeren, werkt de identificatie van de eerste partij nog steeds normaal. Activeringsfuncties van derden zijn alleen beschikbaar wanneer de browser cookies van derden toestaat.

## Beperkingen

* Identiteitsgedrag van derden is volledig afhankelijk van de browser van de bezoeker die cookies van derden toestaat. Er is geen fallback voor activering door derden in browsers die deze blokkeren.
* Voor automatische koppelingen moet de bezoeker terugkeren naar de site. Het aandeel van uw publiek dat in aanmerking komt voor activering door derden neemt geleidelijk toe.
