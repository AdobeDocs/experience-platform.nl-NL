---
title: Overzicht van de Source Connector van Mixpanel
description: Leer hoe u een verbinding tot stand brengt tussen Mixpanel en Adobe Experience Platform met behulp van API's of de gebruikersinterface.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: 6f8abca8f0db8a559fe62e6c143f2d0506d3b886
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# [!DNL Mixpanel]

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een analyseprogramma van derden. Tot de ondersteuning van analyseproviders behoren: [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) is een hulpprogramma voor productanalyse waarmee u gegevens kunt vastleggen over de manier waarop gebruikers met een digitaal product werken. Met Mixpanel kunt u deze productgegevens analyseren aan de hand van eenvoudige, interactieve rapporten, waarmee u met een paar klikken de gegevens kunt opvragen en visualiseren.

Bronnen gebruiken de [Mixpanel Event Export API > Download](https://developer.mixpanel.com/reference/raw-event-export) om uw gebeurtenisgegevens te downloaden zoals deze worden ontvangen en opgeslagen binnen [!DNL Mixpanel], samen met alle gebeurteniseigenschappen (inclusief `distinct_id`) en de exacte tijdstempel die de gebeurtenis naar het Experience Platform is verzonden. Mixpanel gebruikt tokens aan toonder als verificatiemechanisme om te communiceren met de API voor het exporteren van gebeurtenissen in het Mixpanel.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Verifieer uw [!DNL Mixpanel] account

In deze sectie worden de vereiste stappen beschreven die moeten worden uitgevoerd om uw account te verifiëren en uw account [!DNL Mixpanel] gegevens naar platform.

Om een [!DNL Mixpanel] bronverbinding en gegevensstroom, u moet eerst een geldige [!DNL Mixpanel] account. Als u geen geldige [!DNL Mixpanel] account, zie de [register van Mixpanel](https://mixpanel.com/register/) pagina om uw account te maken.

Als u eenmaal een [!DNL Mixpanel] account, navigeer naar de [!DNL Project Details] in de [!DNL Project Seettings] pagina van de [!DNL Mixpanel] UI om uw projectidentiteitskaart terug te winnen en uw timezone te vormen.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

Navigeer vervolgens naar de [!DNL Service Accounts] in de [!DNL Project Settings] pagina in de [!DNL Mixpanel] UI om uw geloofsbrieven van de de dienstrekening terug te winnen.

>[!TIP]
>
>Voor beste praktijken, selecteer een de dienstrekening die [niet verlopen](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Mixpanel-serviceaccount](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Tot slot creeer een Platform [schema](../../../xdm/schema/composition.md) vereist voor de [!DNL Mixpanel Event Export API]. Voor meer informatie over de afbeeldingen die voor uw schema worden vereist, zie de gids op [een [!DNL Mixpanel] bronverbinding in de gebruikersinterface](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![Schema maken](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Verbinden [!DNL Mixpanel] naar Platform met API&#39;s

In de onderstaande documentatie vindt u informatie over de verbinding [!DNL Mixpanel] naar Platform met API&#39;s of de gebruikersinterface:

* [Een bronverbinding en een gegevensstroom maken voor [!DNL Mixpanel] de Flow Service API gebruiken](../../tutorials/api/create/analytics/mixpanel.md)

## Verbinden [!DNL Mixpanel] naar Platform met behulp van UI

* [Een [!DNL Mixpanel] bronverbinding in de gebruikersinterface](../../tutorials/ui/create/analytics/mixpanel.md)
* [Maak een gegevensstroom voor een bronverbinding van de klantensucces in UI](../../tutorials/ui/dataflow/analytics.md)
