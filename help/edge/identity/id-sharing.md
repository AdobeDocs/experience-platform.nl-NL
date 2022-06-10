---
title: Id's delen via mobiel naar web en verschillende domeinen
description: Leer hoe u id's van bezoekers van mobiele naar webeigenschappen en in verschillende domeinen kunt behouden
keywords: Identiteit;mobiel;id;delen;domein;cross-domain;sdk;platform;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: 3b65143e33804b251f888dbe2a69d238b3f4cda3
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# Id&#39;s delen via mobiel naar web en verschillende domeinen

## Overzicht

De Adobe Experience Platform Web SDK ondersteunt mogelijkheden voor het delen van bezoekersidentificaties, waarmee klanten een betere persoonlijke ervaring kunnen bieden, tussen mobiele apps en mobiele webinhoud, en in verschillende domeinen.

## Gebruiksscenario’s {#use-cases}

### Lever consistente personalisatie tussen mobiele apps en mobiele websites

Een kledingbedrijf wil de ervaring van hun klanten personaliseren die op hun belangen wordt gebaseerd, en de verpersoonlijking nauwkeurig houden in een mobiele toepassing die ook WebViews laadt. Met de functie voor het delen van mobiele tot webid kunnen ze ervoor zorgen dat de meest nauwkeurige aanbiedingen aan klanten worden gepresenteerd met dezelfde bezoeker-id in de app en mobiele webinhoud door te geven [!DNL ECID] naar de URL van het mobiele web.

### Zorg voor consistente personalisatie in verschillende domeinen

Een detailhandelaar met veelvoudige online winkels wil de winkelervaring over hun domeinen personaliseren, die op klantenbelangen wordt gebaseerd. Gebruikend de het delen eigenschap van identiteitskaart van SDK van het Web dwars-domein, kan de detailhandelaar nauwkeurige aanbiedingen leveren die op klantenbelangen, over elk van hun domeinen worden gebaseerd.

### De rapportage van bezoekersactiviteiten verbeteren

Een technologieverkoper wil zijn bezoekersactiviteit rapporteren met informatie over wanneer zijn bezoekers van de mobiele toepassing naar hun mobiele website of naar hun andere domeinen verhuizen. Gebruikend de het delen eigenschap van identiteitskaart van SDK van het Web dwars-domein, kan het marketing team bezoekers over hun Webeigenschappen nauwkeurig volgen en activiteitenrapporten produceren.

## Vereisten {#prerequisites}

Als u de id&#39;s van mobiel naar web en tussen domeinen wilt delen, moet u [!DNL Web SDK] versie 2.11.0 of hoger.

Voor mobiele Edge Network-implementaties wordt deze functie ondersteund in het dialoogvenster [Identiteit voor Edge Network](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) extensie die begint met versie 1.1.0 (iOS en Android).

Deze functie is ook compatibel met [!DNL VisitorAPI.js] versie 1.7.0 of hoger.

## Id&#39;s delen via mobiele apparaten {#mobile-to-web}

Gebruik de `getUrlVariables` API van de [Identiteit voor Edge Network](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables) extensie om de id&#39;s op te halen als queryparameters en deze aan uw URL te koppelen bij het openen van de URL [!DNL webViews].

Geen extra configuratie wordt vereist voor Web SDK om goed te keuren `ECID` waarden in de queryreeks.

De parameter van het vraagkoord omvat:

* `MCID`: De Experience Cloud-id (`ECID`)
* `MCORGID`: De Experience Cloud `orgID` dat moet overeenkomen met `orgID` geconfigureerd in het dialoogvenster [!DNL Web SDK].
* `TS`: Een tijdstempelparameter die niet ouder kan zijn dan vijf minuten.


Bij het delen van een mobiele id naar een web wordt gebruikgemaakt van de `adobe_mc` parameter. Wanneer de `adobe_mc` parameter aanwezig en geldig is, `ECID` van het vraagkoord wordt automatisch toegevoegd aan de identiteitskaart in het eerste verzoek dat aan het Netwerk van de Rand wordt gemaakt. Alle volgende Edge Network-interacties gebruiken `ECID`.

Raadpleeg de documentatie voor meer informatie over het doorgeven van gebruikers-id&#39;s van een mobiele app aan een WebView [webweergaven verwerken](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Id delen tussen domeinen {#cross-domain-sharing}

Voor het delen van verschillende domeinen-id&#39;s voegt SDK van het Web versie 2.11.0 steun voor `appendIdentityToUrl` gebruiken. Wanneer gebruikt, produceert dit bevel `adobe_mc` querytekenreeksparameter.

