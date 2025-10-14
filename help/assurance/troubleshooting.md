---
title: Handleiding voor probleemoplossing in Adobe Experience Platform Assurance
description: Dit document bevat oplossingen voor algemene problemen bij het gebruik van Adobe Experience Platform Assurance.
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# Problemen met Adobe Experience Platform Assurance oplossen

Als u problemen ondervindt met het verkrijgen van de garantie voor uw werk, raadpleegt u de suggesties onder de volgende onderwerpen over kwesties die u vaak tegenkomt.

Om vlottere implementatie toe te laten en om het even welke potentiële kwesties te ontdekken, verzeker u het programma SDK hebben aangezet per [&#x200B; laat Debug het Registreren &#x200B;](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) in de Begonnen sectie toe.

U kunt SDK logboekniveaus veranderen gebruikend [`setLogLevel` &#x200B;](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API.

## Problemen met toepassingen op apparaten

### QR-code opent app niet

* Open de koppeling rechtstreeks. Kopieer de verbinding van **Details van de Zitting**. Plak het bestand in de adresbalk van de browser van het apparaat om het te openen. Als het niet opent, te zien gelieve sectie [&#x200B; App geen verbinding &#x200B;](#app-does-not-open-link) zal openen.
* Gebruik een andere QR-lezer. Voor iOS 11 of hoger gebruikt u de Foto-app om de QR-code te lezen.

### De app opent de koppeling niet

* Controleer of de implementatie van de diepe koppeling correct is geconfigureerd in de app.
   * **Android:** Diepe Verbindingen (de Verbindingen van de Toepassing)
      * [&#x200B; creeer Diepe Verbindingen aan de Context van de Toepassing &#x200B;](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** Het Regeling van de Douane URL of Universele Verbindingen
      * [&#x200B; het bepalen van een Regeling van Douane URL voor Uw app &#x200B;](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [&#x200B; ondersteunend Universele Verbindingen in Uw app &#x200B;](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>Voor Android hoeft de `startSession` API niet expliciet te worden aangeroepen. Voor iOS, gebruik API zoals die in [&#x200B; wordt beschreven de Verzekering van Adobe Experience Platform &#x200B;](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### Er wordt een verificatiebedekking weergegeven, maar de toepassing kan geen verbinding maken

* Zorg voor internetverbinding van het apparaat via de webbrowser van het apparaat.
* Als de app nooit verbinding heeft gemaakt met de Betrouwbaarheidsservice, moet u controleren of deze correct is ingesteld voor Betrouwbaarheid. Zie instructies bij het installeren van de [&#x200B; bibliotheek van SDK van de Verzekering van Adobe Experience Platform &#x200B;](./tutorials/implement-assurance.md).
* Controleer of de sessie overeenkomt met de koppeling en of deze correct is ingevoerd voor de verwachte sessie. Zie [&#x200B; bericht van het Logboek &quot;informatie OrgID is niet beschikbaar&quot;](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) (dit is ongewoon en relevant slechts als u toegang tot meer dan één instantie van ORG hebt).

### Foutopsporing in Adobe Analytics

**de Verwerkingsstatus van Post - Geen zuivert Vlag**

Als gebeurtenissen in de weergave Analytics Events niet voldoen aan de door Post verwerkte status &quot;No Debug Flag&quot;, biedt de huidige versie van Adobe Analytics of Assurance SDK mogelijk geen ondersteuning voor de functie Analytics Debugging.
Upgrade de Adobe Analytics- en Assurance SDK-extensies naar de meest recente versies om dit probleem op te lossen.

| Vereiste minimumversie | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Betrouwbaarheid | > 1.0.0 | > 1.0.0 |

### Compatibiliteit met React Native MobileCore en AEPAssurance

| AEP-betrouwbaarheidsversie | Mobiele kernversie | Instructie installeren |
| --------------------- | ------------------- | ------------------- |
| response-native-avoldoende voor v2.x.x | [&#x200B; reactie-inheems-acpcore &#x200B;](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| response-native-garantie v3.x.x | [&#x200B; reactie-inheems-apcore &#x200B;](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

Als u `react-native-acpcore` gebruikt met Verzekering, kan de toepassing van React Native met één van de volgende foutenmeldingen niet bouwen:

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

of

```
AppDelegate: AEPAssurance.h file not found
```

**Oplossing**

Als dat gebeurt, verlaagt u de `react-native-aepassurance` met de volgende npm-opdracht:

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

Deze fout komt voor omdat de `react-native-acpcore` uitbreiding **slechts** compatibel met `react-native-aepassurance` versies 2.x.x en hieronder is.
