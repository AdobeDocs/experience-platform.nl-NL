---
keywords: Experience Platform;home;populaire onderwerpen;datumbereik
title: Abonneren op Adobe I/O-gebeurtenismeldingen
description: Dit document bevat stappen voor het abonneren op Adobe I/O-gebeurtenismeldingen voor Adobe Experience Platform-services. De informatie van de verwijzing betreffende beschikbare gebeurtenistypen wordt ook verstrekt, samen met verbindingen aan verdere documentatie over hoe te om teruggekeerde gebeurtenisgegevens voor elke toepasselijke  [!DNL Experience Platform]  dienst te interpreteren.
feature: Alerts
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 0%

---

# Abonneren op Adobe I/O-gebeurtenismeldingen

Met [!DNL Observability Insights] kunt u zich abonneren op Adobe I/O-gebeurtenismeldingen met betrekking tot Adobe Experience Platform-activiteiten. Deze gebeurtenissen worden naar een geconfigureerde webhaak verzonden om een efficiënte automatisering van de bewaking van activiteiten te vergemakkelijken.

Dit document bevat stappen voor het abonneren op Adobe I/O-gebeurtenismeldingen voor Adobe Experience Platform-services. Er wordt ook informatie over beschikbare gebeurtenistypen gegeven, samen met koppelingen naar verdere documentatie over hoe u teruggestuurde gebeurtenisgegevens kunt interpreteren voor elke toepasselijke [!DNL Experience Platform] -service.

## Aan de slag

