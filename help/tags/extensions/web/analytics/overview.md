---
title: Overzicht Adobe Analytics-extensie
description: Meer informatie over de Adobe Analytics-tagextensie in Adobe Experience Platform.
source-git-commit: 8dfb7bdc16d0654ee1d76dc5f5af50938b122d33
workflow-type: tm+mt
source-wordcount: '2179'
ht-degree: 2%

---

# Overzicht Adobe Analytics-extensie

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Gebruik deze verwijzing voor informatie over het vormen van de uitbreiding van Adobe Analytics, en de opties beschikbaar wanneer het gebruiken van deze uitbreiding om een regel te bouwen.

## De Adobe Analytics-extensie configureren

Deze sectie bevat een verwijzing naar de opties die beschikbaar zijn bij het configureren van de Adobe Analytics-extensie.

Als de extensie Adobe Analytics nog niet is geïnstalleerd, opent u de eigenschap en selecteert u **[!UICONTROL Extensions > Catalog]**, plaatst u de aanwijzer op de extensie Adobe Analytics en selecteert u **[!UICONTROL Install]**.

Als u de extensie wilt configureren, opent u het tabblad Extensies, plaatst u de muisaanwijzer op de extensie en selecteert u **[!UICONTROL Configure]**.

![](../../../images/ext-analytics-config.png)

## Bibliotheekbeheer

Selecteer een optie in de sectie Bibliotheekbeheer van de configuratiepagina. De volgende configuratieopties zijn beschikbaar:

### De bibliotheek voor mij beheren

#### Rapportsuites

Geef een of meer rapportsuites op voor elk van de volgende omgevingen:

* Ontwikkeling
* Staging
* Productie

### De bibliotheek gebruiken die al op de pagina is geïnstalleerd

#### De volgende rapportsuites instellen in Beheer

Als u deze optie selecteert, geeft u een of meer rapportsuites op voor elk van de volgende omgevingen:

* Ontwikkeling
* Staging
* Productie

#### De module Activiteitenoverzicht gebruiken

De activiteitenkaart wordt geladen als afzonderlijke module (zoals de module van de AAM). Standaard is een activiteitenoverzicht ingeschakeld, maar als u deze liever zou uitschakelen, kunt u dit doen door het selectievakje in de configuratie uit te schakelen.

#### Beheer is toegankelijk voor de algemene variabele met de naam

Als u dit selectievakje inschakelt, kan het tracker-object globaal worden gebruikt. U kunt bijvoorbeeld de variabele `window.s.pageName` ergens op uw site definiëren.

### De bibliotheek laden via een aangepaste URL

#### HTTP-URL

Geef de URL op waar de bibliotheek zich bevindt.

#### HTTPS-URL

Geef de URL op waar de bibliotheek zich bevindt.

#### De volgende rapportsuites instellen in Beheer

Als u deze optie selecteert, geeft u een of meer rapportsuites op voor elk van de volgende omgevingen:

* Ontwikkeling
* Staging
* Productie

#### Beheer is toegankelijk voor de algemene variabele met de naam

Geef het trackerobject op dat globaal moet worden gebruikt.

### Aangepaste bibliotheekcode opgeven

#### Editor openen

Hiermee kunt u code [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html) invoegen. Deze code wordt automatisch gevuld wanneer het gebruiken van de automatische configuratiemethode.

>[!NOTE]
>
>De validator die in de tagcode-editor wordt gebruikt, is ontworpen om problemen met door ontwikkelaars geschreven code te identificeren. Code die een minificatieproces heeft doorlopen, zoals de code AppMeasurement.js die is gedownload van de Manager van de Code, zou verkeerd kunnen worden gemarkeerd als hebbend kwesties door de markeringsvalidator, die gewoonlijk kan worden genegeerd.

#### De volgende rapportsuites instellen in Beheer

Als u deze optie selecteert, geeft u een of meer rapportsuites op voor elk van de volgende omgevingen:

* Ontwikkeling
* Staging
* Productie

#### Beheer is toegankelijk voor de algemene variabele met de naam

Geef het trackerobject op dat globaal moet worden gebruikt.

## Algemeen

Selecteer een optie in het gedeelte Algemeen van de configuratiepagina. De volgende configuratieopties zijn beschikbaar:

### EU-conformiteit voor Adobe Analytics inschakelen

Hiermee wordt het bijhouden van gegevens op basis van het privacycookie van de EU in- of uitgeschakeld.

Wanneer u het selectievakje EU-conformiteit inschakelt, wordt het veld [!UICONTROL Tracking Cookie Name] weergegeven. De Cookie bijhouden overschrijft de standaardnaam van het volgende cookie. U kunt de naam die tags gebruiken aanpassen om de status van uw uitschakelfunctie bij te houden voor het ontvangen van andere cookies.

