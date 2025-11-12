---
title: Overzicht van SugarCRM Source
description: Leer hoe u SugarCRM koppelt aan Adobe Experience Platform met behulp van API's of de gebruikersinterface.
last-substantial-update: 2023-08-23T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# [!DNL SugarCRM]

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een CRM-toepassing van derden. Tot de ondersteuning voor CRM-providers behoren [!DNL SugarCRM] .

[[!DNL SugarCRM] &#x200B;](https://www.sugarcrm.com/) is een systeem van het het relatiebeheer van de klant (CRM). De functionaliteit van [!DNL SugarCRM] omvat verkoop-kracht automatisering, marketing campagnes, klantensteun, samenwerking, Mobiele CRM, Sociale CRM en rapportering.

Met de bron [!DNL SugarCRM] kunt u accounts, contactpersonen en gebeurtenisgegevens invoeren vanuit de volgende API-eindpunten:

* [&#x200B; Rekeningen &#x200B;](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [&#x200B; Contacten &#x200B;](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [Gebeurtenissen](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)

[!DNL SugarCRM] gebruikt tokens aan toonder als verificatiemechanisme om te communiceren met de API&#39;s voor accounts van [!DNL SugarCRM] accounts en contactpersonen en de API voor gebeurtenissen van [!DNL SugarCRM] .

## IP adres lijst van gewenste personen

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform aan te sluiten. Voor meer informatie, lees de gids op [&#x200B; voegend op lijst van gewenste personen IP adressen om met Experience Platform &#x200B;](../../ip-address-allow-list.md) voor meer informatie te verbinden.

## Vereisten

Voordat u een [!DNL SugarCRM] -bronverbinding kunt maken, moet u eerst controleren of:

* Een [!DNL SugarMarket] account. Als u nog geen account hebt, moet u contact opnemen met uw [!DNL SugarCRM] -accountmanager om een geldig [!DNL SugarMarket] -account te verkrijgen.

* Een unieke API-gebruikersnaam en -account die los staan van een gebruikersaccount die is gekoppeld aan het marketing- of verkoopproces. Deze unieke gebruikersnaam en accountcombinatie moeten API-toegangsrechten hebben. Voor meer informatie over het proces om een rekening op te zetten, bezoek de [[!DNL SugarMarket RESTFUL API] &#x200B;](https://market.apidocs.sugarcrm.com/#intro) documentatie.

## Verbinden [!DNL SugarCRM Accounts & Contacts] met Experience Platform

* [&#x200B; creeer een bronverbinding om  [!DNL SugarCRM Accounts & Contacts]  gegevens aan Experience Platform te brengen gebruikend APIs &#x200B;](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [&#x200B; creeer een bronverbinding om  [!DNL SugarCRM Accounts & Contacts]  gegevens aan Experience Platform te brengen gebruikend het gebruikersinterface &#x200B;](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [Een gegevensstroom maken voor een CRM-bron met behulp van de Flow Service API](../../tutorials/api/collect/crm.md)


## Verbinden [!DNL SugarCRM Events] met Experience Platform

* [&#x200B; creeer een bronverbinding om  [!DNL SugarCRM Events]  gegevens aan Experience Platform te brengen gebruikend APIs &#x200B;](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [&#x200B; creeer een bronverbinding om  [!DNL SugarCRM Events]  gegevens aan Experience Platform te brengen gebruikend het gebruikersinterface &#x200B;](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Een gegevensstroom maken voor een CRM-bronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/crm.md)
