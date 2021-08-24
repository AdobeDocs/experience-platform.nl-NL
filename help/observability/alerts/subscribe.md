---
keywords: Experience Platform;home;populaire onderwerpen;datumbereik
title: Abonneren op Adobe I/O-gebeurtenismeldingen
description: Dit document bevat stappen voor het abonneren op Adobe I/O-gebeurtenismeldingen voor Adobe Experience Platform-services. De informatie van de verwijzing betreffende beschikbare gebeurtenistypen wordt ook verstrekt, samen met verbindingen aan verdere documentatie over hoe te om teruggekeerde gebeurtenisgegevens voor elke toepasselijke  [!DNL Platform] dienst te interpreteren.
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: 8c00fb98a213b578f6970c1e1978f0159f8f38df
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# Abonneren op Adobe I/O-gebeurtenismeldingen

[!DNL Observability Insights] Hiermee kunt u zich abonneren op Adobe I/O Event-meldingen met betrekking tot Adobe Experience Platform-activiteiten. Deze gebeurtenissen worden naar een geconfigureerde webhaak verzonden om een efficiënte automatisering van de bewaking van activiteiten te vergemakkelijken.

Dit document bevat stappen voor het abonneren op Adobe I/O-gebeurtenismeldingen voor Adobe Experience Platform-services. Er wordt ook informatie over de beschikbare gebeurtenistypen gegeven, samen met koppelingen naar verdere documentatie over hoe de geretourneerde gebeurtenisgegevens voor elke toepasselijke [!DNL Platform]-service moeten worden geïnterpreteerd.

## Aan de slag

Dit document vereist een goed begrip van webhaken en hoe te om een webhaak van één toepassing aan een andere aan te sluiten. Raadpleeg de [[!DNL I/O Events] documentatie](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) voor een inleiding op websites.

## Webhaak maken

Als u [!DNL I/O Event]-meldingen wilt ontvangen, moet u een webhaak registreren door een unieke webhaak-URL op te geven als onderdeel van de gegevens voor gebeurtenisregistratie.

U kunt uw webhaak configureren met behulp van de client van uw keuze. Voor een tijdelijk webhaakadres dat als onderdeel van deze zelfstudie moet worden gebruikt, gaat u naar [Webhaak.site](https://webhook.site/) en kopieert u de opgegeven unieke URL.

![](../images/notifications/webhook-url.png)

Tijdens het eerste validatieproces verzendt [!DNL I/O Events] een `challenge` vraagparameter in een verzoek van GET naar de webhaak. U moet uw webhaak vormen om de waarde van deze parameter in de antwoordlading terug te keren. Als u Webhaak.site gebruikt, selecteert u **[!DNL Edit]** in de rechterbovenhoek en voert u `$request.query.challenge$` onder **[!DNL Response body]** in voordat u **[!DNL Save]** selecteert.

![](../images/notifications/response-challenge.png)

## Nieuw project maken in Adobe Developer Console

Ga naar [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) en meld u aan met uw Adobe ID. Volg vervolgens de stappen die worden beschreven in de zelfstudie over het maken van een leeg project](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in de documentatie van de Adobe Developer Console.[

## Abonneren op gebeurtenissen

Nadat u een nieuw project hebt gemaakt, navigeert u naar het overzichtsscherm van dat project. Selecteer **[!UICONTROL Add event]**.

![](../images/notifications/add-event-button.png)

Er wordt een dialoogvenster weergegeven waarin u een gebeurtenisprovider kunt toevoegen aan uw project:

* Als u zich abonneert op Experience Platform-waarschuwingen, selecteert u **[!UICONTROL Platform notifications]**
* Als u zich abonneert op Adobe Experience Platform [!DNL Privacy Service]-berichten, selecteert u **[!UICONTROL Privacy Service Events]**

Als u een gebeurtenisprovider hebt gekozen, selecteert u **[!UICONTROL Next]**.

![](../images/notifications/event-provider.png)

In het volgende scherm wordt een lijst weergegeven met gebeurtenistypen waarop u zich wilt abonneren. Selecteer de gebeurtenissen waarop u zich wilt abonneren en selecteer **[!UICONTROL Next]**.

>[!NOTE]
>
>Als u onzeker bent welke gebeurtenissen om aan voor de dienst in te tekenen u met werkt, raadpleeg de dienst-specifieke berichtdocumentatie:
>
>* [[!DNL Privacy Service] meldingen](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] meldingen](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service (sources)] meldingen](../../sources/notifications.md)


![](../images/notifications/choose-event-subscriptions.png)

In het volgende scherm wordt u gevraagd een JSON Web Token (JWT) te maken. U wordt gegeven de optie om een zeer belangrijk paar automatisch te produceren, of uw eigen openbare sleutel te uploaden die in de terminal wordt geproduceerd.

In deze zelfstudie wordt de eerste optie gevolgd. Selecteer het optievak voor **[!UICONTROL Generate a key pair]**, dan selecteer **[!UICONTROL Generate keypair]** knoop in de bodem-juiste hoek.

![](../images/notifications/generate-keypair.png)

Wanneer het sleutelpaar produceert, wordt het automatisch gedownload door browser. U moet dit bestand zelf opslaan omdat het niet wordt voortgezet in de Developer Console.

In het volgende scherm kunt u de details van het nieuwe sleutelpaar bekijken. Selecteer **[!UICONTROL Next]** om door te gaan.

![](../images/notifications/keypair-generated.png)

Geef in het volgende scherm een naam en een beschrijving voor de gebeurtenisregistratie op in de sectie [!UICONTROL Event registration details]. De beste manier is om een unieke, gemakkelijk identificeerbare naam te maken om deze gebeurtenisregistratie te onderscheiden van andere registraties voor hetzelfde project.

![](../images/notifications/registration-details.png)

Verderop op het zelfde scherm onder [!UICONTROL How to receive events] sectie, kunt u naar keuze vormen hoe te om gebeurtenissen te ontvangen. **[!UICONTROL Webhook]** kunt u een aangepast webhaadres opgeven om gebeurtenissen te ontvangen, terwijl u  **[!UICONTROL Runtime action]** dit kunt doen met  [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

Selecteer **[!UICONTROL Webhook]** voor deze zelfstudie en geef de URL op van de webhaak die u eerder hebt gemaakt. Als u klaar bent, selecteert u **[!UICONTROL Save configured events]** om de gebeurtenisregistratie te voltooien.

![](../images/notifications/receive-events.png)

De detailspagina voor de pas gecreëerde gebeurtenisregistratie verschijnt, waar u zijn configuratie kunt uitgeven, ontvangen gebeurtenissen herzien, zuivert het vinden uitvoeren, en nieuwe gebeurtenisleveranciers toevoegen.

![](../images/notifications/registration-complete.png)

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een webhaak geregistreerd om [!DNL I/O Event] berichten voor [!DNL Experience Platform] en/of [!DNL Privacy Service] te ontvangen. Raadpleeg de volgende documentatie voor meer informatie over beschikbare gebeurtenissen en hoe u berichtladingen voor elke service kunt interpreteren:

* [[!DNL Privacy Service] meldingen](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] meldingen](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service] (bronnen) meldingen](../../sources/notifications.md)

Zie [[!DNL Observability Insights] overzicht](../home.md) voor meer informatie over hoe u uw activiteiten kunt controleren op [!DNL Experience Platform] en [!DNL Privacy Service].
