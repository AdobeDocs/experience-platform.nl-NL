---
title: Adobe Target-implementatie met Adobe Experience Platform Debugger testen
description: Leer hoe u Adobe Experience Platform Debugger kunt gebruiken om een website die met Adobe Target is ingeschakeld, te testen en er fouten in op te sporen.
exl-id: f99548ff-c6f2-4e99-920b-eb981679de2d
source-git-commit: bc6069f2cfa4459860fe98588b293ffeed7fb1f1
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 0%

---

# Een Adobe Target-implementatie met Adobe Experience Platform Debugger testen

Adobe Experience Platform Debugger biedt een reeks nuttige hulpmiddelen voor het testen van en het opsporen van fouten in een website die is uitgerust met een Adobe Target-implementatie. In deze handleiding vindt u een aantal algemene workflows en aanbevolen procedures voor het gebruik van Platform Debugger op een website die geschikt is voor Doel.

## Vereisten

Als u Platform Debugger wilt gebruiken voor Doel, moet de website de functie [at.js-bibliotheek](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/) versie 1.x of hoger. Vorige versies worden niet ondersteund.

## Platformfoutopsporing initialiseren

Open de website die u wilt testen in een browser en open vervolgens de extensie Platform Debugger.

Selecteren **[!DNL Target]** in de linkernavigatie. Als Foutopsporing van het Platform ontdekt dat een compatibele versie van at.js op de plaats loopt, worden de de implementatiedetails van Adobe Target getoond.

![De doelweergave die is geselecteerd in Foutopsporing op platform, geeft aan dat Adobe Target actief is op de momenteel weergegeven browserpagina](../images/solutions/target/target-initialized.png)

## Algemene configuratiegegevens

De informatie over de globale configuratie van de implementatie wordt getoond bij de bovenkant van de mening van het Doel in Debugger van het Platform.

![Algemene configuratiegegevens voor doel gemarkeerd in Foutopsporing van platform](../images/solutions/target/global-config.png)

| Naam | Beschrijving |
| --- | --- |
| Clientcode | Een unieke id die uw organisatie identificeert. |
| Versie | De versie van de Adobe Target-bibliotheek die momenteel op de website is geïnstalleerd. |
| Algemene aanvraagnaam | De naam van [global mbox](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?) voor de doelimplementatie, waarbij de standaardnaam `target-global-mbox`. |
| Gebeurtenis bij laden van pagina | Een Booleaanse waarde die aangeeft of een [page load, gebeurtenis](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams) heeft plaatsgevonden. Gebeurtenissen voor het laden van pagina&#39;s worden alleen ondersteund voor at.js 2.x. Voor niet-compatibele versies wordt deze waarde standaard ingesteld op `None`. |

{style="table-layout:auto"}

## [!DNL Network Requests] {#network}

Selecteren **[!DNL Network Requests]** om summiere informatie over elk netwerkverzoek te bekijken dat op de pagina wordt gemaakt.

![De [!DNL Network Requests] sectie voor doel geselecteerd in Foutopsporing van platform](../images/solutions/target/network-requests.png)

Terwijl u handelingen uitvoert op de pagina (inclusief het opnieuw laden van de pagina), worden automatisch nieuwe kolommen toegevoegd aan de tabel, zodat u de volgorde van handelingen kunt weergeven en kunt zien hoe waarden tussen elke aanvraag worden gewijzigd.

![De [!DNL Network Requests] sectie voor doel geselecteerd in Foutopsporing van platform](../images/solutions/target/new-request.png)

De volgende waarden worden vastgelegd:

