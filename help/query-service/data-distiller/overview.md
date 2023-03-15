---
title: Distiller-overzicht van gegevens
description: Een overzicht van de Distiller-gebruikslimieten voor gegevens van Query Service met betrekking tot uw licentierechten.
source-git-commit: ae4ecd43071a198592193a1a598a064cdc6be2f6
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# Overzicht van Data Distiller

Data Distiller is een pakket dat een subset van de functies van Adobe Experience Platform bevat. Met Data Distiller kunt u gegevensvoorbereiding na inname (zoals reinigen, vormen en manipulatie) uitvoeren voor realtime klantprofiel of analytische gebruiksgevallen door batchquery&#39;s uit te voeren in Query Service. Uw gebruik van Data Distiller is afhankelijk van uw machtiging voor toepassingen op basis van Platforms.

## Licentiegebruik {#license-usage}

De  [Distiller-gebruiksdashboard voor gegevens](./license-usage.md) is beschikbaar zodra u Data Distiller-computeruren hebt aangeschaft. Met het gebruiksdashboard voor licenties kunt u het gebruik van de juiste computeruren controleren. Zie de [Distiller-gebruiksdocument voor gegevens](./license-usage.md) om belangrijke informatie over het de vergunningsgebruik van de Dienst van de Vraag van uw organisatie te bekijken.

<!-- Update these descriptions post 23.3 release
## Scoping parameters {#scoping-parameters}

Scoping parameters are usage limits that relate to the scoping of your required set up, and are defined by your license capacity. Without add-ons, Data Distiller's scoping parameters are as follows: 

* **Compute Hours**: You can use PSQL or the Query Service API to run batch queries executed in any sandbox (scheduled or otherwise) to scan and write data. This uses your allotted Compute Hours per year as determined in the scoping process of your license agreement. Total Compute Hours is accumulated across all Sandboxes.
* **Data Ingested**: The data ingested into Adobe Experience Platform which can be queried using Data Distiller is subject to the limitations described in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer.
* **Data Lake Storage**: The data lake storage provided in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer may also be used with Data Distiller. Data Lake Storage is a shared feature.
* **Query Service Users**: The number of Query Service users detailed in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer may also be used with Data Distiller. Query Service Users is a shared feature. 
-->

## Guardrails

Zie de [Query Service-handleidingen](../guardrails.md) document met betrekking tot standaardgebruikslimieten voor Query Service-gegevens met betrekking tot uw licentierechten.

<!-- Update these descriptions post 23.3 release
## Static limits

A static limit is the usage limit that relates to the functional boundaries of Adobe Experience Platform Activation. [More information on Adobe Experience Platform Activation](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) can be found in the Adobe help documents. A summary of Data Distiller static limits are listed below, for more complete information please refer to the Query Service guardrail document.  

* **Batch Queries**: Scheduled batch queries time out after 24 hours.
* **Query Service**: You can use Query Service for the following purposes: 
    * To run SQL queries for data analysis and post ingestion data preparation (cleaning, shaping, and manipulation).
    * To run SQL queries to create roll-up metrics to surface directly into a BI tool.
    * To quickly inspect data within Adobe Experience Platform.
    * To generate meaningful insights from your data.
* **Reporting API Call**: To ensure queries run on aggregated data using the reporting API have enough resources to execute efficiently. This includes queries that enhance existing data models such as those provided by Real-Time Customer Data Platform. The reporting API tracks resource utilization by assigning concurrency slots to each query. A maximum of four reporting API calls are available concurrently. If you access the reporting API through a BI tool and require more concurrency slots, a BI server is required.
-->

