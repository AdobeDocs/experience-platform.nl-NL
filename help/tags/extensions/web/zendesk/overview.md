---
title: Zendesk event forward extension
description: Zendesk event forward extension for Adobe Experience Platform.
source-git-commit: ae585660bbf057f25e6f0dfc2520e6bb0af9d8d0
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 3%

---

# [!DNL Zendesk] Overzicht van de API-extensie voor gebeurtenissen

[Zendesk](https://www.zendesk.com) is een oplossing van de klantendienst en verkoophulpmiddel. De Zendesk [gebeurtenis doorsturen](../../../ui/event-forwarding/overview.md) extensie gebruikt de [[!DNL Zendesk Events API]](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) om gebeurtenissen van het Adobe Experience Platform Edge Network naar Zendesk te verzenden voor verdere verwerking. U kunt de uitbreiding gebruiken om de interactie van het klantenprofiel voor gebruik in stroomafwaartse analyse en actie te verzamelen.

In dit document wordt beschreven hoe u de extensie in de gebruikersinterface kunt installeren en configureren.

## Vereisten

U moet een Zendesk-account hebben om deze extensie te kunnen gebruiken. U kunt zich registreren voor een Zendesk-account op het tabblad [Zendesk-website](https://www.zendesk.com/register/).

U moet ook de volgende gegevens verzamelen voor uw Zendesk-configuratie:

| Type toets | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Subdomein | Tijdens het registratieproces is een unieke **subdomein** wordt specifiek voor de account gemaakt. Zie de [Documentatie van Zendesk](https://developer.zendesk.com/documentation/ticketing/working-with-oauth/creating-and-using-oauth-tokens-with-the-api/) voor meer informatie . | `xxxxx.zendesk.com` waarbij `xxxxx` is de waarde die is opgegeven tijdens het aanmaken van de account) |
| API-token | Zendesk gebruikt tokens aan toonder als verificatiemechanisme om te communiceren met de Zendesk-API. Nadat u zich hebt aangemeld bij de Zendesk-portal, genereert u een API-token. Zie de [Documentatie van Zendesk](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token) voor meer informatie . | `cwWyOtHAv12w4dhpiulfe9BdZFTz3OKaTSzn2QvV` |

{style=&quot;table-layout:auto&quot;}

Tot slot moet u een gebeurtenis tot stand brengen die geheim voor het API teken door:sturen. Het geheime type instellen op **[!UICONTROL Token]** en stel de waarde in op het API-token dat u hebt opgehaald bij uw Zendesk-configuratie. Raadpleeg de documentatie bij [geheimen in gebeurtenis die door:sturen](../../../ui/event-forwarding/secrets.md) voor meer details bij het vormen geheimen.

## De extensie installeren {#install}

Als u de Zendesk-extensie wilt installeren in de gebruikersinterface, navigeert u naar **Gebeurtenis doorsturen** en selecteer een eigenschap waaraan u de extensie wilt toevoegen of waarvoor u een nieuwe eigenschap wilt maken.

Wanneer u de gewenste eigenschap hebt geselecteerd of gemaakt, navigeert u naar **Extensies** > **Catalogus**. Zoeken naar &quot;[!DNL Zendesk]&quot;, en selecteer dan **[!DNL Install]** over de extensie Zendesk.

![Installatieknop voor de Zendesk-extensie die wordt geselecteerd in de gebruikersinterface](../../../images/extensions/zendesk/install.png)

## De extensie configureren {#configure}

>[!IMPORTANT]
>
>Afhankelijk van uw implementatiebehoeften, kunt u een schema, gegevenselementen, en een dataset tot stand moeten brengen alvorens de uitbreiding te vormen. Controleer alle configuratiestappen voordat u begint om te bepalen welke entiteiten u moet instellen voor uw geval van gebruik.

Selecteren **Extensies** in de linkernavigatie. Onder **Geïnstalleerd**, selecteert u **Configureren** over de extensie Zendesk.

![De knop Configureren voor de Zendesk-extensie die wordt geselecteerd in de gebruikersinterface](../../../images/extensions/zendesk/configure.png)

Onder **[!UICONTROL Zendesk Domain]**, voert u de waarde in voor uw Zendesk-subdomein. Onder **[!UICONTROL Zendesk Token]** Selecteer het geheim dat u eerder hebt gemaakt en dat de API-token bevat.

![Configuratieopties ingevuld in de gebruikersinterface](../../../images/extensions/zendesk/input.png)

## Vorm een gebeurtenis door:sturen regel

Begin creërend een nieuwe gebeurtenis door:sturen regel [regel](../../../ui/managing-resources/rules.md) en configureer de voorwaarden naar wens. Selecteer bij het selecteren van de handelingen voor de regel de optie [!UICONTROL Splunk] en selecteert u vervolgens de extensie [!UICONTROL Create Event] actietype.

![Regel definiëren](../../../images/extensions/zendesk/rule.png)

Wanneer u de actieconfiguratie instelt, wordt u gevraagd gegevenselementen toe te wijzen aan de verschillende eigenschappen die naar Zendesk worden verzonden.

![Configuratie van handeling definiëren](../../../images/extensions/zendesk/action-configurations.png)

Deze gegevenselementen moeten worden toegewezen zoals hieronder wordt vermeld.

### `event` toetsen

`event` is een JSON-object dat de gebeurtenis vertegenwoordigt die door de gebruiker wordt geactiveerd. Raadpleeg het Zendesk-document op het tabblad [anatomie van een gebeurtenis](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/) voor meer informatie over de eigenschappen die door de `event` object.

Naar de volgende toetsen kan worden verwezen binnen de `event` object bij toewijzing aan gegevenselementen:

| `event` key | Type | Pad Platform | Beschrijving | Verplicht | Limieten |
| --- | --- | --- | --- | --- | --- |
| `source` | Tekenreeks | `arc.event.xdm._extconndev.event_source` | De toepassing die de gebeurtenis heeft verzonden. | Ja | Niet gebruiken `Zendesk` als een waarde omdat het een beschermde bronnaam voor standaardgebeurtenissen van Zendesk is. Pogingen om het te gebruiken zullen in een fout resulteren.<br>De waarde mag niet langer zijn dan 40 tekens. |
| `type` | Tekenreeks | `arc.event.xdm._extconndev.event_type` | Een naam voor het gebeurtenistype. Met dit veld kunt u verschillende soorten gebeurtenissen voor een bepaalde bron aangeven. U kunt bijvoorbeeld een set gebeurtenissen maken voor gebruikersaanmeldingen en een andere set voor winkelwagentjes. | Ja | De waarde mag niet langer zijn dan 40 tekens. |
| `description` | Tekenreeks | `arc.event.xdm._extconndev.description` | Een beschrijving van de gebeurtenis. | Nee | (N.v.t.) |
| `created_at` | Tekenreeks | `arc.event.xdm.timestamp` | Een ISO-8601-tijdstempel die de tijd weergeeft waarop de gebeurtenis is gemaakt. | Nee | (N.v.t.) |
| `properties` | Object | `arc.event.xdm._extconndev.EventProperties` | Een aangepast JSON-object met informatie over de gebeurtenis. | Ja | (N.v.t.) |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Zie de [[!DNL Zendesk Events API] documentatie](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) voor aanvullende informatie over eigenschappen van gebeurtenissen.

### `profile` toetsen

`profile` is een JSON-object dat de gebruiker vertegenwoordigt die de gebeurtenis heeft geactiveerd. Raadpleeg het Zendesk-document op het tabblad [anatomie van een profiel](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/) voor meer informatie over de eigenschappen die door de `profile` object.

Naar de volgende toetsen kan worden verwezen binnen de `profile` object bij toewijzing aan gegevenselementen:

| `profile` key | Type | Pad Platform | Beschrijving | Verplicht | Limieten |
| --- | --- | --- | --- | --- | --- |
| `source` | Tekenreeks | `arc.event.xdm._extconndev.profile_source` | Het product dat of de service die aan het profiel is gekoppeld, zoals `Support`, `CompanyName`, of `Chat`. | Ja | (N.v.t.) |
| `type` | Tekenreeks | `arc.event.xdm._extconndev.profile_type` | Een naam voor het profieltype. U kunt dit veld gebruiken om verschillende soorten profielen voor een bepaalde bron te maken. U kunt bijvoorbeeld een set bedrijfsprofielen maken voor klanten en een andere voor werknemers. | Ja | De lengte van het profieltype mag niet langer zijn dan 40 tekens. |
| `name` | Tekenreeks | `arc.event.xdm._extconndev.name` | De naam van de persoon uit het profiel | Nee | (N.v.t.) |
| `user_id` | Tekenreeks | `arc.event.xdm._extconndev.user_id` | De gebruikersnaam van de persoon in Zendesk. | Nee | (N.v.t.) |
| `identifiers` | Array | `arc.event.xdm._extconndev.identifiers` | Een array met ten minste één id. Elke id bestaat uit een type en een waarde. | Ja | Zie de [Documentatie van Zendesk](https://developer.zendesk.com/api-reference/custom-data/profiles_api/profiles_api/#identifiers-array) voor meer informatie over de `identifiers` array. Alle velden en waarden moeten uniek zijn. |
| `attributes` | Object | `arc.event.xdm._extconndev.attrbutes` | Een object dat door de gebruiker gedefinieerde eigenschappen over de persoon bevat. | Nee | Zie de [Documentatie van Zendesk](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/#attributes) voor meer informatie over profielkenmerken. |

{style=&quot;table-layout:auto&quot;}

## Gegevens valideren in Zendesk {#validate}

Als de gebeurtenisverzameling en Adobe Experience Platform-integratie succesvol zijn, worden de gebeurtenissen in de Zendesk-console weergegeven zoals hieronder wordt weergegeven. Dit wijst op een succesvolle integratie.

Profielen:

![Pagina Profielen van Zendesk](../../../images/extensions/zendesk/zendesk-profiles.png)

Gebeurtenissen:

![Pagina Zendesk Events](../../../images/extensions/zendesk/zendesk-events.png)

## Aanvraaglimieten {#limits}

Op basis van het accounttype [!DNL Events API] U kunt het volgende aantal aanvragen per minuut afhandelen:

| [!DNL Account Type] | Verzoeken per minuut |
| --- | --- |
| [!DNL Team] | 250 |
| [!DNL Growth] | 250 |
| [!DNL Professional] | 500 |
| [!DNL Enterprise] | 750 |
| [!DNL Enterprise Plus] | 1000 |

{style=&quot;table-layout:auto&quot;}

Zie de [Documentatie van Zendesk](https://developer.zendesk.com/api-reference/ticketing/account-configuration/usage_limits/#:~:text=API%20requests%20made%20by%20Zendesk%20apps%20are%20subject,sources%20for%20the%20account%2C%20including%20internal%20product%20requests.) voor meer informatie over deze limieten .

## Fouten en problemen oplossen {#errors-and-troubleshooting}

Tijdens het gebruik of het configureren van de extensie kunnen de onderstaande fouten worden geretourneerd door de Zendesk Events API:

| Foutcode | Beschrijving | Resolutie | Voorbeeld |
|---|---|---|---|
| 400 | **Ongeldige profiellengte:** Deze fout treedt op wanneer de lengte van een profielkenmerk meer dan 40 tekens bevat. | Beperk de lengte van de profielkenmerkgegevens tot maximaal 40 tekens. | `{"error": [{"code":"InvalidProfileTypeLength","title": "Profile type length > 40 chars"}]}` |
| 401 | **Route niet gevonden:** Deze fout treedt op wanneer een ongeldig domein is opgegeven. | Controleer of een geldig domein in de volgende indeling wordt opgegeven: `{subdomain}.zendesk.com` | `{"error": [{"description": "No route found for host {subdomain}.zendesk.com","title": "RouteNotFound"}]}` |
| 401 | **Ongeldige of ontbrekende verificatie:** Deze fout treedt op wanneer de toegang tot het token ongeldig is, ontbreekt of verlopen is. | Controleer of het toegangstoken geldig is en niet verlopen is. | `{"error": [{"code":"MissingOrInvalidAuthentication","title": "Invalid or Missing Authentication"}]}` |
| 403 | **Onvoldoende machtigingen:** Deze fout treedt op wanneer er onvoldoende rechten zijn om toegang te krijgen tot de bron. | Controleer of de vereiste machtigingen zijn opgegeven. | `{"error": [{"code":"PermissionDenied","title": "Insufficient permisssions to perform operation"}]}` |
| 429 | **Te veel verzoeken:** Deze fout treedt op wanneer de recordlimiet voor eindpuntobjecten is overschreden. | Zie de sectie hierboven op [aanvraaglimieten](#limits) voor nadere bijzonderheden over de drempelwaarden per grenswaarde. | `{"error": [{"code":"TooManyRequests","title": "Too Many Requests"}]}` |

{style=&quot;table-layout:auto&quot;}

## Volgende stappen

In dit document wordt beschreven hoe u de Zendesk-gebeurtenis kunt installeren en configureren voor het doorsturen van de extensie in de gebruikersinterface. Raadpleeg de officiële documentatie voor meer informatie over het verzamelen van gebeurtenisgegevens in Zendesk:

* [Aan de slag met gebeurtenissen](https://developer.zendesk.com/documentation/custom-data/events/getting-started-with-events/)
* [Zendesk Events API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/)
* [Informatie over de API voor gebeurtenissen](https://developer.zendesk.com/documentation/custom-data/events/about-the-events-api/)
* [Anatomie van een gebeurtenis](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/)
* [Zendesk Profiles-API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/#profile-object)
* [De API voor profielen](https://developer.zendesk.com/documentation/custom-data/profiles/about-the-profiles-api/)
* [Anatomie van een profiel](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/)
