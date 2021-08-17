---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen
title: Overzicht van e-mailmarketingdoelen
type: Tutorial
description: Met e-mailserviceproviders (ESP's) kunt u uw marketingactiviteiten voor e-mail beheren, bijvoorbeeld voor het verzenden van promotionele e-mailcampagnes.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 2%

---

# Overzicht van e-mailmarketingdoelen {#email-marketing-destinations}

## Overzicht {#overview}

Met e-mailserviceproviders (ESP&#39;s) kunt u uw marketingactiviteiten voor e-mail beheren, zoals het verzenden van promotionele e-mailcampagnes. Adobe Experience Platform integreert met ESPs door u toe te staan om segmenten aan e-mail marketing bestemmingen te activeren.

Platform exporteert uw segmenten als `.csv`-bestanden en levert deze naar de gewenste locatie. Plan de gegevensimport in uw e-mailmarketingplatform vanaf de opslaglocatie die is ingeschakeld in [!DNL Platform]. Het proces om gegevens in te voeren varieert voor elke partner. Lees de afzonderlijke bestemmingsartikelen voor meer informatie.

## Ondersteunde e-mailmarketingdoelen {#supported-destinations}

Adobe Experience Platform ondersteunt de volgende e-mailmarketingdoelen:

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Salesforce-Marketing Cloud](salesforce-marketing-cloud.md)

## Verbinding maken met een nieuwe marketingbestemming voor e-mail {#connect-destination}

Om segmenten naar e-mail marketing bestemmingen voor uw campagnes te verzenden, moet het Platform eerst met de bestemming verbinden. Zie de [zelfstudie over het maken van doelen](../../ui/connect-destination.md) voor gedetailleerde informatie over het instellen van een nieuwe bestemming.

## Tips en trucs bij het activeren van het publiek naar marketingbestemmingen via e-mail {#best-practices}

### Identiteitsselectie {#identity}

Adobe adviseert dat u een uniek herkenningsteken van uw [samenvoegingsschema](../../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Dit is het veld waarvan de gebruikers-id&#39;s zijn weggefilterd. Meestal is dit veld het e-mailadres, maar het kan ook een id voor een loyaliteitsprogramma of een telefoonnummer zijn. Raadpleeg de onderstaande tabel voor de meest gangbare unieke id&#39;s en hun XDM-veld in het schema.

| Unieke id | XDM-veld in Unified Schema |
|----------------- | ---------------------------|
| E-mailadres | `personalEmail.address` |
| Telefoon | `mobilePhone.number` |
| ID Loyalty-programma | `Customer-defined XDM field` |

### Andere doelkenmerken

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

## Gegevens van de opslaglocatie naar de bestemming importeren {#import-data-into-destination}

Lees de afzonderlijke artikelen van de e-mailmarketing bestemming om te leren hoe te om gegevens van uw opslagplaats in bestemmingen in te voeren:

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Salesforce-Marketing Cloud](salesforce-marketing-cloud.md)

## Segmenten activeren voor e-mailmarketingdoelen {#activate}

Voor instructies op hoe te om segmenten aan e-mail marketing bestemmingen te activeren, verwijs naar [profielen en segmenten aan een bestemming ](../../ui/activate-destinations.md) activeren.

## Aanvullende bronnen

* [Gegevens naar doelen activeren](../../ui/activate-destinations.md)
* [E-mailmarketingdoelen maken en gegevens activeren met de Flow Service API](../../api/email-marketing.md)
