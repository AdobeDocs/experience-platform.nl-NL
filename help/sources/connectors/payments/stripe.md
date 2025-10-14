---
title: Stripe
description: Leer hoe je betalingsgegevens van je Stripe-account kunt opnemen in Adobe Experience Platform
exl-id: 191d217e-036d-491a-b7dd-abcad74625ba
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 0%

---

# [!DNL Stripe]

Duizenden bedrijven van elke omvang gebruiken [!DNL Stripe] zowel online als persoonlijk om betalingen te accepteren, nieuwe inkomstenbronnen te genereren en wereldwijd uit te breiden met behulp van Adobe Experience Platform, Adobe Commerce en [!DNL Magento Open Source] .

Gebruik de [!DNL Stripe] -bron in Experience Platform om gegevens in te voeren die tijdens de aanschafstroom door uw klanten zijn vastgelegd. Zodra geconsumeerd, gebruik deze gegevens om gepersonaliseerde aanbiedingen tot stand te brengen en rijkere bedrijfsinzichten te ontgrendelen.

>[!TIP]
>
>Voor vragen over de [!DNL Stripe] bron op Experience Platform neemt u contact op met [!DNL Stripe] op adobe-partnership <span>@stripe.com.

>[!BEGINSHADEBOX]

**het gebruiksgeval van de Steekproef voor de [!DNL Stripe] bron**

Uw zaken staat klanten toe om punten op uw online opslag met de optie te kopen **nu** en **te betalen later** (gebruikend [!DNL Klarna], [!DNL Afterpay], [!DNL Affirm], of [!DNL Zip]).

Gebruik de [!DNL Stripe] gegevensbron om het gebruik van **te analyseren kopen nu** en **betaal later** opties en met gepersonaliseerde aanbiedingen aan deze klanten experimenteren. Denk bijvoorbeeld aan het aanbevelen van add-on-items om het aantal artikelen in hun winkelwagentje uit te breiden voordat je het winkelwagentje afhandelt.

>[!ENDSHADEBOX]

Lees het onderstaande document voor informatie over hoe u uw [!DNL Stripe] bronaccount kunt instellen, de vereiste gegevens kunt ophalen en uw schema&#39;s kunt maken.

## Vereisten {#prerequisites}

In de volgende secties vindt u informatie over de vereiste instellingen die u moet voltooien voordat u uw [!DNL Stripe] -account kunt verbinden met Experience Platform.

### Uw toegangstoken ophalen

