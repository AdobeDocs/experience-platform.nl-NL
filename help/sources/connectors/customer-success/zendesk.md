---
title: Overzicht van Zendesk Source Connector
description: Leer hoe u Zendesk met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# [!DNL Zendesk]

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een toepassing voor klantsucces van derden. Tot de ondersteuning voor succesproviders van klanten behoren [!DNL Zendesk] .

Deze Adobe Experience Platform [ bronnen ](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=nl) hefboomwerkingen [ het Onderzoek API van Zendesk > de Resultaten van het Onderzoek van de Uitvoer ](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) die gebruikersinformatie in Experience Platform van Zendesk voor verdere verwerking terugkeert.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

## Verifieer uw [!DNL Zendesk] -account

[!DNL Zendesk] gebruikt tokens aan toonder als verificatiemechanisme om te communiceren met de [!DNL Zendesk] -API.

In deze sectie worden de vereiste stappen beschreven die moeten worden uitgevoerd om uw [!DNL Zendesk] -account te verifiëren.

* De eerste stap bij het verifiëren van uw [!DNL Zendesk] -account is ervoor te zorgen dat u over een [!DNL Zendesk] -ondersteuningsaccount beschikt. Als u niet hebt zie reeds de [[!DNL Zendesk]  registratiepagina ](https://www.zendesk.com/register/) om uw rekening van Zendesk te registreren en tot stand te brengen.
* Zodra u met succes hebt geregistreerd, navigeer aan de [[!DNL Zendesk]  website ](https://www.zendesk.com/login/) en verstrek uw **subdomain**.
* Selecteer vervolgens **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]** .
* Ten slotte haalt u uw API-token op uit de sectie **[!DNL API token]** .

![ het teken van Zendesk API ](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Zie [[!DNL Zendesk documentation on subdomains] ](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->) voor informatie over hoe te om uw subdomain terug te winnen. Voor informatie bij het produceren van uw API teken, zie de [[!DNL Zendesk]  gids bij het produceren van een nieuw API teken ](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>).

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Zendesk] en Experience Platform via API&#39;s of de gebruikersinterface:

## Verbinding maken [!DNL Zendesk] met Experience Platform via API&#39;s

* [Creeer een bronverbinding en een dataflow voor  [!DNL Zendesk]  gebruikend de Dienst API van de Stroom](../../tutorials/api/create/customer-success/zendesk.md)

## Verbinding maken [!DNL Zendesk] met Experience Platform via de gebruikersinterface

* [Creeer a [!DNL Zendesk ] bronverbinding in UI](../../tutorials/ui/create/customer-success/zendesk.md)
* [Maak een gegevensstroom voor een bronverbinding van de klantensucces in UI](../../tutorials/ui/dataflow/customer-success.md)
