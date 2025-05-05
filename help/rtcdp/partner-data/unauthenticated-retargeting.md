---
title: Niet-geverifieerde herbestemming op de server
description: Leer hoe u niet-geverifieerde gebruikers opnieuw als doel instelt met behulp van ECID's
feature: Use Cases, Customer Acquisition
exl-id: 008f4534-29e7-49b9-b0be-9e0c3962ee21
source-git-commit: ba2154e84f24ddf4ec270121bdcbb6dd5d3dff42
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Niet-geverifieerde herbestemming op de server {#unauthenticated-retargeting}

Als cookies van derden hun effectiviteit verliezen, gaan bedrijven over naar oplossingen zonder cookies voor persoonlijke betrokkenheid en herbestemming. Offsite heroriënteren maakt het bedrijven mogelijk om gebruikers met hoge bedoelingen te bereiken op basis van hun vorige interacties, zonder dat ze op JavaScript aan de clientzijde hoeven te vertrouwen.

## Waarom overwegen niet-geregistreerde bezoekers opnieuw te richten {#why-use-case}

Door Adobe Experience Platform Web SDK en server-side gebeurtenis het door:sturen te integreren, kunt u gebeurtenis het stromen en gegevens het door:sturen stroomlijnen. Hierdoor kunnen niet-geverifieerde gebruikers die ECID&#39;s (Experience Cloud-id&#39;s) gebruiken, naadloos opnieuw worden aangewezen, waardoor consistente betrokkenheid op alle platforms wordt gegarandeerd. Met deze oplossing, kunt u omzettingskansen verhogen door unauthenticated gebruikers effectief opnieuw te richten die op hun vroegere interactie worden gebaseerd.

## Vereisten en planning {#prerequisites-and-planning}

Alvorens met de plaatsing van het Web SDK en de Gebeurtenis door:sturen configuratie te werk te gaan, zorg het volgende ervoor:

1. **Adobe met de opstelling van SDK van het Web**: De SDK van het Web van Adobe moet worden uitgevoerd om gebeurtenisinzameling en gegevens het door:sturen te vergemakkelijken.

2. **Adobe Experience Platform Edge Network configuratie**: Zorg Edge Network wordt gevormd om gebeurtenis te steunen in real time door:sturen voor offsite het opnieuw richten.

3. **ECID Synchronisatie**: Zorg ervoor ECIDs over platforms wordt gesynchroniseerd om naadloze publiek aanpassing toe te laten.

## Offsite heroriëntering bereiken {#achieve-offsite-retargeting}

1. **stelt SDK van het Web** op: Voer SDK van het Web van Adobe op uw website uit om gebeurtenisgegevens in real time, met inbegrip van gebruikersinteractie zoals paginameningen, klikken, en ander gedrag te vangen.

2. **laat Gebeurtenis door:sturen** toe: Vorm gebeurtenis door:sturen binnen Platform om verzamelde gebruikersgegevens te verzenden, die efficiënte gegevensoverdracht voor publieksactivering verzekeren.

3. **vorm server-Kant Activering**: De server-zijmogelijkheden van Adobe van het gebruik om het opnieuw richten publiek te activeren dat op ECIDs wordt gebaseerd, die nauwkeurige publiek verzekeren zich richt op over platforms.

4. **creeer Getrapte Soorten publiek**: Gebruik de hulpmiddelen van de publiekssegmentatie van het Platform om geconcentreerd publiek te bepalen dat op gebruikersgedrag, zoals meningen, interactie, of verlaten wortels wordt gebaseerd.

5. **activeer Soorten publiek**: Zodra uw opnieuw gerichte publiek wordt gecreeerd, activeer hen om gepersonaliseerde inhoud te leveren, ervoor zorgend de gebruikers op hun vroegere interactie met uw plaats opnieuw worden betrokken.

## Een publiek maken met het berekende kenmerk {#create-audience}

Als u doelgebruikers met een hoge intentie effectief wilt heroriënteren, maakt u een publiek op basis van hun eerdere interacties met uw website. Gebruik Platform om gebruikers te segmenteren met behulp van berekende kenmerken.

1. **identificeer zeer belangrijk gedrag**: Selecteer gebruikersacties om zoals paginameningen te volgen of te klikken.

2. **creeer publiek**: De hulpmiddelen van de publiekssegmentatie van het gebruik om gebruikers te groeperen die op gedrag worden gebaseerd.

3. **ECID van de Synchronisatie**: Zorg ervoor ECIDs over platforms voor nauwkeurige publiek aanpassing wordt gesynchroniseerd.

## Uw publiek activeren {#activate-audience}

Als u eenmaal een publiek hebt gemaakt, activeert u dit op verschillende platformen om gebruikers erbij te betrekken.

1. **publiek van het Overzicht**: Zorg de publiekssegmenten op het juiste gedrag wijzen.

2. **creeer activeringsregels**: Plaats voorwaarden voor wanneer en hoe de gebruikers gebaseerd op acties worden betrokken.

3. **duw aan Platform**: Activeer het publiek.

4. **prestaties van de Monitor**: De prestaties van het publiek van het spoor en passen zonodig aan.

## De extensie voor herbestemming van de site configureren {#configure-extension}

### De Web SDK implementeren

Zorg ervoor dat de Adobe Web SDK op de juiste wijze is geïntegreerd in uw website. Deze SDK maakt het mogelijk real-time gebeurtenisgegevens te verzamelen, wat cruciaal is voor een efficiënte heroriëntatie.

### Gebeurtenis doorsturen inschakelen

Opstelling een gebeurtenis door:sturen binnen Platform om verzamelde gegevens van het gebruikersgedrag naar het opnieuw richten van platforms te verzenden. Het door:sturen van gebeurtenissen zorgt ervoor dat de gegevens efficiënt worden overgebracht, toelatend ondernemingen om high-intent gebruikers te richten zonder zich op koekjes te verlaten.

### Koppelen aan regel voor opnieuw toewijzen

Zorg ervoor dat de extensie voor herbestemming buiten de site is gekoppeld aan een geldige gebeurtenisregel in de gegevensverzameling van Adobe Experience Platform. Doorgaans moet een algemene regel worden gemaakt die op toetshandelingen, zoals `page load` of specifieke gebruikersinteracties, wordt geactiveerd.

Meer leren over het vormen van de uitbreiding, lees de [ Gebeurtenis door:sturen ](https://experienceleague.adobe.com/nl/docs/experience-platform/tags/event-forwarding/getting-started) documentatie.

## Andere gebruiksgevallen {#other-use-cases}

Dit document biedt een overzicht van de belangrijkste gebruiksgevallen en technische overwegingen voor het succesvol ontwikkelen en gebruiken van de Web SDK en de Event Forwarding opstelling. Door de beschreven procedures te volgen en ervoor te zorgen dat aan de vereiste voorwaarden wordt voldaan, kunt u de mogelijkheden voor het bijhouden en analyseren van gegevens aanzienlijk verbeteren.

U kunt verdere gebruiksgevallen onderzoeken die door de steun van partnergegevens in Real-Time CDP worden toegelaten:

- [ verbind en verkrijg nieuwe klanten ](./prospecting.md) door partnergegevens te gebruiken.
- [ personaliseer onsite ervaringen ](./offsite-retargeting.md) met partner-gesteunde bezoekerserkenning.
- [ de profielen van de Supplement van de Eerste partij ](./supplement-first-party-profiles.md) met partner-Geleverde attributen.
