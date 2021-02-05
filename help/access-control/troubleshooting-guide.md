---
keywords: Experience Platform;thuis;populaire onderwerpen;het oplossen van problemen;toegangsbeheer
solution: Experience Platform
title: Handleiding voor probleemoplossing bij toegangsbeheer
topic: troubleshooting guide
description: Dit document bevat antwoorden op veelgestelde vragen over toegangsbeheer in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# Handleiding voor probleemoplossing bij toegangsbeheer

Dit document bevat antwoorden op veelgestelde vragen over toegangsbeheer in Adobe Experience Platform. Raadpleeg de [handleiding voor het oplossen van Experience Platforms](../landing/troubleshooting.md) voor vragen en het oplossen van problemen met betrekking tot andere [!DNL Platform] services.

[!DNL Experience Platform] Gebruikt productprofielen in de  [Adobe Admin ](http://adminconsole.adobe.com) Consoleto om op rol-gebaseerde toegangscontrole te verstrekken, die gebruikers met toestemmingen en zandbakken verbindt.  Zie [toegangsbeheeroverzicht](home.md) voor meer informatie.

## Waar kan ik mijn huidige toegangstoestemmingen vinden?

Als u een systeembeheerder, productbeheerder of productprofielbeheerder voor uw IMS-organisatie bent, kunt u het toegewezen productprofiel en de machtigingen die het biedt in de Adobe Admin Console bekijken. Zie [toegangsbeheer gebruikershandleiding](./ui/overview.md) voor instructies over hoe te om [!DNL Admin Console] te navigeren om de toestemmingen van een productprofiel te bekijken.

Als u geen beheerder bent, kunt u uw huidige toegangstoestemmingen nog bekijken door een verzoek naar het `/acl/effective-policies` eindpunt in de Controle API van de Toegang te verzenden. Zie de sectie &quot;van de Mening efficiënt beleid&quot;in [de ontwikkelaarsgids ](./api/effective-policies.md) van de toegangscontrole voor meer informatie.

## Sommige functies in de interface [!DNL Platform] zijn niet beschikbaar. Hoe wordt de toegang tot deze eigenschappen gecontroleerd door toestemmingen?

Als u geen toegangstoestemmingen voor een bepaalde [!DNL Platform] eigenschap hebt, zal die eigenschap worden verborgen of grayed-out in [!DNL Experience Platform] UI. Als u bijvoorbeeld het tabblad &quot;[!UICONTROL Profielen]&quot; wilt weergeven, hebt u de machtiging &quot;[!UICONTROL Profielen weergeven]&quot; of &quot;[!UICONTROL Profielen beheren]&quot; nodig. Neem contact op met de beheerder als u aanvullende machtigingen voor [!DNL Experience Platform] mogelijkheden nodig hebt.

## Hoe worden de toestemmingen gegroepeerd, en welke groep bevat de toestemming ik wil gebruiken?

Machtigingen worden gegroepeerd en gecategoriseerd op basis van de [!DNL Platform]-mogelijkheden waarop ze van toepassing zijn (zoals [!DNL Data Management] en [!DNL Profile Management]). Voor een volledige lijst van beschikbare toestemmingen en de groepen zij tot behoren, zie [toestemmingensectie](home.md#permissions) in het overzicht van de toegangscontrole.

Zie [toegangsbeheeroverzicht](home.md) voor meer informatie bij het verstrekken van op rol-gebaseerd toegangsbeheer.