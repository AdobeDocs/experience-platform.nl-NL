---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Veelgestelde vragen over Privacy Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 5921f89ce551a4bdec4c5038d579cebd0451f5f2
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%

---


# Handleiding voor het oplossen van problemen met Privacys Service

Adobe Experience Platform Privacy Service verstrekt een RESTful API en gebruikersinterface om bedrijven te helpen verzoeken van de privacy van klantengegevens beheren. Met Privacy Service kunt u verzoeken indienen om toegang te krijgen tot persoonlijke of persoonlijke klantgegevens en deze te verwijderen, zodat u gemakkelijker kunt voldoen aan de regels van de organisatie en de wettelijke privacy.

Dit document bevat antwoorden op veelgestelde vragen over Privacy Service en informatie over veelvoorkomende fouten in de API.

## Wat is het verschil tussen een gebruiker en een gebruiker-id wanneer u privacyverzoeken indient in de API? {#user-ids}

Als u een nieuwe privacytaak in de API wilt maken, moet de JSON-payload van de aanvraag een `users` array bevatten met specifieke informatie voor elke gebruiker waarop de privacyaanvraag van toepassing is. Elk item in de `users` array is een object dat een bepaalde gebruiker vertegenwoordigt, geïdentificeerd door de `key` waarde ervan.

Elk gebruikersobject (of `key`) bevat op zijn beurt een eigen `userIDs` array. Deze array bevat een lijst met specifieke id-waarden **voor die ene gebruiker**.

Bekijk de volgende `users` voorbeeldarray:

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

De array bevat twee objecten die afzonderlijke gebruikers vertegenwoordigen die door hun `key` waarden worden geïdentificeerd (&quot;DavidSmith&quot; en &quot;user12345&quot;). &quot;DavidSmith&quot; heeft slechts één vermelde ID (hun e-mailadres), terwijl &quot;user12345&quot; twee ID (hun e-mailadres en ECID) heeft.

Zie de handleiding over [identiteitsgegevens voor privacyverzoeken](identity-data.md)voor meer informatie over het verstrekken van identiteitsgegevens van gebruikers.


## Kan ik Privacy Service gebruiken om gegevens op te schonen die per ongeluk naar het Platform zijn verzonden?

Adobe biedt geen ondersteuning voor het gebruik van Privacy Service voor het wissen van gegevens die per ongeluk naar een product zijn verzonden. Privacy Service is ontworpen om u te helpen bij het voldoen aan uw verplichtingen voor toegang tot of het verwijderen van verzoeken van betrokkenen (of consumenten). Deze verzoeken zijn tijdgevoelig en worden met betrekking tot het toepasselijke privacyrecht afgerond. Het indienen van verzoeken die geen toegang tot of verwijderingsverzoeken voor betrokkenen/consumenten zijn, heeft gevolgen voor alle klanten van de Privacy Service en voor de mogelijkheid voor Privacy Service om de juiste wettelijke termijnen te ondersteunen.

Neem contact op met uw accountmanager (CDM) om problemen met PII&#39;s of gegevens te coördineren en een inspanningsniveau te bieden.

## Hoe krijg ik informatie over de status van mijn privacyverzoek of baan?

U kunt details over een bepaalde baan terugwinnen door de Privacy Service API of gebruikersinterface te gebruiken.

### De API gebruiken

