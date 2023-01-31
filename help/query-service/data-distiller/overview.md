---
title: Distiller-overzicht van gegevens
description: Een overzicht van de Distiller-gebruikslimieten voor gegevens van Query Service met betrekking tot uw licentierechten.
source-git-commit: b3003cc62e8d3555b887a23f0614020bd2c5e81e
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Overzicht van Data Distiller

Data Distiller is een pakket dat een subset van de functies van Adobe Experience Platform bevat. Met Data Distiller kunt u gegevensvoorbereiding na inname (zoals reinigen, vormen en manipulatie) uitvoeren voor realtime klantprofiel of analytische gebruiksgevallen door batchquery&#39;s uit te voeren in Query Service. Uw gebruik van Data Distiller is afhankelijk van uw machtiging voor toepassingen op basis van Platforms.

## Licentiegebruik {#license-usage}

De  [Distiller-gebruiksdashboard voor gegevens](./license-usage.md) is beschikbaar zodra u Data Distiller-computeruren hebt aangeschaft. Met het gebruiksdashboard voor licenties kunt u het gebruik van de juiste computeruren controleren. Zie de [Distiller-gebruiksdocument voor gegevens](./license-usage.md) om belangrijke informatie over het de vergunningsgebruik van de Dienst van de Vraag van uw organisatie te bekijken.

## Parameters voor segmentering {#scoping-parameters}

Scoping-parameters zijn gebruikslimieten die betrekking hebben op het bereik van de vereiste instelling en die worden gedefinieerd door de capaciteit van uw licentie. Zonder add-ons zijn de bereikparameters voor gegevens-Distiller als volgt:

* **Rekenuren**: U kunt PSQL of de API van de Dienst van de Vraag gebruiken om partijvragen in om het even welke (geplande of anders) uitgevoerde zandbak in werking te stellen om gegevens af te tasten en te schrijven. Hierbij worden de toegewezen rekenuren per jaar gebruikt, zoals bepaald in het bereikproces van uw licentieovereenkomst. Het totaal aantal rekenuren wordt geaccumuleerd over alle Sandboxen.
* **Gegevens gebruikt**: Voor de gegevens die in Adobe Experience Platform worden ingevoerd en die via Data Distiller kunnen worden aangevraagd, gelden de beperkingen die worden beschreven in uw huidige licentie voor Adobe Real-time Customer Data Platform, Customer Journey Analytics en/of Adobe Journey Optimizer.
* **Opslag gegevensmeer**: De opslag van gegevens in het meer die in uw toenmalige vergunning aan Adobe Real-time Customer Data Platform, Customer Journey Analytics, en/of Adobe Journey Optimizer wordt verstrekt kan ook met de Distiller van Gegevens worden gebruikt. Data Lake Storage is een gedeelde functie.
* **Query Service-gebruikers**: Het aantal gebruikers van de Dienst van de Vraag die in uw toen huidige vergunning aan Adobe Real-time Customer Data Platform, Customer Journey Analytics, en/of Adobe Journey Optimizer worden gedetailleerd kan ook met Gegevens Distiller worden gebruikt. Gebruikers van de Query-service zijn een gedeelde functie.

## Guardrails

Zie de [Query Service-handleidingen](../guardrails.md) document met betrekking tot standaardgebruikslimieten voor Query Service-gegevens met betrekking tot uw licentierechten.

## Statische grenswaarden

Een statische limiet is de gebruikslimiet die betrekking heeft op de functionele grenzen van Adobe Experience Platform Activation. [Meer informatie over Adobe Experience Platform-activering](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) vindt u in de Help-documenten voor Adobe. Hieronder vindt u een overzicht van de statische limieten van Data Distiller. Raadpleeg het handboek Query Service voor meer informatie.

* **Batchquery&#39;s**: De geplande tijd van partijvragen uit na 24 uren.
* **Query-service**: U kunt de Dienst van de Vraag voor de volgende doeleinden gebruiken:
   * SQL-query&#39;s uitvoeren voor gegevensanalyse en gegevensvoorbereiding na inname (opschonen, vormgeven en manipuleren).
   * Om SQL vragen in werking te stellen om roll-up metriek aan oppervlakte direct in een hulpmiddel van BI tot stand te brengen.
   * Gegevens snel inspecteren in Adobe Experience Platform.
   * Om betekenisvolle inzichten van uw gegevens te produceren.
* **API-aanroep melden**: Om ervoor te zorgen dat query&#39;s die worden uitgevoerd op geaggregeerde gegevens met behulp van de API voor rapportage over voldoende bronnen beschikken om efficiënt te kunnen worden uitgevoerd. Dit omvat vragen die bestaande gegevensmodellen zoals die door Real-time Customer Data Platform worden verstrekt verbeteren. De rapporterende API volgt middelgebruik door gelijktijdig muntgroeven aan elke vraag toe te wijzen. Er zijn maximaal vier API-aanroepen voor rapportage tegelijk beschikbaar. Als u toegang hebt tot de API voor rapportage via een BI-programma en meer sleuven voor gelijktijdige uitvoering nodig hebt, is een BI-server vereist.


