---
title: Audience Validation
description: Leer hoe Experience Platform uw publiek valideert om ervoor te zorgen dat ze verder stroomafwaarts presteren.
source-git-commit: 52439e55d3c48631488b17b6b04256bcbbe37bcb
workflow-type: tm+mt
source-wordcount: '1630'
ht-degree: 0%

---


# Validatie van publiek

Wanneer u een publieksdefinitie in Adobe Experience Platform schrijft, biedt publieksvalidatie ingebouwde validaties en instructies om ervoor te zorgen dat uw publiek niet alleen nauwkeurig, maar ook stabiel en schaalbaar is.

Door zich aan de beste praktijken van de publieksdefinitie te houden, verzekert u uw publiek sneller kan evalueren, uw logica efficiënt blijft zelfs wanneer uw publieksgrootte groeit, en het risico van evaluatiestoornissen tijdens hoog-verkeersperiodes vermindert. Geoptimaliseerd publiek verbetert ook de activeringssnelheid voor doelen, vermindert realtime personalisatielatentie en behoudt de algehele stabiliteit van de sandbox.

Experience Platform voert deze validaties in real time uit aangezien u uw publiek in de Bouwer van het Segment bouwt. Wanneer u gebeurtenissen of attributen toevoegt die bevestigingsdrempels overschrijden, ontvangt u direct binnen de interface van de Bouwer van het Segment terugkoppelen.

## Validatietypen {#validation-types}

Wanneer de publieksbevestiging op uw publiek loopt, zijn er twee verschillende types van concepten die kunnen worden geschonden: Kritieke bevestigingsconcepten en de constructies van de prestatiesoptimalisering.

Als een kritieke validatie wordt overtreden, voorkomt het systeem dat u uw publiek opslaat om de stabiliteit van uw sandbox te beschermen. Als een constructie van de prestatiesoptimalisering wordt geschonden, zult u uw publiek kunnen bewaren, maar het wordt *hoogst geadviseerd* u werkt uw publieksdefinitie bij om prestatieskwesties te vermijden.

## Validatiecontroles {#validation-checks}

Momenteel worden de volgende validaties ondersteund:

| Validatiecontrole | Type | Drempel |
| ---------------- | ---- | --------- |
| Logische complexiteit | Kritieke validatie | De publieksdefinitie bevat te veel query&#39;s, wat leidt tot onnodige logische complexiteit. |
| Opeenvolgende gebeurtenissen | Kritieke validatie | Er zijn meer dan zes opeenvolgende gebeurtenissen binnen een publieksdefinitie. |
| Geaggregeerd aantal | Optimalisatie van prestaties | Er zijn meer dan 3 samenvoegingsfuncties binnen een publieksdefinitie. |
| Geneste gegevens | Optimalisatie van prestaties | Er zijn meer dan 2 niveaus van genestelde gegevensdiepte (serie of kaartgegevenstypes) binnen een publieksdefinitie. |
| Grootte publiek | Optimalisatie van prestaties | De kwalificatiegrootte van het publiek is groter dan 30% van het totale aantal profielen in de sandbox. |

### [!BADGE &#x200B; Kritieke bevestiging &#x200B;]{type=Negative} Logische ingewikkeldheid {#logical-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_rewritescheck"
>title="Efficiëntie van query, waarschuwing"
>abstract="Uw publiek bevat te veel query&#39;s, wat leidt tot onnodige logische complexiteit. Vereenvoudig de definitie van uw publiek voordat u verdergaat."

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_cnfcomplexitycheck"
>title="Logische complexiteit"
>abstract="Uw publiek bevat te veel query&#39;s, wat leidt tot onnodige logische complexiteit. Vereenvoudig de definitie van uw publiek voordat u verdergaat."

De logische complexiteitsbevestiging analyseert de structuur van uw logische verklaringen (EN, OF, NIET) binnen uw publieksdefinitie. Meer bepaald zoekt het naar publieksdefinities die het systeem dwingen een buitensporig aantal vergelijkingen per profiel uit te voeren.

