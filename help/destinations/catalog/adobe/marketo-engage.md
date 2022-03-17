---
title: Marketo Engage-bestemming
description: Marketo Engage is de enige CXM-oplossing (end-to-end Customer Experience Management) voor marketing, reclame, analyse en handel. Hiermee kunt u activiteiten automatiseren en beheren van CRM-beheer en de betrokkenheid van klanten tot marketing en inkomstentoewijzing op basis van account.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Marketo Engage-bestemming {#beta-marketo-engage-destination}

## Overzicht {#overview}

Marketo Engage is de enige CXM-oplossing (end-to-end Customer Experience Management) voor marketing, reclame, analyse en handel. Hiermee kunt u activiteiten automatiseren en beheren van CRM-beheer en de betrokkenheid van klanten tot marketing en inkomstentoewijzing op basis van account.

De bestemming laat marketers toe om segmenten te duwen die in Adobe Experience Platform aan Marketo worden gecreeerd waar zij als statische lijsten zullen verschijnen.

## Ondersteunde identiteiten {#supported-identities}

| Doelidentiteit | Beschrijving |
|---|---|
| ECID | Een naamruimte die ECID vertegenwoordigt. Naar deze naamruimte kan ook worden verwezen door de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [ECID](/help/identity-service/ecid.md) voor meer informatie . |
| Email | Een naamruimte die een e-mailadres vertegenwoordigt. Dit type naamruimte is vaak gekoppeld aan één persoon en kan daarom worden gebruikt om die persoon op verschillende kanalen te identificeren. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>In de [toewijzingsstap](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) van de doelworkflow activeren: *verplicht* om identiteiten toe te wijzen en *optioneel* om kenmerken toe te wijzen. Het toewijzen van e-mail- en/of ECID via het tabblad Identiteitsnaamruimte is het belangrijkste wat u moet doen om ervoor te zorgen dat de persoon gelijk is aan de persoon in Marketo. Toewijzing via e-mail zorgt voor de hoogste match-rate.

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (e-mail, ECID) die in de Marketo Engage-bestemming worden gebruikt. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Doel instellen en segmenten activeren {#set-up}

Voor gedetailleerde instructies over hoe te opstelling de bestemming en activeert segmenten, lees [Een Adobe Experience Platform-segment naar een statische Marketo-lijst verplaatsen](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) in de documentatie van Marketo.

In de onderstaande video ziet u ook de stappen voor het configureren van een Marketo-bestemming en het activeren van segmenten.

>[!NOTE]
>
>De gebruikersinterface van het Experience Platform wordt vaak bijgewerkt en kan sinds de opname van deze video zijn veranderd. Voor de meest actuele informatie raadpleegt u de bovenstaande handleiding.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [gegevensbeheer - overzicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
