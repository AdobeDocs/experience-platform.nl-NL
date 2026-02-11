---
audience: user
solution: Data Collection
user-guide-title: Dataverzameling
breadcrumb-title: Dataverzameling
user-guide-description: Leer hoe u gegevens naar Adobe Experience Platform verzendt.
feature: Data Collection
role: Developer
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 14%

---


# Dataverzameling {#collection}

+ [Overzicht](home.md)
+ [Machtigingen](permissions.md)
+ BrightScript {#brightscript}
   + [Overzicht van BrightScript](brightscript/brs-overview.md)
+ JavaScript {#js}
   + [Web SDK JavaScript - overzicht](js/js-overview.md)
   + [Aanvullende informatie](js/release-notes.md)
   + Installatie {#install}
      + [Installatieoverzicht](js/install/overview.md)
      + [Basiscode](js/install/base-code.md)
      + [Bibliotheek](js/install/library.md)
      + [NPM](js/install/npm.md)
      + [Aangepaste build](js/install/create-custom-build.md)
   + Opdrachten {#commands}
      + [appendIdentityToUrl](js/commands/appendidentitytourl.md)
      + [applyProposities](js/commands/applypropositions.md)
      + [applyResponse](js/commands/applyresponse.md)
      + vormen {#configure}
         + [Overzicht](js/commands/configure/overview.md)
         + [autoCollectPropositionInteractions](js/commands/configure/autocollectpropositioninteractions.md)
         + [clickCollection](js/commands/configure/clickcollection.md)
         + [clickCollectionEnabled](js/commands/configure/clickcollectionenabled.md)
         + [context](js/commands/configure/context.md)
         + [gesprek](js/commands/configure/conversation.md)
         + [datastreamId](js/commands/configure/datastreamid.md)
         + [debugEnabled](js/commands/configure/debugenabled.md)
         + [defaultConsent](js/commands/configure/defaultconsent.md)
         + [downloadLinkQualifier](js/commands/configure/downloadlinkqualifier.md)
         + [edgeBasePath](js/commands/configure/edgebasepath.md)
         + [edgeConfigOverrides](js/commands/configure/edgeconfigoverrides.md)
         + [edgeDomain](js/commands/configure/edgedomain.md)
         + [idMigrationEnabled](js/commands/configure/idmigrationenabled.md)
         + [onBeforeEventSend](js/commands/configure/onbeforeeventsend.md)
         + [onBeforeLinkClickSend](js/commands/configure/onbeforelinkclicksend.md)
         + [orgId](js/commands/configure/orgid.md)
         + [prehideStyle](js/commands/configure/prehidingstyle.md)
         + [pushNotifications](js/commands/configure/pushnotifications.md)
         + [streamingMedia](js/commands/configure/streamingmedia.md)
         + [targetMigrationEnabled](js/commands/configure/targetmigrationenabled.md)
         + [thirdPartyCookiesEnabled](js/commands/configure/thirdpartycookiesenabled.md)
      + [createMediaSession](js/commands/createmediasession.md)
      + [getIdentity](js/commands/getidentity.md)
      + [getLibraryInfo](js/commands/getlibraryinfo.md)
      + [getMediaAnalyticsTracker](js/commands/getmediaanalyticstracker.md)
      + sendEvent {#sendevent}
         + [Overzicht](js/commands/sendevent/overview.md)
         + [data](js/commands/sendevent/data.md)
         + [documentUnloading](js/commands/sendevent/documentunloading.md)
         + [edgeConfigOverrides](js/commands/sendevent/edgeconfigoverrides.md)
         + [eventType](js/commands/sendevent/eventtype.md)
         + [personalisatie](js/commands/sendevent/personalization.md)
         + [renderDecisions](js/commands/sendevent/renderdecisions.md)
         + [xdm](js/commands/sendevent/xdm.md)
      + [sendMediaEvent](js/commands/sendmediaevent.md)
      + [sendPushSubscription](js/commands/sendpushsubscription.md)
      + [setConsent](js/commands/setconsent.md)
      + [setDebug](js/commands/setdebug.md)
      + [subscribeRulesetItems](js/commands/subscriberulesetitems.md)
      + [Opdrachtreacties](js/commands/command-responses.md)
   + [Haken controleren](js/monitoring-hooks.md)
   + [Veelgestelde vragen](js/faq.md)
+ Tags voor JavaScript op de client {#tags}
   + [Overzicht](tags/overview.md)
   + [buildInfo](tags/buildinfo.md)
   + [bedrijf](tags/company.md)
   + [_container](tags/container.md)
   + [koekje](tags/cookie.md)
   + [milieu](tags/environment.md)
   + [getVar](tags/getvar.md)
   + [getVisitorId](tags/getvisitorid.md)
   + [registreerapparaat](tags/logger.md)
   + [_monitors](tags/monitors.md)
   + [setDebug](tags/setdebug.md)
   + [setVar](tags/setvar.md)
   + [track](tags/track.md)
+ Gebruiksscenario’s {#use-cases}
   + [Overzicht](use-cases/overview.md)
   + [Clienttips](use-cases/client-hints.md)
   + [Status client](use-cases/client-state.md)
   + [Commerciële gegevens verzamelen](use-cases/collect-commerce-data.md)
   + [Een CSP configureren](use-cases/configuring-a-csp.md)
   + [Foutopsporing](use-cases/debugging.md)
   + [Gebeurtenisdeduplicatie](use-cases/event-duplication.md)
   + Identiteit {#identity}
      + [Overzicht](use-cases/identity/id-overview.md)
      + [Apparaat-id&#39;s van eerste partij](use-cases/identity/first-party-device-ids.md)
      + [ID delen](use-cases/identity/id-sharing.md)
   + [Meerdere SDK-instanties](use-cases/multiple-instances.md)
   + Personalisatie {#personalization}
      + [Overzicht](use-cases/personalization/pers-overview.md)
      + [Gebeurtenissen weergeven](use-cases/personalization/display-events.md)
      + [flikkering beheren](use-cases/personalization/manage-flicker.md)
      + [Aangepaste inhoud renderen](use-cases/personalization/rendering-personalization-content.md)
      + [Gebeurtenissen van de bovenste en onderste pagina](use-cases/personalization/top-bottom-page-events.md)
