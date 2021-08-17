---
title: Marketo Engage-bestemming
description: Marketo Engage is de enige CXM-oplossing (end-to-end Customer Experience Management) voor marketing, reclame, analyse en handel. Hiermee kunt u activiteiten automatiseren en beheren van CRM-beheer en de betrokkenheid van klanten tot marketing en inkomstentoewijzing op basis van account.
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '325'
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

## Instellen {#set-up}

Hier vindt u instructies over het instellen van de bestemming [a1/>.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en)

## Verbinden met de bestemming {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../../ui/connect-destination.md) worden beschreven.

## Gebruik en beheer van gegevens {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Zie [Overzicht gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html) voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt.

## Segmenten naar dit doel activeren {#activate}

Zie [Profielen en segmenten activeren aan een doel](../../ui/activate-destinations.md) voor instructies bij het activeren van publiekssegmenten aan bestemmingen.
