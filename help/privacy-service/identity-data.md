---
keywords: Experience Platform;home;popular topics;ECID;ecid
solution: Experience Platform
title: Identiteitsgegevens voor privacyverzoeken
topic: overview
description: Dit document biedt algemene richtlijnen voor het configureren van gegevensbewerkingen en het benutten van Adobe-technologieën om de juiste identiteitsgegevens voor privacyverzoeken van klanten op te halen.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---


# Identiteitsgegevens voor privacyverzoeken

Adobe Experience Platform kan alleen aanvragen van klanten voor hun persoonlijke gegevens verwerken (zoals aanvragen voor toegang, verwijderen of het niet-verkopen van gegevens) als het beschikt over unieke id&#39;s die een specifieke klant koppelen aan de opgeslagen privégegevens in uw Adobe Experience Cloud-toepassingen. [!DNL Privacy Service] [!DNL Privacy Service] gebruikt deze id&#39;s vervolgens om alle gegevens te verzamelen die onder de identiteit van de klant binnen zijn opgeslagen [!DNL Experience Cloud], en deze te verwerken volgens het verzoek van de klant.

Dit document biedt algemene richtlijnen voor het configureren van gegevensbewerkingen en het benutten van Adobe-technologieën om de juiste identiteitsgegevens voor privacyverzoeken van klanten op te halen.

## Identiteiten en naamruimten

Wanneer een klant met uw merk door verscheidene verschillende kanalen kan in wisselwerking staan, kan het lastig zijn om de ongelijke herkenningstekens te verzoenen die van die vele interactie worden geregistreerd. Hierdoor kan het moeilijk worden om te bepalen welke gegevens bij een bepaalde persoon in uw [!DNL Experience Cloud] toepassingen horen.

Bijvoorbeeld, wanneer het behandelen van de verzoeken van klantengegevens binnen [!DNL Privacy Service], kan een identiteit een kokerwaarde vertegenwoordigen die onder een Adobe-gecontroleerd domein, een kokerwaarde onder een derdedomein wordt geplaatst en met Adobe wordt gedeeld, of een douaneherkenningsteken dat u uitdrukkelijk binnen uw IMS Organisatie bepaalt.

Daarom moet elke verzonden identiteit vergezeld gaan van een naamruimte die context biedt door de identiteitswaarde te koppelen aan het systeem van oorsprong. [!DNL Privacy Service] Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;e-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

Adobe Experience Platform Identity Service bewaart een opslag van wereldwijd gedefinieerde en door de gebruiker gedefinieerde naamruimten. Zie het overzicht [](../identity-service/namespaces.md)van naamruimten voor meer informatie over naamruimten. Voor een lijst van standaardnamespaces en namespace kwalificfiers die algemeen binnen worden gebruikt, zie de [!DNL Privacy Service]bijlage sectie [](api/appendix.md) in de ontwikkelaarsgids.

## ECID en Opt-in Service

Adobe Experience Cloud [!DNL Identity Service] fungeert als een gemeenschappelijk identificatiekader voor [!DNL Experience Cloud]en wijst een unieke, permanente id toe aan elke bezoeker van de site. Met de [!DNL Experience Cloud] id (ECID) wordt de activiteit van een klant bijgehouden via het gebruik van een cookie van de eerste partij, kan een apparaat in meerdere toepassingen op unieke wijze worden geïdentificeerd en kunt u dezelfde sitebezoeker en de gegevens ervan in verschillende [!DNL Experience Cloud] toepassingen identificeren. Raadpleeg het overzicht [van de](https://docs.adobe.com/content/help/en/id-service/using/intro/overview.html) Experience Cloud Identity Service voor meer informatie.

De open-binnen Dienst, een uitbreiding van [!DNL Experience Cloud Identity Service], staat u opstellings protocollen op uw toepassing toe om bezoekers te laten bepalen of u een koekje op het apparaat of browser van de bezoeker kunt plaatsen. Raadpleeg de [documentatie](https://docs.adobe.com/content/help/nl-NL/id-service/using/implementation/opt-in-service/optin-overview.html)van de Opt-in-service voor meer informatie over de Opt-in-service, inclusief hoe u de service voor uw toepassing kunt instellen.

Nadat aan uw sitebezoekers ECID&#39;s zijn toegewezen, kunt u de Adobe gebruiken [!DNL Privacy JavaScript Library] om deze id&#39;s op te halen voor gebruik in privacyverzoeken, zoals beschreven in de volgende sectie.

## [!DNL Privacy JS Library]

Het [!DNL Adobe Privacy JavaScript Library] biedt verschillende functies waarmee u de identiteit van klanten die in de browser zijn opgeslagen, kunt ophalen en verwijderen. De bibliotheek kan worden gevormd om identiteitsinformatie van verscheidene toepassingen van Adobe, met inbegrip van ECID terug te winnen. Door het gebruik van callbacks of beloften, kunt u met succes opgehaalde IDs behandelen en hen verzenden naar [!DNL Privacy Service] API.

Voor meer informatie over [!DNL Privacy JS Library], met inbegrip van codesteekproeven voor verscheidene gemeenschappelijke gebruiksgevallen, gelieve te verwijzen naar het overzicht [van de Bibliotheek van](js-library.md)Privacy JS.

## Volgende stappen

Dit document gaf een kort overzicht van de centrale concepten betrokken bij het terugwinnen van de gegevens van de klantenidentiteit voor gebruik in privacyverzoeken. U wordt aangeraden de documentatiekoppelingen in elke sectie te controleren voor meer informatie over deze concepten en services. Voor stappen op hoe te om teruggewonnen IDs naar [!DNL Privacy Service] voor het creëren van toegang, schrapping, of uit-van-verkoop verzoeken te verzenden, zie de de ontwikkelaarsgids [van de](api/getting-started.md)Privacy Service.