Om de status van een bepaalde baan terug te winnen die Privacy Service API gebruiken, doe een verzoek aan het wortel (`GET /`) eindpunt, gebruikend identiteitskaart van de baan in de verzoekweg. Zie de sectie over het [controleren van de status van een taak](api/privacy-jobs.md#check-the-status-of-a-job) in de handleiding voor ontwikkelaars van Privacys Service voor meer informatie.

### De gebruikersinterface gebruiken

Alle actieve taakverzoeken worden vermeld in de **widget Taakverzoeken** op het dashboard voor de gebruikersinterface van de Privacy Service. De status voor elke taakaanvraag wordt weergegeven onder de kolom **Status** . Raadpleeg de gebruikershandleiding bij de [Privacy Service voor meer informatie over het weergeven van taakaanvragen in de gebruikersinterface](ui/user-guide.md).

## Hoe kan ik de resultaten van mijn voltooide privacytaken downloaden?

De Privacy Service-API en de gebruikersinterface bieden beide methoden voor het downloaden van de resultaten van voltooide taken in ZIP-indeling.

### De API gebruiken

Maak een verzoek aan het wortel (`GET /`) eindpunt in Privacy Service API, gebruikend identiteitskaart van de baan waarvan resultaten u in de verzoekweg wilt downloaden. Als de status van de taak is voltooid, neemt de API een `downloadURL` kenmerk op in de antwoordinstantie. Dit kenmerk bevat een URL die u in de adresbalk van uw browser kunt plakken om het ZIP-bestand te downloaden.

Zie de sectie over het [opzoeken van een taak op basis van de id](api/privacy-jobs.md#check-the-status-of-a-job) in de handleiding voor ontwikkelaars van Privacys Service voor meer informatie.

### De gebruikersinterface gebruiken

Zoek op het UI-dashboard voor Privacys Service naar de taak die u wilt downloaden van de **widget Taakverzoeken** . Klik op de id van de taak om de pagina _Taakdetails_ te openen. Klik van hieruit op **Downloaden** in de rechterbovenhoek om het ZIP-bestand te downloaden. Raadpleeg de gebruikershandleiding [bij de](ui/user-guide.md) Privacy Service voor meer informatie.

## Algemene foutberichten

In de volgende tabel worden enkele veelvoorkomende fouten in de Privacy Service beschreven, met beschrijvingen die u helpen bij het oplossen van hun respectieve problemen.

| Foutbericht | Beschrijving |
| --- | --- |
| Er zijn geen gebruikersnaam gevonden. | Sommige van de gebruikers-id&#39;s die in de aanvraag zijn opgegeven, zijn niet gevonden en overgeslagen. Zorg ervoor dat u de juiste naamruimte(n) en id-waarden gebruikt in de payload van de aanvraag. Zie het document over het [verstrekken van identiteitsgegevens](./identity-data.md) voor een meer gedetailleerde verklaring. |
| Ongeldige naamruimte | Een opgegeven naamruimte voor de identiteit van een gebruiker-id is ongeldig. Zie de sectie over [standaardnaamruimten](./api/appendix.md#standard-namespaces) in de Privacy Service-ontwikkelaarsgids in de bijlage voor een lijst met geaccepteerde naamruimten. Als u een aangepaste naamruimte gebruikt, moet u ervoor zorgen dat de `type` eigenschap van de id is ingesteld op &#39;custom&#39;. |
| Gedeeltelijk voltooid | De taak is voltooid, maar sommige gegevens zijn niet van toepassing op de opgegeven aanvraag en zijn overgeslagen. |
| De gegevens hebben niet de vereiste indeling. | Een of meer gegevenswaarden voor de opgegeven toepassing zijn onjuist opgemaakt. Controleer de taakdetails voor meer informatie. |
| De IMS-organisatie is niet ingericht. | Dit bericht treedt op wanneer uw IMS-organisatie niet is ingericht voor Privacy Service. Neem contact op met de beheerder voor meer informatie. |
| Toegang en machtigingen zijn vereist. | Toegang en machtigingen zijn vereist om Privacy Service te kunnen gebruiken. Neem contact op met de beheerder om toegang te krijgen. |
| Er is een probleem opgetreden bij het uploaden en archiveren van de toegangsgegevens. | Wanneer deze fout optreedt, uploadt u de toegangsgegevens opnieuw en probeert u het opnieuw. |
| De werkbelasting is overschreden voor de huidige documentsnelheidslimiet. | Als deze fout optreedt, verlaagt u de verzendfrequentie en probeert u het opnieuw. |