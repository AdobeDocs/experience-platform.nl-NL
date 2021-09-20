---
title: Marketo Engage-bestemming
description: Marketo Engage is de enige CXM-oplossing (end-to-end Customer Experience Management) voor marketing, reclame, analyse en handel. Hiermee kunt u activiteiten automatiseren en beheren van CRM-beheer en de betrokkenheid van klanten tot marketing en inkomstentoewijzing op basis van account.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 1f18e07af7ef0d90f882fa668c5659330bce5960
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# (bèta) Marketo Engage-bestemming {#beta-marketo-engage-destination}

>[!IMPORTANT]
>
>De bestemming van de Marketo Engage in Adobe Experience Platform is momenteel in Bèta. De documentatie en functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

Marketo Engage is de enige CXM-oplossing (end-to-end Customer Experience Management) voor marketing, reclame, analyse en handel. Hiermee kunt u activiteiten automatiseren en beheren van CRM-beheer en de betrokkenheid van klanten tot marketing en inkomstentoewijzing op basis van account.

De segmentschakelaar laat marketers toe om segmenten die in Adobe Experience Platform aan Marketo worden gecreeerd te duwen waar zij als statische lijsten zullen verschijnen.

## Ondersteunde identiteiten {#supported-identities}

| Doelidentiteit | Beschrijving |
|---|---|
| ECID | Een naamruimte die ECID vertegenwoordigt. Naar deze naamruimte kan ook worden verwezen door de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [ECID](/help/identity-service/ecid.md) voor meer informatie. |
| Email | Een naamruimte die een e-mailadres vertegenwoordigt. Dit type naamruimte is vaak gekoppeld aan één persoon en kan daarom worden gebruikt om die persoon op verschillende kanalen te identificeren. |

## Exporttype {#export-type}

De Uitvoer van het segment - u exporteert alle leden van een segment (publiek) met de herkenningstekens (naam, telefoonaantal, of anderen) die in de bestemming van de Marketo Engage worden gebruikt.

## Doel instellen en segmenten activeren {#set-up}

Lees [Push an Adobe Experience Platform Segment to a Marketo Static List](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) in de documentatie van Marketo voor gedetailleerde instructies voor het instellen van de bestemming en het activeren van segmenten.

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie [gegeven governance overzicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->