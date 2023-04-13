---
title: Overzicht bron van SugarCRM
description: Leer hoe u SugarCRM koppelt aan Adobe Experience Platform met behulp van API's of de gebruikersinterface.
badge: Beta
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# (bèta) [!DNL SugarCRM]

>[!NOTE]
>
>De [!DNL SugarCRM] De bron is in bèta. Zie de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een CRM-toepassing van derden. Ondersteuning voor CRM-providers omvat [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) is een systeem van het klantenrelatiebeheer (CRM). [!DNL SugarCRM]Tot de functies van Dell behoren automatisering van verkoopkrachten, marketingcampagnes, klantenondersteuning, samenwerking, Mobile CRM, sociale CRM en rapportage.

De [!DNL SugarCRM] De bron staat u toe om rekeningen, contacten, en gebeurtenisgegevens van de volgende API eindpunten in te voeren:

* [Accounts](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [Contactpersonen](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [Gebeurtenissen](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)


[!DNL SugarCRM] gebruikt dragertokens als authentificatiemechanisme om met het [!DNL SugarCRM] Account en contact-API&#39;s en de [!DNL SugarCRM] Gebeurtenissen-API.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Vereisten

Voordat u een [!DNL SugarCRM] bronverbinding, moet u eerst ervoor zorgen dat u het volgende hebt:

* A [!DNL SugarMarket] account. U moet contact opnemen met uw [!DNL SugarCRM] accountmanager om een geldige [!DNL SugarMarket] account als u er nog geen hebt.

* Een unieke API-gebruikersnaam en -account die los staan van een gebruikersaccount die is gekoppeld aan het marketing- of verkoopproces. Deze unieke gebruikersnaam en accountcombinatie moeten API-toegangsrechten hebben. Ga voor meer informatie over het proces voor het instellen van een account naar de [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro) documentatie.

## Verbinden [!DNL SugarCRM Accounts & Contacts] naar Platform

* [Een bronverbinding maken voor [!DNL SugarCRM Accounts & Contacts] gegevens naar Platform met API&#39;s](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [Een bronverbinding maken voor [!DNL SugarCRM Accounts & Contacts] gegevens naar Platform met behulp van de gebruikersinterface](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [Creeer een dataflow voor een bron van CRM gebruikend de Dienst API van de Stroom](../../tutorials/api/collect/crm.md)


## Verbinden [!DNL SugarCRM Events] naar Platform

* [Een bronverbinding maken voor [!DNL SugarCRM Events] gegevens naar Platform met API&#39;s](../../tutorials/api/create/crm/sugarcrm-events.md).
* [Een bronverbinding maken voor [!DNL SugarCRM Events] gegevens naar Platform met behulp van de gebruikersinterface](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Een gegevensstroom maken voor een CRM-bronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/crm.md)
