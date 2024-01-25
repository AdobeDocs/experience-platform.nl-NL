---
title: Adobe Analytics Source Connector voor rapportsuite-gegevens
description: Dit document biedt een overzicht van Analytics en beschrijft de gebruiksgevallen voor Analytics-gegevens.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: b82bbdf7957e5a8d331d61f02293efdaf878971c
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 0%

---

# Adobe Analytics-bronaansluiting voor rapportsuite-gegevens

Met Adobe Experience Platform kunt u Adobe Analytics-gegevens invoeren via de bronconnector van Analytics. De [!DNL Analytics] bronverbindingsstromen gegevens verzameld door [!DNL Analytics] naar Platform in real time, converterend SCDS-Geformatteerd [!DNL Analytics] gegevens in [!DNL Experience Data Model] (XDM) velden voor gebruik door Platform.

Dit document biedt een overzicht van [!DNL Analytics] en beschrijft de gebruiksgevallen voor [!DNL Analytics] gegevens.

## Adobe Analytics- en analysegegevens

[!DNL Analytics] is een krachtige motor die u meer over uw klanten helpt leren, hoe zij met uw Web-eigenschappen in wisselwerking staan, zien waar uw digitale marketing uitgaven efficiënt is, en gebieden van verbetering identificeren. [!DNL Analytics] verwerkt miljarden webtransacties per jaar en de [!DNL Analytics] Met de bronaansluiting kunt u eenvoudig op deze rijke gedragsgegevens tikken en de [!DNL Real-Time Customer Profile] over een paar minuten.

![Een afbeelding die de reis van gegevens uit verschillende toepassingen van de Adobe, met inbegrip van Adobe Analytics illustreert.](./images/analytics-data-experience-platform.png)

Op hoog niveau [!DNL Analytics] verzamelt gegevens via verschillende digitale kanalen en meerdere datacenters over de hele wereld. Zodra de gegevens worden verzameld, worden de de Identificatie van de Bezoeker, de Regels van de Segmentatie en van de Transformatie van de Architectuur (VISTA), en verwerkingsregels toegepast om de inkomende gegevens te vormen. Nadat de ruwe gegevens door deze lichte verwerking zijn gegaan, wordt het dan beschouwd klaar voor consumptie door [!DNL Real-Time Customer Profile]. In een parallel aan het bovenstaande proces worden dezelfde verwerkte gegevens op micro-basis verzameld en opgenomen in gegevenssets van het platform, die door [!DNL Query Service]en andere toepassingen voor gegevensdetectie.

Zie de [overzicht van verwerkingsregels](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=nl) voor meer informatie over verwerkingsregels.

## Experience Data Model (XDM)

XDM is een openbaar gedocumenteerde specificatie die gemeenschappelijke structuren en definities voor een toepassing verstrekt om met de diensten op Experience Platform te communiceren te gebruiken.

Door te voldoen aan XDM-standaarden kunnen gegevens op uniforme wijze worden opgenomen, waardoor het eenvoudiger wordt om gegevens te leveren en informatie te verzamelen.

Voor meer informatie over XDM raadpleegt u de [XDM System, overzicht](../../../xdm/home.md).

## Hoe worden velden toegewezen van Adobe Analytics aan XDM?

>[!IMPORTANT]
>
>Transformaties van de Prep van gegevens kunnen latentie aan algemene dataflow toevoegen. De extra toegevoegde latentie is afhankelijk van de complexiteit van de transformatielogica.

Wanneer een bronverbinding wordt gevestigd voor het brengen [!DNL Analytics] gegevens in Experience Platform die de gebruikersinterface van het Platform gebruiken, worden de gegevensgebieden automatisch in kaart gebracht en opgenomen in [!DNL Real-Time Customer Profile] binnen minuten. Voor instructies over het maken van een bronverbinding met [!DNL Analytics] het gebruiken van Platform UI, zie [Zelfstudie over de bronaansluiting voor analyse](../../tutorials/ui/create/adobe-applications/analytics.md).

Voor gedetailleerde informatie over veldtoewijzing tussen [!DNL Analytics] en Experience Platform, zie [Adobe Analytics-veldtoewijzing](./mapping/analytics.md) hulplijn.

## Wat is de verwachte latentie voor de Gegevens van Analytics op Platform?

De verwachte latentie voor Analytics Data on Platform wordt beschreven in de onderstaande tabel. De latentie zal afhankelijk van klantenconfiguratie, gegevensvolumes, en de toepassingen van de consument variëren. Bijvoorbeeld als de implementatie Analytics is geconfigureerd met `A4T` de latentie naar de pijpleiding zal toenemen tot 5-10 minuten.

| Analysegegevens | Verwachte vertraging |
| -------------- | ---------------- |
| Nieuwe gegevens naar [!DNL Real-Time Customer Profile] (A4T **niet** ingeschakeld) | &lt; 2 minuten |
| Nieuwe gegevens naar [!DNL Real-Time Customer Profile] (A4T **is** ingeschakeld) | tot 30 minuten |
| Nieuwe gegevens voor Data Lake | &lt; 2,25 uur |
| Terugvulling van gebeurtenissen van minder dan 10 miljard | &lt; 4 weken |

