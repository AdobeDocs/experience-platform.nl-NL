---
title: Gegevens met toestemming van de klant verwerken met de Adobe Experience Platform Web SDK
topic-legacy: getting started
description: Leer hoe u de SDK van Adobe Experience Platform Web integreert om gegevens over toestemming van klanten te verwerken in Adobe Experience Platform.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '1299'
ht-degree: 0%

---

# Integreer het Web SDK van het Platform om de gegevens van de klanteninstemming te verwerken

Met de Adobe Experience Platform Web SDK kunt u de door CMP&#39;s (Consent Management Platforms) gegenereerde toestemmingssignalen van klanten ophalen en deze naar Adobe Experience Platform verzenden wanneer er een gebeurtenis plaatsvindt waarbij de toestemming wordt gewijzigd.

**De SDK interface niet met CMP&#39;s uit het vak**. Het is aan u om te bepalen hoe te om SDK in uw website te integreren, naar toestemmingsveranderingen in CMP te luisteren, en het aangewezen bevel te roepen. Dit document biedt algemene richtlijnen voor het integreren van uw CMP met de Web SDK van het Platform.

## Vereisten {#prerequisites}

In deze zelfstudie wordt ervan uitgegaan dat u al hebt bepaald hoe u gegevens over toestemming binnen uw CMP kunt genereren en dat u een gegevensset hebt gemaakt die machtigingsvelden bevat die voldoen aan de Adobe-standaard of de TCF 2.0-standaard (Transparency and Consent Framework). Als u deze dataset nog niet hebt gecreeerd, verwijs naar de volgende leerprogramma&#39;s alvorens aan deze gids terug te keren:

* [Een gegevensset maken met de standaard Adobe](./adobe/dataset.md)
* [Creeer een dataset gebruikend de norm TCF 2.0](./iab/dataset.md)

Deze handleiding volgt de workflow voor het instellen van de SDK met behulp van de tagextensie in de gebruikersinterface voor gegevensverzameling. Raadpleeg de volgende documenten in plaats van deze handleiding als u de extensie niet wilt gebruiken en de zelfstandige versie van de SDK rechtstreeks op uw site wilt insluiten:

* [Een gegevensstroom configureren](../../../edge/datastreams/overview.md)
* [De SDK installeren](../../../edge/fundamentals/installing-the-sdk.md)
* [De SDK configureren voor toestemmingsopdrachten](../../../edge/consent/supporting-consent.md)

De installatiestappen in deze handleiding vereisen een goed begrip van de uitbreidingen van tags en hoe deze in webtoepassingen worden ge??nstalleerd. Raadpleeg de volgende documentatie voor meer informatie:

* [Overzicht van codes](../../../tags/home.md)
* [Snelstartgids](../../../tags/quick-start/quick-start.md)
* [Overzicht van publicatie](../../../tags/ui/publishing/overview.md)

## Een gegevensstroom instellen

SDK kan alleen gegevens naar Experience Platform verzenden als u eerst een gegevensstroom configureert. Selecteer in de gebruikersinterface voor gegevensverzameling de optie **[!UICONTROL Datastreams]** in de linkernavigatie.

