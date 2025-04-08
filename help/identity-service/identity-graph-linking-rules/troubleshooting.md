---
title: De Gids van het oplossen van problemen voor de Regels van de Verbinding van de Grafiek van de Identiteit
description: Leer hoe te om gemeenschappelijke kwesties in identiteitsgrafiek problemen op te lossen die regels verbinden.
exl-id: 98377387-93a8-4460-aaa6-1085d511cacc
source-git-commit: 0e7911e21c546fb40cd51f03a5a6d6a2aa751dec
workflow-type: tm+mt
source-wordcount: '3331'
ht-degree: 0%

---

# Handleiding voor het oplossen van problemen met koppelingsregels voor identiteitsgrafieken

>[!AVAILABILITY]
>
>De regels voor identiteitsgrafiekkoppelingen zijn momenteel in Beperkte Beschikbaarheid. Neem contact op met uw Adobe-accountteam voor informatie over hoe u toegang kunt krijgen tot de functie in ontwikkelingssandboxen.

Wanneer u regels voor identiteitsgrafieken test en valideert, kan er een aantal problemen optreden die te maken hebben met gegevensinvoer en grafiekgedrag. Lees dit document om te leren hoe te om sommige gemeenschappelijke kwesties problemen op te lossen die u zou kunnen ontmoeten wanneer het werken met identiteitsgrafiek die regels verbindt.

## Overzicht gegevensinvoer {#data-ingestion-flow-overview}

Het volgende diagram is een vereenvoudigde weergave van hoe gegevens stromen naar Adobe Experience Platform en Toepassingen. Gebruik dit diagram als verwijzing om u te helpen een beter inzicht in de inhoud van deze pagina krijgen.

![ een diagram van hoe de gegevensopname in de Dienst van de Identiteit stroomt.](../images/troubleshooting/dataflow_in_identity.png)

Het is van belang de volgende factoren in aanmerking te nemen:

* Voor het stromen gegevens, zal het Profiel van de Klant in real time, de Dienst van de Identiteit, en het gegevenspeer beginnen de gegevens te verwerken wanneer de gegevens worden verzonden. Nochtans, is de latentie om de verwerking van de gegevens te voltooien afhankelijk van de dienst. Doorgaans duurt het langer om gegevens in een meer gegevens te verwerken dan bij Profiel en Identiteit.
   * Als de gegevens niet verschijnen wanneer het runnen van een vraag tegen een dataset zelfs na een paar uren, dan is het waarschijnlijk dat de gegevens niet in Experience Platform werden opgenomen.
* Voor partijgegevens, zullen alle gegevens eerst in gegevens meer stromen, dan zullen de gegevens aan Profiel en Identiteit worden verspreid als de dataset voor Profiel en Identiteit wordt toegelaten.
* Voor op inname betrekking hebbende kwesties, is het belangrijk dat de kwestie op een dienst-niveau voor nauwkeurige het zuiveren en het oplossen van problemen wordt geïsoleerd. Er zijn drie mogelijke typen problemen die in overweging moeten worden genomen:

| Type congestieprobleem | Worden de gegevens opgenomen in het data Lake? | Worden de gegevens opgenomen in Profiel? | Worden de gegevens opgenomen in Identity Service? |
| --- | --- | --- | --- |
| Algemene ingestie | Nee | Nee | Nee |
| Grafiekkwestie | Ja | Ja | Nee |
| Probleem met profielfragment | Ja | Nee | Ja |

## Problemen met gegevensinvoer {#data-ingestion-issues}

>[!NOTE]
>
>* Deze sectie veronderstelt dat de gegevens met succes in gegevens meer zijn opgenomen en dat er geen syntaxis of andere fouten waren die de gegevens zouden verhinderen in Experience Platform in de eerste plaats worden opgenomen.
>
>* In de voorbeelden wordt ECID gebruikt als de cookie-naamruimte en CRMID als de naamruimte voor personen.

### Mijn identiteiten worden niet opgenomen in de identiteitsservice{#my-identities-are-not-getting-ingested-into-identity-service}

Er zijn verschillende redenen waarom dit zou kunnen gebeuren, waaronder, maar niet beperkt tot:

