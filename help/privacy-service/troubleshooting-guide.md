---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Veelgestelde vragen over privacyservice
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 7e2e36e13cffdb625b7960ff060f8158773c0fe3

---


# Veelgestelde vragen over privacyservice

Dit document bevat antwoorden op veelgestelde vragen over de privacyservice van het Adobe Experience Platform.

De Dienst van de privacy verstrekt RESTful API en gebruikersinterface om bedrijven te helpen verzoeken van de privacy van klantengegevens beheren. Met de Privacy Service kunt u verzoeken indienen om toegang te krijgen tot persoonlijke of persoonlijke klantgegevens en deze te verwijderen, waardoor u gemakkelijker kunt voldoen aan de regels van de organisatie en de wettelijke privacy.

## Kan ik de privacyservice gebruiken om gegevens op te schonen die per ongeluk naar het platform zijn verzonden?

Adobe biedt geen ondersteuning voor het gebruik van de Privacy Service voor het wissen van gegevens die per ongeluk naar een product zijn verzonden. De Dienst van de privacy wordt ontworpen om u bij het voldoen aan uw verplichtingen voor de toegang van het gegevenssubject (of consument) of schrappingsverzoeken te helpen. Deze verzoeken zijn tijdgevoelig en worden met betrekking tot het toepasselijke privacyrecht afgerond. De indiening van verzoeken die geen toegang tot of verwijderingsverzoeken voor betrokkenen/consumenten zijn, heeft gevolgen voor alle klanten van de privacydienst en voor de mogelijkheid voor de privacydienst om de juiste wettelijke termijnen te ondersteunen.

Neem contact op met uw accountmanager (CDM) om problemen met PII&#39;s of gegevens te coördineren en een inspanningsniveau te bieden.

## Hoe krijg ik informatie over de status van mijn privacyverzoek of baan?

U kunt details over een bepaalde baan terugwinnen door de Dienst API van de Privacy of gebruikersinterface te gebruiken.

### De API gebruiken

Om de status van een bepaalde baan terug te winnen die de Dienst API van de Privacy gebruikt, doe een verzoek aan het wortel (`GET /`) eindpunt, gebruikend identiteitskaart van de baan in de verzoekweg. Voor meer details, zie de sectie over het [controleren van de status van een baan](api/privacy-jobs.md#check-the-status-of-a-job) in de de ontwikkelaarsgids van de Dienst van de Privacy.

### De gebruikersinterface gebruiken

Alle actieve taakverzoeken worden vermeld in de widget **Taakverzoeken** op het UI-dashboard voor de privacyservice. De status voor elke taakaanvraag wordt weergegeven onder de kolom **Status** . Voor meer informatie over het bekijken van baanverzoeken in UI, gelieve de de gebruikersgids [van de Dienst van de](ui/user-guide.md)Privacy te raadplegen.

## Hoe kan ik de resultaten van mijn voltooide privacytaken downloaden?

De API voor de privacyservice en de gebruikersinterface bieden beide methoden voor het downloaden van de resultaten van voltooide taken in ZIP-indeling.

### De API gebruiken

Maak een verzoek aan het wortel (`GET /`) eindpunt in de Dienst API van de Privacy, gebruikend identiteitskaart van de baan waarvan resultaten u in de verzoekweg wilt downloaden. Als de status van de taak is voltooid, neemt de API een `downloadURL` kenmerk op in de antwoordinstantie. Dit kenmerk bevat een URL die u in de adresbalk van uw browser kunt plakken om het ZIP-bestand te downloaden.

Voor meer details, zie de sectie over het [omhoog zoeken van een baan door zijn identiteitskaart](api/privacy-jobs.md#check-the-status-of-a-job) in de de ontwikkelaarsgids van de Dienst van de Privacy.

### De gebruikersinterface gebruiken

Zoek op het UI-dashboard voor de privacyservice de taak die u wilt downloaden van de **widget Taakverzoeken** . Klik op de id van de taak om de pagina _Taakdetails_ te openen. Klik van hieruit op **Downloaden** in de rechterbovenhoek om het ZIP-bestand te downloaden. Raadpleeg de gebruikershandleiding [van de](ui/user-guide.md) Privacy Service voor meer informatie.