---
title: Source-overzicht algolieprofielen
description: Meer informatie over de Algoliaanse gebruikersprofielen in de Adobe Experience Platform
last-substantial-update: 2025-04-29T00:00:00Z
exl-id: b35d4753-4c33-4074-9ed5-50f94dedd8a4
source-git-commit: 9bc7d372eba9ffcfe64f90d2d58a532411e5f1ce
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# [!DNL Algolia User Profiles]

[[!DNL Algolia] ](https://www.algolia.com/) is een krachtig onderzoek en ontdekking API platform dat ondernemingen toelaat om snelle, relevante, en klantgerichte onderzoekservaring te leveren. Het biedt zoekmogelijkheden in real time met functies zoals typetolerantie, filteren, faceteren en door AI aangedreven relevantie-tuning. [!DNL Algolia] helpt bedrijven hun betrokkenheid bij gebruikers, conversietarieven en de algehele gebruikerservaring te verbeteren door krachtige zoekoplossingen te bieden voor websites, e-commerceplatforms en toepassingen.

Enkele van de belangrijkste voordelen van [!DNL Algolia] zijn:

* Snel zoeken met snelle resultaten.
* Zeer relevante aanbevelingen van AI.
* Aanpasbare rangschikking om prioriteit te geven aan bedrijfsbehoeften.
* Schaalbaarheid om hoge verkeersbelastingen moeiteloos aan te kunnen.

Voor meer informatie, bezoek de [[!DNL Algolia]  productdocumentatie ](https://resources.algolia.com/).

## Architectuur

Self-Serve Bronnen (Batch SDK) biedt alle noodzakelijke functies, zoals verificatie, paginering of het volledig en gedeeltelijk ophalen van gegevens. De [!DNL Algolia User Profiles] -bron gebruikt deze functies om de integratie te voltooien.

![ Architectuur van de Integratie van Algolië &amp; van Experience Platform ](../../images/tutorials/create/algolia/user-profiles/algolia-aep-user-profiles-arch.png)

## Vereisten {#prerequisites}

U moet de volgende stappen uitvoeren voordat u uw [!DNL Algolia] -account kunt verbinden met Experience Platform.

1. Gebruik het [[!DNL Algolia]  dashboard ](https://dashboard.algolia.com/users/sign_up) aan login aan uw [!DNL Algolia] rekening of creeer een nieuwe rekening.
2. [ bereidt uw Index ](https://www.algolia.com/doc/guides/sending-and-managing-data/prepare-your-data/in-depth/prepare-data-in-depth/) voor.
3. [ opstelling uw facetten ](https://www.algolia.com/doc/guides/managing-results/refine-results/faceting/).
4. [ verzendt gebruikersgebeurtenissen ](https://www.algolia.com/doc/guides/sending-events/getting-started/).
5. [ personaliseer uw Index ](https://www.algolia.com/doc/guides/personalization/advanced-personalization/configure/setup/indices/).

### Machtigingen configureren voor Experience Platform

U moet zowel **[!UICONTROL View Sources]** - als **[!UICONTROL Manage Sources]** -machtigingen hebben ingeschakeld voor uw account om uw [!DNL Algolia] -account te kunnen verbinden met Experience Platform. Neem contact op met de productbeheerder om de benodigde machtigingen te verkrijgen. Voor meer informatie, lees de [ gids UI van de toegangscontrole ](../../../access-control/abac/ui/permissions.md).

### IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het nalaten om uw gebied-specifieke IP adressen aan uw lijst van gewenste personen toe te voegen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [ IP pagina van de lijst van gewenste personen van het adres ](../../ip-address-allow-list.md) voor meer informatie.

## Sluit uw [!DNL Algolia] -account aan op Experience Platform

Zodra u de eerste vereisten hebt voltooid, kunt u aan de volgende stap te werk gaan en [ uw  [!DNL Algolia]  rekening aan Experience Platform ](../../tutorials/ui/create/data-partners/algolia-user-profiles.md) verbinden.
