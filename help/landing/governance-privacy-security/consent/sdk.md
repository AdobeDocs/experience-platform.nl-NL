---
title: Gegevens met toestemming van de klant verwerken met Adobe Experience Platform Web SDK
description: Leer hoe u de Adobe Experience Platform Web SDK integreert om gegevens over klanttoestemming in Adobe Experience Platform te verwerken.
role: Developer
feature: Consent, Web SDK
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1293'
ht-degree: 0%

---

# Integreer de Experience Platform Web SDK om gegevens over toestemming van klanten te verwerken

Met de Adobe Experience Platform Web SDK kunt u de door CMP&#39;s (Consent Management Platforms) gegenereerde toestemmingssignalen van klanten ophalen en deze naar Adobe Experience Platform verzenden wanneer er een gebeurtenis plaatsvindt die aanleiding geeft tot wijziging van de toestemming.

**SDK interface niet met om het even welke CMPs uit de doos**. Het is aan u om te bepalen hoe te om de SDK in uw website te integreren, naar toestemmingsveranderingen in CMP te luisteren, en het aangewezen bevel te roepen. Dit document biedt algemene richtlijnen voor het integreren van uw CMP met de Experience Platform Web SDK.

## Vereisten {#prerequisites}

In deze zelfstudie wordt ervan uitgegaan dat u al hebt bepaald hoe u gegevens over toestemming binnen uw CMP kunt genereren en dat u een gegevensset hebt gemaakt die machtigingsvelden bevat die voldoen aan de Adobe-standaard of de TCF 2.0-standaard (IAB Transparency and Consent Framework). Als u deze dataset nog niet hebt gecreeerd, verwijs naar de volgende leerprogramma&#39;s alvorens aan deze gids terug te keren:

* [Een gegevensset maken met de Adobe-standaard](./adobe/dataset.md)
* [Creeer een dataset gebruikend de norm TCF 2.0](./iab/dataset.md)

Deze handleiding volgt de workflow voor het instellen van de SDK met de tagextensie in de gebruikersinterface. Raadpleeg de volgende documenten in plaats van deze handleiding als u de extensie niet wilt gebruiken en de zelfstandige versie van de SDK liever rechtstreeks op uw site wilt insluiten:

* [Een gegevensstroom configureren](/help/datastreams/overview.md)
* [De SDK installeren](/help/collection/js/install/overview.md)
* [SDK configureren voor toestemmingsopdrachten](/help/collection/js/commands/configure/defaultconsent.md)

De installatiestappen in deze handleiding vereisen een goed begrip van de uitbreidingen van tags en hoe deze in webtoepassingen worden geïnstalleerd. Raadpleeg de volgende documentatie voor meer informatie:

* [Overzicht van codes](/help/tags/home.md)
* [Snelstartgids](/help/tags/quick-start/quick-start.md)
* [Overzicht van publicatie](/help/tags/ui/publishing/overview.md)

## Een gegevensstroom instellen

Als de SDK gegevens naar Experience Platform moet verzenden, moet u eerst een gegevensstroom configureren. Selecteer **[!UICONTROL Datastreams]** in de linkernavigatie in de gebruikersinterface voor gegevensverzameling of de gebruikersinterface van Experience Platform.

