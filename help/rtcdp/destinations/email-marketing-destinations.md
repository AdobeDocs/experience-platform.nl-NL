---
title: E-mailmarketingdoelen
seo-title: E-mailmarketingdoelen
description: Met e-mailserviceproviders (ESP's) kunt u uw marketingactiviteiten voor e-mail beheren, bijvoorbeeld voor het verzenden van promotionele e-mailcampagnes.
seo-description: Met e-mailserviceproviders (ESP's) kunt u uw marketingactiviteiten voor e-mail beheren, bijvoorbeeld voor het verzenden van promotionele e-mailcampagnes.
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---


# E-mailmarketingdoelen {#email-marketing-destinations}

Met e-mailserviceproviders (ESP&#39;s) kunt u uw marketingactiviteiten voor e-mail beheren, zoals het verzenden van promotionele e-mailcampagnes. Het Platform van de Gegevens van de Klant van Adobe in real time integreert met ESPs door u toe te staan om segmenten aan e-mail marketing bestemmingen te activeren.

Om segmenten naar e-mail marketing bestemmingen voor uw campagnes te verzenden, moet Adobe in real time CDP eerst met de bestemming verbinden.

Het verbinden met e-mail marketing bestemmingen is een proces in drie stappen. Elk van de stappen wordt hieronder verder beschreven op deze pagina.

Maak in de Connect-doelstroom, zoals beschreven in de onderstaande sectie, verbinding met Amazon S3 of SFTP. CDP in real time exporteert uw segmenten als `.csv` of `.txt` dossiers en levert hen aan uw aangewezen plaats. Plan de gegevensimport in uw e-mailmarketingplatform vanaf de opslaglocatie die in Real-Time CDP is ingeschakeld. Het proces om gegevens in te voeren varieert voor elke partner. Zie de afzonderlijke bestemmingsartikelen voor meer informatie.

## Stap 1 - Verbind bestemming {#connect-destination}

1. Selecteer in **[!UICONTROL Verbindingen > Doelen]** de e-mailmarketingbestemming waarmee u verbinding wilt maken en selecteer vervolgens de **[!UICONTROL Connect-bestemming]**.

   ![Verbinden met doel](/help/rtcdp/destinations/assets/connect-email-marketing.png)

2. Als u in de stap **[!UICONTROL Verificatie]** eerder een verbinding met uw e-mailmarketingbestemming had ingesteld, selecteert u **[!UICONTROL Bestaande account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding in te stellen met uw marketingbestemming voor e-mail. In de **[!UICONTROL het type]** van Verbinding selecteur, kunt u tussen **Amazon S3**, **SFTP met Wachtwoord**, **SFTP met SSH Sleutel** selecteren. Vul de informatie hieronder in, afhankelijk van het verbindingstype en selecteer vervolgens **[!UICONTROL Connect]**.

   Voor **S3-verbindingen** moet u uw Amazon Access Key-id en de Geheime toegangstoets opgeven.

   Voor **SFTP met de verbindingen van het Wachtwoord** , moet u Domein, Haven, Gebruikersnaam, en Wachtwoord voor uw server van SFTP verstrekken.

   Voor **SFTP met SSH Zeer belangrijke** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel SSH voor uw server van SFTP verstrekken.

3. Voer in de stap **[!UICONTROL Setup]** een **[!UICONTROL naam]** en een **[!UICONTROL beschrijving]** in voor uw nieuwe bestemming en de indeling **** Bestand voor de geëxporteerde bestanden. <br>
Als u Amazon S3 als opslagoptie hebt geselecteerd in de vorige stap, voegt u de naam **[!UICONTROL van het]** emmertje en het pad **[!UICONTROL naar de]** map in in de opslaglocatie van de cloud waar de bestanden worden geleverd. Voeg voor de opslagoptie SFTP het **[!UICONTROL mappad]** in waarin de bestanden worden geleverd. <br>
Ook in deze stap kunt u elke **[!UICONTROL Gebruikszaak]** voor marketingdoeleinden selecteren die op deze bestemming moet worden toegepast. Gebruiksgevallen voor marketingdoeleinden geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde gevallen voor marketinggebruik of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Voor meer informatie over het op de markt brengen van gebruiksgevallen, zie de [Governance van Gegevens in Echte tijd CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) pagina. Zie het overzicht [van het beleid voor](/help/data-governance/policies/overview.md#core-actions)gegevensgebruik voor informatie over de afzonderlijke door Adobe gedefinieerde gevallen van marketinggebruik. <br>
   ![E-mailinstallatiestap](/help/rtcdp/destinations/assets/email-setup-step.png)

## Stap 2 - selecteer welke segmentleden om in uw bestemmingsuitvoer te omvatten {#select-segments}

Selecteer op de pagina Segmenten **** selecteren welke segmenten u naar de bestemming wilt verzenden. Meer informatie over de velden in de onderstaande secties vindt u.

![Segmenten selecteren](/help/rtcdp/destinations/assets/email-select-segments.png)

## Stap 3 - selecteer welke schemagebieden als bestemmingsattributen in uw uitgevoerde dossiers te gebruiken {#destination-attributes}

In deze stap selecteert u welke velden u wilt exporteren naar marketingdoelen per e-mail.

![Doelkenmerken](/help/rtcdp/destinations/assets/destination-attributes.png)

### Identity {#identity}

Wij adviseren dat u een uniek herkenningsteken van uw [verenigingsschema](../../profile/home.md#profile-fragments-and-union-schemas)selecteert. Dit is het veld waarvan de identiteit van uw gebruikers wordt weggefilterd. Meestal is dit veld het e-mailadres, maar het kan ook een id voor een loyaliteitsprogramma of een telefoonnummer zijn. Zie de lijst hieronder voor de gemeenschappelijkste unieke herkenningstekens en hun gebied XDM in het unieschema.

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

* [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
* [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Segmenten activeren voor e-mailmarketingdoelen

Voor instructies op hoe te om segmenten aan e-mail marketing bestemmingen te activeren, zie Gegevens aan Doelen [activeren](/help/rtcdp/destinations/activate-destinations.md).