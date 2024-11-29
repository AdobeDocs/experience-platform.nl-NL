---
title: Bijlage voor sandbox Tooling API-handleiding
description: Dit document bevat aanvullende informatie over het werken met de API voor sandboxgereedschappen.
exl-id: fdfa019d-ce0e-456b-b591-7d96d1115e02
source-git-commit: 955c6946786e9425bdb99d623595420a6d13747e
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Handboek sandbox-API

Dit document bevat aanvullende informatie over het werken met de [!DNL Sandbox] API.

## Query-parameters gebruiken {#query}

De sandbox Tooling-API ondersteunt het gebruik van queryparameters voor het pagineren en filteren van resultaten bij het weergeven van pakketten.

>[!NOTE]
>
>`limit` kan afzonderlijk worden doorgegeven en gestart.

| Parameter | Beschrijving |
| --- | --- |
| `limit` | Het maximumaantal records dat in de reactie moet worden geretourneerd. De standaardlimiet is 20. |
| `start` | Het begin van de plaats waar een subsetlijst met items moet beginnen. |
| `targetSandbox` | Vertegenwoordigt de naam van de zandbak waar u uw artefacten wilt invoeren. |
| `jobType` | Het type taak. Deze waarde kan `NEW`, `RESUME` of `ROLLBACK` zijn. |
| `jobStatus` | De status van de taak. Deze waarde kan `PENDING`, `IN_PROGRESS`, `SUCCESS`, `FAILED` of `CANCELLED` zijn. |
| `requestType` | Het type verzoek. Deze waarde kan `EXPORT`, `IMPORT` of `COPY` zijn. |
| `expiryPeriod` | Deze door de gebruiker opgegeven tijdsperiode definieert de vervaldatum van het pakket (in dagen) vanaf het moment dat het pakket werd gepubliceerd. Deze waarde mag niet negatief zijn. De standaardwaarde is 90 dagen vanaf het moment dat de update- of publicatie-API wordt aangeroepen. |
| `packageType` | Het type pakket. Deze waarde kan `PARTIAL` of `FULL` zijn. |
| `status` | De status van het pakket. Deze waarde kan `DRAFT`, `PUBLISHED`, `PUBLISH_IN_PROGRESS` of `PUBLISH_FAILED` zijn. |
