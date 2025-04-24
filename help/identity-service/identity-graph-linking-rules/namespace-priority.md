---
title: Prioriteit naamruimte
description: Leer over namespace prioriteit in de Dienst van de Identiteit.
exl-id: bb04f02e-3826-45af-b935-752ea7e6ed7c
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 1%

---

# Prioriteit naamruimte {#namespace-priority}

>[!CONTEXTUALHELP]
>id="platform_identities_namespacepriority"
>title="Prioriteit naamruimte"
>abstract="De prioriteit Namespace bepaalt hoe de verbindingen uit de identiteitsgrafiek worden verwijderd."

>[!AVAILABILITY]
>
>De Regels van de Vereniging van de Grafiek van de identiteit zijn momenteel in Beperkte Beschikbaarheid, en kunnen door alle klanten in ontwikkelingszandbakken worden betreden.
>
>* **de vereisten van de Activering**: De eigenschap zal inactief blijven tot u vormt en uw [!DNL Identity Settings] bewaart. Zonder deze configuratie, zal het systeem normaal, zonder veranderingen in gedrag blijven werken.
>* **Belangrijke nota&#39;s**: Tijdens deze Beperkte fase van de Beschikbaarheid, kan de segmentatie van Edge onverwachte resultaten van het segmentlidmaatschap veroorzaken. Streaming en batchsegmentatie functioneren echter naar behoren.
>* **Volgende stappen**: Voor informatie over hoe te om deze eigenschap in productiestanddozen toe te laten, gelieve uw Adobe accountteam te contacteren.

Elke klantenimplementatie is uniek en gemaakt om de doelstellingen van een bepaalde organisatie te ontmoeten, en als dusdanig, varieert het belang van bepaalde namespace van klant tot klant. Voorbeelden in de praktijk zijn:

* Uw bedrijf zou elk e-mailadres kunnen overwegen om een enig-persoonentiteit te vertegenwoordigen en daarom [ identiteitsmontages ](./identity-settings-ui.md) gebruiken om e-mailnamespace als uniek te vormen. Een ander bedrijf, echter, zou eenpersoonsentiteiten kunnen willen vertegenwoordigen aangezien het hebben van veelvoudige e-mailadressen, en zo e-mailnamespace vormen niet-uniek. Deze bedrijven zouden een andere naamruimte voor identiteiten als uniek moeten gebruiken, zoals een naamruimte CRMID, zodat er een id voor één persoon kan zijn die is gekoppeld aan de meerdere e-mailadressen.
* U kunt online gedrag verzamelen met behulp van een naamruimte &quot;Aanmeldings-id&quot;. Deze login identiteitskaart kon een 1:1 verhouding met CRMID hebben, die dan attributen van een systeem van CRM opslaat en als belangrijkste namespace kan worden beschouwd. In dit geval, bepaalt u dan dat CRMID namespace een nauwkeurigere vertegenwoordiging van een persoon is, terwijl Login ID namespace de tweede belangrijkste is.

U moet configuraties in de identiteitsservice maken die het belang van uw naamruimten weerspiegelen, aangezien dit van invloed is op de manier waarop profielen en de bijbehorende identiteitsgrafieken worden gevormd en gesplitst.

## Uw prioriteiten bepalen

De bepaling van naamruimteprioriteit is gebaseerd op de volgende factoren:

### Identiteitsgrafiekstructuur

Als de grafiekstructuur van uw organisatie gelaagd is, dan zou de namespaceprioriteit dit moeten weerspiegelen zodat de correcte verbindingen in het geval van grafiekinstorting worden verwijderd.

>[!TIP]
>
>* &quot;Grafieksamenvouwen&quot; verwijst naar scenario&#39;s waarbij meerdere verschillende profielen per ongeluk worden samengevoegd tot één identiteitsgrafiek.
>
>* Een gelaagde grafiek verwijst naar identiteitsgrafieken die meerdere niveaus van verbindingen hebben. Bekijk de onderstaande afbeelding voor een voorbeeld van een grafiek met drie lagen.

![ een diagram van grafieklagen ](../images/namespace-priority/graph-layers.png)

### Semantische betekenis van de naamruimte

Een identiteit vertegenwoordigt een echt object. Er zijn drie objecten die in de identiteitsgrafiek worden weergegeven. In volgorde van belangrijkheid zijn ze:

* Personen (apparaat, e-mail, telefoonnummer)
* Hardwareapparaat
* Webbrowser (Cookie)

