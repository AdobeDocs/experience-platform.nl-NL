---
title: Overzicht Source Connector Mixpanel
description: Leer hoe u een verbinding tot stand brengt tussen Mixpanel en Adobe Experience Platform met behulp van API's of de gebruikersinterface.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: 6f8abca8f0db8a559fe62e6c143f2d0506d3b886
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# [!DNL Mixpanel]

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een analyseprogramma van derden. Tot de ondersteuning voor analyseproviders behoren [!DNL Mixpanel] .

[[!DNL Mixpanel] ](https://www.mixpanel.com) is een hulpmiddel van de productanalyse dat u toelaat om gegevens te vangen over hoe de gebruikers met een digitaal product in wisselwerking staan. Met Mixpanel kunt u deze productgegevens analyseren aan de hand van eenvoudige, interactieve rapporten, waarmee u met een paar klikken de gegevens kunt opvragen en visualiseren.

Bronnen gebruiken de [ Uitvoer API van de Gebeurtenis van het Mixpanel > Download ](https://developer.mixpanel.com/reference/raw-event-export) om uw gebeurtenisgegevens te downloaden aangezien het binnen [!DNL Mixpanel] wordt ontvangen en opgeslagen, samen met alle gebeurteniseigenschappen (met inbegrip van `distinct_id`) en nauwkeurige timestamp werd de gebeurtenis verzonden naar Experience Platform. Mixpanel gebruikt tokens aan toonder als verificatiemechanisme om te communiceren met de API voor het exporteren van gebeurtenissen in het Mixpanel.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

## Verifieer uw [!DNL Mixpanel] -account

In deze sectie worden de vereiste stappen beschreven die moeten worden uitgevoerd om uw account te verifiëren en uw [!DNL Mixpanel] -gegevens naar het platform te brengen.

Als u een [!DNL Mixpanel] bronverbinding en gegevensstroom wilt maken, moet u eerst een geldige [!DNL Mixpanel] -account hebben. Als u geen geldige [!DNL Mixpanel] rekening hebt, zie het [ register van Mixpanel ](https://mixpanel.com/register/) pagina om uw rekening tot stand te brengen.

Nadat u een [!DNL Mixpanel] -account hebt gemaakt, navigeert u naar het tabblad [!DNL Project Details] in de pagina [!DNL Project Seettings] van de [!DNL Mixpanel] -gebruikersinterface om uw project-id op te halen en uw tijdzone te configureren.

![ mixpanel-project-montages ](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

Navigeer vervolgens naar het tabblad [!DNL Service Accounts] in de [!DNL Project Settings] -pagina in de [!DNL Mixpanel] -gebruikersinterface om de gegevens van uw serviceaccount op te halen.

>[!TIP]
>
>Voor beste praktijken, selecteer een de dienstrekening die [ niet ](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration) verloopt.

![ de Rekening van de Dienst van Mixpanel ](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Tot slot creeer een Platform [ schema ](../../../xdm/schema/composition.md) dat voor [!DNL Mixpanel Event Export API] wordt vereist. Voor meer informatie over de afbeeldingen die voor uw schema worden vereist, zie de gids bij [ het creëren van a  [!DNL Mixpanel]  bronverbinding in UI ](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![ creeer Schema ](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Verbinding maken [!DNL Mixpanel] met platform met behulp van API&#39;s

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Mixpanel] en Platform via API&#39;s of de gebruikersinterface:

* [Creeer een bronverbinding en een dataflow voor  [!DNL Mixpanel]  gebruikend de Dienst API van de Stroom](../../tutorials/api/create/analytics/mixpanel.md)

## Verbinding maken [!DNL Mixpanel] met platform via de gebruikersinterface

* [Creeer a [!DNL Mixpanel]  bronverbinding in UI](../../tutorials/ui/create/analytics/mixpanel.md)
* [Maak een gegevensstroom voor een bronverbinding van de klantensucces in UI](../../tutorials/ui/dataflow/analytics.md)
