---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Privacy Service probleemoplossingsgids
topic-legacy: troubleshooting
description: Dit document bevat antwoorden op veelgestelde vragen over Privacy Service en informatie over veelvoorkomende fouten in de API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---

# [!DNL Privacy Service] gids voor problemen

Adobe Experience Platform [!DNL Privacy Service] verstrekt een RESTful API en gebruikersinterface om bedrijven te helpen de privacyverzoeken van klantengegevens beheren. Met [!DNL Privacy Service], kunt u verzoeken indienen om toegang te krijgen tot persoonlijke of persoonlijke klantgegevens en deze te verwijderen, zodat u gemakkelijker kunt voldoen aan de regels van de organisatie en de wettelijke privacy.

Dit document geeft antwoorden op veelgestelde vragen over [!DNL Privacy Service], alsmede informatie over veelvoorkomende fouten in de API.

## Wat is het verschil tussen een gebruiker en een gebruiker-id wanneer u privacyverzoeken indient in de API? {#user-ids}

Als u een nieuwe privacytaak in de API wilt maken, moet de JSON-payload van de aanvraag een `users` array die specifieke informatie bevat voor elke gebruiker waarop de privacyaanvraag van toepassing is. Elk item in het dialoogvenster `users` array is een object dat een bepaalde gebruiker vertegenwoordigt, geïdentificeerd door de `key` waarde.

Elk gebruikersobject (of `key`) bevat zijn eigen `userIDs` array. Deze array bevat specifieke id-waarden **voor die specifieke gebruiker**.

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

De array bevat twee objecten die afzonderlijke gebruikers vertegenwoordigen die door hun `key` waarden (&quot;DavidSmith&quot; en &quot;user12345&quot;). &quot;DavidSmith&quot; heeft slechts één vermelde ID (hun e-mailadres), terwijl &quot;user12345&quot; twee ID (hun e-mailadres en ECID) heeft.

Zie de handleiding voor meer informatie over het opgeven van identiteitsgegevens van gebruikers [identiteitsgegevens voor privacyverzoeken](identity-data.md).


## Kan ik gebruiken [!DNL Privacy Service] om gegevens op te schonen die per ongeluk zijn verzonden naar [!DNL Platform]?

Adobe ondersteunt het gebruik van [!DNL Privacy Service] voor het wissen van gegevens die per ongeluk bij een product zijn ingediend. [!DNL Privacy Service] is ontworpen om u te helpen bij het voldoen aan uw verplichtingen voor toegang tot of het verwijderen van verzoeken van betrokkenen (of consumenten). Deze verzoeken zijn tijdgevoelig en worden met betrekking tot het toepasselijke privacyrecht afgerond. Het indienen van verzoeken die geen toegang tot of verwijderingsverzoeken voor betrokkenen/consumenten zijn, heeft gevolgen voor alle [!DNL Privacy Service] klanten en de mogelijkheden voor [!DNL Privacy Service] de passende wettelijke termijnen te ondersteunen.

Neem contact op met uw accountmanager (CDM) om problemen met PII&#39;s of gegevens te coördineren en een inspanningsniveau te bieden.

## Hoe krijg ik informatie over de status van mijn privacyverzoek of baan?

U kunt details over een bepaalde baan terugwinnen door te gebruiken [!DNL Privacy Service] API of gebruikersinterface.

### De API gebruiken