Als uw publieksdefinitie een bovenmatig aantal vergelijkingen per profiel heeft, leidt deze toegenomen complexiteit tot een langzamere evaluatie per profiel. Hierdoor neemt de algemene tijd voor de evaluatie van het publiek toe.

Als u wilt voorkomen dat deze validatie wordt geactiveerd, houdt u de publieksdefinitie eenvoudig. Als je je eigen publieksdefinitie niet begrijpt, is het te ingewikkeld en kan Experience Platform langer duren om het publiek te evalueren.

**Voorbeeld**

Laten we zeggen dat u klanten wilt vinden die in bepaalde staten wonen. U _kon_ dit inefficiënt schrijven door te controleren om te zien of heeft het profiel de waarde voor een staat die één van de vermelde 45 waarden aanpast, als volgt:

+++ Inefficiënte publieksdefinitie

```
State.equals("AL", "AK", "AZ", "AR", "CA", "CO", "CT", "DE", "FL", "GA","HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC", "SD", "TN", "TX", "UT")
```

+++

Als u echter een niet-controle gebruikt, hoeft u alleen te controleren of het profiel geen van de vijf vermelde waarden heeft. Dit leidt tot een veel efficiëntere query.

+++ Efficiënte publieksdefinitie

```
not(State.equals("VT", "VA", "WA", "WV", "WI", "WY" ))
```

+++

Alternatief, zeggen wij u klanten wilt vinden die Canadezen op uw proefplan zijn. Een minder efficiënte benadering zou zijn om Canadezen op uw proefplan te zoeken door elk ander plan manueel uit te sluiten, één voor één, en te controleren dat het profiel in geen van hen is.

+++ Inefficiënte publieksdefinitie

```
NOT(
    plan.equals("basic") OR
    plan.equals("standard") OR
    plan.equals("premium") OR
    plan.equals("enterprise")
) AND NOT (
    region.equals("us-east") OR
    region.equals("us-west") OR
    region.equals("eu-central") OR
    region.equals("apac")
)
```

+++

In plaats daarvan, zou u direct moeten zijn en het specifieke plan richten u wilt omvatten.

+++ Efficiënte publieksdefinitie

```
plan.equals("trial") AND region.equals("canada")
```

+++

### [!BADGE &#x200B; Kritieke bevestiging &#x200B;]{type=Negative} Opeenvolgende gebeurtenisingewikkeldheid {#sequential-event-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_chaincountcheck"
>title="Limiet voor gebeurtenisreeksen"
>abstract="Uw publiek bevat te veel opeenvolgende gebeurtenissen. U kunt maximaal zes opeenvolgende gebeurtenissen binnen uw publieksdefinitie hebben. Verwijder enkele opeenvolgende gebeurtenissen uit de definitie van uw publiek voordat u doorgaat."

Door de validatie van de complexiteit van opeenvolgende gebeurtenissen wordt het aantal opeenvolgende gebeurtenissen in een reeks beperkt tot 6 gebeurtenissen.

Opeenvolgende segmentatie is een van de meest computationeel gecompliceerde bewerkingen binnen Experience Platform, aangezien het systeem de gehele geschiedenis van Experience Events van een klant moet scannen, deze op tijdstempel moet sorteren en moet controleren of de opgegeven volgorde overeenkomt met uw query. Als gevolg hiervan moet het aantal permutaties dat het systeem moet berekenen drastisch stijgen wanneer de keten groeit.

Als u wilt voorkomen dat deze validatie wordt geactiveerd, richt u zich op de grondbeginselen van uw sequentiële keten door het begin, midden en einde van de rit te definiëren. Directe stappen worden vaak geïmpliceerd binnen de definitieve omzetting.

**Voorbeeld**

Laten we zeggen dat u gebruikers wilt aanspreken die een product hebben bekeken, het aan het winkelwagentje hebben toegevoegd en het hebben gekocht. Een minder efficiënte benadering zou elke individuele staat van de weg van de gebruiker controleren. De volgende query doorloopt bijvoorbeeld deze reeks gebeurtenissen: Aanmelden bij website -> Zoeken naar product -> Weergaven van een productpagina -> Toevoegen aan winkelwagentje -> Navigeert naar uitchecken -> Aankoopgebeurtenis

