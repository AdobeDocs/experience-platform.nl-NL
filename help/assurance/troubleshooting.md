---
title: Handleiding voor probleemoplossing in Adobe Experience Platform Assurance
description: Dit document bevat oplossingen voor algemene problemen bij het gebruik van Adobe Experience Platform Assurance.
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# Problemen met Adobe Experience Platform Assurance oplossen

Als u problemen ondervindt met het verkrijgen van de garantie voor uw werk, raadpleegt u de suggesties onder de volgende onderwerpen over kwesties die u vaak tegenkomt.

Om een soepele implementatie mogelijk te maken en mogelijke problemen te ontdekken, zorgt u ervoor dat SDK-registratie per [Foutopsporingsregistratie inschakelen](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) in de sectie Aan de slag.

U kunt de SDK-logniveaus wijzigen met de [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API.

## Problemen met toepassingen op apparaten

### QR-code opent app niet

* Open de koppeling rechtstreeks. De koppeling kopiëren vanuit **Sessiegegevens**. Plak het in de adresbalk van de browser van het apparaat om het te openen. Als het niet wordt geopend, raadpleegt u de sectie [De app opent de koppeling niet](#app-does-not-open-link).
* Gebruik een andere QR-lezer. Voor iOS 11 of hoger gebruikt u de Foto-app om de QR-code te lezen.

### De app opent de koppeling niet

* Controleer of de implementatie van de diepe koppeling correct is geconfigureerd in de app.
   * **Android:** Diepe koppelingen (App-koppelingen)
      * [Diepe koppelingen naar toepassingscontext maken](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** Aangepast URL-schema of universele koppelingen
      * [Een aangepast URL-schema voor uw app definiëren](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [Universele koppelingen in uw app ondersteunen](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>Voor Android: `startSession` API hoeft niet expliciet te worden aangeroepen. Gebruik voor iOS de API zoals beschreven in [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### Er wordt een verificatiebedekking weergegeven, maar de toepassing kan geen verbinding maken

* Zorg voor internetverbinding van het apparaat via de webbrowser van het apparaat.
* Als de app nooit verbinding heeft gemaakt met de Betrouwbaarheidsservice, moet u controleren of deze correct is ingesteld voor Betrouwbaarheid. Zie de instructies voor het installeren van de [Adobe Experience Platform Assurance](./tutorials/implement-assurance.md) SDK-bibliotheek.
* Controleer of de sessie overeenkomt met de koppeling en of deze correct is ingevoerd voor de verwachte sessie. Zie [Logbericht &quot;OrgID information is not available&quot;](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) (dit komt alleen voor als u toegang hebt tot meer dan één ORG-instantie).

### Foutopsporing in Adobe Analytics

**Status naverwerking - Geen foutopsporingsvlag**

Als gebeurtenissen in de weergave Analytics Events de status &quot;No Debug Flag&quot; (Geen foutopsporingsvlag na verwerking) in de weergave Analytics Events niet worden gebruikt, wordt de functie Analytics Debugging (Foutopsporing na verwerking) mogelijk niet ondersteund door de huidige versie van Adobe Analytics of Assurance SDK.
Upgrade de Adobe Analytics- en Assurance SDK-extensies naar de meest recente versies om dit probleem op te lossen.

| Vereiste minimumversie | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Betrouwbaarheid | > 1.0.0 | > 1.0.0 |

### Native MobileCore- en AEPAssurance-compatibiliteit Reageren

| AEP-betrouwbaarheidsversie | Mobiele kernversie | Instructie installeren |
| --------------------- | ------------------- | ------------------- |
| response-native-avoldoende voor v2.x.x | [native-acpcore reageren](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| response-native-garantie v3.x.x | [native-epcore reageren](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

Als u `react-native-acpcore` Met de Verzekering, kan de React inheemse toepassing er niet in slagen om met één van de volgende foutenmeldingen te bouwen:

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

of

```
AppDelegate: AEPAssurance.h file not found
```

**Oplossing**

Als dat het geval is, gelieve uw te degraderen `react-native-aepassurance` met de volgende npm-opdracht:

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

Deze fout treedt op omdat `react-native-acpcore` extensie is **alleen** compatibel met `react-native-aepassurance` versies 2.x.x en lager.
