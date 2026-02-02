---
title: Salesforce Marketing Cloud (V2) Source - Overzicht
description: Leer hoe u Salesforce Marketing Cloud (V2) met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
last-substantial-update: 2025-02-02T00:00:00Z
source-git-commit: 4d47eae91711596677335b03568add9f6fbade74
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# Overzicht van de bron [!DNL Salesforce Marketing Cloud] (V2)

>[!IMPORTANT]
>
>De originele [[!DNL Salesforce Marketing Cloud]  (V1) &#x200B;](salesforce-marketing-cloud.md) bron is afgekeurd vanaf Januari 2026. Er zijn geen migraties beschikbaar voor deze vervangen bron en u moet uw gegevens opnieuw implementeren met de nieuwe bron [!DNL Salesforce Marketing Cloud] (V2).

De integratie tussen Adobe [&#x200B; Real-Time CDP &#x200B;](../../../rtcdp/overview.md) en [!DNL Salesforce Marketing Cloud] wordt ontworpen om de Uitbreidingen van Gegevens wegens de flexibiliteit en de controle te gebruiken zij verstrekken. In tegenstelling tot de StandaardLijsten van het Systeem (de Mening van Gegevens en de Ingebouwde Voorwerpen), die tot vooraf bepaalde gebieden beperkt zijn en hoofdzakelijk systeem-vlakke het volgen dienen, kunt u de Uitbreidingen van Gegevens gebruiken om douanevelden te bepalen, een grote verscheidenheid van zaken-specifieke gegevens te organiseren, en uw gegevensstructuren aan unieke vereisten aan te passen.

Vanwege deze mate van aanpassing en schaalbaarheid is de integratie tussen Real-Time CDP en [!DNL Salesforce Marketing Cloud] afhankelijk van gegevensuitbreidingen en niet van standaardsysteemtabellen. Deze benadering biedt een flexibelere, scalable, en geïntegreerde stichting voor het beheren van gegevens aan, die ervoor zorgen dat het zich op uw bedrijfsdoelstellingen richt

U kunt de [!DNL Salesforce Marketing Cloud] -bron gebruiken om uw [!DNL Salesforce Marketing Cloud] -account te verbinden met Real-Time CDP en Adobe Experience Platform. Lees de onderstaande documentatie voor meer informatie.

## Voorbeelden van hoofdletters gebruiken {#use-case-examples}

### E-mailcampagnes aanpassen met contactgegevens

Een handelsmerk wil e-mailcampagnes personaliseren die op de stadia van de klantenlevenscyclus worden gebaseerd (bijvoorbeeld, nieuwe klant, herhaalde koper, loyale klant). Hiertoe maken ze een Contactgegevens-extensie om belangrijke klantgegevens op te slaan, zoals naam, e-mail, levenscyclusfase en aankoopgedrag. Deze gegevens worden vervolgens in Experience Platform opgenomen voor een verdergaande segmentatie en doelgerichtheid.

Door de gegevens van de Contact Data Extension in Experience Platform in te voeren, kan het merk klanten segmenteren op basis van hun levenscyclusfase en aankoopgedrag. Ze kunnen bijvoorbeeld een welkomstaanbod sturen naar nieuwe klanten, een loyaliteitsbeloning voor herhaalde kopers of zelfs inactieve klanten opnieuw betrekken bij gerichte aanbiedingen. Deze benadering zorgt voor gepersonaliseerde communicatie en maakt een meer relevante en effectieve betrokkenheid van klanten mogelijk.

### Campagnegegevens voor gepersonaliseerde segmentering worden verzameld

Een marketingteam wil hun e-mailcampagnes optimaliseren door zich te richten op klanten op basis van hun betrokkenheid bij vorige campagnes. Hiertoe maken ze een extensie Campagne voor gegevens in [!DNL Salesforce Marketing Cloud] om gegevens over de betrokkenheid van klanten op te slaan, zoals het openen van e-mail, klikken en reacties op campagnes. Deze gegevens worden vervolgens in Experience Platform opgenomen voor verdere segmentatie en personalisatie.

Door deze gegevens van de Uitbreiding van de Gegevens van de Campagne in Experience Platform op te nemen, kan het marketing team klanten segmenteren die op vroegere overeenkomst worden gebaseerd, zoals zij die op productaanbiedingen klikte of positief antwoordde. Klanten die zich hebben aangemeld, kunnen gerichte aanbiedingen ontvangen in toekomstige e-mails, terwijl klanten die negatief hebben gereageerd vervolgacties van de klantenservice kunnen ontvangen. Deze integratie met Experience Platform zorgt ervoor dat het marketingteam meer persoonlijke en relevante inhoud kan leveren op basis van het gedrag van de klant.

### Klanten aanwijzen op basis van activiteitengegevens

Een marketingteam wil zich richten op klanten op basis van hun activiteiten, zoals websitebezoeken, het verzenden van formulieren of interactie met eerdere e-mailcampagnes. Om dit te bereiken, creëren zij een Uitbreiding van Gegevens van Activiteiten om informatie over de de dienstactiviteiten van elke klant op te slaan. Deze gegevens worden vervolgens in Experience Platform opgenomen voor verdere segmentatie en gepersonaliseerde campagne-gerichtheid.

Door de gegevens van de Uitbreiding van Gegevens van Activiteiten in Experience Platform op te nemen, kan het marketingteam klanten segmenteren op basis van hun betrokkenheidsgeschiedenis. Klanten die onlangs een bezoek hebben gebracht aan de website maar een aankoop niet hebben voltooid, kunnen bijvoorbeeld per e-mail een herinnering ontvangen met speciale aanbiedingen. Op dezelfde manier kunnen klanten die een formulier hebben ingevuld, gepersonaliseerde follow-upcommunicatie ontvangen. Deze benadering zorgt ervoor dat elke klant relevante inhoud ontvangt op basis van zijn meest recente activiteiten, waardoor de betrokkenheid en conversietarieven worden verbeterd.

## Vereisten {#prerequisites}

Lees de onderstaande secties voor de vereiste configuratie die u moet voltooien voordat u uw bron kunt verbinden met Experience Platform.

### Toepassing instellen voor verificatie {#set-up-application-for-authentication}

Wanneer het bouwen van een integratie met [!DNL Salesforce Marketing Cloud], één van de eerste stappen is een **Geïnstalleerd Pakket** binnen [!DNL Salesforce Marketing Cloud] tot stand te brengen. Het geïnstalleerde pakket genereert de clientgegevens die nodig zijn om API-aanroepen te verifiëren, definieert het integratietype en het bijbehorende machtigingsbereik. Bovendien, verstrekt het geïnstalleerde pakket de correcte API eindpunten voor uw huurder. Het dient ook als beheerde container voor het beheren van, het controleren van, en het intrekken van toegang, ervoor zorgend dat alle integraties veilig, controleerbaar, en gericht op Salesforce aanbevolen authentificatiemodel zijn.

Als u een geïnstalleerd pakket wilt maken, gebruikt u de gebruikersinterface van [!DNL Salesforce Marketing Cloud] en navigeert u naar **[!DNL Setup]** > **[!DNL Apps]** > **[!DNL Installed Packages]** en selecteert u **[!DNL New]** . Gebruik de interface [!DNL New Package Details] om een naam en informatie voor het pakket op te geven. Selecteer **[!DNL Save]** als u klaar bent.

![&#x200B; de nieuwe pakketinterface van Salesforce Marketing Cloud UI.](../../images/tutorials/create/sfmc/new-package.png)

Wanneer het nieuwe pakket is gemaakt, selecteert u **[!DNL Add Component]** .

![&#x200B; Add de interface van de Component van Salesforce Marketing Cloud UI.](../../images/tutorials/create/sfmc/add-component.png)

Selecteer **[!DNL API Integration]** als het componenttype.

![&#x200B; het venster van de componentenselectie met &quot;geselecteerde Integratie API.](../../images/tutorials/create/sfmc/api-integration.png)

Selecteer **[!DNL Server-to-Server]** als integratietype.

![&#x200B; het de selectievenster van het integratietype &#x200B;](../../images/tutorials/create/sfmc/server-to-server.png)

Navigeer ten slotte naar **[!DNL Scope]** > **[!DNL Data]** . Selecteer onder **[!DNL Data Extensions]** de optie **[!DNL Read]** .

![&#x200B; de sectie van gegevensuitbreidingen van Toepassingsgebied in Salesforce Marketing &#x200B;](../../images/tutorials/create/sfmc/data-extensions.png)

Selecteer **[!DNL Save]** en kopieer en bewaar dan uw **cliëntgeheim**. Selecteer **[!DNL Finish]** wanneer deze bewerking is voltooid.

![&#x200B; het venster van Salesforce Marketing Cloud voor het produceren van een cliëntgeheim.](../../images/tutorials/create/sfmc/generate-secret.png)

Alvorens [!DNL Salesforce Marketing Cloud] UI te verlaten, kopieer **cliëntidentiteitskaart** en **unieke prefix van basisURI** aangezien u beide waarden zult gebruiken om een verbinding aan Experience Platform tot stand te brengen. Voor de basis-URI voor verificatie moet u alles verwijderen na `.auth.marketingcloudapis.com/`

![&#x200B; de de componenteninterface van Salesforce Marketing Cloud waar de cliëntidentiteitskaart en unieke basis URI kunnen worden teruggewonnen.](../../images/tutorials/create/sfmc/client-id-and-uri.png)

Voor gedetailleerde stappen bij het creëren van een geïnstalleerd pakket, lees de [[!DNL Salesforce]  documentatie &#x200B;](https://trailhead.salesforce.com/content/learn/modules/marketing-cloud-developer-basics/set-up-your-developer-environment).

### Vereiste referenties verzamelen {#gather-required-credentials}

U moet waarden opgeven voor de volgende referenties om [!DNL Salesforce Marketing Cloud] te verbinden met Experience Platform.

| Credentials | Beschrijving |
| --- | --- |
| Client-id | De openbaar gemaakte id die door [!DNL Salesforce Marketing Cloud] wordt gebruikt om uw account te identificeren bij het autoriseren naar Experience Platform. De client-id kan worden opgehaald uit het deelvenster Componenten van de gebruikersinterface van [!DNL Salesforce Marketing Cloud] . |
| Clientgeheim | De vertrouwelijke sleutel die slechts aan de cliënttoepassing en vergunningsserver wordt bekend. U kunt uw cliëntgeheim produceren door de [&#x200B; hierboven geschetste stappen van de toepassingsopstelling te volgen &#x200B;](#set-up-application-for-authentication). |
| Basiseindpunt | Het voorvoegsel van de basis-URI voor verificatie voor [!DNL Salesforce Marketing Cloud] . |

{style="table-layout:auto"}

## Verbinden [!DNL Salesforce Marketing Cloud] met Experience Platform

Ga door om uw [!DNL Salesforce Marketing Cloud] bronverbinding in Experience Platform te configureren. Voor een geleidelijke gids bij vestiging de verbinding door UI, verwijs hier naar het [&#x200B; leerprogramma &#x200B;](../../tutorials/ui/create/marketing-automation/sfmc.md). Lees deze zelfstudie voor meer informatie over het verbinden van uw [!DNL Salesforce Marketing Cloud] -account, het selecteren van gegevens, het toewijzen van velden, het plannen van indelingen en het controleren van uw gegevensstromen.