Dit document vereist een goed begrip van webhaken en hoe te om een webhaak van één toepassing aan een andere aan te sluiten. Verwijs naar de [[!DNL I/O Events]  documentatie &#x200B;](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) voor een inleiding aan webhooks.

## Webhaak maken

Als u [!DNL I/O Event] -meldingen wilt ontvangen, moet u een webhaak registreren door een unieke webhaak-URL op te geven als onderdeel van de gegevens voor gebeurtenisregistratie.

U kunt uw webhaak configureren met behulp van de client van uw keuze. Voor een tijdelijk webhaakadres om als deel van dit leerprogramma te gebruiken, bezoek [&#x200B; WebHaak.site &#x200B;](https://webhook.site/) en kopieer unieke verstrekte URL.

![](../images/notifications/webhook-url.png)

Tijdens het eerste validatieproces verzendt [!DNL I/O Events] een query-parameter `challenge` in een GET-aanvraag naar de webhaak. U moet uw webhaak vormen om de waarde van deze parameter in de antwoordlading terug te keren. Als u Webhaak.site gebruikt, selecteert u **[!DNL Edit]** in de rechterbovenhoek en voert u `$request.query.challenge$` onder **[!DNL Response body]** in voordat u **[!DNL Save]** selecteert.

![](../images/notifications/response-challenge.png)

## Een nieuw project maken in Adobe Developer Console

Ga naar [&#x200B; Adobe Developer Console &#x200B;](https://www.adobe.com/go/devs_console_ui) en teken binnen met uw Adobe ID. Daarna, volg de stappen die in het leerprogramma worden geschetst op [&#x200B; creërend een leeg project &#x200B;](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) in de documentatie van Adobe Developer Console.

## Abonneren op gebeurtenissen

>[!NOTE]
>
>De meldingsgebeurtenis voor gegevensinvoer is afgekeurd in Adobe I/O. In plaats daarvan, zou u de **I/O gebeurtenis van de Looppas van de Stroom van 0&rbrace; Bronnen moeten gebruiken.**

Nadat u een nieuw project hebt gemaakt, navigeert u naar het overzichtsscherm van dat project. Selecteer **[!UICONTROL Add event]** van hier.

![](../images/notifications/add-event-button.png)

Er wordt een dialoogvenster weergegeven waarin u een gebeurtenisprovider kunt toevoegen aan uw project:

* Selecteer **[!UICONTROL Platform notifications]** als u zich abonneert op Experience Platform-waarschuwingen
* Selecteer **[!UICONTROL Privacy Service Events]** als u zich abonneert op Adobe Experience Platform [!DNL Privacy Service] -berichten

Wanneer u een gebeurtenisprovider hebt gekozen, selecteert u **[!UICONTROL Next]** .

![](../images/notifications/event-provider.png)

In het volgende scherm wordt een lijst weergegeven met gebeurtenistypen waarop u zich wilt abonneren. Selecteer de gebeurtenissen waarop u zich wilt abonneren en selecteer vervolgens **[!UICONTROL Next]** .

>[!NOTE]
>
>Raadpleeg de volgende documentatie als u niet zeker weet op welke gebeurtenissen u zich moet abonneren voor de service waarmee u werkt:
>
>* [&#x200B; de berichten van het Platform &#x200B;](./rules.md)
>* [&#x200B; de berichten van Privacy Service &#x200B;](../../privacy-service/privacy-events.md)

>[!IMPORTANT]
>
>Waarschuwingen met betrekking tot Edge worden momenteel in bèta weergegeven en zijn alleen beschikbaar voor bepaalde bètaklanten.

![](../images/notifications/choose-event-subscriptions.png)

In het volgende scherm wordt u gevraagd een JSON Web Token (JWT) te maken. U wordt gegeven de optie om een zeer belangrijk paar automatisch te produceren, of uw eigen openbare sleutel te uploaden die in de terminal wordt geproduceerd.

In deze zelfstudie wordt de eerste optie gevolgd. Selecteer het optievak voor **[!UICONTROL Generate a key pair]** en selecteer vervolgens de knop **[!UICONTROL Generate keypair]** in de rechterbenedenhoek.

![](../images/notifications/generate-keypair.png)

Wanneer het sleutelpaar produceert, wordt het automatisch gedownload door browser. U moet dit bestand zelf opslaan omdat het niet in de Developer Console wordt voortgezet.

In het volgende scherm kunt u de details van het nieuwe sleutelpaar bekijken. Selecteer **[!UICONTROL Next]** om door te gaan.

![](../images/notifications/keypair-generated.png)

Geef in het volgende scherm een naam en een beschrijving voor de gebeurtenisregistratie op in de sectie [!UICONTROL Event registration details] . De beste manier is om een unieke, gemakkelijk identificeerbare naam te maken om deze gebeurtenisregistratie te onderscheiden van andere registraties voor hetzelfde project.

![](../images/notifications/registration-details.png)

Verderop op hetzelfde scherm onder de sectie [!UICONTROL How to receive events] kunt u desgewenst configureren hoe gebeurtenissen moeten worden ontvangen. **[!UICONTROL Webhook]** staat u toe om een adres van de douanewebsite te verstrekken om gebeurtenissen te ontvangen, terwijl **[!UICONTROL Runtime action]** u toestaat om het zelfde te doen gebruikend [&#x200B; Adobe I/O Runtime &#x200B;](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

Selecteer **[!UICONTROL Webhook]** voor deze zelfstudie en geef de URL op van de webhaak die u eerder hebt gemaakt. Als u klaar bent, selecteert u **[!UICONTROL Save configured events]** om de gebeurtenisregistratie te voltooien.

![](../images/notifications/receive-events.png)

De detailspagina voor de pas gecreëerde gebeurtenisregistratie verschijnt, waar u zijn configuratie kunt uitgeven, ontvangen gebeurtenissen herzien, zuivert het vinden uitvoeren, en nieuwe gebeurtenisleveranciers toevoegen.

![](../images/notifications/registration-complete.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een webhaak geregistreerd om [!DNL I/O Event] -meldingen voor [!DNL Experience Platform] en/of [!DNL Privacy Service] te ontvangen. Raadpleeg de volgende documentatie voor meer informatie over beschikbare gebeurtenissen en hoe u berichtladingen voor elke service kunt interpreteren:

* [[!DNL Privacy Service] meldingen](../../privacy-service/privacy-events.md)
* [[!DNL Flow Service] (bronnen) meldingen](../../sources/notifications.md)

Zie het [[!DNL Observability Insights]  overzicht &#x200B;](../home.md) voor meer informatie over hoe u uw activiteiten op [!DNL Experience Platform] en [!DNL Privacy Service] kunt controleren.
