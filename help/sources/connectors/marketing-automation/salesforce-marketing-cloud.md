---
solution: Experience Platform
title: Bronoverzicht van Salesforce-Marketing Cloud
description: Leer hoe u Salesforce-Marketing Cloud met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: bc37d41d0f7b0ff0cf4d52242f41467f2891d613
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

Experience Platform biedt ondersteuning voor het opnemen van gegevens van derde marketingautomatiseringssystemen. De ondersteuning voor leveranciers van marketingautomatisering omvat: [!DNL Salesforce Marketing Cloud].

## Vereisten

Voordat u verbinding kunt maken met uw [!DNL Salesforce Marketing Cloud] bron aan Platform, moet u ervoor zorgen dat het volgende **machtigingsbereik** zijn ingericht voor uw [!DNL Salesforce Marketing Cloud] combinatie van client-id en clientgeheim:

* `campaign_read`
* `list_and_subscribers_read`

U kunt om werkingsgebied verzoeken door een vraag aan te stellen `v2/userinfo` van de [!DNL Salesforce Marketing Cloud] API. Zie de [[!DNL Salesforce Marketing Cloud] Document met API-integratierechten](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) voor richtsnoeren over het aanvragen en vergelijken van het bereik.

Voor meer informatie over werkingsgebied met inbegrip van een lijst van hun verwante toestemmingen en gedrag, zie dit [[!DNL Salesforce Marketing Cloud] REST API-document](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>Aangepaste objectinvoer wordt momenteel niet ondersteund door de [!DNL Salesforce Marketing Cloud] bronintegratie.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Verbinden [!DNL Salesforce Marketing Cloud] naar Platform met API&#39;s

In de onderstaande documentatie vindt u informatie over het maken van een verbinding [!DNL Salesforce Marketing Cloud] naar Platform met API&#39;s:

* [Een basisverbinding voor een Salesforce-Marketing Cloud maken met de Flow Service API](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
* [Een gegevensstroom maken voor een marketingautomatiseringsbron met behulp van de Flow Service API](../../tutorials/api/collect/marketing-automation.md)

## Verbinden [!DNL Salesforce Marketing Cloud] naar Platform met behulp van de gebruikersinterface

In de onderstaande documentatie vindt u informatie over het maken van een verbinding [!DNL Salesforce Marketing Cloud] Platform met behulp van de gebruikersinterface:

* [Een Salesforce-bronverbinding voor Marketingen Cloud maken in de gebruikersinterface](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Een gegevensstroom maken voor een bronverbinding voor marketingautomatisering in de gebruikersinterface](../../tutorials/ui/dataflow/marketing-automation.md)
