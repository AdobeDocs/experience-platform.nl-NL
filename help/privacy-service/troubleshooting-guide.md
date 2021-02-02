---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Handleiding voor het oplossen van problemen met Privacys Service
topic: troubleshooting
description: Dit document bevat antwoorden op veelgestelde vragen over Privacy Service en informatie over veelvoorkomende fouten in de API.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---


# [!DNL Privacy Service] gids voor problemen

Adobe Experience Platform [!DNL Privacy Service] biedt een RESTful API en een gebruikersinterface om bedrijven te helpen bij het beheren van privacyverzoeken voor klantgegevens. Met [!DNL Privacy Service] kunt u verzoeken indienen om toegang te krijgen tot persoonlijke of persoonlijke klantgegevens en deze te verwijderen, waardoor u gemakkelijker kunt voldoen aan de regels voor organisatie en juridische privacy.

Dit document bevat antwoorden op veelgestelde vragen over [!DNL Privacy Service] en informatie over veelvoorkomende fouten in de API.

## Wat is het verschil tussen een gebruiker en een gebruiker-id wanneer u privacyverzoeken indient in de API? {#user-ids}

Als u een nieuwe privacytaak in de API wilt maken, moet de JSON-payload van de aanvraag een `users`-array bevatten met specifieke informatie voor elke gebruiker waarop de privacyaanvraag van toepassing is. Elk item in de `users`-array is een object dat een bepaalde gebruiker vertegenwoordigt, geïdentificeerd door de waarde `key` ervan.

Elk gebruikersobject (of `key`) bevat op zijn beurt een eigen `userIDs`-array. Deze array bevat specifieke id-waarden **voor die ene bepaalde gebruiker**.

Bekijk het volgende voorbeeld `users` array:

```json
"users": [
  {
    "key": "DavidSmith",
    "action": ["access"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "dsmith@acme.com",
        "type": "standard"
      }
    ]
  },
  {
    "key": "user12345",
    "action": ["access", "delete"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "ajones@acme.com",
        "type": "standard"
      },
      {
        "namespace": "ECID",
        "type": "standard",
        "value":  "443636576799758681021090721276",
        "isDeletedClientSide": false
      }
    ]
  }
]
```

De array bevat twee objecten die afzonderlijke gebruikers vertegenwoordigen die worden aangeduid met hun `key`-waarden (&quot;DavidSmith&quot; en &quot;user12345&quot;). &quot;DavidSmith&quot; heeft slechts één vermelde ID (hun e-mailadres), terwijl &quot;user12345&quot; twee ID (hun e-mailadres en ECID) heeft.

Voor meer informatie over het verstrekken van informatie van de gebruikersidentiteit, zie de gids over [identiteitsgegevens voor privacyverzoeken](identity-data.md).


## Kan ik [!DNL Privacy Service] gebruiken om gegevens op te schonen die per ongeluk naar [!DNL Platform] zijn verzonden?

Adobe biedt geen ondersteuning voor het gebruik van [!DNL Privacy Service] voor het wissen van gegevens die per ongeluk naar een product zijn verzonden. [!DNL Privacy Service] is ontworpen om u te helpen bij het voldoen aan uw verplichtingen voor toegang tot of het verwijderen van verzoeken van betrokkenen (of consumenten). Deze verzoeken zijn tijdgevoelig en worden met betrekking tot het toepasselijke privacyrecht afgerond. De indiening van verzoeken die geen toegang tot gegevens/verzoeken van consumenten of verzoeken tot verwijdering zijn, is van invloed op alle [!DNL Privacy Service]-klanten en op de mogelijkheid voor [!DNL Privacy Service] om de juiste wettelijke tijdlijnen te ondersteunen.

Neem contact op met uw accountmanager (CDM) om problemen met PII&#39;s of gegevens te coördineren en een inspanningsniveau te bieden.

## Hoe krijg ik informatie over de status van mijn privacyverzoek of baan?

U kunt details over een bepaalde baan terugwinnen door [!DNL Privacy Service] API of gebruikersinterface te gebruiken.

### De API gebruiken

