---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gegevensconnector Analytics
topic: overview
translation-type: tm+mt
source-git-commit: 662ca170b7416dfb55cfb6b8cbaef640c1f83d31
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 2%

---


# Gegevensconnector Analytics

Met Adobe Experience Platform kunt u Adobe Analytics-gegevens invoeren via de Analytics Data Connector (ADC). ADC streamt gegevens die door [!DNL Analytics] aan [!DNL Platform] in real time worden verzameld, die [!DNL Analytics] gegevens SCDS-formatted in [!DNL Experience Data Model] (XDM) gebieden voor consumptie door [!DNL Platform]. omzetten

Dit document biedt een overzicht van [!DNL Analytics] en een beschrijving van de gebruikte [!DNL Analytics] gegevens.

## Adobe Analytics- en analysegegevens

[!DNL Analytics] is een krachtige motor om u te helpen meer over uw klanten leren, hoe zij met uw Web-eigenschappen in wisselwerking staan, zien waar uw digitale marketing uitgaven efficiënt is, en gebieden van verbetering identificeren. [!DNL Analytics] verwerkt biljoenen webtransacties per jaar en ADC stelt u in staat om gemakkelijk gebruik te maken van deze rijke gedragsgegevens en deze binnen enkele minuten te verrijken. [!DNL Real-time Customer Profile]

![](./images/analytics-data-experience-platform.png)

Op hoog niveau worden gegevens verzameld via verschillende digitale kanalen en meerdere datacenters over de hele wereld. [!DNL Analytics] Zodra de gegevens zijn verzameld, worden de regels van Visitor Identification, Segmentation and Transformation Architecture (VISTA) en de verwerkingsregels toegepast om de inkomende gegevens vorm te geven. Nadat de ruwe gegevens door deze lichte verwerking zijn gegaan, wordt het dan beschouwd klaar voor consumptie door [!DNL Real-time Customer Profile]. In een parallel aan het bovenstaande proces worden dezelfde verwerkte gegevens op micro-basis opgeslagen en opgenomen in gegevenssets van Platforms voor gebruik door [!DNL Data Science Workspace], [!DNL Query Service]en andere toepassingen voor gegevensdetectie.

Zie Overzicht [van](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html) verwerkingsregels voor meer informatie over verwerkingsregels.

## Experience Data Model (XDM)

XDM is een openbaar gedocumenteerde specificatie die gemeenschappelijke structuren en definities voor een toepassing verstrekt om met de diensten op te communiceren [!DNL Experience Platform].

Door te voldoen aan XDM-standaarden kunnen gegevens op uniforme wijze worden opgenomen, waardoor het eenvoudiger wordt om gegevens te leveren en informatie te verzamelen.

Zie het [XDM-systeemoverzicht](../../../xdm/home.md)voor meer informatie over XDM.

## Hoe worden velden toegewezen van Adobe Analytics aan XDM?

Wanneer een bronverbinding tot stand wordt gebracht voor het brengen van [!DNL Analytics] gegevens in [!DNL Experience Platform] gebruikend het [!DNL Platform] gebruikersinterface, worden de gegevensgebieden automatisch in kaart gebracht en in [!DNL Real-time Customer Profile] notulen opgenomen. Voor instructies bij het creëren van een bronverbinding met [!DNL Analytics] het gebruiken van [!DNL Platform] UI, zie het de schakelaarleerprogramma [van de Gegevens van de](../../tutorials/ui/create/adobe-applications/analytics.md)Analyse.

Voor meer informatie over de veldtoewijzing tussen [!DNL Analytics] en [!DNL Experience Platform], raadpleegt u de [Adobe Analytics-handleiding voor veldtoewijzing](./mapping/analytics.md) .

## Wat is de verwachte latentie voor de Gegevens van Analytics over Platform?

| Analysegegevens | Verwachte vertraging |
| -------------- | ---------------- |
| Nieuwe gegevens aan [!DNL Real-time Customer Profile] (A4T **niet** ingeschakeld) | &lt; 2 minuten |
| Nieuwe gegevens aan [!DNL Real-time Customer Profile] (A4T **is** ingeschakeld) | &lt; 15 minuten |
| Nieuwe gegevens voor Data Lake | &lt; 45 minuten |
| Backfill-gegevens (13 maanden of 10 miljard gebeurtenissen, afhankelijk van welke waarde lager is) | &lt; 4 weken |

>[!NOTE] De latentie zal afhankelijk van klantenconfiguratie, gegevensvolumes, en de toepassingen van de consument variëren. Bijvoorbeeld, als de implementatie van Analytics met `A4T` de latentie aan Pijpleiding wordt gevormd zal tot 5-10 minuten stijgen.

## Primaire id-id&#39;s in analysegegevens

Elke hit van de gegevensconnector Analytics bevat een primaire id die afhankelijk is van het feit of een ECID of een AID bestaat. Als er een ECID is, wordt de ECID aangewezen als primaire identificator. Als er sprake is van steun, wordt de steun als primaire steun aangemerkt.