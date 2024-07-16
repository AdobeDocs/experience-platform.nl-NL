---
title: Overzicht van Customer.io Source
description: Leer hoe u Customer.io met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface door gebruik te maken van webhaken
badge: Beta
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>De bron [!DNL Customer.io] is in bèta. Gelieve te lezen het [ overzicht van bronnen ](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit streaming toepassingen. Tot de ondersteuning voor streamingproviders behoren [!DNL Customer.io] .

[[!DNL Customer.io] ](https://customer.io/) is een geautomatiseerd overseinenplatform voor marketers die meer controle en flexibiliteit willen om gegeven-gedreven e-mail, dupberichten, in-app berichten, en SMS te groeperen en te verzenden.

De [!DNL Customer.io] bron staat u toe om gesteunde schema&#39;s van de webhaakgebeurtenis en hun bijbehorende gebeurtenisgegevens van [!DNL Customer.io] in te voeren gebruikend [[!DNL Customer.io]  Meldend Webhooks ](https://customer.io/docs/api/webhooks/).

De ondersteunde webhaakgebeurtenisschema&#39;s zijn:

* Gebeurtenissen van klant
* E-mailgebeurtenissen
* SMS-gebeurtenissen
* Gebeurtenissen voor pushmeldingen
* Berichtgebeurtenissen in de app
* Gebeurtenissen Slack
* Webhaakgebeurtenissen

Voor een lijst van gebeurtenissen die door webhooks beschikbaar zijn, gelieve te verwijzen naar de [[!DNL Customer.io]  Meldend de gebeurtenissen van Webhaak ](https://customer.io/docs/webhooks/#events) documentatie.

## Vereisten {#prerequisites}

Voordat u een [!DNL Customer.io] -bronverbinding kunt maken, moet u eerst controleren of:

* Een [!DNL Customer.io] account. Als u niet één hebt lees de [[!DNL Customer.io]  aanmeldingspagina ](https://fly.customer.io/signup) om uw rekening te registreren en tot stand te brengen.
* Nadat u uw account hebt gemaakt, moet u ook uw account laten valideren. Volg de stappen die op de [[!DNL Customer.io]  worden gedocumenteerd de verificatie van de Rekening ](https://customer.io/docs/account-verification/) pagina om het proces te voltooien.

### [!DNL Customer.io] Webhaak instellen {#set-up-webhook}

Zodra u met succes uw gegevensstroom hebt gecreeerd, moet u opstelling een Meldende Webhaak om Platform over [!DNL Customer.io] gebeurtenissen te informeren. Webhooks kunnen u onmiddellijk op de hoogte stellen wanneer de klantkenmerken veranderen of wanneer mensen uw berichten openen, en deze informatie naar uw [!DNL Customer.io] bron verzenden. Voor meer informatie, lees de leerprogramma&#39;s op [ die uw het stromen eindpunt URL ](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) krijgen en [ vestiging a  [!DNL Customer.io]  Webhaak ](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Verbinding maken [!DNL Customer.io] met platform {#connect-to-platform}

In de onderstaande documentatie vindt u informatie over het maken van een [!DNL Customer.io] streaming verbinding met [!DNL Platform] via API&#39;s of de gebruikersinterface:

### Verbinding maken [!DNL Customer.io] met platform met behulp van API&#39;s {#connect-to-platform-using-api}

* [Creeer een bronverbinding en dataflow om  [!DNL Customer.io]  gegevens aan Platform te brengen gebruikend APIs.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Verbinding maken [!DNL Customer.io] met platform via de gebruikersinterface {#connect-to-platform-using-ui}

* [Creeer een bronverbinding en dataflow om  [!DNL Customer.io]  gegevens aan Platform te brengen gebruikend het gebruikersinterface](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
