---
title: Overzicht van Chatlio Source
description: Leer hoe u Chatlio met Adobe Experience Platform kunt verbinden met behulp van API's of de gebruikersinterface door gebruik te maken van webhaken
badge: Beta
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>De bron [!DNL Chatlio] is in bèta. Gelieve te lezen het [&#x200B; overzicht van bronnen &#x200B;](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens in streaming toepassingen. Tot de ondersteuning voor streamingproviders behoren [!DNL Chatlio] .

[[!DNL Chatlio] &#x200B;](https://chatlio.com/) is een live chat-app die volledig is geïntegreerd met [!DNL Slack] en die meerdere ondersteuningsagents mogelijk maakt om een individuele sitebezoeker tegelijkertijd te helpen. [!DNL Chatlio] gebruikt [!DNL Chatio Zapier App] om verbinding te maken [!DNL Chatlio] met meer dan 2000 verschillende apps en services.

De [!DNL Chatlio] bron staat u toe om gesteunde schema&#39;s van de webhaakgebeurtenis en hun bijbehorende gebeurtenisgegevens van [!DNL Chatlio.com] in te voeren gebruikend [[!DNL Chatlio]  Webhooks &#x200B;](https://chatlio.com/docs/webhooks/).

De ondersteunde webhaken zijn:

* Chattranscripties exporteren
* Offlineberichten exporteren
* Het nieuwe gesprek is begonnen
* Bezoeker heeft niet tijdig een antwoord gekregen
* Bezoeker heeft feedback gegeven na een chat

## Vereisten {#prerequisites}

Voordat u een [!DNL Chatlio] -bronverbinding kunt maken, moet u eerst controleren of:

* Een [!DNL Chatlio] account. Als u niet één hebt reeds bezoek de [[!DNL Chatlio]  aanmeldingspagina &#x200B;](https://chatlio.com/app/#/signup) om uw rekening te registreren en tot stand te brengen.
* Nadat u met succes een rekening hebt geregistreerd, volg de [[!DNL Chatlio]  opstellingsdocumentatie &#x200B;](https://chatlio.com/docs/setup/) om uw rekeningsopstelling te voltooien.

### WebHaak instellen [!DNL Chatlio] {#set-up-webhook}

Nadat u de gegevensstroom hebt gemaakt, moet u een webhaak instellen om Experience Platform op de hoogte te brengen van [!DNL Chatlio] -gebeurtenissen. Webhooks kunnen u onmiddellijk op de hoogte stellen wanneer de klantkenmerken veranderen of wanneer mensen uw berichten openen en deze gegevens naar uw [!DNL Chatlio] -bron verzenden.

Voor meer informatie, lees de leerprogramma&#39;s op [&#x200B; die uw het stromen eindpunt URL &#x200B;](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) krijgen en [&#x200B; vestiging a  [!DNL Chatlio]  Webhaak &#x200B;](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Verbinden [!DNL Chatlio] met Experience Platform {#connect-to-platform}

In de onderstaande documentatie vindt u informatie over het maken van een [!DNL Chatlio] streamingconnector voor verbinding met [!DNL Experience Platform] via API&#39;s of de gebruikersinterface:

### Verbinding maken [!DNL Chatlio] met Experience Platform via API&#39;s {#connect-to-platform-using-api}

* [Creeer een bronverbinding om  [!DNL Chatlio]  gegevens aan Experience Platform te brengen gebruikend APIs.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Verbinding maken [!DNL Chatlio] met Experience Platform via de gebruikersinterface {#connect-to-platform-using-ui}

* [Creeer een bronverbinding om  [!DNL Chatlio]  gegevens aan Experience Platform te brengen gebruikend het gebruikersinterface](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
