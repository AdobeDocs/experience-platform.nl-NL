---
title: Chatlio Source Overview
description: Leer hoe u Chatlio met Adobe Experience Platform kunt verbinden met behulp van API's of de gebruikersinterface door gebruik te maken van webhaken
badge: "Bèta"
source-git-commit: 2c13cb5a951a3144d0047b567194732acdc35dab
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>De [!DNL Chatlio] De bron is in bèta. Lees de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

Experience Platform biedt ondersteuning voor het opnemen van gegevens in streaming toepassingen. Tot de ondersteuning voor streaming providers behoren [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) is een live chat-app die volledig is geïntegreerd met [!DNL Slack] en maakt het mogelijk meerdere ondersteuningsmedewerkers tegelijk te helpen voor een individuele sitebezoeker. [!DNL Chatlio] gebruikt de [!DNL Chatio Zapier App] om verbinding te maken [!DNL Chatlio] met meer dan 2000 verschillende apps en services.

De [!DNL Chatlio] bron staat u toe om gesteunde schema&#39;s van de webhaakgebeurtenis en hun bijbehorende gebeurtenisgegevens van in te voeren [!DNL Chatlio.com] met de [[!DNL Chatlio] Webhaken](https://chatlio.com/docs/webhooks/).

De ondersteunde webhaken zijn:

* Chattranscripties exporteren
* Offlineberichten exporteren
* Het nieuwe gesprek is begonnen
* Bezoeker heeft niet tijdig antwoord gekregen
* Bezoeker heeft feedback gegeven na een chat

## Vereisten {#prerequisites}

Voordat u een [!DNL Chatlio] bronverbinding, moet u eerst ervoor zorgen dat u het volgende hebt:

* A [!DNL Chatlio] account. Als u er nog geen hebt, gaat u naar [[!DNL Chatlio] aanmeldingspagina](https://chatlio.com/app/#/signup) om uw account te registreren en te maken.
* Nadat u een account hebt geregistreerd, volgt u de [[!DNL Chatlio] installatiedocumentatie](https://chatlio.com/docs/setup/) om de accountinstellingen te voltooien.

### Instellen [!DNL Chatlio] webhaak {#set-up-webhook}

Nadat u de gegevensstroom hebt gemaakt, moet u een webhaak instellen om het Platform te informeren over [!DNL Chatlio] gebeurtenissen. Webhooks kunnen u onmiddellijk op de hoogte stellen wanneer de klantkenmerken veranderen of wanneer mensen uw berichten openen en deze gegevens naar uw [!DNL Chatlio] bron.

Lees voor meer informatie de zelfstudies op [ophalen van URL van het streamingeindpunt](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) en [een [!DNL Chatlio] Webhaak](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Verbinden [!DNL Chatlio] naar Platform {#connect-to-platform}

In de onderstaande documentatie vindt u informatie over het maken van een [!DNL Chatlio] streamingconnector voor verbinding met [!DNL Platform] API&#39;s of de gebruikersinterface gebruiken:

### Verbinden [!DNL Chatlio] naar Platform met API&#39;s {#connect-to-platform-using-api}

* [Een bronverbinding maken voor [!DNL Chatlio] gegevens naar Platform met behulp van API&#39;s.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Verbinden [!DNL Chatlio] naar Platform met behulp van de gebruikersinterface {#connect-to-platform-using-ui}

* [Een bronverbinding maken voor [!DNL Chatlio] gegevens naar Platform met behulp van de gebruikersinterface](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)

