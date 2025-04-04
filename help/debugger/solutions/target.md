---
title: Adobe Target-implementatie met Adobe Experience Platform Debugger testen
description: Leer hoe u Adobe Experience Platform Debugger kunt gebruiken om een website die met Adobe Target is ingeschakeld, te testen en er fouten in op te sporen.
exl-id: f99548ff-c6f2-4e99-920b-eb981679de2d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 0%

---

# Een Adobe Target-implementatie met Adobe Experience Platform Debugger testen

Adobe Experience Platform Debugger beschikt over een reeks nuttige hulpmiddelen voor het testen van en het opsporen van fouten in een website die is uitgerust met een Adobe Target-implementatie. In deze handleiding vindt u een aantal gangbare workflows en tips en trucs voor het gebruik van Experience Platform Debugger op een website met Target.

## Vereisten

Om Foutopsporing van Experience Platform voor Doel te gebruiken, moet de website [ at.js bibliotheek ](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/) versie 1.x of hoger gebruiken. Vorige versies worden niet ondersteund.

## Experience Platform Debugger initialiseren

Open de website die u wilt testen in een browser en open vervolgens de extensie Experience Platform Debugger.

Selecteer **[!DNL Target]** in de linkernavigatie. Als Foutopsporing van Experience Platform ontdekt dat een compatibele versie van at.js op de plaats loopt, worden de de implementatiedetails van Adobe Target getoond.

![ de mening van het Doel die in Foutopsporing van Experience Platform wordt geselecteerd, erop wijzend dat Adobe Target op de momenteel bekeken browser pagina ](../images/solutions/target/target-initialized.png) actief is

## Algemene configuratiegegevens

De informatie over de globale configuratie van de implementatie wordt getoond bij de bovenkant van de mening van het Doel in Foutopsporing van Experience Platform.

![ Globale configuratieinformatie voor Doel die binnen Debugger van Experience Platform wordt benadrukt ](../images/solutions/target/global-config.png)

| Naam | Beschrijving |
| --- | --- |
| Clientcode | Een unieke id die uw organisatie identificeert. |
| Versie | De versie van de Adobe Target-bibliotheek die momenteel op de website is geïnstalleerd. |
| Algemene aanvraagnaam | De naam van [ globale mbox ](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?) voor de implementatie van het Doel, die de standaardnaam `target-global-mbox` is. |
| Gebeurtenis bij laden van pagina | Een booleaanse waarde erop wijst die of de gebeurtenis van de a [ paginading ](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams) heeft plaatsgevonden. Gebeurtenissen voor het laden van pagina&#39;s worden alleen ondersteund voor at.js 2.x. Voor niet-compatibele versies wordt deze waarde standaard ingesteld op `None` . |

{style="table-layout:auto"}

## [!DNL Network Requests] {#network}

Selecteer **[!DNL Network Requests]** om summiere informatie over elke netwerkverzoek te bekijken die op de pagina wordt gemaakt.

![ de [!DNL Network Requests] sectie voor Doel binnen Debugger van Experience Platform wordt geselecteerd ](../images/solutions/target/network-requests.png)

Terwijl u handelingen uitvoert op de pagina (inclusief het opnieuw laden van de pagina), worden automatisch nieuwe kolommen toegevoegd aan de tabel, zodat u de volgorde van handelingen kunt weergeven en kunt zien hoe waarden tussen elke aanvraag worden gewijzigd.

![ de [!DNL Network Requests] sectie voor Doel binnen Debugger van Experience Platform wordt geselecteerd ](../images/solutions/target/new-request.png)

De volgende waarden worden vastgelegd:

