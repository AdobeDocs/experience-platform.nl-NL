---
product: experience-platform
audience: user
user-guide-title: Help-systeem voor Experience Data Model (XDM)
breadcrumb-title: Handleiding Experience Data Model (XDM)
user-guide-description: Gebruik XDM-klassen (Experience Data Model) en -mixen om ervaringsgegevens te standaardiseren.
feature: Schemas
translation-type: tm+mt
source-git-commit: 4a67bcbd2a1458ae47ba64fe2647da442fdf4695
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 6%

---


# Systeem {#xdm} van de Gegevens van de ervaring Model (XDM)

* [XDM System, overzicht](home.md)
* Schemas {#schema}
   * [Basisbeginselen van de schemacompositie](schema/composition.md)
   * [Aanbevolen procedures voor gegevensmodellering](schema/best-practices.md)
   * [Beperkingen voor XDM-veldtypen](schema/field-constraints.md)
   * [XDM-veldwoordenboek](schema/field-dictionary.md)
* Klassen {#classes}
   * [Afzonderlijk XDM-profiel](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
   * [Segmentdefinitie](./classes/segment-definition.md)
* Mixins {#mixins}
   * Profielmixen {#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [Demografische details](./mixins/profile/person-details.md)
      * [Persoonlijke contactgegevens](./mixins/profile/personal-details.md)
      * [Details segmentlidmaatschap](./mixins/profile/segmentation.md)
      * [Contactgegevens werken](./mixins/profile/work-details.md)
   * Gebeurtenismixen {#event}
      * [Gegevens van eindgebruiker](./mixins/event/enduserids.md)
      * [Omgevingsdetails](./mixins/event/environment-details.md)
   * [Updates van Mixernamen](./mixins/name-updates.md)
* Datatypen {#data-types}
   * [Toepassing](./data-types/application.md)
   * [Beacon](./data-types/beacon.md)
   * [Browserdetails](./data-types/browser-details.md)
   * [Commerce](./data-types/commerce.md)
   * [Inhoud en voorkeuren](./data-types/consents.md)
   * [Apparaat](./data-types/device.md)
   * [E-mailadres](./data-types/email-address.md)
   * [Omgeving](./data-types/environment.md)
   * [Geo](./data-types/geo.md)
   * [Geo Circle](./data-types/geo-circle.md)
   * [Geo-coördinaten](./data-types/geo-coordinates.md)
   * [Gegevens over geointeractie](./data-types/geo-interaction-details.md)
   * [Geo-vorm](./data-types/geo-shape.md)
   * [Identiteit](./data-types/identity.md)
   * [Meetlat](./data-types/measure.md)
   * [Volgorde](./data-types/order.md)
   * [Betalingsobject](./data-types/payment-item.md)
   * [Persoon](./data-types/person.md)
   * [Naam persoon](./data-types/person-name.md)
   * [Telefoonnummer](./data-types/phone-number.md)
   * [Context plaatsen](./data-types/place-context.md)
   * [Details van POI](./data-types/poi-details.md)
   * [POI-interactie](./data-types/poi-interaction.md)
   * [Postadres](./data-types/postal-address.md)
   * [Zoeken](./data-types/search.md)
   * [Abonnement](./data-types/subscription.md)
   * [Webinteractie](./data-types/web-interactions.md)
   * [Webpaginadetails](./data-types/webpage-details.md)
* [!UICONTROL Schemas] Gebruikersinterface {#ui}
   * [Overzicht](./ui/overview.md)
   * [XDM-bronnen verkennen](./ui/explore.md)
   * Bronnen maken en bewerken {#resources}
      * [Schemas](./ui/resources/schemas.md)
      * [Klassen](./ui/resources/classes.md)
      * [Mixins](./ui/resources/mixins.md)
      * [Datatypen](./ui/resources/data-types.md)
   * Veld {#fields} definiëren
      * [Overzicht](./ui/fields/overview.md)
      * [Vereiste velden](./ui/fields/required.md)
      * [Objectvelden](./ui/fields/object.md)
      * [Arrayvelden](./ui/fields/array.md)
      * [Enumvelden](./ui/fields/enum.md)
      * [Identiteitsvelden](./ui/fields/identity.md)
      * [Relatievelden](./ui/fields/relationship.md)
   * [Voorbeeld-XDM-gegevens genereren](./ui/sample.md)
   * [XDM-schema&#39;s exporteren](./ui/export.md)
* Schema Registry API {#api}
   * [Overzicht](api/overview.md)
   * [Aan de slag](api/getting-started.md)
   * [Schemas](api/schemas.md)
   * [Gedrag](api/behaviors.md)
   * [Klassen](api/classes.md)
   * [Mixins](api/mixins.md)
   * [Datatypen](api/data-types.md)
   * [Beschrijvers](api/descriptors.md)
   * [Unies](api/unions.md)
   * [Exporteren/importeren](api/export-import.md)
   * [Voorbeeldgegevens](api/sample-data.md)
   * [Controlelogboek](api/audit-log.md)
   * [Ad-hocregelingen](api/ad-hoc.md)
   * [Aanhangsel](api/appendix.md)
* Tutorials {#tutorials}
   * [Een schema maken (UI)](tutorials/create-schema-ui.md)
   * [Een schema maken (API)](tutorials/create-schema-api.md)
   * [Bepaal een verband tussen twee schema&#39;s (UI)](tutorials/relationship-ui.md)
   * [Een relatie definiëren tussen twee schema&#39;s (API)](tutorials/relationship-api.md)
   * [Een ad-hocschema (API) maken](tutorials/ad-hoc.md)
* [Handleiding voor probleemoplossing](troubleshooting-guide.md)
* [API-referentie](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [Opmerkingen bij de release Platform](https://www.adobe.com/go/platform-release-notes-en)