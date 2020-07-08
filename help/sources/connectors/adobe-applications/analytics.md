---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Analytics-gegevensconnector
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 2%

---


# Analytics Data Connector

Met Adobe Experience Platform kunt u Adobe Analytics-gegevens invoeren via de Analytics Data Connector (ADC). ADC streamt gegevens die door Adobe Analytics zijn verzameld naar Platform in real-time, waarbij Analytics-gegevens met SCDS-indeling worden omgezet in XDM-velden (Experience Data Model) voor gebruik door Platform.

Dit document biedt een overzicht van Adobe Analytics en beschrijft de gebruiksscenario&#39;s voor Analytics-gegevens.

## Adobe Analytics- en Analytics-gegevens

Adobe Analytics is een krachtige engine waarmee u meer kunt leren over uw klanten, hoe ze communiceren met uw wegeigenschappen, kunt zien waar uw uitgaven voor digitale marketing effectief zijn en verbeteringsgebieden kunt identificeren. Adobe Analytics verwerkt biljoenen webtransacties per jaar en ADC stelt u in staat om eenvoudig gebruik te maken van deze rijke gedragsgegevens en het Real-time klantprofiel in een paar minuten te verrijken.

![](./images/analytics-data-experience-platform.png)

Op hoog niveau verzamelt Adobe Analytics gegevens via verschillende digitale kanalen en meerdere datacenters over de hele wereld. Zodra de gegevens zijn verzameld, worden de regels van Visitor Identification, Segmentation and Transformation Architecture (VISTA) en de verwerkingsregels toegepast om de inkomende gegevens vorm te geven. Nadat de ruwe gegevens door deze lichte verwerking zijn gegaan, wordt het dan beschouwd klaar voor consumptie door het Profiel van de Klant in real time. In een proces parallel aan het bovengenoemde, worden de zelfde verwerkte gegevens microbatched en ingebed in Platform datasets voor gebruik door de Werkruimte van de Wetenschap van Gegevens, de Dienst van de Vraag, en andere gegevens-ontdekkingstoepassingen.

Zie Overzicht [van](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules.html) verwerkingsregels voor meer informatie over verwerkingsregels.

## Experience Data Model (XDM)

XDM is een openbaar gedocumenteerde specificatie die gemeenschappelijke structuren en definities voor een toepassing verstrekt om met de diensten op Adobe Experience Platform te communiceren te gebruiken.

Door te voldoen aan XDM-standaarden kunnen gegevens op uniforme wijze worden opgenomen, waardoor het eenvoudiger wordt om gegevens te leveren en informatie te verzamelen.

Zie het [XDM-systeemoverzicht](../../../xdm/home.md)voor meer informatie over XDM.

## Hoe worden velden toegewezen van Adobe Analytics aan XDM?

Wanneer een bronverbinding tot stand is gebracht voor het in Experience Platform brengen van Analytics-gegevens via de gebruikersinterface van het Platform, worden gegevensvelden automatisch toegewezen aan en opgenomen in het Real-time Klantprofiel binnen enkele minuten. Zie de zelfstudie over de [Analytics-gegevensaansluiting voor instructies over het maken van een bronverbinding met Adobe Analytics via de interface van het Platform](../../tutorials/ui/create/adobe-applications/analytics.md).

Voor meer informatie over de veldtoewijzing tussen Analytics en Experience Platform gaat u naar de handleiding voor [Adobe Analytics-toewijzing](./mapping/analytics.md) .

## Wat is de verwachte vertraging voor Analytics Data on Platform?

| Analytics-gegevens | Verwachte vertraging |
| -------------- | ---------------- |
| Nieuwe gegevens naar Real-time klantprofiel (A4T **niet** ingeschakeld) | &lt; 2 minuten |
| Nieuwe gegevens naar Real-time klantprofiel (A4T **is** ingeschakeld) | &lt; 15 minuten |
| Nieuwe gegevens voor Data Lake | &lt; 45 minuten |
| Backfill-gegevens (13 maanden of 10 miljard gebeurtenissen, afhankelijk van welke waarde lager is) | &lt; 4 weken |

>[!NOTE]
>
>De latentie zal afhankelijk van klantenconfiguratie, gegevensvolumes, en de toepassingen van de consument variëren. Bijvoorbeeld, als de implementatie van Analytics met `A4T` de latentie aan Pijpleiding wordt gevormd zal tot 5-10 minuten stijgen.