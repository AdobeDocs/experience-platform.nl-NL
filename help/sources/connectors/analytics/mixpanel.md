---
title: Overzicht Source Connector Mixpanel
description: Leer hoe u een verbinding tot stand brengt tussen Mixpanel en Adobe Experience Platform met behulp van API's of de gebruikersinterface.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# [!DNL Mixpanel]

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een analysetoepassing van derden. Tot de ondersteuning voor analyseproviders behoren [!DNL Mixpanel] .

[[!DNL Mixpanel] ](https://www.mixpanel.com) is een hulpmiddel van de productanalyse dat u toelaat om gegevens te vangen over hoe de gebruikers met een digitaal product in wisselwerking staan. Met Mixpanel kunt u deze productgegevens analyseren aan de hand van eenvoudige, interactieve rapporten, waarmee u met een paar klikken de gegevens kunt opvragen en visualiseren.

Bronnen gebruiken de [ Uitvoer API van de Gebeurtenis van het Mixpanel > Download ](https://developer.mixpanel.com/reference/raw-event-export) om uw gebeurtenisgegevens te downloaden aangezien het wordt ontvangen en binnen [!DNL Mixpanel], samen met alle gebeurteniseigenschappen (met inbegrip van `distinct_id`) wordt opgeslagen en nauwkeurige timestamp de gebeurtenis werd verzonden naar Experience Platform. Mixpanel gebruikt tokens aan toonder als verificatiemechanisme om te communiceren met de API voor het exporteren van gebeurtenissen in het Mixpanel.

## IP adres lijst van gewenste personen

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform aan te sluiten. Voor meer informatie, lees de gids op [ voegend op lijst van gewenste personen IP adressen om met Experience Platform ](../../ip-address-allow-list.md) voor meer informatie te verbinden.

## Verifieer uw [!DNL Mixpanel] -account

In deze sectie worden de vereiste stappen beschreven die moeten worden uitgevoerd om uw account te verifiëren en uw [!DNL Mixpanel] -gegevens naar Experience Platform te verzenden.

Als u een [!DNL Mixpanel] bronverbinding en gegevensstroom wilt maken, moet u eerst een geldige [!DNL Mixpanel] -account hebben. Als u geen geldige [!DNL Mixpanel] rekening hebt, zie het [ register van Mixpanel ](https://mixpanel.com/register/) pagina om uw rekening tot stand te brengen.

Nadat u een [!DNL Mixpanel] -account hebt gemaakt, navigeert u naar het tabblad [!DNL Project Details] in de pagina [!DNL Project Seettings] van de [!DNL Mixpanel] -gebruikersinterface om uw project-id op te halen en uw tijdzone te configureren.

![ mixpanel-project-montages ](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

Navigeer vervolgens naar het tabblad [!DNL Service Accounts] in de [!DNL Project Settings] -pagina in de [!DNL Mixpanel] -gebruikersinterface om de gegevens van uw serviceaccount op te halen.

>[!TIP]
>
>Voor beste praktijken, selecteer een de dienstrekening die [ niet ](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration) verloopt.

![ de Rekening van de Dienst van Mixpanel ](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Tot slot creeer een Experience Platform [ schema ](../../../xdm/schema/composition.md) dat voor [!DNL Mixpanel Event Export API] wordt vereist. Voor meer informatie over de afbeeldingen die voor uw schema worden vereist, zie de gids bij [ het creëren van a  [!DNL Mixpanel]  bronverbinding in UI ](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![ creeer Schema ](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Verbinding maken [!DNL Mixpanel] met Experience Platform via API&#39;s

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Mixpanel] en Experience Platform via API&#39;s of de gebruikersinterface:

* [Creeer een bronverbinding en een dataflow voor  [!DNL Mixpanel]  gebruikend de Dienst API van de Stroom](../../tutorials/api/create/analytics/mixpanel.md)

## Verbinding maken [!DNL Mixpanel] met Experience Platform via de gebruikersinterface

* [Creeer a [!DNL Mixpanel]  bronverbinding in UI](../../tutorials/ui/create/analytics/mixpanel.md)
* [Maak een gegevensstroom voor een bronverbinding van de klantensucces in UI](../../tutorials/ui/dataflow/analytics.md)
