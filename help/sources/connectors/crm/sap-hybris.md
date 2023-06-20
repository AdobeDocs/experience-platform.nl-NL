---
title: Overzicht van bron van SAP-hybride
description: Leer hoe u SAP Hybris met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 32e2c13dcdbf2f13b4025354dfc50f5ccaf5f664
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---

# [!DNL SAP Hybris]

>[!NOTE]
>
>De [!DNL SAP Hybris] De bron is in bèta. Zie de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

[[!DNL SAP Hybris]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), is een op de cloud gebaseerde oplossing voor e-commerce-platforms voor B2B- en B2C-ondernemingen beschikbaar als onderdeel van het SAP Customer Experience-portfolio. [[!DNL SAP] Abonnementsfacturering](https://www.sap.com/products/financial-management/subscription-billing.html) is een product dat onder de portfolio valt en maakt een volledig levenscyclusbeheer met een abonnement mogelijk met vereenvoudigde verkoop- en betalingservaringen via gestandaardiseerde integratie.

De [!DNL SAP Hybris] bron staat u toe om klanten en contactinformatie in Platform van in te voeren [[!DNL SAP] Abonnementsfacturering](https://www.sap.com/products/financial-management/subscription-billing.html) Onderstaande eindpunten voor de API van zakelijke partners:

* [Klanten](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Contactpersonen](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Bovendien, als [!DNL SAP Hybris] wordt uitgevoerd om klantgegevens op te halen, [Contact opnemen met de klant](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) API wordt ook aangeroepen om de contactgegevens van de klant op te halen.

## IP adres lijst van gewenste personen {#ip-allow-list}

Een lijst van IP adressen kan vereisen om aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Vereisten {#prerequisites}

Voordat u uw [!DNL SAP Hybris] gegevens aan Experience Platform, moet u eerst ervoor zorgen dat u het volgende hebt:

* A [!DNL SAP Subscription Billing] account. Neem contact op met uw [!DNL SAP] accountmanager. Zie de [[!DNL SAP] Configuratie van Platform](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) voor meer informatie.

* [!DNL SAP] servicesleutel. De [!DNL SAP] de de dienstsleutel staat u toe om tot [!DNL SAP Subscription Billing] API via Experience Platform. [!DNL SAP Hybris] vereist het volgende:
   * Client-id
   * Clientgeheim
   * URL. Het URL-patroon is als volgt: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Deze waarde wordt later gebruikt om waarden te verkrijgen voor `region` en `tokenEndpoint` wanneer u [Basisverbinding maken](../../tutorials/api/create/crm/sap-hybris.md#base-connection) met de API of wanneer u [Verbind uw [!DNL SAP Hybris] account](../../tutorials/ui/create/crm/sap-hybris.md#connect-account) via de gebruikersinterface van het Platform.

+++Select om een voorbeeld van de de dienstsleutel te zien

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

## Volgende stappen

In de onderstaande documentatie vindt u informatie over het maken van een verbinding [!DNL SAP Hybris] Platforms met behulp van API&#39;s of de gebruikersinterface:

* [Een bronverbinding en gegevensstroom maken om te zorgen [!DNL SAP Hybris] gegevens naar Platform met API&#39;s](../../tutorials/api/create/crm/sap-hybris.md).
* [Verbind uw [!DNL SAP Hybris] account aan Experience Platform met behulp van de gebruikersinterface](../../tutorials/ui/create/crm/sap-hybris.md).
* [Creeer een dataflow voor een bron van CRM gebruikend UI](../../tutorials/ui/dataflow/crm.md)
