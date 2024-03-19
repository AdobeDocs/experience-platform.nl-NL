---
title: Stripe
description: Leer hoe u betalingsgegevens van uw Stripe-account kunt opnemen in Adobe Experience Platform
badge: Beta
source-git-commit: f8df3ddb96ad0810a7a46b0a55125336c427aebd
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# [!DNL Stripe]

>[!NOTE]
>
>De [!DNL Stripe] De bron is in bèta. Lees de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Duizenden bedrijven van elke omvang gebruiken [!DNL Stripe] zowel online als persoonlijk om betalingen te accepteren, nieuwe inkomstenbronnen te genereren en wereldwijd uit te breiden met behulp van Adobe Experience Platform, Adobe Commerce en [!DNL Magento Open Source].

Gebruik de [!DNL Stripe] bron in Experience Platform voor het opnemen van gegevens die tijdens de aanschafstroom door uw klanten zijn vastgelegd. Zodra geconsumeerd, gebruik deze gegevens om gepersonaliseerde aanbiedingen tot stand te brengen en rijkere bedrijfsinzichten te ontgrendelen.

>[!TIP]
>
>Voor vragen over de [!DNL Stripe] bron op Experience Platform, contact [!DNL Stripe] in adobe-partnership<span>@stripe.com.

>[!BEGINSHADEBOX]

**Voorbeeld van het gebruik van hoofdletters en kleine letters voor de [!DNL Stripe] bron**

Uw bedrijf staat klanten toe om artikelen in uw online winkel te kopen met de optie om **Nu kopen** en **later betalen** (gebruiken [!DNL Klarna], [!DNL Afterpay], [!DNL Affirm], of [!DNL Zip]).

Gebruik de [!DNL Stripe] gegevensbron om het gebruik van **Nu kopen** en **later betalen** en experimenteer met persoonlijke aanbiedingen aan deze klanten. Denk bijvoorbeeld aan het aanbevelen van add-on-items om het aantal artikelen in hun winkelwagentje uit te breiden voordat je het winkelwagentje afhandelt.

>[!ENDSHADEBOX]

Lees het onderstaande document voor meer informatie over het instellen van uw [!DNL Stripe] bronrekening, wint de noodzakelijke geloofsbrieven terug, en creeer uw schema&#39;s.

## Vereisten {#prerequisites}

In de volgende secties vindt u informatie over de vereiste instellingen die u moet voltooien voordat u de verbinding tot stand brengt [!DNL Stripe] aan Experience Platform.

### Uw toegangstoken ophalen

