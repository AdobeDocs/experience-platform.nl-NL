---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor probleemoplossing bij toegangsbeheer
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: c4da32630d3a6476956347b76d611553ef1853fa

---


# Handleiding voor probleemoplossing bij toegangsbeheer

Dit document bevat antwoorden op veelgestelde vragen over toegangsbeheer in het Adobe Experience Platform. Voor vragen en het oplossen van problemen met betrekking tot andere diensten van het Platform, gelieve te verwijzen naar de het oplossen van problemengids [van het Platform van de](../landing/troubleshooting.md)Ervaring.

De ervaring Platform gebruikt productprofielen in de Console [van](http://adminconsole.adobe.com) Adobe Admin om op rol-gebaseerde **toegangscontrole** te verstrekken, die gebruikers met toestemmingen en zandbakken verbindt.  Zie het [toegangsbeheeroverzicht](home.md) voor meer informatie.

## Waar kan ik mijn huidige toegangstoestemmingen vinden?

Als u een systeembeheerder, productbeheerder of productprofielbeheerder voor uw IMS-organisatie bent, kunt u het toegewezen productprofiel en de machtigingen die in de beheerconsole van Adobe zijn opgegeven, bekijken. Zie de gebruikershandleiding voor [toegangsbeheer](./ui/overview.md) voor instructies over het navigeren in de beheerconsole om de machtigingen van een productprofiel weer te geven.

Als u geen beheerder bent, kunt u uw huidige toegangstoestemmingen nog bekijken door een verzoek naar het `/acl/effective-policies` eindpunt in de Controle API van de Toegang te verzenden. Zie de sectie van de &quot;van de Mening efficiënte beleid&quot;in de ontwikkelaarsgids [van de](./api/effective-policies.md) toegangscontrole voor meer informatie.

## Sommige functies in de interface van het platform zijn niet beschikbaar. Hoe wordt de toegang tot deze eigenschappen gecontroleerd door toestemmingen?

Als u geen toegangstoestemmingen voor een bepaalde eigenschap van het Platform hebt, zal die eigenschap worden verborgen of grayed-out in de UI van het Platform van de Ervaring. Als u bijvoorbeeld het tabblad Profielen wilt weergeven, hebt u de machtigingen Profielen weergeven of Profielen beheren nodig. Neem contact op met de beheerder als u aanvullende machtigingen nodig hebt voor de mogelijkheden van het Experience Platform.

## Hoe worden de toestemmingen gegroepeerd, en welke groep bevat de toestemming ik wil gebruiken?

Machtigingen worden gegroepeerd en gecategoriseerd op basis van de platformmogelijkheden waarop ze van toepassing zijn (zoals gegevensbeheer en profielbeheer). Voor een volledige lijst van beschikbare toestemmingen en de groepen zij tot behoren, zie de [toestemmingensectie](home.md#permissions) in het overzicht van de toegangscontrole.

Zie het overzicht [van de](home.md) toegangscontrole voor meer informatie bij het verstrekken van op rol-gebaseerd toegangsbeheer.