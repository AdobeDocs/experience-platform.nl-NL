---
keywords: Experience Platform;startpagina;populaire onderwerpen
solution: Experience Platform
title: Privacy Service-gids voor probleemoplossing
description: Dit document bevat antwoorden op veelgestelde vragen over Privacy Service en informatie over veelvoorkomende fouten in de API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 1%

---

# [!DNL Privacy Service] gids voor probleemoplossing

Adobe Experience Platform [!DNL Privacy Service] biedt een RESTful-API en -gebruikersinterface waarmee bedrijven privacyverzoeken van klantgegevens kunnen beheren. Met [!DNL Privacy Service] kunt u verzoeken indienen om toegang te krijgen tot persoonlijke of persoonlijke klantgegevens en deze te verwijderen, zodat u gemakkelijker kunt voldoen aan de regels voor organisatie en juridische privacy.

Dit document bevat antwoorden op veelgestelde vragen over [!DNL Privacy Service] en informatie over veelvoorkomende fouten in de API.

## Wat is het verschil tussen een gebruiker en een gebruiker-id wanneer u privacyverzoeken indient in de API? {#user-ids}

Als u een nieuwe privacytaak in de API wilt maken, moet de JSON-payload van de aanvraag een `users` -array bevatten met specifieke informatie voor elke gebruiker waarop de privacyaanvraag van toepassing is. Elk item in de array `users` is een object dat een bepaalde gebruiker vertegenwoordigt, geïdentificeerd door de waarde `key` ervan.

Elk gebruikersobject (of `key` ) bevat op zijn beurt een eigen `userIDs` -array. Deze serie maakt een lijst van specifieke waarden van identiteitskaart **voor die bepaalde gebruiker**.

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

De array bevat twee objecten die afzonderlijke gebruikers vertegenwoordigen die worden aangeduid met hun `key` -waarden (&quot;DavidSmith&quot; en &quot;user12345&quot;). &quot;DavidSmith&quot; heeft slechts één vermelde ID (hun e-mailadres), terwijl &quot;user12345&quot; twee ID (hun e-mailadres en ECID) heeft.

