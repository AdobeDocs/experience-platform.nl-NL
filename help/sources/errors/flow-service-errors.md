---
title: Flow Service-foutberichten
description: Leer over de foutenmeldingen die u wanneer het gebruiken van de Dienst van de Stroom voor bronnen kunt ontmoeten.
exl-id: af79c547-25d0-459a-8de7-eb14206a8694
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 0%

---

# Foutberichten voor Flow Service

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen Experience Platform. De service biedt een gebruikersinterface en RESTful API waarmee u eenvoudig bronverbindingen met verschillende gegevensproviders kunt instellen. Deze bronverbindingen laten u toe om uw derdesystemen voor authentiek te verklaren, tijden voor ingestitielooppas te plaatsen, en gegevensinvoer te beheren.

Dit document bevat een catalogus met foutberichten, beschrijvingen en voorgestelde resoluties over Flow Service.

## Interne validatiefouten in Flow Service

In de volgende tabel worden fouten met betrekking tot interne validatie in Flow Service beschreven.

| Foutcode | Titel | Gedetailleerd bericht |
| --- | --- | --- |
| `1100-400` | Ongeldig verzoek | Het verzoek kan niet worden verwerkt. Fout van flowprovider: heeft geen recht op deze bewerking. |
| `1101-404` | Bron niet gevonden | De gevraagde bron is niet gevonden. Fout van flowprovider: resource met opgegeven id bestaat niet. |
| `1102-500` | Interne fout | Er is een interne fout opgetreden. Probeer het opnieuw. Neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1103-503` | Service niet beschikbaar | De service is tijdelijk niet beschikbaar. Probeer het opnieuw. Neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1104-504` | Time-out gateway | Er is een time-out opgetreden bij de gateway. Probeer het opnieuw. Neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1400-500` | Interne fout | Er is een interne fout opgetreden. Probeer het opnieuw. Neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1401-400` | Ongeldig verzoek | De parameter voor limiet en aantal kunnen niet samen in hetzelfde verzoek worden gegeven. Geef alleen de limiet of de parameter count op en probeer het opnieuw. |
| `1402-400` | Ongeldig verzoek | De handeling &#39;finalize&#39; wordt alleen ondersteund voor providerverzoeken. |
| `1403-400` | Koptekst ontbreekt | De koptekst &#39;If-Match&#39; ontbreekt in de aanvraag. Geef de koptekst op en probeer het opnieuw. |
| `1404-412` | Versie komt niet overeen | De geleverde versie &#39;v1&#39; komt niet overeen met de huidige versie op entiteit &#39;cc01fc2c-0000-0200&#39;. Zorg ervoor dat de geleverde versie overeenkomt met de huidige versie op entiteit en probeer het opnieuw. |
| `1405-400` | Ongeldig verzoek | De aanvraaginstantie mag niet null of leeg zijn. Geef een aanvraaginstantie op en probeer het opnieuw. |
| `1406-400` | Ongeldig verzoek | De subbewerking &#39;progress&#39; kan niet worden toegepast met andere subtransacties. Werk de lijst met subbewerkingen bij en probeer het opnieuw. |
| `1407-400` | Ongeldig verzoek | De status is mislukt. Kan niet worden gebruikt met `progress` subOp. Verwijder de `progress` subOp of gebruik status=&#39;inProgress&#39; en probeer het opnieuw. |
| `1408-400` | Ongeldig verzoek | Het percentage-voltooide zou 100 voor de voltooide of ontbroken staten moeten zijn. Werk het voltooide percentage bij en probeer het opnieuw. |
| `1409-400` | Ongeldig verzoek | De bewerking &#39;finalize&#39; kan niet worden toegepast op het huidige ingeschakelde frame. Werk de bewerking bij en probeer het opnieuw. |
| `1410-400` | Ongeldig verzoek | `State` is niet toegestaan in de aanvraag voor het maken van doorloop. |
| `1411-400` | Ongeldig verzoek | Kan entiteit-id niet ophalen. Ongeldig verzoek ontvangen met pad &#39;baseConnections/123&#39;. |
| `1412-400` | Ongeldig verzoek | Ongeldige toewijzingsversie in aanvraag. Geef de juiste toewijzingsversie op. |
| `1413-400` | Ongeldig verzoek | De opgegeven specificatie-id is ongeldig. Geef een geldige specificatie-id op en probeer het opnieuw. |
| `1414-400` | Ongeldig verzoek | De verbindingsspecificatie van een verbinding kan niet worden bijgewerkt. |
| `1415-400` | Ongeldig verzoek | De auth-specificatie &#39;authConnection&#39; is niet gevonden voor de verbindingsspecificatie ID ba6e206f-f233-ab16. |
| `1416-400` | Ongeldig verzoek | Verwijderen of bijwerken kan alleen worden toegepast op een verbinding met de status ingeschakeld, uitgeschakeld of geïnitialiseerd. |
| `1417-400` | Ongeldig verzoek | Verwijderen of Bijwerken op verbindingen in de status `initializing` is niet toegestaan met UserToken. |
| `1418-400` | Ongeldig verzoek | De basisverbinding met ID 35dcaad3-122a-4278 kan niet worden geschrapt omdat de basisverbinding in één of meerdere stromen wordt gebruikt. Zorg ervoor dat de corresponderende stromen worden verwijderd voordat u een basisverbinding verwijdert. |
| `1419-400` | Ongeldig verzoek | Fout bij valideren van toewijzing met id 45d90285d2d249acb87a72a2f12f7401, versie 0. Dit kan te wijten zijn aan ontoereikende machtigingen voor toegewezen velden. Controleer uw toewijzing of neem contact op met uw beheerder. |
| `1420-400` | Ongeldig verzoek | De huidige status die wordt uitgeschakeld, kan niet worden bijgewerkt. |
| `1421-400` | Ongeldig verzoek | Het bijwerken van de huidige status kan niet worden overgezet. |
| `1422-400` | Ongeldig verzoek | De handeling uitschakelen kan niet worden toegepast op het huidige frame {state} . Werk de handeling bij en probeer het opnieuw. |
| `1423-400` | Ongeldig verzoek | Een niet-afgehandelde field baseSpec werd verstrekt in ConnectionSpecFiltering. Werk het veld {field} bij en probeer het opnieuw. |
| `1424-400` | Ongeldig verzoek | OrderBy wordt niet ondersteund met sandboxquery&#39;s voor verschillende sandboxen. |
| `1425-400` | Ongeldig verzoek | Fout bij het afstemmen van het schema in de doelgegevensset 64ef1a3c0ef met het schema in toewijzing 91ac5a2c0eb. Het schema met zelfde identiteitskaart en de versie moeten in zowel afbeelding als doeldataset worden gebruikt. |
| `1426-400` | Ongeldig verzoek | Het gebruikerstoken is niet geautoriseerd om de verbindingsspecificatie te maken/bijwerken. Controleer of de gebruikerstoken is geautoriseerd en probeer het opnieuw. |
| `1427-400` | Ongeldig verzoek | Het gebruikerstoken is onbevoegd om stroomlooppas tot stand te brengen/bij te werken. Controleer of de gebruikerstoken is geautoriseerd en probeer het opnieuw. |
| `1428-400` | Ongeldig verzoek | Voorgangersstroom niet gevonden met id aa6a206f-f233-4c2d. |
| `1429-400` | Ongeldig verzoek | Voorgangersstroom niet gevonden met id aa6a206f-f233-4c2d. |
| `1430-400` | Ongeldig verzoek | Stroom niet gevonden met id aa6a206f-f233-4c2d. |
| `1431-400` | Ongeldig verzoek | Lege array &#39;fields&#39; is niet toegestaan in beleid. |
| `1432-400` | Ongeldig verzoek | De opgegeven sorteervolgorde is niet correct, prepend + voor oplopende volgorde en - voor aflopende volgorde in fieldName. |
| `1433-400` | Ongeldig verzoek | Onjuist veld= #id is doorgegeven in orderBy, bijvoorbeeld +name, -name, name. |
| `1434-400` | Ongeldig verzoek | Niet-ondersteunde bewerking &#39;move&#39; ontvangen. Gebruik een van de ondersteunde bewerkingstypen en probeer het opnieuw. |
| `1435-400` | Ongeldig verzoek | Niet-ondersteunde subactie &#39;reverse&#39; ontvangen. Gebruik een van de ondersteunde subactietypen en probeer het opnieuw. |
| `1436-400` | Ongeldig verzoek | Niet-ondersteunde sub-operation PROGRESS ontvangen voor operation enable. |
| `1437-400` | Ongeldig verzoek | Niet-ondersteunde statuswaarde &#39;started&#39; ontvangen. Werk de statuswaarde bij en probeer het opnieuw. |
| `1438-400` | Ongeldig verzoek | Niet-ondersteunde aggregaatbewerking &#39;gemiddelde&#39; ontvangen. |
| `1439-400` | Bron niet gevonden | De gevraagde stroombron 3f4ae131-b384-4e73 is niet gevonden. Controleer de bron-id voordat u het opnieuw probeert. |
| `1440-400` | Ongeldig verzoek | Operator &#39;~&#39; niet geïmplementeerd. |
| `1441-400` | Ongeldig verzoek | Geaggregeerde functie &#39;average&#39; niet geïmplementeerd. |
| `1442-400` | Ongeldig verzoek | Samenvoegen niet toegestaan op veld-id. |
| `1443-400` | Ongeldig verzoek | Operator &#39;&lt;=&#39; is niet toegestaan voor meerdere waarden. |
| `1444-400` | Ongeldig verzoek | Flow 3f4ae131-b384-4e73 bevindt zich niet in de verwachte toestand. |
| `1445-400` | Ongeldig verzoek | PATCH Connection Feature not enabled. |
| `1446-400` | Ongeldig verzoek | De flow-id mag niet null of leeg zijn. Werk de flow-id bij en probeer het opnieuw. |
| `1447-400` | Ongeldig verzoek | Gevonden actieve stromen met id aa6a206f-f233-4c2d. |
| `1448-400` | Ongeldig verzoek | Operator >= niet ondersteund voor veld-id. |
| `1449-400` | Ongeldig verzoek | Ongeldige veldverbindingen in filterparams. |
| `1450-400` | Ongeldig verzoek | Ongeldige operator!> in filterparams. |
| `1451-400` | Ongeldig verzoek | Ongeldige params testParam verstrekt in vraagparams. |
| `1452-400` | Ongeldig verzoek | Ongeldige waarde 1676643256,1676643210 voor veld createdAt. |
| `1453-400` | Ongeldig verzoek | Ongeldige vraagwaarde createdAt= die in vraagparam wordt verstrekt. |
| `1454-400` | Ongeldig verzoek | Niet-afgehandeld type filterwaarde opgegeven. |
| `1455-400` | Ongeldig verzoek | Er is een fout opgetreden tijdens het valideren van patchinstructies: ontbrekend veld &quot;keyDoesNotExist&quot;. |
| `1456-400` | Ongeldig verzoek | Het definitief maken van frames is geen geldige waarde. Toegestane waarden worden [ toegelaten, gehandicapt, initialiserend ]. |
| `1457-400` | Ongeldig verzoek | Bewerking-update kan niet worden toegepast bij het voltooien van de status delete. |
| `1458-400` | Ongeldig verzoek | Bewerking verwijderen kan niet worden toegepast bij het voltooien van een bewerking. |

