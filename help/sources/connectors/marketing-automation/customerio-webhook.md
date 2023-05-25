---
title: Overzicht van Customer.io-bron
description: Leer hoe u Customer.io met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface door gebruik te maken van webhaken
badge: Beta
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: cfe5f34316e9db072f0a320143354f2771b4a3a9
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>De [!DNL Customer.io] De bron is in bèta. Lees de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit streaming toepassingen. Tot de ondersteuning voor streaming providers behoren [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) is een geautomatiseerd berichtenplatform voor marketers die meer controle en flexibiliteit willen om gegevensgestuurde e-mails, pushberichten, in-app berichten en SMS te verzenden en te verzorgen.

De [!DNL Customer.io] bron staat u toe om gesteunde schema&#39;s van de webhaakgebeurtenis en hun bijbehorende gebeurtenisgegevens van in te voeren [!DNL Customer.io] met de [[!DNL Customer.io] Webhaken melden](https://customer.io/docs/api/webhooks/).

De ondersteunde webhaakgebeurtenisschema&#39;s zijn:

* Gebeurtenissen van klant
* E-mailgebeurtenissen
* SMS-gebeurtenissen
* Gebeurtenissen voor pushmeldingen
* Berichtgebeurtenissen in de app
* Slack Events
* Webhaakgebeurtenissen

Voor een lijst met gebeurtenissen die beschikbaar zijn via webhooks, raadpleegt u de [[!DNL Customer.io] Webhgebeurtenissen melden](https://customer.io/docs/webhooks/#events) documentatie.

## Vereisten {#prerequisites}

Voordat u een [!DNL Customer.io] bronverbinding, moet u eerst ervoor zorgen dat u het volgende hebt:

* A [!DNL Customer.io] account. Als u geen leest, leest u de [[!DNL Customer.io] aanmeldingspagina](https://fly.customer.io/signup) om uw account te registreren en te maken.
* Nadat u uw account hebt gemaakt, moet u ook uw account laten valideren. Voer de stappen uit die op de [[!DNL Customer.io] Accountverificatie](https://customer.io/docs/account-verification/) pagina om het proces te voltooien.

### Instellen [!DNL Customer.io] Webhaak {#set-up-webhook}

Zodra u met succes uw dataflow hebt gecreeerd, moet u opstelling een Meldende Webhaak om Platform over te informeren [!DNL Customer.io] gebeurtenissen. Webhooks kunnen u onmiddellijk op de hoogte stellen wanneer de klantkenmerken veranderen of wanneer mensen uw berichten openen en deze gegevens naar uw [!DNL Customer.io] bron. Lees voor meer informatie de zelfstudies op [ophalen van URL van het streamingeindpunt](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) en [een [!DNL Customer.io] Webhaak](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Verbinding maken [!DNL Customer.io] naar Platform {#connect-to-platform}

In de onderstaande documentatie vindt u informatie over het maken van een [!DNL Customer.io] streamingverbinding voor verbinding met [!DNL Platform] API&#39;s of de gebruikersinterface gebruiken:

### Verbinden [!DNL Customer.io] naar Platform met API&#39;s {#connect-to-platform-using-api}

* [Een bronverbinding en gegevensstroom maken om te zorgen [!DNL Customer.io] gegevens naar Platform met behulp van API&#39;s.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Verbinden [!DNL Customer.io] naar Platform met behulp van de gebruikersinterface {#connect-to-platform-using-ui}

* [Een bronverbinding en gegevensstroom maken om te zorgen [!DNL Customer.io] gegevens naar Platform met behulp van de gebruikersinterface](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
