---
keywords: Experience Platform;thuis;populaire onderwerpen;het oplossen van problemen;toegangsbeheer
solution: Experience Platform
title: Handleiding voor probleemoplossing bij toegangsbeheer
topic-legacy: troubleshooting guide
description: Dit document bevat antwoorden op veelgestelde vragen over toegangsbeheer in Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: 79ffdf35e27d74a64ea8e25544fdeeb293b58306
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Handleiding voor probleemoplossing bij toegangsbeheer

Dit document bevat antwoorden op veelgestelde vragen over toegangsbeheer in Adobe Experience Platform. Voor vragen en problemen met betrekking tot andere problemen [!DNL Platform] , raadpleeg de [Handleiding voor het oplossen van problemen met Experience Platforms](../landing/troubleshooting.md).

[!DNL Experience Platform] gebruikt productprofielen in de [Adobe Admin Console](https://adminconsole.adobe.com) om op rol-gebaseerd toegangsbeheer te verstrekken, verbindend gebruikers met toestemmingen en zandbakken.  Zie de [toegangsbeheeroverzicht](home.md) voor meer informatie .

## Waar kan ik mijn huidige toegangstoestemmingen vinden?

Als u een systeembeheerder, productbeheerder of productprofielbeheerder voor uw IMS-organisatie bent, kunt u het toegewezen productprofiel en de machtigingen die het biedt in de Adobe Admin Console bekijken. Zie de [gebruikershandleiding voor toegangsbeheer](./ui/overview.md) voor instructies over hoe te om te navigeren [!DNL Admin Console] om de machtigingen van een productprofiel weer te geven.

Als u geen beheerder bent, kunt u uw huidige toegangstoestemmingen nog bekijken door een verzoek naar te verzenden `/acl/effective-policies` eindpunt in het Toegangsbeheer-API. Zie de sectie &quot;Effectief beleid weergeven&quot; in [toegangsbeheerontwikkelaarsgids](./api/effective-policies.md) voor meer informatie .

## Sommige functies in het dialoogvenster [!DNL Platform] UI is niet beschikbaar. Hoe wordt de toegang tot deze eigenschappen gecontroleerd door toestemmingen?

Als u geen toegangsrechten hebt voor een bepaalde [!DNL Platform] wordt deze functie verborgen of grijs weergegeven in het dialoogvenster [!DNL Experience Platform] UI. Als u bijvoorbeeld &quot;[!UICONTROL Profiles]&quot; tabblad, moet u de &quot;[!UICONTROL View Profiles]&quot; of &quot;[!UICONTROL Manage Profiles]&quot; bevoegdheden. Neem contact op met de beheerder als u aanvullende machtigingen nodig hebt voor [!DNL Experience Platform] mogelijkheden.

## Hoe worden de toestemmingen gegroepeerd, en welke groep bevat de toestemming ik wil gebruiken?

Machtigingen worden gegroepeerd en gecategoriseerd door de [!DNL Platform] mogelijkheden waarop ze van toepassing zijn (zoals [!DNL Data Management] en [!DNL Profile Management]). Voor een volledige lijst van beschikbare toestemmingen en de groepen zij tot behoren, zie [machtigingensectie](home.md#permissions) in het overzicht van het toegangsbeheer.

Zie de [toegangsbeheeroverzicht](home.md) voor meer informatie bij het verstrekken van op rol-gebaseerd toegangsbeheer.

## Wat gebeurt er na het migreren van Adobe IO naar bedrijfs-id?

Het toegangsbeheer gebruikt gebruiker - identiteitskaart (een interne unieke identiteitskaart die aan een gebruiker wordt toegewezen) voor het verlenen van toestemmingen. Wanneer een organisatie van Adobe ID naar bedrijfs-id wordt gemigreerd, gaan alle machtigingen die voor de gebruikers zijn ingesteld, verloren omdat de gebruikers-id wordt gewijzigd en het toegangsbeheer de nieuwe gebruikers-id gebruikt. Als uw organisatie is gemigreerd naar bedrijfs-id, neemt u contact op met uw Adobe-vertegenwoordiger om uw gebruikersnaam te migreren van Adobe ID naar bedrijfs-id.
