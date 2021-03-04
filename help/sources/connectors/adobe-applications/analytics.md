---
keywords: Experience Platform;home;populaire onderwerpen;Analytics Data Connector;analytics;Analytics
solution: Experience Platform
title: Adobe Analytics Source Connector voor rapportsuite-gegevens
topic: ' - overzicht'
description: Dit document biedt een overzicht van Analytics en beschrijft de gebruiksgevallen voor Analytics-gegevens.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 2%

---


# Adobe Analytics-connector voor rapportsuite-gegevens

Met Adobe Experience Platform kunt u Adobe Analytics-gegevens invoeren via de Analytics Data Connector (ADC). ADC streamt gegevens die door [!DNL Analytics] in real time worden verzameld tot [!DNL Platform], die SCDS-Geformatteerde [!DNL Analytics] gegevens in [!DNL Experience Data Model] (XDM) gebieden voor consumptie door [!DNL Platform] omzetten.

Dit document biedt een overzicht van [!DNL Analytics] en beschrijft de gebruiksgevallen voor [!DNL Analytics]-gegevens.

## Adobe Analytics- en analysegegevens

[!DNL Analytics] is een krachtige motor om u te helpen meer over uw klanten leren, hoe zij met uw Web-eigenschappen in wisselwerking staan, zien waar uw digitale marketing uitgaven efficiënt is, en gebieden van verbetering identificeren. [!DNL Analytics] verwerkt biljoenen webtransacties per jaar en ADC stelt u in staat om gemakkelijk gebruik te maken van deze rijke gedragsgegevens en deze  [!DNL Real-time Customer Profile] in enkele minuten te verrijken.

![](./images/analytics-data-experience-platform.png)

Op een hoog niveau verzamelt [!DNL Analytics] gegevens via verschillende digitale kanalen en meerdere datacenters over de hele wereld. Zodra de gegevens zijn verzameld, worden de regels van Visitor Identification, Segmentation and Transformation Architecture (VISTA) en de verwerkingsregels toegepast om de inkomende gegevens vorm te geven. Nadat de ruwe gegevens door deze lichtgewichtverwerking zijn gegaan, wordt het dan beschouwd klaar voor consumptie door [!DNL Real-time Customer Profile]. In een parallel aan het bovenstaande proces worden dezelfde verwerkte gegevens op micro-basis gebatcheerd en opgenomen in gegevenssets met Platforms voor gebruik door [!DNL Data Science Workspace], [!DNL Query Service] en andere toepassingen voor gegevensdetectie.

Zie [Overzicht van verwerkingsregels](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html) voor meer informatie over verwerkingsregels.

## Experience Data Model (XDM)

XDM is een openbaar gedocumenteerde specificatie die gemeenschappelijke structuren en definities voor een toepassing verstrekt om met de diensten op [!DNL Experience Platform] te gebruiken te communiceren.

Door te voldoen aan XDM-standaarden kunnen gegevens op uniforme wijze worden opgenomen, waardoor het eenvoudiger wordt om gegevens te leveren en informatie te verzamelen.

Voor meer informatie over XDM, te zien gelieve [XDM systeemoverzicht](../../../xdm/home.md).

## Hoe worden velden toegewezen van Adobe Analytics aan XDM?

Wanneer een bronverbinding tot stand is gebracht voor het overbrengen van [!DNL Analytics]-gegevens naar [!DNL Experience Platform] via de gebruikersinterface [!DNL Platform], worden gegevensvelden automatisch toegewezen en binnen minuten opgenomen in [!DNL Real-time Customer Profile]. Voor instructies over het creëren van een bronverbinding met [!DNL Analytics] gebruikend [!DNL Platform] UI, zie [de zelfstudie van de gegevensschakelaar van Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Voor gedetailleerde informatie over de gebiedstoewijzing die tussen [!DNL Analytics] en [!DNL Experience Platform] voorkomt, gelieve [Adobe Analytics gebied afbeelding](./mapping/analytics.md) gids te bezoeken.

## Wat is de verwachte latentie voor de Gegevens van Analytics over Platform?

| Analysegegevens | Verwachte vertraging |
| -------------- | ---------------- |
| Nieuwe gegevens naar [!DNL Real-time Customer Profile] (A4T **not** ingeschakeld) | &lt; 2=&quot;&quot; minutes=&quot;&quot;> |
| Nieuwe gegevens naar [!DNL Real-time Customer Profile] (A4T **is** ingeschakeld) | &lt; 15=&quot;&quot; minutes=&quot;&quot;> |
| Nieuwe gegevens voor Data Lake | &lt; 90=&quot;&quot; minutes=&quot;&quot;> |
| Backfill-gegevens (13 maanden of 10 miljard gebeurtenissen, afhankelijk van welke waarde lager is) | &lt; 4=&quot;&quot; weeks=&quot;&quot;> |

>[!NOTE]
>
>De latentie zal afhankelijk van klantenconfiguratie, gegevensvolumes, en de toepassingen van de consument variëren. Bijvoorbeeld, als de implementatie van Analytics met `A4T` wordt gevormd zal de latentie aan Pijpleiding tot 5-10 minuten stijgen.

## Primaire id-id&#39;s in analysegegevens

Elke hit van de gegevensconnector Analytics bevat een primaire id die afhankelijk is van het feit of een ECID of een AID bestaat. Als er een ECID is, wordt de ECID aangewezen als primaire identificator. Als er sprake is van steun, wordt de steun als primaire steun aangemerkt.