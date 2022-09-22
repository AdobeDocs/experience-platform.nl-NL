---
title: Gegevenselementen
description: De elementen van gegevens zijn de bouwstenen voor uw gegevenswoordenboek (of gegevenskaart). Gebruik gegevenselementen om gegevens te verzamelen, te organiseren en te leveren over marketing- en advertentietechnologie.
exl-id: 1e7b03cc-5a54-403d-bf8d-dbc206cfeb2d
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1610'
ht-degree: 1%

---

# Gegevenselementen

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

De elementen van gegevens zijn de bouwstenen voor uw gegevenswoordenboek (of gegevenskaart). Gebruik gegevenselementen om gegevens te verzamelen, te organiseren en te leveren over marketing- en advertentietechnologie.

Eén gegevenselement is een variabele waarvan de waarde kan worden toegewezen aan querytekenreeksen, URL&#39;s, cookie-waarden, JavaScript-variabelen enzovoort. U kunt in Adobe Experience Platform naar deze waarde verwijzen met de variabelenaam. Deze verzameling gegevenselementen wordt het woordenboek met gedefinieerde gegevens dat u kunt gebruiken om uw regels (gebeurtenissen, voorwaarden en handelingen) samen te stellen. Dit gegevenswoordenboek wordt over tags gedeeld voor gebruik met extensies die u aan de eigenschap hebt toegevoegd.

>[!IMPORTANT]
>
>Wijzigingen worden pas van kracht nadat ze [gepubliceerd](../publishing/overview.md).

Gebruik gegevenselementen zo breed mogelijk tijdens het maken van regels om de definitie van dynamische gegevens te consolideren en de efficiëntie van het coderingsproces te verbeteren. U definieert de gegevensregels eenmaal en gebruikt deze vervolgens op meerdere plaatsen.

Het concept van herbruikbare gegevenselementen is zeer krachtig en u zou hen als beste praktijken moeten gebruiken.

Bijvoorbeeld als er een bepaalde manier is dat u paginanamen of product IDs van verwijzingen voorziet of informatie van de parameters van het vraagkoord van een verwante marketing verbinding of van [!DNL AdWords]enzovoort, kunt u een gegevenswoordenboek (gegevenselementen) maken door informatie van de bron op te halen en deze gegevens vervolgens in verschillende labelregels te gebruiken.

Gebruikend paginanaam als voorbeeld, veronderstel u een bepaald pagina-naam schema door een gegevenslaag van verwijzingen te voorzien, `document.title` -element of een titeltag binnen de website. Met tags in Adobe Experience Platform kunt u een gegevenselement maken als een enkel referentiepunt voor dat specifieke punt van gegevens. U kunt dit gegevenselement dan gebruiken in om het even welke regel die de paginanaam moet van verwijzingen voorzien. Als u om een of andere reden in de toekomst besluit om de manier te wijzigen waarop u naar de paginanaam verwijst (bijvoorbeeld `document.title` maar u wilt nu naar een bepaalde gegevenslaag verwijzen), te hoeven u niet vele verschillende regels uit te geven om die verwijzing te veranderen. U wijzigt eenvoudig de verwijzing eenmaal in het gegevenselement en alle regels die naar dat gegevenselement verwijzen, worden automatisch bijgewerkt.

>[!NOTE]
>
>Als in een regel niet naar een gegevenselement wordt verwezen, wordt het niet op een pagina geladen, tenzij het specifiek wordt aangeroepen in een aangepast script

De elementen van gegevens worden bevolkt met gegevens wanneer zij in regels worden gebruikt of wanneer manueel geroepen in een manuscript. Op een hoog niveau kunt u:

