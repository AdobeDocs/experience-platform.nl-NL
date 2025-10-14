---
title: Overzicht Adobe Analytics-extensie
description: Meer informatie over de Adobe Analytics-tagextensie in Adobe Experience Platform.
exl-id: 33ebdcb6-9bf0-44e6-b016-e93fe78af578
source-git-commit: 764a9a29df0be6064d36f952d2e8a61acfa9bd33
workflow-type: tm+mt
source-wordcount: '2309'
ht-degree: 2%

---

# Overzicht Adobe Analytics-extensie

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor dataverzameling in Adobe Experience Platform.  Als gevolg hiervan zijn er verschillende terminologiewijzigingen in de productdocumentatie doorgevoerd. Raadpleeg het volgende [&#x200B; document &#x200B;](../../../term-updates.md) voor een geconsolideerde referentie van de terminologiewijzigingen.

Gebruik deze verwijzing voor informatie over het vormen van de uitbreiding van Adobe Analytics, en de opties beschikbaar wanneer het gebruiken van deze uitbreiding om een regel te bouwen.

## De Adobe Analytics-extensie configureren

Deze sectie bevat een referentie voor de beschikbare opties bij het configureren van de Adobe Analytics-extensie.

Als de Adobe Analytics-extensie nog niet is geïnstalleerd, opent u de eigenschap en selecteert u **[!UICONTROL Extensions > Catalog]** , plaatst u de aanwijzer op de Adobe Analytics-extensie en selecteert u **[!UICONTROL Install]** .

Als u de extensie wilt configureren, opent u het tabblad Extensies, plaatst u de muisaanwijzer op de extensie en selecteert u **[!UICONTROL Configure]** .

![](../../../images/ext-analytics-config.png)

## Bibliotheekbeheer

Selecteer een optie in de sectie Bibliotheekbeheer van de configuratiepagina. De volgende configuratieopties zijn beschikbaar:

### Bibliotheek voor mij beheren

#### Rapportauites

Geef een of meer rapportsuites op voor elk van de volgende omgevingen:

* Ontwikkeling
* Staging
* Productie

### Gebruik de bibliotheek die al op de pagina is geïnstalleerd

#### De volgende rapportsuites instellen in Beheer

Als u deze optie selecteert, geeft u een of meer rapportsuites op voor elk van de volgende omgevingen:

* Ontwikkeling
* Staging
* Productie

#### De module Activiteitenoverzicht gebruiken

De activiteitenkaart wordt geladen als een afzonderlijke module (zoals de AAM module). Standaard is activiteitenoverzicht ingeschakeld, maar als u deze liever wilt uitschakelen, kunt u dit doen door het selectievakje in de configuratie uit te schakelen.

#### Beheer is toegankelijk voor de globale variabele genaamd

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

#### Beheer is toegankelijk voor de algemene variabele genaamd

Geef het trackerobject op dat globaal moet worden gebruikt.

### Aangepaste bibliotheekcode opgeven

#### Editor openen

Laat u kern [&#x200B; AppMeasurement.js &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=nl-NL) code opnemen. Deze code wordt automatisch gevuld wanneer het gebruiken van de automatische configuratiemethode.

>[!NOTE]
>
>De validator die in de tagcode-editor wordt gebruikt, is ontworpen om problemen met door ontwikkelaars geschreven code te identificeren. De code die door een minificatieproces-zoals code AppMeasurement.js is gegaan die van de Manager van de Code wordt gedownload - zou verkeerd kunnen worden gemarkeerd zoals hebbend kwesties door de markeringsvalidator, die gewoonlijk kan worden genegeerd.

#### De volgende rapportsuites instellen in Beheer

Als u deze optie selecteert, geeft u een of meer rapportsuites op voor elk van de volgende omgevingen:

* Ontwikkeling
* Staging
* Productie

#### Beheer is toegankelijk voor de algemene variabele genaamd

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

Tekenset kan in aangepaste code Analytics worden ingesteld met de variabele `s.charSet` .
Voor meer informatie over karakterreeksen, zie de [&#x200B; charSet documentatie &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/charset.html?lang=nl-NL).

### Valuta

Bepaalt de omrekeningskoers die moet worden toegepast op inkomsten- en valutagebeurtenissen. Als bezoekers op uw site in meerdere valuta&#39;s kunnen kopen, kunt u door de valutacode in te stellen ervoor zorgen dat het geldbedrag correct wordt omgezet en opgeslagen.

Voor meer informatie over de gesteunde muntcodes, zie [&#x200B; currencyCode &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/currencycode.html?lang=nl-NL).

### Trackingserver

Gebruikt voor de implementaties van het eerste-partijkoekje om te dicteren waar het eerste-partijkoekje wordt opgeslagen. Als u de Dienst van identiteitskaart van het Experience Cloud gebruikt, adviseert de Adobe tegen het bevolken van dit gebied.

Trackingserver kan in aangepaste code voor Analytics worden ingesteld met de variabele `s.trackingServer` .

Zie [&#x200B; trackingServer &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackingserver.html?lang=nl-NL) in de gids van de Implementatie van Adobe Analytics.

### SSL-tracking-server

Wordt gebruikt voor SSL-first-party-cookimimplementaties om te bepalen waar het first-party cookie wordt opgeslagen. Als u de Experience Cloud-id-service gebruikt, wordt u aangeraden dit veld niet te vullen met een Adobe. Als deze niet is gedefinieerd, gebruiken SSL-gegevens de Tracking-server.

SSL Tracking Server kan worden ingesteld in aangepaste code Analytics met behulp van de variabele `s.trackingServerSecure` .

Zie [&#x200B; trackingServerSecure &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackingserversecure.html?lang=nl-NL).

## Algemene variabelen

Gebruik deze sectie aan opstelling [&#x200B; eVars en Props &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html?lang=nl-NL), en om hiërarchieën tot stand te brengen.

Globale variabelen zijn variabelen die in het object Analytics tracking worden ingesteld wanneer dat object op de pagina wordt geïnitialiseerd. Alle variabelen die u hier instelt, worden ingesteld wanneer het volgende object op elke pagina wordt gemaakt. Als deze variabelen eenmaal zijn ingesteld, zijn ze net als alle andere variabelen die op een andere manier zijn ingesteld. Specifiek, betekent dit dat een regel deze variabelen kan wijzigen, veranderen of ontruimen.

Als uw webtoepassing normaal gesproken één baken per pagina verzendt, kunt u met deze sectie het eenvoudig maken om uw variabelen op één plaats in te stellen. Als uw toepassing meer dan één baken per pagina verzendt (zoals in een toepassing van één pagina), en u moet uw variabelen ontruimen en hen terugstellen gebruikend het zelfde het volgen voorwerp, is het eenvoudiger om op regels te vertrouwen om uw variabelen te plaatsen en te ontruimen.

## Koppelingen bijhouden

Selecteer een optie in de sectie Koppeling bijhouden van de configuratiepagina. De volgende configuratieopties zijn beschikbaar:

### ClickMapen inschakelen

[&#x200B; ClickMap &#x200B;](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html?lang=nl-NL) is een elektrisch toestel voor Internet Explorer en Firefox, en een module van Rapporten &amp; Analytics.

### Download-koppelingen volgen

Koppelingen naar downloadbare bestanden op uw site bijhouden.

Zie [&#x200B; s.trackDownLoadLinks &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackdownloadlinks.html?lang=nl-NL).

### Extensies downloaden

Als de optie Koppelingen voor downloaden bijhouden is ingeschakeld, kunt u de extensies selecteren van de bestandskoppelingen die worden opgenomen in het rapport Downloads. Als uw site koppelingen bevat naar bestanden met een van de vermelde extensies, worden de URL&#39;s van deze koppelingen weergegeven in de rapportage.

Zie [&#x200B; s.linkDownloadFileTypes &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/linkdownloadfiletypes.html?lang=nl-NL).

### Uitgaande koppelingen bijhouden

Hiermee wordt bepaald of een geselecteerde koppeling een afsluitkoppeling is.

Zie [&#x200B; s.trackExternalLinks &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackexternallinks.html?lang=nl-NL).

**Enige-Pagina App Overwegingen:** wegens de manier sommige SPA websites worden gecodeerd, zou een interne verbinding aan een pagina op de SPA plaats kunnen kijken als het een uitgaande verbinding is.

U kunt een van de volgende methoden gebruiken om uitgaande koppelingen van SPA sites bij te houden:

* Als u geen uitgaande verbindingen van uw SPA wilt volgen, neem een ingang in de nooit sectie van het Spoor op.  Bijvoorbeeld `http://testsite.com/spa/\#` . Alle \#-koppelingen naar deze host worden genegeerd. Alle uitgaande verbindingen aan andere gastheren worden gevolgd, zoals [&#x200B; https://www.google.com &#x200B;](https://www.google.com).
* Als er sommige verbindingen zijn die u op uw SPA wilt volgen, gebruik altijd de sectie van het Spoor.

Als u bijvoorbeeld een pagina met een spa/\#/about hebt, kunt u &quot;about&quot; plaatsen in de sectie Altijd bijhouden.

De pagina &quot;about&quot; is de enige uitgaande koppeling die wordt bijgehouden. Om het even welke andere verbindingen op de pagina (bijvoorbeeld, [&#x200B; https://www.google.com &#x200B;](https://www.google.com)) worden niet gevolgd.

>[!NOTE]
>
>Deze twee opties sluiten elkaar uit.

### URL-parameters behouden

Zoektekenreeksen blijven behouden.

Zie [&#x200B; s.linkLeaveQueryString &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/linkleavequerystring.html?lang=nl-NL).

## Cookies

Configureer veldbeschrijvingen voor de algemene instellingen voor cookies die worden gebruikt voor het implementeren van de Adobe Analytics-extensie. De volgende configuratieopties zijn beschikbaar:

### Bezoeker-id

Unieke waarde die een klant in zowel de online als off-line systemen vertegenwoordigt.

Zie [&#x200B; bezoekorID &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html?lang=nl-NL).

### Naamruimte van bezoeker

Variabele waarmee het domein wordt geïdentificeerd waarmee cookies worden ingesteld.

Zie [&#x200B; bezoekorNamespace &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitornamespace.html?lang=nl-NL).

### Domeinperioden

Het domein waarop het Analytics-cookie `s_cc` en `s_sq` worden ingesteld door het aantal punten in het domein van de pagina-URL te bepalen. Deze variabele wordt ook gebruikt door bepaalde plug-ins voor het bepalen van het juiste domein voor het instellen van het cookie van de plug-in.

Zie [&#x200B; s.cookieDomainPeriods &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/cookiedomainperiods.html?lang=nl-NL).

### Domeinperioden van de eerste partij

De variabele `fpCookieDomainPeriods` is voor cookies die zijn ingesteld door JavaScript (`s_sq` , `s_cc` , plug-ins) en die inherent eerstehands cookies zijn, zelfs als in uw implementatie de domeinen van derden 2o7.net of omtrdc.net worden gebruikt.

Zie [&#x200B; s.fpCookieDomainPeriods &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/fpcookiedomainperiods.html?lang=nl-NL).

### Cookie Lifetime

Bepaalt de levensduur van een cookie.

Zie [&#x200B; s.cookieLifetime &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/cookielifetime.html?lang=nl-NL).

### Beveiligde cookies

Met deze variabele kan AppMeasurement beveiligde cookies schrijven.

Zie [&#x200B; writeSecureCookies &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/writesecurecookies.html?lang=nl-NL)


## Paginacode aanpassen

Gebruik de editor om uw paginacode aan te passen.

## Adobe Audience Manager

Gebruik dit gedeelte van de extensieconfiguratie om op te geven hoe Audience Manager werkt met Analytics.

Laat **automatisch delen de gegevens van de Analytics met Audience Manager** toe.

De volgende opties worden weergegeven:

![](../../../images/an-ext-aam.png)

Het subdomein Audience Manager wordt toegewezen door Adobe Audience Manager. Het wordt soms bedoeld als uw &quot;Naam van de Partner&quot;of &quot;Subdomain van de Partner.&quot; Neem contact op met uw Adobe-consultant of klantenservice als u uw partnernaam niet kent.

U kunt geavanceerde montages vormen door **te selecteren tonen geavanceerde montages** en uw voorkeur in te gaan.

![](../../../images/an-ext-aam-adv.png)

Voor informatie over elke het plaatsen, selecteer het infopictogram, of verwijs naar de [&#x200B; documentatie van Adobe Audience Manager &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=nl-NL).

## Typen handelingen voor extensies voor Analytics

In deze sectie worden de actietypen beschreven die beschikbaar zijn in de extensie Analytics.

De extensie Analytics biedt de volgende handelingen:

* [Variabelen instellen](#set-variables)
* [Bandbaken verzenden](#send-beacon)
* [Variabelen wissen](#clear-variables)

### Variabelen instellen {#set-variables}

>[!IMPORTANT]
>
>U kunt het baken niet verzenden met de actie &quot;set variables&quot;. Als u het baken wilt verzenden, moet u de handeling &quot;verzendbaken&quot; selecteren.

U kunt tussen twee verschillende meningen in **Vastgestelde Variabelen** kiezen:

>[!BEGINTABS]

>[!TAB  verstrekken individuele attributen ]

In deze weergave kunt u verschillende variabelen opgeven, zoals `eVars` , `Props` , `Events` .

![&#x200B; de pagina van de de vormmening van Adobe Analytics, waar de extra attributen vermeld zijn.](../../../images/adobe_analytics_extension_form_view.png)

#### eVars

Plaats één of meerdere [&#x200B; Vars &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html?lang=nl-NL).

1. Selecteer een eVar in de vervolgkeuzelijst.
1. Geef op of u de eVar wilt instellen als de waarde (Instellen als) of een andere eVar wilt kopiëren (Dupliceren van).
1. Geef een waarde op voor Instellen als of selecteer de eVar die u wilt dupliceren.
1. (Optioneel) Selecteer eVar toevoegen om meer variabelen in te stellen.
1. Selecteer **[!UICONTROL Keep Changes]**.

#### Props

Plaats één of meerdere [&#x200B; eigenschappen &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=nl-NL).

1. Selecteer een eigenschap in het vervolgkeuzemenu.
1. Geef op of u de eigenschap wilt instellen als de waarde (Instellen als) of een andere eVar wilt kopiëren (Dupliceren van).
1. Geef een waarde op voor Instellen als of selecteer de eVar waaruit u de eigenschap wilt dupliceren.
1. (Optioneel) Selecteer **[!UICONTROL Add prop]** om meer eigenschappen in te stellen.
1. Selecteer **[!UICONTROL Keep Changes]**.

#### Gebeurtenissen

Plaats één of meerdere [&#x200B; gebeurtenissen &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/events-overview.html?lang=nl-NL).

1. Selecteer een gebeurtenis in de vervolgkeuzelijst.
1. (Facultatief) selecteer of specificeer een gegevenselement dat voor [&#x200B; wordt gebruikt gebeurtenisrangschikking &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/events/event-serialization.html?lang=nl-NL).
1. (Optioneel) Selecteer **[!UICONTROL Add event]** om meer gebeurtenissen in te stellen.
1. Selecteer **[!UICONTROL Keep Changes]**.

>[!TAB  JSON Mening ]

In deze mening, kunt u een versie JSON van de **Vastgestelde Variabelen** actie bekijken en uitgeven.

![&#x200B; mening die van A de huidige vastgestelde variabelenconfiguratie in formaat JSON in de uitbreiding van Adobe Analytics vertegenwoordigt.](../../../images/adobe_analytics_extension_json_view.png)

#### JSON

In de **Vastgestelde Veranderingen** actie, gebruik de mening JSON om JSON- gegevens te uploaden, te kopiëren of te downloaden en het op uw apparaat op te slaan.

Er bestaan echter wel enkele beperkingen:

* **de code van de Douane**: Als u douanecode gebruikt om variabelen te bevolken, zal het niet in de mening JSON verschijnen. In plaats daarvan wordt een waarschuwing weergegeven wanneer u de JSON bekijkt, kopieert of downloadt, met de melding dat wijzigingen die via aangepaste code zijn aangebracht, niet worden opgenomen.
* **Exemplaar van attribuut URL**: Het kopiëren van een waarde van een URL wordt niet gesteund in de mening JSON. Er wordt een waarschuwing weergegeven om deze beperking aan te geven.
* **Gearchiveerde variabelen**: Gearchiveerde of afgekeurde variabelen worden getoond in de mening JSON en een alarm wordt getoond informerend dat de gearchiveerde variabelen zijn geplaatst.
* **Elementen van Gegevens**: De elementen van gegevens worden vertegenwoordigd in de mening JSON. Als de JSON-gegevens naar een andere eigenschap Codes worden gekopieerd, worden de corresponderende gegevenselementen daar mogelijk niet gedefinieerd en worden deze niet correct omgezet wanneer ze worden uitgevoerd.

>[!ENDTABS]

#### Hiërarchie

Plaats de [&#x200B; Hiërarchie van de Analyse &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=nl-NL) variabele.

Geef elk niveau in de hiërarchie op.

Configureer desgewenst extra hiërarchieën.

#### Paginanaam

Deze waarde verwijst naar de naam van een bepaalde pagina en komt overeen met de [`pageName` variabele &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/pagename.html?lang=nl-NL) in Analytics.

>[!IMPORTANT]
>
>In Adobe Experience Manager-implementaties vertelt deze variabele AEM waar het opgehaalde analyserapport moet worden opgeslagen. Om ervoor te zorgen dat rapporten correct worden voortgeduurd, moet het koord van de paginanaam als dubbelepuntspad aan de plaats worden geformatteerd.
>
>Een webpagina bij `content/we-retail/language-masters/en/men.html` moet bijvoorbeeld de paginanaamwaarde `content:we-retail:language-masters:en:men` hebben.

#### Overige informatie

Geef andere informatie op die door de pagina&#39;s wordt gebruikt.

Deze instellingen zijn:

* Pagina-URL
* Server
* Kanaal
* Verwijzer
* Campaign
* Koop-id

  Een waarde of queryparameter opgeven

* Staat
* Postcode
* Transactie-id

U vindt deze instellingen in het menu &quot;Algemene variabelen&quot; door het selectievakje &quot;Extra instellingen&quot; te selecteren.

#### Aangepaste paginacode

**Beschrijving**

Gebruik de editor om uw aangepaste paginacode op te geven.

**Montages**

1. Selecteer **[!UICONTROL Open Editor]**.
1. Typ de aangepaste code.
1. Selecteer **[!UICONTROL Save]**.

### Bandbaken verzenden {#send-beacon}

#### Een pagina vergroten - s.t()

Selecteer deze optie als u een weergave wilt verhogen.

#### Een pagina niet vergroten - s.tl()

Schakel deze optie in als u de weergave niet wilt verhogen.

**Montages**

1. Selecteer een koppelingstype.

   U kunt een van de volgende opties selecteren:

   * Eigen koppeling
   * Koppeling downloaden
   * Koppeling afsluiten

1. Stel de parameter voor de geselecteerde koppeling in.
   * Eigen koppeling: geef de naam van de koppeling op.
   * Koppeling downloaden: geef een bestandsnaam op.
   * Koppeling afsluiten: geef de doel-URL op.
1. Selecteer **[!UICONTROL Keep Changes]**.

### Variabelen wissen {#clear-variables}

Er zijn geen configuratieopties als het handelingstype Variabelen wissen is geselecteerd.