Wanneer een pagina wordt geladen, controleert het systeem of is een cookie met de naam sat\_track ingesteld (of de aangepaste cookienaam die is opgegeven op de pagina Eigenschap bewerken). Overweeg de volgende informatie:

* Als het cookie niet bestaat of als het cookie bestaat en op iets anders is ingesteld dan true, wordt het laden van het gereedschap overgeslagen wanneer deze instelling is ingeschakeld. Betekenis, zal om het even welk gedeelte van een regel die het hulpmiddel gebruikt niet van toepassing zijn. Als een regel analyses bevat van EU-conformiteit op en code van derden en het cookie is ingesteld op false, wordt de code van derden nog steeds uitgevoerd. De analytische variabelen worden echter niet ingesteld.
* Als het cookie bestaat maar is ingesteld op true, wordt het gereedschap normaal geladen.

U bent verantwoordelijk voor het instellen van het cookie sat\_track (of aangepaste benoemde cookies) op false als een bezoeker het cookie uitschakelt. U kunt dit bereiken met behulp van aangepaste code:

```javascript
_satellite.cookie.set("sat_track", "false");
```

U moet ook een mechanisme hebben om die cookie in te stellen op true als u wilt dat een bezoeker zich later kan aanmelden:

```javascript
_satellite.cookie.set("sat_track", "true");
```

### Tekenset

Hiermee bepaalt u hoe de afbeeldingsaanvraag wordt gecodeerd. Als in uw implementatie of site niet-ASCII-tekens worden gebruikt, is het belangrijk dat u hier een tekenset definieert. U kunt een vooraf ingestelde tekenset selecteren of een aangepaste tekenset opgeven. Adobe raadt u aan dezelfde tekencodering als uw site te gebruiken. Deze waarde is doorgaans UTF-8.

Tekenset kan in aangepaste code Analytics worden ingesteld met de variabele `s.charSet`.
Raadpleeg de [charSet-documentatie](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/charset.html) voor meer informatie over tekensets.

### Valutacode

Bepaalt de omrekeningskoers die moet worden toegepast op inkomsten- en valutagebeurtenissen. Als bezoekers op uw site in meerdere valuta&#39;s kunnen kopen, zorgt het instellen van de valutacode ervoor dat het geldbedrag correct wordt omgezet en opgeslagen.

Zie [currencyCode](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/currencycode.html) voor meer informatie over de ondersteunde valutacodes.

### Trackingserver

Gebruikt voor de implementaties van het eerste-partijkoekje om te dicteren waar het eerste-partijkoekje wordt opgeslagen. Als u de dienst van identiteitskaart van de Experience Cloud gebruikt, adviseert Adobe tegen het bevolken van dit gebied.

Trackingserver kan in aangepaste code voor Analytics worden ingesteld met de variabele `s.trackingServer`.

Zie [trackingServer](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackingserver.html) in de handleiding voor Adobe Analytics-implementatie.

### SSL-traceringsserver

Gebruikt voor SSL first-party koekjesimplementaties om te dicteren waar het eerste-partijkoekje wordt opgeslagen. Als u de dienst van identiteitskaart van de Experience Cloud gebruikt, adviseert Adobe tegen het bevolken van dit gebied. Als deze optie niet is gedefinieerd, gebruiken SSL-gegevens Tracking Server.

SSL het Volgen Server kan in de aangepaste code van de Analyse worden geplaatst gebruikend veranderlijke `s.trackingServerSecure`.

Zie [trackingServerSecure](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackingserversecure.html).

## Algemene variabelen

Gebruik deze sectie aan opstelling [eVars en Props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html), en om hiërarchieën tot stand te brengen.

Algemene variabelen zijn variabelen die in het object Analytics tracking worden ingesteld wanneer dat object op de pagina wordt geïnitialiseerd. Alle variabelen die u hier instelt, worden ingesteld wanneer het volgende object op elke pagina wordt gemaakt. Als deze variabelen eenmaal zijn ingesteld, zijn ze net als alle andere variabelen die op een andere manier zijn ingesteld. Specifiek, betekent dit dat een regel deze variabelen kan wijzigen, veranderen of ontruimen.

Als uw webtoepassing normaal gesproken één baken per pagina verzendt, kunt u met deze sectie het eenvoudig maken om uw variabelen op één plaats in te stellen. Als uw toepassing meer dan één baken per pagina verzendt (zoals in een toepassing van één pagina), en u moet uw variabelen ontruimen en hen terugstellen gebruikend het zelfde het volgen voorwerp, is het eenvoudiger om op regels te vertrouwen om uw variabelen te plaatsen en te ontruimen.