De status van een bepaalde taak ophalen met de opdracht [!DNL Privacy Service] API, een aanvraag indienen bij de hoofdmap (`GET /`), gebruikt u de id van de taak in het aanvraagpad. Zie de sectie over [controleren van de status van een baan](api/privacy-jobs.md#check-the-status-of-a-job) in de [!DNL Privacy Service] API-handleiding.

### De gebruikersinterface gebruiken

Alle actieve taakaanvragen worden vermeld in het dialoogvenster **[!UICONTROL Job Requests]** widget op de [!DNL Privacy Service] UI-dashboard. De status voor elke taakaanvraag wordt weergegeven onder de **[!UICONTROL Status]** kolom. Voor meer informatie over het weergeven van taakaanvragen in de gebruikersinterface raadpleegt u de [Gebruikershandleiding voor Privacy Service](ui/user-guide.md).

## Hoe kan ik de resultaten van mijn voltooide privacytaken downloaden?

De [!DNL Privacy Service] API en gebruikersinterface bieden beide methoden voor het downloaden van de resultaten van voltooide taken in ZIP-indeling.

### De API gebruiken

Een aanvraag indienen bij de hoofdmap (`GET /`) in de [!DNL Privacy Service] API, met de id van de taak waarvan u de resultaten wilt downloaden in het aanvraagpad. Als de status van de taak is voltooid, bevat de API een `downloadURL` in de reactiehoofdtekst. Dit kenmerk bevat een URL die u in de adresbalk van uw browser kunt plakken om het ZIP-bestand te downloaden.

Zie de sectie over [een taak zoeken op basis van de id](api/privacy-jobs.md#check-the-status-of-a-job) in de [!DNL Privacy Service] API-handleiding.

### De gebruikersinterface gebruiken

Op de [!DNL Privacy Service] UI-dashboard, zoek de taak die u wilt downloaden van het **Taakverzoeken** widget. Selecteer de id van de taak om de pagina Taakdetails te openen. Selecteer **Downloaden** in de rechterbovenhoek om het ZIP-bestand te downloaden. Zie de [Gebruikershandleiding voor Privacy Service](ui/user-guide.md) voor meer gedetailleerde stappen.

## Algemene foutberichten

In de volgende tabel worden enkele veelvoorkomende fouten in [!DNL Privacy Service], met beschrijvingen die helpen hun respectieve problemen op te lossen.

| Foutbericht | Beschrijving |
| --- | --- |
| Er zijn geen gebruikersnaam gevonden. | Sommige van de gebruikers-id&#39;s die in de aanvraag zijn opgegeven, zijn niet gevonden en overgeslagen. Zorg ervoor dat u de juiste naamruimte(n) en id-waarden gebruikt in de payload van de aanvraag. Document weergeven op [identiteitsgegevens verstrekken](./identity-data.md) voor een nadere toelichting. |
| Ongeldige naamruimte | Een opgegeven naamruimte voor de identiteit van een gebruiker-id is ongeldig. Zie de sectie over [standaardnaamruimten](./api/appendix.md#standard-namespaces) in de [!DNL Privacy Service] API-handleiding voor een lijst met toegestane naamruimten. Als u een aangepaste naamruimte gebruikt, moet u controleren of u de id&#39;s instelt `type` eigenschap aan &quot;custom&quot;. |
| Gedeeltelijk voltooid | De taak is voltooid, maar sommige gegevens zijn niet van toepassing op de opgegeven aanvraag en zijn overgeslagen. |
| De gegevens hebben niet de vereiste indeling. | Een of meer gegevenswaarden voor de opgegeven toepassing zijn onjuist opgemaakt. Controleer de taakdetails voor meer informatie. |
| De IMS-organisatie is niet ingericht. | Dit bericht treedt op wanneer uw IMS-organisatie niet is ingericht voor [!DNL Privacy Service]. Neem contact op met de beheerder voor meer informatie. |
| Toegang en machtigingen zijn vereist. | Toegang en machtigingen zijn vereist voor gebruik [!DNL Privacy Service]. Neem contact op met de beheerder om toegang te krijgen. |
| Er is een probleem opgetreden bij het uploaden en archiveren van de toegangsgegevens. | Wanneer deze fout optreedt, uploadt u de toegangsgegevens opnieuw en probeert u het opnieuw. |
| De werkbelasting is overschreden voor de huidige documentsnelheidslimiet. | Als deze fout optreedt, verlaagt u de verzendfrequentie en probeert u het opnieuw. |
