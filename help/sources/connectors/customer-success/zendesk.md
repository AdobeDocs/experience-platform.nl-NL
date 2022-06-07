---
keywords: Experience Platform;home;populaire onderwerpen;Zendesk;zendesk
solution: Experience Platform
title: Overzicht van Zendesk Source Connector
description: Leer hoe u Zendesk met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: 61b694ca5fbd3548243663b3f1bff06aaca72434
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# (bèta) [!DNL Zendesk]

>[!NOTE]
>
>De [!DNL Zendesk] De bron is in bèta. Zie de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een toepassing voor klantsucces van derden. Tot de ondersteuning voor succesproviders van klanten behoren: [!DNL Zendesk].

Deze Adobe Experience Platform [bronnen](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en) gebruikt de [Zendesk Search API > Export Search Results](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) die gebruikersinformatie van Zendesk voor verdere verwerking in Experience Platform teruggeeft.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Verifieer uw [!DNL Zendesk] account

[!DNL Zendesk] gebruikt dragertokens als authentificatiemechanisme om met het [!DNL Zendesk] API.

In deze sectie worden de vereiste stappen beschreven die moeten worden uitgevoerd om uw [!DNL Zendesk] account.

* De eerste stap bij het verifiëren van uw [!DNL Zendesk] account is om ervoor te zorgen dat je [!DNL Zendesk] ondersteuningsaccount. Als u er nog geen hebt, raadpleegt u de [[!DNL Zendesk] registratiepagina](https://www.zendesk.com/register/) om uw Zendesk-account te registreren en te maken.
* Als u zich hebt geregistreerd, navigeert u naar de [[!DNL Zendesk] website](https://www.zendesk.com/login/) en uw **subdomein**.
* Selecteer vervolgens **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* Ten slotte haalt u uw API-token op van de **[!DNL API token]** sectie.

![Zendesk API-token](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Zie de [[!DNL Zendesk documentation on subdomains]](https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain-) voor informatie over hoe te om uw subdomain terug te winnen. Voor informatie over het genereren van uw API-token raadpleegt u de [[!DNL Zendesk] handleiding voor het genereren van een nieuw API-token](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token).

In de onderstaande documentatie vindt u informatie over het maken van een verbinding [!DNL Zendesk] Platforms met behulp van API&#39;s of de gebruikersinterface:

## Verbinden [!DNL Zendesk] naar Platform met API&#39;s

* [Een bronverbinding en een gegevensstroom maken voor [!DNL Zendesk] de Flow Service API gebruiken](../../tutorials/api/create/customer-success/zendesk.md)

## Verbinden [!DNL Zendesk] naar Platform met behulp van de gebruikersinterface

* [Een [!DNL Zendesk ]bronverbinding in de gebruikersinterface](../../tutorials/ui/create/customer-success/zendesk.md)
* [Maak een gegevensstroom voor een bronverbinding van de klantensucces in UI](../../tutorials/ui/dataflow/customer-success.md)
