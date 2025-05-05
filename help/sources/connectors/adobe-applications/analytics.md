---
title: Adobe Analytics Source Connector voor Report-Suite Data
description: Dit document biedt een overzicht van Analytics en beschrijft de gebruiksgevallen voor Analytics-gegevens.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 0%

---

# Adobe Analytics-bronaansluiting voor rapportsuite-gegevens

Met Adobe Experience Platform kunt u Adobe Analytics-gegevens invoeren via de bronconnector van Analytics. De [!DNL Analytics] bronconnector streamt gegevens die door [!DNL Analytics] in realtime naar Experience Platform zijn verzameld, waarbij gegevens met SCDS-indeling [!DNL Analytics] worden omgezet in [!DNL Experience Data Model] (XDM)-velden voor gebruik door Experience Platform.

Dit document biedt een overzicht van [!DNL Analytics] en beschrijft de mogelijke toepassingen van [!DNL Analytics] -gegevens.

## Adobe Analytics- en analysegegevens

[!DNL Analytics] is een krachtige engine waarmee u meer kunt leren over uw klanten, hoe ze met uw wegeigenschappen werken, kunt zien waar uw uitgaven voor digitale marketing effectief zijn en verbeteringsgebieden kunt identificeren. Met [!DNL Analytics] worden biljoenen webtransacties per jaar afgehandeld en met de [!DNL Analytics] -bronconnector kunt u eenvoudig tikken op deze rijke gedragsgegevens en de [!DNL Real-Time Customer Profile] binnen enkele minuten verrijken.

![ grafisch die A de reis van gegevens van verschillende toepassingen van Adobe, met inbegrip van Adobe Analytics illustreert.](./images/analytics-data-experience-platform.png)

Op hoog niveau verzamelt [!DNL Analytics] gegevens via verschillende digitale kanalen en meerdere datacenters over de hele wereld. Zodra de gegevens worden verzameld, worden de de Identificatie van de Bezoeker, de Regels van de Segmentatie en van de Transformatie van de Architectuur (VISTA), en verwerkingsregels toegepast om de inkomende gegevens te vormen. Nadat onbewerkte gegevens deze lichte verwerking hebben doorlopen, wordt deze vervolgens als gebruiksklaar beschouwd door [!DNL Real-Time Customer Profile] . In een parallel aan het bovenstaande proces worden dezelfde verwerkte gegevens op micro-basis gebatcheerd en opgenomen in Experience Platform-gegevenssets voor gebruik door [!DNL Query Service] en andere toepassingen voor gegevensdetectie.

Zie het [ overzicht van verwerkingsregels ](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=nl) voor meer informatie over verwerkingsregels.

## Experience-datamodel (XDM)

XDM is een openbaar gedocumenteerde specificatie die gemeenschappelijke structuren en definities voor een toepassing verstrekt om met de diensten op Experience Platform te gebruiken te communiceren.

Door te voldoen aan XDM-standaarden kunnen gegevens op uniforme wijze worden opgenomen, waardoor het eenvoudiger wordt om gegevens te leveren en informatie te verzamelen.

Om meer over XDM te leren, te zien gelieve het [ XDM overzicht van het Systeem ](../../../xdm/home.md).

## Hoe worden velden toegewezen van Adobe Analytics aan XDM?

>[!IMPORTANT]
>
>Transformaties van de Prep van gegevens kunnen latentie aan algemene dataflow toevoegen. De extra toegevoegde latentie is afhankelijk van de complexiteit van de transformatielogica.

Wanneer een bronverbinding tot stand is gebracht voor het verzenden van [!DNL Analytics] -gegevens naar Experience Platform via de Experience Platform-gebruikersinterface, worden gegevensvelden automatisch toegewezen aan en opgenomen in [!DNL Real-Time Customer Profile] binnen enkele minuten. Voor instructies bij het creëren van een bronverbinding met [!DNL Analytics] gebruikend Experience Platform UI, zie het [ Van de bron Analyse schakelaarleerprogramma ](../../tutorials/ui/create/adobe-applications/analytics.md).

