---
title: SAP - Overzicht van de Bron van de Handel
description: Leer hoe u SAP Commerce met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
last-substantial-update: 2023-07-26T00:00:00Z
badge: Beta
source-git-commit: a848ea11e388678ade780fd81ef3ff6a3477b741
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>De [!DNL SAP Commerce] De bron is in bèta. Zie de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), is een op de cloud gebaseerde oplossing voor e-commerce-platforms voor B2B- en B2C-ondernemingen beschikbaar als onderdeel van het SAP Customer Experience-portfolio. [[!DNL SAP] Abonnementsfacturering](https://www.sap.com/products/financial-management/subscription-billing.html) is een product dat onder de portfolio valt en maakt een volledig levenscyclusbeheer met een abonnement mogelijk met vereenvoudigde verkoop- en betalingservaringen via gestandaardiseerde integratie.

De [!DNL SAP Commerce] bron staat u toe om klanten en contactinformatie in Platform van in te voeren [[!DNL SAP] Abonnementsfacturering](https://www.sap.com/products/financial-management/subscription-billing.html) Onderstaande eindpunten voor de API van zakelijke partners:

* [Klanten](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Contactpersonen](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Bovendien, als [!DNL SAP Commerce] wordt uitgevoerd om klantgegevens op te halen, [Contact opnemen met de klant](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) API wordt ook aangeroepen om de contactgegevens van de klant op te halen.

## IP adres lijst van gewenste personen {#ip-allow-list}

Een lijst van IP adressen kan vereisen om aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Vereisten {#prerequisites}

Voordat u uw [!DNL SAP Commerce] gegevens aan Experience Platform, moet u eerst ervoor zorgen dat u het volgende hebt:

* A [!DNL SAP Subscription Billing] account. Neem contact op met uw [!DNL SAP] accountmanager. Zie de [[!DNL SAP] Configuratie van Platform](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) voor meer informatie.

* [!DNL SAP] servicetoets. De [!DNL SAP] de de dienstsleutel staat u toe om tot [!DNL SAP Subscription Billing] API via Experience Platform. [!DNL SAP Commerce] vereist het volgende:
   * Client-id
   * Clientgeheim
   * URL. Het URL-patroon is als volgt: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Deze waarde wordt later gebruikt om waarden te verkrijgen voor `region` en `tokenEndpoint` wanneer u [Basisverbinding maken](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) met de API of wanneer u [Verbind uw [!DNL SAP Commerce] account](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) via de gebruikersinterface van het Platform.

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

In de onderstaande documentatie vindt u informatie over de verbinding [!DNL SAP Commerce] Platforms met API&#39;s of de gebruikersinterface:

* [Een bronverbinding en gegevensstroom maken voor [!DNL SAP Commerce] gegevens naar Platform met API&#39;s](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [Verbind uw [!DNL SAP Commerce] account aan Experience Platform met behulp van de gebruikersinterface](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [Een gegevensstroom maken voor een bron met behulp van de gebruikersinterface](../../tutorials/ui/dataflow/ecommerce.md)