De opdracht accepteert een object met één eigenschap. `url`en retourneert een object met de eigenschap `url`.

Deze opdracht wacht niet op een toestemmingsupdate. Als er geen toestemming is gegeven, wordt de URL ongewijzigd geretourneerd.

Als een `ECID` niet wordt opgegeven, `/acquire` het eindpunt zal worden geroepen om een `ECID`.

Hieronder ziet u hoe een klant het delen van verschillende domeinen-id&#39;s op zijn website kan implementeren.

Deze code voegt een gebeurtenislistener toe voor alle klikken op de pagina en of de klik zich op een koppeling naar een overeenkomend domein bevond (in dit geval `adobe.com` of `behance.com`), voegt de identiteit toe aan de URL en leidt de gebruiker daar om.

```js
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

## De extensie Tags gebruiken {#tags-extension}

Vergelijkbaar met het gebruik van de [!DNL Web SDK], is er geen aanvullende configuratie vereist in de [!DNL Tags] extensie voor het gebruik van identiteiten die via de URL zijn doorgegeven.

Als u de id&#39;s van mobiele apparaten naar websites en andere domeinen wilt delen via de extensie Tags, moet u versie 2.12.0 of hoger van de extensie Tags gebruiken.

Als u identiteiten van de huidige pagina naar andere domeinen wilt delen, is er een nieuwe actie beschikbaar in het dialoogvenster [!DNL Web SDK] [!DNL Tags] extensie. Deze handeling is bedoeld voor gebruik met een **[!UICONTROL Core - Click]** gebeurtenistype en een vergelijkingsvoorwaarde voor waarden.

Voer de beschreven stappen uit [hier](../../tags/ui/managing-resources/rules.md) om een regel met de volgende configuratie tot stand te brengen:

* [!UICONTROL Event Configuration]:
   * **[!UICONTROL Extension: Core]**
   * **[!UICONTROL Event Type: Click]**
   * Selecteer **[!UICONTROL When the user clicks on > specific elements]**
   * Typ in het dialoogvenster **[!UICONTROL Selector]**: `a[href]`. Deze gebeurtenis wordt geactiveerd telkens wanneer op een ankertag op de pagina met een `href` eigenschap.

      ![UI-afbeelding die de gebeurtenisconfiguratie weergeeft met de hierboven beschreven instellingen](assets/id-sharing-event-configuration.png)

* [!UICONTROL Condition Configuration]
   * **[!UICONTROL Logic Type]**: [!UICONTROL Regular]
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL Condition Type]**: [!UICONTROL Value Comparison]
   * **[!UICONTROL Left Operand]**: [!UICONTROL `%this.hostname%`]. Dit is een speciaal gegevenselement dat werkt met [!UICONTROL Core - Click] gebeurtenissen en wordt de hostnaam van de koppeling waarop is geklikt, hersteld.
   * **[!UICONTROL Operator]**: [!UICONTROL Matches Regex]
   * **[!UICONTROL Right Operand]**: Typ een reguliere expressie die overeenkomt met de domeinen waarmee u identiteiten wilt delen. Zo kunt u bijvoorbeeld koppelingen afstemmen met hostnamen die eindigen met `adobe.com` of `behance.com`, gebruik deze reguliere expressie: `behance.com$|adobe.com$`. De gekoppelde pagina moet de [!DNL Web SDK] of [!DNL Visitor ID] geïnstalleerd om de identiteit te accepteren.

      ![UI-afbeelding die de configuratie van de voorwaarde weergeeft met de hierboven beschreven instellingen](assets/id-sharing-condition-configuration.png)

* [!UICONTROL Action Configuration]
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action Type]**: [!UICONTROL Redirect with identity]
   * **[!UICONTROL Instance]**: Selecteer uw exemplaar. In de meeste gevallen, zult u slechts één gevormde instantie hebben. Als u meerdere exemplaren hebt, selecteert u de instantie met de identiteit die u wilt delen.

      ![UI-afbeelding die de actieconfiguratie weergeeft met de hierboven beschreven instellingen](assets/id-sharing-action-configuration.png)

De **[!UICONTROL Redirect with identity]** Met deze handeling wordt de browser belet door de koppeling te navigeren. Vervolgens roept het de `appendIdentityToUrl` op de [!DNL Web SDK] -instantie.

Ten slotte wordt de gebruiker doorgestuurd naar de [!DNL URL] met de `adobe_mc` parameter querytekenreeks toegevoegd.