{style="table-layout:auto"}


## Verificatiefouten van gebruikerstoken voor autorisatie

De volgende tabel bevat een overzicht van fouten met betrekking tot de verificatie van de gebruikerstoken voor autorisatie

| Foutcode | Titel | Gedetailleerd bericht |
| --- | --- | --- |
| `2000-401` | Ongeldig machtigingstoken | De machtigingstoken heeft geen toegang tot deze organisatie of de organisatie bestaat niet. Controleer of de organisatie bestaat of neem contact op met uw beheerder voor toegang. |
| `2001-401` | Koptekst ontbreekt of is leeg | De header x-gw-ims-org-id ontbreekt of is leeg. Werk de koptekstwaarde bij en probeer het opnieuw. |
| `2002-401` | Koptekst ontbreekt | De header x-gw-ims-org-id ontbreekt in de aanvraag. Werk de koptekstwaarde bij en probeer het opnieuw. |
| `2100-404` | Sandbox niet gevonden | De sandbox met de naam &#39;dev&#39; is niet gevonden. Controleer of de naam van de sandbox correct is en probeer het opnieuw. |
| `2101-404` | Sandbox niet gevonden | De sandbox met de naam &#39;dev&#39; is niet gevonden. Fout in Sandbox Management API: sandbox met naam &#39;dev&#39; niet aanwezig. Controleer of de bron bestaat. |
| `2102-500` | Sandbox ophalen op naamfout | Er is een probleem opgetreden bij het ophalen van een sandbox met de naam &#39;dev&#39;. Fout door Sandbox Management API: er is iets misgegaan. Probeer het opnieuw. |
| `2103-404` | Sandbox niet gevonden | De sandbox met ID 8da3ef09-b469-404a en name dev zijn niet gevonden. Controleer of de waarden voor de ID- en sandboxnaam correct zijn en probeer het opnieuw. |
| `2104-500` | Sandbox ophalen door id-fout | Er is een probleem opgetreden bij het ophalen van een sandbox met de id &#39;8da3ef09-b469-404a&#39; en de naam &#39;dev&#39;. Fout door Sandbox Management API: er is iets misgegaan. Probeer het opnieuw. |
| `2105-400` | Koptekst ontbreekt | De naam van de header x-sandbox ontbreekt in de aanvraag. Voeg de koptekst toe aan de aanvraag en probeer het opnieuw. |
| `2106-404` | Standaardsandboxfout ophalen | De standaardinformatie voor de sandbox kan niet worden gevonden. |
| `2107-500` | Standaardsandboxfout ophalen | Er is een probleem opgetreden bij het ophalen van een standaardsandbox. Fout door Sandbox Management API: er is iets misgegaan. Probeer het opnieuw. |
| `2108-500` | Fout bij ophalen actieve sandboxen | Er is een probleem opgetreden bij het ophalen van een actieve sandbox. Fout door Sandbox Management API: er is iets misgegaan. Probeer het opnieuw. |
| `2110-400` | Kopteksten zijn niet toegestaan | De header x-sandbox-id is niet toegestaan met de gebruikerstoken. Werk de koptekst bij en probeer het opnieuw. |
| `2111-403` | Kopteksten met beperkte waarde | De naam van de header x-sandbox met waarde * is beperkt met de gebruikerstoken. Werk de koptekst en de waarde bij en probeer het opnieuw. |
| `2112-400` | Kopteksten met een andere waarde zijn niet toegestaan | De headers x-sandbox-name en x-sandbox-id moeten beide de waarde * hebben voor cross-sandbox query. Werk de kopteksten bij en probeer het opnieuw. |
| `2113-400` | Kopteksten met waarde niet toegestaan | De headers x-sandbox-id en x-sandbox-name met waarde * zijn niet toegestaan voor de aanvraag. Werk de kopteksten bij en probeer het opnieuw. |
| `2114-400` | Leeg token | Leeg token opgegeven. Geef een token op en probeer het opnieuw. |
| `2115-400` | Ongeldig token | Er is een ongeldig token opgegeven. Geef een geldige token op en probeer het opnieuw. |
| `2116-500` | Interne fout | Er is een interne fout opgetreden tijdens het offline decoderen van een token voor bereikresolutie. |
| `2117-500` | Interne fout | Er is een interne fout opgetreden bij het controleren van de machtigingen voor de gebruiker. Probeer het opnieuw. Neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `2118-403` | Ontbrekende machtiging | De machtiging voor schrijven ontbreekt. Neem contact op met de beheerder om de machtigingen op te lossen en probeer het opnieuw. |
| `2119-400` | Zoekparameter ontbreekt | De aanvraagcontext bevat niet de vereiste specificeerId van de vraagparameter. Geef de ontbrekende queryparameter op en probeer het opnieuw. |
| `2120-403` | Verboden | U hebt onvoldoende machtigingen om de bewerking uit te voeren. Neem contact op met de beheerder om de machtigingen op te lossen en probeer het opnieuw. |
| `2121-403` | Verboden | Het machtigingenbeheer wordt geweigerd op resource Enterprise Source. Neem contact op met de beheerder om de machtigingen op te lossen en probeer het opnieuw. |
| `2200-500` | Fout bij verzoek externe service | Er is een probleem opgetreden tijdens het aanroepen van de Catalogusservice voor het valideren van het schema. |
| `2250-500` | Fout bij verzoek externe service | Er is een probleem opgetreden tijdens het aanroepen van de Data Prep-service voor het valideren van toewijzingen. |

{style="table-layout:auto"}
