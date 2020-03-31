---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: 66fef5b98d2c21d1ac8b272e2c8557d26daa3364

---


# Overzicht van de Privacyservice van Adobe Experience Platform

Om betere klantenervaringen te leveren, moet u persoonlijke gegevens van uw klanten verzamelen en opslaan. Wanneer u deze gegevens gebruikt, is het belangrijk dat u de privacy van uw klanten begrijpt en respecteert. De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek.

Adobe Experience Platform Privacy Service biedt een RESTful API en een gebruikersinterface waarmee u deze gegevensaanvragen van uw klanten kunt beheren. Met de Privacy Service kunt u verzoeken om toegang tot persoonlijke of persoonlijke klantgegevens van Adobe Experience Cloud-toepassingen en deze verwijderen. Zo kunt u de automatische naleving van wettelijke en organisatorische privacyregels vereenvoudigen.

## Waarom privacyservice?

De privacydienst is ontwikkeld als reactie op een fundamentele verschuiving in de manier waarop bedrijven de persoonsgegevens van hun klanten moeten beheren. Het centrale doel van de Dienst van de Privacy is naleving van de regels van de gegevensprivacy te automatiseren die, wanneer geschonden, in grote boetes kunnen resulteren en gegevensverrichtingen voor uw zaken kunnen verstoren.

### Privacy Service en GDPR

De [algemene gegevensbeschermingsverordening](https://eugdpr.org/) (GDPR) introduceerde verschillende nieuwe rechten inzake gegevensbescherming voor leden van de Europese Unie, waaronder het **recht op toegang** en het **recht om te worden vergeten**. Dit betekent dat iedere EU-burger wiens persoonlijke gegevens door uw bedrijf zijn verzameld, op elk moment toegang kan vragen tot of kan verzoeken tot zijn gegevens. Als u niet binnen 30 dagen aan deze verzoeken voldoet, kan dit leiden tot boetes van miljoenen dollar voor uw organisatie.

De privacydienst ondersteunt toegang tot en schrapping van aanvragen voor GDPR en volgt deze los van verzoeken uit hoofde van de CCPA-verordening. Raadpleeg de veelgestelde vragen [over de](gdpr/faq.md) GDPR en de [terminologiedocumenten](gdpr/terminology.md) voor meer informatie.

### Privacy Service en CCPA

De [California Consumer Privacy Act](https://www.caprivacy.org/about) (CCPA) verbetert de privacyrechten en consumentenbescherming voor inwoners van Californië in de Verenigde Staten. De CCPA biedt de inwoners van Californië nieuwe privacyrechten op het gebied van gegevens, waaronder het recht op toegang tot en verwijdering van hun persoonsgegevens, om te weten of hun persoonsgegevens worden verkocht of openbaar gemaakt (en aan wie), en het recht om te weigeren hun gegevens aan derden te laten verkopen.

De Dienst van de privacy steunt toegang en schrapt verzoeken om de verordening CCPA, en volgt hen gescheiden van verzoeken van GDPR. De Privacy Service steunt ook het verzenden van opt-out-of-verkoop verzoeken voor de toepassingen van de ErvingsCloud die hen steunen. Zie de Veelgestelde vragen [](ccpa/faq.md) CCPA voor meer informatie.

## Hoe gebruik ik de privacyservice voor het beheer van aanvragen voor privacytaken

De Dienst van de privacy verstrekt RESTful API en een gebruikersinterface die u toestaan om de verzoeken van uw klanten tot toegang te hebben/te schrappen van hun privé gegevens of het opting uit verkoop (ook genoemd geworden **privacybanen**) te leiden. De service biedt ook een centraal audit- en logboekmechanisme waarmee u de status en de resultaten van privacytaken met Experience Cloud-toepassingen kunt bekijken.

>[!NOTE] Afmeldingsverzoeken worden momenteel alleen ondersteund door de API voor de privacyservice.

### De API gebruiken

Met de API [voor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) privacyservice kunt u met RESTful API-aanroepen privacytaken maken en beheren, zodat u programmatisch kunt voldoen aan de privacyregels voor uw Experience Cloud-toepassingen. Zie de handleiding voor ontwikkelaars van de [](api/getting-started.md)Privacy Service API voor meer informatie over het gebruik van de API.

### De gebruikersinterface gebruiken

Met de interface van de privacyservice kunt u privacytaken maken en controleren met een grafische interface. UI omvat een widget van het Rapport **van de** Status die een visuele vertegenwoordiging van de status van alle actieve verzoeken verstrekt, en staat u toe om nieuwe verzoeken tot stand te brengen door de ingebouwde **Bouwer** van het Verzoek te gebruiken of door JSON- dossiers te uploaden. Voor meer informatie bij het gebruiken van UI, zie de de gebruikersgids [van de Dienst van de](ui/overview.md)Privacy.