Voor gedetailleerde informatie over de gebiedstoewijzing die tussen [!DNL Analytics] en Experience Platform voorkomt, zie de [ het gebiedstoewijzing van Adobe Analytics ](./mapping/analytics.md) gids.

## Wat is de verwachte latentie voor Analytics Data on Experience Platform?

De verwachte latentie voor Analytics Data on Experience Platform wordt in de onderstaande tabel beschreven. De latentie zal afhankelijk van klantenconfiguratie, gegevensvolumes, en de toepassingen van de consument variëren. Bijvoorbeeld, als de implementatie van Analytics met `A4T` wordt gevormd zal de latentie aan Pijpleiding tot 5-10 minuten stijgen.

| Analysegegevens | Verwachte vertraging |
| -------------- | ---------------- |
| Nieuwe gegevens aan [!DNL Real-Time Customer Profile] (A4T **&#x200B;**&#x200B;toegelaten niet) | &lt; 2 minuten |
| Nieuwe gegevens aan [!DNL Real-Time Customer Profile] (A4T **wordt** toegelaten) | tot 30 minuten |
| Nieuwe gegevens voor Data Lake | &lt; 2,25 uur |
| Nieuwe gegevens aan Customer Journey Analytics zonder [ stitching ](https://experienceleague.adobe.com/docs/analytics-platform/using/stitching/overview.html?lang=en) | &lt; 3,75 uur |
| Nieuwe gegevens voor Customer Journey Analytics met stitching | &lt; 7 uur |
| Terugvulling van gebeurtenissen van minder dan 10 miljard | &lt; 4 weken |

Voor meer informatie over de latentie van Customer Journey Analytics, zie: [ Guardrails van Customer Journey Analytics ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html?lang=en).

De back-up van Analytics voor productiesandboxen wordt standaard ingesteld op 13 maanden. Voor analysegegevens in niet-productiesandboxen wordt de backfill ingesteld op drie maanden. De limiet van 10 miljard gebeurtenissen die in bovenstaande tabel worden genoemd, is strikt in verhouding tot de verwachte latentie.

Wanneer u een bron van de Analyse gegevens in een productiesandbox creeert, worden twee gegevensstromen gecreeerd:

* Een dataflow die een 13 maanden backfill van historische gegevens van de rapportreeks in gegevens meer doet. Deze gegevensstroom eindigt wanneer de backfill volledig is.
* Een dataflow-flow die live-gegevens verzendt naar het data-meer en [!DNL Real-Time Customer Profile] . Deze gegevensstroom wordt voortdurend uitgevoerd.

>[!NOTE]
>
>Back-upvulgegevens voor analysemogelijkheden worden niet opgenomen in [!DNL Profile] en worden dus niet opgenomen in licentieprofielen.

## Primaire id&#39;s in [!DNL Analytics] gegevens

Elke hit van de [!DNL Analytics] -bronconnector bevat een primaire id die afhankelijk is van het feit of een ECID of een AID bestaat. Als er een ECID is, wordt de ECID aangewezen als primaire identificator. Als er sprake is van steun, wordt de steun als primaire steun aangemerkt.

De volgende tabel bevat meer informatie over identiteitsvelden in uw [!DNL Analytics] -gegevens.

| Identiteitsveld | Beschrijving |
| --- | --- |
| STEUN | De HULP is de primaire apparaat-id in Adobe Analytics en is gegarandeerd aanwezig op elke gebeurtenis die via de [!DNL Analytics] -bron wordt doorgegeven. AID wordt soms bedoeld als *identiteitskaart van de Analyse van de Oudheid* of als `s_vi` koekjesidentiteitskaart Ondanks dit, wordt een STEUN gecreeerd zelfs als het `s_vi` koekje niet aanwezig is. AID wordt vertegenwoordigd door `post_visid_high` en `post_visid_low` kolommen in [[!DNL Analytics]  gegevensvoer ](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Voor om het even welke bepaalde gebeurtenis, bevat het gebied van STEUN één enkele identiteit die één van de verscheidene verschillende types kan zijn die in de [ orde van verrichtingen voor  [!DNL Analytics]  worden beschreven IDs ](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Nota**: Binnen een volledige rapportenreeks, kan AID een mengeling van types over gebeurtenissen bevatten. |
| ECID | De ECID (Experience Cloud-id) is een apart veld voor apparaat-id dat in Adobe Analytics wordt ingevuld wanneer [!DNL Analytics] wordt geïmplementeerd met de Experience Cloud Identity Service. De ECID wordt ook wel MCID (Marketing Cloud ID) genoemd. Als ECID op een gebeurtenis bestaat, kan STEUN op ECID afhankelijk van worden gebaseerd of de Analytics [ respijtperiode ](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) wordt gevormd. De ECID wordt vertegenwoordigd door de `mcvisid` in de gegevensinvoer Analytics. Voor meer informatie over ECID, zie het [ overzicht ECID ](../../../identity-service/features/ecid.md). Voor informatie over hoe ECID met [!DNL Analytics] werkt, zie het document op [ Analytics en de Verzoeken van identiteitskaart van Experience Cloud ](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html). |
| AACUSTOMID | De AACUSTOMID is een apart identifier-veld dat in Adobe Analytics wordt ingevuld op basis van het gebruik van de variabele `s.VisitorID` in de [!DNL Analytics] -implementatie. AACUSTOMID wordt vertegenwoordigd door de `cust_visid` kolom in [[!DNL Analytics]  gegevensvoer ](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Als AACUSTOMID aanwezig is, dan zal STEUN op AACUSTOMID worden gebaseerd omdat AACUSTOMID alle andere herkenningstekens zoals die door de [ orde van verrichtingen voor  [!DNL Analytics]  IDs ](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html) worden bepaald. |

### Hoe de [!DNL Analytics] -bron omgaat met identiteiten

De [!DNL Analytics] -bron geeft deze identiteiten als volgt door aan Experience Platform in XDM-vorm:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Deze velden zijn niet gemarkeerd als identiteiten. In plaats daarvan worden dezelfde identiteiten (indien aanwezig in de gebeurtenis) als sleutel-waardeparen naar XDM `identityMap` gekopieerd:

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

Wanneer de identiteit of identiteiten naar `identityMap` worden gekopieerd, wordt `endUserIDs._experience.mcid.namespace.code` ook ingesteld op dezelfde gebeurtenis:

* Als AID aanwezig is, wordt `endUserIDs._experience.aaid.namespace.code` ingesteld op &quot;AID&quot;.
* Als ECID aanwezig is, wordt `endUserIDs._experience.mcid.namespace.code` ingesteld op ECID.
* Als AACUSTOMID aanwezig is, wordt `endUserIDs._experience.aacustomid.namespace.code` ingesteld op &quot;AACUSTOMID&quot;.

Als ECID aanwezig is in het identiteitsoverzicht, wordt dit gemarkeerd als de primaire identiteit voor de gebeurtenis. In dit geval, kan de STEUN op ECID wegens de [ periode van de de respijtperiode van de Dienst van de Identiteit ](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) worden gebaseerd. Anders wordt STEUN gemarkeerd als de primaire identiteit voor de gebeurtenis. AACUSTOMID is nooit gemarkeerd als primaire id voor de gebeurtenis. Als AACUSTOMID echter aanwezig is, is de STEUN gebaseerd op AACUSTOMID vanwege de volgorde van Experience Cloud.

>[!NOTE]
>
>U kunt de Prep van Gegevens gebruiken om secundaire identiteiten uit Analytics, zoals STEUN en AACUSTOMID uit te filtreren. Als deze id&#39;s worden uitgefilterd, worden deze id&#39;s niet opgenomen in Profiel als ze beschikbaar zijn in de inkomende analysegegevens. Ongefilterde gegevens blijven in het datumpomeer worden geladen.
