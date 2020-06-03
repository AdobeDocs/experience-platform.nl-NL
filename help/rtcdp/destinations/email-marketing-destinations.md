---
title: E-mailmarketingdoelen
seo-title: E-mailmarketingdoelen
description: Met e-mailserviceproviders (ESP's) kunt u uw marketingactiviteiten voor e-mail beheren, bijvoorbeeld voor het verzenden van promotionele e-mailcampagnes.
seo-description: Met e-mailserviceproviders (ESP's) kunt u uw marketingactiviteiten voor e-mail beheren, bijvoorbeeld voor het verzenden van promotionele e-mailcampagnes.
translation-type: tm+mt
source-git-commit: 121ae74e9c352b1f6fc12093d815e711ebd817b8
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---


# E-mailmarketingdoelen {#email-marketing-destinations}

Met e-mailserviceproviders (ESP&#39;s) kunt u uw marketingactiviteiten voor e-mail beheren, zoals het verzenden van promotionele e-mailcampagnes. Adobe Real-time Customer Data Platform kan met ESP&#39;s worden geïntegreerd door segmenten te activeren voor e-mailmarketingdoelen.

Om segmenten naar e-mail marketing bestemmingen voor uw campagnes te verzenden, moet Adobe in real time CDP eerst met de bestemming verbinden.

Het verbinden met e-mail marketing bestemmingen is een proces in drie stappen. Elk van de stappen wordt hieronder verder beschreven op deze pagina.

Maak in de Connect-doelstroom, zoals beschreven in de onderstaande sectie, verbinding met Amazon S3 of SFTP. CDP in real time exporteert uw segmenten als `.csv` of `.txt` dossiers en levert hen aan uw aangewezen plaats. Plan de gegevensimport in uw e-mailmarketingplatform vanaf de opslaglocatie die in Real-Time CDP is ingeschakeld. Het proces om gegevens in te voeren varieert voor elke partner. Zie de afzonderlijke bestemmingsartikelen voor meer informatie.

## Stap 1 - Verbind bestemming {#connect-destination}

1. Selecteer in **[!UICONTROL Verbindingen > Doelen]** de e-mailmarketingbestemming waarmee u verbinding wilt maken en selecteer vervolgens de **[!UICONTROL Connect-bestemming]**.

   ![Verbinden met doel](/help/rtcdp/destinations/assets/connect-destination-1.png)

2. Selecteer in de wizard Connect het type **[!UICONTROL Verbinding]** voor uw opslaglocatie. U kunt kiezen tussen **Amazon S3**, **SFTP met wachtwoord**, **SFTP met SSH-sleutel**. Vul de informatie hieronder in, afhankelijk van het verbindingstype en selecteer vervolgens **[!UICONTROL Connect]**.

Voor **S3 verbindingen**, moet u uw Zeer belangrijke identiteitskaart van de Toegang en Geheime Sleutel van de Toegang verstrekken.

Voor **SFTP met de verbindingen van het Wachtwoord** , moet u Domein, Haven, Gebruikersnaam, en Wachtwoord verstrekken.

Voor **SFTP met SSH Zeer belangrijke** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel van SSH verstrekken.

## Stap 2 - selecteer welke schemagebieden als bestemmingsattributen in uw uitgevoerde dossiers te gebruiken {#destination-attributes}

In deze stap selecteert u welke velden u wilt exporteren naar marketingdoelen per e-mail.

![Doelkenmerken](/help/rtcdp/destinations/assets/destination-attributes.png)

### Identity {#identity}

Wij adviseren dat u een uniek herkenningsteken van uw [verenigingsschema](../../profile/home.md#profile-fragments-and-union-schemas)selecteert. Dit is het veld waarvan de identiteit van uw gebruikers wordt weggefilterd. Meestal is dit veld het e-mailadres, maar het kan ook een id voor een loyaliteitsprogramma of een telefoonnummer zijn. Zie de onderstaande tabel voor de meest gebruikelijke unieke id&#39;s en hun XDM-veld in één schema.

| Unieke id | XDM-veld in Unified Schema |
---------|----------
| E-mailadres | `personalEmail.address` |
| Telefoon | `mobilePhone.number` |
| ID Loyalty-programma | `Customer-defined XDM field` |

### Andere doelkenmerken

Kies in de keuzelijst Schema welke andere velden u naar de e-mailbestemming wilt exporteren. Enkele aanbevolen opties zijn:

| Schema | XDM-veld |
---------|----------
| Voornaam | `person.name.firstName` |
| Achternaam | `person.name.lastName` |
| Telefoon | `mobilePhone.number` |
| Plaats adres | `homeAddress.city` |
| Adresstatus | `homeAddress.stateProvince` |
| Postcode adres | `homeAddress.postalCode` |
| Geboortedatum | `person.birthDayAndMonth` |

## Stap 3 - de Gegevens van de invoer van uw opslagplaats in de bestemming

Zie de afzonderlijke artikelen van de e-mailmarketing bestemming om te leren hoe te om gegevens van uw opslagplaats in bestemmingen in te voeren:

* [Adobe-campagne](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
* [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Segmenten activeren voor e-mailmarketingdoelen

Voor instructies op hoe te om segmenten aan e-mail marketing bestemmingen te activeren, zie Gegevens aan Doelen [activeren](/help/rtcdp/destinations/activate-destinations.md).