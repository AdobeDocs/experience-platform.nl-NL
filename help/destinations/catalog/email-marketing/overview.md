---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen
title: Overzicht van e-mailmarketingdoelen
type: Tutorial
description: Met e-mailserviceproviders (ESP's) kunt u uw marketingactiviteiten voor e-mail beheren, bijvoorbeeld voor het verzenden van promotionele e-mailcampagnes. Leer welke ESP's worden ondersteund als Experience Platform-doelen.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 1%

---

# Overzicht van e-mailmarketingdoelen {#email-marketing-destinations}

## Overzicht {#overview}

Met e-mailserviceproviders (ESP&#39;s) kunt u uw marketingactiviteiten voor e-mail beheren, zoals het verzenden van promotionele e-mailcampagnes. Adobe Experience Platform integreert met ESP&#39;s door het publiek te activeren naar marketingbestemmingen via e-mail.

## Ondersteunde e-mailmarketingdoelen {#supported-destinations}

Adobe Experience Platform ondersteunt de volgende e-mailmarketingdoelen:

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [Mailchimp-rentecategorieën](mailchimp-interest-categories.md)
* [Mailchimp-tags](mailchimp-tags.md)
* [(API) Oracle Eloqua](oracle-eloqua-api.md)
* [ (API)  [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud-exact-target.md)
* [(Bestanden) Oracle Eloqua](oracle-eloqua.md)
* [(Bestanden) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud.md)
* [[!DNL Salesforce Marketing Cloud Account Engagement]](salesforce-marketing-cloud-account-engagement.md)
* [Oracle Responsys](oracle-responsys.md)
* [SendGrid](sendgrid.md)

## Verbinding maken met een nieuwe marketingbestemming voor e-mail {#connect-destination}

Experience Platform moet eerst verbinding maken met het doel om een publiek naar marketingbestemmingen voor uw campagnes te sturen. Zie het [ leerprogramma van de bestemmingsverwezenlijking ](../../ui/connect-destination.md) voor gedetailleerde informatie bij vestiging een nieuwe bestemming.

## Tips en trucs bij het activeren van het publiek naar marketingbestemmingen via e-mail {#best-practices}

### Identiteitsselectie {#identity}

Adobe adviseert dat u een uniek herkenningsteken van uw [ verenigingsschema ](../../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Dit is het veld waarvan de gebruikers-id&#39;s zijn weggefilterd. Meestal is dit veld het e-mailadres, maar het kan ook een id voor een loyaliteitsprogramma of een telefoonnummer zijn. Raadpleeg de onderstaande tabel voor de meest gangbare unieke id&#39;s en hun XDM-veld in het schema.

| Unieke id | XDM-veld in Unified Schema |
|----------------- | ---------------------------|
| E-mailadres | `personalEmail.address` |
| Telefoon | `mobilePhone.number` |
| ID Loyalty-programma | `Customer-defined XDM field` |

{style="table-layout:auto"}

### Andere doelkenmerken {#other-destination-attributes}

Kies in de keuzelijst Schema welke andere velden u naar de e-mailbestemming wilt exporteren. Enkele aanbevolen opties zijn:

| Schema | XDM-veld |
|------ | ---------|
| Voornaam | `person.name.firstName` |
| Achternaam | `person.name.lastName` |
| Telefoon | `mobilePhone.number` |
| Plaats adres | `homeAddress.city` |
| Adresstatus | `homeAddress.stateProvince` |
| Postcode adres | `homeAddress.postalCode` |
| Geboortedatum | `person.birthDayAndMonth` |
| Segmentlidmaatschap | `segmentMembership.status` |

{style="table-layout:auto"}

## Soorten publiek naar marketingdoelen e-mailen {#activate}

Sommige e-mailmarketingdoelen in de catalogus exporteren profielen op streamingwijze, via API-integratie met de bestemming.

Andere doelen exporteren bestanden naar een locatie voor cloudopslag. Nadat het exporteren is voltooid, moet u gegevens importeren van de opslaglocatie van de cloud naar uw marketingbestemming voor e-mail.

Volg de verbindingen in de [ gesteunde e-mail marketing bestemmingen ](#supported-destinations) sectie leren hoe te om publiek aan elke e-mail marketing bestemming te activeren.

## Aanvullende bronnen {#additional-resources}

* [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md)
* [E-mailmarketingdoelen maken en gegevens activeren met de Flow Service API](../../api/connect-activate-batch-destinations.md)