+++ Inefficiënte publieksdefinitie

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "login"), B: WHAT(eventType = "search"), C: WHAT(eventType = "productView"), D: WHAT(eventType = "addToCart"), E: WHAT(eventType = "checkout"), F: WHAT(eventType = "purchase") ])
```

+++

Nochtans, door de opeenvolging aan zijn begin, midden, en eind te verminderen, moet u slechts een opeenvolging van gebeurtenissen hebben die 3 lange gebeurtenissen is, resulterend in een efficiëntere vraag. De volgende query doorloopt bijvoorbeeld deze reeks gebeurtenissen: geeft een productpagina weer -> Toevoegen aan winkelwagentje -> Aankoopgebeurtenis

+++ Efficiënte publieksdefinitie

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "productView"), B: WHAT(eventType = "addToCart"), C: WHAT(eventType = "purchase") ])
```

+++

### [!BADGE &#x200B; optimalisering van Prestaties &#x200B;]{type=Caution} Geaggregeerde telling {#aggregated-count}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_countaggregationcheck"
>title="Waarschuwing bij telfilter"
>abstract="Uw publiek heeft te veel samenvoegingsgebeurtenissen. Gebruik maximaal 3 samenvoegingsgebeurtenissen voor uw publiek. Om prestatieskwesties te vermijden, zou u sommige samenvoegingsgebeurtenissen uit uw publieksdefinitie moeten verwijderen."

De geaggregeerde tellingcontrole beperkt het aantal aggregatiegebeurtenissen dat binnen uw publiek wordt gebruikt tot drie voorwaarden.

Een standaardgebeurtenis hoeft slechts één overeenkomende gebeurtenis te vinden om een gebruiker in aanmerking te laten komen. Nochtans, moet een samenvoegingsgebeurtenis de volledige geschiedenis van een gebruiker **&#x200B;**&#x200B;van gebeurtenissen lezen en analyseren alvorens het een besluit kan nemen, die tot langzamere verwerkingstijden met meer gebruikte samenvoegingsgebeurtenissen leiden.

Als u wilt voorkomen dat deze validatie wordt geactiveerd, gebruikt u alleen specifieke tellingen wanneer dit strikt noodzakelijk is voor de publieksdefinitie. Als u alleen hoeft te weten of een gebruiker zich eenmaal heeft aangemeld, kunt u bijvoorbeeld de standaardlogica ‘Exists’ gebruiken in plaats van een gebeurtenis ‘Count > 0’ te gebruiken.

### [!BADGE &#x200B; optimalisering van Prestaties &#x200B;]{type=Caution} Geneste gegevenscomplexiteit {#nested-data-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_arraydepthcheck"
>title="Waarschuwing: geneste gegevens"
>abstract="Uw publiek heeft te veel geneste gegevenslagen. Gebruik maximaal twee lagen gegevens in uw publiek. Om prestatieskwesties te vermijden, zou u uw publieksdefinitie moeten afvlakken."

Door de validatie van de geneste gegevenscomplexiteit wordt het aantal geneste gegevens binnen een publieksdefinitie beperkt tot twee lagen.

Hoewel Experience Platform het gebruik van array- en kaartobjecten voor de opslag van complexe gegevenstypen ondersteunt, is het voor het uitpakken van geneste structuren om een waarde te vinden complexere traversale logica vereist. De diepere gegevens worden genest in een serie, langer het duurt om voor bevestiging terug te winnen.

Als u vaak segmentatie op een diep genest attribuut uitvoert, kunt u uw team van de gegevenstechniek moeten contacteren om de attributen aan een hoger niveau binnen het profielschema voor gemakkelijkere toegang te kopiëren.

