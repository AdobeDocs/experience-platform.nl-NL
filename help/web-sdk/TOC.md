---
solution: Data Collection
audience: user
user-guide-title: Adobe Experience Platform Web SDK Help
breadcrumb-title: Handleiding voor Web SDK
user-guide-description: Interactie met Experience Cloud-services via het Edge-netwerk.
feature: Web SDK
role: Developer
source-git-commit: 7231d3a5ad9553707392c32004d02e355e3c919f
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 19%

---


# Adobe Experience Platform Web SDK {#web-sdk}

* [Overzicht van Web SDK](home.md)
* [Aanvullende informatie](release-notes.md)
* Web SDK-installatie {#install}
   * [Overzicht](install/overview.md)
   * [De SDK van het web installeren met de tagextensie](install/extension.md)
   * [De SDK van het web installeren met de JavaScript-bibliotheek](install/library.md)
   * [De SDK van het web installeren met behulp van het NPM-pakket](install/npm.md)
* Opdrachten {#commands}
   * configure {#configure}
      * [Overzicht](commands/configure/overview.md)
      * [autoTrackPropositionInteractionsEnabled](commands/configure/autotrackpropositioninteractionsenabled.md)
      * [clickCollectionEnabled](commands/configure/clickcollectionenabled.md)
      * [clickCollection](commands/configure/clickcollection.md)
      * [context](commands/configure/context.md)
      * [datastreamId](commands/configure/datastreamid.md)
      * [debugEnabled](commands/configure/debugenabled.md)
      * [defaultConsent](commands/configure/defaultconsent.md)
      * [downloadLinkQualifier](commands/configure/downloadlinkqualifier.md)
      * [edgeBasePath](commands/configure/edgebasepath.md)
      * [edgeDomain](commands/configure/edgedomain.md)
      * [idMigrationEnabled](commands/configure/idmigrationenabled.md)
      * [streamingMedia](commands/configure/streamingmedia.md)
      * [onBeforeEventSend](commands/configure/onbeforeeventsend.md)
      * [onBeforeLinkClickSend](commands/configure/onbeforelinkclicksend.md)
      * [orgId](commands/configure/orgid.md)
      * [prehideStyle](commands/configure/prehidingstyle.md)
      * [targetMigrationEnabled](commands/configure/targetmigrationenabled.md)
      * [thirdPartyCookiesEnabled](commands/configure/thirdpartycookiesenabled.md)
   * sendEvent {#sendevent}
      * [Overzicht](commands/sendevent/overview.md)
      * [data](commands/sendevent/data.md)
      * [documentUnloading](commands/sendevent/documentunloading.md)
      * [personalisatie](commands/sendevent/personalization.md)
      * [renderDecisions](commands/sendevent/renderdecisions.md)
      * [type](commands/sendevent/type.md)
      * [xdm](commands/sendevent/xdm.md)
   * [appendIdentityToUrl](commands/appendidentitytourl.md)
   * [applyProposities](commands/applypropositions.md)
   * [applyResponse](commands/applyresponse.md)
   * [createMediaSession](commands/createmediasession.md)
   * [getIdentity](commands/getidentity.md)
   * [getLibraryInfo](commands/getlibraryinfo.md)
   * [getMediaAnalyticsTracker](commands/getmediaanalyticstracker.md)
   * [setConsent](commands/setconsent.md)
   * [setDebug](commands/setdebug.md)
   * [sendMediaEvent](commands/sendmediaevent.md)
   * [subscribeRulesetItems](commands/subscriberulesetitems.md)
   * [Gegevensstroomoverschrijvingen configureren](commands/datastream-overrides.md)
   * [Opdrachtreacties](commands/command-responses.md)

* Identiteit {#identity}
   * [Overzicht](identity/overview.md)
   * [Apparaat-id&#39;s van eerste partij](identity/first-party-device-ids.md)
   * [Id&#39;s delen via mobiel naar web en verschillende domeinen](identity/id-sharing.md)

* Personalisatie {#personalization}
   * [Weergavegebeurtenissen beheren](personalization/display-events.md)
   * [Aangepaste inhoud renderen](personalization/rendering-personalization-content.md)
   * [Personalization via hybride implementatie](personalization/hybrid-personalization.md)
   * [flikkering beheren](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [Overzicht](personalization/adobe-target/target-overview.md)
      * [Implementatie van één pagina](personalization/adobe-target/spa-implementation.md)
      * [Toegang krijgen tot reactietokens](personalization/adobe-target/accessing-response-tokens.md)
      * [Dbox-id van derden gebruiken](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [Het vergelijken van de bibliotheek at.js met het Web SDK](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Analytics for Target (A4T) logging {#a4t}
         * [Overzicht](personalization/adobe-target/analytics-logging/overview.md)
         * [Logboekregistratie op de client](personalization/adobe-target/analytics-logging/client-side.md)
         * [Logboekregistratie op de server](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer decisioning {#offer-decisioning}
      * [Overzicht](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [Overzicht](personalization/ajo/overview.md)
      * [Implementatie van één pagina](personalization/ajo/web-spa-implementation.md)
      * [Ondersteuning voor Web In-app Messaging in Web SDK configureren](personalization/web-in-app-messaging.md)

* Toestemming {#consent}
   * IAB Transparency and Consent Framework 2.0 {#iab-tcf}
      * [Overzicht](consent/iab-tcf/overview.md)
      * [Integreren met tags](consent/iab-tcf/with-tags.md)
      * [Integreren zonder tags](consent/iab-tcf/without-tags.md)

* Gebruiksscenario’s {#use-cases}
   * [Overzicht](use-cases/overview.md)
   * [Gegevens naar Adobe Analytics verzenden met de Web SDK](use-cases/adobe-analytics.md)
   * [Client-tips voor gebruikersagent](use-cases/client-hints.md)
   * [Commerciële gegevens verzamelen](use-cases/collect-commerce-data.md)
   * [Een CSP configureren](use-cases/configuring-a-csp.md)
   * [Foutopsporingsmethoden](use-cases/debugging.md)
   * [Meerdere Web SDK-instanties gebruiken](use-cases/multiple-instances.md)
   * [Gebeurtenissen voor de bovenste en onderste pagina configureren](use-cases/top-bottom-page-events.md)
* [Haken controleren](monitoring-hooks.md)
* [Veelgestelde vragen](faq.md)
* [Bronnen](resources.md)
