---
title: Overzicht van SugarCRM Source
description: Leer hoe u SugarCRM koppelt aan Adobe Experience Platform met behulp van API's of de gebruikersinterface.
last-substantial-update: 2023-08-23T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# [!DNL SugarCRM]

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een CRM-toepassing van derden. Tot de ondersteuning voor CRM-providers behoren [!DNL SugarCRM] .

[[!DNL SugarCRM] ](https://www.sugarcrm.com/) is een systeem van het het relatiebeheer van de klant (CRM). De functionaliteit van [!DNL SugarCRM] omvat verkoop-kracht automatisering, marketing campagnes, klantensteun, samenwerking, Mobiele CRM, Sociale CRM en rapportering.

Met de bron [!DNL SugarCRM] kunt u accounts, contactpersonen en gebeurtenisgegevens invoeren vanuit de volgende API-eindpunten:

* [ Rekeningen ](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [ Contacten ](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [Gebeurtenissen](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)

[!DNL SugarCRM] gebruikt tokens aan toonder als verificatiemechanisme om te communiceren met de API&#39;s voor accounts van [!DNL SugarCRM] accounts en contactpersonen en de API voor gebeurtenissen van [!DNL SugarCRM] .

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

## Vereisten

Voordat u een [!DNL SugarCRM] -bronverbinding kunt maken, moet u eerst controleren of:

* Een [!DNL SugarMarket] account. Als u nog geen account hebt, moet u contact opnemen met uw [!DNL SugarCRM] -accountmanager om een geldig [!DNL SugarMarket] -account te verkrijgen.

* Een unieke API-gebruikersnaam en -account die los staan van een gebruikersaccount die is gekoppeld aan het marketing- of verkoopproces. Deze unieke gebruikersnaam en accountcombinatie moeten API-toegangsrechten hebben. Voor meer informatie over het proces om een rekening op te zetten, bezoek de [[!DNL SugarMarket RESTFUL API] ](https://market.apidocs.sugarcrm.com/#intro) documentatie.

## Verbinden [!DNL SugarCRM Accounts & Contacts] met Experience Platform

* [ creeer een bronverbinding om  [!DNL SugarCRM Accounts & Contacts]  gegevens aan Experience Platform te brengen gebruikend APIs ](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [ creeer een bronverbinding om  [!DNL SugarCRM Accounts & Contacts]  gegevens aan Experience Platform te brengen gebruikend het gebruikersinterface ](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [Een gegevensstroom maken voor een CRM-bron met behulp van de Flow Service API](../../tutorials/api/collect/crm.md)


## Verbinden [!DNL SugarCRM Events] met Experience Platform

* [ creeer een bronverbinding om  [!DNL SugarCRM Events]  gegevens aan Experience Platform te brengen gebruikend APIs ](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [ creeer een bronverbinding om  [!DNL SugarCRM Events]  gegevens aan Experience Platform te brengen gebruikend het gebruikersinterface ](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Een gegevensstroom maken voor een CRM-bronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/crm.md)