| Naam | Beschrijving |
| --- | --- |
| [!DNL Page Title] | De titel van de pagina die deze aanvraag heeft geïnitieerd. |
| [!DNL Page URL] | De URL van de pagina die de aanvraag heeft geïnitieerd. |
| [!DNL URL] | De onbewerkte URL van de aanvraag. |
| [!DNL Method] | De HTTP-methode voor de aanvraag. |
| [!DNL Query String] | De queryreeks van de aanvraag, overgenomen van de URL. |
| [!DNL POST Body] | De hoofdtekst van het verzoek (alleen ingesteld voor POST-verzoeken). |
| [!DNL Pathname] | De padnaam van de aanvraag-URL. |
| [!DNL Hostname] | De hostnaam van de aanvraag-URL. |
| [!DNL Domain] | Het domein van de aanvraag-URL. |
| [!DNL Timestamp] | Een tijdstempel van wanneer de aanvraag (of gebeurtenis) heeft plaatsgevonden, binnen de tijdzone van de browser. |
| [!DNL Time Since Page Load] | De verstreken tijd sinds de pagina aanvankelijk op het tijdstip van de aanvraag werd geladen. |
| [!DNL Initiator] | De aanvrager van de aanvraag. Met andere woorden, wie heeft het verzoek ingediend? |
| [!DNL clientCode] | De id voor de account van uw organisatie, zoals door Target wordt herkend. |
| [!DNL requestType] | De API die is gebruikt voor de aanvraag. Als u at.js 1.x gebruikt, is de waarde `/json`. Als u at.js 2.x gebruikt, is de waarde `delivery` . |
| [!DNL Audience Manager Blob] | Biedt informatie over gecodeerde Audience Manager-metagegevens die de &#39;blob&#39; worden genoemd. |
| [!DNL Audience Location Hint] | The data collection region ID. Dit is een numerieke id voor de geografische locatie van een bepaald datacenter van de ID-service. Voor meer informatie, zie de documentatie van Audience Manager over [ DCS Gebied IDs, Locaties, en de Namen van de Gastheer ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html) en de gids van de Dienst van de Identiteit van Experience Cloud op [`getLocationHint` ](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html#reference-a761030ff06c4439946bb56febf42d4c). |
| [!DNL Browser Height] | De browserhoogte in pixels. |
| [!DNL Browser Time Offset] | De tijdverschuiving van de browser die is gekoppeld aan de tijdzone. |
| [!DNL Browser Width] | De browserbreedte in pixels. |
| [!DNL Color Depth] | De kleurdiepte van het scherm. |
| [!DNL context] | Een object dat contextuele informatie bevat over de browser die is gebruikt om de aanvraag uit te voeren, inclusief schermafmetingen en clientplatform. |
| [!DNL prefetch] | De parameters die worden gebruikt tijdens `prefetch` -verwerking. |
| [!DNL execute] | De parameters die tijdens `execute` verwerking worden gebruikt. |
| [!DNL Experience Cloud Visitor ID] | Als wordt ontdekt, verstrekt informatie over [ identiteitskaart van Experience Cloud (ECID) ](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) die aan de huidige plaatsbezoeker wordt toegewezen. |
| [!DNL experienceCloud] | Houdt Experience Cloud IDs voor deze specifieke gebruikerszitting: A4T [ extra gegevens identiteitskaart ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?#section_2C1F745A2B7D41FE9E30915539226E3A), en identiteitskaart van de a [ bezoeker (ECID) ](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html). |
| [!DNL id] | [ identiteitskaart van het Doel ](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID) voor de bezoeker. |
| [!DNL Mbox Host] | De [ gastheer ](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) dat het verzoek van het Doel werd gemaakt aan. |
| [!DNL Mbox PC] | Een koord dat [`mbox` ](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) zittingsidentiteitskaart en [ Adobe Target Edge ](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934) plaatshint inkapselt. Deze waarde wordt door at.js gebruikt om ervoor te zorgen dat de zitting en de plaats van Edge kleverig blijven. |
| [!DNL Mbox Referrer] | De verwijzing URL voor het specifieke [`mbox` ](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) verzoek. |
| [!DNL Mbox URL] | De URL voor de [`mbox` ](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) server. |
| [!DNL Mbox Version] | De versie van [`mbox` ](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) die wordt gebruikt. |
| [!DNL mbox3rdPartyId] | De [`mbox3rdPartyId` ](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) die aan de huidige bezoeker wordt toegewezen. |
| [!DNL mboxRid] | De [`mbox` ](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) verzoek-id. |
| [!DNL requestId] | Een unieke id voor de aanvraag. |
| [!DNL Screen Height] | De hoogte van het scherm in pixels. |
| [!DNL Screen Width] | De breedte van het scherm in pixels. |
| [!DNL Supplemental Data ID] | Een door het systeem gegenereerde id die wordt gebruikt om bezoekers te koppelen aan de overeenkomende Adobe Target- en Adobe Analytics-aanroepen. Zie [ A4T het oplossen van problemengids ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?#section_75002584FA63456D8D9086172925DD8D) voor meer informatie. |
| [!DNL vst] | De [ configuratie van de Dienst API van de Identiteit van Experience Cloud ](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html). |
| [!DNL webGLRenderer] | Verstrekt informatie over renderer WebGL die op de pagina wordt gebruikt, als toepasselijk. |

{style="table-layout:auto"}

Selecteer de tabelcel in kwestie om de details van een parameter voor een bepaalde netwerkgebeurtenis weer te geven. Er verschijnt een popover met nadere informatie over de parameter, waaronder een beschrijving en de waarde ervan. Als de waarde een JSON-object is, bevat het dialoogvenster een volledig navigeerbare weergave van de structuur van het object.

![ de [!DNL Network Requests] sectie voor Doel binnen Debugger van Experience Platform wordt geselecteerd ](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

Selecteer **[!DNL Configuration]** om een selectie van extra foutopsporingsgereedschappen voor Doel in of uit te schakelen.

![ de [!DNL Configuration Requests] sectie voor Doel binnen Debugger van Experience Platform wordt geselecteerd ](../images/solutions/target/configuration.png)

| Het gereedschap Foutopsporing | Beschrijving |
| --- | --- |
| [!DNL Target Console Logging] | Wanneer toegelaten, staat u tot de logboeken van at.js in de browser consoletabblad toegang. Deze functie kan ook worden ingeschakeld door een `mboxDebug` query-param (met elke waarde) toe te voegen aan de URL van de browser. |
| [!DNL Target Disable] | Als deze optie is ingeschakeld, worden alle functies van het doel op de pagina uitgeschakeld. Dit kan worden gebruikt om te bepalen als een specifiek aanbod van het Doel is wat de kwestie op de pagina veroorzaakt. |
| [!DNL Target Trace] | **Nota**: U moet worden het programma geopend om deze eigenschap toe te laten.<br><br> wanneer toegelaten, wordt het volgen tokens verzonden met elke vraag, en een spoorvoorwerp is teruggekeerd in elke reactie. `at.js` parseert het antwoord `window.__targetTraces` . Elk spoorvoorwerp bevat de zelfde informatie zoals [[!DNL Network Requests] tabel], met de volgende toevoegingen:<ul><li>Een profielmomentopname, die u toestaat om attributen vóór en na verzoeken te zien.</li><li>Gelijke en niet overtroffen [ activiteiten ](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html), die tonen waarom het huidige profiel voor specifieke activiteiten of niet kwalificeerde.<ul><li>Dit kan helpen identificeren voor welk publiek een profiel op een bepaald punt in aanmerking komt, en waarom.</li><li>Doeldocumenten bevatten meer informatie over verschillende activiteitstypen</li></ul></li></ul> |

{style="table-layout:auto"}
