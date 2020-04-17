---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Identiteitsgegevens voor privacyverzoeken
topic: overview
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# Identiteitsgegevens voor privacyverzoeken

Adobe Experience Platform Privacy Service kan alleen aanvragen van klanten voor hun persoonlijke gegevens verwerken (zoals aanvragen voor toegang, verwijderen of het niet-verkopen) als deze zijn voorzien van unieke id&#39;s die een koppeling vormen tussen een specifieke klant en de opgeslagen privégegevens in toepassingen die geschikt zijn voor Adobe Experience Cloud. De Dienst van de privacy gebruikt dan deze herkenningstekens om alle gegevens te verzamelen die onder de identiteit van de klant binnen de Cloud van de Ervaring worden opgeslagen, en het te verwerken volgens het verzoek van de klant.

Dit document biedt algemene richtlijnen voor het configureren van gegevensbewerkingen en het benutten van Adobe-technologieën om de juiste identiteitsgegevens op te halen voor privacyverzoeken van klanten.

## Identiteiten en naamruimten

Wanneer een klant met uw merk door verscheidene verschillende kanalen kan in wisselwerking staan, kan het lastig zijn om de ongelijke herkenningstekens te verzoenen die van die vele interactie worden geregistreerd. Hierdoor kan het moeilijk worden om te bepalen welke gegevens bij een bepaalde persoon in uw Experience Cloud-toepassingen horen.

Wanneer u bijvoorbeeld een verzoek om klantgegevens in de privacyservice afhandelt, kan een identiteit een cookiewaarde zijn die is ingesteld onder een door Adobe beheerd domein, een cookiewaarde onder een domein van een andere fabrikant en wordt gedeeld met Adobe, of een aangepaste id die u expliciet definieert binnen uw IMS-organisatie.

Daarom moet elke identiteit die naar de privacydienst wordt verzonden, vergezeld gaan van een **naamruimte** die context biedt door de identiteitswaarde te koppelen aan het systeem van oorsprong. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;E-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

De identiteitsservice van Adobe Experience Platform bewaart een archief met wereldwijd gedefinieerde en door de gebruiker gedefinieerde naamruimten. Zie het overzicht [](../identity-service/namespaces.md)van naamruimten voor meer informatie over naamruimten. Voor een lijst van standaardnamespaces en namespace kwalificfiers die algemeen in de Dienst van de Privacy worden gebruikt, zie de [bijlage sectie](api/appendix.md) in de ontwikkelaarsgids.

## ECID en Opt-in Service

De Adobe Experience Cloud Identity Service fungeert als een algemeen identificatiekader voor Experience Cloud en wijst een unieke, permanente id toe aan elke bezoeker van de site. Met de Experience Cloud ID (ECID) wordt de activiteit van een klant bijgehouden door het gebruik van een cookie van de eerste partij, kunt u een apparaat op unieke wijze identificeren in meerdere toepassingen en kunt u dezelfde sitebezoeker en hun gegevens identificeren in verschillende Experience Cloud-toepassingen. Zie het overzicht [van de](https://docs.adobe.com/content/help/en/id-service/using/intro/overview.html) Experience Cloud Identity Service voor meer informatie.

De open-binnen Dienst, een uitbreiding van de Dienst van de Identiteit van de Ervaring Cloud, staat u opstellingsprotocollen op uw toepassing toe om bezoekers te laten bepalen of u een koekje op het apparaat of browser van de bezoeker kunt plaatsen. Raadpleeg de [documentatie](https://docs.adobe.com/content/help/en/id-service/using/implementation/opt-in-service/optin-overview.html)van de Opt-in-service voor meer informatie over de Opt-in-service, inclusief hoe u de service voor uw toepassing kunt instellen.

Nadat aan uw sitebezoekers ECID&#39;s zijn toegewezen, kunt u de Adobe Privacy JavaScript-bibliotheek gebruiken om deze id&#39;s op te halen voor gebruik in privacyverzoeken, zoals beschreven in de volgende sectie.

## Privacy JS Library

De Adobe Privacy JavaScript-bibliotheek bevat verschillende functies waarmee u de identiteit van klanten die in de browser zijn opgeslagen, kunt ophalen en verwijderen. De bibliotheek kan worden geconfigureerd om identiteitsgegevens op te halen uit verschillende Adobe-toepassingen, waaronder ECID. Door het gebruik van callbacks of beloften, kunt u met succes teruggewonnen IDs behandelen en hen verzenden naar de Dienst API van de Privacy.

Voor meer informatie over de bibliotheek van Privacy JS, met inbegrip van codesteekproeven voor verscheidene gemeenschappelijke gebruiksgevallen, gelieve te verwijzen naar het overzicht [van de Bibliotheek van](js-library.md)Privacy JS.

## Volgende stappen

Dit document gaf een kort overzicht van de centrale concepten betrokken bij het terugwinnen van de gegevens van de klantenidentiteit voor gebruik in privacyverzoeken. U wordt aangeraden de documentatiekoppelingen in elke sectie te controleren voor meer informatie over deze concepten en services. Voor stappen op hoe te om opgehaalde IDs naar de Dienst van de Privacy te verzenden voor het creëren van toegang, schrapping, of uit-van-verkoop verzoeken, zie de de ontwikkelaarsgids [van de Dienst van de](api/getting-started.md)Privacy.