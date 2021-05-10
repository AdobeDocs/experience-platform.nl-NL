---
keywords: Experience Platform;home;populaire onderwerpen;Analytics Source Connector;analytics;Analytics
solution: Experience Platform
title: Adobe Analytics Source Connector voor rapportsuite-gegevens
topic-legacy: overview
description: Dit document biedt een overzicht van Analytics en beschrijft de gebruiksgevallen voor Analytics-gegevens.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
translation-type: tm+mt
source-git-commit: af5ad975bbfd6a67fe66c90e33da1365d49c8899
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 1%

---

# Adobe Analytics-bronaansluiting voor rapportsuite-gegevens

Met Adobe Experience Platform kunt u Adobe Analytics-gegevens invoeren via de bronconnector van Analytics. De [!DNL Analytics] gegevens van de bronschakelaar stromen die door [!DNL Analytics] in Platform in real time worden verzameld, die SCDS-Geformatteerde [!DNL Analytics] gegevens in [!DNL Experience Data Model] (XDM) gebieden voor consumptie door Platform omzetten.

Dit document biedt een overzicht van [!DNL Analytics] en beschrijft de gebruiksgevallen voor [!DNL Analytics]-gegevens.

## Adobe Analytics- en analysegegevens

[!DNL Analytics] is een krachtige motor die u meer over uw klanten helpt leren, hoe zij met uw Web-eigenschappen in wisselwerking staan, zien waar uw digitale marketing uitgaven efficiënt is, en gebieden van verbetering identificeren. [!DNL Analytics] verwerkt biljoenen webtransacties per jaar en met de  [!DNL Analytics] bronaansluiting kunt u eenvoudig op deze rijke gedragsgegevens tikken en de gegevens  [!DNL Real-time Customer Profile] in een paar minuten verrijken.

![](./images/analytics-data-experience-platform.png)

Op een hoog niveau verzamelt [!DNL Analytics] gegevens via verschillende digitale kanalen en meerdere datacenters over de hele wereld. Zodra de gegevens worden verzameld, worden de de Identificatie van de Bezoeker, de Regels van de Segmentatie en van de Transformatie van de Architectuur (VISTA), en verwerkingsregels toegepast om de inkomende gegevens te vormen. Nadat de ruwe gegevens door deze lichtgewichtverwerking zijn gegaan, wordt het dan beschouwd klaar voor consumptie door [!DNL Real-time Customer Profile]. In een parallel aan het bovenstaande proces worden dezelfde verwerkte gegevens op micro-basis gebatcheerd en opgenomen in gegevenssets met Platforms voor gebruik door [!DNL Data Science Workspace], [!DNL Query Service] en andere toepassingen voor gegevensdetectie.

Zie [verwerkingsregels overzicht](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html) voor meer informatie over verwerkingsregels.

## Experience Data Model (XDM)

XDM is een openbaar gedocumenteerde specificatie die gemeenschappelijke structuren en definities voor een toepassing verstrekt om met de diensten op Experience Platform te communiceren te gebruiken.

Door te voldoen aan XDM-standaarden kunnen gegevens op uniforme wijze worden opgenomen, waardoor het eenvoudiger wordt om gegevens te leveren en informatie te verzamelen.

Voor meer informatie over XDM, te zien gelieve [XDM systeemoverzicht](../../../xdm/home.md).

## Hoe worden velden toegewezen van Adobe Analytics aan XDM?

Wanneer een bronverbinding tot stand wordt gebracht voor het brengen van [!DNL Analytics] gegevens in Experience Platform gebruikend het gebruikersinterface van het Platform, worden de gegevensgebieden automatisch in kaart gebracht en in [!DNL Real-time Customer Profile] binnen notulen opgenomen. Voor instructies bij het creëren van een bronverbinding met [!DNL Analytics] die de UI van het Platform gebruiken, zie [de leerprogramma van de bronschakelaar van de Analyse](../../tutorials/ui/create/adobe-applications/analytics.md).

Voor gedetailleerde informatie over de gebiedstoewijzing die tussen [!DNL Analytics] en Experience Platform voorkomt, zie [het gebiedstoewijzing van Adobe Analytics](./mapping/analytics.md) gids.

## Wat is de verwachte latentie voor de Gegevens van Analytics over Platform?

| Analysegegevens | Verwachte vertraging |
| -------------- | ---------------- |
| Nieuwe gegevens naar [!DNL Real-time Customer Profile] (A4T **not** ingeschakeld) | &lt; 2=&quot;&quot; minutes=&quot;&quot;> |
| Nieuwe gegevens naar [!DNL Real-time Customer Profile] (A4T **is** ingeschakeld) | &lt; 15=&quot;&quot; minutes=&quot;&quot;> |
| Nieuwe gegevens voor Data Lake | &lt; 90=&quot;&quot; minutes=&quot;&quot;> |
| Backfill-gegevens (13 maanden of 10 miljard gebeurtenissen, afhankelijk van welke waarde lager is) | &lt; 4=&quot;&quot; weeks=&quot;&quot;> |

>[!NOTE]
>
>De latentie zal afhankelijk van klantenconfiguratie, gegevensvolumes, en de toepassingen van de consument variëren. Bijvoorbeeld, als [!DNL Analytics] implementatie met `A4T` wordt gevormd zal de latentie aan Pijpleiding tot 5-10 minuten stijgen.

## Primaire id&#39;s in [!DNL Analytics]-gegevens

Elke hit van de [!DNL Analytics] bronconnector bevat een primaire id die afhankelijk is van het feit of een ECID of een AID bestaat. Als er een ECID is, wordt de ECID aangewezen als primaire identificator. Als er sprake is van steun, wordt de steun als primaire steun aangemerkt.
