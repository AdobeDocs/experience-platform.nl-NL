---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 10%

---


# Overzicht van Adobe Experience Platform Privacy Service

Om betere klantenervaringen te leveren, moet u persoonlijke gegevens van uw klanten verzamelen en opslaan. Wanneer u deze gegevens gebruikt, is het belangrijk dat u de privacy van uw klanten begrijpt en respecteert. De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek.

Adobe Experience Platform Privacy Service verstrekt RESTful API en gebruikersinterface om u te helpen deze gegevensverzoeken van uw klanten beheren. Met Privacy Service kunt u verzoeken indienen om toegang te krijgen tot persoonlijke of persoonlijke klantgegevens uit Adobe Experience Cloud-toepassingen en deze te verwijderen. Zo kunt u de automatische naleving van wettelijke en organisatorische privacyregels vereenvoudigen.

## Waarom Privacy Service?

Privacy Service is ontwikkeld als reactie op een fundamentele verschuiving in de manier waarop bedrijven de persoonsgegevens van hun klanten moeten beheren. Het centrale doel van Privacy Service is het automatiseren van naleving van de regels van de gegevensprivacy die, wanneer geschonden, in grote boetes kunnen resulteren en gegevensverrichtingen voor uw zaken kunnen verstoren.

### Privacy Service en GDPR

De [](https://eugdpr.org/)General Data Protection Regulation (GDPR, ofwel Algemene verordening gegevensbescherming (AVG)) heeft diverse nieuwe dataprivacyrechten geïntroduceerd voor leden van de Europese Unie, waaronder het **recht op toegang** en het **recht om vergeten te worden**. Dit betekent dat iedere EU-burger wiens persoonlijke data door uw bedrijf zijn verzameld, op elk moment kan vragen om toegang tot of verwijdering van zijn of haar data. Als u niet binnen 30 dagen aan deze verzoeken voldoet, kan dit leiden tot boetes van miljoenen dollar voor uw organisatie.

Privacy Service ondersteunt toegang tot en schrapping van aanvragen voor GDPR en volgt deze los van verzoeken uit hoofde van de CCPA-verordening. Raadpleeg de veelgestelde vragen [over de](gdpr/faq.md) GDPR en de [terminologiedocumenten](gdpr/terminology.md) voor meer informatie.

### Privacy Service en CCPA

De [California Consumer Privacy Act](https://www.caprivacy.org/about) (CCPA) verbetert de privacyrechten en consumentenbescherming voor inwoners van Californië in de Verenigde Staten. De CCPA biedt de inwoners van Californië nieuwe privacyrechten op het gebied van gegevens, waaronder het recht op toegang tot en verwijdering van hun persoonsgegevens, om te weten of hun persoonsgegevens worden verkocht of openbaar gemaakt (en aan wie), en het recht om te weigeren hun gegevens aan derden te laten verkopen.

De Privacy Service steunt toegang en schrapt verzoeken om de verordening CCPA, en volgt hen los van verzoeken van GDPR. Privacy Service ondersteunt ook het verzenden van &quot;opt-out&quot;-aanvragen voor Experience Cloud-toepassingen die deze toepassingen ondersteunen. Zie de Veelgestelde vragen [](ccpa/faq.md) CCPA voor meer informatie.

## Privacy Service gebruiken om privacytaakaanvragen te beheren

Privacy Service biedt een RESTful-API en -gebruikersinterface waarmee u de verzoeken van uw klanten om toegang te krijgen tot of gegevens uit het privébestand te verwijderen of om uit de verkoop te kiezen (ook wel **privacytaken** genoemd). De service biedt ook een centraal audit- en logboekmechanisme waarmee u de status en resultaten van privacytaken met Experience Cloud-toepassingen kunt bekijken.

>[!NOTE]
>
>Uitschakelen-aanvragen worden momenteel alleen ondersteund door de Privacy Service-API.

### De API gebruiken

Met de [Privacy Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) kunt u met RESTful API-aanroepen privacytaken maken en beheren, zodat u programmatisch kunt voldoen aan de privacyregels voor uw Experience Cloud-toepassingen. Zie de handleiding voor ontwikkelaars van de [Privacy Service-API voor meer informatie over het gebruik van de API](api/getting-started.md).

### De gebruikersinterface gebruiken

Met de interface van de Privacy Service kunt u met een grafische interface privacytaken maken en controleren. UI omvat een widget van het Rapport **van de** Status die een visuele vertegenwoordiging van de status van alle actieve verzoeken verstrekt, en staat u toe om nieuwe verzoeken tot stand te brengen door de ingebouwde **Bouwer** van het Verzoek te gebruiken of door JSON- dossiers te uploaden. Raadpleeg de gebruikershandleiding bij de [Privacy Service voor meer informatie over het gebruik van de gebruikersinterface](ui/overview.md).