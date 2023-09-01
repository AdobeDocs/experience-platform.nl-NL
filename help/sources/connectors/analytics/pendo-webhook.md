---
title: Overzicht van PNO-bron
description: Leer hoe u verbinding maakt tussen Pendo en Adobe Experience Platform met behulp van API's of de gebruikersinterface met behulp van webhaken
badge: Beta
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>De [!DNL Pendo] De bron is in bèta. Lees de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een analyseprogramma van derden. Tot de ondersteuning van analyseproviders behoren: [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) is een product-analytische app die wordt ontwikkeld om softwarebedrijven te helpen producten te ontwikkelen die op klanten reageren. Met de app kunnen softwareproducenten hun producten insluiten met een groot aantal tools die zowel tot een betere productervaring voor gebruikers als tot nieuwe inzichten voor het productteam kunnen leiden.

De [!DNL Pendo] bron staat u toe om gesteunde schema&#39;s van de webhaakgebeurtenis en hun bijbehorende gebeurtenisgegevens van in te voeren [!DNL Pendo.io] met de [[!DNL Pendo] Webhaken](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). De [!DNL Pendo] bron werkt met [!DNL Pendo] URL-webhooks.

De ondersteunde webhaken zijn:

* [Hulplijn](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) Weergegeven
* [Opiniepeiling](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) Weergegeven/verzonden
* [Net Score voor promotor](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) Weergegeven/verzonden

## Vereisten {#prerequisites}

Voordat u een [!DNL Pendo] bronverbinding, moet u eerst ervoor zorgen dat u het volgende hebt:

A [!DNL Pendo] account. Als u er nog geen hebt, raadpleegt u de [[!DNL Pendo] registreren](https://app.pendo.io/register) pagina om uw account te registreren en te maken.

### Instellen [!DNL Pendo] Webhaak {#set-up-webhook}

Zodra u met succes uw gegevensstroom hebt gecreeerd, moet u opstelling een webhaak om Platform over te informeren [!DNL Pendo] gebeurtenissen. [!DNL Pendo] Webhooks kunnen realtime meldingen naar andere services verzenden wanneer bepaalde gebeurtenissen plaatsvinden en deze gegevens naar uw [!DNL Pendo] bron. Lees voor meer informatie de zelfstudies op [ophalen van URL van het streamingeindpunt](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) en [een [!DNL Pendo] Webhaak](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Verbinding maken [!DNL Pendo] naar platform {#connect-to-platform}

De onderstaande documentatie bevat informatie over het maken van een [!DNL Pendo] streamingconnector voor verbinding met [!DNL Platform] API&#39;s of de gebruikersinterface gebruiken:

### Verbinden [!DNL Pendo] naar Platform met API&#39;s {#connect-to-platform-using-api}

* [Een bronverbinding maken voor [!DNL Pendo] gegevens naar Platform met API&#39;s.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Verbinden [!DNL Pendo] naar Platform met behulp van UI {#connect-to-platform-using-ui}

* [Een bronverbinding maken voor [!DNL Pendo] gegevens aan Platform gebruikend het gebruikersinterface](../../tutorials/ui/create/analytics/pendo-webhook.md)
