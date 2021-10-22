---
keywords: Experience Platform;home;populaire onderwerpen;ECID;ecid
solution: Experience Platform
title: Identiteitsgegevens voor privacyverzoeken
topic-legacy: overview
description: Dit document biedt algemene richtlijnen voor het configureren van gegevensbewerkingen en het benutten van Adobe-technologieën om de juiste identiteitsgegevens voor privacyverzoeken van klanten op te halen.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Identiteitsgegevens voor privacyverzoeken

In opdracht van Adobe Experience Platform [!DNL Privacy Service] om klantenverzoeken voor hun privé gegevens (met inbegrip van toegang, schrapping, of opt-out-of-verkoop verzoeken) te verwerken, moet het van unieke herkenningstekens worden voorzien die een specifieke klant aan hun opgeslagen privé gegevens in uw Adobe Experience Cloud toegelaten toepassingen verbinden. [!DNL Privacy Service] gebruikt vervolgens deze id&#39;s om alle gegevens te verzamelen die onder de identiteit van de klant binnen zijn opgeslagen [!DNL Experience Cloud]en verwerkt deze op verzoek van de klant.

Dit document biedt algemene richtlijnen voor het configureren van gegevensbewerkingen en het benutten van Adobe-technologieën om de juiste identiteitsgegevens voor privacyverzoeken van klanten op te halen.

## Identiteiten en naamruimten

Wanneer een klant met uw merk door verscheidene verschillende kanalen kan in wisselwerking staan, kan het lastig zijn om de ongelijke herkenningstekens te verzoenen die van die vele interactie worden geregistreerd. Dit kan het op zijn beurt moeilijk maken te bepalen welke gegevens bij een bepaalde persoon in uw [!DNL Experience Cloud] toepassingen.

Bijvoorbeeld bij het verwerken van verzoeken om klantgegevens in [!DNL Privacy Service], kan een identiteit een koekjeswaarde vertegenwoordigen die onder een Adobe-gecontroleerd domein, een koekjeswaarde onder een derdedomein wordt geplaatst en met Adobe wordt gedeeld, of een douaneherkenningsteken die u uitdrukkelijk binnen uw IMS Organisatie bepaalt.

Daarom moet elke identiteit die aan [!DNL Privacy Service] gaat vergezeld van een naamruimte die context biedt door de identiteitswaarde te koppelen aan het systeem van oorsprong. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;e-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

Adobe Experience Platform Identity Service bewaart een opslag van wereldwijd gedefinieerde en door de gebruiker gedefinieerde naamruimten. Voor meer gedetailleerde informatie over naamruimten raadpleegt u de [Overzicht van naamruimte in identiteit](../identity-service/namespaces.md). Voor een lijst met standaardnaamruimten en naamruimtetekens die veel worden gebruikt in [!DNL Privacy Service], zie de [aanhangsel](api/appendix.md) in de API-handleiding.

## ECID en Opt-in Service

Adobe Experience Cloud [!DNL Identity Service] dient als gemeenschappelijk identificatiekader voor [!DNL Experience Cloud]en wijst een unieke, permanente id toe aan elke sitebezoeker. De [!DNL Experience Cloud] ID (ECID) houdt de activiteit van een klant door het gebruik van een eerderangs koekje bij, kan een apparaat in veelvoudige toepassingen uniek identificeren, en staat u toe om de zelfde plaatsbezoeker en hun gegevens in verschillende toepassingen te identificeren [!DNL Experience Cloud] toepassingen. Zie de [Overzicht van Experience Cloud-identiteitsservice](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) voor meer informatie .

Opt-in Dienst, een uitbreiding van [!DNL Experience Cloud Identity Service]kunt u protocollen voor uw toepassing instellen, zodat bezoekers kunnen bepalen of u een cookie kunt instellen op het apparaat of de browser van de bezoeker. Voor meer gedetailleerde informatie over de OptIn-service, waaronder het instellen van de service voor uw toepassing, raadpleegt u [Opt-in de documentatie van de Dienst](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html).

Nadat aan uw sitebezoekers ECID&#39;s zijn toegewezen, kunt u de Adobe gebruiken [!DNL Privacy JavaScript Library] om die id&#39;s op te halen voor gebruik in privacyverzoeken, zoals beschreven in de volgende sectie.

## [!DNL Privacy JS Library]

De [!DNL Adobe Privacy JavaScript Library] biedt verschillende functies waarmee u de identiteit van klanten die in de browser zijn opgeslagen, kunt ophalen en verwijderen. De bibliotheek kan worden gevormd om identiteitsinformatie van verscheidene toepassingen van Adobe, met inbegrip van ECID terug te winnen. Door het gebruik van callbacks of beloften, kunt u met succes teruggewonnen IDs behandelen en hen verzenden naar [!DNL Privacy Service] API.

Meer informatie over [!DNL Privacy JS Library], met inbegrip van codevoorbeelden voor verscheidene gemeenschappelijke gebruiksgevallen, gelieve te verwijzen naar [Overzicht van Privacy JS Library](js-library.md).

## Volgende stappen

Dit document gaf een kort overzicht van de centrale concepten betrokken bij het terugwinnen van de gegevens van de klantenidentiteit voor gebruik in privacyverzoeken. U wordt aangeraden de documentatiekoppelingen in elke sectie te controleren voor meer informatie over deze concepten en services. Voor stappen voor het verzenden van opgehaalde id&#39;s naar [!DNL Privacy Service] voor het creëren van toegang, schrapping, of opt-out van verkoop verzoeken, zie [Handleiding Privacy Service-API](api/overview.md).
