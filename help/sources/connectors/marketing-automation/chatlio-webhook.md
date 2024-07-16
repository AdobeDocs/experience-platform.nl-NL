---
title: Overzicht van Chatlio Source
description: Leer hoe u Chatlio met Adobe Experience Platform kunt verbinden met behulp van API's of de gebruikersinterface door gebruik te maken van webhaken
badge: Beta
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>De bron [!DNL Chatlio] is in bèta. Gelieve te lezen het [ overzicht van bronnen ](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens in streaming toepassingen. Tot de ondersteuning voor streamingproviders behoren [!DNL Chatlio] .

[[!DNL Chatlio] ](https://chatlio.com/) is een live chat-app die volledig is geïntegreerd met [!DNL Slack] en die meerdere ondersteuningsagents mogelijk maakt om een individuele sitebezoeker tegelijkertijd te helpen. [!DNL Chatlio] gebruikt [!DNL Chatio Zapier App] om verbinding te maken [!DNL Chatlio] met meer dan 2000 verschillende apps en services.

De [!DNL Chatlio] bron staat u toe om gesteunde schema&#39;s van de webhaakgebeurtenis en hun bijbehorende gebeurtenisgegevens van [!DNL Chatlio.com] in te voeren gebruikend [[!DNL Chatlio]  Webhooks ](https://chatlio.com/docs/webhooks/).

De ondersteunde webhaken zijn:

* Chattranscripties exporteren
* Offlineberichten exporteren
* Het nieuwe gesprek is begonnen
* Bezoeker heeft niet tijdig een antwoord gekregen
* Bezoeker heeft feedback gegeven na een chat

## Vereisten {#prerequisites}

Voordat u een [!DNL Chatlio] -bronverbinding kunt maken, moet u eerst controleren of:

* Een [!DNL Chatlio] account. Als u niet één hebt reeds bezoek de [[!DNL Chatlio]  aanmeldingspagina ](https://chatlio.com/app/#/signup) om uw rekening te registreren en tot stand te brengen.
* Nadat u met succes een rekening hebt geregistreerd, volg de [[!DNL Chatlio]  opstellingsdocumentatie ](https://chatlio.com/docs/setup/) om uw rekeningsopstelling te voltooien.

### WebHaak instellen [!DNL Chatlio] {#set-up-webhook}

Nadat u de gegevensstroom hebt gemaakt, moet u een webhaak instellen om Platform op de hoogte te brengen van [!DNL Chatlio] -gebeurtenissen. Webhooks kunnen u onmiddellijk op de hoogte stellen wanneer de klantkenmerken veranderen of wanneer mensen uw berichten openen en deze gegevens naar uw [!DNL Chatlio] -bron verzenden.

Voor meer informatie, lees de leerprogramma&#39;s op [ die uw het stromen eindpunt URL ](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) krijgen en [ vestiging a  [!DNL Chatlio]  Webhaak ](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Verbinden [!DNL Chatlio] met platform {#connect-to-platform}

In de onderstaande documentatie vindt u informatie over het maken van een [!DNL Chatlio] streamingconnector voor verbinding met [!DNL Platform] via API&#39;s of de gebruikersinterface:

### Verbinding maken [!DNL Chatlio] met platform met behulp van API&#39;s {#connect-to-platform-using-api}

* [Creeer een bronverbinding om  [!DNL Chatlio]  gegevens aan Platform te brengen gebruikend APIs.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Verbinding maken [!DNL Chatlio] met platform via de gebruikersinterface {#connect-to-platform-using-ui}

* [Creeer een bronverbinding om  [!DNL Chatlio]  gegevens aan Platform te brengen gebruikend het gebruikersinterface](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
