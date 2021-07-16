---
title: End-to-end testen uploaden en implementeren voor een extensie
description: Leer hoe u uw extensie kunt valideren, uploaden en testen in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '2390'
ht-degree: 0%

---

# Test van begin tot eind uploaden en implementeren

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Als u de extensies van tags in Adobe Experience Platform wilt testen, gebruikt u de API-tags en/of opdrachtregelprogramma&#39;s om de extensiepakketten te uploaden. Vervolgens gebruikt u de UI voor gegevensverzameling om het extensiepakket te installeren op een eigenschap en de mogelijkheden ervan uit te oefenen in een tagbibliotheek en te bouwen.

In dit document wordt beschreven hoe u end-to-end tests voor uw extensie kunt implementeren.

>[!NOTE]
>
>In deze handleiding wordt ervan uitgegaan dat u Mac OS gebruikt terwijl Node.js en npm zijn geïnstalleerd en beschikbaar.

## Uw extensie valideren {#validate}

Als uw team tevreden is met de prestaties van uw extensie en de resultaten die ze zien in het gereedschap [Sandbox](https://www.npmjs.com/package/@adobe/reactor-sandbox#running-the-sandbox), moet u klaar zijn om uw extensiepakket te uploaden naar tags.

Voordat u gaat uploaden, moet u controleren of de vereiste velden of instellingen aanwezig zijn. Bijvoorbeeld, die uw [uitbreidingsmanifest](../manifest.md), uw [uitbreidingsconfiguratie](../configuration.md), uw [views](../web/views.md), en uw [bibliotheekmodules](../web/format.md) (bij een minimum) herzien is goede praktijk.

Een specifiek voorbeeld hiervan is uw logobestand: Voeg een `"iconPath": "example.svg",` lijn aan uw `extension.json` dossier toe en neem dat dossier van het logobeeld in uw project op. Dit is het relatieve pad naar het pictogram dat voor de extensie wordt weergegeven. Het mag niet beginnen met een schuine streep. Er moet worden verwezen naar een SVG-bestand met de extensie `.svg`. De SVG moet normaal worden weergegeven wanneer deze vierkant wordt gerenderd en kan door de gebruikersinterface worden geschaald. Zie [SVG-artikel schalen](https://css-tricks.com/scale-svg/) voor meer informatie.

>[!NOTE]
>
>Neem voor openbare extensies een item op in uw `extension.json` met een koppeling naar uw Exchange-aanbieding. Uw [extensiemanifest](../manifest.md) zou een ingang als deze moeten omvatten: `"exchangeUrl":"https://www.adobeexchange.com/experiencecloud.details.12345.html"` verwijzen naar de URL van je Exchange-aanbieding.

## Een Adobe I/O-integratie maken {#integration}

Als u de API- of opdrachtregelprogramma&#39;s wilt gebruiken, hebt u een technisch account met Adobe I/O nodig. U moet de technische account maken in de I/O-console en vervolgens het gereedschap Uploader gebruiken om het extensiepakket te uploaden.

Raadpleeg de handleiding [Access Tokens](https://developer.adobelaunch.com/api/guides/access_tokens/) voor informatie over het maken van een technisch account voor gebruik met tags in Adobe Experience Platform.

>[!IMPORTANT]
>
>Om tot een Integratie in Adobe I/O te leiden moet u een Beheerder van de Organisatie van de Experience Cloud of een Experience Cloud zijn Org Ontwikkelaar.

Als u geen Integratie kunt tot stand brengen, is het waarschijnlijk dat u niet de correcte toestemmingen hebt. Hiervoor is een Org Admin nodig om de stappen voor u te voltooien of om u toe te wijzen als ontwikkelaar.

## Upload Your extension package {#upload}

Nu u geloofsbrieven hebt, bent u bereid om uw uitbreidingspakket van begin tot eind te testen.

Wanneer u uw extensiepakket voor het eerst uploadt, wordt de status `development` weergegeven. Dit betekent dat het alleen zichtbaar is voor uw eigen organisatie en alleen met een eigenschap die is gemarkeerd voor extensieontwikkeling.

Gebruik de bevellijn om het volgende bevel binnen de folder in werking te stellen die uw .zip pakket bevat.

```bash
npx @adobe/reactor-uploader
```

`npx` kunt u een npm-pakket downloaden en uitvoeren zonder het daadwerkelijk op uw computer te installeren. Dit is de eenvoudigste manier om de Uploader uit te voeren.

Voor Uploader moet u verschillende gegevens invoeren. De technische account-id, de API-sleutel en andere gegevens kunnen worden opgehaald van de Adobe I/O-console. Navigeer naar de [pagina Integraties](https://console.adobe.io/integrations) in de I/O-console. Selecteer de juiste organisatie in het vervolgkeuzemenu, zoek de juiste integratie en selecteer **[!UICONTROL View]**.

- Wat is het pad naar uw persoonlijke sleutel? /path/to/private.key. Dit is de plaats u uw privé sleutel in stap 2 hierboven bewaarde.
- Wat is je Org ID? Kopieer en plak deze vanuit de overzichtspagina van de I/O-console die u eerder hebt geopend.
- Wat is je technische account-id? Kopieer en plak deze vanuit de I/O-console.
- Wat is uw API-sleutel? Kopieer en plak deze vanuit de I/O-console.
- Wat is het clientgeheim? Kopieer en plak deze vanuit de I/O-console.
- Wat is het pad naar het extension_package dat u wilt uploaden? /path/to/extension_package.zip. Als u de uploader aanroept vanuit de map die het ZIP-pakket bevat, kunt u dit gewoon in de lijst selecteren in plaats van het pad te typen.

Uw extensiepakket wordt vervolgens geüpload en de uploader geeft u de id van het extension_package.

>[!NOTE]
>
>Tijdens het uploaden of patchen worden extensiepakketten in een status in behandeling geplaatst, terwijl het systeem het pakket asynchroon extraheert en implementeert. Tijdens dit proces kunt u de `extension_package`-id voor de status opvragen met de API en de gebruikersinterface voor gegevensverzameling. Er wordt een extensiekaart weergegeven in de catalogus die is gemarkeerd als In behandeling.

>[!NOTE]
>
>Als u de uploader vaak wilt uitvoeren, kan het lastig zijn al deze informatie telkens in te voeren. U kunt deze ook als argumenten doorgeven vanaf de opdrachtregel. Raadpleeg de sectie [Opdrachtregelargumenten](https://www.npmjs.com/package/@adobe/reactor-uploader#command-line-arguments) van de NPM-documenten voor meer informatie.

## Een ontwikkeleigenschap maken {#property}

Nadat u zich in UI van de Inzameling van Gegevens ondertekent, wordt het scherm van Eigenschappen getoond. Een eigenschap is een container voor de tags die u wilt implementeren en kan op een of meerdere sites worden gebruikt.

![](../images/getting-started/properties-screen.png)

De eerste keer dat u zich aanmeldt, worden er geen eigenschappen op het scherm weergegeven. Selecteer **Nieuwe eigenschap** om een eigenschap te maken. Voer een naam en een URL in. Gebruik de URL van uw testsite of de pagina waarop u de extensie gaat testen. Dit domeinveld kan door sommige extensies worden gebruikt of door een voorwaarde met de extensie Core.

>[!NOTE]
>
>`localhost` werkt niet als een URL-waarde. Gebruik in plaats daarvan een willekeurige modelwaarde voor het testen als u een `localhost` URL gebruikt. Bijvoorbeeld, example.com.

Als u deze eigenschap wilt gebruiken voor het testen van extensieontwikkeling, moet u **ADVANCED-OPTIONS** uitbreiden en het selectievakje **Configureren voor extensieontwikkeling** inschakelen.

![](../images/getting-started/launch-create-a-dev-property.png)

Selecteer **Opslaan** onder aan om de nieuwe eigenschap op te slaan.

Het scherm Eigenschappen wordt weergegeven. Selecteer de naam van de eigenschap die u zojuist hebt gemaakt. Het scherm van het Overzicht van het Bezit verschijnt. Het voorziet verbindingen met elk gebied van het systeem van de globale navigatiekoppelingen in de kolom op de linkerzijde.

## De extensie installeren {#install-extension}

Als u de extensie in deze eigenschap wilt installeren, selecteert u de koppeling **Extensions** in de belangrijkste navigatiekoppelingen in de linkerkolom. De **Core** extensie wordt weergegeven op het **Geïnstalleerde** scherm. De extensie Core bevat alle functionaliteit voor tagbeheer binnen de gegevensverzameling.

![](../images/getting-started/extensions.png)

Als u de extensie wilt toevoegen, selecteert u het tabblad **Catalogus**.

![](../images/getting-started/catalog.png)

De catalogus bevat kaartpictogrammen voor elke beschikbare extensie. Als uw extensie niet wordt weergegeven in de catalogus, controleert u of u de bovenstaande stappen hebt uitgevoerd in de secties Stel Adobe beheerconsole in en Creating Your Extension Package. Uw extensiepakket wordt mogelijk ook weergegeven als In behandeling als het Platform de eerste verwerking niet heeft voltooid.

Als u de vorige stappen hebt gevolgd en nog steeds geen extensiepakket in behandeling of Mislukt ziet in de catalogus, moet u de status van het extensiepakket rechtstreeks controleren met de API. Voor informatie over hoe te om de aangewezen API vraag te maken, lees [Fetch een ExtensionPackage](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/fetch/) in de API documentatie.

Nadat uw extensiepakket klaar is met verwerken, selecteert u **Installeren** onder aan de kaart.

![](../images/getting-started/install-extension.png)

Het configuratiescherm wordt geopend (op voorwaarde dat de extensie er een heeft). Voeg alle informatie toe die nodig is om uw extensie te configureren en selecteer **Opslaan** onderaan. In het voorbeeld van het configuratiescherm dat u hier ziet, wordt de Facebook-extensie gebruikt waarvoor een Pixel-id is vereist.

![](../images/getting-started/fb-extension.png)

U moet nu het **Geïnstalleerde** uitbreidingsscherm met de uitbreiding van de Kern en uw uitbreiding zien.

![](../images/getting-started/extension-installed.png)

## Bronnen maken om uw extensie te testen {#resources}

Extensies bieden nieuwe mogelijkheden voor gebruikers van Adobe Experience Platform. Deze worden typisch getoond in de Elementen van Gegevens of de Bouwer van de Regel.

### Gegevenselementen

Het doel van elementen met taggegevens is om gebruikers te helpen bij het behouden van waarden. Elk gegevenselement is een toewijzing of aanwijzer aan brongegevens. Eén gegevenselement is een variabele die kan worden toegewezen aan querytekenreeksen, URL&#39;s, cookie-waarden, JavaScript-variabelen enzovoort. Selecteer **Gegevenselementen** op de linkernavigatiebalk en **Nieuw gegevenselement maken**.

![](../images/getting-started/data-element-create-new-link.png)

Extensies kunnen gegevenselementen definiëren als dat nodig is om de extensie te laten werken of eenvoudig als gebruiksvriendelijk voor gebruikers. Wanneer een extensie gegevenselementen bevat, worden deze weergegeven in een vervolgkeuzelijst voor gebruikers op het scherm **Gegevenselement maken**:

![](../images/getting-started/create-data-element.png)

Wanneer een gebruiker uw extensie selecteert in het vervolgkeuzemenu **Extension**, wordt het vervolgkeuzemenu **Gegevenselement Type** gevuld met alle gegevenselementen die door de extensie worden geleverd. De gebruiker kan dan elk gegevenselement aan zijn bronwaarde in kaart brengen. De elementen van gegevens kunnen dan worden gebruikt wanneer het bouwen van regels in de Gebeurtenis van de Verandering van het Element van Gegevens of de Gebeurtenis van de Code van de Douane om een uit te voeren regel teweeg te brengen. Een gegevenselement kan ook in de Voorwaarde van het Element van Gegevens of andere Voorwaarden, Uitzonderingen, of Acties in een regel worden gebruikt.

Zodra het gegevenselement wordt gecreeerd (de afbeelding wordt opstelling), kunnen de gebruikers de brongegevens door het gegevenselement eenvoudig van verwijzingen te voorzien van verwijzingen voorzien. Als de bron van de waarde verandert (site wordt opnieuw ontworpen, enz.) gebruikers hoeven de afbeelding slechts één keer bij te werken in de gebruikersinterface voor gegevensverzameling en alle gegevenselementen ontvangen automatisch de nieuwe bronwaarde.

### Regels

Selecteer **Regels** in de linkernavigatie, dan **Nieuwe Regel** creëren.

![](../images/getting-started/rules-link.png)

Voer eerst een beschrijvende naam in als regel. Het scherm **Regel maken** wordt ingesteld als een instructie `if-then`.

![](../images/getting-started/create-new-rule.png)

Als een gebeurtenis plaatsvindt en de voorwaarden worden doorgegeven en er zijn geen uitzonderingen, wordt de actie geactiveerd. Deze zelfde stroom bestaat in uitbreidingen waar u gebeurtenissen, voorwaarden, uitzonderingen, gegevenselementen, of acties kunt tot stand brengen of hefboomwerking.

Voeg met het Facebook-extensievoorbeeld een gebeurtenis toe telkens wanneer een pagina op de testsite wordt geladen.

![](../images/getting-started/load-event.png)

Met `Window Loaded` **Gebeurtenistype** zorgt u ervoor dat elke keer dat een pagina op de testsite wordt geladen deze regel wordt geactiveerd. Selecteer **Wijzigingen behouden**. In dit voorbeeld negeert u **Voorwaarden** als de regel moet worden geactiveerd voor elke pagina op de testsite.

Selecteer **Toevoegen** onder **ACTIES**. Het **scherm van de Configuratie van de Actie** verschijnt. Daarna moet u de uitbreiding kiezen die de regel moet worden toegepast op, en de actie om voor te komen wanneer de regel wordt teweeggebracht. Selecteer **Facebook Pixel** in de vervolgkeuzelijst **Extensie** en **Paginaweergave verzenden** in de vervolgkeuzelijst **Type handeling**. Selecteer **Wijzigingen behouden** en **Opslaan** op het volgende **Regels bewerken**-scherm.

![](../images/getting-started/action-configuration.png)

Selecteer tijdens het testen van de extensie relevante gebeurtenissen, voorwaarden, enzovoort. die door uw extensie worden geleverd, in een willekeurig aantal regels.

## Uw wijzigingen publiceren {#publish}

Selecteer **Publiceren** in de hoofdnavigatie en vervolgens op **Nieuwe bibliotheek toevoegen**-koppeling:

![](../images/getting-started/add-new-library.png)

Een bibliotheek is een set instructies voor hoe extensies, gegevenselementen en regels met elkaar en met een website communiceren. Bibliotheken worden gecompileerd in builds. Een bibliotheek kan net zoveel wijzigingen bevatten als een gebruiker gemakkelijk kan maken of testen in één keer.

Voeg op het scherm **Bibliotheek maken** een naam toe in het tekstveld **Naam**. Tags bieden een standaardontwikkelomgeving met de naam **Development**. Selecteer **Ontwikkeling** in de vervolgkeuzelijst **Omgeving**. Voeg voor het gemak alle beschikbare bronnen toe. Selecteer **Alle gewijzigde bronnen toevoegen** en selecteer **Opslaan**.

>[!NOTE]
>
>Wanneer u een bron aan een bibliotheek toevoegt, wordt een momentopname van die bron op dat exacte moment genomen en aan de bibliotheek toegevoegd. Wanneer u later wijzigingen aanbrengt in uw bronnen (bijvoorbeeld als gevolg van correcties die u moet aanbrengen), moet u de bibliotheek ook bijwerken met de nieuwste wijzigingen in uw bronnen. De **Add Alle Gewijzigde Middelen** knoop is nuttig ook voor dit doel.

![](../images/getting-started/create-new-library.png)

Nu alle wijzigingen zijn opgenomen in de nieuwe bibliotheek (met de naam **dev** in het opgegeven voorbeeld), selecteert u **Opslaan en bouwen op ontwikkeling**.

![](../images/getting-started/build-for-dev.png)

Nadat het bouwstijlproces voltooit, een groene **succes** indicatorvertoningen naast de bibliotheeknaam.

![](../images/getting-started/successful-build.png)

De tagbibliotheek is nu gepubliceerd en beschikbaar voor gebruik. De testpagina moet de nieuwe bibliotheek gebruiken om het paginagedrag voor de eindgebruiker in browser te testen.

## Tags op een testsite installeren {#install-data-collection-tags}

Installatie-instructies zijn beschikbaar op het tabblad Omgevingen. Op deze pagina worden alle beschikbare omgevingen weergegeven en kunt u meer maken. Terwijl de bibliotheek naar de ontwikkelomgeving is gepubliceerd, selecteert u het vakpictogram in de kolom **INSTALL** op de rij **Development**.

![](../images/getting-started/launch-installation-instructions.png)

Het dialoogvenster **Web-installatie instructies** voor de ontwikkelomgeving wordt weergegeven. Selecteer het kopieerpictogram om de gehele `<script>`-tag te kopiëren.

![](../images/getting-started/launch-installation-instructions-dialogue.png)

Voltooi de installatie door deze enkele `<script>`-tag in de sectie `<head>` van uw document- of sitesjabloon te plaatsen. Ga vervolgens naar de testsite om het gedrag van uw gepubliceerde tagbibliotheek te bekijken.

## Testen {#test}

Hieronder volgt een lijst met handige consoleopdrachten voor het valideren van uw extensie op uw testpagina of site.

- `_satellite.setDebug(true);` zal zuivert wijze en output nuttige registrerenverklaringen aan de console toelaten.
- Het `_satellite._container`-object bevat nuttige informatie over de geïmplementeerde bibliotheek, zoals details over de opgenomen build, gegevenselementen, regels en extensies.

Het doel van deze test is de functionaliteit van de geïmplementeerde bibliotheek te controleren en ervoor te zorgen dat het extensiepakket zich gedraagt zoals u had verwacht nadat het in een bibliotheek is opgenomen.

Wanneer u veranderingen ontdekt die aan uw uitbreidingspakket moeten worden aangebracht, is het herhalingsproces gelijkaardig aan het ontwikkelingsproces.

1. Breng wijzigingen aan in de code in uw project.
1. Valideer de wijzigingen met het gereedschap Sandbox.
1. Gebruik het gereedschap Packager om een nieuw ZIP-pakket te maken
1. Gebruik het gereedschap Uploader om het nieuwe ZIP-pakket te uploaden. Het proces volgt dezelfde instructies als voor de eerste upload. Aangezien er in de ontwikkelingsmodus al een extensiepakket met die naam bestaat, wordt de oudere versie door dit nieuwe pakket overschreven in plaats van een nieuwe versie te maken.

   >[!NOTE]
   >
   >Argumenten kunnen op de bevellijn worden overgegaan om tijd te besparen door het herhaalde ingaan van geloofsbrieven te vermijden. Lees voor meer informatie hierover de [reactoruploader documentatie](https://www.npmjs.com/package/@adobe/reactor-uploader).
1. De installatiestap kan worden overgeslagen wanneer een bestaand pakket wordt bijgewerkt.
1. Wijzig middelen - als de configuratie voor om het even welk van uw uitbreidingscomponenten is veranderd, zult u die middelen in de Inzameling van Gegevens UI moeten bijwerken.
1. Voeg de meest recente wijzigingen toe aan uw bibliotheek en maak de bibliotheek opnieuw.
1. Voltooi nog een testronde.

<!--
## Document {#document}

Your [exchange listing](./create-listing.md) is a great place for marketing and support information for your extension, but our tags [Help Docs](https://experienceleague.adobe.com/docs/launch/using/overview.html) are used every day by our customers. We encourage you to submit a pull request to [add your extension documentation](https://github.com/AdobeDocs/launch.en/blob/master/help/extension-reference/3rd-party-extensions.md) into the tags user docs. Open source docs for the win! 🚀
-->
