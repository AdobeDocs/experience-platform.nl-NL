---
keywords: Experience Platform;home;populaire onderwerpen;ECID;ecid
solution: Experience Platform
title: Identiteitsgegevens voor privacyverzoeken
description: Dit document biedt algemene richtlijnen voor het configureren van uw gegevensbewerkingen en het benutten van Adobe-technologieën om de juiste identiteitsgegevens op te halen voor privacyverzoeken van klanten.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Identiteitsgegevens voor privacyverzoeken

Adobe Experience Platform [!DNL Privacy Service] kan alleen aanvragen van klanten voor hun persoonlijke gegevens verwerken (zoals aanvragen voor toegang, verwijderen of het niet-verkopen) als deze zijn voorzien van unieke id&#39;s die een specifieke klant koppelen aan de opgeslagen privégegevens in uw Adobe Experience Cloud-toepassingen. [!DNL Privacy Service] gebruikt deze id&#39;s vervolgens om alle gegevens te verzamelen die onder de identiteit van de klant binnen [!DNL Experience Cloud] zijn opgeslagen, en deze te verwerken volgens de aanvraag van de klant.

Dit document biedt algemene richtlijnen voor het configureren van uw gegevensbewerkingen en het benutten van Adobe-technologieën om de juiste identiteitsgegevens op te halen voor privacyverzoeken van klanten.

## Identiteiten en naamruimten

Wanneer een klant met uw merk door verscheidene verschillende kanalen kan in wisselwerking staan, kan het lastig zijn om de ongelijke herkenningstekens te verzoenen die van die vele interactie worden geregistreerd. Hierdoor kan het moeilijk worden om te bepalen welke gegevens bij een bepaalde persoon in uw [!DNL Experience Cloud] -toepassingen horen.

Wanneer u bijvoorbeeld verzoeken om klantgegevens in [!DNL Privacy Service] afhandelt, kan een identiteit een cookiewaarde vertegenwoordigen die is ingesteld onder een domein dat door de Adobe wordt gecontroleerd, een cookie-waarde onder een domein van een andere fabrikant en die wordt gedeeld met Adobe, of een aangepaste id die u expliciet definieert binnen uw organisatie.

Daarom moet elke identiteit die naar [!DNL Privacy Service] wordt verzonden, vergezeld gaan van een naamruimte die context biedt door de identiteitswaarde te koppelen aan het systeem van oorsprong. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;e-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

Adobe Experience Platform Identity Service bewaart een opslag van wereldwijd gedefinieerde en door de gebruiker gedefinieerde naamruimten. Voor meer gedetailleerde informatie over namespaces, zie het [ overzicht van identiteitskaart namespace ](../identity-service/features/namespaces.md). Voor een lijst van standaard namespaces en namespace bepalende eigenschappen die algemeen in [!DNL Privacy Service] worden gebruikt, zie de [ appendix sectie ](api/appendix.md) in de API gids.

## ECID en Opt-in Service

Adobe Experience Cloud [!DNL Identity Service] fungeert als een gemeenschappelijk identificatiekader voor [!DNL Experience Cloud] en wijst een unieke, permanente id toe aan elke sitebezoeker. Met de [!DNL Experience Cloud] ID (ECID) wordt de activiteit van een klant bijgehouden via het gebruik van een cookie van de eerste partij, kunt u een apparaat in meerdere toepassingen op unieke wijze identificeren en kunt u dezelfde sitebezoeker en de gegevens ervan identificeren in verschillende [!DNL Experience Cloud] -toepassingen. Zie het [ overzicht van de Dienst van de Identiteit van het Experience Cloud ](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) voor meer informatie.

De open Dienst, een uitbreiding van [!DNL Experience Cloud Identity Service], staat u opstellingsprotocollen op uw toepassing toe om bezoekers te laten bepalen of u een koekje op het apparaat of browser van de bezoeker kunt plaatsen. Voor meer gedetailleerde informatie over de Opt-in Dienst, met inbegrip van hoe te opstelling de dienst voor uw toepassing, gelieve te verwijzen [ Opt-binnen de documentatie van de Dienst ](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html).

Nadat aan uw sitebezoekers ECID&#39;s zijn toegewezen, kunt u de Adobe [!DNL Privacy JavaScript Library] gebruiken om deze id&#39;s op te halen voor gebruik in privacyverzoeken, zoals beschreven in de volgende sectie.

## [!DNL Privacy JS Library]

[!DNL Adobe Privacy JavaScript Library] biedt verschillende functies waarmee u de identiteit van klanten die in de browser zijn opgeslagen, kunt ophalen en verwijderen. De bibliotheek kan worden gevormd om identiteitsinformatie van verscheidene toepassingen van de Adobe, met inbegrip van ECID terug te winnen. Door callbacks of beloftes te gebruiken, kunt u met succes opgehaalde IDs programmatically behandelen en hen verzenden naar [!DNL Privacy Service] API.

Voor meer informatie over [!DNL Privacy JS Library], met inbegrip van codesteekproeven voor verscheidene gemeenschappelijke gebruiksgevallen, gelieve te verwijzen naar het [ overzicht van de Bibliotheek JS van de Privacy JS ](js-library.md).

## Volgende stappen

Dit document gaf een kort overzicht van de centrale concepten betrokken bij het terugwinnen van de gegevens van de klantenidentiteit voor gebruik in privacyverzoeken. U wordt aangeraden de documentatiekoppelingen in elke sectie te controleren voor meer informatie over deze concepten en services. Voor stappen op hoe te om opgehaalde IDs naar [!DNL Privacy Service] te verzenden voor het creëren van toegang, schrapping, of uit-van-verkoop verzoeken, zie de [ Privacy Service API gids ](api/overview.md).