## Koppelingen bijhouden

Selecteer een optie in de sectie Koppeling bijhouden van de configuratiepagina. De volgende configuratieopties zijn beschikbaar:

### ClickMap inschakelen

[](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html) ClickMapis een stop-in voor Internet Explorer en Firefox, en een module van Rapporten &amp; Analytics.

### Download-koppelingen volgen

Koppelingen naar downloadbare bestanden op uw site bijhouden.

Zie [s.trackDownLoadLinks](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackdownloadlinks.html).

### Extensies downloaden

Als de optie Koppelingen voor downloaden bijhouden is ingeschakeld, kunt u de extensies selecteren van de bestandskoppelingen die worden opgenomen in het rapport Downloads. Als uw site koppelingen bevat naar bestanden met een van de vermelde extensies, worden de URL&#39;s van deze koppelingen weergegeven in de rapportage.

Zie [s.linkDownloadFileTypes](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/linkdownloadfiletypes.html).

### Uitgaande koppelingen bijhouden

Hiermee wordt bepaald of een geselecteerde koppeling een afsluitkoppeling is.

Zie [s.trackExternalLinks](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackexternallinks.html).

**Overwegingen bij de toepassing van één pagina:** vanwege de manier waarop sommige SPA websites zijn gecodeerd, ziet een interne koppeling naar een pagina op de SPA-site er mogelijk uit als een uitgaande koppeling.

U kunt een van de volgende methoden gebruiken om uitgaande koppelingen van SPA sites bij te houden:

* Als u geen uitgaande verbindingen van uw SPA wilt volgen, neem een ingang in de nooit sectie van het Spoor op.  Bijvoorbeeld, `http://testsite.com/spa/\#`. Alle \#-koppelingen naar deze host worden genegeerd. Alle uitgaande verbindingen aan andere gastheren worden gevolgd, zoals [https://www.google.com](https://www.google.com).
* Als er sommige verbindingen zijn die u op uw SPA wilt volgen, gebruik altijd de sectie van het Spoor.

Als u bijvoorbeeld een pagina met een spa/\#/about hebt, kunt u &quot;about&quot; plaatsen in de sectie Altijd bijhouden.