* Login aan het [[!DNL Stripe]  dashboard &#x200B;](https://dashboard.stripe.com/login) gebruikend uw [!DNL Stripe] e-mailadres en wachtwoord.
* Selecteer [!DNL Developers] in het dashboard van **[!DNL API keys for developers]** .
* Onder de **API sleutels** tabel, uitgezochte **[!DNL Reveal test key]** om uw toegangstoken te openbaren.
* U kunt dit token nu gebruiken als toegangstoken wanneer u uw [!DNL Stripe] -account aansluit op Experience Platform met behulp van de [!DNL Flow Service] API of de Experience Platform-gebruikersinterface.

### Vereiste referenties verzamelen

Als u uw [!DNL Stripe] -account wilt verbinden met Experience Platform, moet u waarden opgeven voor de volgende verificatiereferenties:

>[!BEGINTABS]

>[!TAB  API ]

U moet de volgende referenties opgeven wanneer u een verbinding maakt met uw [!DNL Stripe] -account met de [!DNL Flow Service] API.

| Credentials | Beschrijving |
| --- | --- |
| `accessToken` | Uw token voor [!DNL Stripe] OAuth 2-verificatie van code vernieuwen. |
| `connectionSpec.id` | De verbindingsspecificatie-id van de [!DNL Stripe] -bron. Deze id is vast als: `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`. |

>[!TAB  UI ]

U moet de volgende referenties opgeven wanneer u uw [!DNL Stripe] -account aansluit via de Experience Platform-gebruikersinterface.

| Credentials | Beschrijving |
| --- | --- |
| Toegangstoken | Uw token voor [!DNL Stripe] OAuth 2-verificatie van code vernieuwen. |

>[!ENDTABS]

Voor meer informatie bij het gebruiken van [!DNL Stripe] APIs, lees de [[!DNL Stripe]  documentatie over API sleutels &#x200B;](https://docs.stripe.com/keys).

### Een XDM-schema (Experience Data Model) maken

De [!DNL Stripe] -bron ondersteunt het opnemen van gegevens van de volgende bronpaden:

* Heffingen
* Lidmaatschappen
* Restituties
* Transacties balanceren
* Klanten
* Prijzen

U moet een XDM-schema maken om een dataset te beschrijven, waarin de velden en gegevenstypen kunnen worden opgeslagen die van [!DNL Stripe] naar Experience Platform worden verzonden.

>[!BEGINTABS]

>[!TAB  Heffingen ]

In [!DNL Stripe], **laden** vertegenwoordigen pogingen om geld in uw [!DNL Stripe] te bewegen. Lees de [[!DNL Stripe]  API gids op lasten &#x200B;](https://docs.stripe.com/api/charges) voor meer informatie over specifieke ladingsattributen.

+++Selecteren om het Stripe Charge-object weer te geven  

```json
{
  "id": "ch_3MmlLrLkdIwHu7ix0snN0B15",
  "object": "charge",
  "amount": 1099,
  "amount_captured": 1099,
  "amount_refunded": 0,
  "application": null,
  "application_fee": null,
  "application_fee_amount": null,
  "balance_transaction": "txn_3MmlLrLkdIwHu7ix0uke3Ezy",
  "billing_details": {
    "address": {
      "city": null,
      "country": null,
      "line1": null,
      "line2": null,
      "postal_code": null,
      "state": null
    },
    "email": null,
    "name": null,
    "phone": null
  },
  "calculated_statement_descriptor": "Stripe",
  "captured": true,
  "created": 1679090539,
  "currency": "usd",
  "customer": null,
  "description": null,
  "disputed": false,
  "failure_balance_transaction": null,
  "failure_code": null,
  "failure_message": null,
  "fraud_details": {},
  "invoice": null,
  "livemode": false,
  "metadata": {},
  "on_behalf_of": null,
  "outcome": {
    "network_status": "approved_by_network",
    "reason": null,
    "risk_level": "normal",
    "risk_score": 32,
    "seller_message": "Payment complete.",
    "type": "authorized"
  },
  "paid": true,
  "payment_intent": null,
  "payment_method": "card_1MmlLrLkdIwHu7ixIJwEWSNR",
  "payment_method_details": {
    "card": {
      "brand": "visa",
      "checks": {
        "address_line1_check": null,
        "address_postal_code_check": null,
        "cvc_check": null
      },
      "country": "US",
      "exp_month": 3,
      "exp_year": 2024,
      "fingerprint": "mToisGZ01V71BCos",
      "funding": "credit",
      "installments": null,
      "last4": "4242",
      "mandate": null,
      "network": "visa",
      "three_d_secure": null,
      "wallet": null
    },
    "type": "card"
  },
  "receipt_email": null,
  "receipt_number": null,
  "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xTTJKVGtMa2RJd0h1N2l4KOvG06AGMgZfBXyr1aw6LBa9vaaSRWU96d8qBwz9z2J_CObiV_H2-e8RezSK_sw0KISesp4czsOUlVKY",
  "refunded": false,
  "review": null,
  "shipping": null,
  "source_transfer": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": null,
  "transfer_group": null
}
```

+++

>[!TAB  Abonnementen ]

In [!DNL Stripe], kunt u **abonnementen** gebruiken om een klant op een terugkomende basis te laden. Lees de [[!DNL Stripe]  API gids op abonnementen &#x200B;](https://docs.stripe.com/api/subscriptions) voor meer informatie over specifieke abonnementattributen.

+++Selecteren om het Stripe Subscription-object weer te geven

```json
{
  "id": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
  "object": "subscription",
  "application": null,
  "application_fee_percent": null,
  "automatic_tax": {
    "enabled": false,
    "liability": null
  },
  "billing_cycle_anchor": 1679609767,
  "billing_thresholds": null,
  "cancel_at": null,
  "cancel_at_period_end": false,
  "canceled_at": null,
  "cancellation_details": {
    "comment": null,
    "feedback": null,
    "reason": null
  },
  "collection_method": "charge_automatically",
  "created": 1679609767,
  "currency": "usd",
  "current_period_end": 1682288167,
  "current_period_start": 1679609767,
  "customer": "cus_Na6dX7aXxi11N4",
  "days_until_due": null,
  "default_payment_method": null,
  "default_source": null,
  "default_tax_rates": [],
  "description": null,
  "discount": null,
  "ended_at": null,
  "invoice_settings": {
    "issuer": {
      "type": "self"
    }
  },
  "items": {
    "object": "list",
    "data": [
      {
        "id": "si_Na6dzxczY5fwHx",
        "object": "subscription_item",
        "billing_thresholds": null,
        "created": 1679609768,
        "metadata": {},
        "plan": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "plan",
          "active": true,
          "aggregate_usage": null,
          "amount": 1000,
          "amount_decimal": "1000",
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "interval": "month",
          "interval_count": 1,
          "livemode": false,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "tiers_mode": null,
          "transform_usage": null,
          "trial_period_days": null,
          "usage_type": "licensed"
        },
        "price": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "price",
          "active": true,
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "custom_unit_amount": null,
          "livemode": false,
          "lookup_key": null,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "recurring": {
            "aggregate_usage": null,
            "interval": "month",
            "interval_count": 1,
            "trial_period_days": null,
            "usage_type": "licensed"
          },
          "tax_behavior": "unspecified",
          "tiers_mode": null,
          "transform_quantity": null,
          "type": "recurring",
          "unit_amount": 1000,
          "unit_amount_decimal": "1000"
        },
        "quantity": 1,
        "subscription": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
        "tax_rates": []
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/subscription_items?subscription=sub_1MowQVLkdIwHu7ixeRlqHVzs"
  },
  "latest_invoice": "in_1MowQWLkdIwHu7ixuzkSPfKd",
  "livemode": false,
  "metadata": {},
  "next_pending_invoice_item_invoice": null,
  "on_behalf_of": null,
  "pause_collection": null,
  "payment_settings": {
    "payment_method_options": null,
    "payment_method_types": null,
    "save_default_payment_method": "off"
  },
  "pending_invoice_item_interval": null,
  "pending_setup_intent": null,
  "pending_update": null,
  "quantity": 1,
  "schedule": null,
  "start_date": 1679609767,
  "status": "active",
  "test_clock": null,
  "transfer_data": null,
  "trial_end": null,
  "trial_settings": {
    "end_behavior": {
      "missing_payment_method": "create_invoice"
    }
  },
  "trial_start": null
}
```

+++

>[!TAB  Terugbetalingen ]

In [!DNL Stripe], kunt u **terugbetalingen** gebruiken om een eerder gecreeerde last terug te betalen. Lees de [[!DNL Stripe]  API gids over terugbetalingen &#x200B;](https://docs.stripe.com/api/refunds) voor meer informatie over specifieke terugbetalingsattributen.

+++Selecteren om het object Stripe Refund weer te geven

```json
{
  "id": "re_1Nispe2eZvKYlo2Cd31jOCgZ",
  "object": "refund",
  "amount": 1000,
  "balance_transaction": "txn_1Nispe2eZvKYlo2CYezqFhEx",
  "charge": "ch_1NirD82eZvKYlo2CIvbtLWuY",
  "created": 1692942318,
  "currency": "usd",
  "destination_details": {
    "card": {
      "reference": "123456789012",
      "reference_status": "available",
      "reference_type": "acquirer_reference_number",
      "type": "refund"
    },
    "type": "card"
  },
  "metadata": {},
  "payment_intent": "pi_1GszsK2eZvKYlo2CfhZyoZLp",
  "reason": null,
  "receipt_number": null,
  "source_transfer_reversal": null,
  "status": "succeeded",
  "transfer_reversal": null
}
```

+++

>[!TAB  Transacties van het Saldo ]

In [!DNL Stripe], **balanstransacties** vertegenwoordigen de beweging van middelen tussen uw [!DNL Stripe] rekeningen. Lees de [[!DNL Stripe]  API gids op saldotransacties &#x200B;](https://docs.stripe.com/api/balance_transactions) voor meer informatie over specifieke attributen van de saldotransactie.

+++Selecteren om het Stripe Balance Transaction-object weer te geven

```json
{
  "id": "txn_1MiN3gLkdIwHu7ixxapQrznl",
  "object": "balance_transaction",
  "amount": -400,
  "available_on": 1678043844,
  "created": 1678043844,
  "currency": "usd",
  "description": null,
  "exchange_rate": null,
  "fee": 0,
  "fee_details": [],
  "net": -400,
  "reporting_category": "transfer",
  "source": "tr_1MiN3gLkdIwHu7ixNCZvFdgA",
  "status": "available",
  "type": "transfer"
}
```

+++

>[!TAB  Klanten ]

In [!DNL Stripe], **klanten** vertegenwoordigen een bepaalde klant van uw zaken. Voor informatie over specifieke klantenattributen, lees de [[!DNL Stripe]  API gids over klanten &#x200B;](https://docs.stripe.com/api/customers) voor meer informatie over specifieke klantenattributen.

+++Selecteren om het Stripe Customer-object weer te geven

```json
{
  "id": "cus_NffrFeUfNV2Hib",
  "object": "customer",
  "address": null,
  "balance": 0,
  "created": 1680893993,
  "currency": null,
  "default_source": null,
  "delinquent": false,
  "description": null,
  "discount": null,
  "email": "jennyrosen@example.com",
  "invoice_prefix": "0759376C",
  "invoice_settings": {
    "custom_fields": null,
    "default_payment_method": null,
    "footer": null,
    "rendering_options": null
  },
  "livemode": false,
  "metadata": {},
  "name": "Jenny Rosen",
  "next_invoice_sequence": 1,
  "phone": null,
  "preferred_locales": [],
  "shipping": null,
  "tax_exempt": "none",
  "test_clock": null
}
```

+++

>[!TAB  Prijzen ]

In [!DNL Stripe], **prijzen** vertegenwoordigen de eenheidskosten, de munt, en de facultatieve factureringscyclus voor zowel terugkomende als eenmalige aankoop van producten. Lees de [[!DNL Stripe]  API gids op prijzen &#x200B;](https://docs.stripe.com/api/prices) voor meer informatie over specifieke prijsattributen.

+++Selecteren om het object Stripe Price weer te geven

```json
{
  "id": "price_1MoBy5LkdIwHu7ixZhnattbh",
  "object": "price",
  "active": true,
  "billing_scheme": "per_unit",
  "created": 1679431181,
  "currency": "usd",
  "custom_unit_amount": null,
  "livemode": false,
  "lookup_key": null,
  "metadata": {},
  "nickname": null,
  "product": "prod_NZKdYqrwEYx6iK",
  "recurring": {
    "aggregate_usage": null,
    "interval": "month",
    "interval_count": 1,
    "trial_period_days": null,
    "usage_type": "licensed"
  },
  "tax_behavior": "unspecified",
  "tiers_mode": null,
  "transform_quantity": null,
  "type": "recurring",
  "unit_amount": 1000,
  "unit_amount_decimal": "1000"
}
```

+++

>[!ENDTABS]


### IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [&#x200B; pagina van de lijst van gewenste personen van het 0&rbrace; IP adres &lbrace;voor meer informatie.](../../ip-address-allow-list.md)

### Machtigingen configureren voor Experience Platform

U moet zowel **[!UICONTROL View Sources]** - als **[!UICONTROL Manage Sources]** -machtigingen hebben ingeschakeld voor uw account om uw [!DNL Stripe] -account te kunnen verbinden met Experience Platform. Neem contact op met de productbeheerder om de benodigde machtigingen te verkrijgen. Voor meer informatie, lees de [&#x200B; gids UI van de toegangscontrole &#x200B;](../../../access-control/ui/overview.md).

## Volgende stappen

Nadat u aan de voorwaarde hebt voldaan, kunt u doorgaan met het maken van een verbinding en het invoeren van uw [!DNL Stripe] -gegevens naar Experience Platform. Lees de volgende handleidingen voor het invoeren van [!DNL Stripe] -betalingsgegevens naar Experience Platform met behulp van API&#39;s of de gebruikersinterface:

* [&#x200B; voegt betalingsgegevens van uw rekening van Stripe aan Experience Platform toe gebruikend de Dienst API van de Stroom &#x200B;](../../tutorials/api/create/payments/stripe.md).
* [&#x200B; de Gegevens van de Ingest betalingen van uw rekening van Stripe aan Experience Platform gebruikend het gebruikersinterface &#x200B;](../../tutorials/ui/create/payments/stripe.md).
