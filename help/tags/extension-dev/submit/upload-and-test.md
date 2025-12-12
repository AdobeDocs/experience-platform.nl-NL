---
title: End-to-end testen uploaden en implementeren voor een extensie
description: Leer hoe u uw extensie kunt valideren, uploaden en testen in Adobe Experience Platform.
exl-id: 6176a9e1-fa06-447e-a080-42a67826ed9e
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '2299'
ht-degree: 0%

---

# Test van begin tot eind uploaden en implementeren

Als u tagextensies wilt testen in Adobe Experience Platform, gebruikt u de API-tags en/of opdrachtregelprogramma&#39;s om de extensiepakketten te uploaden. Vervolgens gebruikt u de gebruikersinterface van Experience Platform of de gebruikersinterface voor gegevensverzameling om uw extensiepakket te installeren in een eigenschap en de mogelijkheden ervan uit te oefenen in een tagbibliotheek en te bouwen.

In dit document wordt beschreven hoe u end-to-end tests voor uw extensie kunt implementeren.

>[!NOTE]
>
>In deze handleiding wordt ervan uitgegaan dat u MacOS gebruikt terwijl Node.js en npm zijn geïnstalleerd en beschikbaar.

## Uw extensie valideren {#validate}

Zodra uw team met de prestaties van uw uitbreiding en de resultaten wordt tevredengesteld die zij in het [ Sandbox ](https://www.npmjs.com/package/@adobe/reactor-sandbox#running-the-sandbox) hulpmiddel zien, zou u bereid moeten zijn om uw uitbreidingspakket aan markeringen te uploaden.

Voordat u gaat uploaden, moet u controleren of de vereiste velden of instellingen aanwezig zijn. Bijvoorbeeld, die uw [ uitbreidingsmanifest ](../manifest.md) herzien, is uw [ uitbreidingsconfiguratie ](../configuration.md), uw [ meningen ](../web/views.md), en uw [ bibliotheekmodules ](../web/format.md) (bij een minimum) goede praktijk.

Een specifiek voorbeeld is uw logobestand: voeg een `"iconPath": "example.svg",` -regel toe aan uw `extension.json` -bestand en neem dat logoafbeeldingsbestand op in uw project. Dit is het relatieve pad naar het pictogram dat voor de extensie wordt weergegeven. Het mag niet beginnen met een schuine streep. Het moet verwijzen naar een SVG-bestand met een `.svg` -extensie. De SVG wordt normaal weergegeven wanneer deze vierkant wordt gerenderd en kan door de gebruikersinterface worden geschaald. Zie [ hoe te artikel van SVG ](https://css-tricks.com/scale-svg/) voor meer details schrapen.

>[!NOTE]
>
>Neem voor openbare extensies een item in de `extension.json` op met een koppeling naar de aanbieding op eBay Exchange. Uw [ uitbreidingsmanifest ](../manifest.md) zou een ingang als dit moeten omvatten: `"exchangeUrl":"https://www.adobeexchange.com/experiencecloud.details.12345.html"` die aan URL van uw lijst van de Uitwisseling richten.

## Een Adobe I/O-integratie maken {#integration}

Als u de API- of opdrachtregelprogramma&#39;s wilt gebruiken, hebt u een technisch account bij Adobe I/O nodig. U moet de technische account maken in de I/O-console en vervolgens het gereedschap Uploader gebruiken om het extensiepakket te uploaden.

Voor informatie bij het creëren van een technische rekening voor gebruik met markeringen in Adobe Experience Platform, gelieve te verwijzen naar [ Reactor API die ](../../api/getting-started.md) gids Aan de slag wordt.

>[!IMPORTANT]
>
>Als u een integratie wilt maken in Adobe I/O, moet u een Experience Cloud Organization Administrator of een Experience Cloud Org Developer zijn.

Als u geen integratie kunt tot stand brengen, is het waarschijnlijk dat u niet de correcte toestemmingen hebt. Hiervoor is een Org Admin nodig om de stappen voor u te voltooien of om u toe te wijzen als ontwikkelaar.

## Upload Uw extensiepakket {#upload}

Nu u geloofsbrieven hebt, bent u bereid om uw uitbreidingspakket van begin tot eind te testen.

Wanneer u het extensiepakket voor het eerst uploadt, wordt de status `development` weergegeven. Dit betekent dat het alleen zichtbaar is voor uw eigen organisatie en alleen met een eigenschap die is gemarkeerd voor extensieontwikkeling.

Gebruik de bevellijn om het volgende bevel binnen de folder in werking te stellen die uw .zip pakket bevat.

```bash
npx @adobe/reactor-uploader
```

Met `npx` kunt u een npm-pakket downloaden en uitvoeren zonder het daadwerkelijk op uw computer te installeren. Dit is de eenvoudigste manier om de Uploader uit te voeren.

>[!NOTE]
> Standaard verwacht de uploader Adobe I/O-referenties voor een server-naar-server Oauth-flow. De oudere `jwt-auth` gebruikersgegevens
> kan worden gebruikt door `npx @adobe/reactor-uploader@v5.2.0` tot aan afschrijving uit te voeren op 1 januari 2025. De vereiste parameters
> om de `jwt-auth` versie in werking te stellen kan [ hier ](https://github.com/adobe/reactor-uploader/tree/cdc27f4f0e9fa3136b8cd5ca8c7271428b842452) worden gevonden.

Voor uploader hoeft u slechts enkele gegevens in te voeren. De `clientId` en `clientSecret` kunnen worden opgehaald uit de Adobe I/O-console. Navigeer aan de [ pagina van Integraties ](https://console.adobe.io/integrations) in de I/O console. Selecteer de juiste organisatie in het vervolgkeuzemenu, zoek de juiste integratie en selecteer **[!UICONTROL View]** .

- Wat is uw `clientId`? Kopieer en plak deze vanuit de I/O-console.
- Wat is uw `clientSecret`? Kopieer en plak deze vanuit de I/O-console.
- Als u de uploader aanroept vanuit de map die het ZIP-pakket bevat, kunt u dit gewoon in de lijst selecteren in plaats van het pad te typen.

Uw extensiepakket wordt vervolgens geüpload en de uploader geeft u de id van het extension_package.

>[!NOTE]
>
>Tijdens het uploaden of patchen worden extensiepakketten in een status in behandeling geplaatst, terwijl het systeem het pakket asynchroon extraheert en implementeert. Tijdens dit proces kunt u de `extension_package` -id voor de status opvragen met de API en de interface. Er wordt een extensiekaart weergegeven in de catalogus die is gemarkeerd als In behandeling.

>[!NOTE]
>
>Als u de uploader vaak wilt uitvoeren, kan het lastig zijn al deze informatie telkens in te voeren. U kunt deze ook als argumenten doorgeven vanaf de opdrachtregel. Controle uit de [ sectie van de Argumenten van de Lijn van het Bevel ](https://www.npmjs.com/package/@adobe/reactor-uploader#command-line-arguments) van de NPM- documenten voor meer info.

Als u het uploaden van uw uitbreiding wilt beheren gebruikend direct API, zie de voorbeeldvraag [ creërend ](../../api/endpoints/extension-packages.md#create) of [ bijwerkt ](../../api/endpoints/extension-packages.md#update) een uitbreidingspakket in API docs voor meer detail.

## Een ontwikkeleigenschap maken {#property}

Nadat u zich hebt aangemeld bij de gebruikersinterface en **[!UICONTROL Tags]** hebt geselecteerd in de linkernavigatie, wordt het [!UICONTROL Properties] -scherm weergegeven. Een eigenschap is een container voor de tags die u wilt implementeren en kan op een of meerdere sites worden gebruikt.

![](../images/getting-started/properties-screen.png)

De eerste keer dat u zich aanmeldt, worden er geen eigenschappen op het scherm weergegeven. Selecteer **Nieuw Bezit** om te creëren. Voer een naam en een URL in. Gebruik de URL van uw testsite of de pagina waarop u de extensie gaat testen. Dit domeinveld kan door sommige extensies worden gebruikt of door een voorwaarde met de extensie Core.

>[!NOTE]
>
>`localhost` werkt niet als een URL-waarde. Gebruik in plaats daarvan een willekeurige modelwaarde voor het testen als u een `localhost` URL gebruikt. Bijvoorbeeld example.com.

Om dit bezit voor het testen van de uitbreidingsontwikkeling te gebruiken, moet u **GEAVANCEERDE OPTIONS** uitbreiden en ervoor zorgen om de doos voor **te controleren voor uitbreidingsontwikkeling** vormen.

![](../images/getting-started/launch-create-a-dev-property.png)

Selecteer **sparen** bij de bodem om uw nieuw bezit te bewaren.

Het scherm Eigenschappen wordt weergegeven. Selecteer de naam van de eigenschap die u zojuist hebt gemaakt. Het scherm van het Overzicht van het Bezit verschijnt. Het voorziet verbindingen met elk gebied van het systeem van de globale navigatiekoppelingen in de kolom op de linkerzijde.

## De extensie installeren {#install-extension}

Om uw uitbreiding in dit bezit te installeren, selecteer de **verbinding van Uitbreidingen** in de belangrijkste navigatiekoppelingen in de linkerkolom. De **uitbreiding van de Kern** wordt getoond op het **Geïnstalleerde** scherm. De extensie Core bevat alle functionaliteit voor tagbeheer binnen de gegevensverzameling.

![](../images/getting-started/extensions.png)

Om uw uitbreiding toe te voegen, selecteer de **Catalogus** tabel.

![](../images/getting-started/catalog.png)

In de catalogus worden kaartpictogrammen weergegeven voor elke beschikbare extensie. Als uw extensie niet wordt weergegeven in de catalogus, controleert u of u de bovenstaande stappen hebt uitgevoerd in de secties Adobe Administration Console Set Up and Creating Your Extension Package. Uw extensiepakket wordt mogelijk ook weergegeven als In behandeling als Experience Platform de eerste verwerking niet heeft voltooid.

Als u de vorige stappen hebt uitgevoerd en nog steeds geen extensiepakket in behandeling of Mislukt ziet in de catalogus, moet u de status van het extensiepakket rechtstreeks controleren met de API. Voor informatie over hoe te om de aangewezen API vraag te maken, lees [ Vets een ExtensionPackage ](../../api/endpoints/extension-packages.md#lookup) in de API documentatie.

Nadat uw extensiepakket verwerking heeft gebeëindigd, selecteert u **Installeren** onder aan de kaart.

![](../images/getting-started/install-extension.png)

Het configuratiescherm wordt geopend (op voorwaarde dat de extensie er een heeft). Voeg om het even welke informatie nodig toe om uw uitbreiding te vormen en **te selecteren sparen** bij de bodem. In het voorbeeld van het configuratiescherm dat u hier ziet, wordt de Facebook-extensie gebruikt waarvoor een Pixel-id is vereist.

![](../images/getting-started/fb-extension.png)

U zou nu het **Geïnstalleerde** uitbreidingsscherm met de uitbreiding van de Kern en uw uitbreiding moeten zien.

![](../images/getting-started/extension-installed.png)

## Bronnen maken om uw extensie te testen {#resources}

Extensies bieden nieuwe mogelijkheden voor gebruikers van Adobe Experience Platform. Deze worden typisch getoond in de Elementen van Gegevens of de Bouwer van de Regel.

### Gegevenselementen

Het doel van elementen met taggegevens is om gebruikers te helpen bij het behouden van waarden. Elk gegevenselement is een toewijzing of aanwijzer aan brongegevens. Eén gegevenselement is een variabele die kan worden toegewezen aan querytekenreeksen, URL&#39;s, cookie-waarden, JavaScript-variabelen, enzovoort. Selecteer **Elementen van Gegevens** van de linkernavigatiebar, en **creeer Nieuw Element van Gegevens**.

![](../images/getting-started/data-element-create-new-link.png)

Extensies kunnen gegevenselementen definiëren als dat nodig is om de extensie te laten werken of eenvoudig als gebruiksvriendelijk voor gebruikers. Wanneer een uitbreiding gegevenselemetypes verstrekt, verschijnen zij in een vervolgkeuzelijst voor gebruikers op **het Create scherm van het Element van Gegevens**:

![](../images/getting-started/create-data-element.png)

Wanneer een gebruiker uw uitbreiding van **Uitbreiding** dropdown selecteert, wordt het **Type van Element van Gegevens** dropdown bevolkt met om het even welke die types van gegevenselement door uw uitbreiding worden verstrekt. De gebruiker kan dan elk gegevenselement aan zijn bronwaarde in kaart brengen. De elementen van gegevens kunnen dan worden gebruikt wanneer het bouwen van regels in de Gebeurtenis van de Verandering van het Element van Gegevens of de Gebeurtenis van de Code van de Douane om een uit te voeren regel teweeg te brengen. Een gegevenselement kan ook in de Voorwaarde van het Element van Gegevens of andere Voorwaarden, Uitzonderingen, of Acties in een regel worden gebruikt.

Zodra het gegevenselement wordt gecreeerd (de afbeelding wordt opstelling), kunnen de gebruikers de brongegevens door het gegevenselement eenvoudig van verwijzingen te voorzien van verwijzingen voorzien. Als de bron van de waarde ooit verandert (site-herontwerpen, enz.) hoeven gebruikers de toewijzing slechts eenmaal bij te werken in de gebruikersinterface en ontvangen alle gegevenselementen automatisch de nieuwe bronwaarde.

### Regels

Selecteer de **verbinding van Regels** in de linkernavigatie, dan **creeer Nieuwe Regel**.

![](../images/getting-started/rules-link.png)

Voer eerst een beschrijvende naam in als regel. **creeer het scherm van de Regel** is opstelling als een `if-then` verklaring.

![](../images/getting-started/create-new-rule.png)

Als een gebeurtenis plaatsvindt en de voorwaarden worden doorgegeven en er zijn geen uitzonderingen, wordt de actie geactiveerd. Deze zelfde stroom bestaat in uitbreidingen waar u gebeurtenissen, voorwaarden, uitzonderingen, gegevenselementen, of acties kunt tot stand brengen of hefboomwerking.

Voeg met het voorbeeld van de Facebook-extensie een gebeurtenis toe telkens wanneer een pagina op de testsite wordt geladen.

![](../images/getting-started/load-event.png)

Het `Window Loaded` **Type van Gebeurtenis** zorgt ervoor dat om het even welke tijd een pagina op de testplaats laadt deze regel zal worden teweeggebracht. Selecteer **houden Veranderingen**. Voor dit voorbeeld, negeer **Voorwaarden** aangezien de regel voor om het even welke pagina op de testplaats zou moeten worden teweeggebracht.

Onder **ACTIES** uitgezocht **voeg** toe. Het **scherm van de Configuratie van de Actie** verschijnt.Daarna moet u de uitbreiding kiezen dat de regel moet worden toegepast op, en de actie om voor te komen wanneer de regel wordt teweeggebracht. Selecteer **het Pixel van Facebook** van de **3} dropdown lijst van de Uitbreiding {, en** verzend de Mening van de Pagina **van het** Type van Actie **dropdown lijst.** Selecteer **houden Veranderingen**, en dan **sparen** op het volgende **uitgeven het scherm van de Regel**.

![](../images/getting-started/action-configuration.png)

Selecteer tijdens het testen van de extensie relevante gebeurtenissen, voorwaarden, enzovoort. die door uw extensie worden geleverd, in een willekeurig aantal regels.

## Uw wijzigingen publiceren {#publish}

In de belangrijkste navigatie, uitgezochte **het Publiceren**, dan op **voeg Nieuwe Bibliotheek** verbinding toe:

![](../images/getting-started/add-new-library.png)

Een bibliotheek is een set instructies voor hoe extensies, gegevenselementen en regels met elkaar en met een website communiceren. Bibliotheken worden gecompileerd in builds. Een bibliotheek kan net zoveel wijzigingen bevatten als een gebruiker op een gemakkelijke manier tegelijk kan maken of testen.

Op **creeer Bibliotheek** scherm, voeg een naam op het **3} tekstgebied van de Naam {toe.** De markeringen verstrekken een standaardontwikkelomgeving genoemd **Ontwikkeling**. Selecteer **Ontwikkeling** van de **milieu** dropdown lijst. Voeg voor het gemak alle beschikbare bronnen toe. Selecteer **toevoegen Alle Gewijzigde Middelen**, dan uitgezocht **sparen**.

>[!NOTE]
>
>Wanneer u een bron aan een bibliotheek toevoegt, wordt een momentopname van die bron op dat exacte moment genomen en aan de bibliotheek toegevoegd. Wanneer u later wijzigingen aanbrengt in uw bronnen (bijvoorbeeld als gevolg van correcties die u moet aanbrengen), moet u de bibliotheek ook bijwerken met de nieuwste wijzigingen in uw bronnen. **voeg Alle Gewijzigde Middelen** knoop toe is nuttig ook voor dit doel.

![](../images/getting-started/create-new-library.png)

Nu alle veranderingen in de pas gecreëerde bibliotheek (genoemd **dev** in het verstrekte voorbeeld) inbegrepen zijn, uitgezocht **sparen en bouwt aan Ontwikkeling**.

![](../images/getting-started/build-for-dev.png)

Nadat het bouwstijlproces voltooit, een groene **succes** indicatorvertoningen naast de bibliotheeknaam.

![](../images/getting-started/successful-build.png)

De tagbibliotheek is nu gepubliceerd en beschikbaar voor gebruik. De testpagina moet de nieuwe bibliotheek gebruiken om het paginagedrag voor de eindgebruiker in browser te testen.

## Tags op een testsite installeren {#install-data-collection-tags}

Installatie-instructies zijn beschikbaar op het tabblad Omgevingen. Op deze pagina worden alle beschikbare omgevingen weergegeven en kunt u meer maken. Aangezien de bibliotheek aan het milieu van de Ontwikkeling werd gepubliceerd selecteer het bakpictogram in de **INSTALLEER** kolom op de **3} rij van de Ontwikkeling.**

![](../images/getting-started/launch-installation-instructions.png)

Het **Web installeert de dialoog van Instructies** voor het milieu van de Ontwikkeling verschijnt. Selecteer het kopieerpictogram om de volledige `<script>` -tag te kopiëren.

![](../images/getting-started/launch-installation-instructions-dialogue.png)

Voltooi de installatie door deze enkele `<script>` -tag in de `<head>` -sectie van uw document- of sitesjabloon te plaatsen. Ga vervolgens naar de testsite om het gedrag van uw gepubliceerde tagbibliotheek te bekijken.

## Testen {#test}

Hieronder volgt een lijst met handige consoleopdrachten voor het valideren van uw extensie op uw testpagina of site.

- In `_satellite.setDebug(true);` worden de foutopsporingsmodus ingeschakeld en worden nuttige logboekinstructies naar de console uitgevoerd.
- Het `_satellite._container` -object bevat nuttige informatie over de geïmplementeerde bibliotheek, waaronder informatie over de opgenomen build, gegevenselementen, regels en extensies.

Het doel van deze test is de functionaliteit van de geïmplementeerde bibliotheek te controleren en ervoor te zorgen dat het extensiepakket zich gedraagt zoals u had verwacht nadat het in een bibliotheek is opgenomen.

Wanneer u veranderingen ontdekt die aan uw uitbreidingspakket moeten worden aangebracht, is het herhalingsproces gelijkaardig aan het ontwikkelingsproces.

1. Breng wijzigingen aan in de code in uw project.
1. Valideer de wijzigingen met het gereedschap Sandbox.
1. Gebruik het gereedschap Packager om een nieuw ZIP-pakket te maken
1. Gebruik het gereedschap Uploader om het nieuwe ZIP-pakket te uploaden. Het proces volgt dezelfde instructies als voor de eerste upload. Aangezien er in de ontwikkelingsmodus al een extensiepakket met die naam bestaat, wordt de oudere versie door dit nieuwe pakket overschreven in plaats van een nieuwe versie te maken.

   >[!NOTE]
   >
   >Argumenten kunnen op de bevellijn worden overgegaan om tijd te besparen door het herhaalde ingaan van geloofsbrieven te vermijden. Voor meer informatie over dit, lees de [ reactor-uploader documentatie ](https://www.npmjs.com/package/@adobe/reactor-uploader).
1. De installatiestap kan worden overgeslagen wanneer een bestaand pakket wordt bijgewerkt.
1. Wijzig middelen - als de configuratie voor om het even welk van uw uitbreidingscomponenten is veranderd, zult u die middelen in UI moeten bijwerken.
1. Voeg de meest recente wijzigingen toe aan uw bibliotheek en maak de bibliotheek opnieuw.
1. Voltooi nog een testronde.
