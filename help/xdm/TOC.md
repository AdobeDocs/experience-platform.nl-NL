---
audience: user
user-guide-title: Experience Data Model (XDM) System Help
breadcrumb-title: Handleiding voor Experience Data Model (XDM)
user-guide-description: Verken een overzicht van het systeem van Experience Data Model (XDM) binnen het Experience Platform en leer hoe u klassen en schemaveldgroepen kunt gebruiken om ervaringsgegevens te standaardiseren.
feature: Schemas
role: Developer
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 8%

---


# XDM-systeem (Experience Data Model) {#xdm}

* [XDM System, overzicht](home.md)
* Schemas {#schema}
   * [Basisbeginselen van de schemacompositie](schema/composition.md)
   * [Aanbevolen procedures voor gegevensmodellering](schema/best-practices.md)
   * [Gevoelige en persoonlijke gegevens](./schema/sensitive-and-personal-data.md)
   * [Beperkingen voor XDM-veldtypen](schema/field-constraints.md)
   * [Naamruimte in XDM](./schema/namespaces.md)
   * Industriële gegevensmodellen {#industries}
      * [Overzicht](./schema/industries/overview.md)
      * [Detailhandel](./schema/industries/retail.md)
      * [Financiële diensten](./schema/industries/financial.md)
      * [Gezondheidszorg](./schema/industries/healthcare.md)
      * [Telecommunicatie](./schema/industries/telecom.md)
      * [Reizen en gastvrijheid](./schema/industries/travel-hospitality.md)
   * Gegevensmodel gezondheidszorg V2 {#healthcare}
      * [Gezondheidszorg V2](./schema/healthcare/healthcare-v2.md)
      * Klassen {#classes}
         * [Locatie](./schema/healthcare/classes/location.md)
      * Veldgroepen {#field-groups}
         * [Account](./schema/healthcare/field-groups/account.md)
         * [Aanstelling](./schema/healthcare/field-groups/appointment.md)
         * [Zorgplan](./schema/healthcare/field-groups/care-plan.md)
         * [Dekking](./schema/healthcare/field-groups/coverage.md)
         * [Goal](./schema/healthcare/field-groups/goal.md)
         * [Immunisatie](./schema/healthcare/field-groups/immunization.md)
         * [Locatie](./schema/healthcare/field-groups/location.md)
         * [Geneesmiddelen](./schema/healthcare/field-groups/medication.md)
         * [Geneesmiddelenverlies](./schema/healthcare/field-groups/medication-dispense.md)
         * [Aanvraag voor geneesmiddelen](./schema/healthcare/field-groups/medication-request.md)
         * [Organisatie](./schema/healthcare/field-groups/organization.md)
         * [Patiënt](./schema/healthcare/field-groups/patient.md)
         * [Praktijkster](./schema/healthcare/field-groups/practioner.md)
         * [ Programma ](./schema/healthcare/field-groups/schedule.md)
      * Gegevenstypen {#data-types}
         * [Adres](./schema/healthcare/data-types/address.md)
         * [Aantekening](./schema/healthcare/data-types/annotation.md)
         * [Beschikbaarheid](./schema/healthcare/data-types/availability.md)
         * [Codeable Concept](./schema/healthcare/data-types/codeable-concept.md)
         * [Codeerbare referentie](./schema/healthcare/data-types/codeable-reference.md)
         * [Codering](./schema/healthcare/data-types/coding.md)
         * [Contactpunt](./schema/healthcare/data-types/contact-point.md)
         * [Dosering](./schema/healthcare/data-types/dosage.md)
         * [Duur](./schema/healthcare/data-types/duration.md)
         * [Uitgebreide contactgegevens](./schema/healthcare/data-types/extended-contact-detail.md)
         * [Menselijke naam](./schema/healthcare/data-types/human-name.md)
         * [Id](./schema/healthcare/data-types/identifier.md)
         * [Geld](./schema/healthcare/data-types/money.md)
         * [Periode](./schema/healthcare/data-types/period.md)
         * [Persoon](./schema/healthcare/data-types/person.md)
         * [Aantal](./schema/healthcare/data-types/quantity.md)
         * [Bereik](./schema/healthcare/data-types/range.md)
         * [Verhouding](./schema/healthcare/data-types/ratio.md)
         * [Referentie](./schema/healthcare/data-types/reference.md)
         * [Herhalen](./schema/healthcare/data-types/repeat.md)
         * [Eenvoudig aantal](./schema/healthcare/data-types/simple-quantity.md)
         * [Timing](./schema/healthcare/data-types/timing.md)
         * [Virtuele service](./schema/healthcare/data-types/virtual-service-detail.md)
   * [XDM-veldwoordenboek](schema/field-dictionary.md)
* Klassen {#classes}
   * [Afzonderlijk XDM-profiel](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
   * [Geneesmiddelen](./classes/medication.md)
   * [Payer](./classes/payer.md)
   * [Plan](./classes/plan.md)
   * [Beleid](./classes/policy.md)
   * [Product](./classes/product.md)
   * [Perspectief](./classes/prospect.md)
   * [Provider](./classes/provider.md)
   * [Segmentdefinitie](./classes/segment-definition.md)
   * B2B-klassen {#b2b}
      * [XDM Business Account](./classes/b2b/business-account.md)
      * [XDM Zakelijke account Person Relatie](./classes/b2b/business-account-person-relation.md)
      * [XDM Business Campaign](./classes/b2b/business-campaign.md)
      * [XDM Business Campaign-leden](./classes/b2b/business-campaign-members.md)
      * [XDM Business Opportunity](./classes/b2b/business-opportunity.md)
      * [XDM Business Opportunity Person Relatie](./classes/b2b/business-opportunity-person-relation.md)
      * [XDM Business Marketing List](./classes/b2b/business-marketing-list.md)
      * [Leden van XDM Business Marketing List](./classes/b2b/business-marketing-list-members.md)
* Veldgroepen {#field-groups}
   * Afzonderlijk XDM-profiel {#profile}
      * [Inhoud en voorkeuren](./field-groups/profile/consents.md)
      * [Demografische details](./field-groups/profile/demographic-details.md)
      * [Gegevens van het lid in de gezondheidszorg](./field-groups/profile/healthcare-member-details.md)
      * [IAB TCF 2.0 Toestemming](./field-groups/profile/iab.md)
      * [IdentityMap](./field-groups/profile/identitymap.md)
      * [Loyalty-details](./field-groups/profile/loyalty-details.md)
      * [Persoonlijke contactgegevens](./field-groups/profile/personal-contact-details.md)
      * [Verbetering van profielpartner (voorbeeld)](./field-groups/profile/profile-partner-enrichment.md)
      * [Details segmentlidmaatschap](./field-groups/profile/segmentation.md)
      * [Telecom-abonnement](./field-groups/profile/telecom-subscription.md)
      * [Contactgegevens werken](./field-groups/profile/work-contact-details.md)
      * [XDM Business Person-componenten](./field-groups/profile/business-person-components.md)
      * [XDM Business Person - Gegevens](./field-groups/profile/business-person-details.md)
   * Afzonderlijk XDM-perspectiefprofiel {#prospect-profile}
      * [Details partnerperspectief (voorbeeld)](./field-groups/prospect-profile/partner-prospect-details.md)
   * XDM ExperienceEvent {#event}
      * [Adobe Analytics Full Extension](./field-groups/event/analytics-full-extension.md)
      * [Advertising-gegevens](./field-groups/event/advertising-details.md)
      * [Toepassingsdetails](./field-groups/event/application-details.md)
      * [Balansoverdrachten](./field-groups/event/balance-transfers.md)
      * [Boot Detection](./field-groups/event/bot-detection-information.md)
      * [Campagne marketing details](./field-groups/event/campaign-marketing-details.md)
      * [Kaarthandelingen](./field-groups/event/card-actions.md)
      * [Kanaaldetails](./field-groups/event/channel-details.md)
      * [Commerce-gegevens](./field-groups/event/commerce-details.md)
      * [Aanbetalingsgegevens](./field-groups/event/deposit-details.md)
      * [Device Trade-In-details](./field-groups/event/device-trade-in-details.md)
      * [Mijnreservering](./field-groups/event/dining-reservation.md)
      * [Gegevens van eindgebruiker](./field-groups/event/enduserids.md)
      * [Omgevingsdetails](./field-groups/event/environment-details.md)
      * [Vluchtreservering](./field-groups/event/flight-reservation.md)
      * [IAB TCF 2.0 Toestemming](./field-groups/event/iab.md)
      * [Voorbehoud voor indiening](./field-groups/event/lodging-reservation.md)
      * [Interactiegegevens van MediaAnalytics](./field-groups/event/mediaanalytics-interaction.md)
      * [Gegevens prijsaanvraag](./field-groups/event/quote-request-details.md)
      * [Reserveringsdetails](./field-groups/event/reservation-details.md)
      * [Sitetool - details](./field-groups/event/sitetool-details.md)
      * [Zoeken op ondersteuningssite](./field-groups/event/support-site-search.md)
      * [Upgradedetails](./field-groups/event/upgrade-details.md)
      * [Details uploaden](./field-groups/event/upsell-details.md)
      * [Webdetails](./field-groups/event/web-details.md)
   * XDM Business Campaign {#b2b-campaign}
      * [XDM Business Campaign - details](./field-groups/b2b-campaign/details.md)
   * XDM Business Campaign-leden {#b2b-campaign-members}
      * [XDM Business Campaign-leden - Gegevens](./field-groups/b2b-campaign-members/details.md)
   * Medicatie {#medication}
      * [Geneesmiddelen voor gezondheidszorg](./field-groups/medication/healthcare-medication.md)
   * Overzicht {#plan}
      * [Details van het zorgplan](./field-groups/plan/healthcare-plan-details.md)
   * Product {#product}
      * [Productcatalogus](./field-groups/product/product-catalog.md)
      * [Productcategorie](./field-groups/product/product-category.md)
   * Provider {#provider}
      * [Gezondheidszorgverlener](./field-groups/provider/healthcare-provider.md)
   * Gedeeld {#shared}
      * [Details externe Source System Audit](./field-groups/shared/external-source-system-audit-details.md)
   * [Updates van veldgroepnamen](./field-groups/name-updates.md)
* Gegevenstypen {#data-types}
   * [Accountgegevens](./data-types/account-details.md)
   * [Ad Break](./data-types/ad-break.md)
   * [Adres](./data-types/address.md)
   * [Advertising-detailverzameling](./data-types/advertising-details-collection.md)
   * [Advertising Details Reporting](./data-types/advertising-details-reporting.md)
   * [Advertising Pod Details Collection](./data-types/advertising-pod-details-collection.md)
   * [Advertising Pod Details Reporting](./data-types/advertising-pod-details-reporting.md)
   * [Toepassing](./data-types/application.md)
   * [B2B Source](./data-types/b2b-source.md)
   * [Beacon](./data-types/beacon.md)
   * [Browserdetails](./data-types/browser-details.md)
   * [Kar](./data-types/cart.md)
   * [Categoriegegevens](./data-types/category-data.md)
   * [Verzameling hoofdstukdetails](./data-types/chapter-details-collection.md)
   * [Rapportage over details van hoofdstuk](./data-types/chapter-details-reporting.md)
   * [Commerce-bereik](./data-types/commerce-scope.md)
   * [Commerce](./data-types/commerce.md)
   * [Constante tekenreeks](./data-types/consent-string.md)
   * [Inhoud en voorkeuren](./data-types/consents.md)
   * [Valuta](./data-types/currency.md)
   * [Verzameling van aangepaste metagegevens](./data-types/custom-metadata-details-collection.md)
   * [Rapportage van details van aangepaste metagegevens](./data-types/custom-metadata-details-reporting.md)
   * [Apparaat](./data-types/device.md)
   * [E-mailadres](./data-types/email-address.md)
   * [Omgeving](./data-types/environment.md)
   * [Verzameling met foutdetails](./data-types/error-details-collection.md)
   * [Experience Channel](./data-types/experience-channel.md)
   * [Kenmerken externe Source System Audit](./data-types/external-source-system-audit-attributes.md)
   * [Financiële rekening](./data-types/financial-account.md)
   * [Veld voor algemene toestemming](./data-types/consent-field.md)
   * [Algemeen veld Voorkeuren voor marketing met abonnementen](./data-types/marketing-field-subscriptions.md)
   * [Algemeen veld Voorkeuren voor marketing](./data-types/marketing-field.md)
   * [Algemeen Personalization-voorkeurenveld](./data-types/personalization-field.md)
   * [Geo Circle](./data-types/geo-circle.md)
   * [Geo-coördinaten](./data-types/geo-coordinates.md)
   * [Geo-vorm](./data-types/geo-shape.md)
   * [Details van Geo-interactie](./data-types/geo-interaction-details.md)
   * [Geo](./data-types/geo.md)
   * [Identiteit](./data-types/identity.md)
   * [Implementatiedetails](./data-types/implementation-details.md)
   * [Impressies](./data-types/impressions.md)
   * [Zoeken op interne site](./data-types/internal-site-search.md)
   * [Toetswaardenpaar](./data-types/key-value-pair.md)
   * [Lijst met eindverzameling frames](./data-types/list-of-states-end-collection.md)
   * [Lijst met staten die verzameling starten](./data-types/list-of-states-start-collection.md)
   * [Marketing](./data-types/marketing.md)
   * [Meetlat](./data-types/measure.md)
   * [Details van mediagroep](./data-types/media-collection-details.md)
   * [Gebeurtenisgegevens media](./data-types/media-event-information.md)
   * [Rapportgegevens voor media](./data-types/media-reporting-details.md)
   * [Volgorde](./data-types/order.md)
   * [Details van POI](./data-types/poi-details.md)
   * [Interactie tussen POI](./data-types/poi-interaction.md)
   * [Betalingsobject](./data-types/payment-item.md)
   * [Naam persoon](./data-types/person-name.md)
   * [Persoon](./data-types/person.md)
   * [Telefoonnummer](./data-types/phone-number.md)
   * [Context plaatsen](./data-types/place-context.md)
   * [Gegevenrapportage van Player-status](./data-types/player-state-data-reporting.md)
   * [Postadres](./data-types/postal-address.md)
   * [Item in productlijst](./data-types/product-list-item.md)
   * [QoE (Quality of Experience) - Gegevens verzamelen](./data-types/qoe-data-details-collection.md)
   * [Rapportage gegevens QoE-gegevens](./data-types/qoe-data-details-reporting.md)
   * [Object terugbetalen](./data-types/refund-item.md)
   * [Aanvraaglijst](./data-types/requisition-list.md)
   * [Item retourneren](./data-types/return-item.md)
   * [Retourneren](./data-types/return.md)
   * [Zoeken](./data-types/search.md)
   * [Sessiedetails verzamelen](./data-types/session-details-collection.md)
   * [Rapportage over sessiegegevens](./data-types/session-details-reporting.md)
   * [Verzending](./data-types/shipping.md)
   * [Abonnement](./data-types/subscription.md)
   * [Telecom-abonnement](./data-types/telecom-subscription.md)
   * [Transactie](./data-types/transaction.md)
   * [Webinformatie](./data-types/web-information.md)
   * [Webinteractie](./data-types/web-interaction.md)
   * [Webpagina-details](./data-types/webpage-details.md)
* [!UICONTROL Schemas] UI {#ui}
   * [Overzicht](./ui/overview.md)
   * [XDM-bronnen verkennen](./ui/explore.md)
   * Bronnen maken en bewerken {#resources}
      * [Schema&#39;s](./ui/resources/schemas.md)
      * [Klassen](./ui/resources/classes.md)
      * [Veldgroepen](./ui/resources/field-groups.md)
      * [Datatypen](./ui/resources/data-types.md)
   * Velden definiëren {#fields}
      * [Overzicht](./ui/fields/overview.md)
      * [Arrayvelden](./ui/fields/array.md)
      * [Enumvelden](./ui/fields/enum.md)
      * [Identiteitsvelden](./ui/fields/identity.md)
      * [Kaart](./ui/fields/map.md)
      * [Objectvelden](./ui/fields/object.md)
      * [Relatievelden](./ui/fields/relationship.md)
      * [Vereiste velden](./ui/fields/required.md)
   * [Workflows op basis van velden](./ui/field-based-workflows.md)
   * [Machine leren-ondersteund schema maken](./ui/ml-assisted-schema-creation.md)
   * [Voorbeeld-XDM-gegevens genereren](./ui/sample.md)
   * [XDM-schema&#39;s exporteren](./ui/export.md)
* Schemaregister-API {#api}
   * [Overzicht](api/overview.md)
   * [Aan de slag](api/getting-started.md)
   * [Schema&#39;s](api/schemas.md)
   * [Gedrag](api/behaviors.md)
   * [Klassen](api/classes.md)
   * [Schema veldgroepen](api/field-groups.md)
   * [Datatypen](api/data-types.md)
   * [Beschrijvers](api/descriptors.md)
   * [Unies](api/unions.md)
   * [CSV naar schemaomzetting](api/csv-to-schema.md)
   * [Exporteren](api/export.md)
   * [Importeren](api/import.md)
   * [Voorbeeldgegevens](api/sample-data.md)
   * [Controlelogboek](api/audit-log.md)
   * [Ad-hocregelingen](api/ad-hoc.md)
   * [Mixinen (afgekeurd)](api/mixins.md)
   * [Bijlage](api/appendix.md)
* Zelfstudies {#tutorials}
   * [Een schema maken in de gebruikersinterface](tutorials/create-schema-ui.md)
   * [Een schema maken in de API](tutorials/create-schema-api.md)
   * [Specifieke velden toevoegen aan een schema (API)](./tutorials/specific-fields-api.md)
   * [Aangepaste velden definiëren (API)](./tutorials/custom-fields-api.md)
   * [Voorgestelde waarden toevoegen aan een veld (API)](tutorials/suggested-values.md)
   * [Een XDM-veld in de gebruikersinterface verwijderen](tutorials/field-deprecation-ui.md)
   * [Een XDM-veld in de API verwijderen](tutorials/field-deprecation-api.md)
   * [Een schemarelatie definiëren in de gebruikersinterface](tutorials/relationship-ui.md)
   * [Een schemarelatie definiëren in de API](tutorials/relationship-api.md)
   * [Een schemarelatie definiëren in Real-Time CDP B2B edition](tutorials/relationship-b2b.md)
   * [De labels voor gegevensgebruik voor een schema beheren](tutorials/labels.md)
   * [Een ad-hocschema maken](tutorials/ad-hoc.md)
* [Handleiding voor probleemoplossing](troubleshooting-guide.md)
* [ API verwijzing ](https://www.adobe.io/experience-platform-apis/references/schema-registry/)
* [Releaseopmerkingen bij Experience Platform](https://experienceleague.adobe.com/nl/docs/experience-platform/release-notes/latest)
