---
keywords: Experience Platform;home;popular topics;troubleshooting;access control
solution: Experience Platform
title: Handleiding voor probleemoplossing bij toegangsbeheer
topic: troubleshooting guide
description: Dit document bevat antwoorden op veelgestelde vragen over toegangsbeheer in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# Handleiding voor probleemoplossing bij toegangsbeheer

Dit document bevat antwoorden op veelgestelde vragen over toegangsbeheer in Adobe Experience Platform. Voor vragen en het oplossen van problemen met betrekking tot andere [!DNL Platform] diensten, gelieve te verwijzen naar de het oplossen van problemengids [van](../landing/troubleshooting.md)Experience Platforms.

[!DNL Experience Platform] Gebruikt productprofielen in de [Adobe Admin Console](http://adminconsole.adobe.com) om op rol-gebaseerde toegangscontrole te verstrekken, die gebruikers met toestemmingen en zandbakken verbinden.  Zie het [toegangsbeheeroverzicht](home.md) voor meer informatie.

## Waar kan ik mijn huidige toegangstoestemmingen vinden?

Als u een systeembeheerder, productbeheerder of productprofielbeheerder voor uw IMS-organisatie bent, kunt u het toegewezen productprofiel en de machtigingen die het biedt in de Adobe Admin Console bekijken. Zie de gebruikershandleiding voor [toegangsbeheer](./ui/overview.md) voor instructies over het navigeren door het profiel [!DNL Admin Console] om de machtigingen van een productprofiel weer te geven.

Als u geen beheerder bent, kunt u uw huidige toegangstoestemmingen nog bekijken door een verzoek naar het `/acl/effective-policies` eindpunt in de Controle API van de Toegang te verzenden. Zie de sectie van de &quot;van de Mening efficiënte beleid&quot;in de ontwikkelaarsgids [van de](./api/effective-policies.md) toegangscontrole voor meer informatie.

## Sommige functies in de [!DNL Platform] gebruikersinterface zijn niet beschikbaar. Hoe wordt de toegang tot deze eigenschappen gecontroleerd door toestemmingen?

Als u geen toegangstoestemmingen voor een bepaalde [!DNL Platform] eigenschap hebt, zal die eigenschap worden verborgen of grayed-out in [!DNL Experience Platform] UI. Als u bijvoorbeeld het tabblad &quot;[!UICONTROL Profielen]&quot; wilt weergeven, hebt u de machtigingen &quot;[!UICONTROL Profielen]weergeven&quot; of &quot;Profielenbeheren&quot; nodig. Neem contact op met de beheerder als u aanvullende machtigingen voor [!DNL Experience Platform] mogelijkheden nodig hebt.

## Hoe worden de toestemmingen gegroepeerd, en welke groep bevat de toestemming ik wil gebruiken?

Machtigingen worden gegroepeerd en gecategoriseerd op basis van de [!DNL Platform] mogelijkheden waarop ze van toepassing zijn (zoals [!DNL Data Management] en [!DNL Profile Management]). Voor een volledige lijst van beschikbare toestemmingen en de groepen zij tot behoren, zie de [toestemmingensectie](home.md#permissions) in het overzicht van de toegangscontrole.

Zie het overzicht [van de](home.md) toegangscontrole voor meer informatie bij het verstrekken van op rol-gebaseerd toegangsbeheer.