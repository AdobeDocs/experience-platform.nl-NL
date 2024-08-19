---
title: Prioriteit naamruimte
description: Leer over namespace prioriteit in de Dienst van de Identiteit.
badge: Beta
exl-id: bb04f02e-3826-45af-b935-752ea7e6ed7c
source-git-commit: c9610f935a074adf82d96c1eb824c159b18f2837
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 0%

---

# Prioriteit naamruimte

>[!AVAILABILITY]
>
>De regels voor identiteitsgrafiekkoppelingen staan momenteel in bèta. Neem contact op met het accountteam van de Adobe voor meer informatie over de deelnemingscriteria. De functie en documentatie kunnen worden gewijzigd.

Elke klantenimplementatie is uniek en gemaakt om de doelstellingen van een bepaalde organisatie te ontmoeten, en als dusdanig, varieert het belang van bepaalde namespace van klant tot klant. Voorbeelden in de praktijk zijn:

* Aan de ene kant zou u de naamruimte E-mail kunnen beschouwen als een persoonentiteit en dus uniek per persoon. Anderzijds, zou een andere klant e-mailnamespace als onbetrouwbare herkenningsteken kunnen beschouwen en daarom kunnen zij één enkele identiteitskaart van CRM toestaan om aan veelvoudige identiteiten met e-mailnamespace worden geassocieerd.
* U kunt online gedrag verzamelen met behulp van een naamruimte &quot;Aanmeldings-id&quot;. Deze login identiteitskaart kon een 1:1 verhouding met identiteitskaart van CRM hebben, die dan attributen van een systeem van CRM opslaat en als belangrijkste namespace kan worden beschouwd. In dit geval, bepaalt u dan dat identiteitskaart van CRM namespace een nauwkeurigere vertegenwoordiging van een persoon is, terwijl login identiteitskaart namespace het tweede belangrijkste is.

U moet configuraties maken in Identiteitsservice die het belang van uw naamruimten weerspiegelen, aangezien dit van invloed is op de manier waarop profielen worden gevormd en gesegmenteerd.

## Uw prioriteiten bepalen

De bepaling van naamruimteprioriteit is gebaseerd op de volgende factoren:

### Identiteitsgrafiekstructuur

Als de gestructureerde grafiek van uw organisatie gelaagd is, dan zou de namespaceprioriteit op dit moeten wijzen zodat de correcte verbindingen in het geval van grafiekinstorting worden verwijderd.

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

Een andere manier om dit onderwerp te benaderen is door kardinaliteit. Hoeveel identiteiten worden er voor een bepaalde personenentiteit gecreëerd? In de meeste gevallen zal een persoon één CRM-id hebben, een handvol hardware-id&#39;s (IDFA/GAID-voorinstellingen mogen niet vaak voorkomen) en nog meer cookies (een individu zou zich op meerdere apparaten kunnen begeven, de incognitomodus kunnen gebruiken of cookies op een bepaald moment kunnen herstellen). Over het algemeen, **lagere kardinaliteit wijst op een namespace met een hogere waarde**.

## Valideer uw instellingen voor naamruimteprioriteit

Zodra u een idee van hebt hoe u aan uw namespaces voorrang zult geven, kunt u het hulpmiddel van de Simulatie van de Grafiek gebruiken om diverse scenario&#39;s van de grafiekondergang uit te testen en ervoor te zorgen dat uw prioritaire configuraties de verwachte grafiekresultaten terugkeren. Voor meer informatie, lees de gids bij het gebruiken van het [ hulpmiddel van de Simulatie van de Grafiek ](./graph-simulation.md).

## Naamruimteprioriteit configureren

De prioriteit Namespace kan worden gevormd gebruikend [!UICONTROL Identity Settings]. In de interface [!UICONTROL Identity Settings] kunt u een naamruimte slepen en neerzetten om het relatieve belang ervan te bepalen.

>[!IMPORTANT]
>
>U kunt geen voorkeur geven aan naamruimten van apparaten/cookies boven naamruimten van personen. Deze beperking zorgt ervoor dat de misconfiguraties niet voorkomen.

## Prioriteitsgebruik voor naamruimte

Momenteel, beïnvloedt de nameprioriteit systeemgedrag van het Profiel van de Klant in real time. In het onderstaande diagram wordt dit concept geïllustreerd. Voor meer informatie, lees de gids op [ Adobe Experience Platform en de diagrammen van de toepassingsarchitectuur ](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications).

![ een diagram van namespace prioritaire toepassingswerkingsgebied ](../images/namespace-priority/application-scope.png)

### Identiteitsservice: algoritme voor identiteitsoptimalisatie