Nadat u een nieuwe gegevensstroom hebt gemaakt of een bestaande gegevensstroom hebt geselecteerd om te bewerken, selecteert u de schakelknop naast **[!UICONTROL Adobe Experience Platform]** . Gebruik vervolgens de hieronder vermelde waarden om het formulier in te vullen.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Veld DataStream | Waarde |
| --- | --- |
| [!UICONTROL Sandbox] | De naam van de zandbak van Experience Platform [ ](/help/sandboxes/home.md) die de vereiste het stromen verbinding en datasets aan opstelling bevat de datastream. |
| [!UICONTROL Event Dataset] | Een [!DNL XDM ExperienceEvent] dataset die u van plan bent om gebeurtenisgegevens naar het gebruiken van SDK te verzenden. Hoewel u een gebeurtenissendataset moet verstrekken om een Experience Platform datastream te creëren, gelieve te merken dat toestemmingsgegevens die via gebeurtenissen worden verzonden niet in stroomafwaartse handhavingswerkschema&#39;s worden nageleefd. |
| [!UICONTROL Profile Dataset] | [!DNL Profile] - toegelaten dataset met de gebieden van de klantentoestemming die u [ ](#prerequisites) creeerde. |

Als u klaar bent, selecteert u **[!UICONTROL Save]** onder aan het scherm en gaat u verder met het volgen van eventuele extra aanwijzingen om de configuratie te voltooien.

## Experience Platform Web SDK installeren en configureren

Zodra u een gegevensstroom zoals die in de vorige sectie wordt beschreven hebt gecreeerd, moet u dan de uitbreiding vormen van Experience Platform Web SDK die u uiteindelijk op uw plaats zult opstellen. Als u de extensie SDK niet op de eigenschap tag hebt geïnstalleerd, selecteert u **[!UICONTROL Extensions]** in de linkernavigatie, gevolgd door de tab **[!UICONTROL Catalog]** . Selecteer vervolgens **[!UICONTROL Install]** onder de extensie Experience Platform SDK in de lijst met beschikbare extensies.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Selecteer onder **[!UICONTROL Edge Configurations]** bij het configureren van de SDK de gegevensstroom die u in de vorige stap hebt gemaakt.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Selecteer **[!UICONTROL Save]** om de extensie te installeren.

### Een gegevenselement maken om de standaardtoestemming in te stellen

Als de extensie SDK is geïnstalleerd, kunt u een gegevenselement maken dat de waarde voor de standaardtoestemming voor gegevensverzameling (`collect.val`) voor uw gebruikers vertegenwoordigt. Dit kan handig zijn als u verschillende standaardwaarden wilt hebben, afhankelijk van de gebruiker, zoals `pending` voor gebruikers in de Europese Unie en `in` voor gebruikers in Noord-Amerika.

In dit geval kunt u het volgende implementeren om standaardtoestemming in te stellen op basis van het gebied van de gebruiker:

1. Bepaal het gebied van de gebruiker op de Webserver.
1. Geef vóór de tag `script` (code insluiten) op de webpagina een aparte `script` -tag weer die een `adobeDefaultConsent` -variabele instelt op basis van het gebied van de gebruiker.
1. Stel een gegevenselement in dat de variabele `adobeDefaultConsent` JavaScript gebruikt en gebruik dit gegevenselement als de standaardwaarde voor de toestemming voor de gebruiker.

Als het gebied van de gebruiker door CMP wordt bepaald, kunt u de volgende stappen in plaats daarvan gebruiken:

1. Verwerk de gebeurtenis &quot;CMP geladen&quot; op de pagina.
1. Stel in de gebeurtenishandler een variabele `adobeDefaultConsent` in op basis van het gebied van de gebruiker en laad vervolgens het script van de tagbibliotheek met JavaScript.
1. Stel een gegevenselement in dat de variabele `adobeDefaultConsent` JavaScript gebruikt en gebruik dit gegevenselement als de standaardwaarde voor de toestemming voor de gebruiker.

Als u een gegevenselement in de gebruikersinterface wilt maken, selecteert u **[!UICONTROL Data Elements]** in de linkernavigatie en selecteert u **[!UICONTROL Add Data Element]** om naar het dialoogvenster voor het maken van gegevenselementen te navigeren.

Van hieruit moet u een [!UICONTROL JavaScript Variable] data-element maken op basis van `adobeDefaultConsent` . Selecteer **[!UICONTROL Save]** wanneer u klaar bent.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Zodra het gegevenselement wordt gecreeerd, navigeer terug naar de de uitbreidingsconfig van SDK van het Web pagina. Selecteer onder de sectie [!UICONTROL Privacy] de optie **[!UICONTROL Provided by data element]** en gebruik het dialoogvenster dat verschijnt om het gegevenselement met standaardtoestemmingen te selecteren dat u eerder hebt gemaakt.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### De extensie op uw website implementeren

Nadat u de extensie hebt geconfigureerd, kunt u deze integreren in uw website. Verwijs naar de [ het publiceren gids ](/help/tags/ui/publishing/overview.md) in de markeringen documentatie voor gedetailleerde informatie over hoe te om uw bijgewerkte bibliotheek op te stellen bouwt.

## Opdrachten voor wijzigen van toestemming maken {#commands}

Als u de SDK-extensie eenmaal in uw website hebt geïntegreerd, kunt u de Experience Platform Web SDK `setConsent` -opdracht gebruiken om gegevens met toestemming naar Experience Platform te verzenden.

De opdracht `setConsent` voert twee handelingen uit:

1. Hiermee werkt u de profielkenmerken van de gebruiker rechtstreeks bij in het archief Profiel. Hiermee worden geen gegevens naar het datumpigment verzonden.
1. Creeert een [ Gebeurtenis van de Ervaring ](/help/xdm/classes/experienceevent.md) die een timestamped rekening van de gebeurtenis van de toestemmingsverandering registreert. Deze gegevens worden rechtstreeks naar het datumpigment verzonden en kunnen worden gebruikt om wijzigingen in de voorkeur voor toestemming in de loop van de tijd bij te houden.

### Wanneer wordt `setConsent` aangeroepen

Er zijn twee situaties waarin `setConsent` op uw site moet worden aangeroepen:

1. Wanneer toestemming op de pagina wordt geladen (met andere woorden op elke pagina die wordt geladen)
1. Als onderdeel van een CMP-haak of gebeurtenislistener die wijzigingen in toestemmingsinstellingen detecteert

### `setConsent` syntaxis

De opdracht [`setConsent`](/help/collection/js/commands/setconsent.md) verwacht een payload-object dat een enkele array-type eigenschap bevat: `consent` . De array `consent` moet ten minste één object bevatten dat de vereiste toestemmingsvelden voor de Adobe-standaard bevat.

De vereiste toestemmingsgebieden voor de norm van Adobe worden getoond in het volgende voorbeeld `setConsent` vraag:

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
        time: "YYYY-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| Payload, eigenschap | Beschrijving |
| --- | --- |
| `standard` | De gebruikte toestemmingsnorm. Voor de Adobe-standaard moet deze waarde worden ingesteld op `Adobe` . |
| `version` | Het versienummer van de toestemmingsnorm die onder `standard` wordt vermeld. Deze waarde moet worden ingesteld op `2.0` voor verwerking van toestemming volgens de Adobe-standaard. |
| `value` | De bijgewerkte toestemmingsinformatie van de klant, die als voorwerp XDM wordt verstrekt die aan de structuur van de profiel-Toegelaten de toestemmingsgebieden van de dataset in overeenstemming is. |

>[!NOTE]
>
>Als u andere toestemmingsnormen samen met `Adobe` (zoals `IAB TCF`) gebruikt, kunt u extra voorwerpen aan de `consent` serie voor elke norm toevoegen. Elk object moet geschikte waarden voor `standard` , `version` en `value` bevatten voor de toestemmingsstandaard die ze vertegenwoordigen.

De volgende JavaScript biedt een voorbeeld van een functie die de voorkeurswijzigingen voor toestemming op een website verwerkt. Deze functie kan worden gebruikt als callback in een gebeurtenislistener of een CMP-haak:

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

  // Pass the XDM object to the Experience Platform Web SDK
  alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: consentXDM
    }]
  });
});
```

## SDK-reacties verwerken

Alle [!DNL Experience Platform SDK] opdrachten retourneren beloftes die aangeven of de aanroep is geslaagd of mislukt. U kunt deze reacties vervolgens gebruiken voor extra logica, zoals het weergeven van bevestigingsberichten aan de klant. Zie [ reacties van het Bevel ](/help/collection/js/commands/command-responses.md) voor meer informatie.

Nadat u `setConsent` -aanroepen met de SDK hebt uitgevoerd, kunt u met de profielviewer in de Experience Platform-gebruikersinterface controleren of gegevens in het Profile Store worden gedownload. Zie de sectie over [ doorbladerend profielen door identiteit ](/help/profile/ui/user-guide.md#browse-identity) voor meer informatie.

## Volgende stappen

Door deze gids te volgen, hebt u de uitbreiding van Experience Platform Web SDK gevormd om toestemmingsgegevens naar Experience Platform te verzenden. Raadpleeg voor hulp bij het testen van uw implementatie de documentatie voor de toestemmingsnorm die u implementeert:

* [Adobe-standaard](./adobe/overview.md#test)
* [TCF 2.0 standaard](./iab/overview.md#test)