| Naam | Beschrijving |
| --- | --- |
| [!DNL Page Title] | De titel van de pagina die deze aanvraag heeft geïnitieerd. |
| [!DNL Page URL] | De URL van de pagina die de aanvraag heeft geïnitieerd. |
| [!DNL URL] | De onbewerkte URL van de aanvraag. |
| [!DNL Method] | De HTTP-methode voor de aanvraag. |
| [!DNL Query String] | De queryreeks van de aanvraag, overgenomen van de URL. |
| [!DNL POST Body] | De hoofdtekst van het verzoek (alleen ingesteld voor verzoeken van POSTEN). |
| [!DNL Pathname] | De padnaam van de aanvraag-URL. |
| [!DNL Hostname] | De hostnaam van de aanvraag-URL. |
| [!DNL Domain] | Het domein van de aanvraag-URL. |
| [!DNL Timestamp] | Een tijdstempel van wanneer de aanvraag (of gebeurtenis) heeft plaatsgevonden, binnen de tijdzone van de browser. |
| [!DNL Time Since Page Load] | De verstreken tijd sinds de pagina aanvankelijk op het tijdstip van de aanvraag werd geladen. |
| [!DNL Initiator] | De aanvrager van de aanvraag. Met andere woorden, wie heeft het verzoek ingediend? |
| [!DNL clientCode] | De id voor de account van uw organisatie, zoals door Target wordt herkend. |
| [!DNL requestType] | De API die is gebruikt voor de aanvraag. Als u at.js 1.x gebruikt, is de waarde `/json`. Als u at.js 2.x gebruikt, is de waarde `delivery`. |
| [!DNL Audience Manager Blob] | Verstrekt informatie over gecodeerde die meta-gegevens van de Audience Manager als &quot;blob&quot;worden bedoeld. |
| [!DNL Audience Location Hint] | The data collection region ID. Dit is een numerieke id voor de geografische locatie van een bepaald datacenter van de ID-service. Raadpleeg de documentatie bij de Audience Manager over [Id&#39;s, locaties en hostnamen van DCS-regio&#39;s](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html) en de handleiding voor identiteitsdienst van Experiencen Cloud op [`getLocationHint`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html#reference-a761030ff06c4439946bb56febf42d4c). |
| [!DNL Browser Height] | De browserhoogte in pixels. |
| [!DNL Browser Time Offset] | De tijdverschuiving van de browser die is gekoppeld aan de tijdzone. |
| [!DNL Browser Width] | De browserbreedte in pixels. |
| [!DNL Color Depth] | De kleurdiepte van het scherm. |
| [!DNL context] | Een object dat contextuele informatie bevat over de browser die is gebruikt om de aanvraag uit te voeren, inclusief schermafmetingen en clientplatform. |
| [!DNL prefetch] | De parameters waarin wordt gebruikt tijdens `prefetch` verwerking. |
| [!DNL execute] | De parameters die tijdens worden gebruikt `execute` verwerking. |
| [!DNL Experience Cloud Visitor ID] | Als er een wordt gedetecteerd, geeft u informatie over de [Experience Cloud-id (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) die is toegewezen aan de huidige sitebezoeker. |
| [!DNL experienceCloud] | Bevat de Experience Cloud-id&#39;s voor deze specifieke gebruikerssessie: een A4T [aanvullende gegevens-id](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?#section_2C1F745A2B7D41FE9E30915539226E3A)en [bezoeker-id (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html). |
| [!DNL id] | De [Doel-id](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID) voor de bezoeker. |
| [!DNL Mbox Host] | De [host](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) dat het verzoek van Target is ingediend. |
| [!DNL Mbox PC] | Een tekenreeks die het [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) sessie-id en de [Adobe Target Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934) locatiehint. Deze waarde wordt door at.js gebruikt om ervoor te zorgen dat de zitting en de plaats van de Rand kleverig blijven. |
| [!DNL Mbox Referrer] | De URL-referentie voor de specifieke [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) verzoek. |
| [!DNL Mbox URL] | De URL voor de [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) server. |
| [!DNL Mbox Version] | De versie van [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) worden gebruikt. |
| [!DNL mbox3rdPartyId] | De [`mbox3rdPartyId`](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) toegewezen aan de huidige bezoeker. |
| [!DNL mboxRid] | De [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) aanvraag-id. |
| [!DNL requestId] | Een unieke id voor de aanvraag. |
| [!DNL Screen Height] | De hoogte van het scherm in pixels. |
| [!DNL Screen Width] | De breedte van het scherm in pixels. |
| [!DNL Supplemental Data ID] | Een door het systeem gegenereerde id die wordt gebruikt om bezoekers te koppelen aan de overeenkomende Adobe Target- en Adobe Analytics-aanroepen. Zie de [A4T-gids voor probleemoplossing](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?#section_75002584FA63456D8D9086172925DD8D) voor meer informatie . |
| [!DNL vst] | De [API-configuratie van Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html). |
| [!DNL webGLRenderer] | Verstrekt informatie over renderer WebGL die op de pagina wordt gebruikt, als toepasselijk. |

{style="table-layout:auto"}

Selecteer de tabelcel in kwestie om de details van een parameter voor een bepaalde netwerkgebeurtenis weer te geven. Er verschijnt een popover met nadere informatie over de parameter, waaronder een beschrijving en de waarde ervan. Als de waarde een JSON-object is, bevat het dialoogvenster een volledig navigeerbare weergave van de structuur van het object.

![De [!DNL Network Requests] sectie voor doel geselecteerd in Foutopsporing van platform](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

Selecteren **[!DNL Configuration]** om een selectie van extra het zuiveren hulpmiddelen voor Doel toe te laten of onbruikbaar te maken.

![De [!DNL Configuration Requests] sectie voor doel geselecteerd in Foutopsporing van platform](../images/solutions/target/configuration.png)

| Het gereedschap Foutopsporing | Beschrijving |
| --- | --- |
| [!DNL Target Console Logging] | Wanneer toegelaten, staat u tot de logboeken van at.js in de browser consoletabblad toegang. Deze functie kan ook worden ingeschakeld door een `mboxDebug` vraag (met om het even welke waarde) aan browser URL. |
| [!DNL Target Disable] | Als deze optie is ingeschakeld, worden alle functies van het doel op de pagina uitgeschakeld. Dit kan worden gebruikt om te bepalen als een specifiek aanbod van het Doel is wat de kwestie op de pagina veroorzaakt. |
| [!DNL Target Trace] | **Opmerking**: U moet zijn aangemeld om deze functie in te schakelen.<br><br>Als deze optie is ingeschakeld, worden trackingtokens verzonden bij elke query en wordt in elke reactie een trace-object geretourneerd. `at.js` parseert de reactie `window.__targetTraces`. Elk trace-object bevat dezelfde informatie als [[!DNL Network Requests] tab], met de volgende toevoegingen:<ul><li>Een profielmomentopname, die u toestaat om attributen vóór en na verzoeken te zien.</li><li>Gelijktijdig en niet-gematcht [activiteiten](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html), waaruit blijkt waarom het huidige profiel al dan niet in aanmerking kwam voor specifieke activiteiten.<ul><li>Dit kan helpen identificeren voor welk publiek een profiel op een bepaald punt in aanmerking komt, en waarom.</li><li>Doeldocumenten bevatten meer informatie over verschillende activiteitstypen</li></ul></li></ul> |

{style="table-layout:auto"}
