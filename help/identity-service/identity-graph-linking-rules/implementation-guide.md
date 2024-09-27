---
title: Implementatiegids voor koppelingsregels voor identiteitsgrafieken
description: Leer de aanbevolen stappen die u moet volgen wanneer u uw gegevens implementeert met configuraties van regels voor identiteitsgrafieken.
badge: Beta
exl-id: 368f4d4e-9757-4739-aaea-3f200973ef5a
source-git-commit: adfb1e83289435e6991d4cdd2e2a45e3d5a9b32f
workflow-type: tm+mt
source-wordcount: '1536'
ht-degree: 0%

---

# Implementatiegids voor koppelingsregels voor identiteitsgrafieken

>[!AVAILABILITY]
>
>De regels voor identiteitsgrafiekkoppelingen staan momenteel in bèta. Neem contact op met het accountteam van de Adobe voor meer informatie over de deelnemingscriteria. De functie en documentatie kunnen worden gewijzigd.

Lees dit document voor een stapsgewijze uitleg die u kunt volgen bij het implementeren van uw gegevens met Adobe Experience Platform Identity Service.

Stapsgewijze omtrek:


1. [Volledige voorwaarden voor implementatie](#prerequisites-for-implementation)
2. [De benodigde naamruimten maken](#namespace)
3. [Gebruik het grafieksimulatiehulpmiddel om met het algoritme van de identiteitsoptimalisering vertrouwd te maken](#graph-simulation)
4. [Gebruik het hulpmiddel van identiteitsinstellingen om uw unieke naamruimten aan te wijzen en prioritaire classificaties voor uw naamruimten te vormen](#identity-settings)
5. [Een XDM-schema (Experience Data Model) maken](#schema)
6. [Een gegevensset maken](#dataset)
7. [Gegevens naar Experience Platform verzenden](#ingest)

## Vereisten voor de implementatie {#prerequisites-for-implementation}

In deze sectie worden de vereiste stappen beschreven die u moet voltooien voordat u identiteitsgrafiek implementeert die regels aan uw gegevens koppelt.

### Unieke naamruimte

#### Naamruimtevereiste voor één persoon {#single-person-namespace-requirement}

U moet ervoor zorgen dat de unieke naamruimte met de hoogste prioriteit altijd aanwezig is in elk profiel. Hierdoor kan de identiteitsdienst de juiste persoon-id in een bepaalde grafiek detecteren.

+++Selecteren om een voorbeeld weer te geven van een grafiek zonder naamruimte voor één persoon

Zonder een unieke naamruimte die uw persoon-id vertegenwoordigt, kunt u eindigen met een grafiek die een koppeling bevat naar verschillende personen-id&#39;s voor dezelfde ECID. In dit voorbeeld zijn zowel B2BCRM als B2CCRM tegelijkertijd gekoppeld aan dezelfde ECID. Deze grafiek suggereert dat Tom, met zijn B2C-aanmeldingsaccount, een apparaat deelde met Summer, met haar B2B-aanmeldingsaccount. Het systeem herkent echter dat dit één profiel is (grafiek samenvouwen).

![ de grafiekscenario van A waar twee persoonherkenningstekens met zelfde ECID verbonden zijn.](../images/graph-examples/multi_namespaces.png)

+++

+++Selecteren om een voorbeeld weer te geven van een grafiek met naamruimte voor één persoon-id

Op basis van een unieke naamruimte (in dit geval een CRMID in plaats van twee verschillende naamruimten) kan de identiteitsdienst de persoon-id zien die het laatst aan de ECID is gekoppeld. In dit voorbeeld, omdat een unieke CRMID bestaat, kan de Dienst van de Identiteit een &quot;gedeeld apparaat&quot;scenario erkennen, waar twee entiteiten het zelfde apparaat delen.

![ een gedeeld scenario van de apparatengrafiek, waar twee persoonherkenningstekens met zelfde ECID verbonden zijn, maar de oudere verbinding wordt verwijderd.](../images/graph-examples/crmid_only_multi.png)

+++

### Prioriteitsconfiguratie naamruimte

Als u [ Adobe Analytics bronschakelaar ](../../sources/tutorials/ui/create/adobe-applications/analytics.md) gebruikt om gegevens in te voeren, dan moet u uw ECIDs een hogere prioriteit geven dan identiteitskaart van Adobe Analytics (HULP) omdat de Dienst van de Identiteit HULP blokkeert. Door ECID een prioriteit te geven, kunt u Real-Time Klantprofiel de opdracht geven om niet-geverifieerde gebeurtenissen op te slaan naar ECID in plaats van naar HULP.

### XDM Experience-gebeurtenissen

* Tijdens uw pre-implementatieproces, moet u ervoor zorgen dat de voor authentiek verklaarde gebeurtenissen die uw systeem naar Experience Platform zal verzenden altijd een persoonsidentificatie, zoals CRMID bevatten.
* Verzend geen lege tekenreeks als identiteitswaarde wanneer u gebeurtenissen verzendt met behulp van XDM-ervaringsgebeurtenissen. Dit leidt tot systeemfouten.

+++Selecteren om een voorbeeld weer te geven van een lading met een lege tekenreeks

In het volgende voorbeeld wordt een fout geretourneerd omdat de identiteitswaarde voor `Phone` wordt verzonden als een lege tekenreeks.

```json
    "identityMap": {
        "ECID": [
            {
                "id": "24165048599243194405404369473457348936",
                "primary": false
            }
        ],
        "Phone": [
            {
                "id": "",
                "primary": true
            }
        ]
    }
```

+++

U moet ervoor zorgen dat u een volledig gekwalificeerde identiteit hebt wanneer u gebeurtenissen verzendt die XDM ervaringsgebeurtenissen gebruiken.

+++Selecteren om een voorbeeld weer te geven van een gebeurtenis met een volledig gekwalificeerde identiteit

```json
    "identityMap": {
        "ECID": [
            {
                "id": "24165048599243194405404369473457348936",
                "primary": false
            }
        ]
    }
```

+++

## Machtigingen instellen {#set-permissions}

De eerste stap in het implementatieproces voor Identity Service is ervoor te zorgen dat uw account voor Experience Platforms wordt toegevoegd aan een rol die is voorzien van de vereiste machtigingen. Uw beheerder kan machtigingen voor uw account configureren door naar de gebruikersinterface voor machtigingen in Adobe Experience Cloud te navigeren. Van daar, moet uw rekening aan een rol met de volgende toestemmingen worden toegevoegd:

* [!UICONTROL View Identity Settings]: pas deze machtiging toe om unieke naamruimten en naamruimtenprioriteit weer te geven in de pagina Bladeren naar naamruimte voor identiteiten.
* [!UICONTROL Edit Identity Settings]: pas deze machtiging toe om uw identiteitsinstellingen te kunnen bewerken en opslaan.

Voor meer informatie over toestemmingen, lees de [ gids van toestemmingen ](../../access-control/abac/ui/permissions.md).

## Uw naamruimten maken {#namespace}

Als dit voor uw gegevens nodig is, moet u eerst de juiste naamruimten voor uw organisatie maken. Voor stappen op hoe te om tot een douane te leiden namespace, lees de gids bij [ creërend een douanespatie in UI ](../features/namespaces.md#create-custom-namespaces).

## Het gereedschap Grafieksimulatie gebruiken {#graph-simulation}

Daarna, navigeer aan het [ hulpmiddel van de grafieksimulatie ](./graph-simulation.md) in de werkruimte UI van de Dienst van de Identiteit. U kunt het hulpmiddel van de grafieksimulatie gebruiken om identiteitsgrafieken te simuleren, die met een verscheidenheid van verschillende unieke namespace en namespace prioritaire configuraties worden gebouwd.

Door verschillende configuraties te maken, kunt u het gereedschap voor grafieksimulatie gebruiken om te leren en beter te begrijpen hoe het algoritme voor identiteitsoptimalisatie en bepaalde configuraties het gedrag van de grafiek beïnvloeden.

## Identiteitsinstellingen configureren {#identity-settings}

Zodra u een beter idee van hebt hoe u uw grafiek wilt gedragen, navigeer aan het [ hulpmiddel van identiteitsmontages ](./identity-settings-ui.md) in de werkruimte UI van de Dienst van de Identiteit.

Gebruik het hulpmiddel van identiteitsinstellingen om uw unieke naamruimten aan te wijzen en uw naamruimten op volgorde van prioriteit te vormen. Zodra u met het toepassen van uw montages wordt gebeëindigd, moet u minstens zes uren wachten alvorens u te werk gaat om gegevens in te voeren, aangezien het minstens zes uren voor nieuwe montages om in de Dienst van de Identiteit moet worden weerspiegeld.

## Een XDM-schema maken {#schema}

Wanneer uw unieke naamruimten en naamruimteprioriteiten zijn ingesteld, kunt u nu doorgaan naar de vereiste instelling om uw gegevens in te voeren. Eerst moet u een XDM-schema maken. Afhankelijk van uw gegevens moet u mogelijk een schema maken voor zowel XDM Individual Profile als XDM ExperienceEvent.

Om gegevens in het Profiel van de Klant in real time in te voeren, moet u ervoor zorgen dat uw schema minstens één gebied bevat dat als primaire identiteit is aangewezen. Door een primaire identiteit in te stellen, kunt u een bepaald schema inschakelen voor profielopname.

Voor instructies op hoe te om een schema tot stand te brengen, lees de gids bij [ creërend een schema XDM in UI ](../../xdm/tutorials/create-schema-ui.md).

## Een gegevensset maken {#dataset}

Daarna, creeer een dataset om een structuur voor de gegevens te verstrekken die u gaat opnemen. Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. Datasets werken in combinatie met schema&#39;s en om gegevens in te voeren in het Real-Time Klantprofiel, moet uw gegevensset zijn ingeschakeld voor het opnemen van profielen. Opdat uw dataset voor Profiel wordt toegelaten, moet het een schema van verwijzingen voorzien dat voor de opname van het Profiel wordt toegelaten.

Voor instructies op hoe te om een dataset tot stand te brengen, lees de [ gids UI van de dataset ](../../catalog/datasets/user-guide.md).

## Gegevens verzamelen {#ingest}

Op dit punt, zou u het volgende moeten hebben:

* De noodzakelijke toestemmingen om tot de eigenschappen van de Dienst van de Identiteit toegang te hebben.
* Naamruimten voor uw gegevens.
* Aangewezen unieke naamruimten en geconfigureerde prioriteiten voor uw naamruimten.
* Minstens één XDM-schema. (Afhankelijk van uw gegevens en het specifieke gebruiksgeval, kunt u zowel profiel als ervaringsschema&#39;s moeten tot stand brengen.)
* Een dataset die van uw schema gebaseerd is.

Zodra u alle hierboven vermelde punten hebt, kunt u beginnen uw gegevens aan Experience Platform in te voeren. U kunt gegevensinvoer op verschillende manieren uitvoeren. U kunt de volgende services gebruiken om uw gegevens naar het Experience Platform te brengen:

* [ Partij en het stromen opname ](../../ingestion/home.md)
* [Gegevensverzameling in Experience Platform](../../collection/home.md)
* [Experience Platforms](../../sources/home.md)

>[!TIP]
>
>Als uw gegevens eenmaal zijn ingevoerd, verandert de XDM Raw-gegevenslading niet meer. U kunt uw primaire identiteitsconfiguraties in UI nog zien. Deze configuraties worden echter overschreven door identiteitsinstellingen.

Gebruik voor alle feedback de optie **[!UICONTROL Beta feedback]** in de gebruikersinterface van de identiteitsservice.

## Grafieken valideren {#validate}

Gebruik het identiteitsdashboard voor inzicht in de staat van uw identiteitsgrafieken, zoals uw algemene identiteitstelling en tendensen van het grafiekaantal, identiteitstelling door namespace, en grafiektelling door grafiekgrootte. U kunt het identiteitsdashboard ook gebruiken om trends weer te geven op grafieken met twee of meer identiteiten, ingedeeld in naamruimte.

Selecteer de ellipsen (`...`) en selecteer vervolgens **[!UICONTROL View more]** voor meer informatie en om te controleren of er geen samengevouwen grafieken zijn.

## Bijlage {#appendix}

Lees deze sectie voor extra informatie die u kunt verwijzen wanneer het uitvoeren van uw identiteitsmontages en unieke namespaces.

### LoginID-scenario van Dangling {#dangling-loginid-scenario}

De volgende grafiek simuleert een &quot;gevaarlijk&quot;loginID scenario. In dit voorbeeld zijn twee verschillende loginID&#39;s gebonden aan dezelfde ECID. `{loginID: ID_C}` is echter niet gekoppeld aan de CRMID. Daarom is er geen manier voor de Dienst van de Identiteit om te ontdekken dat deze twee loginIDs twee verschillende entiteiten vertegenwoordigen.

>[!BEGINTABS]

>[!TAB  Ambiguous loginID ]

In dit voorbeeld blijft `{loginID: ID_C}` gevaarlijk en is het niet gekoppeld aan een CRMID. Aldus, wordt de persoonentiteit waaraan deze loginID zou moeten worden geassocieerd dubbelzinnig verlaten.

![ een voorbeeld van een grafiek met een &quot;gevaarlijk&quot;loginID scenario.](../images/graph-examples/dangling_example.png)

>[!TAB  loginID is verbonden met een CRMID ]

In dit voorbeeld is `{loginID: ID_C}` gekoppeld aan `{CRMID: Tom}` . Daarom kan het systeem vaststellen dat deze loginID aan Tom is gekoppeld.

![ LoginID is verbonden met een CRMID.](../images/graph-examples/id_c_tom.png)

>[!TAB  loginID is verbonden met een andere CRMID ]

In dit voorbeeld is `{loginID: ID_C}` gekoppeld aan `{CRMID: Summer}` . Daarom kan het systeem opmerken dat deze loginID met een andere persoonentiteit, in dit geval, Summer wordt geassocieerd.

In dit voorbeeld wordt ook getoond dat Tom en Summer verschillende persoonentiteiten moeten hebben die een apparaat delen, dat wordt vertegenwoordigd door `{ECID: 111}` .

![ LoginID is verbonden met een andere CRMID.](../images/graph-examples/id_c_summer.png)

>[!ENDTABS]

## Volgende stappen

Lees de volgende documentatie voor meer informatie over koppelingsregels voor identiteitsgrafieken:

* [Overzicht van regels voor identiteitsgrafiek](./overview.md)
* [Algoritme voor identiteitsoptimalisatie](./identity-optimization-algorithm.md)
* [Voorbeelden van grafiekconfiguraties](./example-configurations.md)
* [Problemen oplossen en veelgestelde vragen](./troubleshooting.md)
* [Prioriteit naamruimte](./namespace-priority.md)
* [UI voor grafieksimulatie](./graph-simulation.md)
* [Gebruikersinterface voor identiteitsinstellingen](./identity-settings-ui.md)