Naamruimten voor personen zijn relatief onveranderlijk in vergelijking met hardwareapparaten (zoals IDFA, GAID), die relatief onveranderlijk zijn in vergelijking met webbrowsers. In principe zult u (persoon) altijd één eenheid zijn, die meerdere hardwareapparaten kan hebben (telefoon, laptop, tablet, enz.) en meerdere browsers (Google Chrome, Safari, FireFox, enz.)

Een andere manier om dit onderwerp te benaderen is door kardinaliteit. Hoeveel identiteiten worden er voor een bepaalde personenentiteit gecreëerd? In de meeste gevallen zal een persoon één CRMID, een handvol herkenningstekens van het hardwareapparaat (het zou niet vaak moeten gebeuren IDFA/GAID), en zelfs meer koekjes hebben (een individu zou op veelvoudige apparaten kunnen doorbladeren, zou incognitomodus kunnen gebruiken, of zou koekjes op elk bepaald ogenblik terugstellen). Over het algemeen, **lagere kardinaliteit wijst op een namespace met een hogere waarde**.

## Valideer uw instellingen voor naamruimteprioriteit

Zodra u een idee van hebt hoe u aan uw namespaces voorrang zult geven, kunt u het hulpmiddel van de Simulatie van de Grafiek in UI gebruiken om diverse scenario&#39;s van de grafiekondergang uit te testen en ervoor te zorgen dat uw prioritaire configuraties de verwachte grafiekresultaten terugkeren. Voor meer informatie, lees de gids bij het gebruiken van het [ hulpmiddel van de Simulatie van de Grafiek ](./graph-simulation.md).

## Naamruimteprioriteit configureren

De prioriteit van Namespace kan worden gevormd gebruikend [ identiteitsmontages UI ](./identity-settings-ui.md). In de interface van identiteitsinstellingen kunt u een naamruimte slepen en neerzetten om het relatieve belang ervan te bepalen.

>[!IMPORTANT]
>
>U kunt geen voorkeur geven aan naamruimten van apparaten/cookies boven naamruimten van personen. Deze beperking zorgt ervoor dat de misconfiguraties niet voorkomen.

## Prioriteitsgebruik voor naamruimte

Momenteel, beïnvloedt de nameprioriteit systeemgedrag van het Profiel van de Klant in real time. In het onderstaande diagram wordt dit concept geïllustreerd. Voor meer informatie, lees de gids op [ Adobe Experience Platform en de diagrammen van de toepassingsarchitectuur ](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications).

![ een diagram van namespace prioritaire toepassingswerkingsgebied ](../images/namespace-priority/application-scope.png)

## Identiteitsservice: algoritme voor identiteitsoptimalisatie

Voor relatief complexe grafiekstructuren speelt naamruimteprioriteit een belangrijke rol bij het verwijderen van de juiste koppelingen wanneer de scenario&#39;s voor het samenvouwen van grafieken worden uitgevoerd. Voor meer informatie lees het [ overzicht van het algoritme van de identiteitsoptimalisering ](../identity-graph-linking-rules/identity-optimization-algorithm.md).

## Klantprofiel in realtime: primaire identiteitsbepaling voor ervaringsgebeurtenissen

* Zodra u identiteitsmontages voor een bepaalde zandbak hebt gevormd, zal de primaire identiteit voor ervaringsgebeurtenissen door de hoogste namespace prioriteit in de configuratie worden bepaald.
   * Dit komt omdat ervaringsgebeurtenissen dynamisch van aard zijn. Een identiteitskaart kan drie of meer identiteiten bevatten, en namespace prioriteit zorgt ervoor dat belangrijkste namespace aan de ervaringsgebeurtenis wordt geassocieerd.
* Dientengevolge, zullen de volgende configuraties **niet meer door Real-Time Profiel van de Klant** worden gebruikt:
   * De primaire identiteitsconfiguratie (`primary=true`) wanneer het verzenden van identiteiten in identityMap gebruikend het Web SDK, Mobiele SDK, of Edge Network API (identiteitsnaamruimte en identiteitswaarde zullen in Profiel blijven worden gebruikt). **Nota**: De diensten buiten het Profiel van de Klant in real time zoals de opslag van het gegevensmeer of Adobe Target zullen de primaire identiteitsconfiguratie blijven gebruiken (`primary=true`).
   * Alle velden die als primaire identiteit zijn gemarkeerd in een schema van de klasse Event van de XDM-ervaring.
   * Standaard primaire identiteitsinstellingen in de Adobe Analytics-bronconnector (ECID of AID).
* Anderzijds, **namespace de prioriteit bepaalt geen primaire identiteit voor profielverslagen**.
   * Voor profielverslagen, zou u uw identiteitsgebieden in het schema, met inbegrip van de primaire identiteit moeten blijven bepalen. Lees de gids op [ bepalend identiteitsgebieden in UI ](../../xdm/ui/fields/identity.md) voor meer informatie.