Voor relatief complexe grafiekstructuren speelt naamruimteprioriteit een belangrijke rol bij het verwijderen van de juiste koppelingen wanneer de scenario&#39;s voor het samenvouwen van grafieken worden uitgevoerd. Voor meer informatie lees het [ overzicht van het algoritme van de identiteitsoptimalisering ](../identity-graph-linking-rules/identity-optimization-algorithm.md).

### Klantprofiel in realtime: primaire identiteitsbepaling voor ervaringsgebeurtenissen

* Voor ervaringsgebeurtenissen, zodra u Identiteitsinstellingen voor een bepaalde sandbox hebt geconfigureerd, wordt de primaire identiteit bepaald door de hoogste naamruimteprioriteit.
   * Dit komt omdat ervaringsgebeurtenissen dynamisch van aard zijn. Een identiteitskaart kan drie of meer identiteiten bevatten, en namespace prioriteit zorgt ervoor dat belangrijkste namespace aan de ervaringsgebeurtenis wordt geassocieerd.
* Dientengevolge, zullen de volgende configuraties **niet meer door Real-Time Profiel van de Klant** worden gebruikt:
   * Het selectievakje &quot;Primair&quot; op het elementtype data in WebSDK (dat naar `primary=true` in identityMap vertaalt). **Nota**: De naamruimte van de identiteit en de identiteitswaarde zullen in Profiel blijven worden gebruikt. Bovendien moet u nog uw &quot;Primaire&quot;checkbox montages vormen omdat de diensten buiten het Profiel van de Klant in real time naar deze configuratie zullen blijven verwijzen.
   * Alle velden die als primaire identiteit zijn gemarkeerd in een schema van de klasse Event van de XDM-ervaring.
   * Standaard primaire identiteitsinstellingen in de Adobe Analytics-bronconnector (ECID of AID).
* Anderzijds, **namespace de prioriteit bepaalt geen primaire identiteit voor profielverslagen**.
   * Voor profielverslagen, kunt u de schemawerkruimte in de UI van het Experience Platform gebruiken om uw identiteitsgebieden, met inbegrip van de primaire identiteit te bepalen. Lees de gids op [ bepalend identiteitsgebieden in UI ](../../xdm/ui/fields/identity.md) voor meer informatie.

>[!TIP]
>
>* De prioriteit van Namespace is **een bezit van een namespace**. Het is een numerieke waarde die aan een naamruimte wordt toegewezen om het relatieve belang ervan aan te geven.
>
>* Primaire identiteit is de identiteit waarin een profielfragment wordt opgeslagen. Een profielfragment is een record met gegevens waarin informatie over een bepaalde gebruiker wordt opgeslagen: kenmerken (gewoonlijk opgenomen via CRM-records) of gebeurtenissen (gewoonlijk opgenomen via ervaringsgebeurtenissen of online gegevens).

### Voorbeeldgrafiekscenario

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

| Handeling van de gebruiker (Experience-gebeurtenis) | Verificatiestatus | Gegevensbron | Identiteitskaart | Primaire identiteit (primaire sleutel van profielfragment) |
| --- | --- | --- | --- | --- |
| Pagina met creditcardaanbiedingen weergeven | Niet geverifieerd (anoniem) | Web SDK | {ECID} | ECID |
| Help-pagina weergeven | Niet geverifieerd | Mobiele SDK | {ECID, IDFA} | IDFA |
| Accountbalans bekijken | Geverifieerd | Web SDK | {CRM ID, ECID} | CRM-id |
| Aanmelden voor thuislening | Geverifieerd | Bronconnector voor analyse | {CRM ID, ECID, HULP} | CRM-id |
| Breng $1.000 van controle aan besparingen over | Geverifieerd | Mobiele SDK | {CRM ID, GAID, ECID} | CRM-id |

{style="table-layout:auto"}

### Segmentatieservice: opslag van metagegevens voor segmentlidmaatschap

![ A diagram van de opslag van het segmentlidmaatschap ](../images/namespace-priority/segment-membership-storage.png)

Voor een bepaald samengevoegd profiel, zullen de segmentlidmaatschappen tegen de identiteit met hoogste prioriteit worden opgeslagen namespace.

Stel dat er twee profielen zijn:

* Het eerste profiel vertegenwoordigt John.
* Het tweede profiel staat voor Jane.

Als de John en Jane een apparaat delen, dan brengt ECID (Webbrowser) van één persoon aan een andere over. Nochtans, beïnvloedt dit niet de informatie van het segmentlidmaatschap die tegen John en Jane wordt opgeslagen.