* [ De dataset wordt niet toegelaten voor Profiel ](../../catalog/datasets/enable-for-profile.md).
* De record wordt overgeslagen omdat de gebeurtenis slechts één identiteit bevat.
* [ de bevestigingsmislukking van A kwam in de Dienst van de Identiteit voor ](../guardrails.md#identity-value-validation).
   * Een ECID kan bijvoorbeeld langer zijn dan 38 tekens.
* Door gebrek, [ worden AIDs geblokkeerd van opname ](../guardrails.md#identity-namespace-ingestion).
* De identiteit wordt verwijderd wegens [ systeemgidsen ](../guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated).

Binnen de context van identiteitsgrafiek die regels verbindt, kan een verslag van de Dienst van de Identiteit worden verworpen omdat de inkomende gebeurtenis twee of meer identiteiten met zelfde unieke namespace maar verschillende identiteitswaarde heeft. Dit scenario gebeurt gewoonlijk als gevolg van implementatiefouten.

Overweeg het volgende evenement met twee veronderstellingen:

1. De veldnaam CRMID is gemarkeerd als een identiteit met de naamruimte CRMID.
2. De naamruimte-CRMID wordt gedefinieerd als een unieke naamruimte.

De volgende gebeurtenis retourneert een foutbericht waarin wordt aangegeven dat inname is mislukt.

<!-- because the ingestion of this erroneous event would have resulted in graph collapse. In the following event, two entities (Alice and Bob) are both associated with the same namespace (CRMID). -->

```json
{ 
  "_id": "random_string", 
  "eventType": "web browsing event", 
  "identityMap": { 
    "ECID": [ 
      { 
        "id": "11111111111111111111111111111111111111", 
        "primary": false 
      } 
    ], 
    "CRMID": [ 
      { 
        "id": "Alice", 
        "primary": true 
      } 
    ] 
  }, 
  "CRMID": "Bob", 
  "timestamp": "2024-08-17T15:22:51+00:00", 
  "web": { 
    "webPageDetails": { 
      "URL": "https://www.adobe.com/acrobat.html", 
      "name": "Adobe Acrobat" 
    } 
  } 
} 
```

**de stappen van het Oplossen van problemen**

Om deze fout op te lossen, moet u eerst de volgende informatie verzamelen:

* De identiteitswaarde (`identity_value`) u verwachtte om in de identiteitsgrafiek worden opgenomen.
* De dataset (`dataset_name`) waarin de gebeurtenis binnen werd verzonden.

Daarna, gebruik [ de Dienst van de Vraag van Adobe Experience Platform ](../../query-service/home.md) en stel de volgende vraag in werking:

>[!TIP]
>
>Vervang `dataset_name` en `identity_value` door de gegevens die u hebt verzameld.

```sql
  SELECT key, col.id as identityValue, timestamp, _id, identityMap, * 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id = 'identity_value' 
```

Nadat u de query hebt uitgevoerd, zoekt u de gebeurtenisrecord die u had verwacht om een grafiek te genereren en controleert u vervolgens of de identiteitswaarden in dezelfde rij verschillend zijn. Bekijk de volgende afbeelding voor een voorbeeld:

![ een naamloze vraag die in gedupliceerde namespaces resulteerde.](../images/troubleshooting/duplicated_unique_namespace.png)

>[!NOTE]
>
>Als de twee identiteiten precies hetzelfde zijn en als de gebeurtenis via streaming wordt opgenomen, wordt de identiteit door zowel Identiteit als Profiel gededupliceerd.

### Ervaring na verificatieGebeurtenissen worden toegeschreven aan het verkeerde geverifieerde profiel

De prioriteit Namespace speelt een belangrijke rol in hoe de gebeurtenisfragmenten primaire identiteit bepalen.

* Zodra u hebt gevormd en uw [ identiteitsmontages ](./identity-settings-ui.md) voor een bepaalde zandbak opgeslagen, zal het Profiel dan [ namespace prioriteit ](namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events) gebruiken om de primaire identiteit te bepalen. In het geval van identityMap gebruikt Profile de markering `primary=true` niet meer.
* Hoewel Profiel niet langer naar deze markering verwijst, kunnen andere services op Experience Platform de markering `primary=true` blijven gebruiken.

Opdat [ voor authentiek verklaarde gebruikersgebeurtenissen ](implementation-guide.md#ingest-your-data) aan de persoon worden gebonden namespace, moeten alle voor authentiek verklaarde gebeurtenissen de persoon namespace (CRMID) bevatten. Dit betekent dat zelfs nadat een gebruiker zich aanmeldt, de naamruimte van de persoon nog steeds aanwezig moet zijn op elke geverifieerde gebeurtenis.

U kunt de markering `primary=true` &#39;events&#39; blijven zien wanneer u een profiel opzoekt in de profielviewer. Dit wordt echter genegeerd en wordt niet gebruikt door Profiel.

HULP&#39;s worden standaard geblokkeerd. Daarom als u de [ bronVerbinding van Adobe Analytics ](../../sources/tutorials/ui/create/adobe-applications/analytics.md) gebruikt, moet u ervoor zorgen dat ECID aan hoger dan ECID wordt voorrang gegeven zodat de unauthenticated gebeurtenissen een primaire identiteit van ECID zullen hebben.

**de stappen van het Oplossen van problemen**

1. Om te bevestigen dat de voor authentiek verklaarde gebeurtenissen zowel de persoon als koekjesnamespace bevatten, lees de stappen die in de sectie over [ worden geschetst het oplossen van problemenfouten betreffende gegevens die niet aan de Dienst van de Identiteit worden opgenomen ](#my-identities-are-not-getting-ingested-into-identity-service).
2. Om te bevestigen dat de voor authentiek verklaarde gebeurtenissen de primaire identiteit van de persoon namespace (b.v. CRMID) hebben, onderzoek persoonnamespace op profielkijker gebruikend het geen-aaneenschakeling fusiebeleid (dit is het fusiebeleid dat geen privé grafiek gebruikt). Deze zoekopdracht retourneert alleen gebeurtenissen die zijn gekoppeld aan de naamruimte van de persoon.

### Mijn ervaring is dat gebeurtenisfragmenten niet in het profiel worden opgenomen {#my-experience-event-fragments-are-not-getting-ingested-into-profile}

Er zijn verschillende redenen die ertoe bijdragen waarom uw ervaringsfragmenten niet in Profiel worden opgenomen, met inbegrip van maar niet beperkt tot:

* [ De dataset wordt niet toegelaten voor Profiel ](../../catalog/datasets/enable-for-profile.md).
* [ de bevestigingsmislukking van A kan op Profiel ](../../xdm/classes/experienceevent.md) zijn voorgekomen.
   * Een ervaringsgebeurtenis moet bijvoorbeeld zowel een `_id` als een `timestamp` bevatten.
   * Bovendien moet `_id` uniek zijn voor elke gebeurtenis (record).

In de context van naamruimteprioriteit weigert Profiel elke gebeurtenis die twee of meer identiteiten met de hoogste naamruimteprioriteit bevat. Als GAID bijvoorbeeld niet is gemarkeerd als een unieke naamruimte en als er twee identiteiten zijn binnengekomen met een GAID-naamruimte en er verschillende identiteitswaarden zijn binnengekomen, worden de gebeurtenissen niet opgeslagen in Profiel.

**de stappen van het Oplossen van problemen**

Als uw gegevens worden verzonden naar gegevens het meer, maar niet het Profiel, en u gelooft dat dit toe te schrijven aan het verzenden van twee of meer identiteiten met de hoogste namespaceprioriteit in één enkele gebeurtenis is, dan kunt u de volgende vraag in werking stellen om te bevestigen dat er twee verschillende identiteitswaarden tegen zelfde namespace worden verzonden:

>[!TIP]
>
>Bij de volgende query&#39;s moet u:
>
>* Vervang `_testimsorg.identification.core.email` door het pad dat de identiteit verzendt.
>* Vervang `Email` door de naamruimte met de hoogste prioriteit. Dit is dezelfde naamruimte die niet wordt opgenomen.
>* Vervang `dataset_name` door de dataset die u wenst om te vragen.

```sql
  SELECT identityMap, key, col.id as identityValue, _testimsorg.identification.core.email, _id, timestamp 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id != _testimsorg.identification.core.email and key = 'Email' 
```

Bij deze query wordt ervan uitgegaan dat:

* Eén identiteit wordt verzonden vanuit de identityMap en een andere identiteit wordt verzonden vanuit een identiteitsbeschrijving. **NOTA**: In de schema&#39;s van het Gegevensmodel van de Ervaring (XDM), is de identiteitsbeschrijver het gebied duidelijk als identiteit.
* De CRMID wordt verzonden via identityMap. Als de CRMID als gebied wordt verzonden, verwijder `key='Email'` uit WHERE clausule.

>[!NOTE]
>
>**op implementatie WebSDK en ECID duplicatie**: Als het ECID gebied als identiteit (identiteitsbeschrijver) in plaats van identityMap duidelijk is, dan wordt tweede ECID geproduceerd in identityMap. Door deze duplicatie kan worden voorkomen dat anonieme gebeurtenissen worden opgeslagen in het Real-Time Klantprofiel, omdat twee ECID&#39;s in één gebeurtenis aanwezig zijn.

## Problemen met grafiekgedrag {#graph-behavior-related-issues}

In deze sectie worden algemene problemen beschreven die u kunt tegenkomen met betrekking tot het gedrag van de identiteitsgrafiek.

### Unauthenticated ExperienceEvents worden gekoppeld aan het verkeerde geverifieerde profiel

Het algoritme van de identiteitsoptimalisering zal [ de onlangs gevestigde verbindingen respecteren en de oudste verbindingen ](./identity-optimization-algorithm.md#identity-optimization-algorithm-details) verwijderen. Daarom is het mogelijk dat, zodra deze functie is ingeschakeld, ECID&#39;s opnieuw van de ene persoon naar de andere worden toegewezen (opnieuw gekoppeld). Volg onderstaande stappen om te begrijpen hoe een identiteit in de loop der tijd gekoppeld wordt:

**de stappen van het Oplossen van problemen**

>[!NOTE]
>
>De volgende stappen zullen informatie onder de volgende veronderstellingen terugwinnen:
>
>* Één enkele dataset is in gebruik (dit zal niet veelvoudige datasets) vragen.
>
>* Het gegeven wordt niet geschrapt van het gegevensmeer toe te schrijven aan schrapping door [ het Geavanceerde Beheer van de Levenscyclus van Gegevens ](../../hygiene/home.md), [ Privacy Service ](../../privacy-service/home.md), of andere diensten die schrapping leiden.

Eerst moet u de volgende informatie verzamelen:

1. Het identiteitssymbool (namespaceCode) van de cookie-naamruimte (bijvoorbeeld ECID) en de naamruimte voor de persoon (bijvoorbeeld CRMID) die zijn verzonden.
1.1. Voor de implementaties van SDK van het Web, zijn dit gewoonlijk namespaces inbegrepen in identityMap.
1.2. Voor de implementaties van de bron van de Analytics, zijn dit de koekjesherkenningsteken inbegrepen in identityMap. De persoon-id is een eVar-veld dat als een identiteit is gemarkeerd.
2. De dataset waarin de gebeurtenis in (dataset_name) werd verzonden.
3. De identiteitswaarde van de cookie-naamruimte die moet worden opgezocht (identity_value).

Identiteitssymbolen (namespaceCode) zijn hoofdlettergevoelig. Om alle identiteitssymbolen voor een bepaalde dataset in identityMap terug te winnen, stel de volgende vraag in werking:

```sql
SELECT distinct explode(*)FROM (SELECT map_keys(identityMap) FROM dataset_name)
```

Als u de identiteitswaarde van uw cookie-id niet kent en u wilt zoeken naar een cookie-id die aan meerdere personen-id&#39;s zou zijn gekoppeld, moet u de volgende query uitvoeren. Bij deze query wordt ECID gebruikt als de cookie-naamruimte en CRMID als de naamruimte voor de persoon.

>[!BEGINTABS]

>[!TAB  de implementatie van SDK van het Web ]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct identityMap['CRMID'][0]['id']) as crmidCount FROM dataset_name GROUP BY identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

>[!TAB  de bronschakelaarimplementatie van Analytics ]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct personID) as crmidCount FROM dataset_name group by identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

**Nota:** personID verwijst naar de weg van de beschrijver. U vindt deze informatie onder schema&#39;s.

>[!ENDTABS]

Nu u de cookiewaarden hebt geïdentificeerd verbonden aan veelvoudige persoon IDs, neem één van de resultaten en gebruik het in de volgende vraag om een chronologische mening van te krijgen wanneer die koekjeswaarde met een verschillende persoon herkenningsteken werd verbonden:

>[!BEGINTABS]

>[!TAB  de implementatie van SDK van het Web ]

```sql
  SELECT identityMap['CRMID'][0]['id'] as personEntity, * 
  FROM dataset_name 
  WHERE identitymap['ECID'][0].id ='identity_value' 
  ORDER BY timestamp desc 
```

>[!TAB  de bronschakelaarimplementatie van Analytics ]

```sql
SELECT _experience.analytics.customDimensions.eVars.eVar10 as personEntity, * 
FROM dataset_name 
WHERE identitymap['ECID'][0].id ='identity_value' 
ORDER BY timestamp desc 
```

**Nota**: Dit voorbeeld veronderstelt dat `eVar10` als identiteit duidelijk is. Voor uw configuraties moet u de eVar wijzigen op basis van de implementatie van uw eigen organisatie.

>[!ENDTABS]

### Het algoritme voor identiteitsoptimalisatie werkt niet zoals verwacht

**de stappen van het Oplossen van problemen**

Verwijs naar de documentatie op [ algoritme van de identiteitsoptimalisering ](./identity-optimization-algorithm.md), evenals de types van grafiekstructuren die worden gesteund.

* Lees de [ gids van de grafiekconfiguratie ](./example-configurations.md) voor voorbeelden van gesteunde grafiekstructuren.
* U kunt de [ implementatiegids ](./implementation-guide.md#appendix) voor voorbeelden van niet gesteunde grafiekstructuren ook lezen. Er zijn twee scenario&#39;s die zouden kunnen gebeuren:
   * Geen enkele naamruimte in al uw profielen.
   * Een [ &quot;gevaarlijk identiteitskaart&quot;](./implementation-guide.md#dangling-loginid-scenario) scenario komt voor. In dit scenario kan de Identiteitsdienst niet bepalen of de gevaarlijke id is gekoppeld aan een van de personen-entiteiten in de grafieken.

U kunt het [ hulpmiddel van de grafieksimulatie in UI ](./graph-simulation.md) ook gebruiken om gebeurtenissen te simuleren en uw eigen unieke namespace en namespace prioritaire montages te vormen. Dit kan u helpen een basislijninzicht te geven in hoe het algoritme voor identiteitsoptimalisatie zich zou moeten gedragen.

Als uw simulatieresultaten uw verwachtingen van het grafiekgedrag aanpassen, dan kunt u controleren en zien als uw [ identiteitsmontages ](./identity-settings-ui.md) de montages aanpast die u in uw simulatie hebt gevormd.

### Ik zie samengevouwen grafieken in mijn zandbak zelfs na het vormen van identiteitsmontages

De grafieken van de identiteit zullen aan uw gevormde unieke namespace en namespace prioriteit _naleven nadat_ de montages zijn bewaard. Om het even welke &quot;doen ineenstorten&quot;grafieken die _bestaan alvorens_ u sparen uw nieuwe montages niet zal worden beïnvloed, tot de nieuwe gegevens worden opgenomen dusdanig dat de doen ineenstorten grafiek wordt bijgewerkt. De primaire identiteit van gebeurtenisfragmenten op het Profiel van de Klant in real time zal niet worden bijgewerkt zelfs na namespace prioritaire veranderingen.

**de stappen van het Oplossen van problemen**

U kunt de [ kijker van de identiteitsgrafiek ](../features/identity-graph-viewer.md) gebruiken om te controleren of uw grafiek vóór of na uw montages werd opgenomen. Controleer de laatst bijgewerkte tijdstempel onder [!UICONTROL Link properties] om te zien wanneer Identity Service de grafiek heeft opgenomen. Als de tijdstempel zich vóór de configuratie bevindt, geeft dat aan dat de grafiek is samengevouwen voordat de functie is ingeschakeld.

![ de kijker van de identiteitsgrafiek met een voorbeeldgrafiek.](../images/troubleshooting/graph_viewer.png)

### Ik wil weten hoeveel &#39;samengevouwen&#39; grafieken er in mijn sandbox staan

Gebruik het identiteitsdashboard voor inzicht in de staat van uw identiteitsgrafiek, zoals het aantal identiteiten en grafieken. Verwijs naar metrisch, &quot;Aantal van de Grafiek met veelvoudige namespaces&quot;voor een telling van grafieken die zijn doen ineenstorten - dit zijn grafieken die twee of meer identiteiten met zelfde namespace bevatten. Ervan uitgaande dat de sandbox geen gegevens heeft en dat u een naamruimte (bijvoorbeeld CRMID) hebt geconfigureerd om uniek te zijn, wordt verwacht dat er geen grafieken met twee of meer CRMID&#39;s moeten zijn. In het onderstaande voorbeeld zijn er twee grafieken die twee of meer e-mailadressen bevatten.

![ het identiteitsdashboard met metriek op identiteitstelling, grafiektelling, telling door namespace, grafiektelling door grootte en grafiektelling van grafieken meer dan twee namespaces.](../images/troubleshooting/identity_dashboard.png)

U kunt een gedetailleerde uitsplitsing in de [ de uitvoerdataset van de profielmomentopname ](../../dashboards/query.md) in gegevensmeer vinden door de hieronder vraag in werking te stellen:

>[!NOTE]
>
>* Vervang `dataset_name` door de werkelijke naam van de gegevensset.
>
>* De aantallen komen mogelijk niet exact overeen. Het identiteitsdashboard is gebaseerd op de telling van de identiteitsgrafiek en de volgende vraag is gebaseerd op profieltelling met twee of meer identiteiten. De gegevens worden onafhankelijk verwerkt en bijgewerkt door de service.

```sql
  SELECT key, identityCountInGraph, count(identityCountInGraph) as graphCount 
  FROM (SELECT key, cardinality(value) as identityCountInGraph 
  FROM (SELECT explode(identityMap) 
  FROM dataset_name 
  WHERE cardinality(identityMap) > 1)) /* by definition, graphs have 2 or more identities */ 
  WHERE key not in ('ecid', 'aaid', 'idfa', 'gaid') /* filter out common device/cookie namespaces */ 
  GROUP BY 1, 2 
  ORDER BY 1, 2 asc 
```

U kunt de volgende vraag in de de uitvoerdataset van de profielmomentopname gebruiken om steekproefidentiteiten van &quot;doen ineenstorten&quot;grafieken te verkrijgen.

```sql
  SELECT identityMap 
  FROM dataset_name 
  WHERE cardinality(identityMap['CRMID'])>1 /* any graphs with 2+ CRMID. Change CRMID namespace if needed */ 
```

>[!TIP]
>
>De twee hierboven vermelde vragen zullen verwachte resultaten opleveren als de zandbak niet voor de gedeelde interimbenadering van het apparaat wordt toegelaten en zich anders gedraagt dan de identiteitsgrafiek die regels verbindt.

## Veelgestelde vragen {#faq}

Deze sectie schetst een lijst van antwoorden op vaak gestelde vragen over de verbindingsregels van de identiteitsgrafiek.

## Algoritme voor identiteitsoptimalisatie {#identity-optimization-algorithm}

Lees deze sectie voor antwoorden op vaak gestelde vragen over het [ algoritme van de identiteitsoptimalisering ](./identity-optimization-algorithm.md).

### Ik heb een CRMID voor elk van mijn zaken verenigt (B2C CRMID, B2B CRMID), maar ik heb geen unieke namespace over al mijn profielen. Wat zal gebeuren als ik B2C CRMID en B2B CRMID als uniek merk, en mijn identiteitsmontages toelaat?

Dit scenario wordt niet ondersteund. Daarom kunt u grafieken zien ineenstorten in gevallen waar een gebruiker hun B2C CRMID aan login gebruikt, en een andere gebruiker hun B2B CRMID aan login gebruikt. Voor meer informatie, lees de sectie over [ enige persoon namespace vereiste ](./implementation-guide.md#single-person-namespace-requirement) in de implementatiepagina.

### Worden bestaande samengevouwen grafieken door algoritme voor identiteitsoptimalisatie gecorrigeerd?

Bestaande samengevouwen grafieken worden alleen door het grafiekalgoritme beïnvloed (&#39;fixed&#39;) als deze grafieken worden bijgewerkt nadat u de nieuwe instellingen hebt opgeslagen.

### Als twee personen zich aanmelden en uitloggen met hetzelfde apparaat, wat gebeurt er dan met de gebeurtenissen? Zullen alle gebeurtenissen over naar de laatste voor authentiek verklaarde gebruiker overgaan?

* Anonieme gebeurtenissen (gebeurtenissen met ECID als primaire identiteit in Real-Time klantprofiel) worden overgedragen naar de laatst geverifieerde gebruiker. De reden hiervoor is dat de ECID wordt gekoppeld aan de CRMID van de laatst geverifieerde gebruiker (op Identity Service).
* Alle geverifieerde gebeurtenissen (gebeurtenissen met CRMID die als primaire identiteit zijn gedefinieerd) blijven bij de persoon.

Voor meer informatie, lees de gids bij [ bepalend de primaire identiteit voor ervaringsgebeurtenissen ](../identity-graph-linking-rules/namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events).

### Hoe zullen de verplaatsingen in Adobe Journey Optimizer worden beïnvloed wanneer de ECID van de ene persoon naar de andere overgaat?

De CRMID van de laatst geverifieerde gebruiker wordt gekoppeld aan de ECID (gedeelde apparaat). ECID&#39;s kunnen op basis van gebruikersgedrag opnieuw van de ene persoon naar de andere worden toegewezen. De impact zal afhangen van hoe de reis wordt gebouwd, zodat is het belangrijk dat de klanten de reis in een omgeving van de ontwikkelingszandbak uittesten om het gedrag te bevestigen.

De belangrijkste punten om te benadrukken zijn als volgt:

* Als een profiel eenmaal een reis binnengaat, leidt het opnieuw toewijzen van een ECID er niet toe dat het profiel halverwege een reis wordt verlaten.
   * Reisuitgangen worden niet geactiveerd door grafiekwijzigingen.
* Als een profiel niet meer aan een ECID is gekoppeld, kan dit leiden tot het wijzigen van het reispad als er een voorwaarde is die de kwalificatie van het publiek gebruikt.
   * Het verwijderen van ECID kan gebeurtenissen wijzigen die aan een profiel zijn gekoppeld. Dit kan resulteren in wijzigingen in de kwalificatie van het publiek.
* Het opnieuw betreden van een reis is afhankelijk van de reiseigenschappen.
   * Als u het opnieuw betreden van een reis uitschakelt, zodra er een profiel van die reis afsluit, zal hetzelfde profiel gedurende 91 dagen niet opnieuw binnenkomen (op basis van de wereldwijde time-out van de reis).
* Als een rit begint met een ECID-naamruimte, het profiel dat wordt ingevoerd en het profiel dat de handeling ontvangt (bijvoorbeeld e-mail, aanbieding) kan verschillend zijn afhankelijk van hoe de reis wordt ontworpen.
   * Als er bijvoorbeeld een wachttijd is tussen de acties en de ECID-overdrachten tijdens de wachttijd, kan een ander profiel worden aangewezen.
   * Met deze functie is ECID niet meer altijd gekoppeld aan één profiel.
   * De aanbeveling is om reizen te beginnen met naamruimten van personen (CRMID).

>[!TIP]
>
>Reizen moeten een profiel met een unieke naamruimte opzoeken omdat een niet-unieke naamruimte opnieuw aan een andere gebruiker kan worden toegewezen.
>
>* ECID&#39;s en niet-unieke e-mail- en telefoonnaamruimten kunnen van de ene persoon naar de andere worden verplaatst.
>* Als een reis een wachtstand heeft en als deze niet-unieke namespaces worden gebruikt om een profiel op een reis te zoeken, dan kan het reisbericht aan de onjuiste persoon worden verzonden.

## Prioriteit naamruimte

Lees deze sectie voor antwoorden op vaak gestelde vragen over [ namespace prioriteit ](./namespace-priority.md).

### Ik heb mijn identiteitsinstellingen ingeschakeld. Wat gebeurt er met mijn instellingen als ik een aangepaste naamruimte wil toevoegen nadat de instellingen zijn ingeschakeld?

Er zijn twee &#39;emmers&#39; van naamruimten: naamruimten van personen en naamruimten van apparaat/cookie. De nieuwe aangepaste naamruimte krijgt de laagste prioriteit in elk &#39;emmertje&#39;, zodat deze nieuwe aangepaste naamruimte geen invloed heeft op bestaande gegevensinvoer.

### Als het Profiel van de Klant in real time niet meer de &quot;primaire&quot;vlag op identityMap gebruikt, moet deze waarde nog worden verzonden?

Ja, de &quot;primaire&quot;vlag op identityMap wordt gebruikt door andere diensten. Voor meer informatie, lees de gids op [ de implicaties van namespaceprioriteit op andere diensten van Experience Platform ](../identity-graph-linking-rules/namespace-priority.md#implications-on-other-experience-platform-services).

### Zal naamruimteprioriteit van toepassing zijn op de gegevenssets van het profielrecord in Real-Time Klantprofiel?

Nee. De prioriteit Namespace zal slechts op de datasets van de Gebeurtenis van de Ervaring van toepassing zijn gebruikend de Klasse XDM ExperienceEvent.

### Hoe werkt deze functie in overeenstemming met de identiteitsgrafiekinstructies van 50 identiteiten per grafiek? Heeft naamruimteprioriteit invloed op deze door het systeem gedefinieerde hulplijn?

Het algoritme voor identiteitsoptimalisatie wordt eerst toegepast om te zorgen dat de persoon die entiteit vertegenwoordigt wordt vertegenwoordigd. Nadien, als de grafiek probeert om de [ graadmeter van de identiteitsgrafiek ](../guardrails.md) (50 identiteiten per grafiek) te overschrijden, dan zal deze logica worden toegepast. De prioriteit Namespace beïnvloedt niet de schrappingslogica van de 50 identiteit/grafiekbegeleiding.

## Testen

Lees deze sectie voor antwoorden op vaak gestelde vragen over het testen van en het zuiveren eigenschappen in identiteitsgrafiek die regels verbinden.

### Wat zijn enkele scenario&#39;s die ik zou moeten testen in een omgeving van de ontwikkelingszandbak?

In het algemeen geldt dat het testen op een ontwikkelingssandbox de gebruiksgevallen moet nabootsen die u wilt uitvoeren in de productiesandbox. Raadpleeg de volgende tabel voor een aantal belangrijke onderdelen die u wilt valideren wanneer u uitgebreide tests uitvoert:

| Testcase | Teststappen | Verwacht resultaat |
| --- | --- | --- |
| Accurate representatie van een entiteit | <ul><li>Anonieme navigatie simuleren</li><li>Mimic two people (John, Jane) logging in using the same device</li></ul> | <ul><li>Zowel John als Jane moeten aan hun attributen en voor authentiek verklaarde gebeurtenissen worden geassocieerd.</li><li>De laatst geverifieerde gebruiker moet zijn gekoppeld aan de anonieme browsergebeurtenissen.</li></ul> |
| Segmentatie | Creeer vier segmentdefinities (**NOTA**: Elk paar segmentdefinitie zou één moeten hebben geëvalueerd gebruikend partij en andere het stromen.) <ul><li>Segmentdefinitie A: segmentkwalificatie gebaseerd op voor authentiek verklaarde gebeurtenissen en/of attributen van John.</li><li>Segmentdefinitie B: segmentkwalificatie gebaseerd op voor authentiek verklaarde gebeurtenissen en/of attributen van Jane.</li></ul> | Ongeacht gedeelde apparatenscenario&#39;s, zouden John en Jane altijd voor hun respectieve segmenten moeten kwalificeren. |
| Bevoegdheden van het publiek/unitaire reizen op Adobe Journey Optimizer | <ul><li>Maak een reis die begint met een kwalificatieactiviteit voor het publiek (zoals de streamingsegmentatie die hierboven is gemaakt).</li><li>Maak een reis die begint met een eenheidsgebeurtenis. Deze eenheidsgebeurtenis moet een geverifieerde gebeurtenis zijn.</li><li>Wanneer u deze reizen maakt, moet u het opnieuw betreden uitschakelen.</li></ul> | <ul><li>Ongeacht gedeelde apparatenscenario&#39;s, zouden John en Jane de respectieve reizen moeten teweegbrengen die zij zouden moeten ingaan.</li><li>John en Jane mogen de reis niet opnieuw betreden wanneer de ECID naar hen wordt overgebracht.</li></ul> |

{style="table-layout:auto"}

### Hoe kan ik controleren of deze functie naar behoren functioneert?

Gebruik het [ hulpmiddel van de grafieksimulatie ](./graph-simulation.md) om te bevestigen dat de eigenschap op een individueel grafiekniveau werkt.

Als u de functie wilt valideren op sandboxniveau, raadpleegt u de sectie [!UICONTROL Graph count with multiple namespaces] in het identiteitsdashboard.