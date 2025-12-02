---
title: Een aangepaste Web SDK-build maken met behulp van het NPM-pakket
description: Maak een aangepaste SDK-build voor het web die alleen de modules bevat die u nodig hebt.
exl-id: 0ba5ae55-9ec0-41b6-9675-e76ade8ca4cd
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 3%

---

# Een aangepaste Web SDK-build maken

De Experience Platform Web SDK-bibliotheek bevat meerdere modules voor verschillende functies, zoals personalisatie, identiteit, het bijhouden van koppelingen en nog veel meer. Afhankelijk van uw gebruiksgevallen hebt u wellicht alleen specifieke functies nodig in plaats van de volledige bibliotheek. Door een aangepaste Web SDK-build te maken, kunt u alleen de modules selecteren die u nodig hebt, de bibliotheekgrootte reduceren en de prestaties verbeteren.

## Gebruiksscenario’s {#use-case}

Het maken van een aangepaste Web SDK-build helpt de bibliotheekgrootte te verkleinen en de prestaties te verbeteren. Hier volgen enkele voorbeelden:

### Media Analytics verwijderen {#media-analytics-removal}

Als uw website geen media-inhoud heeft, kunt u de modules [!DNL Media Analytics] en [!DNL Streaming Media] uitsluiten van de build. Hierdoor kan de SDK-build voor het web met maximaal 50% worden verkleind en de laadsnelheid worden verbeterd.

### Personalization-verwijdering {#personalization}

Als u alleen meetgegevens voor gebruikers wilt verzamelen en Adobe Target of Journey Optimizer niet wilt gebruiken voor personalisatie, kunt u de module [!DNL Personalization] uitsluiten. Hierdoor wordt de bibliotheekgrootte kleiner, maar kunt u toch de benodigde gegevens verzamelen.

## Vereisten {#prerequisites}

Als u een aangepaste Web SDK-build wilt maken, hebt u het Web SDK NPM-pakket nodig. Zorg ervoor u [&#x200B; Node.js &#x200B;](https://nodejs.org/en/download/package-manager/all) geïnstalleerd op uw machine hebt. Zie de documentatie op hoe te [&#x200B; SDK van het Web installeren gebruikend het pakket NPM &#x200B;](npm.md) voor meer details.

## Componenten en afhankelijkheden {#components-dependencies}

Voordat u een aangepaste SDK-build voor het web maakt, definieert u de SDK-componenten en -opdrachten die u wilt gebruiken. Sommige bevelen hangen van specifieke modules af die in de bouwstijl worden omvat.

De lijst toont hieronder het verband tussen de modules van SDK van het Web en de bevelen zij omvatten:

| Moduleafhankelijkheid | Configuratieparameters | Opdrachten | Grootteklasse |
|---------|----------|---------|---------|
| Activiteitenkorps | [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) | N.v.t. | Medium |
| Doelgroepen | N.v.t. | N.v.t. | Klein |
| Context | [`context`](../commands/configure/context.md) | N.v.t. | Klein |
| Regelengine | `personalizationStorageEnabled` | <ul><li>`evaluateRulesets`</li><li>[`subscribeRulesetItems`](../commands/subscriberulesetitems.md)</li></ul> | Medium |
| Gebeurtenissamenvoeging | N.v.t. | `createEventMergeId` | Klein |
| Media Analytics Bridge | N.v.t. | [`getMediaAnalyticsTracker`](../commands/getmediaanalyticstracker.md) | Groot |
| Personalisatie | <ul><li>[`prehidingStyle`](../commands/configure/prehidingstyle.md)</li><li>[`targetMigrationEnabled`](../commands/configure/targetmigrationenabled.md)</li><li>[`autoCollectPropositionInteractions`](../commands/configure/autocollectpropositioninteractions.md)</li></ul> | N.v.t. | Groot |
| Toestemming | [`defaultConsent`](../commands/configure/defaultconsent.md) | [`setConsent`](../commands/setconsent.md) | Klein |
| Streaming media | [`streamingMedia`](../commands/configure/streamingmedia.md) | <ul><li>[`createMediaSession`](../commands/createmediasession.md)</li><li>[`sendMediaEvent`](../commands/sendmediaevent.md)</li></ul> | Groot |

## Een aangepaste Web SDK-build maken met behulp van het NPM-pakket {#create-custom-build}

1. Open de terminal en voer `npx @adobe/alloy` uit. U wordt gevraagd om de componenten van SDK van het Web te selecteren die u uw douane bouwt om wilt omvatten.

   ![&#x200B; Beeld van een terminal die de douane toont bouwt moduleselectie.](../assets/custom-build/npx.png)

   Gebruik de pijltoetsen om omhoog en omlaag te gaan in de lijst met modules.

   * Pers **Ruimte** om de geselecteerde module toe te laten of onbruikbaar te maken.
   * Druk op `A` om alle modules in of uit te schakelen.
   * Druk op `I` om de selectie om te keren.
   * Druk op `Enter` om uw selectie te bevestigen en ga naar de volgende stap.

1. Nadat u de modules hebt geselecteerd om in uw douane te omvatten bouwt, kunt u tussen het bewaren van een geminificeerde of ongeminificeerde versie van uw de bibliotheekbouwstijl van de SDK van het douaneWeb kiezen. Selecteer de gewenste optie en druk op `Enter` .

   ![&#x200B; Beeld van een terminal die de douane toont verklein selectie.](../assets/custom-build/minify.png)

1. Vervolgens wordt u gevraagd waar u de build op uw lokale computer wilt opslaan. Druk op `Enter` om de vooraf geselecteerde locatie te bevestigen of een nieuwe locatie in te voeren.

   ![&#x200B; Beeld van een terminal die de douane toont bouwt sparen optie.](../assets/custom-build/save.png)

1. Nadat u de locatie hebt bevestigd, wordt uw aangepaste build gegenereerd en opgeslagen.

   ![&#x200B; Beeld van een terminal die de douane toont bouwt bewaarde plaats.](../assets/custom-build/saved.png)