1. [Een gegevenselement maken](#create-a-data-element), als je dat nog niet hebt gedaan.
1. Het gegevenselement in een [regel](./rules.md) of een aangepast script.

## Gebruik van gegevenselementen

### In regels

U kunt gegevenselementen in de regel het uitgeven interface gebruiken door het onderzoeksvakje te gebruiken om de naam van uw gegevenselement te vinden.

### In aangepast script

U kunt gegevenselementen in douanescripts gebruiken door `_satellite` objectsyntaxis:

`_satellite.getVar('data element name');`

## Een data-element maken {#create-a-data-element}

De elementen van gegevens zijn de bouwstenen voor regels. Met gegevenselementen kunt u een gegevenswoordenboek (of gegevenskaart) maken van veelgebruikte items op een pagina, ongeacht de oorsprong ervan (queryreeksen, URL&#39;s of cookiewaarden) voor elk object dat zich op uw site bevindt.

1. Open vanuit een eigenschappenpagina de [!UICONTROL Data Elements] tab, dan selecteren **[!UICONTROL Create New Data Element]**.
1. Geef het gegevenselement een naam.
1. Selecteer een extensie en typ deze.

   De beschikbare elementtypen worden bepaald door de extensie. Voor informatie over de typen die beschikbaar zijn met de extensie Core raadpleegt u [Typen gegevenselementen](data-elements.md#types-of-data-elements).

1. Geef alle gevraagde informatie over het gekozen type op in de opgegeven velden.
1. (Optioneel) Voer een standaardwaarde in.

   Als u deze optie niet selecteert, is er geen standaardwaarde.  De meeste gebruikers verlaten dit in zijn standaardstaat.  Verschillende systemen behandelen een lege variabele anders.  Sommige mensen kiezen ervoor om iets in te voeren zoals &quot;geen&quot; of &quot;n.v.t.&quot;, zodat ze consistentie kunnen creëren in de rapportage wanneer het gegevenselement geen waarde retourneert.

1. Selecteer of u een waarde in kleine letters wilt afdwingen en of u regeleinden en spaties wilt verwijderen.
1. Selecteer een duur.

   De beschikbare opties zijn:

   * Geen
      * De waarde wordt niet opgeslagen.
   * Paginaweergave
      * De waarde wordt vastgehouden in een JavaScript-variabele totdat de pagina wordt vernieuwd of een nieuwe pagina wordt geladen.
      * Kan in scripts worden gemaakt en ingesteld met `_satellite` objectsyntaxis:

         `_satellite.setVar('data_element_name')`
   * Sessie
      * De waarden blijven aanwezig in de sessieopslag van de browser totdat het browsertabblad wordt gesloten.
      * Beschikbaar tijdens het hele bezoek ter plaatse.
   * Bezoeker
      * De waarde wordt voor onbepaalde tijd opgeslagen in de lokale opslag van de browser.

1. Selecteer **[!UICONTROL Save]**.

Wanneer u elementen maakt of bewerkt, kunt u deze opslaan en samenstellen op uw [actieve bibliotheek](../publishing/libraries.md#active-library). Hiermee slaat u de wijziging onmiddellijk op in uw bibliotheek en wordt een build uitgevoerd. De status van de build wordt weergegeven. U kunt ook een nieuwe bibliotheek maken op basis van de [!UICONTROL Active Library] vervolgkeuzelijst.

## Typen gegevenselementen {#types-of-data-elements}

Gegevenselementen worden bepaald door de extensie. Er is geen limiet aan de typen die kunnen worden gemaakt.

De volgende secties beschrijven de types van gegevenselementen beschikbaar in de uitbreiding van de Kern. Andere extensies gebruiken andere typen gegevenselementen.

### Cookie

In het veld cookie naam kan naar een beschikbaar domeincookie worden verwezen.

#### Voorbeeld:

`cookieName`

### Aangepaste code

U kunt aangepaste JavaScript invoeren in de gebruikersinterface door  [!UICONTROL Open Editor] en code invoegen in het editorvenster.

Een terugkeerverklaring is noodzakelijk in het redacteursvenster om erop te wijzen welke waarde als waarde van het gegevenselement zou moeten worden geplaatst. Als er geen instructie return is opgenomen, wordt het gegevenselement omgezet in `undefined`.  Hierdoor wordt de fallback geactiveerd om te zoeken naar een opgeslagen waarde en vervolgens naar een standaardwaarde als er geen opgeslagen waarde aanwezig is.

**Voorbeeld:**

```text
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

Aangepaste code kan het volgende accepteren `event` object van de aanroepende regel als een argument. Hierdoor kan de code daar waarde lezen.

**Voorbeeld:**

```text
// `event` is the default object provided by the rule
var eventType = event.$type;
return eventType; // if this data element is called from a "DOM Ready" event, then `core.dom-ready` is returned
```

U kunt dit vervolgens gebruiken in aangepaste scripts met de opdracht `_satellite` objectsyntaxis:

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

Als u percentage (`%`), hoeft u alleen de naam van het gegevenselement op te geven. U hoeft niet op te geven `event`.

```text
%data element name%
```

### DOM-kenmerk

Elke elementwaarde kan worden opgehaald, zoals een div- of H1-tag.

#### Voorbeeld:

CSS-selectieketen:

`id#dc logo img`

Hiermee wordt de waarde opgehaald van:

`src`

### JavaScript-variabele

Met behulp van het padveld kan naar elk beschikbaar JavaScript-object of -variabele worden verwezen.

Als u JavaScript-variabelen of objecteigenschappen in uw opmaak wilt verzamelen en deze wilt gebruiken met een van uw extensies of regels, kunnen gegevenselementen worden gebruikt om deze waarden vast te leggen. Deze manier, kunt u naar het gegevenselement door uw regels verwijzen, en als de bron van de gegevens ooit verandert, moet u slechts uw verwijzing naar de bron (het gegevenselement) in één plaats binnen UI van de Inzameling van Gegevens veranderen.

Stel dat uw markering een JavaScript-variabele bevat met de naam `Page_Name`, als volgt:

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

U moet het pad naar die variabele opgeven wanneer u het gegevenselement maakt.

Als u een gegevensverzamelingsobject gebruikt als onderdeel van uw gegevenslaag, gebruikt u gewoon puntnotatie in het pad om te verwijzen naar het object en de eigenschap die u in het gegevenselement wilt vastleggen, zoals `_myData.pageName`, of `digitalData.pageName`, enz.

#### Voorbeeld:

`window.document.title`

### Lokale opslag

Geef de naam op van het lokale opslagitem in het dialoogvenster [!UICONTROL Local Storage Item Name] veld.

Met lokale opslag kunnen browsers gegevens van pagina tot pagina opslaan ([https://www.w3schools.com/html/html5\_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp)). Lokale opslag werkt veel zoals cookies, maar is veel groter en flexibeler.

Gebruik het opgegeven veld om de waarde op te geven die u voor een lokaal opslagitem hebt gemaakt, zoals `lastProductViewed.`

### Pagina-info

Gebruik deze gegevenspunten om paginainfo voor gebruik in uw regellogica te vangen of informatie te verzenden naar [!DNL Analytics] of externe volgsystemen.

U kunt een van de volgende paginakenmerken selecteren voor gebruik in het gegevenselement:

* URL
* Hostnaam
* Pathname
* Protocol
* Referrer
* Titel

### Tekenreeksparameter van query

Geef één URL-parameter op in het dialoogvenster [!UICONTROL URL Parameter] veld.

Alleen de naamsectie is nodig en speciale aanduidingen zoals &quot;?&quot; of &quot;=&quot; moet worden weggelaten

#### Voorbeeld:

`contentType`

### Willekeurig getal

Gebruik dit gegevenselement om een willekeurig getal te genereren. Deze wordt vaak gebruikt voor het nemen van monsters van gegevens of het maken van id&#39;s, zoals een Actief-id. Het willekeurige getal kan ook worden gebruikt om vertrouwelijke of salt-gevoelige gegevens te verkrijgen. Voorbeelden hiervan zijn:

* Een hoogte-id genereren
* Plaats het nummer in een gebruikerstoken of tijdstempel om ervoor te zorgen dat het uniek is
* Voer een unidirectionele knoeiboel op PII gegevens uit
* Willekeurig beslissen wanneer een enquêteverzoek op de plaats moet tonen

Geef de minimum- en maximumwaarden voor het willekeurige getal op.

**Standaardwaarden:**

Minimaal: 0

Maximaal: 1000000000

### Sessieopslag

Geef de naam op van het opslagitem voor de sessie in het dialoogvenster [!UICONTROL Session Storage Item Name] veld.

Sessieopslag is vergelijkbaar met lokale opslag, behalve dat de gegevens worden verwijderd nadat de sessie is beëindigd, terwijl lokale opslag of een cookie de gegevens kan behouden.

### Bezoekergedrag

Net als Pagina-info gebruikt dit gegevenselement gangbare gedragstypen om logica binnen regels of andere oplossingen voor Platforms te verrijken.

Selecteer een van de volgende kenmerken voor bezoekersgedrag:

* Landingspagina
* Verkeersbron
* Minuten op site
* Aantal sessies
* Aantal sessiepagina&#39;s
* Aantal LiveTime-paginaweergaven
* Is nieuwe bezoeker

Enkele gangbare gebruiksgevallen zijn:

* Een enquête weergeven nadat een bezoeker vijf minuten op de site is geweest
* Als dit de openingspagina voor het bezoek is, vult u een [!DNL Analytics] metrisch
* Nieuwe aanbieding weergeven aan bezoeker na X-aantal aantal aantal sessies
* Een nieuwsbrief weergeven als dit een nieuwe bezoeker is

## Ingebouwde gegevenselementen

U moet een aangepast gegevenselement maken in de gebruikersinterface voor gegevensverzameling als u eerder een van de volgende gegevenselementen hebt gebruikt:

* URI
* Protocol
* Hostnaam