Om de status van een bepaalde baan terug te winnen die [!DNL Privacy Service] API gebruiken, doe een verzoek aan het wortel (`GET /`) eindpunt, gebruikend identiteitskaart van de baan in de verzoekweg. Zie de sectie over [het controleren van de status van een taak](api/privacy-jobs.md#check-the-status-of-a-job) in de [!DNL Privacy Service]-handleiding voor ontwikkelaars voor meer informatie.

### De gebruikersinterface gebruiken

Alle actieve taakverzoeken worden vermeld in **[!UICONTROL Taakverzoeken]** widget op het [!DNL Privacy Service] UI-dashboard. De status voor elk taakverzoek wordt weergegeven onder de kolom **[!UICONTROL Status]**. Voor meer informatie over het bekijken van baanverzoeken in UI, gelieve [Privacy Service te zien gebruikersgids](ui/user-guide.md).

## Hoe kan ik de resultaten van mijn voltooide privacytaken downloaden?

De [!DNL Privacy Service] API en de gebruikersinterface verstrekken allebei methodes om de resultaten van voltooide banen in formaat te downloaden ZIP.

### De API gebruiken

Maak een verzoek aan het wortel (`GET /`) eindpunt in [!DNL Privacy Service] API, gebruikend identiteitskaart van de baan waarvan resultaten u in de verzoekweg wilt downloaden. Als de status van de taak is voltooid, neemt de API een `downloadURL`-kenmerk op in de responstekst. Dit kenmerk bevat een URL die u in de adresbalk van uw browser kunt plakken om het ZIP-bestand te downloaden.

Zie de sectie over [Een taak opzoeken op basis van de id](api/privacy-jobs.md#check-the-status-of-a-job) in de [!DNL Privacy Service]-handleiding voor ontwikkelaars voor meer informatie.

### De gebruikersinterface gebruiken

Zoek op het [!DNL Privacy Service] UI-dashboard de taak die u wilt downloaden van de widget **Taakverzoeken**. Selecteer de id van de taak om de pagina Taakdetails te openen. Selecteer **Download** in de rechterbovenhoek om het ZIP-bestand te downloaden. Zie [Gebruikershandleiding voor Privacys Service](ui/user-guide.md) voor meer gedetailleerde stappen.

## Algemene foutberichten

In de volgende tabel worden enkele algemene fouten in [!DNL Privacy Service] beschreven, met beschrijvingen die u helpen bij het oplossen van hun respectieve problemen.

| Foutbericht | Beschrijving |
| --- | --- |
| Er zijn geen gebruikersnaam gevonden. | Sommige van de gebruikers-id&#39;s die in de aanvraag zijn opgegeven, zijn niet gevonden en overgeslagen. Zorg ervoor dat u de juiste naamruimte(n) en id-waarden gebruikt in de payload van de aanvraag. Zie het document over [het verstrekken van identiteitsgegevens](./identity-data.md) voor een meer gedetailleerde verklaring. |
| Ongeldige naamruimte | Een opgegeven naamruimte voor de identiteit van een gebruiker-id is ongeldig. Zie de sectie over [standaard identiteitsnaamruimten](./api/appendix.md#standard-namespaces) in [!DNL Privacy Service] ontwikkelaarsgids bijlage voor een lijst van toegelaten namespaces. Als u een aangepaste naamruimte gebruikt, moet u ervoor zorgen dat de eigenschap `type` van de id is ingesteld op &quot;custom&quot;. |
| Gedeeltelijk voltooid | De taak is voltooid, maar sommige gegevens zijn niet van toepassing op de opgegeven aanvraag en zijn overgeslagen. |
| De gegevens hebben niet de vereiste indeling. | Een of meer gegevenswaarden voor de opgegeven toepassing zijn onjuist opgemaakt. Controleer de taakdetails voor meer informatie. |
| De IMS-organisatie is niet ingericht. | Dit bericht treedt op wanneer uw IMS-organisatie niet is ingericht voor [!DNL Privacy Service]. Neem contact op met de beheerder voor meer informatie. |
| Toegang en machtigingen zijn vereist. | Toegang en machtigingen zijn vereist om [!DNL Privacy Service] te kunnen gebruiken. Neem contact op met de beheerder om toegang te krijgen. |
| Er is een probleem opgetreden bij het uploaden en archiveren van de toegangsgegevens. | Wanneer deze fout optreedt, uploadt u de toegangsgegevens opnieuw en probeert u het opnieuw. |
| De werkbelasting is overschreden voor de huidige documentsnelheidslimiet. | Als deze fout optreedt, verlaagt u de verzendfrequentie en probeert u het opnieuw. |