Als de segmentkwalificatiecriteria uitsluitend gebaseerd waren op anonieme gebeurtenissen die tegen de ECID waren opgeslagen, zou Jane in aanmerking komen voor dat segment

## Gevolgen voor andere diensten van de Experience Platform {#implications}

In deze sectie wordt beschreven hoe naamruimteprioriteit van invloed kan zijn op andere services van Experience Platforms.

### Geavanceerd levenscyclusbeheer van gegevens

Gegevens-hygiënebestanden verwijderen de aanvraagfuncties voor een bepaalde identiteit op de volgende manier:

* Klantprofiel in realtime: verwijdert elk profielfragment met de opgegeven identiteit als primaire identiteit. **De primaire identiteit op Profiel zal nu gebaseerd op namespace prioriteit worden bepaald.**
* Gegevensmeer: hiermee verwijdert u alle records met de opgegeven identiteit als primaire identiteit.

Voor meer informatie, lees het [ geavanceerde overzicht van het levenscyclusbeheer ](../../hygiene/home.md).

### Berekende kenmerken

Berekende kenmerken gebruiken geen naamruimteprioriteit voor het berekenen van waarden. Als u gegevens verwerkte attributen gebruikt, moet u ervoor zorgen dat identiteitskaart van CRM als uw primaire identiteit voor WebSDK wordt aangewezen. Deze beperking zal naar verwachting in augustus 2024 worden opgelost.

Voor meer informatie, lees de [ gegevens verwerkte handleiding van attributen UI ](../../profile/computed-attributes/ui.md).

### Gegevensmeer

Het opnemen van gegevens aan gegevens zal meer de primaire identiteitsmontages blijven respecteren die op [ worden gevormd SDK van het Web ](../../tags/extensions/client/web-sdk/data-element-types.md#identity-map) en schema&#39;s.

Het meer van gegevens zal geen primaire identiteit bepalen die op namespaceprioriteit wordt gebaseerd. Bijvoorbeeld, zal Adobe Customer Journey Analytics waarden in de identiteitskaart blijven gebruiken zelfs nadat namespace de prioriteit wordt toegelaten (zoals, toevoegend een dataset aan een nieuwe verbinding), omdat de Customer Journey Analytics hun gegevens van gegevens meer verbruikt.

### Schema&#39;s voor Experience Data Model (XDM)

Om het even welk schema dat geen Gebeurtenis van de Ervaring XDM, zoals Individuele Profielen XDM is, zal blijven om het even welke [ gebieden respecteren die u als identiteit ](../../xdm/ui/fields/identity.md) merkt.

Voor meer informatie over schema&#39;s XDM, lees het [ schema&#39;s overzicht ](../../xdm/home.md).

### Intelligente diensten

Wanneer u uw gegevens selecteert, moet u een naamruimte opgeven die wordt gebruikt om de gebeurtenissen te bepalen die de scores berekenen en de gebeurtenissen die de berekende scores opslaan. U wordt aangeraden de naamruimte te selecteren die een persoon vertegenwoordigt.

* Als u gegevens van het Webgedrag gebruikend WebSDk verzamelt, wordt u geadviseerd om identiteitskaart van CRM te kiezen namespace binnen de identiteitskaart.
* Als u gegevens over webgedrag verzamelt via de bronconnector van Analytics, moet u de identiteitsdescriptor (CRM-id) selecteren.

Deze configuratie resulteert in computerscores die alleen gebruikmaken van geverifieerde gebeurtenissen.

Voor meer informatie over, lees de documenten op [ Attribution AI ](../../intelligent-services/attribution-ai/overview.md) en [ Klant AI ](../../intelligent-services/customer-ai/overview.md).

### Privacyservice

[ de verzoeken van de schrapping van de Privacy Service ](../privacy.md) functie op de volgende manier, voor een bepaalde identiteit:

* Klantprofiel in realtime: verwijdert elk profielfragment met de opgegeven identiteitswaarde als primaire identiteit. **De primaire identiteit op Profiel zal nu gebaseerd op namespace prioriteit worden bepaald.**
* Gegevensmeer: hiermee verwijdert u alle records met de opgegeven identiteit als primaire of secundaire identiteit.

Voor meer informatie, lees het [ de dienstoverzicht van de Privacy ](../../privacy-service/home.md).

### Adobe Target en randpersonalisatie

[ de verpersoonlijking van Edge ](../../server-api/personalization-target.md) zal blijven verwijzen naar hoe u uw &quot;Primaire&quot;checkbox op het type van gegevenselement in WebSDK vormde (die aan `primary=true` in identityMap vertaalt).