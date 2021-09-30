---
keywords: doelpersonalisatie; bestemming; doelbestemming ervaringsplatform;doelbestemming adobe;
title: Adobe Target-verbinding
description: Adobe Target is een toepassing die realtime, 1:1 en door AI aangedreven personalisatie en experimenten biedt voor alle inkomende klantinteracties voor websites, mobiele apps en nog veel meer.
source-git-commit: caccd096c9165139d9b966bbfcb311456276192a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---


# Adobe Target-verbinding (bèta) {#adobe-target-connection}

## Overzicht {#overview}

>[!IMPORTANT]
>
>De Adobe Target-verbinding in Adobe Experience Platform bevindt zich momenteel in bèta. De documentatie en functionaliteit kunnen worden gewijzigd.

Adobe Target is een toepassing die realtime, 1:1, door AI aangedreven personalisatie en experimenteren biedt in alle inkomende klantinteracties voor websites, mobiele apps en nog veel meer.

Adobe Target is een personalisatieverbinding in Adobe Experience Platform.

## Vereisten {#prerequisites}

Deze integratie wordt aangedreven door [Adobe Experience Platform Web SDK](../../../edge/home.md). U moet deze SDK gebruiken om deze bestemming te gebruiken.

## Exporttype {#export-type}

**Profielverzoek**  - u vraagt om alle segmenten die in de Adobe Target-bestemming zijn toegewezen voor één profiel.

## Gebruiksscenario’s {#use-cases}

**Banner homepage aanpassen**

Een huisverhuurbedrijf en verkoopbedrijf willen hun homepage met een banner personaliseren, die op de kwalificaties van het klantensegment in Adobe Experience Platform wordt gebaseerd. Het bedrijf kan selecteren welk publiek een persoonlijke ervaring zou moeten krijgen en hen naar Adobe Target sturen als doelcriterium voor hun Target-aanbieding.

## Verbinden met de bestemming {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../../ui/connect-destination.md) worden beschreven.

Adobe Experience Platform maakt automatisch verbinding met het Adobe Target-exemplaar van uw bedrijf. Er is geen verificatie vereist.

### Verbindingsparameters {#parameters}

Terwijl [vestiging](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **Naam**: Vul de voorkeursnaam voor dit doel in.
* **Omschrijving**: Voer een beschrijving in voor uw bestemming. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken. Dit veld is optioneel.
* **DataStream-id**: Dit bepaalt in welke gegevensstroom van de Inzameling van Gegevens de segmenten in de reactie op de pagina zullen worden omvat. In het vervolgkeuzemenu worden alleen gegevensstromen weergegeven waarvoor de doelconfiguratie is ingeschakeld. Zie [Een gegevensstroom configureren](../../../edge/fundamentals/datastreams.md) voor meer informatie.

## Segmenten naar dit doel activeren {#activate}

Lees [Activate profielen en segmenten aan profiel verzoekbestemmingen](../../ui/activate-profile-request-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Geëxporteerde gegevens {#exported-data}

Adobe Target leest profielgegevens van het Adobe Experience Platform Edge Network, zodat er geen gegevens worden geëxporteerd.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Lees voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt het [Overzicht gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