Voor meer informatie bij het verstrekken van de informatie van de gebruikersidentiteit, zie de gids over [&#x200B; identiteitsgegevens voor privacyverzoeken &#x200B;](identity-data.md).


## Kan ik [!DNL Privacy Service] gebruiken om gegevens op te schonen die per ongeluk naar [!DNL Experience Platform] zijn verzonden?

Adobe biedt geen ondersteuning voor het gebruik van [!DNL Privacy Service] voor het wissen van gegevens die per ongeluk naar een product zijn verzonden. [!DNL Privacy Service] is ontworpen om u te helpen bij het voldoen aan uw verplichtingen voor de toegang tot of het verwijderen van verzoeken van betrokkenen (of consumenten). Elk ander gebruik van Privacy Service voor het opschonen of onderhouden van gegevens wordt niet ondersteund of toegestaan.

De verzoeken om privacy zijn tijdgevoelig en zijn voltooid met betrekking tot de toepasselijke privacywetgeving. het indienen van aanvragen die geen toegang tot of verwijderingsverzoeken voor betrokkenen/consumenten zijn, heeft invloed op alle [!DNL Privacy Service] -klanten en op de mogelijkheid voor [!DNL Privacy Service] om de juiste wettelijke tijdlijnen te ondersteunen. Er is nu een vaste uploadlimiet voor dagelijks gebruik om misbruik van de service te voorkomen.

Neem contact op met uw Adobe-accountteam om problemen met PII&#39;s of gegevens te coördineren en te verhelpen.

## Hoe krijg ik informatie over de status van mijn privacyverzoek of baan?

Met de API of gebruikersinterface van [!DNL Privacy Service] kunt u gegevens over een bepaalde taak ophalen.

### De API gebruiken

Om de status van een bepaalde baan terug te winnen die [!DNL Privacy Service] API gebruiken, doe een verzoek aan het wortel (`GET /`) eindpunt, gebruikend identiteitskaart van de baan in de verzoekweg. Voor meer details, zie de sectie op [&#x200B; controlerend het statuut van een baan &#x200B;](api/privacy-jobs.md#check-the-status-of-a-job) in de [!DNL Privacy Service] API gids.

### UI gebruiken

Alle actieve taakaanvragen worden vermeld in de **[!UICONTROL Job Requests]** -widget op het [!DNL Privacy Service] UI-dashboard. De status voor elke taakaanvraag wordt weergegeven onder de kolom **[!UICONTROL Status]** . Voor meer informatie bij het bekijken van baanverzoeken in UI, gelieve te zien de [&#x200B; gebruikersgids van Privacy Service &#x200B;](ui/user-guide.md).

## Hoe kan ik de resultaten van mijn voltooide privacytaken downloaden?

De API van [!DNL Privacy Service] en de gebruikersinterface bieden beide methoden voor het downloaden van de resultaten van voltooide taken in de ZIP-indeling.

### De API gebruiken

Maak een verzoek aan het wortel (`GET /`) eindpunt in [!DNL Privacy Service] API, gebruikend identiteitskaart van de baan waarvan resultaten u in de verzoekweg wilt downloaden. Als de status van de taak is voltooid, neemt de API een attribuut `downloadURL` op in de hoofdtekst van de reactie. Dit kenmerk bevat een URL die u in de adresbalk van uw browser kunt plakken om het ZIP-bestand te downloaden.

Voor meer details, zie de sectie op [&#x200B; zoekend omhoog een baan door zijn identiteitskaart &#x200B;](api/privacy-jobs.md#check-the-status-of-a-job) in de [!DNL Privacy Service] API gids.

### UI gebruiken

Op het [!DNL Privacy Service] dashboard UI, vind de baan u van **de Verzoeken van de Baan** widget wilt downloaden. Selecteer de id van de taak om de pagina Taakdetails te openen. Van hier, uitgezochte **Download** in de hoger-juiste hoek om het dossier van het PIT te downloaden. Zie de [&#x200B; gebruikersgids van Privacy Service &#x200B;](ui/user-guide.md) voor meer gedetailleerde stappen.

## Algemene foutberichten {#common-error-messages}

In de volgende tabel worden enkele algemene fouten in [!DNL Privacy Service] beschreven, met beschrijvingen die u helpen bij het oplossen van hun respectieve problemen.

| Foutbericht | Beschrijving |
| --- | --- |
| Er zijn geen gebruikersnaam gevonden. | Sommige van de gebruikers-id&#39;s die in de aanvraag zijn opgegeven, zijn niet gevonden en overgeslagen. Zorg ervoor dat u de juiste naamruimte(n) en id-waarden gebruikt in de payload van de aanvraag. Zie het document over [&#x200B; het verstrekken van identiteitsgegevens &#x200B;](./identity-data.md) voor een meer gedetailleerde verklaring. |
| Ongeldige naamruimte | Een opgegeven naamruimte voor de identiteit van een gebruiker-id is ongeldig. Zie de sectie op [&#x200B; standaardidentiteitsnamespaces &#x200B;](./api/appendix.md#standard-namespaces) in [!DNL Privacy Service] API gids bijlage voor een lijst van toegelaten namespaces. Als u een aangepaste naamruimte gebruikt, moet u ervoor zorgen dat de eigenschap `type` van de id is ingesteld op &#39;custom&#39;. |
| Gedeeltelijk voltooid | De taak is voltooid, maar sommige gegevens zijn niet van toepassing op de opgegeven aanvraag en zijn overgeslagen. |
| De gegevens hebben niet de vereiste indeling. | Een of meer gegevenswaarden voor de opgegeven toepassing zijn onjuist opgemaakt. Controleer de taakdetails voor meer informatie. |
| De IMS-organisatie is niet ingericht. | Dit bericht treedt op wanneer uw organisatie niet is ingericht voor [!DNL Privacy Service] . Neem contact op met de beheerder voor meer informatie. |
| Toegang en machtigingen zijn vereist. | Toegang en machtigingen zijn vereist om [!DNL Privacy Service] te kunnen gebruiken. Neem contact op met de beheerder om toegang te krijgen. |
| Er is een probleem opgetreden bij het uploaden en archiveren van de toegangsgegevens. | Wanneer deze fout optreedt, uploadt u de toegangsgegevens opnieuw en probeert u het opnieuw. |
| De werkbelasting is overschreden voor de huidige documentsnelheidlimiet. | Als deze fout optreedt, verlaagt u de verzendfrequentie en probeert u het opnieuw. |
| Te veel verzoeken <br> (HTTP 429 fouten) | Als uw voorleggingspatronen de gecontroleerde grens van toegestane gegevensonderwerpbanen overschrijden, zult u een HTTP 429 fout in antwoord op voortgezet verkeer van uw organisatie ontvangen. Privacy Service is bedoeld voor de verwerking van privacyverzoeken van betrokkenen. Het mag niet worden gebruikt voor het opschonen van gegevens. Als u fouten van HTTP 429 ontvangt, worden vertragings en verzoekgrenzen uitgevoerd om Adobe tegen misbruik te beschermen dat wettige nalevingswerk in gevaar zou kunnen brengen.<br> Alternatieve methodes om uw gegevens te minimaliseren worden verstrekt door [&#x200B; plaatsende datasetvervalprogramma&#39;s &#x200B;](../hygiene/ui/dataset-expiration.md) en het gebruiken van [&#x200B; verslag schrapt eigenschap &#x200B;](../hygiene/ui/record-delete.md). Raadpleeg de documentatie bij deze pagina voor meer informatie over het toepassen van deze functies. |
