---
keywords: Experience Platform;home;populaire onderwerpen;ECID;ecid
solution: Experience Platform
title: Identiteitsgegevens voor privacyverzoeken
topic-legacy: overview
description: Dit document biedt algemene richtlijnen voor het configureren van gegevensbewerkingen en het benutten van Adobe-technologieën om de juiste identiteitsgegevens voor privacyverzoeken van klanten op te halen.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 1%

---

# Identiteitsgegevens voor privacyverzoeken

Adobe Experience Platform [!DNL Privacy Service] kan alleen aanvragen van klanten voor hun persoonlijke gegevens verwerken (inclusief verzoeken om toegang, verwijdering of het niet-verkopen) als deze zijn voorzien van unieke id&#39;s die een specifieke klant koppelen aan de opgeslagen privégegevens in uw Adobe Experience Cloud-toepassingen. [!DNL Privacy Service] gebruikt deze id&#39;s vervolgens om alle gegevens te verzamelen die onder de identiteit van de klant binnen zijn opgeslagen  [!DNL Experience Cloud], en deze te verwerken volgens het verzoek van de klant.

Dit document biedt algemene richtlijnen voor het configureren van gegevensbewerkingen en het benutten van Adobe-technologieën om de juiste identiteitsgegevens voor privacyverzoeken van klanten op te halen.

## Identiteiten en naamruimten

Wanneer een klant met uw merk door verscheidene verschillende kanalen kan in wisselwerking staan, kan het lastig zijn om de ongelijke herkenningstekens te verzoenen die van die vele interactie worden geregistreerd. Dit kan het op zijn beurt moeilijk maken om te bepalen welke gegevens tot een bepaalde persoon in uw [!DNL Experience Cloud] toepassingen behoren.

Wanneer bijvoorbeeld gegevensverzoeken van klanten worden afgehandeld in [!DNL Privacy Service], kan een identiteit een cookie-waarde vertegenwoordigen die is ingesteld onder een domein met Adobe-controle, een cookie-waarde onder een domein van derden en die wordt gedeeld met Adobe, of een aangepaste id die u expliciet definieert binnen uw IMS-organisatie.

Daarom is het vereist dat elke identiteit die naar [!DNL Privacy Service] wordt verzonden vergezeld gaat van een naamruimte die context door de identiteitswaarde te koppelen aan zijn systeem van oorsprong verstrekt. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;e-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

Adobe Experience Platform Identity Service bewaart een opslag van wereldwijd gedefinieerde en door de gebruiker gedefinieerde naamruimten. Zie [Naamruimte overzicht](../identity-service/namespaces.md) voor gedetailleerde informatie over naamruimten. Voor een lijst van standaardnamespaces en namespace kwalificfiers die algemeen in [!DNL Privacy Service] worden gebruikt, zie [appendix sectie](api/appendix.md) in de ontwikkelaarsgids.

## ECID en Opt-in Service

Adobe Experience Cloud [!DNL Identity Service] fungeert als een gemeenschappelijk identificatiekader voor [!DNL Experience Cloud] en wijst een unieke, permanente id toe aan elke sitebezoeker. Met de [!DNL Experience Cloud]-id (ECID) wordt de activiteit van een klant bijgehouden via het gebruik van een cookie van de eerste partij, kan een apparaat in meerdere toepassingen op unieke wijze worden geïdentificeerd en kunt u dezelfde sitebezoeker en de gegevens ervan identificeren in verschillende [!DNL Experience Cloud]-toepassingen. Zie [Experience Cloud Identity Service overview](https://docs.adobe.com/content/help/en/id-service/using/intro/overview.html) voor meer informatie.

De open-binnen Dienst, een uitbreiding van [!DNL Experience Cloud Identity Service], staat u opstellingsprotocollen op uw toepassing toe om bezoekers te laten bepalen of u een koekje op het apparaat of browser van de bezoeker kunt plaatsen. Raadpleeg de [Opt-in-servicedocumentatie](https://docs.adobe.com/content/help/nl-NL/id-service/using/implementation/opt-in-service/optin-overview.html) voor gedetailleerde informatie over de aanmeldingsservice, inclusief hoe u de service voor uw toepassing kunt instellen.

Nadat aan uw sitebezoekers ECID&#39;s zijn toegewezen, kunt u de Adobe gebruiken om die id&#39;s op te halen voor gebruik in privacyverzoeken, zoals beschreven in de volgende sectie.[!DNL Privacy JavaScript Library]

## [!DNL Privacy JS Library]

De [!DNL Adobe Privacy JavaScript Library] biedt verschillende functies waarmee u de identiteit van klanten die in de browser zijn opgeslagen, kunt ophalen en verwijderen. De bibliotheek kan worden gevormd om identiteitsinformatie van verscheidene toepassingen van Adobe, met inbegrip van ECID terug te winnen. Door het gebruik van callbacks of beloften, kunt u met succes teruggewonnen IDs behandelen en hen verzenden naar [!DNL Privacy Service] API.

Voor meer informatie over [!DNL Privacy JS Library], met inbegrip van codesteekproeven voor verscheidene gemeenschappelijke gebruiksgevallen, gelieve te verwijzen naar [Overzicht van de Bibliotheek van JS van de Privacy](js-library.md).

## Volgende stappen

Dit document gaf een kort overzicht van de centrale concepten betrokken bij het terugwinnen van de gegevens van de klantenidentiteit voor gebruik in privacyverzoeken. U wordt aangeraden de documentatiekoppelingen in elke sectie te controleren voor meer informatie over deze concepten en services. Voor stappen op hoe te om teruggewonnen IDs naar [!DNL Privacy Service] voor het creëren van toegang te verzenden, schrapt, of uit-van-verkoop verzoeken, zie [de gids van de ontwikkelaar van de Privacy Service](api/getting-started.md).