>[!TIP]
>
>* De prioriteit van Namespace is **een bezit van een namespace**. Het is een numerieke waarde die aan een naamruimte wordt toegewezen om het relatieve belang ervan aan te geven.
>
>* Primaire identiteit is de identiteit waarin een profielfragment wordt opgeslagen. Een profielfragment is een record met gegevens waarin informatie over een bepaalde gebruiker wordt opgeslagen: kenmerken (bijvoorbeeld CRM-records) of gebeurtenissen (bijvoorbeeld bladeren door websites).

### Voorbeeldscenario

Deze sectie verstrekt een voorbeeld van hoe de prioritaire configuratie uw gegevens kan beïnvloeden.

Stel dat de volgende configuraties zijn ingesteld voor een bepaalde sandbox:

| Naamruimte | Real-world toepassing van namespace | Prioriteit |
| --- | --- | --- |
| CRMID | Gebruiker | 1 |
| IDFA | Apple-hardwareapparaat (iPhone, IPad, enz.) | 2 |
| GAID | Google-hardwareapparaat (Google Pixel, Pixelbook, enz.) | 3 |
| ECID | Webbrowser (Firefox, Safari, Google Chrome, enz.) | 4 |
| STEUN | Webbrowser | 5 |

{style="table-layout:auto"}

Gezien de bovenstaande configuraties, zullen gebruikersacties en bepaling van de primaire identiteit als volgt worden opgelost:

| Handeling van de gebruiker (Experience-gebeurtenis) | Verificatiestatus | Gegevensbron | Naamruimten in gebeurtenis | Naamruimte van primaire identiteit |
| --- | --- | --- | --- | --- |
| Pagina met creditcardaanbiedingen weergeven | Niet geverifieerd (anoniem) | Web SDK | `{ECID}` | ECID |
| Help-pagina weergeven | Niet geverifieerd | Mobile SDK | `{ECID, IDFA}` | IDFA |
| Accountbalans bekijken | Geverifieerd | Web SDK | `{CRMID, ECID}` | CRMID |
| Aanmelden voor thuislening | Geverifieerd | Bronconnector voor analyse | `{CRMID, ECID, AAID}` | CRMID |
| Breng $1.000 van controle aan besparingen over | Geverifieerd | Mobile SDK | `{CRMID, GAID, ECID}` | CRMID |

{style="table-layout:auto"}

## Segmentatieservice: opslag van metagegevens voor segmentlidmaatschap

![ A diagram van de opslag van het segmentlidmaatschap ](../images/namespace-priority/segment-membership-storage.png)

Voor een bepaald samengevoegd profiel, zullen de segmentlidmaatschappen tegen de identiteit met de hoogste namespace prioriteit worden opgeslagen.

Stel dat er twee profielen zijn:

* Profiel 1 staat voor John.
   * Het profiel van John kwalificeert voor S1 (segmentlidmaatschap 1). Bijvoorbeeld, kon S1 naar een segment van klanten verwijzen die zich als mannetje identificeren.
   * Het profiel van John kwalificeert ook voor S2 (segmentlidmaatschap 2). Dit zou kunnen verwijzen naar een segment klanten waarvan de loyaliteitsstatus goud is.
* Profiel 2 staat voor Jane.
   * Het profiel van Jane komt in aanmerking voor S3 (segmentlidmaatschap 3). Dit zou naar een segment van klanten kunnen verwijzen die zich als vrouwelijk identificeren.
   * Het profiel van Jane komt ook in aanmerking voor S4 (segmentlidmaatschap 4). Dit zou naar een segment van klanten kunnen verwijzen waarvan loyaliteitsstatus platina is.

Als John en Jane een apparaat delen, dan brengt ECID (Webbrowser) van één persoon aan een andere over. Nochtans, beïnvloedt dit niet de informatie van het segmentlidmaatschap die tegen John en Jane wordt opgeslagen.

Als de segmentkwalificatiecriteria uitsluitend gebaseerd waren op anonieme gebeurtenissen die tegen de ECID waren opgeslagen, zou Jane in aanmerking komen voor dat segment.

## Gevolgen voor andere Experience Platform-services {#implications}

In deze sectie wordt beschreven hoe naamruimteprioriteit van invloed kan zijn op andere Experience Platform-services.

### Geavanceerd beheer van de levenscyclus van gegevens

Gegevens-hygiënebestanden verwijderen de aanvraagfuncties voor een bepaalde identiteit op de volgende manier:

* Klantprofiel in realtime: verwijdert elk profielfragment met de opgegeven identiteit als primaire identiteit. **De primaire identiteit op Profiel zal nu gebaseerd op namespace prioriteit worden bepaald.**
* Gegevensmeer: hiermee verwijdert u alle records met de opgegeven identiteit als primaire identiteit. In tegenstelling tot het Profiel van de Klant in real time, is de primaire identiteit in gegevensmeer gebaseerd op primaire identiteit die op WebSDK (`primary=true`) wordt gespecificeerd, of een gebied duidelijk als primaire identiteit

Voor meer informatie, lees het [ geavanceerde overzicht van het levenscyclusbeheer ](../../hygiene/home.md).

### Berekende kenmerken

Als identiteitsinstellingen zijn ingeschakeld, gebruiken berekende kenmerken naamruimteprioriteit om de berekende kenmerkwaarde op te slaan. Voor een bepaalde gebeurtenis, zal de identiteit met de hoogste namespace prioriteit de waarde van de gegevens verwerkte attributen hebben die tegen het worden geschreven. Voor meer informatie, lees de [ gegevens verwerkte handleiding van attributen UI ](../../profile/computed-attributes/ui.md).

### Gegevensmeer

Het opnemen van gegevens aan gegevens zal meer de primaire identiteitsmontages blijven respecteren die op [ SDK van het Web ](../../tags/extensions/client/web-sdk/data-element-types.md#identity-map) en schema&#39;s worden gevormd.

Het meer van gegevens zal geen primaire identiteit bepalen die op namespaceprioriteit wordt gebaseerd. Adobe Customer Journey Analytics zal bijvoorbeeld waarden in de identiteitskaart blijven gebruiken, zelfs nadat naamruimtenioriteit is ingeschakeld (zoals het toevoegen van een gegevensset aan een nieuwe verbinding), omdat Customer Journey Analytics gegevens uit het datumpeer gebruikt.

### Schema&#39;s voor Experience Data Model (XDM)

Om het even welk schema dat geen Gebeurtenis van de Ervaring XDM, zoals Individuele Profielen XDM is, zal blijven om het even welke [ gebieden respecteren die u als identiteit ](../../xdm/ui/fields/identity.md) merkt.

Voor meer informatie over schema&#39;s XDM, lees het [ schema&#39;s overzicht ](../../xdm/home.md).

### Intelligente diensten

Wanneer u uw gegevens selecteert, moet u een naamruimte opgeven die wordt gebruikt om de gebeurtenissen te bepalen die de scores berekenen en de gebeurtenissen die de berekende scores opslaan. U wordt aangeraden de naamruimte te selecteren die een persoon vertegenwoordigt.

* Als u gegevens van het Webgedrag gebruikend WebSDk verzamelt, wordt u geadviseerd om CRMID te kiezen namespace binnen de identiteitskaart.
* Als u gegevens over webgedrag verzamelt via de bronconnector van Analytics, moet u de identiteitsdescriptor (CRMID) selecteren.

Deze configuratie resulteert in computerscores die alleen gebruikmaken van geverifieerde gebeurtenissen.

Voor meer informatie, lees de documenten op [ AI van de Attributie ](../../intelligent-services/attribution-ai/overview.md) en [ Klant AI ](../../intelligent-services/customer-ai/overview.md).

### Partner-gebouwde bestemmingen

De bijgewerkte resultaten van de publieksuitsluiting voor profielen verbonden aan een gedeeld apparaat kunnen niet naar stroomafwaartse bestemmingen worden verzonden. Dit kan voorkomen in bepaalde zeldzame gevallen waarin:

* De kwalificatie van het publiek is slechts gebaseerd op anonieme activiteit.
* De logins over veelvoudige profielen komen in een korte periode voor.

Voor meer informatie over partner-gebouwde bestemmingen, lees het [ overzicht van bestemmingen ](../../destinations/home.md#adobe-built-and-partner-built-destinations).

### Privacyservice

[ Privacy Service schrappingsverzoeken ](../privacy.md) functie op de volgende manier, voor een bepaalde identiteit:

* Klantprofiel in realtime: verwijdert elk profielfragment met de opgegeven identiteitswaarde als primaire identiteit. **De primaire identiteit op Profiel zal nu gebaseerd op namespace prioriteit worden bepaald.**
* Gegevensmeer: hiermee verwijdert u alle records met de opgegeven identiteit als primaire of secundaire identiteit.

Voor meer informatie, lees het [ de dienstoverzicht van de Privacy ](../../privacy-service/home.md).

### Adobe Target

Bij gebruik van randsegmentatie kan Adobe Target onverwachte gebruikersgerichtheid voor scenario&#39;s voor gedeelde apparaten opleveren.