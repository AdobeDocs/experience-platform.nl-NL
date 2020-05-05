---
title: 'Adobe Target en de Adobe Experience Platform Web SDK. '
seo-title: Adobe Experience Platform Web SDK en Adobe Target gebruiken
description: Leer hoe u persoonlijke inhoud kunt renderen met Experience Platform Web SDK met Adobe Target
seo-description: Leer hoe u persoonlijke inhoud kunt renderen met Experience Platform Web SDK met Adobe Target
translation-type: tm+mt
source-git-commit: db4bfec04a1116ce2b6a0be7ca0e8cb2f9639ad6

---


# Doeloverzicht

De Adobe Experience Platform Web SDK is geïntegreerd met Adobe Target via die [personalisatiefunctie](../../fundamentals/rendering-personalization-content.md) en stelt u in staat om persoonlijke inhoud en beslissingen eenvoudig te bedienen.

## Adobe-doel inschakelen

Als u Doel wilt inschakelen, moet u het volgende doen:

- Laat doel in uw [randconfiguratie](../../fundamentals/edge-configuration.md) met de aangewezen cliëntcode toe.
- Voeg de `renderDecisions` optie toe aan uw gebeurtenissen.

Vervolgens kunt u desgewenst ook:

- Voeg toe `scopes` aan uw gebeurtenissen om specifieke activiteiten op te halen (nuttig voor activiteiten die met de op formulier gebaseerde composer zijn gemaakt).
- Voeg het [voorverborgen fragment](../../fundamentals/managing-flicker.md) toe om alleen bepaalde delen van de pagina te verbergen.

## VEC gebruiken

Met SDK kunt u VEC normaal met één uitzondering gebruiken u de geïnstalleerde en actieve [doelVEC helperuitbreiding](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) nodig hebt.

## De op formulieren gebaseerde composer gebruiken

De op formulieren gebaseerde composer kan ook worden gebruikt om inhoud te retourneren. Het bereik wordt als locatie (mBox) weergegeven in de doelinterface. Ook zult u willen ervoor zorgen dat uw ontwikkelaar naar de reacties zoekt als besluit om werkingsgebied te gebruiken.

## Soorten publiek in XDM

Binnen Doel XDM zullen de gegevens in de Bouwer van de Publiek als douaneparameter verschijnen. De XDM wordt geserialiseerd met behulp van puntnotatie (bijvoorbeeld `web.webPageDetails.name`)

## Terminologie

__Beslissingen__ - In Doel houden deze verband met de ervaring die uit een Activiteit wordt geselecteerd.

__Toepassingsgebied__ - Het toepassingsgebied van de beschikking. In Doel is dit de mBox. Het algemene mBox is het `__view__` bereik.

__Schema__ - Het schema van een besluit is het type aanbod in Target.

__XDM__ - XDM wordt geserialiseerd in puntnotatie en dan gezet in Doel als mBox parameters.