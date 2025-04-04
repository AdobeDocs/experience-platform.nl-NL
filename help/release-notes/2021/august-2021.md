---
title: Aanvullende informatie van augustus 2021 voor Adobe Experience Platform
description: Aanvullende informatie van augustus 2021 voor Adobe Experience Platform.
doc-type: release notes
last-update: August 25, 2021
author: ens28527
exl-id: 0513b9dc-b16c-43b3-8e17-4be4499308d4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 28%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 25 augustus 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [Bestemmingen](#destinations)
- [Waarnembaarheidsinzichten](#observability)
- [Realtime-klantenprofiel](#profile)
- [Bronnen](#sources)

## Bestemmingen {#destinations}

Doelen zijn vooraf gebouwde integraties met bestemmingsplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos in te schakelen. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | De bestemming Airship Attributes, voorheen in bèta, is nu over het algemeen beschikbaar. |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | De bestemming van de Markeringen van het Luchtschip, eerder in bèta, is nu algemeen beschikbaar. |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | De bestemming van het Waas, vroeger in bèta, is nu over het algemeen beschikbaar. |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | Met de Pinterest Customer List-bestemming kunt u een publiek maken op basis van uw klantlijsten, op basis van personen die uw site hebben bezocht of op basis van Pinterest al met uw inhoud hebben gewerkt. |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | Richt uw bestaande volgers en klanten in Twitter en creeer relevante re-marketing campagnes door uw publiek te activeren dat binnen Adobe Experience Platform wordt gebouwd. |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX is een geaggregeerde Verizon Media/Yahoo-infrastructuur die verschillende componenten host die Verizon Media/Yahoo in staat stellen gegevens met zijn externe partners op een veilige, geautomatiseerde en schaalbare manier uit te wisselen. |

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Adobe Experience Platform Destination SDK is een reeks van configuratie APIs die u toestaan om bestemmingsintegratiepatronen voor Experience Platform te vormen om publiek en profielgegevens aan uw eindpunt te leveren, die op gegevens en authentificatieformaten van uw keus wordt gebaseerd. De configuraties worden opgeslagen in Experience Platform en kunnen via API worden opgehaald voor extra updates. |
| [ de verbeteringen van de Bruikbaarheid aan Doelen ](../../destinations/ui/activation-overview.md) | De verbeteringen van de bruikbaarheid aan bestemmingen laten marketers toe om segmenten aan bestaande bestemmingen naadloos te activeren. |

Voor meer algemene informatie over bestemmingen raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Waarnembaarheidsinzichten {#observability}

Met behulp van Observability Insights kunt u de Experience Platform-activiteiten volgen aan de hand van statistische gegevens en gebeurtenismeldingen.

**Nieuwe Eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Waarschuwingen | U kunt nu een abonnement nemen op belangrijke waarschuwingen met betrekking tot workflows die op Experience Platform worden uitgevoerd. Nadat u zich hebt geabonneerd op specifieke waarschuwingsregels, ontvangt u meldingen en e-mails in de gebruikersinterface wanneer een belangrijke levenscyclusgebeurtenis plaatsvindt (zoals het opnemen van gegevens) of als er problemen zijn die uw aandacht vereisen (zoals het mislukken van een innamestroom of het langer duren dan u had verwacht van een segmenttaak). Voor meer informatie, zie het [ alarm overzicht ](../../observability/alerts/overview.md). |

Zie het [ overzicht van de Inzichten van de Waarneming ](../../observability/home.md) voor meer informatie over de dienst.

## Realtime-klantenprofiel {#profile}

Met Adobe Experience Platform kunt u uw klanten gecoördineerde, consistente en relevante ervaringen bieden, ongeacht waar of wanneer ze met uw merk in aanraking komen. Met Real-Time Customer Profile krijgt u een holistisch beeld van elke individuele klant, waarbij gegevens uit meerdere kanalen worden gecombineerd, waaronder online, offline, CRM en gegevens van derden. Met Profile kunt u klantgegevens samenvoegen tot één overzichtelijk overzicht, dat een bruikbaar overzicht met tijdstempel biedt van elke klantinteractie.

| Functie | Beschrijving |
| ------- | ----------- |
| Bladeren door profielen op samenvoegbeleid of identiteit | Wanneer u in Experience Platform door profielen bladert, kunt u nu door samenvoegbeleid bladeren om een voorvertoning weer te geven van 20 voorbeeldprofielen op basis van het geselecteerde samenvoegbeleid. U kunt ook op identiteit bladeren om naar een specifiek profiel te zoeken dat een naamruimte van de identiteit en verwante identiteitswaarde gebruikt. Voor meer informatie, zie de [ Realtime gids UI van het Profiel van de Klant ](../../profile/ui/user-guide.md). |

Meer over het Profiel van de Klant in real time, met inbegrip van leerprogramma&#39;s en beste praktijken voor het werken met profielgegevens leren, gelieve te beginnen door het [ overzicht van het Profiel van de Klant in real time ](../../profile/home.md) te lezen.

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

| Functie | Beschrijving |
| ------- | ----------- |
| Bronaansluiting voor lokale bestandsupload | De categorie voor het opnemen van bestanden is hernoemd naar het lokale systeem, zodat u lokale bestanden rechtstreeks naar Experience Platform kunt overbrengen via de lokale connector voor het uploaden van bestanden. De gegevens die door deze schakelaar worden opgenomen kunnen door het Dashboard van de Controle worden gecontroleerd. Zie het [ lokale dossier uploadt bronoverzicht ](../../sources/connectors/local-system/local-file-upload.md) voor meer informatie. |

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