De pagina &quot;about&quot; is de enige uitgaande koppeling die wordt bijgehouden. Eventuele andere koppelingen op de pagina (bijvoorbeeld [https://www.google.com](https://www.google.com)) worden niet bijgehouden.

>[!NOTE]
>
>Deze twee opties sluiten elkaar uit.

### URL-parameters behouden

Zoektekenreeksen blijven behouden.

Zie [s.linkLeaveQueryString](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/linkleavequerystring.html).

## Cookies

Configureer veldbeschrijvingen voor de algemene instellingen voor cookies die worden gebruikt voor het implementeren van de Adobe Analytics-extensie. De volgende configuratieopties zijn beschikbaar:

### Bezoekers-id

Unieke waarde die een klant in zowel de online als off-line systemen vertegenwoordigt.

Zie [bezoekerID](https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html).

### Naamruimte van bezoeker

Variabele waarmee het domein wordt geïdentificeerd waarmee cookies worden ingesteld.

Zie [bezoekorNamespace](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitornamespace.html).

### Domeinperioden

Het domein waarop het Analytics-cookie `s_cc` en `s_sq` worden ingesteld door het aantal punten in het domein van de pagina-URL te bepalen. Deze variabele wordt ook gebruikt door bepaalde plug-ins voor het bepalen van het juiste domein voor het instellen van het cookie van de plug-in.

Zie [s.cookieDomainPeriods](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/cookiedomainperiods.html).

### Domeinperioden van de eerste partij

De variabele `fpCookieDomainPeriods` is voor cookies die zijn ingesteld door JavaScript (`s_sq`, `s_cc`, plug-ins) die inherent cookies van eerste bedrijven zijn, zelfs als in uw implementatie de domeinen 2o7.net of omtr dc.net van derden worden gebruikt.

Zie [s.fpCookieDomainPeriods](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/fpcookiedomainperiods.html).

### Cookie Lifetime

Hiermee bepaalt u de levensduur van een cookie.

Zie [s.cookieLifetime](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/cookielifetime.html).

### Beveiligde cookies

Met deze variabele kan AppMeasurement beveiligde cookies schrijven.

Zie [writeSecureCookies](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/writesecurecookies.html)


## Paginacode aanpassen

Gebruik de editor om de paginacode aan te passen.

## Adobe Audience Manager

Gebruik deze sectie van de uitbreidingsconfiguratie om te specificeren hoe de Audience Manager met Analytics werkt.

Schakel **Analysegegevens automatisch delen met Audience Manager** in.

De volgende opties worden weergegeven:

![](../../../images/an-ext-aam.png)

Het subdomein Audience Manager wordt toegewezen door Adobe Audience Manager. Het wordt soms bedoeld als uw &quot;Naam van de Partner&quot;of &quot;Subdomain van de Partner.&quot; Neem contact op met uw Adobe-consultant of klantenservice als u uw partnernaam niet kent.

U kunt geavanceerde instellingen configureren door **Geavanceerde instellingen tonen** te selecteren en uw voorkeuren in te voeren.

![](../../../images/an-ext-aam-adv.png)

Voor informatie over elke het plaatsen, selecteer het infopictogram, of verwijs naar de [documentatie van Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html).

## Handelingstypen voor analytische extensies

In deze sectie worden de actietypen beschreven die beschikbaar zijn in de extensie Analytics.

De extensie Analytics biedt de volgende handelingen:

* [Variabelen instellen](#set-variables)
* [Band verzenden](#send-beacon)
* [Variabelen wissen](#clear-variables)

### Variabelen instellen {#set-variables}

Belangrijk: Het gebruiken van een &quot;vastgestelde variabelen&quot;actie zal niet het baken verzenden. U moet de actie &quot;verzendt baken&quot;gebruiken.

#### eVars

Stel een of meer [eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html) in.

1. Selecteer een eVar in het vervolgkeuzemenu.
1. Geef op of u de eVar wilt instellen als de waarde (Instellen als) of kopiëren (Dupliceren vanuit) naar een ander eVar.
1. Geef een waarde op voor Instellen als of selecteer de eVar die u wilt dupliceren.
1. (Optioneel) Selecteer eVar toevoegen om meer eVars in te stellen.
1. Selecteer **[!UICONTROL Keep Changes]**.

#### Props

Stel een of meer [props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html) in.

1. Selecteer een eigenschap in het vervolgkeuzemenu.
1. Geef op of u de eigenschap wilt instellen als de waarde (Instellen als) of als kopie (Dupliceren van) van een ander eVar.
1. Geef een waarde op voor Instellen als of selecteer de eVar waaruit u de eigenschap wilt dupliceren.
1. (Optioneel) Selecteer **[!UICONTROL Add prop]** om meer eigenschappen in te stellen.
1. Selecteer **[!UICONTROL Keep Changes]**.

#### Gebeurtenissen

Stel een of meer [gebeurtenissen](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html) in.

1. Selecteer een gebeurtenis in het vervolgkeuzemenu.
1. (Optioneel) Selecteer of geef een gegevenselement op dat wordt gebruikt voor [gebeurtenisserialisatie](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/event-serialization.html).
1. (Optioneel) Selecteer **[!UICONTROL Add event]** om meer gebeurtenissen in te stellen.
1. Selecteer **[!UICONTROL Keep Changes]**.

#### Hiërarchie

Stel de variabele Analytics [Hierarchy](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html) in.

Geef elk niveau in de hiërarchie op.

Indien gewenst, vorm extra hiërarchieën.

#### Overige informatie

Geef andere gegevens op die door de pagina&#39;s worden gebruikt.

Deze instellingen zijn:

* Paginanaam
* Pagina-URL
* Server
* Kanaal
* Referrer
* Campaign
* Aankoop-id

   Een waarde of query-parameter opgeven

* Staat
* Postcode
* Transactie-id

U vindt deze instellingen in het menu Globale variabelen door het selectievakje Aanvullende instellingen in te schakelen.

#### Aangepaste paginacode

**Beschrijving**

Gebruik de editor om uw aangepaste paginacode op te geven.

**Instellingen**

1. Selecteer **[!UICONTROL Open Editor]**.
1. Typ de aangepaste code.
1. Selecteer **[!UICONTROL Save]**.

### Band verzenden {#send-beacon}

#### Een voorvertoning vergroten - s.t()

Selecteer deze optie als u een paginaweergave wilt vergroten.

#### Een paginaweergave niet verhogen - s.t()

Selecteer deze optie als u een voorvertoning niet wilt vergroten.

**Instellingen**

1. Selecteer een koppelingstype.

   U kunt een van de volgende opties selecteren:

   * Aangepaste koppeling
   * Koppeling downloaden
   * Koppeling afsluiten

1. Stel de parameter voor de geselecteerde koppeling in.
   * Aangepaste koppeling: Geef de naam van de koppeling op.
   * Koppeling downloaden: Geef een bestandsnaam op.
   * Koppeling afsluiten: Geef de doel-URL op.
1. Selecteer **[!UICONTROL Keep Changes]**.

### Variabelen wissen {#clear-variables}

Er zijn geen configuratieopties als het handelingstype Variabelen wissen is geselecteerd.
