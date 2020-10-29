---
product: experience-platform
audience: user
user-guide-title: Help-systeem voor Experience Data Model (XDM)
breadcrumb-title: Handleiding gegevensmodel (XDM)
user-guide-description: Gebruik XDM-klassen (Experience Data Model) en -mixen om ervaringsgegevens te standaardiseren.
translation-type: tm+mt
source-git-commit: 0a5b6bab6a0a11a572a4cd5de95b33f8d61d34bc
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 2%

---


# XDM-systeem (Experience Data Model) {#xdm}

* [XDM System, overzicht](home.md)
* Schemas {#schema}
   * [Basisbeginselen van de schemacompositie](schema/composition.md)
   * [Aanbevolen procedures voor gegevensmodellering](schema/best-practices.md)
   * [Beperkingen voor XDM-veldtypen](schema/field-constraints.md)
   * [XDM-veldwoordenboek](schema/field-dictionary.md)
   * Gebruiksgevallen voor schema {#use-cases}
      * [Toevoeging privacy, mix](schema/privacy-consent.md)
* Klassen {#classes}
   * [Afzonderlijk XDM-profiel](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
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
   * [Beacon](./data-types/beacon.md)
   * [Browserdetails](./data-types/browser-details.md)
   * [Apparaat](./data-types/device.md)
   * [E-mailadres](./data-types/email-address.md)
   * [Omgeving](./data-types/environment.md)
   * [Geo](./data-types/geo.md)
   * [Geo Circle](./data-types/geo-circle.md)
   * [Geo-coördinaten](./data-types/geo-coordinates.md)
   * [Gegevens over geointeractie](./data-types/geo-interaction-details.md)
   * [Geo-vorm](./data-types/geo-shape.md)
   * [Identiteit](./data-types/identity.md)
   * [Naam persoon](./data-types/person-name.md)
   * [Telefoonnummer](./data-types/phone-number.md)
   * [Context plaatsen](./data-types/place-context.md)
   * [Details van POI](./data-types/poi-details.md)
   * [POI-interactie](./data-types/poi-interaction.md)
   * [Postadres](./data-types/postal-address.md)
* Schema-register-API {#api}
   * [Aan de slag](api/getting-started.md)
   * [Bronnen weergeven](api/list-resources.md)
   * [Een resource opzoeken](api/look-up-resource.md)
   * [Een bron bijwerken](api/update-resource.md)
   * [Een bron vervangen](api/replace-resource.md)
   * [Een bron verwijderen](api/delete-resource.md)
   * [Een klasse maken](api/create-class.md)
   * [Een mix maken](api/create-mixin.md)
   * [Een gegevenstype maken](api/create-data-type.md)
   * [Een schema maken](api/create-schema.md)
   * [Unies](api/unions.md)
   * [Beschrijvers](api/descriptors.md)
   * [Ad-hocregelingen](api/ad-hoc.md)
   * [Aanhangsel](api/appendix.md)
* Tutorials {#tutorials}
   * [Een schema maken (API)](tutorials/create-schema-api.md)
   * [Een schema maken (UI)](tutorials/create-schema-ui.md)
   * [Een relatie definiëren tussen twee schema&#39;s (API)](tutorials/relationship-api.md)
   * [Bepaal een verband tussen twee schema&#39;s (UI)](tutorials/relationship-ui.md)
   * [Een ad-hocschema (API) maken](tutorials/ad-hoc.md)
* [Handleiding voor probleemoplossing](troubleshooting-guide.md)
* [API-referentie](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [Opmerkingen bij de release Platform](https://www.adobe.com/go/platform-release-notes-en)