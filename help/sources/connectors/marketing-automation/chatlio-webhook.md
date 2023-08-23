---
title: Chatlio Source Overview
description: Leer hoe u Chatlio met Adobe Experience Platform kunt verbinden met behulp van API's of de gebruikersinterface door gebruik te maken van webhaken
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# [!DNL Chatlio]

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens in streaming toepassingen. Ondersteuning voor streaming providers omvat [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) is een live chat-app die volledig is geïntegreerd met [!DNL Slack] en maakt het mogelijk meerdere ondersteuningsmedewerkers tegelijk te helpen voor een individuele sitebezoeker. [!DNL Chatlio] gebruikt de [!DNL Chatio Zapier App] om verbinding te maken [!DNL Chatlio] met meer dan 2000 verschillende apps en services.

De [!DNL Chatlio] bron staat u toe om gesteunde schema&#39;s van de webhaakgebeurtenis en hun bijbehorende gebeurtenisgegevens van in te voeren [!DNL Chatlio.com] met de [[!DNL Chatlio] Webhaken](https://chatlio.com/docs/webhooks/).

De ondersteunde webhaken zijn:

* Chattranscripties exporteren
* Offlineberichten exporteren
* Het nieuwe gesprek is begonnen
* Bezoeker heeft niet tijdig een antwoord gekregen
* Bezoeker heeft feedback gegeven na een chat

## Vereisten {#prerequisites}

Voordat u een [!DNL Chatlio] bronverbinding, moet u eerst ervoor zorgen dat u het volgende hebt:

* A [!DNL Chatlio] account. Als u er nog geen hebt, gaat u naar [[!DNL Chatlio] aanmeldpagina](https://chatlio.com/app/#/signup) om uw account te registreren en te maken.
* Nadat u een account hebt geregistreerd, volgt u de [[!DNL Chatlio] installatiedocumentatie](https://chatlio.com/docs/setup/) om de accountinstellingen te voltooien.

### Instellen [!DNL Chatlio] webhaak {#set-up-webhook}

Zodra u met succes uw gegevensstroom hebt gecreeerd, moet u opstelling een webhaak om Platform over te informeren [!DNL Chatlio] gebeurtenissen. Webhooks kunnen u onmiddellijk op de hoogte stellen wanneer de klantkenmerken veranderen of wanneer mensen uw berichten openen en deze gegevens naar uw [!DNL Chatlio] bron.

Lees voor meer informatie de zelfstudies op [ophalen van URL van het streamingeindpunt](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) en [een [!DNL Chatlio] Webhaak](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Verbinden [!DNL Chatlio] naar platform {#connect-to-platform}

De onderstaande documentatie bevat informatie over het maken van een [!DNL Chatlio] streamingconnector voor verbinding met [!DNL Platform] API&#39;s of de gebruikersinterface gebruiken:

### Verbinden [!DNL Chatlio] naar Platform met API&#39;s {#connect-to-platform-using-api}

* [Een bronverbinding maken voor [!DNL Chatlio] gegevens naar Platform met API&#39;s.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Verbinden [!DNL Chatlio] naar Platform met behulp van UI {#connect-to-platform-using-ui}

* [Een bronverbinding maken voor [!DNL Chatlio] gegevens aan Platform gebruikend het gebruikersinterface](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