Nadat u een nieuwe gegevensstroom hebt gemaakt of een bestaande gegevensstroom hebt geselecteerd om te bewerken, selecteert u de schakelknop naast **[!UICONTROL Adobe Experience Platform]**. Gebruik vervolgens de hieronder vermelde waarden om het formulier in te vullen.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Veld DataStream | Waarde |
| --- | --- |
| [!UICONTROL Sandbox] | De naam van het Platform [sandbox](../../../sandboxes/home.md) die de vereiste het stromen verbinding en datasets aan opstelling de gegevensstroom bevat. |
| [!UICONTROL Streaming Inlet] | Een geldige streamingverbinding voor Experience Platform. Zie de zelfstudie aan [streaming verbinding maken](../../../ingestion/tutorials/create-streaming-connection-ui.md) als u geen bestaande streaminginlaat hebt. |
| [!UICONTROL Event Dataset] | An [!DNL XDM ExperienceEvent] dataset die u bij het verzenden van gebeurtenisgegevens naar het gebruiken van SDK van plan bent. Terwijl u een gebeurtenisdataset moet verstrekken om een gegevensstroom van het Platform tot stand te brengen, gelieve te merken dat de toestemmingsgegevens die via gebeurtenissen worden verzonden niet in stroomafwaartse handhavingswerkschema&#39;s worden nageleefd. |
| [!UICONTROL Profile Dataset] | De [!DNL Profile]-enabled dataset met de gebieden van de klanteninstemming die u creeerde [eerder](#prerequisites). |

Als u klaar bent, selecteert u **[!UICONTROL Save]** onder aan het scherm en doorgaan met het volgen van eventuele extra vragen om de configuratie te voltooien.

## De SDK van het Web Platform installeren en configureren

Zodra u een gegevensstroom zoals die in de vorige sectie wordt beschreven hebt gecreeerd, moet u de uitbreiding van SDK van het Web van het Platform dan vormen die u uiteindelijk op uw plaats zult opstellen. Als de SDK-extensie niet op de eigenschap Tag is ge??nstalleerd, selecteert u **[!UICONTROL Extensions]** in de linkernavigatie, gevolgd door **[!UICONTROL Catalog]** tab. Selecteer vervolgens **[!UICONTROL Install]** onder de SDK-extensie van het Platform in de lijst met beschikbare extensies.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Bij het configureren van de SDK, onder **[!UICONTROL Edge Configurations]** selecteert u de gegevensstroom die u in de vorige stap hebt gemaakt.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Selecteren **[!UICONTROL Save]** om de extensie te installeren.

### Een gegevenselement maken om de standaardtoestemming in te stellen

Als de SDK-extensie is ge??nstalleerd, kunt u een gegevenselement maken dat de standaardwaarde voor de toestemming voor gegevensverzameling vertegenwoordigt (`collect.val`) voor uw gebruikers. Dit kan handig zijn als u verschillende standaardwaarden wilt hebben, afhankelijk van de gebruiker, zoals `pending` voor gebruikers in de Europese Unie en `in` voor Noord-Amerikaanse gebruikers.

In dit geval kunt u het volgende implementeren om standaardtoestemming in te stellen op basis van het gebied van de gebruiker:

1. Bepaal het gebied van de gebruiker op de Webserver.
1. Voor de `script` -tag (insluitcode) op de webpagina weergeven, een aparte `script` tag die een `adobeDefaultConsent` variabele gebaseerd op het gebied van de gebruiker.
1. Stel een gegevenselement in dat gebruikmaakt van de `adobeDefaultConsent` JavaScript-variabele en gebruik dit gegevenselement als de standaardwaarde voor de toestemming voor de gebruiker.

Als het gebied van de gebruiker door CMP wordt bepaald, kunt u de volgende stappen in plaats daarvan gebruiken:

1. Verwerk de gebeurtenis &quot;CMP geladen&quot; op de pagina.
1. Stel in de gebeurtenishandler een `adobeDefaultConsent` variabele gebaseerd op het gebied van de gebruiker, en laadt dan het manuscript van de markeringsbibliotheek gebruikend JavaScript.
1. Stel een gegevenselement in dat gebruikmaakt van de `adobeDefaultConsent` JavaScript-variabele en gebruik dit gegevenselement als de standaardwaarde voor de toestemming voor de gebruiker.

Als u een gegevenselement wilt maken in de gebruikersinterface voor gegevensverzameling, selecteert u **[!UICONTROL Data Elements]** in de linkernavigatie selecteert u vervolgens **[!UICONTROL Add Data Element]** om naar het dialoogvenster voor het maken van gegevenselementen te navigeren.

Van hieruit moet u een [!UICONTROL JavaScript Variable] gegevenselement gebaseerd op `adobeDefaultConsent`. Selecteren **[!UICONTROL Save]** wanneer gereed.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Zodra het gegevenselement wordt gecreeerd, navigeer terug naar de de uitbreidingsconfig-pagina van SDK van het Web. Onder de [!UICONTROL Privacy] sectie, selecteert u **[!UICONTROL Provided by data element]** en gebruik het dialoogvenster dat verschijnt om het gegevenselement voor standaardtoestemming te selecteren dat u eerder hebt gemaakt.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### De extensie op uw website implementeren

Nadat u de extensie hebt geconfigureerd, kunt u deze integreren in uw website. Zie de [publicatiehandleiding](../../../tags/ui/publishing/overview.md) in de tagdocumentatie voor gedetailleerde informatie over hoe u de bijgewerkte bibliotheek kunt implementeren.

## Opdrachten voor wijzigen van toestemming maken {#commands}

Zodra u de uitbreiding SDK in uw website hebt ge??ntegreerd, kunt u beginnen te gebruiken het Web SDK van het Platform `setConsent` om toestemmingsgegevens naar het Platform te verzenden.

>[!IMPORTANT]
>
>De `setConsent` de opdracht werkt alleen gegevens rechtstreeks bij in de opslag Profiel en verzendt geen gegevens naar het gegevensmeer.

Er zijn twee scenario&#39;s waarin `setConsent` moet op uw site worden aangeroepen:

1. Wanneer toestemming op de pagina wordt geladen (met andere woorden op elke pagina die wordt geladen)
1. Als onderdeel van een CMP-haak of gebeurtenislistener die wijzigingen in toestemmingsinstellingen detecteert

>[!NOTE]
>
>Voor een inleiding aan de gemeenschappelijke syntaxis voor de bevelen van SDK van het Platform, zie het document op [uitvoeren, opdrachten](../../../edge/fundamentals/executing-commands.md).

De `setConsent` bevel verwacht twee argumenten:

1. Een tekenreeks die het opdrachttype aangeeft (in dit geval `"setConsent"`)
1. Een object payload dat ????n eigenschap van het type array bevat: `consent`. De `consent` array moet ten minste ????n object bevatten dat de vereiste toestemmingsvelden voor de Adobe-standaard bevat.

De vereiste toestemmingsgebieden voor de norm van de Adobe worden getoond in het volgende voorbeeld `setConsent` oproep:

```js
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: {
        val: "y"
      },
      share: {
        val: "y"
      },
      personalize: {
        content: {
          val: "y"
        }
      },
      metadata: {
        time: "2020-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| Payload, eigenschap | Beschrijving |
| --- | --- |
| `standard` | De gebruikte toestemmingsnorm. Voor de standaard Adobe moet deze waarde worden ingesteld op `Adobe`. |
| `version` | Het versienummer van de krachtens `standard`. Deze waarde moet worden ingesteld op `2.0` voor de verwerking van Adobe-standaardtoestemmingen. |
| `value` | De bijgewerkte toestemmingsinformatie van de klant, die als voorwerp XDM wordt verstrekt die aan de structuur van de profiel-Toegelaten de toestemmingsgebieden van de dataset in overeenstemming is. |

>[!NOTE]
>
>Als u andere toestemmingsnormen in combinatie met gebruikt `Adobe` (zoals `IAB TCF`), kunt u extra objecten toevoegen aan de `consent` array voor elke standaard. Elk object moet geschikte waarden bevatten voor `standard`, `version`, en `value` voor de door hen vertegenwoordigde toestemmingsnorm.

In het volgende JavaScript ziet u een voorbeeld van een functie die de voorkeurswijzigingen voor toestemming op een website verwerkt. Deze functie kan worden gebruikt als callback in een gebeurtenislistener of een CMP-haak:

```js
var setConsent = function () {

  // Retrieve the current consent data.
  var categories = getConsentData();

  // If the script is running on a consent change, generate a new timestamp.
  // If the script is running on page load, set the timestamp to when the consent values last changed.
  var now = new Date();
  var collectedAt = consentChanged ? now.toISOString() : categories.collectedAt;

  //  Map the consent values and timestamp to XDM
  var consentXDM = {
    collect: {
      val: categories.collect !== -1 ? "y" : "n"
    },
    personalize: {
      content: {
        val: categories.personalizeContent !== -1 ? "y" : "n"
      }
    },
    share: {
      val: categories.share !== -1 ? "y" : "n"
    },
    metadata: {
      time: collectedAt
    }
  };

  // Pass the XDM object to the Platform Web SDK
  alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: consentXDM
    }]
  });
});
```

## Reacties in SDK verwerken

Alles [!DNL Platform SDK] de bevelen keren beloftes terug die erop wijzen of de vraag slaagde of ontbrak. U kunt deze reacties vervolgens gebruiken voor extra logica, zoals het weergeven van bevestigingsberichten aan de klant. Zie de sectie over [afhandeling gelukt of mislukt](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) in de handleiding voor het uitvoeren van SDK-opdrachten voor specifieke voorbeelden.

Zodra u met succes hebt gemaakt `setConsent` Met de SDK kunt u via de profielviewer in de interface van het Platform controleren of gegevens in het archief Profiel worden gedownload. Zie de sectie over [bladeren door profielen op identiteit](../../../profile/ui/user-guide.md#browse-identity) voor meer informatie .

## Volgende stappen

Door deze gids te volgen, hebt u de uitbreiding van SDK van het Web van het Platform gevormd om toestemmingsgegevens naar Experience Platform te verzenden. Raadpleeg voor hulp bij het testen van uw implementatie de documentatie voor de toestemmingsnorm die u implementeert:

* [Adobe standaard](./adobe/overview.md#test)
* [TCF 2.0 standaard](./iab/overview.md#test)
