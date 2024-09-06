---
title: De Gids van het oplossen van problemen voor de Regels van de Verbinding van de Grafiek van de Identiteit
description: Leer hoe te om gemeenschappelijke kwesties in identiteitsgrafiek problemen op te lossen die regels verbinden.
badge: Beta
source-git-commit: cb0e229ac68f53d33b83d54df4062469252f06a3
workflow-type: tm+mt
source-wordcount: '2017'
ht-degree: 0%

---

# De gids van het oplossen van problemen voor identiteitsgrafiek die regels verbindt

>[!AVAILABILITY]
>
>De functie voor identiteitsgrafiekkoppelingen voor regels staat momenteel in bèta. Neem contact op met het accountteam van de Adobe voor meer informatie over de deelnemingscriteria. De functie en documentatie kunnen worden gewijzigd.

Wanneer u regels voor identiteitsgrafieken test en valideert, kan er een aantal problemen optreden die te maken hebben met gegevensinvoer en grafiekgedrag. Lees dit document om te leren hoe te om sommige gemeenschappelijke kwesties problemen op te lossen die u zou kunnen ontmoeten wanneer het werken met identiteitsgrafiek die regels verbindt.

## Overzicht gegevensinvoer {#data-ingestion-flow-overview}

Het volgende diagram is een vereenvoudigde weergave van hoe gegevens stromen naar Adobe Experience Platform en Toepassingen. Gebruik dit diagram als verwijzing om u te helpen een beter inzicht in de inhoud van deze pagina krijgen.

![ een diagram van hoe de gegevensopname in de Dienst van de Identiteit stroomt.](../images/troubleshooting/dataflow_in_identity.png)

Het is van belang de volgende factoren in aanmerking te nemen:

* Voor het stromen gegevens, zal het Profiel van de Klant in real time, de Dienst van de Identiteit, en het gegevenspeer beginnen de gegevens te verwerken wanneer de gegevens worden verzonden. Nochtans, is de latentie om de verwerking van de gegevens te voltooien afhankelijk van de dienst. Doorgaans duurt het langer om gegevens in een meer gegevens te verwerken dan bij Profiel en Identiteit.
   * Als de gegevens niet wanneer het runnen van een vraag tegen een dataset zelfs na een paar uren verschijnen, dan is het waarschijnlijk dat de gegevens niet in Experience Platform werden opgenomen.
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

* De veldnaam CRMID is gemarkeerd als een identiteit met de naamruimte CRMID.
* De naamruimte-CRMID wordt gedefinieerd als een unieke naamruimte.

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

### Mijn ervaring is dat gebeurtenisfragmenten niet in het profiel worden opgenomen {#my-experience-event-fragments-are-not-getting-ingested-into-profile}

Er zijn verschillende redenen die ertoe bijdragen waarom uw ervaringsfragmenten niet in Profiel worden opgenomen, met inbegrip van maar niet beperkt tot:

* [ De dataset wordt niet toegelaten voor Profiel ](../../catalog/datasets/enable-for-profile.md).
* [ de bevestigingsmislukking van A kan op Profiel ](../../xdm/classes/experienceevent.md) zijn voorgekomen.
   * Een ervaringsgebeurtenis moet bijvoorbeeld zowel een `_id` als een `timestamp` bevatten.
   * Bovendien moet `_id` uniek zijn voor elke gebeurtenis (record).

In de context van naamruimteprioriteit weigert Profiel elke gebeurtenis die twee of meer identiteiten met de hoogste naamruimteprioriteit bevat. Als GAID bijvoorbeeld niet is gemarkeerd als een unieke naamruimte en als er twee identiteiten zijn binnengekomen met een GAID-naamruimte en er verschillende identiteitswaarden zijn binnengekomen, worden de gebeurtenissen niet opgeslagen in Profiel.

**de stappen van het Oplossen van problemen**

