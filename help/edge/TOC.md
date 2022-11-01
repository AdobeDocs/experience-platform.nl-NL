---
solution: Data Collection
audience: user
user-guide-title: Help bij Adobe Experience Platform Web SDK
breadcrumb-title: Web SDK Guide
user-guide-description: Interactie met de diensten van Experience Cloud door het netwerk van de Rand.
feature: Web SDK
source-git-commit: 15a1fd71bc5f00efdd475abd3385dc6bf4737a17
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 12%

---


# Adobe Experience Platform Web SDK {#edge}

* [Overzicht van Platform Web SDK](home.md)
* Grondbeginselen {#fundamentals}
   * [Ondersteunde gebruiksgevallen](fundamentals/supported-use-cases.md)
   * [Vereisten](fundamentals/prerequisite.md)
   * [De SDK installeren](fundamentals/installing-the-sdk.md)
   * [De SDK configureren](fundamentals/configuring-the-sdk.md)
   * [Opdrachten uitvoeren](fundamentals/executing-commands.md)
   * [Gebeurtenissen bijhouden](fundamentals/tracking-events.md)
   * [Foutopsporing](fundamentals/debugging.md)
   * [Een CSP configureren](fundamentals/configuring-a-csp.md)
   * [Interactie met meerdere eigenschappen](fundamentals/interacting-with-multiple-properties.md)
   * [Client-tips voor gebruikersagent](fundamentals/user-agent-client-hints.md)
* DataStreams {#datastreams}
   * [Overzicht](./datastreams/overview.md)
   * [Een gegevensstroom configureren](./datastreams/configure.md)
   * [Gegevensvoorvoegsel voor gegevensverzameling](./datastreams/data-prep.md)
* Identiteit {#identity}
   * [Overzicht](identity/overview.md)
   * [Apparaat-id&#39;s van eerste partij](identity/first-party-device-ids.md)
   * [Id&#39;s delen via mobiel naar web en verschillende domeinen](identity/id-sharing.md)
* Gegevensverzameling {#data-collection}
   * [Automatisch verzamelde gegevens](data-collection/automatic-information.md)
   * [Koppelingen bijhouden](data-collection/track-links.md)
   * [Gegevens over handel en producten verzamelen](data-collection/collect-commerce-data.md)
   * Adobe Analytics {#adobe-analytics}
      * [Adobe Analytics gebruiken met Platform Web SDK](data-collection/adobe-analytics/analytics-overview.md)
      * [Variabelen van Analyse toewijzen](data-collection/adobe-analytics/manually-mapping-variables.md)
      * [Automatisch toegewezen variabelen](data-collection/adobe-analytics/automatically-mapped-vars.md)
      * [Gegevens verzenden naar Analytics](data-collection/adobe-analytics/sending-data-to-analytics.md)
* Personalisatie {#personalization}
   * [Aangepaste inhoud renderen](personalization/rendering-personalization-content.md)
   * [Personalisatie via hybride implementatie](personalization/hybrid-personalization.md)
   * [flikkering beheren](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [Overzicht](personalization/adobe-target/target-overview.md)
      * [Implementatie van één pagina](personalization/adobe-target/spa-implementation.md)
      * [Toegang krijgen tot reactietokens](personalization/adobe-target/accessing-response-tokens.md)
      * [Dbox-id van derden gebruiken](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [Het vergelijken van de bibliotheek at.js met het Web SDK](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Analyses voor logboekregistratie van doel (A4T) {#a4t}
         * [Overzicht](personalization/adobe-target/analytics-logging/overview.md)
         * [Logboekregistratie op de client](personalization/adobe-target/analytics-logging/client-side.md)
         * [Logboekregistratie op de server](personalization/adobe-target/analytics-logging/server-side.md)
   * offer decisioning {#offer-decisioning}
      * [Overzicht](personalization/offer-decisioning/offer-decisioning-overview.md)
* Toestemming {#consent}
   * [Ondersteunende toestemming](consent/supporting-consent.md)
   * IAB Transparency and Consent Framework 2.0 {#iab-tcf}
      * [Overzicht](consent/iab-tcf/overview.md)
      * [Integreren met tags](consent/iab-tcf/with-launch.md)
      * [Integreren zonder tags](consent/iab-tcf/without-launch.md)
* Web SDK-tagextensie {#extension}
   * [Web SDK-extensie](extension/web-sdk-extension-configuration.md)
   * [Gebeurtenistypen](extension/event-types.md)
   * [Typen handelingen](extension/action-types.md)
   * [Gegevenstelelementtypen](extension/data-element-types.md)
   * [Toegang tot de ECID](extension/accessing-the-ecid.md)
   * [Opmerkingen bij de release Web SDK](extension/web-sdk-ext-release-notes.md)
* [Aanvullende informatie](release-notes.md)
* [Veelgestelde vragen](web-sdk-faq.md)
* [Bronnen](resources.md)
