---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen
title: Overzicht van e-mailmarketingdoelen
type: Tutorial
description: Met e-mailserviceproviders (ESP's) kunt u uw marketingactiviteiten voor e-mail beheren, bijvoorbeeld voor het verzenden van promotionele e-mailcampagnes.
translation-type: tm+mt
source-git-commit: 02754055e2be8a45a0699386cb559dad8f25717c
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---


# Overzicht van e-mailmarketingdoelen {#email-marketing-destinations}

Met e-mailserviceproviders (ESP&#39;s) kunt u uw marketingactiviteiten voor e-mail beheren, zoals het verzenden van promotionele e-mailcampagnes. Adobe Experience Platform integreert met ESPs door u toe te staan om segmenten aan e-mail marketing bestemmingen te activeren.

Om segmenten naar e-mail marketing bestemmingen voor uw campagnes te verzenden, moet het Platform eerst met de bestemming verbinden.

Verbinding maken met marketingdoelen voor e-mail is een proces in drie stappen ([configure destination](#connect-destination), [activate segments](#select-segments), [import data from storage location into the destination](#import-data-into-destination)). Elk van de stappen wordt hieronder verder beschreven op deze pagina.

In de verbindingsbestemmingsstroom, die in de sectie hieronder wordt beschreven, verbind met of Amazon S3 of SFTP. Platform exporteert uw segmenten als `.csv`- of `.txt`-bestanden en levert deze naar de gewenste locatie. Plan de gegevensimport in uw e-mailmarketingplatform vanaf de opslaglocatie die in het Platform is ingeschakeld. Het proces om gegevens in te voeren varieert voor elke partner. Lees de afzonderlijke bestemmingsartikelen voor meer informatie.

## Doel {#connect-destination} configureren

Selecteer in **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** de e-mailmarketingbestemming waarmee u verbinding wilt maken en selecteer **[!UICONTROL Configure]**.

![Verbinden met doel](../../assets/catalog/email-marketing/overview/connect-email-marketing.png)

Als u in de stap **[!UICONTROL Account]** eerder een verbinding met uw e-mailmarketingbestemming had ingesteld, selecteert u **[!UICONTROL Existing Account]** en selecteert u de bestaande verbinding. U kunt ook **[!UICONTROL New Account]** selecteren om een nieuwe verbinding met uw e-mailmarketingbestemming in te stellen. In de **[!UICONTROL Connection type]** selecteur, kunt u tussen [!UICONTROL Amazon S3], [!UICONTROL Azure Blob], [!UICONTROL SFTP with Password], of [!UICONTROL SFTP with SSH Key] selecteren. Vul de informatie hieronder in, afhankelijk van uw verbindingstype, dan uitgezocht **[!UICONTROL Connect]**.

- Voor **S3 verbindingen**, moet u uw Sleutelidentiteitskaart van de Toegang van Amazon en Geheime Sleutel van de Toegang verstrekken.
- Voor **SFTP met Wachtwoord** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Wachtwoord voor uw server SFTP verstrekken.
- Voor **SFTP met SSH Key** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel SSH voor uw server van SFTP verstrekken.

U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden onder de sectie **[!UICONTROL Key]**. Uw openbare sleutel moet als [!DNL Base64] gecodeerde koord worden geschreven.

Voer in de stap **[!UICONTROL Authentication]** een naam en beschrijving in voor uw nieuwe bestemming en de bestandsindeling voor de geëxporteerde bestanden.

Als u in de vorige stap Amazon S3 als opslagoptie hebt geselecteerd, voegt u de naam van het emmertje en het mappad in de opslaglocatie van de cloud in waar de bestanden worden geleverd. Voeg voor de opslagoptie SFTP het mappad in waar de bestanden worden geleverd.

Bij deze stap kunt u ook elke marketingactie selecteren die op deze bestemming moet worden toegepast. Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Lees voor meer informatie over marketingacties het [Overzicht van het beleid voor gegevensgebruik](../../../data-governance/policies/overview.md).

![E-mailinstallatiestap](../../assets/catalog/email-marketing/overview/email-setup-step.png)

## Selecteer welke segmentleden u wilt opnemen in uw doelexport {#select-segments}

Selecteer op de pagina **[!UICONTROL Select Segments]** welke segmenten naar het doel moeten worden verzonden. Meer informatie over de velden in de onderstaande secties vindt u.

![Segmenten selecteren](../../assets/common/email-select-segments.png)

## Bestandsnamen configureren

Voor informatie over het segmentprogramma en dossier - noem het uitgeven opties, verwijs naar [vorm](../../ui/activate-destinations.md#configure) stap in de activerende bestemmingszelfstudie.

## Kenmerken selecteren - Selecteer welke schemavelden u als doelkenmerken wilt gebruiken in uw geëxporteerde bestanden {#destination-attributes}

In deze stap selecteert u welke velden u wilt exporteren naar marketingdoelen per e-mail en geeft u aan welke velden verplicht zijn.
Voor informatie over deze stap, verwijs naar [Uitgezochte attributen](../../ui/activate-destinations.md#select-attributes) stap in de activerende bestemmingsleerprogramma.

## Identiteit {#identity}

Adobe adviseert dat u een uniek herkenningsteken van uw [samenvoegingsschema](../../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Dit is het veld waarvan de gebruikers-id&#39;s zijn weggefilterd. Meestal is dit veld het e-mailadres, maar het kan ook een id voor een loyaliteitsprogramma of een telefoonnummer zijn. Raadpleeg de onderstaande tabel voor de meest gangbare unieke id&#39;s en hun XDM-veld in het schema.

| Unieke id | XDM-veld in Unified Schema |
----------------- | ---------------------------
| E-mailadres | `personalEmail.address` |
| Telefoon | `mobilePhone.number` |
| ID Loyalty-programma | `Customer-defined XDM field` |

## Andere doelkenmerken

Kies in de keuzelijst Schema welke andere velden u naar de e-mailbestemming wilt exporteren. Enkele aanbevolen opties zijn:

| Schema | XDM-veld |
------ | ---------
| Voornaam | `person.name.firstName` |
| Achternaam | `person.name.lastName` |
| Telefoon | `mobilePhone.number` |
| Plaats adres | `homeAddress.city` |
| Adresstatus | `homeAddress.stateProvince` |
| Postcode adres | `homeAddress.postalCode` |
| Geboortedatum | `person.birthDayAndMonth` |
| Segmentlidmaatschap | `segmentMembership.status` |

## Gegevens van uw opslaglocatie importeren naar de bestemming {#import-data-into-destination}

Lees de afzonderlijke artikelen van de e-mailmarketing bestemming om te leren hoe te om gegevens van uw opslagplaats in bestemmingen in te voeren:

- [Adobe Campaign](./adobe-campaign.md#import-data-into-campaign)
- [Oracle Eloqua](./oracle-eloqua.md#import-data-into-eloqua)
- [Oracle Responsys](./oracle-responsys.md#import-data-into-responsys)
- [Salesforce-Marketing Cloud](./salesforce-marketing-cloud.md#import-data-into-salesforce)

## Segmenten activeren voor e-mailmarketingdoelen

Voor instructies op hoe te om segmenten aan e-mail marketing bestemmingen te activeren, verwijs naar [profielen en segmenten aan een bestemming ](../../ui/activate-destinations.md) activeren.

## Aanvullende bronnen

- [Gegevens naar doelen activeren](../../ui/activate-destinations.md)
- [E-mailmarketingdoelen maken en gegevens activeren met de Flow Service API](../../api/email-marketing.md)