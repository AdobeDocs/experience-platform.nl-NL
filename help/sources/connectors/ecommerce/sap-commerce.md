---
title: SAP Commerce Source - Overzicht
description: Leer hoe u SAP Commerce verbindt met Adobe Experience Platform via API's of de gebruikersinterface.
last-substantial-update: 2023-07-26T00:00:00Z
badge: Beta
exl-id: d2ddfec3-a421-48a7-b765-86ce9162f26f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>De bron [!DNL SAP Commerce] is in bèta. Zie het [&#x200B; overzicht van bronnen &#x200B;](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

[[!DNL SAP Commerce] &#x200B;](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), is een op wolk-gebaseerde e-commerceplatformoplossing voor B2B en B2C ondernemingen beschikbaar als deel van de portefeuille van de Ervaring van de Klant van SAP. [[!DNL SAP]  het Factureren van het Abonnement 1&rbrace; is een product onder de portefeuille en laat volledig beheer van de abonnementslevenscyclus met vereenvoudigde het verkopen en betaling ervaringen door gestandaardiseerde integratie toe.](https://www.sap.com/products/financial-management/subscription-billing.html)

De [!DNL SAP Commerce] bron staat u toe om klanten en contactinformatie in Experience Platform van de [[!DNL SAP]  Billing van het Abonnement &#x200B;](https://www.sap.com/products/financial-management/subscription-billing.html) BedrijfsPartners API eindpunten hieronder in te voeren:

* [&#x200B; Klanten &#x200B;](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [&#x200B; Contacten &#x200B;](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Bovendien, als [!DNL SAP Commerce] in werking wordt gesteld om klantengegevens terug te winnen, wordt [&#x200B; klant-Contact Verhoudingen &#x200B;](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) API ook geroepen om de het contactinformatie van de klant terug te winnen.

## IP adres lijst van gewenste personen {#ip-allow-list}

Een lijst van IP adressen kan vereisen om aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [&#128279;](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0&rbrace; IP adres &lbrace;voor meer informatie.

## Vereisten {#prerequisites}

Voordat u uw [!DNL SAP Commerce] -gegevens naar Experience Platform kunt overbrengen, moet u eerst controleren of het volgende mogelijk is:

* Een [!DNL SAP Subscription Billing] account. Neem contact op met uw accountmanager van [!DNL SAP] als u nog geen geldige factureringsaccount hebt. Verwijs naar het [[!DNL SAP]  document van de Configuratie van het Platform &#x200B;](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) voor extra details.

* [!DNL SAP] -servicetoets. Met de servicetoets [!DNL SAP] hebt u via Experience Platform toegang tot de API van [!DNL SAP Subscription Billing] . [!DNL SAP Commerce] vereist het volgende:
   * Client-id
   * Clientgeheim
   * URL. Het URL-patroon is als volgt: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Deze waarde zal later worden gebruikt om waarden voor `region` en `tokenEndpoint` te verkrijgen wanneer u [&#x200B; basisverbinding &#x200B;](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) creeert gebruikend API of wanneer u [&#x200B; uw  [!DNL SAP Commerce]  rekening &#x200B;](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) door Experience Platform UI verbindt.

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

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL SAP Commerce] en Experience Platform via API&#39;s of de gebruikersinterface:

* [&#x200B; creeer een bronverbinding en dataflow om  [!DNL SAP Commerce]  gegevens aan Experience Platform te brengen gebruikend APIs &#x200B;](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [&#x200B; verbind uw  [!DNL SAP Commerce]  rekening met Experience Platform gebruikend UI &#x200B;](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [Een gegevensstroom maken voor een bron met behulp van de gebruikersinterface](../../tutorials/ui/dataflow/ecommerce.md)
