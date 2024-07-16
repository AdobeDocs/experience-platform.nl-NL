---
title: SAP Commerce Source - Overzicht
description: Leer hoe u SAP Commerce verbindt met Adobe Experience Platform via API's of de gebruikersinterface.
last-substantial-update: 2023-07-26T00:00:00Z
badge: Beta
exl-id: d2ddfec3-a421-48a7-b765-86ce9162f26f
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>De bron [!DNL SAP Commerce] is in bèta. Zie het [ overzicht van bronnen ](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

[[!DNL SAP Commerce] ](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), is een op wolk-gebaseerde e-commerceplatformoplossing voor B2B en B2C ondernemingen beschikbaar als deel van de portefeuille van de Ervaring van de Klant van SAP. [[!DNL SAP]  het Factureren van het Abonnement 1} is een product onder de portefeuille en laat volledig beheer van de abonnementslevenscyclus met vereenvoudigde het verkopen en betaling ervaringen door gestandaardiseerde integratie toe.](https://www.sap.com/products/financial-management/subscription-billing.html)

De [!DNL SAP Commerce] bron staat u toe om klanten en contactinformatie in Platform van de [[!DNL SAP]  Billing van het Abonnement ](https://www.sap.com/products/financial-management/subscription-billing.html) Onderliggende eindpunten van bedrijfsPartners in te voeren API:

* [ Klanten ](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [ Contacten ](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Bovendien, als [!DNL SAP Commerce] in werking wordt gesteld om klantengegevens terug te winnen, wordt [ klant-Contact Verhoudingen ](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) API ook geroepen om de het contactinformatie van de klant terug te winnen.

## IP adres lijst van gewenste personen {#ip-allow-list}

Een lijst van IP adressen kan vereisen om aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

## Vereisten {#prerequisites}

Voordat u de [!DNL SAP Commerce] -gegevens naar het Experience Platform kunt overbrengen, moet u ervoor zorgen dat:

* Een [!DNL SAP Subscription Billing] account. Neem contact op met uw accountmanager van [!DNL SAP] als u nog geen geldige factureringsaccount hebt. Verwijs naar het [[!DNL SAP]  document van de Configuratie van het Platform ](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) voor extra details.

* [!DNL SAP] -servicetoets. Met de servicetoets [!DNL SAP] hebt u via het Experience Platform toegang tot de API van [!DNL SAP Subscription Billing] . [!DNL SAP Commerce] vereist het volgende:
   * Client-id
   * Clientgeheim
   * URL. Het URL-patroon is als volgt: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Deze waarde zal later worden gebruikt om waarden voor `region` en `tokenEndpoint` te verkrijgen wanneer u [ basisverbinding ](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) creeert gebruikend API of wanneer u [ uw  [!DNL SAP Commerce]  rekening ](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) door Platform UI verbindt.

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

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL SAP Commerce] en Platform via API&#39;s of de gebruikersinterface:

* [ creeer een bronverbinding en dataflow om  [!DNL SAP Commerce]  gegevens aan Platform te brengen gebruikend APIs ](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [ verbind uw  [!DNL SAP Commerce]  rekening met Experience Platform gebruikend UI ](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [Een gegevensstroom maken voor een bron met behulp van de gebruikersinterface](../../tutorials/ui/dataflow/ecommerce.md)
