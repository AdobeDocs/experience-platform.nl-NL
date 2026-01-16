---
title: Privacy Service-foutcodes in Adobe Experience Platform
description: Begrijp Privacy Service foutcodes zodat u fouten kunt vaststellen, taakresultaten programmatisch kunt afhandelen en de volgende stappen kunt bepalen bij het verzenden of controleren van privacytaken.
keywords: privacyservice, foutcodes, privacytaken, api-fouten
solution: Experience Platform
source-git-commit: a312dabf5b8c3b52af31e2e127cd4bbeb8dd0021
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 2%

---

# Privacy Service-foutcodes {#privacy-service-error-codes}

Gebruik deze verwijzing om de baanresultaten van Privacy Service te identificeren, mislukkingen te diagnostiseren, en aangewezen volgende stappen te bepalen wanneer het voorleggen van of het controleren van privacybanen in **Adobe Experience Platform**. Leren om, privacybanen tot stand te brengen voor te leggen en te controleren, zie de [ gids van de de banen van de privacy ](./privacy-jobs.md) of de [ gebruikersgids van Privacy Service UI ](../ui/user-guide.md).

Privacy Service-foutcodes zijn een stabiel overheidscontract. Elke foutcode identificeert op unieke wijze een fout- of voltooiingsstatus waarop u kunt vertrouwen voor programmatische afhandeling en operationele workflows.

De volgende garanties zijn van toepassing bij het bouwen van automatiserings- of controleworkflows:

* Foutcodes zijn stabiel na publicatie.
* Foutberichten kunnen veranderen om de duidelijkheid te verbeteren, maar de codewaarde niet.
* Nieuwe foutcodes kunnen in de loop der tijd worden toegevoegd; bestaande codes worden niet opnieuw gebruikt.

Gebruik foutcodes, geen berichttekst, om automatisering of besluitvormingslogica te implementeren. Voor begeleiding bij efficiënte verwerking van privacybanen, de status van de controletaak, en het behandelen van fouten zonder het baseren op opiniepeiling of berichtkoorden, zie [ best practices van Privacy Service ](../best-practices.md).

## Opmaak van foutreactie {#error-response-format}

Privacy Service retourneert foutinformatie in taak en vraagt om antwoorden. De reactie bevat een numerieke foutcode en een leesbaar bericht in de antwoordlading.

De foutcode geeft het gezaghebbende resultaat aan. Het bericht biedt extra context voor het oplossen van problemen.

In dit document worden de betekenis en de intentie van elke foutcode beschreven. Voor gebied-vlakke reactieschema&#39;s en verzoekdetails, zie de [ Privacy Service API documentatie ](https://developer.adobe.com/experience-platform-apis/references/privacy-service/).

## Foutdomeinen {#error-domains}

Foutcodes worden gegroepeerd op functioneel domein, zodat u problemen sneller kunt diagnosticeren.

De volgende domeinen worden in dit document gebruikt:

