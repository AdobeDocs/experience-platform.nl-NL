---
keywords: Experience Platform;home;populaire onderwerpen;problemen oplossen;toegangsbeheer
solution: Experience Platform
title: Handleiding voor probleemoplossing bij toegangsbeheer
description: Dit document bevat antwoorden op veelgestelde vragen over toegangsbeheer in Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Handleiding voor probleemoplossing bij toegangsbeheer

Dit document bevat antwoorden op veelgestelde vragen over toegangsbeheer in Adobe Experience Platform. Voor vragen en het oplossen van problemen met betrekking tot andere [!DNL Experience Platform] diensten, gelieve te verwijzen naar de [ het oplossen van problemengids van Experience Platform ](../landing/troubleshooting.md).

[!DNL Experience Platform] leverages productprofielen in [ Adobe Admin Console ](https://adminconsole.adobe.com) om op rol-gebaseerd toegangsbeheer te verstrekken, die gebruikers met toestemmingen en zandbakken verbinden.  Zie het [ overzicht van de toegangscontrole ](home.md) voor meer informatie.

## Waar kan ik mijn huidige toegangstoestemmingen vinden?

Als u een systeembeheerder, productbeheerder, of product-profielbeheerder voor uw organisatie bent, kunt u uw toegewezen productprofiel en de toestemmingen bekijken het binnen Adobe Admin Console verstrekt. Zie de [ gebruikershandleiding van de toegangscontrole ](./ui/overview.md) voor instructies op hoe te om [!DNL Admin Console] te navigeren om de toestemmingen van een productprofiel te bekijken.

Als u geen beheerder bent, kunt u uw huidige toegangstoestemmingen nog bekijken door een verzoek naar het `/acl/effective-policies` eindpunt in de Controle API van de Toegang te verzenden. Zie de &quot;efficiënte van het beleid van de Mening&quot;sectie in [ de ontwikkelaarsgids van de toegangscontrole ](./api/effective-policies.md) voor meer informatie.

## Sommige functies in de gebruikersinterface van [!DNL Experience Platform] zijn niet beschikbaar. Hoe wordt de toegang tot deze eigenschappen gecontroleerd door toestemmingen?

Als u geen toegangsmachtigingen hebt voor een bepaalde [!DNL Experience Platform] -functie, wordt die functie verborgen of grijs weergegeven in de [!DNL Experience Platform] -gebruikersinterface. Bijvoorbeeld, om &quot;[!UICONTROL Profiles]&quot;tabel te bekijken, moet u of &quot; [!UICONTROL View Profiles]&quot;of &quot;[!UICONTROL Manage Profiles]&quot;toestemmingen hebben. Neem contact op met de beheerder als u aanvullende machtigingen voor [!DNL Experience Platform] -mogelijkheden nodig hebt.

## Hoe worden de toestemmingen gegroepeerd, en welke groep bevat de toestemming ik wil gebruiken?

Machtigingen worden gegroepeerd en gecategoriseerd op basis van de [!DNL Experience Platform] -mogelijkheden waarop ze van toepassing zijn (zoals [!DNL Data Management] en [!DNL Profile Management] ). Voor een volledige lijst van beschikbare toestemmingen en de groepen zij tot behoren, zie de [ sectie van toestemmingen ](home.md#permissions) in het overzicht van de toegangscontrole.

Zie het [ overzicht van de toegangscontrole ](home.md) voor meer informatie bij het verstrekken van op rol-gebaseerd toegangsbeheer.

## Wat gebeurt er met machtigingen na het migreren van Adobe IO naar Business ID?

Het toegangsbeheer gebruikt gebruiker - identiteitskaart (een interne unieke identiteitskaart die aan een gebruiker wordt toegewezen) voor het verlenen van toestemmingen. Wanneer een organisatie van Adobe ID naar bedrijfs-id wordt gemigreerd, gaan alle machtigingen die voor de gebruikers zijn ingesteld, verloren omdat de gebruikers-id wordt gewijzigd en het toegangsbeheer de nieuwe gebruikers-id gebruikt. Als uw organisatie is gemigreerd naar bedrijfs-id, neemt u contact op met uw Adobe-vertegenwoordiger om uw gebruikersnaam te migreren van Adobe ID naar bedrijfs-id.
