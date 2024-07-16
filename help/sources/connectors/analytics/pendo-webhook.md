---
title: Overzicht van Pendo Source
description: Leer hoe u verbinding maakt tussen Pendo en Adobe Experience Platform met behulp van API's of de gebruikersinterface met behulp van webhaken
badge: Beta
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>De bron [!DNL Pendo] is in bèta. Gelieve te lezen het [ overzicht van bronnen ](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een analyseprogramma van derden. Tot de ondersteuning voor analyseproviders behoren [!DNL Pendo] .

[[!DNL Pendo] ](https://pendo.io/) is een product-analytische toepassing die wordt gebouwd om softwarebedrijven te helpen producten ontwikkelen die met klanten resoneren. Met de app kunnen softwareproducenten hun producten insluiten met een groot aantal tools die zowel tot een betere productervaring voor gebruikers als tot nieuwe inzichten voor het productteam kunnen leiden.

De [!DNL Pendo] bron staat u toe om gesteunde schema&#39;s van de webhaakgebeurtenis en hun bijbehorende gebeurtenisgegevens van [!DNL Pendo.io] in te voeren gebruikend [[!DNL Pendo]  Webhooks ](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). De [!DNL Pendo] -bron werkt met [!DNL Pendo] URL-webhaken.

De ondersteunde webhaken zijn:

* [ Gids ](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) Weergegeven
* [ Opiniepeiling ](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) Weergegeven/Voorgelegd
* [ Net Bevorderscore ](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) getoond/voorgelegd

## Vereisten {#prerequisites}

Voordat u een [!DNL Pendo] -bronverbinding kunt maken, moet u eerst controleren of:

Een [!DNL Pendo] account. Als u niet hebt zie reeds de [[!DNL Pendo]  register ](https://app.pendo.io/register) pagina om uw rekening te registreren en tot stand te brengen.

### [!DNL Pendo] Webhaak instellen {#set-up-webhook}

Nadat u de gegevensstroom hebt gemaakt, moet u een webhaak instellen om Platform op de hoogte te brengen van [!DNL Pendo] -gebeurtenissen. [!DNL Pendo] Webhooks kunnen realtime meldingen naar andere services verzenden wanneer bepaalde gebeurtenissen plaatsvinden en deze gegevens naar uw [!DNL Pendo] -bron verzenden. Voor meer informatie, lees de leerprogramma&#39;s op [ die uw het stromen eindpunt URL ](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) krijgen en [ vestiging a  [!DNL Pendo]  Webhaak ](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Verbinding maken [!DNL Pendo] met platform {#connect-to-platform}

In de onderstaande documentatie vindt u informatie over het maken van een [!DNL Pendo] streamingconnector voor verbinding met [!DNL Platform] via API&#39;s of de gebruikersinterface:

### Verbinding maken [!DNL Pendo] met platform met behulp van API&#39;s {#connect-to-platform-using-api}

* [Creeer een bronverbinding om  [!DNL Pendo]  gegevens aan Platform te brengen gebruikend APIs.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Verbinding maken [!DNL Pendo] met platform via de gebruikersinterface {#connect-to-platform-using-ui}

* [Creeer een bronverbinding om  [!DNL Pendo]  gegevens aan Platform te brengen gebruikend het gebruikersinterface](../../tutorials/ui/create/analytics/pendo-webhook.md)