De back-up van Analytics voor productiesandboxen wordt standaard ingesteld op 13 maanden. Voor analysegegevens in niet-productiesandboxen wordt de backfill ingesteld op drie maanden. De limiet van 10 miljard gebeurtenissen die in bovenstaande tabel worden genoemd, is strikt in verhouding tot de verwachte latentie.

Wanneer u een bron van de Analyse gegevens in een productiesandbox creeert, worden twee gegevensstromen gecreeerd:

* Een dataflow die een 13 maanden backfill van historische gegevens van de rapportreeks in gegevens meer doet. Deze gegevensstroom eindigt wanneer de backfill volledig is.
* Een dataflow-flow die live gegevens verzendt naar data Lake en naar [!DNL Real-Time Customer Profile]. Deze gegevensstroom wordt voortdurend uitgevoerd.

>[!NOTE]
>
>Analytics backfill data is not ingepakt in [!DNL Profile] en dus niet in licentieprofielen wordt opgenomen.

## Primaire id&#39;s in [!DNL Analytics] data

Elke keer dat de [!DNL Analytics] De bronschakelaar bevat een primaire herkenningsteken die afhankelijk is van of ECID of een STEUN bestaat. Als er een ECID is, wordt de ECID aangewezen als primaire identificator. Als er sprake is van steun, wordt de steun als primaire steun aangemerkt.

De volgende tabel bevat meer informatie over identiteitsvelden in uw [!DNL Analytics] gegevens.

| Identiteitsveld | Beschrijving |
| --- | --- |
| STEUN | De HULP is de primaire apparaat-id in Adobe Analytics en is gegarandeerd aanwezig op elke gebeurtenis die via de [!DNL Analytics] bron. De steun wordt soms de *Verouderde analyse-id* of als de `s_vi` cookie-id. Desondanks wordt een steunmaatregel ingesteld, zelfs als de `s_vi` cookie is niet aanwezig. De STEUN wordt vertegenwoordigd door de `post_visid_high` en `post_visid_low` kolommen in [[!DNL Analytics] gegevensfeeds](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Voor elke gebeurtenis bevat het veld STEUN één identiteit die een van de verschillende typen kan zijn die in het [volgorde van werkzaamheden voor [!DNL Analytics] ID&#39;s](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Opmerking**: Binnen een volledige rapportenreeks, kan AID een mengeling van types over gebeurtenissen bevatten. |
| ECID | De ECID (Experience Cloud-id) is een apart veld voor apparaat-id dat in Adobe Analytics wordt ingevuld wanneer [!DNL Analytics] wordt geïmplementeerd met de Experience Cloud Identity Service. De ECID wordt ook wel MCID (Marketing Cloud-ID) genoemd. Als er een ECID bestaat voor een gebeurtenis, kan de STEUN gebaseerd zijn op ECID, afhankelijk van of de Analytics [respijtperiode](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) is geconfigureerd. De ECID wordt vertegenwoordigd door de `mcvisid` in Analytics-gegevensfeeds. Voor meer informatie over ECID raadpleegt u de [ECID-overzicht](../../../identity-service/features/ecid.md). Voor informatie over hoe ECID werkt met [!DNL Analytics], zie het document op [Verzoeken voor analyse en Experience Cloud-id](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html). |
| AACUSTOMID | De AACUSTOMID is een apart identificatieveld dat in Adobe Analytics wordt ingevuld op basis van het gebruik van de `s.VisitorID` in de [!DNL Analytics] uitvoering. De AACUSTOMID wordt vertegenwoordigd door de `cust_visid` kolom in [[!DNL Analytics] gegevensfeeds](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Als de AACUSTOMID aanwezig is, zal de STEUN gebaseerd zijn op de AACUSTOMID, omdat de AACUSTOMID alle andere id&#39;s zoals gedefinieerd door de [volgorde van werkzaamheden voor [!DNL Analytics] ID&#39;s](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### Hoe [!DNL Analytics] bron behandelt identiteiten

De [!DNL Analytics] De bron geeft deze identiteiten aan Experience Platform in vorm XDM als over:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Deze velden zijn niet gemarkeerd als identiteiten. In plaats daarvan worden dezelfde identiteiten gekopieerd naar XDM&#39;s `identityMap` als sleutel-waardeparen:

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

Als ECID aanwezig is in het identiteitsoverzicht, wordt dit gemarkeerd als de primaire identiteit voor de gebeurtenis. In dat geval kan de steun op ECID gebaseerd zijn vanwege de [Abonnementsserviceperiode](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). Anders wordt STEUN gemarkeerd als de primaire identiteit voor de gebeurtenis. AACUSTOMID is nooit gemarkeerd als primaire id voor de gebeurtenis. Als AACUSTOMID echter aanwezig is, is de STEUN gebaseerd op AACUSTOMID vanwege de volgorde van de Experiencen Cloud.

>[!NOTE]
>
>U kunt de Prep van Gegevens gebruiken om secundaire identiteiten uit Analytics, zoals STEUN en AACUSTOMID uit te filtreren. Als deze id&#39;s worden uitgefilterd, worden deze id&#39;s niet opgenomen in Profiel als ze beschikbaar zijn in de inkomende analysegegevens. Ongefilterde gegevens blijven in het datumpomeer worden geladen.