Om deze fout op te lossen, leest de het oplossen van problemenstappen die in de gids hierboven op [ worden geschetst het oplossen van problemenfouten betreffende gegevens die niet aan de Dienst van de Identiteit worden opgenomen ](#my-identities-are-not-getting-ingested-into-identity-service).

### Mijn ervaring met gebeurtenisfragmenten die zijn ingepakt, maar die de &quot;verkeerde&quot; primaire identiteit hebben in Profiel

De prioriteit Namespace speelt een belangrijke rol in hoe de gebeurtenisfragmenten primaire identiteit bepalen.

* Zodra u hebt gevormd en uw [ identiteitsmontages ](./identity-settings-ui.md) voor een bepaalde zandbak opgeslagen, zal het Profiel dan [ namespace prioriteit ](namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events) gebruiken om de primaire identiteit te bepalen. In het geval van identityMap gebruikt Profile de markering `primary=true` niet meer.
* Hoewel Profiel niet langer naar deze markering verwijst, kunnen andere services op Experience Platform de markering `primary=true` blijven gebruiken.

Opdat [ voor authentiek verklaarde gebruikersgebeurtenissen ](configuration.md#ingest-your-data) aan de persoon worden gebonden namespace, moeten alle voor authentiek verklaarde gebeurtenissen de persoon namespace (CRMID) bevatten. Dit betekent dat zelfs nadat een gebruiker zich aanmeldt, de naamruimte van de persoon nog steeds aanwezig moet zijn op elke geverifieerde gebeurtenis.

U kunt de markering `primary=true` &#39;events&#39; blijven zien wanneer u een profiel opzoekt in de profielviewer. Dit wordt echter genegeerd en wordt niet gebruikt door Profiel.

HULP&#39;s worden standaard geblokkeerd. Daarom als u de [ bronVerbinding van Adobe Analytics ](../../sources/tutorials/ui/create/adobe-applications/analytics.md) gebruikt, moet u ervoor zorgen dat ECID aan hoger dan ECID wordt voorrang gegeven zodat de unauthenticated gebeurtenissen een primaire identiteit van ECID zullen hebben.

**de stappen van het Oplossen van problemen**

* Om te bevestigen dat de voor authentiek verklaarde gebeurtenissen zowel de persoon als koekjesnamespace bevatten, lees de stappen die in de sectie over [ worden geschetst het oplossen van problemenfouten betreffende gegevens die niet aan de Dienst van de Identiteit worden opgenomen ](#my-identities-are-not-getting-ingested-into-identity-service).
* Om te bevestigen dat de voor authentiek verklaarde gebeurtenissen de primaire identiteit van de persoon namespace (b.v. CRMID) hebben, onderzoek persoonnamespace op profielkijker gebruikend het geen-aaneenschakeling fusiebeleid (dit is het fusiebeleid dat geen privé grafiek gebruikt). Deze zoekopdracht retourneert alleen gebeurtenissen die zijn gekoppeld aan de naamruimte van de persoon.

## Problemen met grafiekgedrag {#graph-behavior-related-issues}

In deze sectie worden algemene problemen beschreven die u kunt tegenkomen met betrekking tot het gedrag van de identiteitsgrafiek.

### De identiteit wordt gekoppeld aan de &#39;verkeerde&#39; persoon

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

* Het identiteitssymbool (namespaceCode) van de cookie-naamruimte (bijvoorbeeld ECID) en de naamruimte voor de persoon (bijvoorbeeld CRMID) die zijn verzonden.
   * Voor de implementaties van SDK van het Web, zijn dit gewoonlijk namespaces inbegrepen in identityMap.
   * Voor de implementaties van de bronschakelaar van de Analytics, zijn dit het koekjesherkenningsteken inbegrepen in identityMap. De persoon-id is een eVar-veld dat als een identiteitsbewijs is gemarkeerd.
* De dataset waarin de gebeurtenis in (dataset_name) werd verzonden.
* De identiteitswaarde van de cookie-naamruimte die moet worden opgezocht (identity_value).

Identiteitssymbolen (namespaceCode) zijn hoofdlettergevoelig. Om alle identiteitssymbolen voor een bepaalde dataset in identityMap terug te winnen, stel de volgende vraag in werking:

```sql
SELECT distinct explode(*)FROM (SELECT map_keys(identityMap) FROM dataset_name)
```

Als u de identiteitswaarde van uw cookie-id niet kent en u wilt zoeken naar een cookie-id die aan meerdere personen-id&#39;s zou zijn gekoppeld, moet u de volgende query uitvoeren. Bij deze query wordt ECID gebruikt als de cookie-naamruimte en CRMID als de naamruimte voor de persoon.

>[!BEGINTABS]

>[!TAB  implementatie van SDK van het Web ]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct identityMap['CRMID'][0]['id']) as crmidCount FROM dataset_name GROUP BY identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

>[!TAB  de bronschakelaarimplementatie van Analytics ]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct personID) as crmidCount FROM dataset_name group by identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

**Nota:** personID verwijst naar de weg van de beschrijver. U vindt deze informatie onder schema&#39;s.

>[!ENDTABS]

Controleer vervolgens de koppeling van de cookie-naamruimte in volgorde van tijdstempel door de volgende query uit te voeren:

>[!BEGINTABS]

>[!TAB  implementatie van SDK van het Web ]

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

**Nota**: Dit voorbeeld veronderstelt dat `eVar10` als identiteit duidelijk is. Voor uw configuraties, moet u de eVar veranderen die op de implementatie van uw eigen organisatie wordt gebaseerd.

>[!ENDTABS]

### Het algoritme voor identiteitsoptimalisatie werkt niet zoals verwacht

**de stappen van het Oplossen van problemen**

Verwijs naar de documentatie op [ algoritme van de identiteitsoptimalisering ](./identity-optimization-algorithm.md), evenals de types van grafiekstructuren die worden gesteund.

* Lees de [ gids van de grafiekconfiguratie ](./example-configurations.md) voor voorbeelden van gesteunde grafiekstructuren.
* U kunt de [ implementatiegids ](./configuration.md#appendix) voor voorbeelden van niet gesteunde grafiekstructuren ook lezen. Er zijn twee scenario&#39;s die zouden kunnen gebeuren:
   * Geen enkele naamruimte in al uw profielen.
   * Een [ &quot;gevaarlijk identiteitskaart&quot;](./configuration.md#dangling-loginid-scenario) scenario komt voor. In dit scenario kan de Identiteitsdienst niet bepalen of de gevaarlijke id is gekoppeld aan een van de personen-entiteiten in de grafieken.

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