* **bevestiging van het Verzoek**: Het verzoek is misvormd of bevat ongeldige waarden. Zie de [ gids van het de baaneindpunt van de privacy ](./privacy-jobs.md) voor verzoekstructuur en bevestigingsvereisten.
* **Vergunning en levering**: Uw organisatie of gebruiker heeft de vereiste toegang niet. Zie [ toestemmingen ](../permissions.md) beheren om op rol-gebaseerde toestemmingsvereisten te herzien.
* **Identiteit en toepasselijkheid**: De herkenningstekens of namespaces zijn niet van toepassing op het verzoek. Zie [ identiteitsgegevens voor privacyverzoeken ](../identity-data.md) voor gesteunde identiteitstypes en namespace vereisten.
* **Beperkend van het Tarief**: Het volume van de verzending overschrijdt platformgrenzen. Als deze fout optreedt, verlaagt u de verzendfrequentie en probeert u het opnieuw.
* **de toegang en verwerking van Gegevens**: Het systeem kan niet tot de gevraagde gegevens toegang hebben of verwerken. Zie de [ het oplossen van problemengids ](../troubleshooting-guide.md) voor gemeenschappelijke oorzaken en saneringsstappen.
* **Encryptie en zeer belangrijk beheer**: De vereiste encryptiesleutels zijn niet beschikbaar. Zie [ Klant Beheerde Sleutels ](../../landing/governance-privacy-security/customer-managed-keys/overview.md) voor zeer belangrijke toegang, configuratie, en terugwinningsbegeleiding.
* **de uitvoeringsstaat van de Baan**: De volledig voltooide baan, gedeeltelijk, of met mislukkingen. Zie de [ gids van het de baaneindpunt van de privacy ](./privacy-jobs.md#status-categories) voor beschrijvingen van de categorieën van de baanstatus en hun betekenis.

>[!NOTE]
>
>Domeintoewijzingen weerspiegelen de intentie van de foutcode, niet de interne servicegrenzen.

## Verwijzing naar foutcode {#error-code-reference}

In de volgende tabel worden alle openbare Privacy Service-foutcodes weergegeven.

| Foutcode | HTTP-status | Titel | Beschrijving |
| ---------- | ----------- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------| 
| 1000-400 | 400 | Opmaakfout | Een of meer gegevenswaarden voor de opgegeven toepassing hebben opmaakproblemen. Controleer de taakdetails voor extra informatie. |
| 1001-400 | 400 | Niet geautoriseerd | Uw organisatie beschikt niet over provisioning. Neem contact op met de beheerder voor meer informatie. |
| 1010-400 | 400 | Ontbrekende machtigingen | U hebt niet de vereiste toestemmingen om deze actie uit te voeren. Neem contact op met de beheerder om toegang aan te vragen. |
| 1020-400 | 400 | Uploaden en archiveren mislukt | Er is een probleem opgetreden tijdens het uploaden en archiveren van toegangsgegevens. Upload de toegangsgegevens en probeer het opnieuw. |
| 1021-400 | 400 | Taakfout | Een of meer privacytaken die zijn gemaakt op basis van de aanvraag zijn mislukt. Bekijk de details van de mislukte taken voor extra informatie. |
| 1022-400 | 400 | Fout bij toegang tot gegevens | Er is een probleem opgetreden tijdens de toegang tot de opgegeven gegevens. Controleer de taakdetails voor extra informatie. |
| 1023-400 | 400 | Fout bij toegang tot gegevens | Er is een probleem opgetreden tijdens het openen of zoeken van de opgegeven id&#39;s voor gegevenssets. Controleer of de opgegeven id&#39;s geldig zijn en probeer het opnieuw. |
| 1024-400 | 400 | Onverwachte fout | Er is een onverwachte fout opgetreden. Controleer de taakdetails voor extra informatie. |
| 1030-400 | 400 | Limiet voor documenttarief overschreden | De werkbelasting overschrijdt de documentsnelheidslimiet. Verlaag de verzendkosten en probeer het opnieuw. |
| 1040-400 | 400 | Toegangsfout voor sleutelversleuteling | De gegevens konden niet worden verwerkt omdat de datastore gecodeerd is en de toegang tot de sleutel is ingetrokken. Neem contact op met de beheerder van de sleutelkluis om de toegang tot de klantensleutel te herstellen. |
| 6000-200 | 200 | Succes | De taak is voltooid. Controleer de taakdetails om verwerkte verslagen en resultaten te bevestigen. |
| 6051 - 200 | 200 | Niet ingericht | Uw organisatie is niet ingericht voor de gevraagde toepassing. Het verzoek is niet van toepassing. |
| 6052-200 | 200 | Gebruikersnamen niet gevonden | Niet alle gebruikers-id&#39;s zijn gevonden en onbekende gebruikers-id&#39;s zijn niet van toepassing op dit product. Controleer of de gebruikers-id&#39;s geldig zijn en probeer het opnieuw. |
| 6053 - 200 | 200 | Ongeldige naamruimte | De opgegeven naamruimte voor de identiteit is niet geldig voor deze toepassing. Gebruik een naamruimte die door het systeem wordt herkend. |
| 6054-200 | 200 | Gedeeltelijk voltooid | De taak die is voltooid voor de toepasselijke gegevens, maar sommige gegevens waren niet van toepassing op de aanvraag. Controleer de taakdetails voor extra informatie. |

{style="table-layout:auto"}
