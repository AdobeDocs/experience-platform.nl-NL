---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van beleidsregels voor gegevensgebruik
topic: policies
translation-type: tm+mt
source-git-commit: d08f06b3c2bdb21e0f4935bbcb6f163892ab9842

---


# Overzicht van beleidsregels voor gegevensgebruik

Om gegevensgebruikslabels effectief te steunen gegevensnaleving, moet het beleid van het gegevensgebruik worden uitgevoerd. Het beleid van het gebruik van gegevens is regels die de soorten marketing acties beschrijven die u aan, of beperkt van, op gegevens binnen het Platform van de Ervaring mag uitvoeren.

Een voorbeeld van een marketing actie zou de wens kunnen zijn om een dataset naar een derdedienst uit te voeren. Als er een beleid is dat zegt dat de specifieke types van gegevens, zoals Persoonlijk Identificeerbare Informatie (PII), niet kunnen worden uitgevoerd en een &quot;I&quot;etiket (de Gegevens van de Identiteit) is toegepast op de dataset, zult u een reactie van de Dienst van het Beleid ontvangen die u vertelt dat een beleid van het gegevensgebruik is geschonden.

## Beleid voor gegevensgebruik maken en gebruiken

Zodra de etiketten van het gegevensgebruik zijn toegepast, kan de gegevensstewards beleid tot stand brengen gebruikend de [DULE Dienst API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)van het Beleid.

Als gegevenssteward, kunt u de Dienst API van het Beleid gebruiken om beleid met betrekking tot marketing acties te beheren en te evalueren die op gegevens worden genomen die etiketten DULE bevatten. Met behulp van de API kunt u beleid maken en bijwerken, de status van een beleid bepalen en met marketingacties werken om te beoordelen of een specifieke actie een beleid voor gegevensgebruik schendt.

Binnen de API van de Dienst van het Beleid, worden alle beleid en marketing acties bedoeld als of `core` of `custom` middelen. `core` bronnen worden gedefinieerd en onderhouden door Adobe, terwijl `custom` bronnen worden gemaakt en onderhouden door individuele klanten. De `custom` middelen zijn dus uniek en zijn alleen zichtbaar voor de organisatie die ze heeft gemaakt.

Voor meer informatie bij het uitvoeren van de belangrijkste verrichtingen die door de DULE Dienst API van het Beleid worden verstrekt, zie de de ontwikkelaarsgids [van de Dienst van het](../api/getting-started.md)Beleid. Voor geleidelijke instructies bij het werken met DULE beleid, zie de zelfstudie over het [creëren van en het evalueren van DULE beleid](create.md).