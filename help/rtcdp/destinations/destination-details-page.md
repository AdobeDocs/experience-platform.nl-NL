---
title: Pagina Gegevens bestemming
seo-title: Pagina Gegevens bestemming
description: 'De detailspagina voor een individuele bestemming verstrekt een overzicht van de bestemmingsdetails, zoals de bestemmingsnaam, identiteitskaart, segmenten aan de bestemming in kaart worden gebracht, en controles om de activering uit te geven en de gegevensstroom toe te laten en onbruikbaar te maken. '
seo-description: 'De detailspagina voor een individuele bestemming verstrekt een overzicht van de bestemmingsdetails, zoals de bestemmingsnaam, identiteitskaart, segmenten aan de bestemming in kaart worden gebracht, en controles om de activering uit te geven en de gegevensstroom toe te laten en onbruikbaar te maken. '
translation-type: tm+mt
source-git-commit: e21cf6794e6c9ee522482cd9ccb95d66b06d330a

---


# Pagina met doeldetails {#destinations-details-page}

De detailspagina voor een individuele bestemming verstrekt een overzicht van de bestemmingsdetails, zoals de bestemmingsnaam, identiteitskaart, segmenten aan de bestemming in kaart worden gebracht, en controles om de activering uit te geven en de gegevensstroom toe te laten en onbruikbaar te maken. Als u deze gegevens wilt weergeven, gaat u naar **Doelen** > **Bladeren** en klikt u op de naam van het doel waarmee u wilt werken.

De kerncomponenten van een individuele bestemming zijn:

* 1 - Doelnaam en -id
* 2 - Segmenten geactiveerd naar doel
* 3 - Rechterspoorinformatie
* 4 - Besturingselementen voor het bewerken van de activering en het in- en uitschakelen van de gegevensstroom

![Doelpagina genummerd](/help/rtcdp/destinations/assets/destination-page-numbered.png)

Navigeer naar een afzonderlijke doelpagina voor een overzicht van de doeldetails, zoals:

## 1. Doelnaam en id

U kunt de doelnaam zien in de paginakop en de doel-id in de pagina-URL.

## 2. Segmenten geactiveerd naar doel

Deze sectie toont welke segmenten momenteel aan de bestemming, evenals verdere informatie over die segmenten in kaart worden gebracht. Zie onderstaande tabel voor meer informatie:

| Item | Beschrijving |
---------|----------|
| Segmentnaam | De naam van het segment. |
| Segmentbeschrijving | De beschrijving van uw segment. |
| Begindatum | De datum vanaf welke deze segmenten aan de bestemming worden geactiveerd. |
| Einddatum | De datum waarop deze segmenten ophouden te worden geactiveerd aan de bestemming. |
| Toewijzing-id | *Niet beschikbaar voor e-mailmarketingdoelen*. Wijst op identiteitskaart waardoor het segment in het bestemmingsplatform gekend is. |

## 3. Rechterspoorinformatie

De juiste spoorlijn omvat informatie over uw bestemming. Zie de onderstaande tabel voor meer informatie:

| Item | Beschrijving |
---------|----------|
| Platform | Vertegenwoordigt het bestemmingsplatform dat het publiek wordt verzonden naar. Zie Catalogus [](/help/rtcdp/destinations/destinations-catalog.md) Doelen voor meer informatie. |
| Beschrijving | U kunt de beschrijving van de doelstroom bewerken. |
| Categorie | Geeft het type doel aan. Zie Catalogus [](/help/rtcdp/destinations/destinations-catalog.md) Doelen voor meer informatie. |
| Verbindingstype | Hiermee geeft u aan in welke vorm uw publiek naar de bestemming wordt gestuurd. Dit kan **cookie** of **op profiel gebaseerde** zijn. |
| Frequentie | Geeft aan hoe vaak het publiek naar de bestemming wordt gestuurd. Kan **streaming** of **batch** zijn. |
| Identiteit | Vertegenwoordigt de identiteitsnaamruimte die door de bestemming wordt geaccepteerd. Het veld Identiteit kan bijvoorbeeld GAID, IDFA en e-mail zijn. Zie standaardnaamruimten in het naamruimteoverzicht [](../../identity-service/namespaces.md)Identiteit voor alle geaccepteerde naamruimten. |
| Gemaakt door | Geeft de gebruiker aan die deze doelstroom heeft gemaakt. |
| Gemaakt | Geeft de UTC-datum en -tijd aan waarop deze doelstroom is gemaakt. |

## 4. Besturingselementen voor het bewerken van de activering en het in- en uitschakelen van de gegevensstroom

Met het activeringsbesturingselement Bewerken kunt u bewerken welke segmenten worden toegewezen aan het doel. Druk op Activering bewerken om de workflow voor [segmentactivering](/help/rtcdp/destinations/activate-destinations.md)te openen.

Met de **schakeloptie Inschakelen/Uitschakelen** kunt u de gegevensexport naar een doel starten en pauzeren.