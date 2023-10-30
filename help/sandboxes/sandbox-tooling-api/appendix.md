---
title: Bijlage voor sandbox Tooling API-handleiding
description: Dit document bevat aanvullende informatie over het werken met de API voor sandboxgereedschappen.
exl-id: fdfa019d-ce0e-456b-b591-7d96d1115e02
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Handboek sandbox-API

Dit document bevat aanvullende informatie over het werken met de [!DNL Sandbox] API.

## Query-parameters gebruiken {#query}

De sandbox Tooling-API ondersteunt het gebruik van queryparameters voor het pagineren en filteren van resultaten bij het weergeven van pakketten.

>[!NOTE]
>
>De `limit` kan afzonderlijk worden doorgegeven en gestart.

| Parameter | Beschrijving |
| --- | --- |
| `limit` | Het maximumaantal records dat in de reactie moet worden geretourneerd. De standaardlimiet is 20. |
| `start` | Het begin van de plaats waar een subsetlijst met items moet beginnen. |
| `targetSandbox` | Vertegenwoordigt de naam van de zandbak waar u uw artefacten wilt invoeren. |
| `jobType` | Het type taak. Deze waarde kan NEW, RESUME en ROLLBACK zijn. |
| `jobStatus` | De status van de taak. Deze waarde kan IN_PROGRESS, SUCCESS, MISLUKT, en GEANNULEERD zijn. |
| `requestType` | Het type verzoek. Deze waarde kan EXPORTEREN, IMPORTEREN en KOPIËREN. |
| `expiryPeriod ` | Deze door de gebruiker opgegeven tijdsperiode definieert de vervaldatum van het pakket (in dagen) vanaf het moment dat het pakket werd gepubliceerd. Deze waarde mag niet negatief zijn. De standaardwaarde is 90 dagen vanaf het moment dat de update- of publicatie-API wordt aangeroepen. |