### [!BADGE &#x200B; Grootte van het publiek van de optimalisering van prestaties 0&rbrace;]{type=Caution} {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_profilestorecheck"
>title="Waarschuwing Doelgrootte"
>abstract="Uw publiek is te breed geschreven. U moet voorkomen dat u een publieksdefinitie schrijft die meer dan 30% van de totale profielen in uw sandbox kwalificeert. Om prestatieskwesties te vermijden, zou u uw publieksdefinitie moeten aanscherpen."

De validatie van de publieksgrootte controleert of de publieksdefinitie zo breed is dat meer dan 30% van de totale profielen in uw sandbox in aanmerking komt voor het publiek.

Hoewel Experience Platform grote doelgroepen kan verwerken, kan een te vage publieksdefinitie (zoals Alle actieve klanten) de evaluatietijd en de activeringslatentie verhogen.

Als u een publiek moet creëren dat meer dan 30% van uw profielopslag kwalificeert, zorg ervoor dat de eerste evaluatie van het publiek gebruikend flexibele publieksevaluatie wordt gedaan. Als u het publiek evalueert met een evaluatie op aanvraag, kan dit de algemene impact van een groot publiek op de dagelijkse segmentatietaak verminderen.

## Volgende stappen

Na het lezen van deze handleiding hebt u meer inzicht in hoe Experience Platform automatische validaties uitvoert om evaluatie, stabiliteit en schaalbaarheid te verbeteren. Voor meer informatie bij het creëren van publiek gebruikend UI, lees de [&#x200B; documentatie van de Bouwer van het Segment &#x200B;](./ui/segment-builder.md).

## Bijlage

In de volgende bijlage worden veelgestelde vragen over publieksvalidatie in Experience Platform weergegeven.

### Veelgestelde vragen {#faq}

**wat gebeurt als ik de waarschuwingen negeer en het publiek bewaart?**

+++ Antwoord

Voor waarschuwingen voor optimalisatie van de prestaties wordt het publiek opgeslagen en probeert het systeem het te evalueren. Het kan echter zijn dat de verwerkingstijd aanzienlijk langzamer wordt. In extreme situaties, als het gegevensvolume hoog genoeg is, kan de segmentatietaak ontbreken of tijd uit, dwingend u om uw publiek opnieuw te ontwerpen.

Voor kritieke validatiefouten kunt u het publiek niet opslaan.

+++

**kan ik om een verhoging aan de &quot;Opeenvolgende grens van de Gebeurtenis&quot;verzoeken?**

+++ Antwoord

Nee, dat kan niet. Dit is een harde garantie die bedoeld is om de stabiliteit van de hele Experience Platform-omgeving te beschermen. Als uw opeenvolging meer dan 6 stappen vereist, is het een sterke indicator dat de logica of in twee verschillende soorten publiek (zoals een publiek van de &quot;Betrokkenheid&quot;en een &quot;publiek van de Omzetting&quot;zou moeten worden vereenvoudigd of worden gebroken).

+++

**zullen deze nieuwe bevestigingen mijn bestaand publiek breken?**

+++ Antwoord

Deze bevestigingen lopen in de tijd van **creatie**. Als gevolg hiervan zullen uw bestaande doelgroepen blijven functioneren zoals ze zijn. Als u echter probeert een bestaand publiek te bewerken dat deze regels overtreedt, moet u het optimaliseren voordat u de wijzigingen kunt opslaan.

+++

**ik heb complexe gegevensvereisten. Hoe kan ik de waarschuwing &quot;Geneste Gegevens&quot;vermijden?**

+++ Antwoord

Het vermijden van de waarschuwing &quot;Geneste gegevens&quot; kunt u het beste oplossen op de modelleerlaag voor gegevens. Enkele tips zijn onder andere het werken met uw team voor gegevensengineering om uw XDM-schema af te vlakken en kritieke kenmerken (zoals `subscriptionStatus` en `loyaltyTier` ) naar het hoofdniveau van het profiel te brengen.

+++

**zullen deze controles op zowel Ontwerp als Gepubliceerd publiek van toepassing zijn?**

+++ Antwoord

Ja, zijn deze controles op *van toepassing alle* publiek dat in Experience Platform wordt geëvalueerd.

+++