* Aanmelden bij de [[!DNL Stripe] dashboard](https://dashboard.stripe.com/login) met uw [!DNL Stripe] e-mailadres en wachtwoord.
* In de [!DNL Developers] dashboard, selecteren **[!DNL API keys for developers]**.
* Onder de **API-sleutels** tab, selecteert u **[!DNL Reveal test key]** om uw toegangstoken te onthullen.
* U kunt dit token nu gebruiken als toegangstoken wanneer u uw [!DNL Stripe] account aan Experience Platform, met behulp van [!DNL Flow Service] API of de interface van het Experience Platform.

### Vereiste referenties verzamelen

Als u verbinding wilt maken met uw [!DNL Stripe] account aan Experience Platform, moet u waarden opgeven voor de volgende verificatiereferenties:

>[!BEGINTABS]

>[!TAB API]

U moet de volgende referenties opgeven wanneer u verbinding maakt met uw [!DNL Stripe] account gebruiken [!DNL Flow Service] API.

| Credentials | Beschrijving |
| --- | --- |
| `accessToken` | Uw [!DNL Stripe] OAuth 2 het teken van de authentificatie van de Code vernieuwt. |
| `connectionSpec.id` | De verbindingsspecificatie-id van de [!DNL Stripe] bron. Deze id is vast als: `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`. |

>[!TAB UI]

U moet de volgende referenties opgeven wanneer u verbinding maakt met uw [!DNL Stripe] -account die de gebruikersinterface van het Experience Platform gebruikt.

| Credentials | Beschrijving |
| --- | --- |
| Toegangstoken | Uw [!DNL Stripe] OAuth 2 het teken van de authentificatie van de Code vernieuwt. |

>[!ENDTABS]

Voor meer informatie over het gebruik [!DNL Stripe] API&#39;s, lees de [[!DNL Stripe] documentatie over API-sleutels](https://docs.stripe.com/keys).

### Een XDM-schema (Experience Data Model) maken

De [!DNL Stripe] de bron steunt opname van gegevens van de volgende middelwegen:

* Heffingen
* Lidmaatschappen
* Restituties
* Transacties balanceren
* Klanten
* Prijzen

U moet een schema XDM creëren om een dataset te beschrijven, die de gebieden en gegevenstypes kan opslaan die van zullen worden verzonden [!DNL Stripe] naar Experience Platform.

>[!BEGINTABS]

>[!TAB Heffingen]

In [!DNL Stripe], **kosten** pogingen vertegenwoordigen om geld naar uw [!DNL Stripe]. Lees de [[!DNL Stripe] API-handleiding voor kosten](https://docs.stripe.com/api/charges) voor meer informatie over specifieke ladingskenmerken.

+++Selecteren om het object Stripe laden weer te geven

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

>[!TAB Abonnementen]

In [!DNL Stripe]kunt u **abonnementen** een klant op terugkerende basis in rekening brengen. Lees de [[!DNL Stripe] API-handleiding voor abonnementen](https://docs.stripe.com/api/subscriptions) voor meer informatie over specifieke abonnementskenmerken.

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

>[!TAB Restituties]

In [!DNL Stripe]kunt u **restituties** om eerder gemaakte kosten te betalen. Lees de [[!DNL Stripe] API-handleiding voor terugbetalingen](https://docs.stripe.com/api/refunds) voor meer informatie over specifieke terugbetalingskenmerken.

+++Selecteren om het object Stripe terugbetalen weer te geven

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

>[!TAB Transacties balanceren]

In [!DNL Stripe], **saldotransacties** vertegenwoordigen de bewegingen van middelen tussen uw [!DNL Stripe] rekeningen. Lees de [[!DNL Stripe] API-handleiding voor balanstransacties](https://docs.stripe.com/api/balance_transactions) voor meer informatie over specifieke kenmerken van balanstransacties.

+++Selecteren om het Transactie-object Stripe balanceren weer te geven

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

>[!TAB Klanten]

In [!DNL Stripe], **klanten** vertegenwoordigen een bepaalde klant van uw zaken. Voor meer informatie over specifieke klantkenmerken leest u de [[!DNL Stripe] API-handleiding voor klanten](https://docs.stripe.com/api/customers) voor meer informatie over specifieke klantkenmerken.

+++Selecteren om het Stripe Customer object te bekijken

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

>[!TAB Prijzen]

In [!DNL Stripe], **prijzen** vertegenwoordigen de kosten per eenheid, de valuta en de optionele factureringscyclus voor zowel terugkerende als eenmalige aanschaf van producten. Lees de [[!DNL Stripe] API-handleiding voor prijzen](https://docs.stripe.com/api/prices) voor meer informatie over specifieke prijskenmerken.

+++Selecteren om het Stripe Price-object weer te geven

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

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

### Machtigingen configureren voor Experience Platform

U moet beide hebben **[!UICONTROL View Sources]** en **[!UICONTROL Manage Sources]** machtigingen die zijn ingeschakeld voor uw account om verbinding te maken met uw [!DNL Stripe] aan Experience Platform. Neem contact op met de productbeheerder om de benodigde machtigingen te verkrijgen. Lees voor meer informatie de [gebruikershandleiding voor toegangsbeheer](../../../access-control/ui/overview.md).

## Volgende stappen

Nadat u de vereiste instellingen hebt voltooid, kunt u verdergaan met de verbinding en uw [!DNL Stripe] gegevens naar Experience Platform. Lees de volgende hulplijnen voor meer informatie over innemen [!DNL Stripe] betalingsgegevens naar Experience Platform via API&#39;s of de gebruikersinterface:

* [Betalingsgegevens vanuit uw Stripe-account aan Experience Platform toevoegen met behulp van de Flow Service API](../../tutorials/api/create/payments/stripe.md).
* [Betalingsgegevens van uw Stripe naar Experience Platform verzenden via de gebruikersinterface](../../tutorials/ui/create/payments/stripe.md).